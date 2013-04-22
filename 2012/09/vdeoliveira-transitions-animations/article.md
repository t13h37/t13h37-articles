# Les transitions et animations CSS

## Introduction

Depuis toujours, les concepteurs web ont tenté de styler et de dynamiser des pages HTML terriblement monotones. À la fin des années 90, un simple effet de survol ne peut pas être réalisé facilement : l’utilisation de JavaScript est inévitable, mais impose de connaître la programmation. L’arrivée des pseudo-classes dynamiques au sein de CSS (`:hover`, `:focus`, `:active`...) a alors facilité l’opération et permis de s’affranchir de scripts souvent lourds.

Plus tard, lorsque que la mode était aux ombres portées et aux coins arrondis, les techniques passaient par la surcharge du balisage HTML et la création d’images étirables, ce qui nuisait considérablement à la sémantique et à l'accessibilité (si toutes les précautions n'étaient pas prises). Aujourd’hui, avec CSS3 et les propriétés `box-shadow` et `border-radius`, ces effets sont facilement réalisables et les anciennes techniques sont fortement déconseillées.

Parallèlement, de nombreux designers-développeurs, frustrés des possibilités offertes par les standards web, se tournèrent vers des solutions radicales, comme Flash, notamment pour ses capacités d’animation, de transformation d’objets dans l’espace, de gestion des textes et du multimédia. Malheureusement, Flash pose de gros soucis d’accessibilité qui sont accentués aujourd’hui sur plateforme mobile où la plupart des appareils ne le supportent pas.

C’est pourquoi le langage CSS se devait d’offrir des fonctionnalités équivalentes pour l’enrichissement de l’expérience utilisateur. C’est désormais chose faite en ce qui concerne les animations d’objets et les transformations géométriques, puisque trois modules dédiés sont arrivés au terme de leur étude par le W3C :

- Transitions CSS ;
- Animations CSS ;
- Transformations CSS.

Cet article détaille l’utilisation et la mise en place des transitions et animations CSS dans vos projets web.


## Transitions et animations en CSS, c’est quoi ?

Les transitions et animations permettent de nouvelles interactions avec l’internaute en favorisant son ressenti (et donc son impression positive) sur le produit qu’il est train d’utiliser. L’ajout subtil de ces transitions et/ou animations améliore grandement le design des interfaces et permet d’en accroître l’utilisabilité.  
Mais quelle est la différence entre transitions et animations ?


### Les transitions

**Une transition CSS est le fait d’animer le changement de valeur d’une propriété** (d'une valeur A à une valeur B), comme par exemple le changement de couleur d’un élément de `color: red;` à `color: blue;`, ou encore le changement de taille de `width: 50px;` à `width: 100px;`. Cette transition intervient lors d’un changement d’état, qui peut être :

- L’utilisation de pseudo-classes (`:hover`, `:focus`, `:active`, `:checked`, etc.) ;
- La modification du DOM via JavaScript (ajout de l’attribut `class`, modification des styles CSS) ;
- Le chargement de la page dans certains navigateurs ;
- [D’autres idées de changement d’état pour lancements de transitions](http://www.impressivewebs.com/css3-transitions-without-hover/ ).

Afin de gérer cette transition, cinq propriétés sont définies :

- `transition-property` : la (les) propriété(s) à animer ;
- `transition-duration` : la durée de la transition ;
- `transition-delay` : le délai avant que l’animation ne se lance ;
- `transition-timing-function` : la méthode d’interpolation (départ rapide, lent...) ;
- et `transition` : c’est la propriété raccourcie des quatre précédentes.

Par défaut, toutes les propriétés sont animées (avec le mot-clé `all`), la durée est de 0 seconde et la méthode d’interpolation est `ease` (nous y reviendrons).
Cela signifie que le code minimal pour réaliser une transition est :

~~~ {lang="css" line="1"}
#elem {
    transition: 1s;
}
~~~

Ce qui équivaut à :

~~~ {lang="css" line="1"}
#elem {
    transition-property: all;
    transition-duration: 1s;
    transition-timing-function: ease;
}
~~~

Dans ce cas, toutes les propriétés animables appliquées à `#elem` lors de son changement d’état subiront une transition de 1 seconde. Retrouvez [la liste des propriétés animables](http://www.w3.org/TR/css3-transitions/#animatable-properties ) sur le site du W3C.

Voici un exemple concret pour réaliser une transition linéaire de 1 seconde sur la largeur et la couleur d’arrière-plan d’un élément :

~~~ {lang="css" line="1"}
#elem {
    transition: width 1s linear, background-color 1s linear;
}
~~~

[Voir la démonstration 1](http://jsfiddle.net/iamvdo/Vu9WG/)


### Les animations

**Une animation CSS correspond à plusieurs transitions qui s'enchaînent**. Une animation permet par exemple un changement de couleur de `color: red;` à `color: blue;`, puis de `color: blue;` à `color: green;`.  Pour cela, chaque transition est donc définie sous forme d’étape (en pourcentage de l’animation globale) via la règle `@keyframes`.

Création d’une animation de changement de taille :

~~~ {lang="css" line="1"}
@keyframes nomAnim {
    0%   { width: 50px;}
    50%  { width: 200px;}
    100% { width: 100px;}
}
~~~

Cette animation définit donc 2 changements de taille : d’abord de `width: 50px;` à `width: 200px;`, puis de `width: 200px;` à `width: 100px;`. Pour définir les étapes, il existe également deux mots-clés: `from` qui équivaut à la valeur 0%, et `to` qui équivaut à la valeur 100%. De plus, il est possible d'ajouter plusieurs étapes séparées par des virgules pour le même groupe de propriétés, comme ceci :

~~~ {lang="css" line="1"}
@keyframes nomAnim {
    from, to { width: 100px;}
    25%, 75% { width: 200px;}
    50%      { width: 50px;}
}
~~~

Cette animation peut ensuite être appliquée par le biais de neuf propriétés :

- `animation-name` : le nom de l’animation à utiliser ;
- `animation-duration` : la durée complète de l’animation ;
- `animation-delay` : le délai avant que l’animation ne se lance ;
- `animation-timing-function` : la méthode d’interpolation (départ rapide, lent...) entre chaque étape (voir plus bas) ;
- `animation-iteration-count` : le nombre de fois où l’animation est répétée. Le mot-clé `infinite` permet d'effectuer l'animation en boucle ;
- `animation-direction` : permet de jouer l'animation en sens inverse ;
- `animation-fill-mode` : état des éléments avant et après l'exécution de l’animation (voir plus bas) ;
- `animation-play-state` : permet de mettre l’animation en pause ;
- `animation` : c’est la propriété raccourcie des huit précédentes.

Par défaut, la durée est de 0 seconde, le nombre de répétitions est 1 et la méthode d’interpolation est `ease`. Les autres propriétés sont optionnelles. 
Cela signifie que le code minimal pour lancer une animation définie avec `@keyframes` est :

~~~ {lang="css" line="1"}
#elem {
    animation: nomAnim 1s;
}
~~~

Exemple d’une animation sur la taille et la couleur d’arrière-plan, de manière infinie :

~~~ {lang="css" line="1"}
@keyframes anim1 {
    from {
        width: 300px;
        background: greenyellow;            
    }
    50%  {
        width: 600px;
        background: deepskyblue;    
    }
    to   {
        width: 450px;
        background: yellowgreen;            
    }
}
#elem {
    animation: anim1 3s infinite; 
}
~~~

[Voir la démonstration 2](http://jsfiddle.net/iamvdo/62vW8/)


## Ajouter une transition/animation

Nous l’avons vu, une transition/animation se lance lors d’un changement d’état. Mais à quel endroit appliquer les propriétés ?  
Il y a trois cas de figure qui fonctionnent de la même façon pour les transitions et les animations :


### Lors du changement d’état 

~~~ {lang="css" line="1"}
ul a img {
    margin-right: 5px;
}
ul a:hover img {
    margin-right: 15px;
    transition: margin-right 0.5s;
}
~~~

Dans ce cas, la transition aura lieu lorsque la souris arrive sur l’élément, mais pas lorsqu’elle le quitte.

[Voir la démonstration 3](http://jsfiddle.net/iamvdo/vje4v/)


### À l’état initial 

~~~ {lang="css" line="1"}
ul a img {
    margin-right: 5px;
    transition: margin-right 0.5s;
}
ul a:hover img {
    margin-right: 15px;        
}
~~~

Dans ce cas, la transition aura lieu lors des deux évènements : lorsque la souris arrive sur l’élément et lorsqu’elle le quitte.

[Voir la démonstration 4](http://jsfiddle.net/iamvdo/hMAZX/)


### À l’état initial et lors du changement d’état 

~~~ {lang="css" line="1"}
ul a img {
    margin-right: 5px;
    transition: margin-right 0.2s 1s;
}
ul a:hover img {
    transition: margin-right 0.5s;        
}
~~~

Dans ce cas, deux transitions ont lieu. Lorsque la souris arrive sur l’élément, une transition de 0.5 secondes est lancée. Lorsqu’elle le quitte, c’est une transition de 0.2 secondes mais avec un délai de 1 seconde.

[Voir la démonstration 5](http://jsfiddle.net/iamvdo/S4nLy/)


## Contrôler les transitions/animations

Bien que les contrôles restent simples, il est toutefois possible de réaliser quelques opérations intéressantes. C’est surtout le cas pour les animations CSS qui permettent plus de finesse dans les réglages.

### Modifier la méthode d’interpolation

La méthode d’interpolation spécifie la façon dont l’animation évolue dans le temps. C’est la propriété `*-timing-function`. Par exemple, lors d’une transition de `width: 50px;` à `width: 100px;` qui dure 2 secondes, la largeur ne sera pas forcément 75px à 1 seconde ! L’évolution de l’animation peut être définie par 5 mots-clés et 2 fonctions :

- `linear` : méthode linéaire ;
- `ease` : le départ est rapide, l’accélération lente. L’accélération semble naturelle ;
- `ease-in` : le départ est lent. L’arrivée semble donc plus rapide ;
- `ease-out` : l’arrivée est lente. Le départ semble donc plus rapide ;
- `ease-in-out` : le départ et l’arrivée sont lents ;
- `cubic-bezier(p2x,p2y,p3x,p3y)` : courbe d’accélération personnalisée ;
- `steps(nb, sart|end)` : animation par palier (image par image). Les transitions/animations ne sont plus fluides.

![Schéma des courbes de Bézier par défaut des transitions et animations CSS](trTimingFn.png )

[Voir la démonstration 6](http://jsfiddle.net/iamvdo/3JSsM/)

#### La fonction `cubic-bezier()`

La fonction `cubic-bezier()` permet un contrôle poussé de la courbe d’accélération (même si nous sommes encore très loin des capacités de Flash). Quatre points p1, p2, p3, p4 sont nécessaires pour définir une courbe de Bézier. Les points p1 et p4 sont respectivement le point de départ et d’arrivée. Les points p2 et p3 sont les tangentes des points p1 et p4 qui définissent la direction et la longueur de la courbe. La fonction `cubic-bezier()` prend quatre paramètres qui sont respectivement :

- la valeur X du point p2 ;
- la valeur Y du point p2 ;
- la valeur X du point p3 ;
- la valeur Y du point p3.

Sachant que les points p1 et p4 sont obligatoirement le point (0,0) et (1,1). 

Les valeurs X doivent êtres comprises entre 0 et 1, car elles correspondent au temps qui passe. Les valeurs Y, elles, peuvent être inférieures à 0 ou supérieures à 1. Dans ce cas, des effets de rebonds peuvent êtres réalisés puisque les valeurs des propriétés seront hors bornes. Par exemple, lors d'une transition de `width: 50px` à `width: 100px`, il est possible que la valeur de `width` soit supérieure à 100px.

Voici un exemple utilisant deux courbes de Bézier personnalisées :

~~~ {lang="css" line="1"}
#elem {
    transition: 1s cubic-bezier( 0.5, 1, 0.5, 0.8); 
}
#elem {
    transition: 1s cubic-bezier( 0.5, 2, 0.5, 0.8);
}
~~~

![Deux exemples de courbes de Bézier personnalisées pour les transitions et animations CSS](trCubic.png )

[Voir la démonstration 7](http://jsfiddle.net/iamvdo/ybMTn/)

Liens utiles pour comprendre les courbes de Bézier en CSS :

- [http://cubic-bezier.com](http://cubic-bezier.com ) ;
- [Ceaser](http://letrainde13h37.fr/breves/ceaser-generateur-animation-easing-css/)


#### La fonction `steps()`

La fonction `steps()` permet de jouer une animation en mode “image par image”. Voici un exemple de ce qu’il est possible de réaliser à l’aide de *sprites* (bienvenue à l'époque des GIFs animés !) :

[Voir la démonstration 7a]( http://jsfiddle.net/iamvdo/cx4JB/ )


### Jouer une animation en sens inverse

Pour les animations uniquement, il est possible de prévoir que certains cycles soient joués en sens inverse.
La propriété `animation-direction` accepte 4 valeurs :

- `normal` : l’animation est jouée normalement, de l’étape 0 % (`from`) à l’étape 100 % (`to`) ;
- `reverse` : l’animation est jouée en sens inverse, de l’étape 100 % à l’étape 0 % ;
- `alternate` : l’animation est jouée normalement les cycles impairs (1,3...) et en sens inverse les cycles pairs (2,4,...) ;
- `alternate-reverse` : l’animation est jouée en sens inverse les cycles impairs (1,3...) et normalement les cycles pairs (2,4..).

Cette propriété est très pratique pour revenir à l’état d’origine en jouant une animation en sens inverse, ou pour réaliser des effets d’apparition/disparition.

~~~ {lang="css" line="1"}
@keyframes pulse {
    from {
        box-shadow: 0 0 0px deepskyblue;
    }
    to {
        box-shadow: 0 0 14px deepskyblue;
    }
}
input:focus {
    animation: pulse 1s infinite alternate;
}
~~~

[Voir la démonstration 8]( http://jsfiddle.net/iamvdo/cEGWp/ )


### Gérer l’état des éléments animés avant et après l’animation

Par défaut, une animation modifie les valeurs des propriétés pendant son exécution uniquement. Cela signifie qu’avant le début de l’animation, les éléments sont tels que définis dans le code CSS, et qu’à la fin de l’animation, les éléments reviennent à leur état d’origine. La propriété `animation-fill-mode` permet donc de conserver l’état de fin ou de début d’animation avant que celle-ci ne soit jouée. Les valeurs sont :

- `backwards` : les éléments sont tels que définis à l’étape 0 % de l’animation avant le début de celle-ci ;
- `forwards` : les éléments sont tels que définis à l’étape 100 % de l’animation après la fin de celle-ci ;
- `both` : combinaison de `backwards` et `forwards` ;
- `none` : par défaut.

Voici un exemple ou les 4 cas sont mis en situation. Un élément centré subit une animation qui modifie sa position et simule un rebond :

- Cas 1: `none` : l'élément est modifié lors de l'animation et revient à son état d'origine à la fin ;
- Cas 2: `backwards` : avant l'animation, l'élément est en haut (état `from`). À la fin, l'élément revient en position d'origine (centrée) ;
- Cas 3: `forwards` : avant l'animation, l'élément est centré. À la fin, l'élément reste en bas (état `to`) ;
- Cas 4: `both` : l'élément est en haut au départ et reste en bas à la fin.


[Voir la démonstration 9](http://jsfiddle.net/iamvdo/pRm9g/ )


## Les limitations 

Bien que tout paraisse rose, certaines limitations existent. En voici quelques unes :

- Toutes les propriétés ne sont pas animables. Par exemple, une transition/animation de `display: none;` à `display: block;` n’est pas possible. Voici [la liste complète des propriétés animables](http://www.w3.org/TR/css3-transitions/#animatable-properties ) ;
- Les étapes d’une animation se définissent en pourcentage de l’animation totale. Dans le cas d’une animation précise, il est souvent nécessaire de définir des nombres décimaux à rallonge (par exemple 33.333%). Il serait parfois plus évident de définir les étapes en secondes ;
- Les transitions/animations sont censées fonctionner sur les pseudo-éléments (`::before` et `::after`), mais malheureusement seul Firefox les supporte ;
- Lorsqu’un délai est fixé, il n’est valable que pour la première itération d’une animation. Pour lancer une animation avec un délai à chaque itération, il faut bien souvent ruser et créer une animation qui n’effectue aucune tâche pendant les n premiers pourcentages (ce qui n’est pas toujours simple) ;
- Il n’existe pas de synchronisation à proprement parler. Par exemple, il n'est pas possible de lancer une animation lorsqu'une autre se termine et dont la durée n'est pas connue. Cependant, de nouveaux évènements JavaScript sont propagés (voir plus bas) ;
- Les animations ne peuvent pas suivre un chemin ou une forme (peut-être dans le futur en utilisant le principe des formes définies dans [le module des Exclusions CSS](http://dev.w3.org/csswg/css3-exclusions/ )) ;
- Et bien entendu, toutes les limitations liées au langage CSS lui même: pas de variable, pas de calcul, pas de changement de valeurs pendant le déroulement d’une transition/animation...  


## Les bonnes pratiques d’intégration

Je vous entends déjà dire : « C’est bien beau les transitions/animations mais en pratique ça donne quoi ? C’est trop tôt, hein ? »  
Et bien non, et ce pour deux raisons :

- le W3C a [demandé aux navigateurs de retirer les préfixes vendeurs](https://twitter.com/csswg/status/210404244682055680 ). Cela signifie donc que les spécifications sont assez matures pour êtres utilisées ;
- tous les navigateurs du marché [supportent déjà les transitions/animations](http://caniuse.com/#feat=css-animation,css-transitions ) (au moins dans leur version la plus récente). Opera 12.5, Firefox 16 et IE10 sont même déjà compatibles avec les versions non préfixées des propriétés.

Il est vrai qu’à l’heure actuelle (septembre 2012), les transitions/animations doivent encore êtres préfixées pour pouvoir êtres utilisées sur certains navigateurs. Mais dans très peu de temps, ce ne sera plus nécessaire. Ce n’est qu’une question de mois ! La mise en place des transitions/animations doit cependant se faire sur le principe de l’amélioration progressive (*progressive enhancement*), c’est à dire qu’elles doivent êtres mises en place pour améliorer l’expérience l’utilisateur, sans interférer avec les fonctionnalités du site ni rendre un élément inaccessible ou inutilisable. Le site doit être fonctionnel avant l’ajout des transitions/animations. Il n’est donc pas primordial (voire tout simplement utile) de mettre en place des solutions de repli pour les navigateurs non compatibles. Cependant, des solutions existent :

- [jQuery animate()](http://api.jquery.com/animate/ ) ;
- [jQuery Transition](http://louisremi.github.com/jquery.transition.js/test/index.html ) ;
- [jQuery Animate Enhanced](https://github.com/benbarnett/jQuery-Animate-Enhanced ) ;
- Les solutions de [David Catuhe](http://blogs.msdn.com/b/eternalcoding/archive/2011/11/24/fr-introduction-224-css3-transitions.aspx ) et [David Rousset](http://blogs.msdn.com/b/davrous/archive/2011/12/06/introduction-aux-animations-css3.aspx#fallback ).

Voici un exemple complet avec préfixes (le préfixe `-ms-` a été volontairement ôté, puisque IE10 supporte la version non-préfixée et qu’IE9 et inférieurs ne supportent pas du tout les transitions) :

~~~ {lang="css" line="1"}
#elem {
    -webkit-transition: width 2s ease-out;
    -moz-transition: width 2s ease-out;
    -o-transition: width 2s ease-out;
    transition: width 2s ease-out;
}
~~~

## Exemples d’intégration

Voici à titre d’apprentissage et d’inspiration quelques intégrations des transitions et animations :

- [Galerie photo avec survol](http://www.css3create.com/Galerie-photo-hover-avec-transition-CSS ) ;
- [Galerie photo avec décalage horizontal](http://www.css3create.com/Astuce-Empecher-le-scroll-avec-l-utilisation-de-target ) ;
- [Fondu sur images](http://css3.bradshawenterprises.com/cfimg/ ).


## Aller plus loin : les évènements JavaScript

Afin d’intégrer les transitions et animations dans un contexte d’application JavaScript, de nouveaux évènements peuvent êtres récupérés. Il est par exemple possible de détecter la fin d'une transition ou encore le début, la fin ou la répétition d’une animation. Les évènements sont donc respectivement: `transitionend`, `animationstart`, `animationend`, `animationiteration`.

Pour les utiliser, il faut d’abord “écouter” l’un des évènements et attacher une fonction qui sera exécutée lorsque l’évènement se produira :

~~~ {lang="css" line="1"}
var elem = document.getElementById(‘elem’);
elem.addEventListener(‘transitionend’, function(e) {
    alert(‘La transition “‘+e.propertyName+’” est finie!’);
}, false);
~~~

[Voir la démonstration 10](http://jsfiddle.net/iamvdo/RVrAc/ )

Comme pour les propriétés, les évènements doivent encore être préfixés. Le tableau suivant précise la syntaxe pour chaque préfixe (avec pour exemple `transitionend`) :

<table>
   <thead>
    <tr>
        <th>Préfixe</th><th>Evènement</th>
    </tr>
   </thead>
   <tbody>
    <tr>
        <td align="center">-webkit-</td><td align="center">webkitTransitionEnd</td>
    </tr>
    <tr>
        <td align="center">-moz-</td><td align="center">transitionend</td>
    </tr>
    <tr>
        <td align="center">-ms-</td><td align="center">MSTransitionEnd</td>
    </tr>
    <tr>
        <td align="center">-o-</td><td align="center">oTransitionEnd</td>
    </tr>
   </tbody>
</table>

Grâce à ces évènements, il devient donc possible de synchroniser les transitions/animations, comme par exemple lancer une animation lorsqu'une autre se termine ou commence via l'ajout de l'attribut `class` en JavaScript. Dans le cadre d’une mise en place en production, pensez à utiliser [Modernizr](http://www.modernizr.com ), une librairie JavaScript qui simplifie l’utilisation des préfixes et aide à la mise en place de l’amélioration progressive.


## Conclusion

Les transitions/animations ne doivent pas êtres vues comme quelque chose de futile ou superflu. Au contraire, elles sont une valeur ajoutée incontournable dans tout design web d’aujourd’hui. Il faut cependant apprendre à les mettre en place avec parcimonie, car leur utilisation trop intensive peut vite provoquer l’effet inverse, à savoir un effet brouillon. De plus, certaines limitations liées à la performance du navigateur peuvent êtres ressenties, notamment une perte de fluidité ou des délais non respectés. Ce n’est pas parce que tout est possible qu’il faut obligatoirement tout faire...
