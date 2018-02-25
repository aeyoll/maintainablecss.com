---
layout: chapter
title: Reuse
section: Background
permalink: /chapters/reuse/
description: Apprenez pourquoi le fait d'éviter la réutilisation et d'adopter la répétition facilite la maintenance CSS.
---

Comme le dit Harry Roberts, "DRY (don't repeat yourself) est souvent mal interprété comme la nécessité de ne jamais répéter exactement la même chose deux fois. C'est peu pratique et généralement contre-productif, et cela peut mener à des abstractions forcées, à un code trop réfléchi et trop élaboré."

Cette abstraction forcée, cet excès de réflexion et ce code surinventé aboutissent souvent à des classes visuelles et atomiques. Nous savons à quel point ils sont douloureux parce que nous en avons discuté en profondeur dans le chapitre [sémantiques](/chapters/semantics/). Les mixins peuvent aussi poser problème, dont nous discuterons sous peu.

Bien que nous essayons souvent d'abstraire les CSS trop souvent trop tôt, il y aura évidemment des moments où la réutilisation a du sens. Il faut répondre à la question : *comment pouvons-nous réutiliser un style?*

## Comment peut-on réutiliser un style ?

Si nous voulons réutiliser un style, une option serait de délimiter par des virgules les sélecteurs à l'intérieur d'un fichier bien nommé, ce qui, si vous utilisez SASS est exactement ce que `@extend` fait. Par exemple, si plusieurs éléments ont besoin de texte rouge, nous pourrions le faire:

    . someThing,
    . anotherThing {
      color: rouge;
    }

Cette approche devrait être utilisée pour des raisons de commodité et non de performance. (Si l'abstraction n'a qu'une seule règle, nous échangeons simplement une ligne de code pour une autre.)

Si un sélecteur s'écarte des règles dans l'abstraction, il doit être supprimé de la liste. Sinon, il pourrait régresser les autres sélecteurs et causer des problèmes pour faire des surcharges.

Il est important de noter qu'il s'agit d'une des nombreuses techniques à notre disposition. Lorsqu'une *chose* est bien comprise, nous pouvons utiliser d'autres techniques, dont nous discuterons dans [Modules](/chapters/modules/), [États](/chapters/states/) et [Modificateurs](/chapters/modifiers).

## Et les mixins ?

Les Mixins offrent le meilleur des deux mondes. Du moins en théorie.

Comme les classes d'utilitaires, la mise à jour d'un mixin se propage à toutes les instances. Si nous n'avons pas la maîtrise de ce qui utilise le mixin, nous augmentons le risque de régression. Au lieu de mettre à jour un mixin, on peut en créer un autre, mais cela entraîne une redondance.

De plus, les mixins finissent facilement avec de nombreuses règles, des paramètres multiples et la conditionnalité. C'est compliqué. La complexité est difficile à maintenir.

Pour atténuer cette complexité, nous pouvons créer des mixins granulaires, par exemple un pour le texte rouge. Au début, ça semble mieux. Mais la déclaration d'un mixing rouge n'est-elle pas la même chose que la règle elle-même, c'est-à-dire `color: red` ?

Si nous avons besoin de mettre à jour la règle à plusieurs endroits, une recherche et un remplacement pourrait être tout ce qui est nécessaire. De plus, lorsque le *mixin* rouge devient *orange*, son nom devra être mis à jour de toute façon.

Avec tout cela dit, les mixins peuvent être très utiles. Nous pourrions, par exemple, vouloir appliquer des règles *clearfix* à différents éléments et uniquement dans certains points de rupture. C'est quelque chose que le CSS de base ne peut pas faire élégamment.

En tant que tels, les mixins ne sont pas *mauvais*, c'est juste que nous devrions les utiliser judicieusement.

## Qu'en est-il de la performance ?

Nous réfléchissons souvent trop à la performance et nous sommes obsédés par les petits détails. Même si le CSS totalisait plus de 100kb, il n'y a pas grand-chose à gagner à respecter DRY le plus possible.

Rendre le fichier CSS petit rend le fichier HTML grand. CSS peut toujours être mis en cache. Mais HTML contient souvent du contenu dynamique et personnalisé&mdash; donc il ne peut pas être mis en cache.

La compression d'une seule image nous donne un meilleur retour sur investissement. Et comme nous en avons discuté, la résolution d'autres formes de redondance améliore la maintenabilité *et* la performance.

Comme vous le verrez dans les chapitres suivants, les conventions de ce guide, signifient que les noms de classes CSS ont des préfixes répétés qui fonctionnent particulièrement bien avec GZip.

## Est-ce que c'est une violation des principes DRY ?

Tenter de réutiliser, par exemple `float: left`, c'est comme essayer de réutiliser des noms de variables dans différents objets Javascript. Ce n'est tout simplement pas en violation de DRY.

## Pensée finale

La recherche du DRY mène à un code trop réfléchi et trop élaboré. Ce faisant, nous rendons la maintenance plus difficile, pas plus facile. Au lieu d'être obsédés par les styles, nous devrions nous concentrer sur la réutilisation de modules tangibles. Quelque chose dont nous discuterons dans les prochains chapitres.
