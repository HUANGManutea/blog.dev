---
title: "IMVV — Section 1 — Chapitre 1 — File ou Pile ? L'art de passer avant les autres"
weight: 1
#description: <descriptive text here>
date: 2025-04-29T14:34:21-10:00
draft: false
showToc: true
image: ""
tags: [Informatique, IMVV]
categories: [Vulgarisation]
---
Quand tu prends un ticket pour attendre ton tour, que tu fais la queue à la caisse, que tu prends l’assiette du haut de la pile pour mettre la table, ou que tu cliques sur le bouton 'Retour' (←) du navigateur internet…
Tu manipules sans le savoir des concepts appellés en informatique **des structures de données**, et **les algorithmes** associés qui les font vivre.

Dans cet article, on va mettre un peu de clarté là-dedans : pas besoin de coder pour comprendre, on va illustrer tout ça avec des situations de la vie courante.

# Définitions

Avant d’aller plus loin, quelques définitions simples, histoire de parler le même langage :

- **Donnée** : une donnée, c’est une information numérique. Ça peut être un numéro de passeport, le nombre de dents d’une personne, la liste des tâches que tu as encore repoussées à demain, ou ton nombre d’amis sur Facebook.
- **Structure de données** : imagine une boîte, une étagère ou un sac à dos, dans lequel tu ranges tes informations d’une certaine manière pour mieux les retrouver ou les traiter. C’est la façon dont on organise les données.
- **Algorithme** : un algorithme, c’est une suite d’étapes ou d’instructions pour manipuler ces données. Comme une recette de cuisine, ou une procédure à suivre pour obtenir un résultat.

# File et pile : deux manières d’attendre… ou de repousser

Maintenant qu’on a les bases, voyons deux structures de données très simples mais très puissantes : la file et la pile.
On les retrouve partout dans notre quotidien, souvent sans s’en rendre compte.

## La file — ou comment attendre son tour (FIFO)

Imagine une file d’attente devant un guichet. Le premier arrivé est le premier servi.
C’est ce qu’on appelle en informatique une **file** (ou *queue* en anglais), avec une logique **FIFO : First In, First Out** (premier entré, premier sorti).

Dès que quelqu’un est servi, c’est le suivant dans la file qui avance.

🎯 C’est une structure **équitable** : chacun attend selon son ordre d’arrivée.

{{<miroir-informatique-vraie-vie-exemples
    reel="Faire la queue à la caisse du magasin||La liste des courses (si on lit de haut en bas)"
    info="Les systèmes de ticket dans les accueils (le numéro est généré par un programme, et les appels suivent cet ordre)||Les commentaires sur une publication Facebook (affichés du plus ancien au plus récent)"
>}}

## La pile — ou comment empiler les priorités (LIFO)

Maintenant, imagine une pile de livres que tu dois réviser pour un examen.
Tu prends celui du haut, tu le lis, puis tu prends celui juste en dessous, et ainsi de suite.
Tu lis dans l’ordre inverse de celui dans lequel tu as empilé les livres.
Tu viens de dépiler ta pile, toujours en commençant par le haut.

C’est exactement le principe de la **pile** (ou *stack* en anglais), qui suit la logique **LIFO : Last In, First Out** (dernier entré, premier sorti).

Tu vas peut-être me dire :

>Oui mais je peux aussi prendre le livre du bas, non ?

C’est vrai. Alors prenons un autre exemple, un peu plus réaliste :

Imagine que tu tombes sur un article de journal qui parle des **nodules polymétalliques dans les fonds marins de la Polynésie française**. Tu n’y connais pas grand-chose, mais ça t’intrigue.
Tu lis l’article, puis tu ouvres une page *Wikipédia* pour comprendre ce qu’est un nodule polymétallique. Sur cette page, tu vois un lien vers les métaux rares, puis vers la transition énergétique, puis… tu vois où je veux en venir.

En lisant ce premier article, tu ne soupçonnais pas toute la **pile** d’informations que tu allais explorer. Et tu viens de **dépiler** ce savoir, en commençant par la dernière page ouverte.

🎯 Ce n’est **pas une structure équitable** : ce qui arrive en dernier est traité en premier.
Mais c’est très utile pour remonter dans le temps, ou revenir sur ses pas, exactement comme le bouton "retour" de ton navigateur.

{{<miroir-informatique-vraie-vie-exemples
    reel="Les cartons dans un coffre bien rempli||Les différentes strates de terre quand tu creuses dans ton jardin (c'est de la terre empilée au cours du temps)"
    info="Le bouton 'Retour' (←) de ton navigateur||Les annulations successives (Undo, CTRL+Z) dans un éditeur de texte"
>}}

Si tu veux connaître d'autres structures de données, tu peux regarder le prochain article : [IMVV — Section 1 — Chapitre 2 — Autres structures de données, j'organise mon bordel](../structures-de-donnees/)

[← Retour à la section](../../les-bases/les-bases/)

[← Retour à l’introduction](../../introduction/)