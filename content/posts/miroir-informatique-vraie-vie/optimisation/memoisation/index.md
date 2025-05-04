---
title: "IMVV — Section 3 — Chapitre 2 — Mémoïsation et Lazy loading, les techniques du fainéant ultime"
#description: <descriptive text here>
date: 2025-05-03T09:43:10-10:00
draft: false
weight: 2
showToc: true
image: ""
tags: [Informatique, IMVV]
categories: [Vulgarisation]
---
Dans l'article précédent [IMVV — Section 3 — Chapitre 1 — La mémoire, ou comment éviter les pénuries dans un magasin](../memoire/), on a vu qu'on pouvait optimiser notre utilisation de la mémoire / du stockage... Mais ce n'est pas suffisant, on doit voir d'autres ~~jutsu~~ techniques pour optimiser encore plus.

Être *fiu* est un art, une vertu. **Non, ce n'est pas une blague**. Tu ne me crois pas ?

*"We will encourage you to develop the three great virtues of a programmer: laziness, impatience, and hubris." — Larry Wall, Programming perl (1991)*.

*"I choose a lazy person to do a hard job. Because a lazy person will find an easy way to do it." — Bill Gates*.

Programmer une machine pour qu'elle fasse le travail à ta place, c'est de la fainéantise.

Et les développeurs sont des personnes qui ont atteint l'apogée du *fiu*. Après tout, qui passe 2 heures à automatiser une tâche qui prend 2 minutes par jour, à part quelqu'un de **vraiment** *fiu* ?

Dans cet article, on verra deux techniques que les développeurs utilisent, mais que toi aussi tu utilises sans le savoir.

## Mémoïsation — ou comment garder une information dans un coin de la tête

Supposons que tu sois responsable de la paie dans une petite entreprise. Pour ce mois-ci, tu dois calculer les salaires à verser à 2 employés.

Tu sais que tous les deux ont un salaire brut de 200 000 XPF. De plus, ils ont fait un excellent travail, ton patron t'a dit de leur rajouter une prime de 50% de leur salaire brut. Enfin, l'un d'eux a fait des heures supplémentaires, il faut donc lui rajouter 20 000 XPF brut sur sa paie.

Pour le 1er salarié, tu pars de 200 000, tu rajoutes 50%, soit 100 000, ce qui lui fera 300 000 XPF brut pour ce mois.

Pour le 2ème salarié, tu sais que le début du calcul est le même, alors tu réutilises le nombre 300 000, et tu rajoutes 20 000 d'heures supplémentaires, donc 320 000 bruts.

Mais tu t’es souvenu que le calcul *200 000 + 50 %* avait déjà été fait, donc tu as directement repris le résultat. Ce que tu viens de faire, c'est de la **mémoïsation** (*memoization* en anglais).

C’est exactement ce que fait ton navigateur web quand il te propose un résultat de recherche déjà visité, ou qu’un site charge plus vite la 2ᵉ fois.

{{% miroir-informatique-vraie-vie-instant-dev %}}
En informatique, on utilise un tableau ou un tableau associatif pour stocker les résultats intermédiares, ces structures sont stockées dans la RAM. De cette façon, on peut rapidement récupérer le résultat qui nous intéresse.
{{% /miroir-informatique-vraie-vie-instant-dev %}}

Attention : En informatique, comme dans la vraie vie, garder des informations de côté peut conduire à une saturation de la mémoire. C'est un des facteurs de burn-out. **Ménagez votre cerveau**, il n'y a pas de mal à noter les choses, de plus, vous aurez moins de risque d'oublier des informations importantes.

## Eager loading et Lazy loading — l'art d'être préparé à toute éventualité

Supposons que tu aies invité tes amis à manger à la maison ce soir. Tu as invité 10 personnes, mais tu sais que 5 vont vraiment venir, les autres t'ont dit "peut-être".

Pour éviter d'être à court de nourriture, tu as préparé pour 10 personnes, au pire, ceux qui sont venus repartiront avec quelques plats, et tu termineras le reste durant la semaine.

Les premiers invités vont arriver, tu n'as pas encore préparé la table. Tu as 2 solutions :
- **Tout préparer d'avance** : sortir toutes les assiettes, les verres, les chaises, les couverts, etc. (solution **eager loading** : tu charges tout dès le début).

- **Attendre de voir qui arrive** : dès qu’un invité entre, tu sors une assiette, un verre, une chaise, etc. (solution **lazy loading** : tu ne charges que ce qui est nécessaire, au moment où c’est nécessaire).

>Mais tu peux aussi exiger des invités qu'ils te disent, la veille au plus tard, si oui ou non ils viennent !

Oui, et que se passe-t-il si l'un d'eux a un empêchement ? En mettant tous les couverts, tu as dépensé de l'énergie pour mettre son couvert, et tu en as re-dépensé pour le ranger. Ce n'est pas très optimisé.

>Si tous les invités arrivent, tu auras fait plusieurs allers-retours pour mettre les couverts, ce n'est pas très optimisé non plus...

Ah, tu mets le doigt sur un point important : **les techniques d'optimisation doivent être utilisées uniquement si on est sûr de leur utilité**.

*"Premature optimization is the root of all evil" — Sir Tony Hoare et Donald Knuth*.

C'est un piège dans lequel tombent plusieurs développeurs juniors. Les écoles supérieures enseignent différentes techniques d'optimisation, on est conditionnés à détecter un problème et à appliquer immédiatement une solution : c'est normal.

Avec l'expérience, on apprend qu'on a besoin d'optimiser uniquement quand une personne se plaint de lenteurs. Et dans ce cas, **on cherche où se trouve la source du problème, on mesure, puis on optimise**. 

>Ok mais... ça me fait bizarre de ne pas préparer une belle table, c'est pas un bon accueil.

Dans ce cas, le **eager loading** a une vraie plus-value. Tu charges tout d'un coup pour l'effet *waow*, pour que les personnes se disent que chez toi, on est bien reçu. La principale fonctionnalité n'est pas d'optimiser le fait de mettre la table, mais d'impressionner tes convives.

Je finis cette partie avec un exemple informatique : Facebook ne charge pas toutes les publications dès le début, seulement une partie.

Quand tu commences à scroller, tu vois ces publications. Si tu te rapproches de la fin, Facebook charge les prochaines publications, on appelle ça **infinite scroll**.

Ainsi, Facebook ne prend pas trop de temps à se charger au début.

>Attends mais... Dans l'article précédent, on parlait des écrans de chargement des jeux vidéos, ça y ressemble un peu, non ?

Exactement, les écrans de chargement sont aussi du **lazy loading**, et pour rejoindre ce qu'on disait sur ces écrans : **le lazy loading économise de la mémoire**.

Enfin, à ton avis, comment Facebook sait qu'il faut charger la suite des publications ?

Eh bien en fait, l'application est **réactive**, on peut écrire son **algorithme de chargement** comme ceci:

```
Quand un certain seuil de scroll est atteint (par exemple, 90% du contenu affiché), alors:
    Charge la suite du contenu
    Passe à autre chose
Fin quand
```

Tu l'auras remarqué, c'est de la **programmation réactive**, ce qu'on a vu dans l'article [IMVV — Section 2 — Chapitre 1 — Paradigmes, ou comment réfléchir différemment](../../l-execution/paradigme/).

## Conclusion

Dans cet article, on a vu différents mécanimes d'optimisation.

Plus important encore, si on se rappelle des précédents articles, on a vu qu'en informatique, en plus de combiner les **structures de données** et les **structures de contrôle**, on pouvait combiner les concepts d'**optimisation** et de **modes d'exécution**.

Le prochaine article est **en cours de rédaction**, on parlera de *complexité*.

[← Retour à la section](../../optimisation/optimisation/)

[← Retour à l’introduction](../../introduction/)