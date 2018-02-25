---
layout: chapter
title: Modifiers
section: Core
permalink: /chapters/modifiers/
description: Utiliser des modificateurs pour changer l'apparence en fonction de légères différences.
---

Comme l'état, les modificateurs remplacent également les styles. Elles sont utiles lorsque les modules (ou composants) présentent de petites différences bien comprises.

Prenez un site de commerce électronique où chaque catégorie a une image de fond unique dans l'en-tête. Tous les en-têtes ont le même rembourrage, la même marge, etc. La seule différence est l'image de fond.

La catégorie des garçons aurait un modificateur comme suit :

	<div class="categoryHeader categoryHeader--boys">

De même, la catégorie des filles aurait un modificateur *filles*:

	<div class="categoryHeader categoryHeader--girls">

Le CSS serait :

	.categoryHeader {
	  padding-top: 50px;
	  padding-bottom: 50px;
	  /* etc */
	}

	.categoryHeader--boys {
	  background-image: url(/path/to/boys.jpg);
	}

	.categoryHeader--girls {
	  background-image: url(/path/to/girls.jpg);
	}

Parce que les différences sont minimes et bien comprises, ce type de réutilisation est plus facile à maintenir.

Nous pouvons utiliser la même approche pour les boutons. La plupart des sites ont un style de bouton primaire et secondaire. Si tout ce qui change est un ou deux styles, nous pouvons avoir un modificateur pour les boutons primaires et secondaires comme suit:

	.button {
	  padding: 20px;
	  border-radius: 3px;
	  /* etc */
	}

	.button--primary {
	  background-color: green;
	}

	.button--secondary {
	  background-color: #eee;
	}

Encore une fois, cela fonctionne seulement parce que les différences sont bien contenues et bien comprises.

## Un dernier mot

Les modificateurs sont une bonne façon de réutiliser les styles à travers un élément bien compris. Mais le modificateur lui-même devrait être un ajustement. S'il contient beaucoup de dérogations, les modificateurs ne sont pas la solution. Utilisez plutôt un [module](/chapters/modules/).
