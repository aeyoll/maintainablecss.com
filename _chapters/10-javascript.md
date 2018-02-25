---
layout: chapter
title: Javascript
section: Extras
permalink: /chapters/javascript/
description: Comment écrire en même temps du CSS et du Javascript maintenable.
---

Nous pouvons utiliser Javascript pour appliquer le même comportement à plusieurs modules ou composants.

Par exemple, nous pouvons utiliser un constructeur `Collapser` qui bascule la visibilité d'un élément.

Nous pouvons adopter deux approches, qui complètent l'approche de la SCN dont nous avons discuté dans les chapitres précédents.

## 1. Etat d'encapsulation du module

Pour ce faire, il faudrait spécifier une classe d'état spécifique au module au constructeur comme suit :

	var module1Collapser = new Collapser(element1, {
	  cssHideClass: 'moduleA-isHidden'
	});

	var module2Collapser = new Collapser(element2, {
	  cssHideClass: 'moduleB-isHidden'
	});

Puis réutilisez les styles CSS comme suit :

	.moduleA-isHidden,
	.moduleB-isHidden {
      display: none;
	}

L'arbitrage est que cette liste pourrait croître rapidement (ou utiliser un mixin). Et chaque fois que nous ajoutons un nouveau comportement, nous devons mettre à jour le CSS. Un petit changement, mais un changement quand même. Dans ce cas, nous pourrions envisager une classe d'état globale.

## 2. Créer une classe d'état globale

Si nous nous trouvons à répéter exactement le même ensemble de styles pour plusieurs modules, il peut être préférable d'utiliser une classe d'état globale comme suit :

	.globalState-isHidden {
      display: none;
	}

Cette approche élimine la longue liste délimitée par des virgules. Et nous n'avons plus besoin de spécifier la classe module lors de l'instanciation. C'est parce que la classe globale sera référencée de l'intérieur.

	var module1Collapser = new Collapser(element1);
	var module2Collapser = new Collapser(element2);

Cependant, cette approche n'a pas toujours un sens. Il se peut que nous ayons deux modules différents qui se comportent de la même façon, mais *s'affichent* différement, ce qui est quelque chose dont nous avons discuté dans [State](/chapters/state/).

## 3. The best of both worlds

We could combine the two approaches by defaulting the class to the global state class. And then only when needed we can specify a class during instantiation as shown in the first example above.

## Un dernier mot

Quand nous pensons à l'état, en particulier avec notre casquette Javascript, nous devons considérer comment cet état affecte le comportement aussi bien que le style. Différentes composants peuvent avoir le même comportement, mais elles peuvent s'afficher de manière différente. Après mûre réflexion, nous pouvons choisir la bonne solution au problème.
