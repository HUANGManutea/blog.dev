---
title: "IMVV — Section 3 — Chapitre 1 — La mémoire, ou comment éviter les pénuries dans un magasin"
#description: <descriptive text here>
date: 2025-05-01T14:35:32-10:00
weight: 1
draft: false
showToc: true
image: ""
tags: [Informatique, IMMV]
categories: [Vulgarisation]
---
La mémoire est une **ressource** au même titre que la fourchette dans le [précédent article](../../l-execution/threads/).

Dans un ordinateur, il existe plusieurs types de mémoire que les programmes vont pouvoir utiliser en fonction de la manière dont ils veulent traiter les données.

Il faut voir la mémoire comme un endroit où on entrepose des données.

Pour cet article on va parler d'un magasin, mais ça marche aussi avec un restaurant.

## La mémoire cache — l'armoire réfrigérée

La **mémoire cache** est le stockage **le plus rapide** qu'un programme peut utiliser. Pour un magasin, il s'agit des étagères et des armoires réfrigérées qui forment les rayons.

Les clients (les threads du programme) ont rapidement accès aux viandes qui sont dans les armoires réfrigérées, ils n'ont qu'à tendre la main. Par contre, on ne peut pas stocker une grande quantité de viande dans ces armoires, pour l'exemple on va dire une dizaine au maximum.

Sur un ordinateur, cette mémoire cache se trouve directement dans le processeur sous les noms **cache L3**, **cache L2** et **cache L1**. On n'ira pas dans le détail ici, mais sachez que plus le nombre est proche de 0, et plus le cache est rapide.

Je prends l'exemple de l'armoire réfrigérée car il y a un mécanisme physique important dans un ordinateur: la mémoire cache peut accueillir des données **uniquement si elle est alimentée en électricité**, en cas de coupure de courant, on **perd les données** qui s'y trouvent.

De la même manière, dans un magasin, en cas de coupure de courant, il faut **jeter toute la viande qui se trouve dans les armoires réfrigérées***.

*: Oui c'est pas tout à fait le cas, mais en cas de coupure prolongée ça l'est.

## La mémoire vive — l'arrière du magasin

Au cours d'une journée, le magasin souhaite vendre bien plus que dix viandes, c'est bien normal. Pour cela, à l'arrière du magasin il y a un stock réfrigéré qui peut en contenir 1000. Un employé viendra remplir les rayons au cours de la journée.

Cette action prend du temps, l'employé doit :

```
Aller dans le stock réfrigéré
Récupérer des viandes
Amener les viandes dans le rayon
Mettre les viandes dans l'armoire réfrigérée
```

Pendant tout ce temps, le client ne peut prendre que les viandes qui sont encore dans l'armoire, il faut donc bien faire attention à ce que l'employé recharge l'armoire quand il reste encore un peu de boîtes.

Dans un ordinateur, la **mémoire vive** (*RAM* en anglais pour *Random Access Memory*), joue le rôle du stock réfrigéré très rapide qu'un programme peut utiliser, mais beaucoup moins rapide que la mémoire cache, environ 50x à 100x moins rapide.

Et tout comme la **mémoire cache**, la RAM peut accueillir des données **uniquement si elle est alimentée en électricité**.

C'est pour ça qu'on appelle ça de la mémoire **vive**, elle doit être **alimentée**.

>Attends, mais tu dis que la RAM est très rapide, mais le processus pour recharger la mémoire cache est lent ? On ne peut pas juste utiliser une grande quantité de mémoire cache?

La mémoire cache coûte très cher, beaucoup plus que la RAM. L'état actuel est donc un compromis entre rapidité et coût, un problème typique en ingénierie.

## Le stockage — la ferme en Nouvelle-Zélande

Le stockage d'un ordinateur est composé des différents disques durs (*HDD*, *SDD*, etc.). Il s'agit d'une **mémoire persistante**, c'est-à-dire que même en cas de coupure de courant, les données restent écrites dans les disques.

Pour notre magasin, de la viande qui reste utilisable même en cas de coupure... Eh bien ce sont les boeufs vivants à la ferme.

>Ton analogie est dégoûtante

Oui je sais, j'ai pas mieux, désolé. En même temps, je ne peux pas vous dire que de la viande fraîche, qui reste longtemps à l'air libre, est encore utilisable.

>En plus, il y a plein d'étapes entre un boeuf vivant et un steak dans l'armoire !

Tout à fait, mais c'est la meilleure analogie possible pour te faire comprendre pourquoi, en cas de coupure, si tu n'as pas sauvegardé ton fichier Word depuis longtemps, tu perds tes données. **Tant que tu n'as pas sauvegardé, tes modifications restent dans le cache et la RAM**.

>Et pourquoi en Nouvelle-Zélande ?

Oh, ça c'est parce qu'aller chercher une donnée dans un disque, c'est très lent comparé à aller la chercher dans la RAM. Si tu as un disque SSD c'est 10x plus lent, si tu as un disque HDD, c'est 100x plus lent.

Si tu joues à des jeux vidéo un peu gourmands en ressources, tu as sûrement remarqué des écrans de chargement plus ou moins longs. C'est surtout parce que **le programme récupère les données qui sont sur le disque**.

## Optimiser la mémoire — pas besoin d'être mentaliste

Vous l'aurez donc compris, un magasin a différents types de mémoire à sa disposition. La manière dont il orchestre les denrées à travers ces différents composants lui permet d'anticiper les variations de stock, et limiter le risque de pénurie.

Lorsqu'un développeur code un programme, il peut aussi anticiper l'utilisation des données et les charger avant d'en avoir besoin.

>Dans l'exemple du jeu vidéo, pourquoi est-ce que toutes les données ne sont pas chargées dès le début? Moi j'en ai marre des écrans de chargement.

Tout d'abord, ce chargement se fait du stockage vers la RAM (puis vers le cache), ensuite, si on chargeait toutes les données d'un coup, il y a de fortes chances pour que ta RAM soit saturée.

A priori, le développeur ne sait pas si tu as peu ou beaucoup de RAM disponible, et puis, maintenir deux versions du code, un qui charge toutes les données, et un qui charge via les écrans de chargement, c'est du travail supplémentaire qui n'apporte pas grand chose.

Les écrans de chargement sont un compromis : plutôt que de risquer de crasher ton ordinateur, le développeur a codé le programme de sorte à charger uniquement le contenu qui sera utilisé dans le niveau, pour tous les niveaux.

## Conclusion

Dans cet article, on a vu les différentes mémoires utilisées par les programmes. À l'image d'un magasin qui évite les pénuries, un développeur doit jongler avec ces mémoires pour que son programme tourne correctement.

Dans le prochain article, [IMVV — Section 3 — Chapitre 2 — Mémoïsation et Lazy loading, les technique du fainéant ultime](../memoisation/), nous verrons des techniques qui feront de toi un bon fainéant.

[← Retour à la section](../../optimisation/optimisation/)

[← Retour à l’introduction](../../introduction/)