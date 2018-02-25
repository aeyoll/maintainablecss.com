---
layout: chapter
title: Modules
section: Core
permalink: /chapters/modules/
description: Apprenez les différences entre les modules et les composants et comment les identifier dans une conception. Nous allons aussi coder quelques exemples de modules ensemble.
---

## Qu'est-ce qu'un module ?

Un module est une unité distincte et indépendante, qui peut être combinée avec d'autres modules pour former une structure plus complexe.

Dans un salon, on peut considérer la télévision, le canapé et des tableaux comme des modules, tous réunis pour créer une pièce utilisable.

Si on enlève une des unités, les autres fonctionnent encore. On n' a pas besoin de la télé pour s'asseoir sur le canapé etc.

Dans un site web, l'en-tête, le formulaire d'inscription, le panier d'achat, l'article, la liste de produits, la navigation et la promotion de la page d'accueil peuvent tous être considérés comme des modules.

## Qu'est-ce qu'un composant ?

Un module est composé de composants. Sans les composants, le module est incomplet ou cassé.

Par exemple, un canapé est composé d'un cadre, d'un rembourrage, de pieds et de coussins, qui sont tous des éléments nécessaires au bon fonctionnement du canapé.

Un logo *module* peut être constitué d'une image et d'un lien, chacun de ces éléments constituant un composant. Sans l'image le logo est brisé, sans le lien le logo est incomplet.

## Modules vs composants

Il est parfois difficile de décider si quelque chose doit être un composant ou un module. Par exemple, nous pourrions avoir un en-tête contenant un logo et un menu. S'agit-il de composants ou de modules?

Dans un projet récent, il était tout à fait logique que le logo soit un composant et le menu un module à part entière. Qu'est-ce qu'un en-tête sans logo ? Et la navigation peut être déplacée sous l'en-tête.

Personne ne comprend mieux que vous vos exigences. Grâce à l'expérience, vous vous en rendrez compte. Et si vous vous trompez, il est facile de passer d'un composant à un module.

Mais assez de théorie. Construisons ensemble trois modules différents. Nous allons essayer de couvrir la plupart des choses auxquelles nous pensons lorsque nous écrivons du CSS.

## 1. Création d'un module panier

Nous allons simplifier ce panier pour plus de simplicité. Chaque produit dans le panier affichera le titre du produit avec la possibilité de le retirer du panier.

Le modèle de panier pourrait l'être :

	<div class="basket">
	  <h1 class="basket-title">Your basket</h1>
	  <div class="basket-item">
	      <h3 class="basket-productTitle">Product title</h3>
          <form>
              <input type="submit" class="basket-removeButton" value="Remove">
	      </form>
	  </div>
	</div>

Et le CSS serait :

	.basket {}
	.basket-title {}
	.basket-item {}
	.basket-productTitle {}
	.basket-removeButton {}

## 2. Création d'un module récapitulatif de commande

Ensuite, nous allons construire un module récapitulatif de commande. Ce module est affiché lors de l'achat et ressemble un peu au panier. Par exemple, il a un titre et affiche une liste de produits.

Il a cependant une esthétique différente et les produits ne peuvent plus être retirés, c'est-à-dire sans forme et sans bouton de retrait.

La première chose à aborder est la tentation de réutiliser le modèle de panier (et CSS). Même s'il y a des similitudes, cela ne veut pas dire qu'elles sont les mêmes.

Si nous essayons de les combiner, nous allons enchevêtrer deux modules avec la logique d'affichage et des surcharges CSS. Cet enchevêtrement par définition est complexe, difficile à maintenir et facilement évitable.

Au lieu de cela, nous devrions créer un nouveau module avec le modèle suivant :

	<div class="orderSummary">
	  <h2 class="orderSummary-title">Order summary</h2>
	  <div class="orderSummary-item">...</div>
	  <div class="orderSummary-item">...</div>
	</div>

Et le CSS serait :

	.orderSummary {}
	.orderSummary-title {}
	.orderSummary-item {}

Aussi contre-intuitif que cela puisse paraître, la duplication est une meilleure perspective. Et ce n'est pas vraiment une duplication. La duplication consiste à copier la même chose. Ces deux modules peuvent sembler similaires mais ils ne sont pas les mêmes.

Garder les choses séparées, garder les choses simples. La simplicité est l'aspect le plus important de la construction de logiciels fiables, évolutifs et maintenables.

## 3. Création d'un module de boutons

Notre module panier n'apparaissant que dans la page panier, nous n'avons pas envisagé de le réutiliser ailleurs. De plus, nous n'avons pas abordé le fait que le bouton de suppression est un composant du panier, ce qui le rend plus difficile à réutiliser entre les modules.

Les boutons sont un exemple de quelque chose que nous voulons réutiliser dans beaucoup d'endroits, et potentiellement *dans* différents modules. (Un bouton n'est pas particulièrement utile en soi.)

Une option serait de transformer le composant bouton en module comme suit:

	<input class="button" type="submit" value="{%raw%}{{text}}{%endraw%}">

Et le CSS serait :

	.button {}

Le problème est que les boutons ont souvent un positionnement, une taille et un espacement légèrement différents selon le contexte. Bien entendu, il y a aussi les media queries à considérer.

Par exemple, dans un module, un bouton peut être placé à droite à côté d'un texte. Dans une autre, il peut être centré avec un texte en dessous et une marge inférieure.

Idéalement, nous devrions aplanir ces incohérences dans le *design*, avant même qu'elles ne se retrouvent dans le code. Mais comme ce n'est pas toujours possible et aux fins de l'exemple, nous supposerons que nous devons nous occuper de ces questions.

Et donc, à cause de ces différences, il est difficile d'abstraire les règles communes parce que nous ne voulons nous retrouver dans un enfer de surcharges. Ou pire encore, nous avons peur de mettre à jour les règles abstraites CSS.

Pour éviter ces problèmes, nous pouvons utiliser un mixin ou un délimiteur-virgure pour les règles communes qui ne sont pas affectées par leur contexte. Par exemple:

	.basket-removeButton,
	.another-loginButton,
	.another-deleteButton {
      background-color: green;
      padding: 10px;
      color: #fff;
	}

Notez que dans cet exemple, nous ne spécifions pas `float`, `margin` ou `width` etc. Ces styles sont appliqués au bouton unique :

	.basket-removeButton {
	  float: right;
	}

	.another-deleteButton {
	  margin-bottom: 10px;
	}

Cela semble raisonnable car cela signifie que nous pouvons opter pour ces styles communs. Le contraire, bien sûr, étant de devoir faire une surcharge. Mais il y a une troisième option.

Imaginez un tunnel d'achat où chaque page a un bouton Continuer et un lien vers l'étape précédente. Nous pouvons le réutiliser en le transformant en module:

	<div class="checkoutActions">
	  <input class="checkoutActions-continue">
	  <a class="checkoutActions-back"></a>
	</div>

Et le CSS serait :

	.checkoutActions-continue { }

	.checkoutActions-back { }

Ce faisant, nous avons résumé et appliqué les styles à un module `. checkoutActions`. Et nous l'avons fait sans affecter des boutons similaires, mais pas identiques.

Nous n'avons pas encore discuté d'avoir plus d'un type de bouton (primaire et secondaire, etc.). Pour ce faire, nous pouvons utiliser des modificateurs, dont il sera question plus loin.

## Un dernier mot

Un module, par définition, est un bloc réutilisable de HTML et CSS. Avant qu'un groupe d'éléments puisse être transformé en module, il faut d'abord comprendre ce qu'il est et quels sont ses différents cas d'utilisation.

Ce n'est qu'alors que nous pourrons concevoir l'abstraction juste. Et ce faisant, nous évitons la complexité en même temps, qui est la source de CSS non maintenable.
