---
layout: chapter
title: Conventions
section: Core
permalink: /chapters/conventions/
description: Apprenez les conventions simples qu'utilise MaintainableCSS pour écrire des modules, des composants et des états.
---

*MaintainableCSS* a la convention suivante :

	.<module>[-<component>][-<state>] {}

Les éléments entre parenthèse carrés sont optionnels selon le module concerné. En voici quelques exemples:

	/* Module container */
	.searchResults {}

	/* Component */
	.searchResults-heading {}

	/* State */
	.searchResults-isLoading {}

Notes :

- le composant et l'état sont tous deux délimités par un tiret
- les noms sont écrits avec lowerCamelCase
- les sélecteurs sont préfixés avec le nom du module

## Dois-je donner un nom de classe à chaque élément?

Non. Vous pouvez écrire `.searchResults p` si vous voulez. Et parfois, il se peut que vous deviez le faire si, par exemple, vous utilisez du Markdown. Mais attention, si vous emboîtez un module qui contient un `p`, il héritera des styles et aura besoin d'un surcharge.

## Pourquoi dois-je préfixer le nom du module?

Bonne question. Voici quelques HTML sans préfixe:

	<div class="basket">
	  <div class="heading">

Et le CSS:

	/* module */
	.basket {}

	/* heading component of basket module */
	.basket .heading {}

Il y a deux problèmes :

1. lorsque vous visualisez HTML, il est difficile de faire la différence entre un module et un composant; et
2. le composant `.basket .heading` héritera des styles du module `.heading` qui a des effets secondaires involontaires.
