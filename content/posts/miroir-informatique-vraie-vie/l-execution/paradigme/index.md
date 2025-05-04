---
title: "IMVV — Section 2 — Chapitre 1 — Paradigmes, ou comment réfléchir différemment"
#description: <descriptive text here>
date: 2025-05-03T16:25:04-10:00
weight: 1
draft: false
showToc: true
image: ""
tags: [Informatique, IMVV]
categories: [Vulgarisation]
---
Dans le précédent article, [IMVV — Section 1 — Chapitre 3 — Structures de contrôle et algorithme, apprendre à réfléchir](../../les-bases/structures-de-controle/), on a vu les différentes structures de contrôle et les algorithmes.

Dans cet article, on verra comment écrire un programme, et qu'en changeant notre manière de réfléchir, certains problèmes sont plus simples à résoudre.

Rassure-toi, nous n'allons pas réellement développer.

N'oublie pas que les objectifs de ces articles sont :
- Te donner une meilleure compréhension des bases de l’informatique,
- T'inspirer pour analyser ou optimiser les situations du quotidien,
- ou peut-être, qui sait, te donner envie d'explorer encore plus loin... jusqu’à en faire ton métier.

## Programmation impérative — je t'ordonne de m'obéir

Si je te demande un exemple de *d'ordre impératif*, tu me diras peut-être : *"Range ta chambre"*. Il en résulte que l'enfant range sa chambre — je parle d'un enfant qui écoute ses parents —.

En informatique, la **programmation impérative** ou **paradigme impératif** est équivalent, le programme est la liste des ordres que l'ordinateur doit suivre.

Dans l'exemple de la recette de gâteau :
```
Préchauffer le four
Verser la farine dans le saladier
Casser les oeufs et mettre le contenu dans le saladier
Verser le lait dans le saladier
Remuer
Verser la préparation dans un moule
Mettre le moule au four
Attendre 20 minutes
Eteindre le four
Sortir le moule du four
Démouler
```

Cette recette est une liste d'ordres.

>Pourquoi on appelle ça un *paradigme* au lieu de dire une *manière de réfléchir* ?

Eh bien, c'est exactement ce que veut dire le mot **paradigme** : une manière de réfléchir. C'est le terme exact, et puis c'est plus court.

## Programmation orientée objet — je manipule des objets

La programmation impérative est centrée sur le fait de donner des ordres à un ordinateur. Mais si on résume un programme, finalement, c'est juste des données et des fonctions qui modifient ces données.

C'est pourquoi nos prédécesseurs ont inventé la **programmation orientée objet**. On manipule des objets, on les transforme, l'attention est maintenant sur les données.

Un exemple :

Supposons que tu souhaites acheter des chaussures. Tu vas au magasin de chaussures et tu vois une belle paire de chaussures. Ces chaussures sont exactement de ta *pointure*, de ta *couleur* préférée, c'est une *marque* que tu aimes bien, et puis leur *design* est vraiment bien. Bref, c'est un bel **objet**.

Par contre, son prix est un peu au-dessous de ton budget. Heureusement, tu as une carte de fidélité qui pourrait faire baisser le prix.

On peut représenter les chaussures en informatique eà l'aide d'une **classe**, qui est un modèle qu'elles suivront toutes :

<figure>
{{< mermaid >}}
classDiagram
    class PaireDeChaussures {
        - pointure
        - couleur
        - marque
        - design
        - prix
        - utiliserCarteDeFidélité()
    }
{{< /mermaid >}}
<figcaption>La paire de chaussures de tes rêves</figcaption>
</figure>

Cette classe est une structure qui nous permet de stocker tous les attributs d'une paire de chaussures au même endroit. Ainsi on pourrait avoir :

```
# La paire de chaussures que tu veux
PaireDeChaussures1{
    pointure: 45
    couleur: noire
    marque: Nike
    design: espadrilles
    prix: 30 000 XPF
}

# Une autre paire de chaussures
PaireDeChaussures2{
    pointure: 45
    couleur: noire
    marque: Nike
    design: espadrilles
    prix: 30 000 XPF
}
```

Et en utilisant la fonction *utiliserCarteDeFidélité()* d'une chaussure, on pourrait faire baisser son attribut *prix*.

## La programmation réactive — Action, réaction

Les précédents paradigmes sont très utiles pour manipuler des données et donner des ordres. Mais imaginons la situation suivante :

Tu as passé un concours il y a un mois. L'examinateur t'a dit que les résultats seraient disponibles sur un site internet. Sur ce site :
- tu peux évidemment regarder les résultats s'il y en a,
- mais tu peux aussi demander à recevoir une notification dès que les résultats sont publiés.

Si tu essayais de programmer ton comportement, en programmation impérative ou orientée objet ça donnerait quelque chose comme ça :

```
Tant que je n'ai pas mes résultats:
    je vais sur le site
    S'il y a mes résultats:
        je les regarde (on sort de la boucle)
    Fin si
Fin tant que
```

En **programmation réactive** :
```
Quand je reçois une notification, alors:
    je vais sur le site
    je regarde mes résultats
Fin quand
```
*"Quand ...,"* marque un **événement**, *"alors"* introduit le **bloc** d'instructions à exécuter en **réaction**, et *"Fin quand"* marque la **fin** de ce bloc.

On dit alors qu'on fait de la **programmation événementielle** (ou *programmation réactive*) : on réagit aux événements extérieurs. L'avantage est qu'avec cet algorithme, tu as dépensé moins d'énergie, tu n'es pas allé regarder tous les jours sur le site.

Si tu es attentif, tu as remarqué que le **bloc est en programmation impérative** : ce qui est important de comprendre, c'est que **les paradigmes ne sont pas opposés**, on peut les combiner.

## Conclusion

Nous avons vu différents façons de réfléchir pour répondre à différents problèmes. Il existe d'autres paradigmes de programmation, dont certains très connus, que je n'ai pas abordé (fonctionnel, par contraintes, etc.).

Toi aussi dans ta vie réelle, quand tu es face à un problème, essaie de changer de point de vue. Peut-être que tu trouveras ainsi solution plus naturelle.

Tu peux lire la suite de cette série ici: [IMVV — Section 2 — Chapitre 2 — Modes d'exécution synchrone et asynchrone, ou comment réagir au changement](../sync-async/)

[← Retour à la section](../../l-execution/l-execution/)

[← Retour à l’introduction](../../introduction/)