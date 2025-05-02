---
title: "IMMV - Section 2 - Chapitre 1 - Synchrone et Asynchrone, ou comment réagir au changement"
#description: <descriptive text here>
date: 2025-05-01T00:10:38-10:00
weight: 1
draft: false
showToc: true
image: ""
tags: [Informatique, IMMV]
categories: [Vulgarisation]
---
Dans le précédent article, [IMVV - Section 1 - Chapitre 3 - Structures de contrôle et algorithme, apprendre à réfléchir](../../les-bases/structures-de-controle/), on a vu les différentes structures de contrôle et les algorithmes.

Maintenant on va parler de la manière dont on réalise un ensemble de tâches — c’est ce qu’on appelle en informatique un **mode d’exécution**. C'est applicable aussi bien pour un humain que pour un ordinateur.

N'oublie pas que les objectifs de ces articles sont :
- Te donner une meilleure compréhension des bases de l’informatique,
- T'inspirer pour analyser ou optimiser les situations du quotidien,
- ou peut-être, qui sait, te donner envie d'explorer encore plus loin... jusqu’à en faire ton métier.

## Programme et application — c'est quoi la différence ?

Un programme informatique est un ensemble d'algorithmes. Le mot *application* veut dire la même chose.  
C’est juste que *application*, ça sonne plus moderne, même si ce mot existe depuis longtemps.

[Merci le marketing Apple et son App Store. 😄](https://retrocomputing.stackexchange.com/questions/27236/difference-between-program-and-application)

## Synchrone — Avoir un serveur dédié à sa table, quel luxe

Prenons l'exemple d'un restaurant chic. Dans ce restaurant chic, il y a 2 tables. Chaque table a son serveur attitré, celui-ci répond uniquement aux besoins de sa table.

Pour la suite de cet exercice de pensée, on va dire qu'il y a 2 familles (famille 1, famille 2), 2 tables (table 1, table 2), 1 serveur, 1 chef.

La **séquence d'actions** que le serveur doit faire, l'**algorithme** est :
```
Si une famille arrive:
    Accueillir la famille
    Installer la famille sur une table libre
    Prendre la commande
    Donner la commande au chef
    Récupérer les plats
    Servir les plats à la famille
    Faire payer la famille
Fin si
```

La famille 1 arrive au restaurant, le serveur les accueille et les installe à la table 1. Il reste en attente de leur commande, à proximité*.

Quand la famille 1 est prête, vu que le serveur est à côté, ils passent commande. Le serveur s'en va ensuite en cuisine pour donner la commande au chef. Le serveur attend les plats. Le chef prépare les plats.

Une fois que les plats sont prêts, il les récupère et les sert à la famille 1. La famille 1 paie et s'en va, heureuse de l'attention portée.

*: A ce moment, la famille 2 arrive au restaurant, ils ne sont pas accueillis, puisque le serveur est en attente de la commande de la famille 1. Alors la famille 2 repart, agacée, ils laisseront un mauvais avis sur internet.

Dans cette configuration, le serveur exécute ses tâches de manière **synchrone**, cela veut dire qu'il exécute l'algorithme étape par étape **sans interruption**. Si une étape nécessite d'attendre, par exemple quand il doit attendre que la famille choisisse sa commande, alors il attend, on dit que le mode synchrone est **bloquant**. Le serveur va au bout de son algorithme.

>Mais c'est nul, il y a une famille qui n'a pas été servie...

Si on reste dans le **mode d'exécution** synchrone, le problème est qu'il n'y a pas assez de serveur. S'il y avait autant de serveurs de tables et de chefs, il n'y aurait aucun souci. Chaque famille aurait été ravie d'avoir un serveur et un chef dédié. Mais on verrait plutôt cette disposition dans les restaurants luxueux, qui peuvent se permettre d'avoir 100 tables, 100 serveurs et 100 chefs.

Par défaut, les applications sont synchrones, car à part le problème de ressources, c’est bien plus simple de faire une tâche après l’autre, cependant, de nos jours, de plus en plus de systèmes sont asynchrones (exemple: navigateurs, certains serveurs applicatifs à la mode).

{{<miroir-informatique-vraie-vie-exemples
    reel="Une personne qui suit une procédure critique||Préparer une salade"
    info="Un distributeur de billets||Une imprimante partagée"
>}}

## Asynchrone — Un serveur pour les gouverner tous

— Oui c'est une référence au Seigneur des Anneaux 😄 —

Reprenons l'exemple du restaurant, toujours avec 2 familles (famille 1, famille 2), 2 tables (table 1, table 2), 1 serveur, 1 chef.

Mais cette fois, on change l'**algorithme** :
```
Quand une famille arrive, alors :
    Le serveur les accueille
    Il les installe à une table libre
    Il leur donne un menu
    Il passe à autre chose
Fin quand

Quand une famille appelle le serveur pour commander, alors :
    Le serveur prend la commande
    Il la transmet au chef
    Il passe à autre chose
Fin quand

Quand la sonnette en cuisine retentit (plats prêts), alors :
    Le serveur récupère les plats
    Le serveur sert les plats à la bonne table
    Il passe à autre chose
Fin quand

Quand une famille veut payer, alors :
    Le serveur encaisse
    Il libère la table
    Il passe à autre chose
Fin quand
```

Cet algorithme est différent de ceux qu'on a vus jusqu'à présent.

*"Quand ...,"* marque un **événement**, *"alors"* introduit le **bloc** d'instructions à exécuter en **réaction**, et *"Fin quand"* marque la **fin** de ce bloc.

On dit alors qu'on fait de la **programmation événementielle** (ou *programmation réactive*) et que l'algorithme est **asynchrone** : il fait de sorte à réagir aux événements extérieurs.

Lorsqu’un événement se produit, le serveur y réagit immédiatement : il exécute les instructions associées, puis passe à l’événement suivant s’il y en a un. Sinon, il attend. Ce mode d'exécution est donc **non bloquant**.

Et dans les faits, c'est ce que fait la plupart des personnes, serveurs ou non. Quand on fait une tâche, et qu'on est interrompu par un bug, un appel, un collègue de travail qui pose une question, on est en **réaction**.

Avec cet algorithme, un serveur seul pourra très bien gérer 2 tables.

{{<miroir-informatique-vraie-vie-exemples
    reel="Les serveurs dans la plupart des restaurants||Mon chien quand il entend les croquettes"
    info="Les notifications sur ton smartphone||Un arrosage automatique avec capteur d'humidité"
>}}

Attention : comme en mode **synchrone**, s'il y a trop de table pour un seul serveur, plusieurs **événements** risquent de s'accumuler en attente de traitement.

>Mais du coup, comment on fait pour résoudre ce problème ?

On verra ça dans le prochain article.

## Conclusion

Dans cet article, on a vu ce qu'étaient les modes d'exécution **synchrone** et **asynchrone**.

Si tu souhaites continuer cette aventure, tu peux regarder la suite ici: [IMMV - Section 2 - Chapitre 2 - Monothread et Multithread, je ne peux pas tout faire en même temps !](../threads/)

[← Retour à la section](../../l-execution/l-execution/)

[← Retour à l’introduction](../../introduction/)
