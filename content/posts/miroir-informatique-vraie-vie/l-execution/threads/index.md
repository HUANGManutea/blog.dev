---
title: "IMVV — Section 2 — Chapitre 2 — Monothread, Multithread, Parallélisme et Concurrence, je ne peux pas tout faire en même temps !"
#description: <descriptive text here>
date: 2025-05-01T10:40:55-10:00
weight: 2
draft: false
showToc: true
image: ""
tags: [Informatique, IMVV]
categories: [Vulgarisation]
---
Dans le précédent article, [IMVV — Section 2 — Chapitre 1 — Synchrone et Asynchrone, ou comment réagir au changement](../sync-async/), on a vu les différents modes d'exécution.

On s'était arrêté sur le problème suivant : Comment faire pour répondre à la montée en charge, à l'accumulation de tâches ?

Eh bien, dans cet article, on va voir comment on résout ce problème, en informatique **comme dans la vraie vie** : les mécanismes sont souvent très proches.

Pour cela on va continuer avec notre exemple de restaurant. Et on va expliciter différents termes que j'avais regroupés en parlant d'algorithmes et de programmes.

N'oublie pas que les objectifs de ces articles sont :
- Te donner une meilleure compréhension des bases de l’informatique,
- T'inspirer pour analyser ou optimiser les situations du quotidien,
- ou peut-être, qui sait, te donner envie d'explorer encore plus loin... jusqu’à en faire ton métier.

## Le programme — l'idée de restaurant

En informatique, quand on parle de **programme**, on parle uniquement d'un ensemble d'algorithmes, des tâches qui le composent. Il n'est **pas encore en train d'être exécuté**. Par exemple, Facebook est un programme — mais **tant que tu ne l’ouvres pas, il ne fait rien**.

Eh bien, c'est pareil pour un restaurant dans la vie de tous les jours, quand je parle du restaurant à un ami, je n'y suis pas physiquement. Je parle juste du **concept de restaurant**, de l'idée que je m'en fais.

## Le processus - le restaurant ouvert

Si je veux parler du restaurant physiquement ouvert, avec les employés qui s'activent, en informatique il faut plutôt utiliser le terme **processus**. C'est le **programme en cours d'exécution**.

Un **processus** possède son propre **contexte d'exécution**, c'est un gros mot pour dire qu'il a ses propres **ressources**, et que personne ne peut lui prendre ses ressources.

En effet, quand le restaurant est ouvert, les assiettes qu'il utilise sont **ses propres assiettes**, **ses propres ressources**. Il n'y a pas un autre restaurant qui lui prendrait ses assiettes pendant qu'il est ouvert, sinon il risque d'avoir des assiettes manquantes.

Pour exécuter un algorithme, un processus est composé d'un **thread principal**, et il peut avoir d'autres thread.

## Le thread — la procédure en cours d'exécution du serveur

Le **thread** (*fil d'exécution* en français) est ce qu’on appelle la **procédure en train de s'exécuter**. C’est un peu comme un **serveur qui suit activement une fiche d'instructions** à un instant donné. Attention, ce n'est **pas le serveur**.

En informatique, on dit que le thread est **l’unité d’exécution**, C’est la plus petite unité qu’un ordinateur puisse piloter pour exécuter du code. il n’existe pas d’unité plus petite qu’un thread pour exécuter une tâche.

Maintenant qu’on comprend ce qu’est un thread — une procédure en cours d'exécution — il faut se demander **qui exécute cette procédure**.

## Le coeur — le serveur

On y arrive enfin, dans un ordinateur, le composant physique qui exécute un thread s'appelle un **coeur** (*core* en anglais). Pour notre restaurant, ce **core** est le serveur. C'est lui, physiquement, qui prend les commandes, sert les plats, etc.

## Concurrence, parallélisme, multithread et monothread — ou comment servir 2 familles en même temps

Un serveur ne peut faire qu'une seule chose à la fois, à un instant donné : quand il prend une commande à l'instant T, il ne peut pas, en même temps, servir des plats.

Par contre, il pourrait s'interrompre pendant les tâches, par exemple, au lieu de prendre toutes les commandes de la famille, d'un coup, il peut :
- prendre la commande d'un 1er plat
- aller chercher un plat à servir
- servir le plat
- prendre la commande d'un 2ème plat
- aller chercher un autre plat à servir
- servir le plat
- etc.

Attention: ici nous n'avons pas découpé les actions. C'est juste que le serveur a jonglé entre les 2 tâches *"prendre la commande"* et *"servir les plats"*. On appelle ce comportement la **concurrence**, car les 2 tâches sont en concurrence pour être terminées.

Dans un ordinateur, les **threads sont concurrents**, et comme énoncé plus haut, étant donné qu'un **processus** est composé d'un **thread principal**, on dit que les **processus sont concurrents**.

>Dans la vraie vie il y a des situations où on ne jongle pas avec les tâches, où il faut être concentré sur une tâche

Tout à fait, et dans ce cas, s'il y a trop de tâches pour une seule personne, on fait intervenir une 2ème personne, une 3ème etc.

Dans notre restaurant, avec 2 serveurs, pendant que l'un prend les commandes de la famille 1, un autre peut servir les plats de la famille 2. On appelle ça le **parallélisme**, les procédures/threads sont exécutés en parallèle.

Enfin, dans un restaurant, si on ne peut avoir qu'un seul **serveur qui suit activement une fiche d'instructions** — un seul thread —, on dit que le restaurant/le programme est **monothread**. S'il y en a plusieurs, on dit que le restaurant/serveur est **multithread**.

>Du coup, la solution pour le restaurant est d'embaucher plus de serveurs ?

C'est l'une des solutions, oui, mais ce n'est pas la seule. Il y a globalement 2 chemins pour répondre à une montée en charge. On peut :
- optimiser les algorithmes pour les rendre plus performants et/ou changer le mode d'exécution,
- ou alors on peut mettre plus de coeurs et faire du multithread.

De la même manière, dans la vraie vie, on peut :
- mieux former le serveur et/ou optimiser les procédures qu'il doit suivre et/ou le motiver pour qu'il travaille plus vite,
- embaucher plus de serveurs.

Dans tous les cas, je ne m'avancerai pas pour apprendre à un restaurateur son métier.

## Le partage de ressources — ou comment partager une fourchette

Dans le restaurant, on va maintenant se mettre du point de vue d'un couple, venu manger en tête à tête dans une ambiance cosy, tamisée, à l'abri des regards.

Le serveur leur annonce la mauvaise nouvelle: il y a assez de couverts pour 2, sauf pour la fourchette. S'ils souhaitent tout de même manger ici, ils devront se partager la fourchette, et interdiction de manger avec les doigts.

Le couple discute, et finalement ce n'est pas un problème, ils sont là pour profiter de l'instant.

Une fois la commande passée et les plats servis, Le couple commence à manger. **Mais comment s’organisent-ils ?**

>Ben ils mangent chacun leur tour, ou alors l'un mange d'abord, et l'autre ensuite ?

**Bingo**, que l'un mange d'abord, puis l'autre, ou qu'ils mangent à tour de rôle, dans tous les cas, ils doivent se **partager une ressource** : la fourchette. Donc l'un **prend le contrôle** de la ressource/fourchette, fait des actions avec cette ressource, puis **libère** la ressource. L'autre peut à son tour prendre le contrôle de la ressource, etc.

Dans un ordinateur, c'est pareil, dans un processus, les threads doivent se partager les ressources. De même, les processus doivent se partager les ressources.

C'est pour ça que sur un ordinateur, quand tu ouvres un document Word partagé avec tes collègues, parfois tu as un message du genre *"le fichier est déjà ouvert par..."* car le document Word est une ~~fourchette~~ ressource partagée entre ton application Word, et celle de ton collègue.

>Elle est bizarre ton explication...

**Je ne vois pas de quoi tu parles.**

Quoiqu'il en soit, tu comprends donc qu'**en rajoutant plus de threads/cores/personnes, on ne va pas forcément plus vite**. Ils doivent se synchroniser pour partager les ressources et parfois attendre.

{{% miroir-informatique-vraie-vie-instant-dev %}}
En informatique, ce partage de ressource s’appelle une **section critique**.
Pour éviter que deux tâches utilisent la ressource en même temps, on utilise des **verrous (locks)**.
{{% /miroir-informatique-vraie-vie-instant-dev %}}

## Conclusion

Dans cet article, on a vu différents termes informatiques qui permettent de comprendre un peu plus comment fonctionne un ordinateur, comment on pouvait répondre à la montée en charge de différentes manières, et que finalement, c'est très proche de la vie réelle.

Nous avons fini cette section "IMVV — Section 2 — L'exécution : comment faire des actions ?".

Dans la prochaine section, [IMVV — Section 3 — L'optimisation : comment se faire passer pour un coach de vie](../../optimisation/optimisation/), on verra comment optimiser des applications et la vie réelle.

[← Retour à la section](../../l-execution/l-execution/)

[← Retour à l’introduction](../../introduction/)