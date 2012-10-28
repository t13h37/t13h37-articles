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

IE9+ supporte cette fonction sans préfixe (!), Firefox utilise le préfixe `-moz-` (a priori jusqu’à la version 16 ou 17), et Chrome et Safari l’implémentent avec le préfixe `-webkit-`. Il n’est apparemment toujours pas dans la version mobile de Webkit par contre.

## Charger un sous-ensemble de caractères

La réactivité a toujours été important, mais la grande étendue de mobiles sur le marché — chacun apportant son lot de variabilité et d’incertitude dans les vitesses de connexion — appuie le trait. Une façon d’accélérer le chargement des pages est de limiter la taille des fichiers externes, ce qui rends une propriété additionnelle de `@font-face` très appréciable.

La propriété en question est `unicode-range` qui prend comme valeur une gamme de références de caractères Unicode. Lors de l’appel d’éléments externes, seuls les caractères spécifiés seront chargés depuis le fichier de police au lieu de l’ensemble complet. Voici le code qui démontre comment ne charger que 3 caractères depuis le fichier foo.ttf :

```
@font-face {
  font-family: foo;
  src: url('foo.ttf');
  unicode-range: U+31-33;
}
```

Ceci est particulièrement utile si vous utilisez des polices d’icônes et souhaitez seulement montrer un sous-ensemble dans une page donnée. Lors d’un test que j’ai effectué, l’utilisation de `unicode-range` a permis d’économiser .85 secondes sur le  chargement d’un fichier de police, ce qui n’est pas sans conséquences. Bien entendu, ce résultat peut varier.

Cette propriété est actuellement implémentée dans IE9+ et les navigateurs Webkit tels que Chrome et Safari.

## Nouvelles pseudo-classes

Les unités et valeurs sont bien sympathiques, mais c’est les sélecteurs et les pseudo-classes qui m’excitent particulièrement. Trouver une combinaison de sélecteurs astucieuse, même si ça reste caché xxx, me fait sentir comme un artiste. Comme le disait le père de Steve Jobs : vous devriez vous assurer que l’arrière de la barrière est aussi bien peint que l’avant même si personne ne le verra, parce que vous vous le saurez.

La première fois que j’ai utilisé `:nth-of-type()`, j’ai eu une révélation, comme si j’avais abattu le mur de la perception. Ok, j’exagère un peu. Mais certaines nouvelles pseudo-classes méritent qu’on s’extasie.

### La pseudo-classe de négation

Vous ne réaliserez probablement pas à quel point la pseudo-class `:not()` est utile jusqu’à ce que vous l’utilisiez. L’argument passé à `:not()` est un sélecteur simple, pas une combinaison. Quand une liste d’éléments est construite par un sélecteur qui inclue `:not()`, tous les éléments correspondant à l’argument seront exclus de cette liste. Je sais, ça m’a paru compliqué aussi, mais c’est en fait assez simple.

Imaginez ceci : vous avez une liste d’éléments et vous souhaitez appliquer une règle à tous ses éléments impairs (?) mais jamais au dernier élément. Pour l’instant, vous devriez faire quelque chose comme ça :

```
li { color: #00F; }
li:nth-child(odd) { color: #F00; }
li:last-child { color: #00F; }
```

Grâce à la pseudo-classe de négation, vous pouvez exclure le dernier élément de la liste en utilisant `:last-child` comme argument, réduisant ainsi le nombre de règles nécessaires, simplifiant l’entretien du code :

```
li { color: #00F; }
li:nth-child(odd):not(:last-child) { color: #F00; }
```

Rien de très novateur, et comme je l’ai montré on peut travailler sans, mais ça reste assez utile. J’ai eu l’opportunité d’utiliser cette pseudo-classe dans un projet construit sur un Webkit intégré (???), et elle a démontré son utilité de manière constante. C’est honnêtement l’une de mes pseudo-classes favorites.

Oui, j’ai des pseudo-classes favorites.

C’est la fonctionnalité la plus largement implémentée de cet article : elle est présente dans IE9+ et tous les navigateurs modernes, sans préfixe. Et si vous êtes familier avec jQuery, vous avez probablement l’habitude de l’utiliser : elle y est présente depuis la version 1.0, ainsi que la méthode `not()` similaire.

### La pseudo-class « correspond à » (?)

La pseudo-class `:matches()` accepte comme argument un sélecteur simple, un sélecteur composé, une liste séparée par des virgules, ou une combinaison de ces éléments. Super ! Mais elle fait quoi ?

Elle est surtout utile pour éliminer le surplus dans des sélecteurs multiples. En guise d’exemple concret, imaginez que vous avez des éléments p dans différents containers mais que vous souhaitez n’en sélectionner que certains ; vous écririez peut-être une règle de style ressemblant à ça :

```
.home header p,
.home footer p,
.home aside p {
  color: #F00;
}
```

Avec `:matches()` vous pouvez raccourcir cette règle considérablement en trouvant les éléments communs à ces sélecteurs ; dans notre exemple tous débutent par `.home`et finissent par `p`, nous pouvons donc utiliser `:matches()` pour agréger tous les éléments entre. Déroutant ? Voici à quoi cela ressemblerai :

```
.home :matches(header,footer,aside) p { color: #F00; }
```

Cette pseudo-classe fait actuellement partie de CSS4 (Sélecteurs CSS Niveau 4, pour être précis), et dans la même spécification il est mentionné que l’on pourra utiliser la même syntaxe (sélecteurs composés séparés par des virgules) dans les futures versions de `:not()`. Excitant !

Aujourd’hui, `:matches()` est disponible dans Chrome et Safari avec le préfixe `-webkit-` et dans Firefox sous son ancien nom, `:any()`, avec le préfixe `-moz-`.

## Aimez-vous enfin les figurants ?

Le meilleur à propos de toutes les nouvelles fonctionnalités de cet article est qu’elles règlent des problématiques réelles, depuis la simple répétition de sélecteurs jusqu’aux nouveaux défis de construction de sites `responsive` à haute-performance. En fait, je peux tout à fait m’imaginer utiliser toutes ces fonctionnalités de manière récurrente.

Les nouvelles fonctionnalités comme les filtres sont peut-être plus visibles, mais il y a de fortes chances que celles présentées ici vous soient utiles dans toutes vos constructions.

Chacune vous facilitera votre vie professionnelle tout en élargissant le champs des possibles, et il n’y a rien d’ennuyeux à ça.