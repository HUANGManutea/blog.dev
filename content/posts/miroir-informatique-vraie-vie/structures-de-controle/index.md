---
title: "IMVV - Chapitre 3 - Structures de contrôle et algorithme, apprendre à réfléchir"
weight: 3
#description: <descriptive text here>
date: 2025-04-30T14:30:37-10:00
draft: true
showToc: true
image: ""
tags: [Informatique, Miroir de la vraie vie]
categories: [Vulgarisation]
---

Dans l'article précédent, on s'était arrêté sur ta question:

>Et c'est quoi le parcours de graphe?

Dans cet article, on va parler des **structures de contrôle** (*control flow statements* en anglais), qu'on utilise dans des **algorithmes** (*algorithms* en anglais).

Avant d'expliquer l'algorithme que tu as fait, le **parcours de graphe**, on doit expliquer les structures de contrôle.

## La boucle — ou comment avoir la flemme

## La condition — ou pourquoi il faut respecter le code de la route

## Revenons à notre parcours de graphe

Pour rappel, tu avais appelé tes amis pour les inviter à ton anniversaire, et tu avais été jusqu'au bout du monde, en sautant de relations en relations, pour inviter Paul.

La succession d'étapes que tu as fait pour appeler tes amis peut être écrit comme ceci:

```
Dans ta liste d'amis, pour chaque ami:
    Tu l'appelles
    Si il répond, alors:
        Tu l'invites à ton anniversaire
    Fin si
Fin pour
```

"Dans ta liste d'amis, pour chaque ami" marque le début d'une **boucle** (*loop* en anglais), et "Fin pour" marque la fin de la boucle.
La boucle te permet de répéter la même action pour un ensemble d'éléments, en l'occurence, appeler un ami.

"Si il répond, alors" marque le début d'une **condition**, et "Fin si" marque la fin de la condition.
La condition te permet de faire une action uniquement si cette condition est respectée. En effet, on peut inviter un ami **si et seulement si** il répond à ton appel.

La **boucle** et la **condition** sont des **structures de contrôle** (*control flow statements* en anglais). 

Si on se représente ça :

La liste d'amis: 

|Manutea|Vai|Purotu|Heiarii|Reva|Jean|
|---|---|---|---|---|---|

*Pour chaque ami* veut dire que tu as parcouru la liste:
- d'abord tu as pris Manutea, puis tu as effectué l'action: tu as appelé Manutea,
- puis tu as pris Vai, puis tu as appelé Vai,
- etc. jusqu'à Jean

>Et Paul?

C'est là où ça devient plus compliqué.
