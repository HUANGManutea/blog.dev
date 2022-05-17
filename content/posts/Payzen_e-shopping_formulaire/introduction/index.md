---
title: "Payzen e-shopping formulaire - Introduction"
date: 2022-05-07T21:26:05-10:00
draft: false
tags: [Payzen, Web]
categories: [Tutoriel]
---

# Introduction

Dans cette série d'articles nous verrons ensemble comment implémenter Payzen By OSB dans une application web fullstack d'e-shopping basique.

Une liste de produits, accompagnés de leur prix, sera affichée,. L'utilisateur pourra acheter un produit.

Afin d'avoir une meilleure idée de l'architecture finale de l'application, nous allons tout d'abord expliquer Payzen By OSB, que j'appellerai Payzen pour aller plus vite.

Note:

Je ne vais pas créer de bases de données pour les produits et l'inventaire, ni pour la gestion des clients. Nous allons nous concentrer sur le paiement. Par la suite vous pourrez de vous-même brancher ce paiement à vos services de commande et de gestion client.

# Présentation de Payzen

Payzen est une plateforme permettant de payer avec [différentes cartes](https://secure.osb.pf/doc/fr-FR/form-payment/standard-payment/vads-payment-cards.html), de plusieurs manières différentes:

- API formulaire de redirection (avec ou sans iFrame)
- API REST
- dépôt de fichier

Note: **A l'heure actuelle, il n'est pas possible de payer avec une carte privative avec l'API REST**, une livraison est en cours pour débloquer cette situation.

La méthode la plus répandue est d'utiliser l'API formulaire de redirection. Elle va nous permettre de générer un formulaire qui pourra par la suite être intégré directement dans l'application via une iFrame, ou d'envoyer au client, par SMS ou par email, un lien vers ce formulaire.

Dans cette série d'articles, nous allons implémenter le formulaire de redirection via iFrame, c'est d'ailleurs ce que font les modules d'intégrations Payzen dans les CMS.

Pour préparer notre implémentation, nous devons récupérer notre **identifiant boutique** ainsi que notre **clé d'API formulaire**, vous pouvez vous référer à [cette documentation](https://secure.osb.pf/doc/fr-FR/form-payment/standard-payment/s-identifier-lors-des-echanges.html), je vous conseille de télécharger la documentation au format PDF pour faciliter les recherches.

Pour ma part, je vais utiliser ces informations de test:

>identifiant boutique: 12345678
>
>clé d'API: 1122334455667788

# Architecture

La documentation de Payzen nous informe que nous avons besoin de la clé d'API, associée au bon identifiant boutique, afin de calculer la signature. En effet, c'est la signature qui permet de vérifier que c'est bien votre application qui envoie une commande.

Nous allons forcément faire un frontend, mais nous ne voulons **surtout pas** stocker la clé d'API dans le frontend. Pour cela nous aurons besoin d'un backend que nous appellerons pour calculer la signature à chaque création de formulaire.

Notre architecture finale devrait ressembler à ceci:

![Architecture](payzen-e-shopping-architecture.png#center "Architecture")

Et le diagramme de séquence:

![Diagramme de séquence](payzen-e-shopping-sequence.png#center "Diagramme de séquence")

La cinématique étant la suivante:
- l'utilisateur clique sur un bouton pour payer,
- le front envoie les données de paiement au back pour récupérer le calcul de la signature du formulaire,
- une fois la signature reçue, le front envoie les données de paiement + la signature à secure.osb.pf qui est la plateforme de paiement de Payzen,
- la plateforme de paiement vérifie la signature, et retourne le formulaire,
- l'utilisateur pourra ensuite renseigner ses informations de carte dans le formulaire et valider,
- enfin, la plateforme de paiement retournera un résultat OK ou KO, qui redirigera l'utilisateur sur la page /success ou /fail du front.

Concernant la stack technologique, nous allons utiliser:

- [Node.js](https://nodejs.org/en/) pour le backend,
- [Next.js](https://nextjs.org/) pour le frontend, avec la librairie [PayzenJS](https://www.npmjs.com/package/PayzenJS) qui permettra d'intégrer facilement l'iFrame dans notre frontend.

Notes:

Avec Next.js il est tout à fait possible de placer le calcul de la signature dans *pages/api*, mais je préfère créer un backend dédié car certains parmi vous ont peut-être un microservice dédié au paiement.

# Structure des articles

Les articles ne seront pas séparés en frontend et backend. D'un point de vue gestion de projet, il me paraît plus logique de développer le back et le front en même temps pour une feature.

Je structurerai chaque fonctionnalité par une ou plusieurs User Stories, pour ceux qui connaissent la méthode Scrum.

# Initialisation du projet

```bash
# créer le dossier
mkdir tutorial-payzen-e-shopping
cd tutorial-payzen-e-shopping
```

## Initialisation du backend

Initialiser le projet backend avec npm

```bash
mkdir backend
cd backend
npm init
>package name: (backend) tutorial-payzen-e-shopping-back
>version: (1.0.0)
>description: backend du tutoriel payzen e-shopping
>entry point: (index.js) main.js
>test command:
>git repository:
>keywords:
>author: HUANG Manutea
>license: (ISC) MIT
```

Rajouter les dépendances utiles dans le package.json, ainsi que le script start:

```bash
"scripts": {
  ...,
  "start": "node main.js"
},
"dependencies": {
  "express": "4.17.2",    # serveur
  "cors": "2.8.5",        # middleware CORS
  "crypto-js": "4.1.1",   # librairie de cryptographie
  "dotenv": "16.0.0"      # librairie de lecture du fichier .env qui contiendra notre clé d'API
},
```

Lancer l'installation

```bash
npm install
```
Créer le fichier main.js

```javascript
// main.js
// modules serveur
const express = require("express");

const app = express();
const port = 3001;

app.post("/sign", (req, res) => {
  res.send("hello world!");
});

app.listen(port, () => {
  console.log(`Payzen e-shopping backend server listening on port ${port}`);
});
```
lancer le serveur

```bash
npm start
```

Dans un autre terminal, lancer curl

```bash
curl -X POST http://localhost:3001/sign
>hello world!
```

## Initialisation du frontend

Créer le projet frontend avec npx:

```bash
# retourner à la racine du projet
cd ..
# créer le projet
npx create-next-app frontend --use-npm --example "https://github.com/vercel/next-learn/tree/master/basics/learn-starter"
```

Lancer le front en mode développement

```bash
cd frontend
npm run dev
```

En utilisant un navigateur, allez à [http://localhost:3000](http://localhost:3000).

# Conclusion

Nous avons parcouru la documentation de Payzen. Cette documentation nous a indiqué comment récupérer les informations importantes d'identifiant boutique et de clé d'API.

Elle nous a également informé que pour générer un formulaire, la plateforme de paiement a besoin d'une signature permettant de signer la requête de création de formulaire.

De ce fait, nous avons conçu une architecture backend/frontend et nous les avons initialisé.

Par la suite, nous allons implémenter les fonctionnalités nécessaires à notre application web d'e-shopping.