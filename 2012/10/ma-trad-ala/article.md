# Apprendre à aimer les parties les moins sexy des CSS (?)

Le futur des CSS nous donne beaucoup d’occasions de s’exciter : d’un côté il y a un paquet de nouvelles méthodes qui vont révolutionner notre façon de mettre en page le web, et de l’autre il y a un ensemble d’effets graphiques qui vont permettre les filtres et *shaders* « à la volée ». Les gens aiment ce genre de trucs. Les magazines et les blogs débordent d’articles sur le sujet.

Mais si ces outils sont l’attraction de la foire aux CSS, alors je crois qu’il est temps de s’intéresser aux figurants : les rouages du langage, comme les sélecteurs, unités et fonctions. Je les appelle les xxx, même si c’est avec une grande affection — affection qu’à mon sens vous devriez partager.

Pour découvrir pourquoi, faisons rapidement le tour de ces parties ennuyeuses des CSS, celles qui sont conçues dans des laboratoires sombres, poins des éclats des choses nouvelles et brillantes dans la vitrine. Certaines de ces composantes existent depuis longtemps mais méritent plus de reconnaissance, et d’autres font juste leur apparition dans les navigateurs. Mais ils seront tous révolutionnaires pour nos méthodes de travail, si c’est de manière modeste.

## Unités de taille relatives

Comme vous êtes un développeur intelligent et progressiste, il est fort probable que vous ayez déjà travaillé avec les dimensions relatives — unités `em` ou pourcentages — alors vous connaîtrez ce problème : devoir utiliser une calculette pour trouver les dimensions à cause de l’héritage. Par exemple, il est assez commun de nos jours d’établir une taille de police de base pour votre document, puis d’utiliser des tailles relatives pour régler vos polices dans le reste de la page. En CSS, cela donne quelque chose comme ça.

```
html { font-size: 10px; }
p { font-size: 1.4em; }
```

C’est très bien, et pas du tout problématique, jusqu’à ce que vous vouliez donner une taille différent à un élément enfant. Par exemple, dans un code tel que celui-ci :

```
The cat sat on the <span>mat</span>.
```

Si vous voulez que ce `span` soit d’une taille de police plus petit, par exemple 1.2em, que devez-vous faire ? Sortir votre calculette et diviser 1.2 par 1.4, pour le résultat suivant :

```
p span { font-size: 0.85714em; }
```

Le problème ne se limite pas à l’utilisation des `em` non plus. Si vous construisez un site fluide en utilisant des pourcentages, vous savez que le pourcentage est relatif à son conteneur ; donc si vous souhaitez fixer la largeur d’un élément à 40% de son parent, dont la largeur est 75%, alors la largeur de l’élément enfant doit être réglée à 53.33333%.

Pas vraiment idéal.

## Longueurs relatives à la racine

Pour combattre ce problème de dimensionnement des polices, nous avons dorénavant accès à l’unité `rem` (*root em*). Il s’agit toujours d’une unité relative, mais qui est toujours relative à une valeur de base fixe, qui est la taille de la police de l’élément racine du document (en HTML, il s’agit toujours de l’élément `html`). En supposant que la taille de la police de l’élément racine est de 10px comme dans l’exemple précédent, les règles CSS nécessaires dans notre cas sont :

```
p { font-size: 1.4rem; }
p span { font-size: 1.2rem; }
```

Les deux règles sont relatives à la taille de police de la racine, ce qui est beaucoup plus élégant et simple à manipuler, surtout si vous avez des valeurs de base de 10px ou 12px. C’est comme si on utilisait à nouveau les valeurs en pixels, mais de manière extensible.

C’est l’une des fonctionnalités CSS les mieux supportées de toutes celles présentées dans cet article ; dans tous les navigateurs modernes, y compris IE9, et seulement absent d’Opera Mobile.

## Longueurs relatives au *viewport*

Si vous trouvez que l’unité `rem` est chouette (c’est mon cas), vous allez adorer la nouvelle panoplie d’unités de longueur pour combattre le problème des pourcentages. Elles fonctionnent de manière similaire à l’unité `rem`, si ce n’est qu’elles sont relatives à la taille du *viewport* de l’appareil plutôt qu’à une taille définie par l’auteur sur la racine du document.

Les deux unités principales sont `vh` et `vw`, qui sont relatives (respectivement) à la hauteur et la largeur du *viewport*. Chacune prends un nombre comme valeur, et ce nombre est égal au même pourcentage de la longueur spécifiée. Comme je me souviens de mes leçons d’écriture de scénario, je vais plutôt vous montrer un exemple :

```
div { height: 50vh; }
```

Dans cet exemple, la hauteur du `div` serait exactement la moitié de la hauteur du *viewport* ; `1vh` = 1% de la hauteur du *viewport*, donc il est logique que `50vh` soit l’équivalent de 50% de la hauteur du *viewport*.

Quand la taille du *viewport* change, celle de la valeur de l’unité aussi —  mais l’avantage par rapport aux pourcentages est de ne pas avoir à se soucier des éléments conteneurs : un élément avec une largeur de `10vw` sera toujours de cette largeur quelle que soit celle de son parent.

Il existe aussi une unité `vmim`, équivalent à la valeur minimale de `vh` ou `vw`, et une unité correspondante `vmax` devrait être ajoutée aux spécifications (ce n’est pas encore le cas à l’heure d’écriture de cet article).

À l’heure actuelle, ces unités sont disponibles dans IE9+, Chrome et Safari 6.

## Valeurs calculées

Quand vous travaillez avec des mises en pages fluides ou *responsive*, vous rencontrerez certainement le problème de mélange d’unités — comme une grille aux dimensions en pourcentage avec des marges fixes.  
Par exemple :

```
div {
  margin: 0 20px;
  width: 33%; 
}
```

Si votre mise en page utilise uniquement des `padding` et des `border`, vous pouvez utiliser `box-sizing` pour vous aider à contourner ce problème de mélange, mais ça ne vous aidera pas avec les `margin`. Une meilleure approche, plus flexible, consiste à utiliser la fonction de valeur `calc()`, qui vous permet d’exécuter des opérations mathématiques avec des unités différentes, comme par exemple :

```
div {
  margin: 0 20px;
  width: calc(33% - 40px);
}
```

Vous n’êtes pas obligé de vous limiter à l’utiliser sur les largeurs uniquement ; vous pouvez aussi l’utiliser partout où des unités de longueur sont permises — et si vous souhaitez vraiment xxx vous pouvez utiliser `calc()` dans `calc()`.

IE9+ supporte cette fonction sans préfixe (!), Firefox utilise le préfixe -moz- (a priori jusqu’à la version 16 ou 17), et Chrome et Safari l’implémentent avec le préfixe -webkit-. Il n’est apparemment toujours pas dans la version mobile de Webkit par contre.

## Charger un sous-ensemble de caractères

La réactivité a toujours été important, mais la grande étendue de mobiles sur le marché — chacun apportant son lot de variabilité et d’incertitude dans les vitesses de connexion — appuie le trait. Une façon d’accélérer le chargement des pages est de limiter la taille des fichiers externes, ce qui rends une propriété additionnelle de `@font-face` très appréciable.






