---
title: "Payzen e-shopping formulaire - Introduction"
date: 2022-05-07T21:26:05-10:00
draft: true
---

Dans cette série d'articles nous verrons ensemble comment implémenter Payzen By OSB dans une application web fullstack.

# Présentation de Payzen

Payzen est une plateforme permettant de payer de plusieurs manières différentes:

- API formulaire de redirection (avec ou sans iFrame)
- API REST
- dépôt de fichier

Note: **A l'heure actuelle, il n'est pas possible de payer avec une carte privative avec l'API REST**, une livraison est en cours pour débloquer cette situation.

La méthode la plus répandue est d'utiliser l'API formulaire de redirection. Elle va nous permettre de générer un formulaire qui pourra par la suite être intégré directement dans l'application via une iFrame, ou être envoyé au client par SMS ou par email.

Dans cette série d'articles, nous allons implémenter le formulaire de redirection via iFrame, c'est d'ailleurs ce que font les modules d'intégrations Payzen dans les CMS.

Pour préparer notre implémentation, nous devons récupérer notre **identifiant boutique** ainsi que notre **clé d'API formulaire**, vous pouvez vous référer à [cette documentation](https://secure.osb.pf/doc/fr-FR/form-payment/standard-payment/s-identifier-lors-des-echanges.html), je vous conseille de télécharger la documentation au format PDF pour faciliter les recherches.

# Architecture

Notre application sera composée comme suit:

- Un backend en Node.js qui servira à calculer la signature d'un appel vers l'API formulaire,
- Un frontend en Next.js qui sera notre site de e-shopping

Ce frontend appelera d'abord notre backend pour calculer la signature, puis enverra le message, avec la signature, à l'API formulaire.

Pour cela, nous utiliserons la librairie [PayzenJS](https://www.npmjs.com/package/PayzenJS).

Commençons par la partie frontend.