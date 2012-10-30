# Apprendre à apprécier les parties les moins sexy de CSS

Le futur des CSS nous donne beaucoup d’occasions de nous enthousiasmer : d’un côté il y a un paquet de nouvelles méthodes qui vont révolutionner notre façon de mettre en page le web, et de l’autre il y a un ensemble d’effets graphiques qui vont permettre d'appliquer des filtres et *shaders 3Ds* « à la volée ». Tout le monde aime ce genre de nouveautés : les magazines et les blogs débordent d’articles à ce propos.

Mais si ces outils font figure de chiens savants des CSS, je crois cependant qu’il est temps de s’intéresser aux figurants : les rouages du langage tels que les sélecteurs, les unités et les fonctions. Je les appelle souvent « les parties les moins sexy de CSS », mais c’est toujours avec beaucoup d'affection - affection qu’à mon sens vous devriez partager.

Pour découvrir pourquoi, faisons rapidement le tour de ces parties pas très sexy qui sont conçues dans des laboratoires sombres, loin de la lumière et de l'éclat de celles que l'on expose fièrement dans la vitrine. Certains composants existent depuis longtemps mais méritent plus de reconnaissance, tandis que d’autres font tout juste leur apparition dans les navigateurs. Tous révolutionneront nos méthodes de travail, même si ce sera parfois bien discrètement et modestement.

## Unités de taille relatives

En tant que développeur intelligent et consciencieux, il est fort probable que vous ayez déjà travaillé avec les dimensions relatives - unités `em` ou pourcentages. Du coup, vous avez certainement déjà été confronté aux problèmes d'héritage qui vous ont forcé à sortir votre calculette.  
De nos jours, il est relativement commun de définir une taille de police de base pour le document, puis d’utiliser des unités relatives pour régler la taille des polices dans le reste de la page. En CSS, cela donne quelque chose comme ça :

~~~ {lang="css" line="1"}
html { font-size: 10px; }
p { font-size: 1.4em; }
~~~

C’est très bien, et ça ne pose aucun problème... jusqu’à ce que vous vouliez donner une taille différente à un élément enfant. Par exemple, dans un code tel que celui-ci :

~~~ {lang="html" line="1"}
Le chat s'est assis sur le <span>tapis</span>.
~~~

Si vous voulez que ce `span` soit d’une taille de police plus petite, par exemple 1.2em, que devez-vous faire ? Sortir votre calculette et diviser 1,2 par 1,4 pour obtenir le résultat suivant :

~~~ {lang="css" line="1"}
p span { font-size: 0.85714em; }
~~~

Bien sûr, le problème ne se limite pas à l’utilisation des `em`.  
Lorsque vous construisez un site fluide en utilisant des pourcentages, vous savez que le pourcentage est relatif à son conteneur. Donc si vous souhaitez fixer la largeur d’un élément à 40 % de celle de son parent (qui est de 75 %), alors la largeur de l’élément enfant doit être réglée à `53.33333%`.

Pas top.

## Longueurs relatives à la racine

Pour combattre ce problème de dimensionnement des polices, nous avons dorénavant accès à l’unité `rem` (*root em*). Il s’agit toujours d’une unité relative, mais qui dépend d'une valeur de base fixe : la taille de la police de l’élément racine du document (l’élément `html`). En supposant que la taille de la police de l’élément racine soit de 10px comme dans l’exemple précédent, les règles CSS nécessaires dans notre cas sont :

~~~ {lang="css" line="1"}
p { font-size: 1.4rem; }
p span { font-size: 1.2rem; }
~~~

Ces deux règles sont relatives à la taille de police de l'élément racine, ce qui est beaucoup plus élégant et simple à manipuler, surtout si vous avez des valeurs de base qui sont 10px ou 12px. C’est un peu comme si on utilisait à nouveau les valeurs en pixels, mais de manière extensible cette fois.

C’est l’une des fonctionnalités CSS les mieux supportées de toutes celles présentées dans cet article. Elle est implémentée par tous les navigateurs modernes, y compris IE9, et seulement [absente sur Opera Mobile](http://caniuse.com/#feat=rem).

## Longueurs relatives au *viewport*

Si vous trouvez que l’unité `rem` est cool (c’est mon cas), vous allez adorer la nouvelle panoplie d’unités de longueur destinées à combattre le problème des pourcentages. Elles fonctionnent de manière similaire à l’unité `rem`, si ce n’est qu’elles sont relatives à la taille du *viewport* de l’appareil du navigateur [^1] plutôt qu’à une taille définie par l’auteur sur la racine du document.

Les deux unités principales sont `vh` et `vw`, qui sont relatives (respectivement) à la hauteur et à la largeur du *viewport*. Chacune prend comme valeur un nombre qui est équivalent au pourcentage de la longueur spécifiée. Comme je me souviens de mes leçons d’écriture de scénario, je vais plutôt vous montrer un exemple :

~~~ {lang="css" line="1"}
div { height: 50vh; }
~~~

Dans cet exemple, la hauteur du `div` serait exactement la moitié de la hauteur du *viewport* ; `1vh` = 1 % de la hauteur du *viewport*, donc il est logique que `50vh` soit l’équivalent de 50 % de la hauteur du *viewport*.

Quand la taille du *viewport* change, celle de la valeur de l’unité aussi. Mais l’avantage par rapport aux pourcentages est de ne pas avoir à se soucier des éléments parents : un élément avec une largeur de `10vw` sera toujours de cette largeur quelle que soit celle de son conteneur.

Il existe aussi une unité `vmin`, équivalent à la valeur minimale de `vh` ou `vw`, et une unité correspondante `vmax` devrait être ajoutée aux spécifications (ce n’est pas encore le cas au moment où j'écris cet article [^2]).

À l’heure actuelle, ces unités sont disponibles dans IE9+, Chrome et Safari 6.

## Valeurs calculées

Quand vous travaillez avec des mises en pages fluides ou *responsive*, vous rencontrerez certainement un problème de mélange d’unités - comme une grille aux dimensions en pourcentage avec des marges fixes.  
Par exemple :

~~~ {lang="css" line="1"}
div {
  margin: 0 20px;
  width: 33%; 
}
~~~

Si votre mise en page utilise uniquement des `padding` et des `border`, vous pouvez utiliser `box-sizing` pour vous aider à contourner ce problème de mélange, mais ça ne vous aidera pas avec les `margin`. Une meilleure approche, plus flexible, consiste à utiliser la fonction de valeur `calc()`, qui vous permet de réaliser des opérations mathématiques comportant différentes unités, comme par exemple :

~~~ {lang="css" line="1"}
div {
  margin: 0 20px;
  width: calc(33% - 40px);
}
~~~

Vous n’êtes pas tenu de l’utiliser seulement sur les largeurs ; vous pouvez l’utiliser partout où des unités de longueur sont permises - et si vous souhaitez vraiment passer de l'autre côté du miroir vous pouvez utiliser `calc()` dans `calc()`.

IE9+ supporte cette fonction sans préfixe (!), Firefox utilise le préfixe `-moz-` (a priori jusqu’à la version 16 ou 17), et Chrome et Safari l’implémentent avec le préfixe `-webkit-`. Par contre [il n’est apparemment toujours pas disponible dans une version mobile de Webkit](http://caniuse.com/#feat=calc).

## Charger un sous-ensemble de caractères

La réactivité a toujours été un paramètre important, mais le grand nombre de mobiles sur le marché - chacun apportant son lot de variabilité et d’incertitudes quant aux vitesses de connexion - accentue le trait. Une façon d’accélérer le chargement des pages est de limiter la taille des fichiers externes, ce qui rend une nouvelle propriété de `@font-face` permettant de réaliser cette opération particulièrement appréciable.

La propriété en question est `unicode-range` qui prend comme valeur un ensemble de références de caractères Unicode. Lors de l’appel d’éléments externes, seuls les caractères spécifiés sont chargés depuis le fichier de police au lieu de l’ensemble complet. Voici le code qui explique comment ne charger que trois caractères depuis le fichier foo.ttf :

~~~ {lang="css" line="1"}
@font-face {
  font-family: foo;
  src: url('foo.ttf');
  unicode-range: U+31-33;
}
~~~

Ceci est particulièrement utile si vous utilisez [des polices d’icônes](http://net.tutsplus.com/tutorials/html-css-techniques/quick-tip-ever-thought-about-using-font-face-for-icons/) et souhaitez seulement en montrer un sous-ensemble dans une page donnée. Lors d’un test que j’ai effectué, l’utilisation de `unicode-range` a permis d’économiser 0,85 seconde sur le  chargement d’un fichier de police, ce qui n’est pas sans conséquences. Bien entendu, ce résultat peut varier suivant le contexte.

Cette propriété est actuellement implémentée dans IE9+ et les navigateurs Webkit tels que Chrome et Safari.

## Nouvelles pseudo-classes

Les unités et valeurs sont bien sympas, mais ce sont les sélecteurs et les pseudo-classes qui m’enthousiasment le plus. Trouver une combinaison de sélecteurs astucieuse, même si elle reste cachée en un lieu que seuls quelques intrépides aventuriers pourront découvrir, me fait me sentir tel un artiste. [Comme le disait le père de Steve Jobs](http://hbr.org/2012/04/the-real-leadership-lessons-of-steve-jobs/) : vous devriez vous assurer que la face arrière de la barrière est aussi bien peinte que la face avant même si personne ne la verra, parce que VOUS vous le saurez.

La première fois que j’ai utilisé `:nth-of-type()`, j’ai eu une révélation, comme si j’avais abattu les portes de la perception. OK, j’exagère un peu. Mais certaines nouvelles pseudo-classes méritent qu’on s’extasie.

### La pseudo-classe de négation

Vous ne réaliserez probablement pas à quel point la pseudo-classe `:not()` est utile jusqu’à ce que vous l’utilisiez. L’argument passé à `:not()` est un sélecteur simple, pas une combinaison. Quand une liste d’éléments est construite par un sélecteur qui inclut `:not()`, tous les éléments correspondant à l’argument seront exclus de cette liste. Je sais, ça m’a paru compliqué aussi, mais en fait c'est assez simple.

Imaginez ceci : vous avez une liste d’éléments et vous souhaitez appliquer une règle à tous ses éléments impairs mais jamais au dernier élément. Pour l’instant, vous devriez faire quelque chose comme ça :

~~~ {lang="css" line="1"}
li { color: #00F; }
li:nth-child(odd) { color: #F00; }
li:last-child { color: #00F; }
~~~

Grâce à la pseudo-classe de négation, vous pouvez exclure le dernier élément de la liste en utilisant `:last-child` comme argument, ce qui réduira le nombre de règles nécessaires et simplifiera un peu l’entretien du code :

~~~ {lang="css" line="1"}
li { color: #00F; }
li:nth-child(odd):not(:last-child) { color: #F00; }
~~~

Rien de très novateur, et comme je l’ai montré on peut travailler sans, mais ça reste assez utile. J’ai eu l’opportunité d’utiliser cette pseudo-classe dans un projet reposant sur un Webkit embarqué, et elle a démontré son utilité de manière constante. C’est honnêtement l’une de mes pseudo-classes favorites.

Tout à fait, j’ai des pseudo-classes favorites.

C’est la fonctionnalité la plus largement implémentée de cet article : elle est présente dans IE9+ et tous les navigateurs modernes, sans préfixe. Et si vous êtes familier avec jQuery, vous avez probablement l’habitude de l’utiliser : elle y est présente depuis la version 1.0, ainsi que la méthode `not()` équivalente.

### La pseudo-classe de correspondance

La pseudo-class `:matches()` accepte comme argument un sélecteur simple, un sélecteur composé, une liste séparée par des virgules, ou une combinaison de ces éléments.  
Super ! Mais elle fait quoi ?

Elle est surtout utile pour éliminer les redondances dans les sélecteurs multiples. En guise d’exemple concret, imaginez que vous ayez des éléments p dans différents containers mais que vous souhaitiez n’en sélectionner que certains ; vous écrirez peut-être une règle de style ressemblant à ça :

~~~ {lang="css" line="1"}
.home header p,
.home footer p,
.home aside p {
  color: #F00;
}
~~~

Avec `:matches()` vous pouvez considérablement raccourcir cette règle en trouvant les éléments communs à ces sélecteurs ; dans notre exemple tous débutent par `.home`et finissent par `p`, nous pouvons donc utiliser `:matches()` pour agréger tous les éléments intermédiaires. Déroutant ? Voici à quoi cela ressemblerait :

~~~ {lang="css" line="1"}
.home :matches(header,footer,aside) p { color: #F00; }
~~~

Cette pseudo-classe fait actuellement partie de CSS4 (Sélecteurs CSS Niveau 4, pour être précis), et dans la même spécification il est mentionné que l’on pourra utiliser la même syntaxe (sélecteurs composés séparés par des virgules) dans les futures versions de `:not()`. Passionnant !

Aujourd’hui, `:matches()` est disponible dans Chrome et Safari avec le préfixe `-webkit-` et dans Firefox sous son ancien nom, `:any()`, avec le préfixe `-moz-`.

## Aimez-vous enfin les figurants ?

La meilleure chose à propos de toutes les nouvelles fonctionnalités de cet article, c'est qu’elles règlent des problémes réels, depuis la simple répétition de sélecteurs jusqu’aux nouveaux défis de la construction de sites *responsive* à haute-performance. En fait, je peux tout à fait imaginer utiliser toutes ces fonctionnalités de manière parfaitement récurrente.

Les nouvelles fonctionnalités comme les filtres sont peut-être plus visibles, mais il est bien plus probable que celles présentées ici vous soient utiles dans tous vos projets.

Chacune d'entre elles  facilitera votre vie professionnelle tout en élargissant le champs des possibles, et c'est assez sexy finalement, non ?



## Notes

[^1]: L'article original mentionne l'appareil (*device*) mais c'est une erreur : ces tailles ne sont pas relatives au *viewport* de l'appareil mais au *viewport* du navigateur.
[^2]: NDT: C'est le cas au moment de cette traduction.

