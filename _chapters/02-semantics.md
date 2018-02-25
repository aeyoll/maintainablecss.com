---
layout: chapter
title: Semantics
section: Background
permalink: /chapters/semantics/
description: Pourquoi nommer quelque chose en fonction de ce qu'il est, au lieu de la façon dont il ressemble ou se comporte est le fondement d'un CSS bien conçu et maintenable.
---

Le HTML sémantique ne concerne pas seulement les éléments que nous utilisons. Il est assez évident que nous devrions utiliser `<a>` pour les liens, `<table>` pour les données tabulaires et `<p>` pour les paragraphes etc. Ce qui est moins évident, ce sont les noms que nous utilisons pour les classes.

Comme le dit Phil Karton, "il n'y a que deux choses difficiles en informatique : l'invalidation de cache et **nommer des choses**." Il semble donc approprié de passer un chapitre entier à en parler.

Le nommage est franchement l'aspect le plus important de la rédaction de CSS maintenable. Il existe deux approches principales : l'approche sémantique et l'approche non sémantique. Discutons de ce que c'est.

## Sémantique vs non-sémantique

	<!-- non sémantique -->
	<div class="red pull-left pb3">
	<div class="grid row">
	<div class="col-xs-4">

	<!-- semantique -->
	<div class="basket">
	<div class="product">
	<div class="searchResults">

Les classes non sémantiques ne transmettent pas ce qu'un élément *représente*. Au mieux, ils nous donnent une idée de ce qu'un élément *ressemble*. Les classes atomiques, visuelles, comportementales et utilitaires sont toutes des formes de classes non sémantiques.

Les classes sémantiques ne transmettent pas leur style. C'est à cela que sert CSS. Les classes sémantiques signifient quelque chose pour HTML, CSS, Javascript et les tests fonctionnels automatisés.

Voicei les raisons pour lesquelles les classes sémantiques fonctionnent mieux :

## 1. Parce qu'elles sont lisibles

Voici un vrai morceau de HTML utilisant des classes atomiques :

	<div class="pb3 pb4-ns pt4 pt5-ns mt4 black-70 fl-l w-50-l">
	  <h1 class="f4 fw6 f1-ns lh-title measure mt0">Heading</h1>
	  <p class="f5 f4-ns fw4 b measure dib-m lh-copy">Tagline</p>
	</div>

- Il est plus facile de lire des mots que des abréviations. Les abréviations doivent être décomposées et cartographiées cognitivement, en supposant que nous sachions ce qu'elles signifient au départ.
- Il est difficile de lire un grand groupe de noms de classe. C'est pourquoi CSS a une syntaxe. Nous avons besoin de parcourir de nombreuses classes pour savoir ce qui se passe, quelles sont les classes qui l'emportent sur lesquelles, et qui s'appliquent à certains points de rupture, etc.
- Ces classes sont ambiguës. Par exemple, est-ce que `black-70` fait référence à la couleur ou au fond ? Si nous avons besoin de l'inspecteur pour le découvrir, cela implique que les noms de classe ne sont pas lisibles.
- Le contenu est occulté par le HTML environnant.

Voici la même chose en utilisant des classes sémantiques :

	<div class="hero">
	  <h1 class="hero-title">Heading</h1>
	  <p class="hero-tagline">Tagline</p>
	</div>

- Ces classes sont faciles à lire. Aucune cartographie mentale n'est requise.
- Le contenu n'est plus occulté.
- Nous savons où le module commence et se termine.
- Le HTML est deux fois plus petit.
- Il est facile de lire le CSS (dans l'inspecteur ou dans le fichier) car il possède déjà des constructions de langage dédiées qui existent à cet effet.

## 2. Parce qu'il est plus facile de construire des sites responsives

Imaginez coder une grille réactive à deux colonnes par laquelle:

- Chaque colonne a un padding de `20px` et `50px` sur petits et grands écrans;
- Chaque colonne a des polices de caractères `2em` et `3em` sur petits et grands écrans; et
- Les colonnes s'empilent sur de petits écrans. Notez que *colonne* est maintenant un nom de classe trompeur.

Avec les classes visuelles/utilitaires, ça ressemble à ceci :

	<div class="grid clearfix">
	  <div class="col pd20 pd50 fs2 fs3">Column 1</div>
	  <div class="col pd20 pd50 fs2 fs3">Column 2</div>
	</div>

- Il y a 7 classes, dont certaines se superposent.
- Pour rendre les colonnes réellement responsive nous aurions besoin d'une classe `fs3large` etc. Il s'agit d'utiliser une convention de nommage qui recrée des constructions de langage déjà trouvées et standardisées dans CSS.
- A certains points de rupture, les classes sont trompeuses et redondantes. Par exemple, `.clearfix` ne s'efface pas sur les petits écrans.

Une évaluation rapide montre déjà une douleur importante.

Avec les classes de sémantique, il ressemble à ceci :

	<div class="thing">
	  <div class="thing-thingA"></div>
	  <div class="thing-thingB"></div>
	</div>

- Ces classes sont encapsulées selon la conception et le contenu du module.
- Il est facile de styliser des éléments sans avoir à écrire une multitude de classes et de changer de nouveau le HTML.
- Ces classes ont du sens dans les petits et grands écrans.
- Les media queries peuvent être utilisées pour effacer des éléments que si nécessaire.

> Question : Quelle est la valeur d'un système de grille réactive codifiée ? Une[mise en page doit s'adapter au contenu](http://adamsilver.io/articles/stop-using-device-breakpoints/), et non l'inverse.

## 3. Parce qu'elles sont plus faciles à trouver

La recherche de HTML avec une classe non-sémantique donne beaucoup de résultats. Comme les classes sémantiques sont uniques, une recherche ne donne qu'un seul résultat, ce qui facilite la recherche du code HTML.

## 4. Parce qu'elles éliminent le risque de régression

La mise à jour d'une classe visuelle peut provoquer une régression à travers une multitude d'éléments. La mise à jour d'une classe sémantique ne s'applique qu'au module en question, ce qui élimine toute régression.

## 5. Parce que les classes visuelles n'en valent pas la peine.

A certains égards, nous pouvons aussi bien faire des styles inligne. Ceci est plus explicite et réduit l'empreinte CSS à zéro. Inline CSS est un problème cependant, car nous ne pouvons pas utiliser les media queries par exemple. Dep plus, placer le CSS dans le HTML mélange les problèmes et supprime la possibilité de le mettre en cache.

> Question: Est-ce que `. red` n'est pas exactement la même abstraction que CSS nous donne déjà gratuitement avec `color: red` ?

## 6. Parce qu'elles fournissent des hooks pour les tests automatisés

Les tests fonctionnels automatisés fonctionnent en recherchant des éléments et en interagissant avec eux. Cela peut inclure:

1. cliquer sur un lien
2. trouver une zone de texte
3. la saisie de texte
4. soumettre un formulaire
5. vérifier certains critères

Nous ne pouvons pas utiliser des classes non sémantiques pour cibler des éléments spécifiques. Et l'ajout des hooks spécifiques pour les tests est un gaspillage puisque l'utilisateur doit télécharger ces choses.

## 7. Parce qu'ils fournissent des hooks pour Javascript

Nous ne pouvons pas utiliser des classes non sémantiques pour cibler des éléments spécifiques afin de les améliorer avec Javascript.

## 8. Parce qu'elles n'ont pas besoin de maintenance

Si nous nommons une chose en fonction de ce qu'elle est, nous n'aurons pas besoin de mettre à jour le HTML à nouveau, par exemple un titre est toujours un titre, peu importe à quoi il *ressemble*.

Avec les classes visuelles, le HTML et le CSS doivent être mis à jour (en supposant qu'il n'y ait pas de sélecteurs disponibles).

## 9. Parce qu'elles sont plus faciles à déboguer

Inspecter un élément avec une multitude de classes atomiques, c'est passer à travers de nombreux sélecteurs. Avec un cours de sémantique, il n'y en a qu'un seul, ce qui rend le travail beaucoup plus facile.

## 10. Parce que les normes le recommandent

Lors de l'utilisation de l'attribut class, les spécifications HTML5 disent en 3.2.5.7:

> "[...] les auteurs sont encouragés à utiliser des valeurs qui décrivent la nature du contenu plutôt que des valeurs qui décrivent la présentation souhaitée du contenu."

## 11. Parce que styliser un statut est plus simple

Considérons le HTML suivant :

	<a class="padding-left-20 red" href="#"></a>

Il est difficile de changer le padding et la couleur au survol. Il vaut mieux éviter d'avoir à régler des problèmes auto-induits comme celui-ci.

## 12. Parce qu'elles produisent une petite empreinte HTML

Comme nous l'avons vu plus haut, les classes atomiques surchargent le HTML. Les classes sémantiques se traduisent par un HTML plus petit. Et alors que le CSS peut augmenter en taille, il est cachable.

## Un dernier mot

Les classes sémantiques sont une pierre angulaire de *MaintainableCSS*. Sans eux, tout le reste n'a pas de sens. Nommez quelque chose en fonction de ce qu'il est et tout le reste se met en place.