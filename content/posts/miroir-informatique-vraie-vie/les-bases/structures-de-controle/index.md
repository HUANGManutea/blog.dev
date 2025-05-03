---
title: "IMVV — Section 1 — Chapitre 3 — Structures de contrôle et algorithme, apprendre à réfléchir"
weight: 3
#description: <descriptive text here>
date: 2025-04-30T14:30:37-10:00
draft: false
showToc: true
image: ""
tags: [Informatique, IMMV]
categories: [Vulgarisation]
---
Dans l'article précédent [IMVV — Section 1 — Chapitre 2 — Autres structures de données, j'organise mon bordel](../structures-de-donnees/), on s'était arrêté sur ta question :

>Et c'est quoi le parcours de graphe?

Dans cet article, on va parler des **structures de contrôle** (*control flow statements* en anglais), qu'on utilise dans des **algorithmes** (*algorithms* en anglais).

Avant d'expliquer l'algorithme que tu as fait, le **parcours de graphe**, on doit expliquer les structures de contrôle.

N'oublie pas que les objectifs de ces articles sont :
- Te donner une meilleure compréhension des bases de l’informatique,
- T'inspirer pour analyser ou optimiser les situations du quotidien,
- ou peut-être, qui sait, te donner envie d'explorer encore plus loin... jusqu’à en faire ton métier.

## Pseudo-code — l'art de la cuisine

Quand tu fais un gâteau, tu réalises les actions suivantes:

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

Toute cette suite d'étapes est ce qu'on appelle un **algorithme**, et la façon dont on l'a écrit, ça s'appelle du **pseudo-code**, parce que ça ressemble à un langage de programmation, mais ce n'en est pas un.

>Mais pourquoi on appelle ça un algorithme? on peut pas juste dire une suite d'actions?

Je te laisse chercher sur internet pourquoi on appelle ça un [algorithme](https://fr.wikipedia.org/wiki/Algorithme).

## La boucle for — ou comment être *fiu*

Ton meilleur ami Manutea te demande *"Comment tu as fait pour inviter toutes ces personnes à ton anniversaire ?"*. Laquelle de ces 2 phrases dirais-tu :
- J'ai appelé Manutea, puis j'ai appelé Vai, puis j'ai appelé Purotu, puis j'ai appelé Heiarii, puis j'ai appelé Reva, puis j'ai appelé Jean, puis j'ai appelé Tiare, puis j'ai appelé Paul
- J'ai pris mon carnet d'adresses, puis **pour chaque** contact, j'ai appelé le numéro correspondant

La 1ère phrase est un **algorithme** sans **boucle** (*loop* en anglais) : chaque action est écrite explicitement.

La 2ème, elle, utilise une **boucle** — tu répètes la même action pour chaque contact.
Sans forcément y penser, tu utilises aussi une **variable** : un espace dans ta tête pour mémoriser un numéro, que tu remplaces à chaque nouvel appel.

Cette manière de répéter une action avec une variable, c’est exactement ce qu’un ordinateur fait quand on lui demande de parcourir une liste.

Si tu relis bien la 2ème phrase, tu verras que **pour chaque** est en gras. En anglais, *pour chaque* se dit *for each*, c'est pour ça qu'on l'appelle la **boucle for** dans la plupart des langages.

Si on essayait d'écrire un **algorithme**, sous forme de **pseudo-code** simple pour décrire la 2ème phrase, ça donnerait :

```
Dans mon carnet d'adresses, pour chaque contact:
    J'ai appelé le numéro correspondant au contact
    J'ai invité l'ami
Fin pour
```

*"Dans mon carnet d'adresses, pour chaque contact"* marque le **début** de la boucle, et *"Fin pour"* marque la **fin** de la boucle.

Entre ces 2 lignes, les actions *"J'ai appelé le numéro correspondant au contact"* et *"J'ai invité l'ami"* forment ce qu'on appelle un **bloc** d'instructions.

Par convention, on **indente** ce bloc — on le décale vers la droite — pour montrer visuellement qu'il est à l'intérieur de la boucle.

>Ok, et quel est le rapport entre la boucle for et *fiu* comme marqué dans le titre ?

Si on devait écrire l'algorithme de la 1ère phrase, ça donnerait :
```
J'ai appelé Manutea
J'ai appelé Vai
J'ai appelé Purotu
J'ai appelé Heiarii
J'ai appelé Reva
J'ai appelé Jean
J'ai appelé Tiare
J'ai appelé Paul
``` 

Chaque ligne est une action, donc il faut écrire autant de lignes qu'il y a de contacts dans ta liste de contacts. Maintenant, que se passerait-il si tu devais inviter 100 personnes? Tu serais *fiu*.

Alors qu'avec la boucle, tu n'as pas besoin de changer ton algorithme, c'est le même, que tu aies 6 contacts ou 100.

>Oui mais dans la vraie vie je dois quand même appeler les amis un par un

Cet exemple n’est pas là pour dire que tu vas programmer ton téléphone —
mais pour te faire sentir la puissance de la boucle : un seul bloc, quelle que soit la longueur de ta liste.

Dans la vraie vie, tu fais un groupe Facebook avec tous tes amis et tu postes des messages d'informations dans le groupe pour organiser, idem pour un groupe SMS. Si t'es old school, tu postes un message dans le journal local et viendra qui verra. D'ailleurs j'en parlerai dans de prochains articles.

## La boucle while — ou comment faire ses devoirs avant d'aller jouer

Quand tu étais plus jeune, on t'a sûrement déjà dit *"Fais d'abord tes devoirs, ensuite tu peux aller jouer"*, ou autrement dit *"**Tant que** tu n'a pas fini tes devoirs, tu travailles, ensuite tu peux aller jouer"*.

Si on devait écrire cet algorithme, ça donnerait:

```
Tant que je n'ai pas fini mes devoirs:
    Je fais mes devoirs
Fin tant que

Je vais jouer
```
*"Tant que je n'ai pas fini mes devoirs"* marque le **début** de la boucle, et "Fin tant que" marque la **fin** de la boucle.

Entre ces 2 lignes, l'action *"Je fais mes devoirs"* forme le **bloc** d'instructions.

Tu l'auras remarqué, c'est très similaire à la **boucle for**, sauf qu'au lieu de parcourir des éléments, on vérifie une **condition**, et on répète la boucle si la condition n'est remplie.

On appelle ça une **boucle while**, car *Tant que* se dit *while* en anglais.

Ensuite, une fois que les devoirs sont finis, on *sort de la boucle*, on fait la suite des instructions, donc *"Je vais jouer"*. On aurait aussi pu avoir d'autres instructions après la **boucle for**, c'est juste que l'exemple ne s'y prêtait pas.

>Mais alors… pourquoi deux types de boucles si elles font (presque) la même chose ? Pourquoi une boucle for, et une boucle while ?

En fait, en fonction du problème qu'on veut résoudre :
- dans certains cas on pourra compter, et dans ce cas on préfèrera utiliser une **boucle for**
- dans certains cas on ne pourra pas compter, et dans ce cas on préfèrera utiliser une **boucle while**

Par exemple, pour un enfant qui joue dehors:

```
Tant qu'il fait beau:
    Je joue
Fin tant que
```

Ici, impossible de compter.

Mais tu commences peut-être à te rendre compte d'une supercherie.

{{% miroir-informatique-vraie-vie-instant-dev %}}
💡 En réalité, **toutes les boucles for peuvent être réécrites en boucle while**.  
La **boucle for** n’est qu’une **boucle while optimisée**, écrite pour être plus simple à lire… quand on sait compter.

Les 2 types de boucles sont des **instructions d'itération**, à la différence des **instructions** simples comme *"Je joue"*, les **instructions d'itération** permettre d'exécuter des **blocs** d'instructions de manière répétée.
{{% /miroir-informatique-vraie-vie-instant-dev %}}

Bravo, tu commences à réfléchir comme un développeur !

**Explications**

Pour rappel:
- dans une liste, l'index commence à 0,
- dans une liste, le dernier index est égal au nombre d'éléments de la liste moins 1
|Amis|Manutea|Vai|Purotu|Heiarii|Reva|Jean|Tiare|Paul|
|---|---|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|6|7|

Nombre d'éléments: 8

- une variable c'est juste un espace mémoire où on stocke une donnée (un tableau, une liste, un prénom, un numéro de téléphone)

Si on reprend l'exemple de la **boucle for**:

```
Dans mon carnet d'adresses, pour chaque contact:
    J'appelle le numéro correspondant au contact
    J'invite l'ami
Fin pour
```

Derrière, voici plutôt ce que fait un ordinateur (de manière simplifiée) :

```
Je crée une variable "index", qui vaut 0
Tant que "index" est inférieur au nombre d'éléments (8) du carnet d'adresses:
    Je regarde le contact qui se trouve à l'"index" dans le carnet d'adresses
    Je récupère son numéro
    Je l'invite
    "index" prend la valeur "index" + 1
Fin tant que
```

Comme tu le vois, c'est un peu plus compliqué, c'est pour ça qu'on préfère utiliser une **boucle for** quand on peut compter.

## L'instruction conditionnelle — ou pourquoi il faut respecter le code de la route

Juste au-dessus, on parlait de **condition** dans la **boucle while**. Mais on n'a jamais expliqué ce que c'était.

Une condition est une question qu'on se pose, et la réponse est soit “oui”, soit “non” — jamais les deux, jamais "un peu".

Quand on écrit *"Tant que je n'ai pas fini mes devoirs"*, à chaque répétition on pose la question "Est-ce que j'ai fini mes devoirs?".

En informatique, comme dans la vraie vie, une condition doit être claire.

On peut utiliser ce concept pour faire des branchements dans notre code, dans une **instruction conditionnelle** (*conditional statement* en anglais).

Prenons un exemple simple : tu es en voiture, tu approches un feu tricolore. Il est vert.

Que fais-tu si le feu passe à l’orange juste devant toi ?

Voici un algorithme qui représente cette situation :

```
Si le feu passe au orange, alors:
    Tu t'arrêtes
Sinon (c'est toujours vert):
    Tu continues et traverse l'intersection
Fin si
```

*"Si le feu passe au orange,"* marque le **début** de l'instruction conditionnelle, *"alors"* marque la **branche** du **si**, *"Sinon"* marque la **branche** du sinon, et *"Fin si"* marque la fin de l'instruction conditionnelle.

De la même manière que pour les **boucles**, chaque **branche** est un **bloc** d'instructions. Comme pour les boucles, chaque branche forme un bloc d’instructions, qu’on indente pour bien le repérer. 

Pour visualiser, imagine un arbre : chaque fois qu’une condition est testée, tu choisis une **branche** à suivre. Le chemin dépend de tes réponses.

## Revenons à notre parcours de graphe

### Rappels

Tu avais appelé tes amis pour les inviter à ton anniversaire, et tu avais été jusqu'au bout du monde, en sautant de relations en relations, pour inviter Paul. Tu avais fait ces actions :

```
Tu comptes inviter tout ton carnet d'adresses.

Tu réalises que tu n’as pas le contact de Paul. Tu l'as croisé en soirée et il était cool, tu voudrais l'inviter... mais t'as oublié de lui demander son numéro.

Heureusement, tu sais que Purotu le connaît.

Tu l'appelles... zut, elle n'a pas son numéro. Mais elle te donne le numéro de Tiare, une autre amie de Paul.
Tu appelles Tiare, tu te présentes, tu l'invites également car tu n'es pas un sauvage. Et tu lui demandes le numéro de Paul.

Bingo, elle l'a, tu appelles Paul et il est chaud pour venir à ton anniversaire.
```

Ci-dessous se trouve le graphe de relation entre les personnes, un graphe **non orienté**.

<figure>
{{< mermaid >}}
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
<figcaption>Graphe de relation entre les personnes</figcaption>
</figure>

En se basant sur ce qu'on a appris dans cet article, on va écrire un algorithme pour représenter les actions que tu as réalisées pour inviter tes amis :

```
# Étape 1 : inviter tous mes amis directs (les noeuds les plus proches de "Toi" dans le graphe)
Je crée une variable "liste d'amis", contenant tous mes amis directs
Je crée une variable "ami", le contact courant

Dans la "liste d'amis", pour chaque "ami" :
    J'appelle "ami"
    Si "ami" répond, alors :
        Je l'invite à mon anniversaire
    Fin si
Fin pour

# Étape 2 : retrouver Paul (en parcourant le graphe en largeur)
Je crée une variable "file", initialisée avec la "liste d'amis"
Je crée une variable "visités", une liste vide

Tant que la "file" n’est pas vide :
    Je prends le premier élément de la "file", je le stocke dans "ami"
    Si "ami" n’est pas dans "visités", alors :
        J’ajoute "ami" à "visités"
        J'appelle "ami"
        Si "ami" répond, alors :
            Je lui demande s’il connaît Paul
            Si "ami" me donne le numéro de Paul :
                Je crée une variable "Paul"
                J'appelle "Paul"
                Si "Paul" répond, alors :
                    Je l’invite à mon anniversaire
                    Je termine la recherche
                Fin si
            Sinon :
                Je récupère la liste des amis de "ami"
                Pour chaque "contact" dans cette liste :
                    J’ajoute "contact" à la "file"
                Fin pour
            Fin si
        Fin si
    Fin si
Fin tant que
```

À première vue, ça a l'air compliqué. Mais en fait si tu prends le temps de décortiquer, de bien regarder, tu verras que ce sont juste les actions que tu as réalisés plus haut, mais dans un langage plus proche de ce que fait un ordinateur.

La seule chose qu'on a fait en plus des concepts de base, c'est qu'on a combiné les structures de contrôle et les structures de données, et le tout nous donne notre **algorithme de parcours de graphe** !

{{% miroir-informatique-vraie-vie-instant-dev %}}
💡 On a parcouru le graphe en largeur, c'est-à-dire qu'on a d'abord regardé les noeuds voisins de notre point de départ.

D'autres algorithmes connus et enseignés en informatique sont le parcours en profondeur, l'algorithme de Dijkstra, A* et Floyd-Warshall, tu peux regarder sur internet si ça t'intéresse.
{{% /miroir-informatique-vraie-vie-instant-dev %}}

## Conclusion

Dans cet article on a appris ce que sont :
- Les structures de contrôle,
    - Les boucles,
    - Les conditions,
- Les variables,
- Les algorithmes.

Il existe d'autres structures de contrôle, des types de variables, et des algorithmes qu'on peut réutiliser pour répondre à beaucoup de problèmes. Comme d'habitude, je te laisse chercher sur internet si tu veux aller plus loin.

Mais le plus important, c'est que tu commences à réfléchir comme un développeur, et à comprendre le **pseudo-code**. Dans la vraie vie, si tu as un problème complexe à résoudre, tu peux essayer de l'écrire comme on l'a fait pour le parcours de graphe. Prends ton temps et décompose le problème.

Nous avons fini cette section "IMMV — Section 1 — Les Bases : structures et contrôle", dans cette section, nous avons également vu les structures de données.

Dans la prochaine section, [IMMV — Section 2 — L'exécution : comment faire des actions ?](../../l-execution/l-execution/), nous verrons que l'ordinateur et l'humain font les actions de manière très similaire.

[← Retour à la section](../../les-bases/les-bases/)

[← Retour à l’introduction](../../introduction/)
