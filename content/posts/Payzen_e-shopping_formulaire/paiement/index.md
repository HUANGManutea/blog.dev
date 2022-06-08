---
title: "Payzen e-shopping formulaire - Paiement"
date: 2022-05-21T22:31:25-10:00
draft: false
---
Cet article fait partie d'une suite de tutoriels d'intégration Payzen dans une application web d'e-shopping. Vous trouverez le précédent article [ici](https://huangmanutea.github.io/blog.dev/posts/payzen_e-shopping_formulaire/inventaire/).

# Introduction

Après voir créé l'inventaire, nous allons maintenant implémenter le paiement, et plus particulièrement le [paiement comptant immédiat](https://secure.osb.pf/doc/fr-FR/form-payment/standard-payment/creer-un-paiement-comptant-immediat.html).

# User Story

1. En tant qu'**utilisateur**
2. Je veux **payer le produit sélectionné**
3. Afin de **créer une commande**


# Déroulement

Pour faire ce paiement, nous utilisons la librairie [PayzenJS](https://www.npmjs.com/package/PayzenJS).

La documentation de cette librairie nous indique que nous devons signer notre requête de génération de formulaire via une requête POST vers un backend, ce qui coïncide avec la documentation Payzen de paiement comptant immédiat.

![signature](payzenjs_signature.png#center "signature")

Nous allons donc tout d'abord créer un formulaire dans notre frontend, puis nous passerons les valeurs des champs dans la propriété *orderData* de la librarie.

Ensuite nous implémenterons la génération de signature dans le backend, pour enfin renseigner l'url de l'endpoint dans la propriété *credentials* de la librairie.

Nous renseignerons également la propriété *target* comme étant égale à **secure.osb.pf**, afin d'utiliser la plateforme spécifique à OSB, car c'est celle-ci qui ***accepte les cartes privatives***.

Enfin, nous renseignerons la propriété *canvas*, qui contiendra l'iframe contenant le formulaire de paiement final.

La librarie s'occupera de faire la requête POST vers le backend, de récupérer la signature, d'envoyer la requêté signée à la plateforme, et enfin d'afficher le formulaire dans l'iframe.

# Frontend

## Item

Dans un premier temps, modifions notre composant *Item* comme suit :

```react
// components/item.js
export default function Item({item, buy}) {

  return (
    <div className="bg-white shadow overflow-hidden sm:rounded-lg hover:opacity-75">
      <div className="flex flex-col p-4 border-b border-gray-200">
        <div className="flex flex-row gap-1">
          <h2>Name:</h2>
          <p>{item.name}</p>
        </div>
        <div className="flex flex-row gap-1">
          <h2>Price:</h2>
          <p>{item.price} <span>XPF</span></p>
        </div>
      </div>
      <div className="flex flex-col p-4">
      <button type="button" className="custom-button custom-button-primary" onClick={() => buy(item)}>Buy</button>
      </div>
    </div>
  )
}
```

Nous avons enlevé la classe *cursor-pointer* de la div principale, afin d'utiliser un bouton à la place (meilleur pour l'accessibilité web).

Ensuite nous avons placé la fonction buy dans les props du composant afin que le parent ait le contrôle de la fonction à exécuter.

Enfin, si vous voulez savoir comment est stylisé le bouton, le style se trouve dans le fichier global.css :

```css
/* styles/global.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

body {
  @apply bg-gray-200;
}

.custom-button {
  @apply w-full inline-flex justify-center rounded-md border border-transparent shadow-sm px-4 py-2 text-base text-center font-medium focus:outline-none focus:ring-2 focus:ring-offset-2 sm:w-auto sm:text-sm;
}

.custom-button-primary {
  @apply bg-teal-600 text-white hover:bg-teal-700 focus:ring-teal-500;
}
```

## Modal

Maintenant nous devons implémenter la fonction *buy* dans le parent, qui est le fichier index.js. Mais nous allons être confrontés à un problème, en effet, cette fonction va utiliser la librairie PayzenJS, qui va afficher le formulaire de paiement dans une iframe.

Nous ne voulons pas afficher l'iframe telle quelle dans la page, ce n'est pas très esthétique.

À la place, nous voulons afficher cette iframe dans un composant *Modal*, qui sera par défaut cachée, qui s'affichera au clic sur un bouton *Buy*, et qui pourra être fermée.

Afin d'avoir un meilleur affichage de l'iframe dans la modale, nous allons utiliser la librarie *@tailwindcss/aspect-ratio* et plus particulièrement les classes *aspect-w-1* et *aspect-h-1*.

```json
/* package.json */
  "devDependencies": {
    "@tailwindcss/aspect-ratio": "^0.4.0",
    [...]
  }
```

```bash
npm install
touch components/modal.js
```

```react
// components/modal.js
export default function Modal({content, close}) {

  return (
    <div className="relative z-10" aria-labelledby="modal-title" role="dialog" aria-modal="true">
      <div className="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>
      <div className="fixed z-10 inset-0 overflow-y-auto">
        <div className="flex items-end sm:items-center justify-center min-h-full p-4 text-center sm:p-0">
          <div className="relative bg-white rounded-lg shadow-xl">
            <div className="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
              <div className="flex flex-col gap-2">
                <div className="flex flex-row justify-end">
                  <button className="text-xl text-gray-500 font-bold" onClick={() => close()}>X</button>
                </div>
                <div className="flex content-center justify-center aspect-w-1 aspect-h-1">
                  {content}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  )
}
```

La prop *content* est un slot, c'est dans cette prop qu'on mettra l'iframe.

La prop *close* est une fonction qui sera appelée lorsqu'on voudra fermer la modale sans poursuivre le paiement.

Il nous reste maintenant à gérer l'affichage de cette modale, c'est dans le parent, *index.js* que nous allons le faire :

```react
// pages/index.js
import Head from 'next/head';
import Item from '../components/item';
import Modal from '../components/modal';
import * as React from "react";

export default function Home({ data }) {
  const [displayModal, setDisplayModal] = React.useState(false)

  const buy = (item) => {
    setDisplayModal(true);
    // TODO paiement
  }

  const onCloseModal = () => {
    setDisplayModal(false);
  }

  return (
    <div className="flex flex-col p-2">
      <Head>
        <title>Tutoriel Payzen e-shopping</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>

      <main>
        <div className='flex flex-row content-center justify-center'>
          <div className='flex flex-col content-center justify-center gap-2'>
            <h1 className="font-bold text-lg text-gray-600 text-center">Boutique</h1>
            <div className='grid grid-cols-4 grid-flow-row gap-2'>
              {data.inventory.map((item, i) => <Item key={i} item={item} buy={buy}/>)}
            </div>
          </div>
        </div>
        <div className={displayModal ? 'block' : 'hidden'}>
          <Modal content={<div id="paymentCanvas"></div>} close={onCloseModal}></Modal>
        </div>
      </main>
    </div>
  )
}
```

Nous utilisons le hook *useState* afin de gérer l'état d'affichage de la modale.

## Retour de paiement

Une fois que le paiement sera fait, comme le décrit la documentation Payzen du formulaire de paiement, nous serons redirigés vers l'url correspondante: *vads_url_success* en cas de paiement validé, *vads_url_return* en cas de paiement refusé.

Nous allons donc créer 2 pages, *success.js* et *fail.js* qui nous serviront de callback url, ces pages nous permettront aussi de retourner sur la page principale.

```bash
mkdir pages/payment-result
touch pages/payment-result/fail.js
touch pages/payment-result/success.js
```

```react
// pages/payment-result/fail.js
import { useRouter } from 'next/router'

export default function Fail() {
  const router = useRouter()

  return (
    <div className="flex flex-col gap-4">
      <h1>Paiement échoué</h1>
      <button className='custom-button custom-button-primary' onClick={() => router.push('/')}>Retour</button>
    </div>
  )
}
```

```react
// pages/payment-result/success.js
import { useRouter } from 'next/router'

export default function Success() {
  const router = useRouter()

  return (
    <div className="flex flex-col gap-4">
      <h1>Paiement réussi</h1>
      <button className='custom-button custom-button-primary' onClick={() => router.push('/')}>Retour</button>
    </div>
  )
}
```

## PayzenJS

Nos composants sont prêts, on passe à l'implémentation du paiement, procédons à l'installation de PayzenJS.

```json
/* package.json */
"dependencies": {
  "next": "latest",
  "PayzenJS": "1.0.5",
  "react": "17.0.2",
  "react-dom": "17.0.2"
},
```

```bash
npm install
```

La librarie PayzenJS a besoin que le DOM soit initialisé, le plus simple pour nous est de charger cette librarie via le hook *useEffect* qui permet d'avoir un comportement proche de la fonction *componentDidMount* d'un *React.Component*, qui se lance une fois le DOM chargé.

```react
// pages/index.js
[...]
import * as React from "react";

let PayzenJS;

export async function getServerSideProps() {
  [...]
}

export default function Home({ data }) {
  const [displayModal, setDisplayModal] = React.useState(false)

  React.useEffect(() => {
    
    PayzenJS = require('PayzenJS/payzenjs');
   
   }, []);

   [...]
}
```

Enfin, il nous reste à utiliser cette librarie :

```react
// pages/index.js
const buy = (item) => {
    setDisplayModal(true);
    PayzenJS.go({
      // plateforme Payzen à utiliser, ne pas changer
      target: "secure.osb.pf",
      // données du canvas où l'iframe sera intégré
      canvas: {
            id: "paymentCanvas", // id de la div cible
            width: "1000px", // largeur de l'iframe
            height: "1000px" // hauteur de l'iframe
      },
      /* données du formulaire,
      * cf. doc : https://secure.osb.pf/doc/fr-FR/form-payment/standard-payment/creer-un-paiement-comptant-immediat.html
      * cf. doc : https://secure.osb.pf/doc/fr-FR/form-payment/standard-payment/gerer-les-moyens-de-paiement-proposes-a-l-acheteur.html
      */
      orderData: {
          vads_action_mode: "INTERACTIVE",
          vads_order_id: `TEST-${Math.round(Math.random() * 1000)}`,
          vads_site_id: "12345678",
          vads_ctx_mode: "TEST", // TEST | PRODUCTION
          vads_amount: item.price,
          vads_currency: "953", // XPF
          vads_payment_cards: "", // laisser vide pour afficher tous les types de cartes
          vads_language: "fr", // laisser 'fr' car par défaut c'est la langue 'en'
          vads_theme_config: 'MODE_IFRAME=false;FORM_TARGET=_top', // affichage et comportement du theme, MODE_IFRAME=false => affichage complet, FORM_TARGET=_top => navigation
          vads_redirect_success_timeout: 5, // timeout du redirect après paiement accepté
          vads_redirect_error_timeout: 3, // timeout du redirect après paiement refusé
          vads_url_success: `http://localhost:3000/payment-result/success`, // url retour paiement accepté
          vads_url_return: `http://localhost:3000/payment-result/fail`, // url retour paiement refusé
          vads_return_mode: "POST" // valeur nécessaire pour que le mode d'affichage de la page de retour soit pris en compte
      },
      
      credentials : {
          // endpoint retournant la signature du formulaire, cf. dossier backend
          source: `http://localhost:3001/sign`
      }
    });
  }
```

C'est tout pour notre frontend, passons maintenant au backend.

# Backend

Pour notre backend, nous stockerons d'abord notre certificat dans un fichier *.env* afin de ne pas le mettre en dur dans le code (et de ne pas le mettre dans git), en utilisant la librarie *dotenv*.

Nous ferons des requêtes à partir d'un autre serveur (le frontend est sur le port 3000, et le backend sur le port 3001), et donc être confrontés à un problème de CORS, c'est pourquoi nous utiliserons le module *cors*.

De plus, la librarie PayzenJS nous enverra un formulaire sous forme d'objet JSON, pour pouvoir l'interpréter, nous utilisons *body-parser*.

Enfin, nous devrons hasher et signer les données de notre formulaire, nous utiliserons la librarie *crypto-js* pour cela.

Ce qui nous donne les dépendances suivantes :

```json
/* package.json */
"dependencies": {
  "express": "4.17.2",
  "cors": "2.8.5",
  "crypto-js": "4.1.1",
  "dotenv": "16.0.0",
  "body-parser": "1.20.0"
}
```

Installez les modules :

```bash
npm install
```

## Dotenv
Dans le dossier backend, placez le certificat dans un fichier .env :

```bash
touch .env
```

```bash
# .env
CERTIFICATE=<secret>
```

Et récupérez-le dans le serveur :

```javascript
// main.js
require('dotenv').config();

// modules serveur
const express = require("express");
[...]
// clé de la boutique disponible dans le back office commerçant Payzen
const certificate = process.env.CERTIFICATE;

[...]
```

## CORS

Utilisez *cors* dans votre serveur:
```javascript
// main.js
// modules serveur
const express = require("express");
const cors = require('cors');
[...]
// middlewares
app.use(cors());
app.options('*', cors());
[...]
```

## Body-parser

Utlisez *body-parser* dans votre serveur :
```javascript
// main.js
const cors = require('cors');
const bodyParser = require('body-parser');
[...]
// middlewares
app.use(cors());
app.options('*', cors());
app.use(bodyParser.json());
[...]
```

## Signature

Avant de commencer à utiliser *crypto-js*, nous devons savoir quelles fonctions de cette librarie nous allons utiliser.

[Cette documentation](https://secure.osb.pf/doc/fr-FR/form-payment/standard-payment/calculer-la-signature.html) nous indique que nous devons utiliser ***hmacSHA256*** et ***Base64***.

![fonctions crypto](fonctions_crypto.png#center "fonctions crypto")

Nous devons trier les noms de champs commençant par "vads_" par ordre alphabétique, concaténer leur valeur associée dans une variable, séparées par des "+", et rajouter le certificat à la fin de cette variable.

Ce qui nous donne finalement ce fichier *main.js* :

```javascript
// main.js
// dotenv
require('dotenv').config();

// modules serveur
const express = require("express");
const cors = require('cors');
const bodyParser = require('body-parser');

// modules signature
const hmacSHA256 = require('crypto-js/hmac-sha256');
const Base64 = require('crypto-js/enc-base64');

const app = express();
const port = 3001;

// middlewares
app.use(cors());
app.options('*', cors());
app.use(bodyParser.json());

// clé de la boutique disponible dans le back office commerçant Payzen
const certificate = process.env.CERTIFICATE;

app.post("/sign", (req, res) => {
  var orderData = req.body;

  console.log(orderData);

  // transformer les données de orderData en chaine : "VALEUR_1+VALEUR_2+...+VALEUR_N+CERTIFICAT"
  let dataToSign = "";

  Object.keys(orderData).sort().forEach((key) => {
    if(key.slice(0,5) === 'vads_') {
	    dataToSign += `${orderData[key]}+`;
	  }
  })
  dataToSign += `${certificate}`;

  // calcul de la signature, l'algorithme à utiliser est défini dans le back office commerçant Payzen
  let signature = Base64.stringify(hmacSHA256(dataToSign, certificate));

  // retourner la signature
  res.send({signature: signature});
});

app.listen(port, () => {
  console.log(`Payzen e-shopping backend server listening on port ${port}`);
});
```

# Test

Nous sommes maintenant prêts à tester notre application.

![Home test](home_test.png#center "Home test")

En cliquant sur le bouton *Buy* du premier *Item* nous voyons le formulaire de paiement s'afficher dans la modale.

![Formulaire de paiement](formulaire_paiement.png#center "Formulaire de paiement")

Attention: les données de test sont uniquement possibles si vous avez bien spécifié la valeur ***TEST*** dans le paramètre ***vads_ctx_mode***.

En cliquant sur une des cartes, par exemple "Banque Socredo Verte", nous voyons une liste de cartes de test. En cliquant sur l'une d'entre elle, le formulaire va automatiquement remplir les champs.


![Formulaire - Carte Socredo Verte](formulaire_carte_socredo.png#center "Formulaire - carte Socredo Verte")

Remarque : À côté de chaque carte se trouve un scénario associé, si vous voulez tester un paiement accepté, vous devez choisir la 1ère carte.

Puis, en cliquant sur valider, vous verrez le formulaire pour le code reçu par SMS, aussi appelé OTP pour *One Time Password*.

En mode TEST, vous pouvez juste recopier la valeur affichée, ou cliquer sur la valeur.

![Formulaire - OTP](formulaire_OTP.png#center "Formulaire - OTP")

Enfin, si vous avez bien choisi la carte associé au "paiement accepté", vous obtiendrez l'écran de commande validée.

![Formulaire - Paiement validé](formulaire_paiement_valide.png#center "Formulaire - Paiement validé")

Vous pouvez ensuite soit attendre la redirection automatique, soit cliquer sur "retourner à la boutique", pour aller sur la page /payment-result/success.

![Page paiement validé](page_paiement_reussi.png#center "Page paiement validé")

Nous voyons dans les DevTools que cette redirection est en fait une requête POST, avec les données suivantes.

![Page paiement validé - Data](page_paiement_reussi_data.png#center "Page paiement validé - Data")

# Conclusion

Dans cet article, nous avons utilisé la librarie PayzenJS afin d'afficher le formulaire de paiement dans une iframe contenue dans une modale.

Nous avons ainsi réussi à faire un paiement, et nous avons été redirigé vers la page de paiement réussi de notre application web.

Mais le travail ne s'arrête pas ici, en effet, une fois que le paiement est effectué, validé ou non, il nous reste à exploiter les données de retour afin de déclencher la suite de la commande, ou d'avertir le client que sa commande n'est pas passée.

De plus, nous devons valider qu'il s'agit bien de notre transaction, et non d'une requête forgée.

Nous verrons cela dans le prochain article.