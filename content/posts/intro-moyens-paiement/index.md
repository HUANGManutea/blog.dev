---
title: "Introduction aux moyens de paiement en Polynésie Française"
date: 2022-05-07T19:18:54-10:00
draft: false
---

# Introduction

Je souhaite que la Polynésie Française se modernise, les moyens de paiement sont un des axes d'amélioration où je peux aider. Dans ce but, je pense créer une série d'articles et de tutoriels sur les moyens de paiement, à commencer par cet article.

**Disclaimer**: Au moment où j'écris cet article, je travaille à l'Océanienne des Services Bancaires (OSB), mes articles seront orientés vers les solutions d'OSB car ce sont celles avec lesquelles je suis le plus familier. Ces articles ne sont pas sponsorisés par OSB, et j'encourage les gens à faire des tutoriels pour les solutions des autres fournisseurs de solutions de paiement.

# Les différents types de carte

En Polynésie Française, il est possible de payer avec plusieurs types de cartes.

Les cartes bancaires internationales:

- Carte Bleue (co-brandées ou non de Visa ou Mastercard),
- American Express (AMEX),
- Union Pay International (UPI),
- Discover,
- Japan Credit Bureau (JCB)

Les 3 derniers types de cartes sont surtout utilisés par les touristes.

Et les cartes privatives proposées par les différentes banques de la place: Socredo, Banque de Tahiti, Banque de Polynésie, Fare Rata.

Note: OFINA est aussi une banque, mais elle n'émet que des cartes AMEX, pas de cartes privatives.

***Les cartes privatives composent la majorité des cartes détenues par les habitants de la Polynésie Française.***

# Pourquoi autant de personnes ont une carte privative ?

Les cartes privatives sont soumises à des réglementations et des frais moins coûteux que les cartes internationales.

En outre, elles sont uniquement régulées par les banques de la place, contrairement aux cartes bancaires internationales, qui sont non seulement régulées par les banques de la place, mais aussi par les réseaux internationaux (GIE CB, Visa, Mastercard, Union Pay, etc.).

***C'est en partie à cause de ces réglementations et frais moins coûteux que les clients des banques doivent remplir moins de conditions pour avoir une carte locale. C'est pour cela que les cartes privatives sont plus répandues sur le territoire.***

Notes:

Les réseaux peuvent décider d'appliquer des amendes voire de désactiver le flux vers un acteur monétaire (banque, processeur de paiement, etc.) si celui-ci ne respecte par la réglementation. Cette réglementation est mise à jour de temps en temps.

Pour les cartes privatives, ce sont les banques de la place qui imposent leur réglementation, par abus de langage, on parle aussi de réseau privatif pour désigner l'ensemble de ces banques.

Ces réglementations sont suivies par les banques centrales des pays, par exemple l'IEOM en Polynésie Française. 

# Fonctionnement des transactions

Le schéma à 4 coins est l'un des schémas de référence de la monétique. Il explique les entités qui entrent en jeu dans une transaction.

![Schéma à 4 coins](schema_4_coins.png "Schéma à 4 coins")

La banque émetteur émet la carte et la fournit au porteur.

La banque acquéreur fournit un contrat accepteur au commerçant, afin que celui-ci puisse encaisser les paiements avec les cartes, moyennant une commission, en plus des services annexes autour de l'encaissement (exemple: relevé TPE). Les TPE et solutions de paiement en ligne sont des services d'encaissement.

Un système d'acceptation est un logiciel ou un ensemble de logiciels, qui permet d'encaisser une carte bancaire, par exemple les TPE et les plateformes de paiement en ligne.

Un paiement se fait généralement en 2 phases:

La phase d'autorisation :

- le porteur insère sa carte dans le TPE OU pose sur la zone sans contact OU rentre les informations de carte dans l'application web,
- le système d'acceptation vérifie les informations et/ou envoie les informations aux banques pour autoriser la transaction,
- le résultat revient et le ticket est imprimé

La phase de télécollecte et de compensation :

- tous les soirs, les TPE renvoient la liste des transactions à la banque acquereur,
- les transactions des TPE et des solutions de paiment en ligne sont ensuite transformées en mouvements financiers (M. Client doit 1000 XPF au commerçant),
- les banques s'échangent ces mouvements financiers

Ce mode de fonctionnement est appelé "dual message", car il y a 2 flux, le flux d'autorisation, et celui de la compensation. Contrairement au mode "single message" où l'autorisation est transformée directement en mouvement financier.

# Les cartes et les systèmes d'acceptation

Pour qu'un système d'acceptation puisse encaisser une carte, elle doit reconnaître la carte.

Pour reconnaître une carte, on utilise le BIN, qui sont les N premiers chiffres du numéro de la carte, N étant défini par le réseau.

De plus, seule une application spécifique à ce réseau peut reconnaître cette carte. Par exemple, pour une transaction avec une carte AMEX sur un TPE, c'est uniquement une application TPE AMEX qui pourra la reconnaître, mais ***seulement si la carte fait partie d'une plage de BIN acceptée par l'application***.

Note: Dans un TPE, il peut y avoir plusieurs applications, quand une carte est insérée, le TPE demande à chaque application "Peux-tu accepter cette carte?".

De la même manière, pour une plateforme de paiement en ligne, celle-ci ne pourra accepter que des cartes qui font partie de ses plages de BIN déclarées.

# Zoom sur le paiement en ligne en Polynésie Française

Comme énoncé précédemment, les cartes privatives sont majoritaires en Polynésie Française, et elles ne sont pas reconnues à l'étranger (sauf pour la carte Socredo UPI, qui passe par le réseau UPI à l'étranger) car les BIN privatifs ne sont pas déclarés dans le monde.

C'est pour cela qu'on ne peut pas payer avec une carte privative sur la plupart des plateformes de paiement en ligne (Paypal, Stripe, etc.).

# Quelles sont les solutions ?
 
Sur le territoire, Payzen, proposée par OSB, est actuellement la solution la plus connue qui accepte les cartes privatives. La Banque de Tahiti quant à elle vient de lancer SystemPay, un produit concurrent.

A mon avis, à l'heure actuelle, c'est vers ces solutions que je conseille les commerçants d'aller, car ***il serait dommage de se priver des cartes privatives, alors qu'elles sont plus nombreuses.***

Notes:

Les 2 solutions sont en réalité basées sur les solutions Payzen et SystemPay de Lyra, société située en France. Certains d'entre vous ont d'ailleurs peut-être déjà été confus en recherchant de la documentation sur ces solutions et se sont perdus entre la documentation Payzen d'OSB, la documentation Payzen de Lyra, la documentation SystemPay de la Banque de Tahiti, et la documentation SystemPay de Lyra.

***Je vous conseille de vous focaliser sur les documentations locales, et ensuite de compléter avec les documentations de Lyra.***

# Conclusion

En Polynésie Française, la plus grande part des cartes bancaires sont des cartes privatives, pour des raisons économiques et réglementaires.

Le fonctionnement même des systèmes d'acceptation impose quels types de cartes ils peuvent accepter, de ce fait, un commerçant local qui cherche une solution de paiement en ligne devrait se tourner vers les plateformes qui acceptent les cartes privatives.

C'est à partir de ce raisonnement que dans les articles suivants, je présenterai comment implémenter Payzen By OSB sur une application web fullstack.

Si vous utilisez un CMS du style Odoo ou Prestashop, il existe des modules déjà tout faits pour intégrer Payzen dans votre site. Je ne parlerai pas des CMS dans cette série d'articles.