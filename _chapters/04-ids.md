---
layout: chapter
title: IDs
section: Background
permalink: /chapters/ids/
description: Apprenez pourquoi l'utilisation des ID comme hooks de style est problématique et ce que vous devriez faire à la place.
---

Sémantiquement parlant, nous devrions utiliser une pièce d'identité quand il n' y a qu'une seule instance d'une chose. Et on devrait utiliser une classe quand il y en a plusieurs.

Cependant, [les ID surpassent les noms de classe](http://www.w3.org/TR/css3-selectors/#specificity) par ordre de grandeur, ce qui est un problème quand on veut surcharger un style.

Pour illustrer le problème, écrasons la couleur d'un élément de *rouge* à *bleu* à l'aide d'un ID.

Voici le HTML:

	<div id="module" class="module-override">

Et le CSS:

	#module {
		color: red;
	}

	.module-override {
		color: blue;
	}

L'élément sera rouge même si la classe d'annulation déclare le bleu. Réglons ça en changeant l'ID d'une classe:

	<div class="module module-override">

Et le CSS:

	.module {
		color: red;
	}

	.module-override {
		color: blue;
	}

Maintenant, l'élément est bleu&mdash; problème résolu.

Bien que l'utilisation des ID pour le style soit problématique, nous pouvons toujours les utiliser pour d'autres choses. Par exemple, nous devrons certainement les utiliser pour connecter :

- des labels pour former des champs
- des ancres dans la page
- des attributs ARIA pour aider les utilisateurs de lecteurs d'écran

## Un dernier mot

Utilisez des ID chaque fois que vous avez besoin d'activer des comportements particuliers pour les navigateurs et la technologie d'assistance. Mais évitez de les utiliser comme hooks pour les styles.
