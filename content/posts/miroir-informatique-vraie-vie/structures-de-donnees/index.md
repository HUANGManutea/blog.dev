---
title: "Autres structure de données, j'organise mon bordel"
#description: <descriptive text here>
date: 2025-04-29T15:41:48-10:00
draft: true
toc: false
image: ""
tags: [Informatique, Miroir de la vraie vie]
categories: [Vulgarisation]
---

Dans le précédent article [File ou Pile ? L'art de passer avant les autres](../file-et-pile/) on a découvert les files et les piles. Cette fois, on va survoler plusieurs autres **structures de données** (*data structures* en anglais) qu'on utilise très souvent en informatique... et dans la vraie vie.

## Le tableau - la base de presque tout

Tu as peut-être remarqué dans le précédent article que la file et la pile se ressemblent beaucoup. En réalité, on peut les représenter toutes les deux avec la même structure : un **tableau**.

En informatique, le tableau (ou *array* en anglais) est l’une des structures les plus simples : on range des éléments les uns à la suite des autres, dans un espace de taille fixe, et chaque élément est repéré par sa position (ou **index**).

Prenons un exemple simple : un tableau d'amis à inviter pour un anniversaire, mais dans mon carnet d'adresse je n'ai que 6 places.

|Amis|Manutea|Vai|Purotu|Heiarii|Reva|(vide)|
|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|

L’**index** est simplement la position de la personne dans le tableau, ce n'est pas un ordre.
Dans la plupart des langages informatiques, l'**index** commence à 0, et pas à 1.
Cet index nous permet d'accéder directement à Vai, l'amie à l'index 2 (ou 3ème élément), pour voir son numéro de téléphone par exemple.

Et ce tableau peut se comporter différemment selon la manière dont on **ajoute** et **retire** les éléments.
Par exemple, on peut le faire fonctionner comme une **file** ou une **pile**, simplement en changeant les règles du jeu.

### Si c'est une file :
- On **ajoute** les amis à la fin. Par exemple, Jean arrive après Reva :
|Amis|Manutea|Vai|Purotu|Heiarii|Reva|Jean|
|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|
- Et on **traite** depuis le début : on retire Manutea du tableau :
|Amis|Vai|Purotu|Heiarii|Reva|Jean|(vide)|
|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|

### Pour une pile :
- On **ajoute** les amis au début. Jean arrive avant Manutea :
|Amis|Jean|Manutea|Vai|Purotu|Heiarii|Reva|
|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|
- Et on **traite** toujours depuis le début : Jean passe en premier :
|Amis|Manutea|Vai|Purotu|Heiarii|Reva|(vide)|
|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|

Dans les deux cas, on utilise un **tableau** pour stocker les amis.
C’est la **logique d’ajout et de retrait** qui transforme ce tableau en pile ou en file.

Et c’est exactement pour ça que, lorsqu’on traite des dossiers empilés, il vaut mieux **commencer par ceux du bas**.
Sinon, on inverse l’ordre d’arrivée… et ce n’est plus une file d’attente, mais une injustice organisée.

Tu as sûrement remarqué un problème: s'il n'y a que 6 places, que se passe-t-il si j'ai 7 amis ?

D'abord, je te félicite d'avoir autant d'amis. Ensuite, on peut s'en sortir, en achetant un carnet d'adresse qui a plus de places, et on recopie nos amis dans ce nouveau carnet.

C'est similaire en informatique, on fait un nouveau tableau, plus grand, et on recopie.

Heureusement, en informatique on a inventé une autre structure.

## La liste - comme le tableau, mais dynamique

La liste (ou *list* en anglais), c’est comme un tableau, **mais en mieux** : **la taille n’est pas fixe**.

Tu peux ajouter ou supprimer des éléments à tout moment, sans te soucier du nombre de places prévues au départ.
Et à tout moment, tu peux demander : “Combien d’éléments j’ai dans cette liste ?” — et obtenir une réponse fiable.

C’est la version souple du tableau, celle qu’on trouve dans la majorité des langages de programmation modernes.

Refaisons les exemples de pile et de file, mais cette fois-ci avec des listes.

### Si c'est une file :
- On **ajoute** les amis à la fin. Par exemple, Jean arrive après Reva :
|Amis|Manutea|Vai|Purotu|Heiarii|Reva|Jean|
|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|

Nombre d'éléments: 6

- Et on **traite** depuis le début : on retire Manutea du tableau :
|Amis|Vai|Purotu|Heiarii|Reva|Jean|
|---|---|---|---|---|---|
|index|0|1|2|3|4|

Nombre d'éléments: 5

### Pour une pile :
- On **ajoute** les amis au début. Jean arrive avant Manutea :
|Amis|Jean|Manutea|Vai|Purotu|Heiarii|Reva|
|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|

Nombre d'éléments: 6

- Et on **traite** toujours depuis le début : Jean passe en premier :
|Amis|Manutea|Vai|Purotu|Heiarii|Reva|
|---|---|---|---|---|---|
|index|0|1|2|3|4|

Nombre d'éléments: 5

On remarque qu'il n'y a plus la case (vide) et le nombre d'élements change.

{{% miroir-informatique-vraie-vie-instant-dev %}}
Pour permettre cette souplesse, la liste est plus gourmande en calculs:
- calcul à la volée du nombre d'éléments,
- réallocation de mémoire.
{{% /miroir-informatique-vraie-vie-instant-dev %}}

Mais en vrai, à moins que tu ne codes un satellite, une carte embarquée, ou une console des années 80, où chaque octet compte, il y a peu de raisons d’utiliser un tableau fixe.
Une liste dynamique t'évitera bien des migraines.

Le tableau et la liste sont des structures très basiques et très puissantes, elles sont les bases de beaucoup d'autres structures qu'on verra par la suite.

## Le tableau associatif - ou comment indexer

On avait pris l'exemple d'un carnet d'adresses qu'on avait mis dans un tableau ou dans une liste. C'est déjà très bien de pouvoir stocker ta liste d'amis, mais si tu as des centaines d'amis et que tu veux appeler Vai pour aller à la mer, tu vas galérer pour chercher dans ce carnet d'adresse.

En effet, avec les 2 dernières structures, tu dois parcourir les éléments un par un, jusqu'à tomber sur Vai. Tu vas perdre beaucoup de temps à chercher son numéro, ça va t'énerver, tu vas l'appeler, lui dire "mais quelle idée d'avoir un prénom qui commence par V!", elle va s'énerver, vous ne serez plus amis, alors que tu voulais juste aller surfer.

Je m'emporte un peu? Peut-être.

Pour résoudre ce problème, en informatique on a inventé le **tableau associatif** (ou *map* en anglais). On utilise le **tableau**, et on va profiter de l'**index** pour justement **indexer** les éléments.

Pour cela, on a besoin de réfléchir un peu:
- On sait que l'index est une position dans le tableau, donc un nombre
- On sait que les prénoms commencent par une lettre (oui, je suis sérieux), on va supposer que c'est une lettre de l'alphabet, et pas un caractère spécial comme *$@
- On sait qu'il y a 26 lettres dans l'alphabet

=> Eurêka:
On peut utiliser la 1ère lettre du prénom, la transformer en index en utilisant sa position dans l'alphabet, et **associer** le prénom à cet index. On dit que l'index est une **clé** et que le prénom est une **valeur** par exemple:

Manutea => M => M est la 14ème lettre de l'alphabet, donc Manutea sera le 14ème élément.
Pour rappel, l'index commence à 0, donc M = index 13.
clé: 13
valeur: Manutea

Pour Heiarii on aura:
clé: 7
valeur: Heiarii

Ce qui nous donne:

|Amis|(vide)|(vide)|(vide)|(vide)|(vide)|(vide)|(vide)|Heiarii|(vide)|(vide)|(vide)|(vide)|(vide)|Manutea|(vide)|Purotu|(vide)|Reva|(vide)|(vide)|(vide)|Vai|(vide)|(vide)|(vide)|(vide)|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|


Avec cette **map**, on pourra facilement accéder aux informations de Vai, puisqu'on pourra juste aller directement à l'index 21.

{{% miroir-informatique-vraie-vie-instant-dev %}}
En vrai, pour calculer l'index, on utilise une fonction de hachage (*hash* en anglais) qui permet de transformer les clés en index. C'est pour ça qu'on appelle ça un **Hash**Map en Java.
{{% /miroir-informatique-vraie-vie-instant-dev %}}

>Oui mais moi je n'ai pas envie de m'embêter à compter sur mes doigts à quelle position est la lettre V...

Tu as raison, dans la vraie vie, dans ton carnet d'adresse pour chaque lettre tu as une encoche où la lettre y est marquée, et tu notes les informations dans les pages qui correspondent à cette lettre.

En informatique c'est le même principe, sauf qu'on ne peut pas utiliser de lettre comme index, alors on est obligé de trouver cette astuce.

>Et en plus, il est nul ton carnet d'adresse, comment je fais si j'ai 2 amis qui s'appellent Vai et Vahine? 
>Je mets Vahine dans la case juste après?
>Et si j'ai des centaines d'amis comme tu le disais au début, je fais comment pour les mettre dans les 26 cases?

Ok, tranquille, pas de stress.

En informatique, on peut combiner les structures, plutôt que d'**associer** un prénom à une lettre, on va associer une **liste** de prénoms à une lettre. Ci-dessous on réécrit notre **map** et on ajoute Vahine :

<table style="text-align: end; border-collapse: collapse; margin-bottom: 1em;">
  <tr>
    <th style="border: 0px"></th>
    <th style="padding: 0 10px;text-align: end;">Clés</th>
    <th style="padding: 0 10px;text-align: end;">7</th>
    <th style="padding: 0 10px;text-align: end;">13</th>
    <th style="padding: 0 10px;text-align: end;">15</th>
    <th style="padding: 0 10px;text-align: end;">17</th>
    <th style="padding: 0 10px;text-align: end;">21</th>
  </tr>
  <tr>
    <td style="border: 0px"></td>
    <td style="border-bottom: 0px"></td>
    <td style="border-bottom: 0px">↓</td>
    <td style="border-bottom: 0px">↓</td>
    <td style="border-bottom: 0px">↓</td>
    <td style="border-bottom: 0px">↓</td>
    <td style="border-bottom: 0px">↓</td>
  </tr>
</table>

<table style="text-align: end; border-collapse: collapse;">
  <tr>
    <td style="border: 0px"></td>
    <td style="border: 0px">
    </td>
    <td style="border: 1px solid var(--border)">
      Heiarii
    </td>
    <td style="border: 1px solid var(--border)">
      Manutea
    </td>
    <td style="border: 1px solid var(--border)">
      Purotu
    </td>
    <td style="border: 1px solid var(--border)">
      Reva
    </td>
    <td style="border: 1px solid var(--border)">
      Vai
    </td>
  </tr>
  <tr>
    <td style="border: 0px"></td>
    <td style="border: 0px">
    </td>
    <td style="border: 0px">
    </td>
    <td style="border: 0px">
    </td>
    <td style="border: 0px">
    </td>
    <td style="border: 0px">
    </td>
    <td style="border: 1px solid var(--border)">
      Vahine
    </td>
  </tr>
</table>

Comme tu l'as remarqué, au lieu de mettre directement les prénoms dans les cases, il y a des flèches qui **pointent vers des listes**. On appelle ça un **pointeur** (ou *pointer* en anglais). c’est un mécanisme qui permet à l’ordinateur de dire *"Va chercher les données ailleurs."*
Plutôt que de stocker directement les valeurs, on stocke l’**endroit** où elles se trouvent.

C'est la plus grande force de l'informatique, on peut combiner différents concepts abstraits pour répondre à notre besoin.

## L'ensemble - une structure unique

Si comme moi tu fais ta liste de courses durant la semaine en prévision des grandes courses du dimanche, tu as peut-être déjà eu la liste qui ressemble à :
- lait
- oeufs
- pops
- viande
- salade
- oeufs

Tu remarques que les **oeufs** apparaissent. On appelle ça un **doublon**.

Ça peut arriver si lundi tu t'es fait une omelette avec les derniers oeufs, tu les as notés pour en racheter.
Puis que vendredi, tu voulais faire un gâteau, mais tu t'es souvenu que tu n'avais plus d'oeufs... et alors tu les as réécrits.

>C'est très spécifique comme explication... C'est ce qui t'es arrivé, pas vrai?

**Tu n'as pas de preuve. Cette accusation est fausse.**

Bref, la liste et le tableau n'ont **aucun moyen d'empêcher la présence de doublons** dans leurs éléments. C'est pour ça qu'en informatique on a inventé l'**ensemble** (ou *set* en anglais), une structure où **chaque élément est unique**.

Par contre, **le set n'est pas ordonné** comme le tableau et la liste. Il n'y a **pas d'index** permettant d'accéder directement au 2ème ou 6ème élément.

{{% miroir-informatique-vraie-vie-instant-dev %}}
En informatique, pour faire un **set**, on utilise en fait une **map** où la clé est l'élément. Le calcul de **hash** nous garantit qu'il ne peut pas y avoir de doublon. Et on met une valeur arbitraire dans la valeur associée, comme 1 ou PRESENT.

Si on veut une structure **ordonnée sans doublons**, on peut :
- coder une liste avec une fonction d'ajout qui rejette les doublons,
- transformer un set en liste,
- utiliser une structure spécialisée, comme **LinkedHashSet** en Java{{% /miroir-informatique-vraie-vie-instant-dev %}}

{{<miroir-informatique-vraie-vie-exemples
    reel="L'ensemble des ingrédients qu’il te reste dans le frigo||L'ensemble des invités à ton anniversaire"
    info="L'ensemble des numéros de passeport en Polynésie française||L'ensemble de tes amis Facebook"
>}}

## Le graphe - ou comment appeler l'ami d'un ami d'un ami

Tu prépares ta liste d’invités pour ton anniversaire, tu comptes inviter tout ton carnet d'adresses.

Et là, tu réalises que tu n’as pas le contact de **Paul**. Tu l'as croisé en soirée et il était cool, tu voudrais l'inviter... mais t'as oublié de lui demander son numéro.

Heureusement, tu sais que **Purotu** le connaît.

Tu l'appelles... zut, elle n'a pas son numéro. Mais elle te donne le numéro de Tiare, une autre amie de Paul.
Tu appelles **Tiare**, tu te présentes, tu l'invite également car tu n'es pas un sauvage. Et tu lui demandes le numéro de Paul.

**Bingo**, elle l'a, tu appelles Paul et il est chaud pour venir à ton anniversaire.

Les liens entre ces personnes peuvent être représentés par un **graphe** (ou *graph* en anglais).

Et ce que tu viens de faire, sans t'en rendre compte, c'est un **parcours de graphe**, un algorithme !

{{< mermaid >}}
---
title: Graphe de relation entre les personnes
---
graph TD
    A[Toi] --- B[Manutea]
    A --- C[Vai]
    A --- D[Purotu]
    A --- E[Heiarii]
    A --- F[Reva]
    A --- G[Jean]
    D --- H[Tiare]
    H --- I[Paul]
{{< /mermaid >}}

Ce graphe est **non orienté**, c'est-à-dire qu'il n'y a pas de sens entre les éléments.

Effectivement pour éviter de fâcher les personnes, on ne va pas dire *"Purotu est l'ami de Tiare, mais Tiare n'est pas l'ami de Purotu"*.

Par contre, on peut utiliser un graphe **orienté** pour représenter les appels que tu as passé.

{{< mermaid >}}
---
title: Graphe des appels que tu as passé
---
graph TD
    A[Toi] --> B[Manutea]
    A --> C[Vai]
    A --> D[Purotu]
    A --> E[Heiarii]
    A --> F[Reva]
    A --> G[Jean]
    A --> H[Tiare]
    A --> I[Paul]
{{< /mermaid >}}

**On a donc les mêmes données, mais on utilise la structure adaptée à ce qu'on veut représenter.**

>Et c'est quoi le parcours de graphe?

Je suis heureux que tu poses cette question, mais ta question dépasse le cadre de cet article.

Si tu souhaites continuer cette aventure, tu peux regarder la suite ici: [Structures de contrôle et algorithme, apprendre à réfléchir](../structures-de-controle/)

On a déjà vu pas mal de choses, je te laisse relire, essayer de combiner les structures entre elles, te renseigner sur internet en cherchant "structure de données" ou "data structure".

Il existe beaucoup de structures de données, celles qui sont présentées dans cet article sont juste les plus basiques, celles qu'on apprend dans les premières heures de cours de programmation.

[← Retour à l’introduction](../introduction/)
