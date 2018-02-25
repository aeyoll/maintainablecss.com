---
layout: chapter
title: Versioning
section: Extras
permalink: /chapters/versioning/
description: Découvrez comment MaintainableCSS facilite la mise à niveau et les modules de test AB pour les sites Web en évolution rapide.
---

Nous pouvons, par exemple, vouloir tester deux versions différentes d'un module pour voir lequel fonctionne le mieux. Pour ce faire, nous devons dupliquer le module et lui donner un nom unique. Par exemple, si nous voulons tester deux paniers différents, le CSS peut être comme suit :

	/* existing module (variant A) */
	.basket {}

	.basket-title {}

	/* new version (variant B) */
	.basket2 {}

	.basket2-title {}

De cette façon, nous pouvons maintenir deux versions pendant les tests jusqu'à ce que nous nous entendions sur la meilleure. Et une fois que nous l'avons fait, il est facile de se débarrasser du module redondant car il n'est pas entrelacé. Un bon code est facile à effacer.