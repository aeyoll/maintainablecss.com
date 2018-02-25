---
layout: chapter
title: State
section: Core
permalink: /chapters/state/
description: Apprenez comment fournir différents styles à vos modules et composants en fonction de l'état, tels que l'affichage, le masquage et le chargement.
---

Bien souvent, en particulier avec des interfaces utilisateur plus riches, le style doit être appliqué en fonction du changement d'état d'un élément. Par exemple, nous pouvons avoir des styles différents lorsqu'un module (ou composant) est :

- showing ou hiding
- active ou inactive
- disabled ou enabled
- loading ou loaded
- hasProducts ou hasNoProducts
- isEmpty ou isFull

Pour représenter l'état, nous avons besoin d'une classe additionnelle qui doit être ajoutée à l'élément module (ou composant) auquel elle se rapporte. Par exemple, si notre module panier a besoin d'un fond gris quand il est vide, le HTML devrait l'être :

	<div class="basket basket-isEmpty">

And the CSS should be:

	.basket-isEmpty {
      background-color: #eee;
	}

Le nom de la classe est préfixé avec le module (ou composant) parce que si les états peuvent être communs, les styles associés peuvent ne pas l'être. Par exemple, un *panier* vide a un fond gris, alors qu'une recherche vide aura une image positionnée.

## Et la réutilisation de l'état ?

Parfois, nous pouvons en fait vouloir réutiliser l'état entre modules ou composants. Par exemple, basculer la visibilité d'un élément. Ceci sera abordé plus en détail dans le chapitre intitulé [Javascript](/chapter/javascript/).

## À propos des attributs ARIA

Tous les états visuels ne peuvent pas être représentés par un attribut[ARIA](https://www.w3.org/TR/wai-aria/states_and_properties#attrs_widgets]. Par exemple, il n'y a aucun attribut pour représenter `hasProducts`. Par conséquent, nous ne devrions les utiliser que lorsque c'est nécessaire et en plus des cours.

De plus, en utilisant un attribut (au lieu d'une classe), le sélecteur a [moins de support](https://www.impressivewebs.com/attribute-selectors/). Alors que les développeurs peuvent considérer ces navigateurs comme vieux, peu sûrs ou non pertinents, nous devrions éviter les techniques qui excluent inutilement les utilisateurs.

## Qu'en est-il des cours d'enchaînement ?

Nous pourrions utiliser un sélecteur enchaîné pour l'état par exemple `. module.isDisabled`. Le problème est que cette approche est moins bien supportée par les navigateurs. Nous devrions éviter les modèles qui excluent inutilement les utilisateurs, à moins qu'il n'y ait une raison impérieuse de le faire.

Cela rend également plus difficile de savoir si/où le style est utilisé, ce qui rend la maintenance plus difficile.

## Un dernier mot

Si le style d'un élément doit changer en fonction de son état, nous devrions ajouter une classe supplémentaire pour appliquer les différences. Si nécessaire, utilisez les attributs ARIA pour la technologie d'assistance et non pour le style. Pour ce faire, nous employons une approche cohérente et inclusive du style.
