# Découverte de la propriété CSS border-image

En bossant sur une petite démo HTML / CSS, j'ai découvert une "nouvelle" propriété CSS : **`border-image`**. En fait, découvert n'est pas le bon mot, il serait plus correct de dire que je me suis véritablement cassée les dents sur ladite propriété, tellement elle est difficile à utiliser.

À première vue, on pourrait croire que `border-image` permet de définir une image pour chaque bordure d'un élément, un peu comme le `border` traditionnel, avec ses variantes `right`, `left`, `top` et `bottom`. Ce serait trop simple !  
En fait, cette propriété est un rêve pour les intégrateurs et développeurs &#39;&#39;front-end''. Mais si, ça a bien dû déjà vous arriver, cette discussion designer-développeur, où le designer vous explique que sa maquette avec ses belles bordures, ça dépote tout question visibilité / ergonomie, et où le développeur répond que ça va être galère à intégrer. Et bien `border-image` est fait pour ce genre de problématiques.  
Par contre, cette fonctionnalité demande un peu de patience pour être maîtrisée. En voiture !

## Syntaxe

Contrairement à ce qu'on pourrait penser, `border-image` permet de découper une image en zones puis de l'appliquer sur un élément. Avant, si on tombait sur une boîte avec des bordures assez complexes, on pouvait découper l'image et la boîte en 9 parties (coins, longueurs et hauteurs) pour intégrer tout ça. `Border-image` va le faire tout seul.  
Cette propriété s'articule en cinq valeurs :

~~~ {lang="css" line="1"}
border-image: source || slice || width || outset || repeat;
~~~

Avant de se lancer dans cette propriété et tous ses attributs il faut d'abord définir la bordure en question. Tout le monde sait comment marche la propriété border, pas besoin de faire un rappel. Ne vous souciez pas trop des valeurs de cette déclaration, seule la largeur va être importante.

~~~ {lang="css" line="1"}
border: double orange 27px;
~~~

Cette première déclaration étant faite, nous pouvons nous lancer dans le premier attribut de la propriété, à savoir **la `source`**.

### Source

Ici, aucune difficulté particulière, l'attribut prend pour valeur une image de n'importe quelle type. Techniquement, on peut même y mettre du SVG, mais nous verrons plus tard que l'implémentation ne suit pas toujours les spécifications, qui sont encore au stade de brouillon.  
Voici donc notre image d'exemple :

~~~ {lang="css" line="1"}
div {
    border: double orange 1px;
    border-image-source: url(small-border.png);
}
~~~

### Slice

Maintenant que l'image est définie, il va falloir la découper. Ca tombe bien, **`slice`** veut dire « tranche » en anglais. C'est donc cet attribut qui va s'en charger. Il va prendre en paramètre un nombre positif, dont l'unité est le pixel, ou des pourcentages. Pour l'ordre d'application, ça fonctionne comme d'habitude (`padding`, `margin`, `border`...) :

- **1 valeur** : a pour `top`, `right`, `bottom` et `left` ;
- **2 valeurs** : a pour `top` et `bottom`, et b pour `right` et `left` ;
- **3 valeurs** : a pour `top`, b pour `right` et `left`, c pour `bottom` ;
- **4 valeurs** : a pour `top`, b pour `right`, c pour `bottom`, d pour `left`.

Une petite grille d'exemple pour vous aider :

![Ici, le résultat sera donc... 25% 30% 12% 20%.](img1.png "Ici, le résultat sera donc... 25% 30% 12% 20%.")

Pour notre image d'exemple, qui est assez régulière, ce sera simple. L'image fait 81 px sur 81 px, et est donc découpée en 9 carrés de 27 px de côté.

~~~ {lang="css" line="1"}
div {
    border: double orange 1px;
    border-image-source: url(small-border.png);
    border-image-slice: 27;
}
~~~

![Ça commence à ressembler à quelque chose !](img2.png "Ça commence à ressembler à quelque chose !")

### Width

Maintenant, il va falloir définir la taille que l'image va prendre, soit le **`width`**. Vous allez me dire que l'on a déjà défini cette taille avec l'attribut `border`, mais en fait, c'est la bordure et non l'image qui a été définie. Ici, on va s'attaquer à l'image.  
Par défaut, cet attribut récupère la taille de la bordure. Mais on peut y appliquer un pourcentage, une valeur ou un nombre multiplicateur. La valeur par défaut pour cet attribut est 1, cela signifie que la valeur du `border-width` sera conservée.

~~~ {lang="css" line="1"}
div {
    border: double orange 1px;
    border-image-source: url(small-border.png);
    border-image-slice: 27;
    border-image-width: 0.5;
}
~~~

![La bordure a été réduite de moitié.](img3.png "La bordure a été réduite de moitié.")

### Outset

L'avant dernier attribut de cette propriété, c'est l'**`outset`**. Cela va correspondre à une forme de `padding` appliqué à la bordure et qui va donc la pousser sans varier la taille de la boîte ni la forme du contenu. Sa valeur est soit un chiffre en 1 et 4, qui sera utilisé comme un multiplicateur du `border-width`, soit une valeur en pixels.  
Sa valeur par défaut est de 0.

~~~ {lang="css" line="1"}
div {
    border: double orange 1px;
    border-image-source: url(small-border.png);
    border-image-slice: 27;
    border-image-width: 27px;
    border-image-outset: 26px;
}
~~~

![Un espace entre la bordure et le texte a été créé.](img4.png "Un espace entre la bordure et le texte a été créé.")

### Repeat

Dernières fonctionnalités mais pas des moindres, l'attribut **`repeat`** va définir la manière dont va se répéter l'image une fois découpée et positionnée. Ici, il y a quatre valeurs différentes :

~~~ {lang="css" line="1"}
div {
    border: double orange 27px;
    border-image-source: url(simple_border.png);
    border-image-slice: 27;
    border-image-width: 27px;
    border-image-outset: 26px;
    border-image-repeat: stretch;
}     
~~~

![L'image est étirée aux coins de l'élément.](img5.png "L'image est étirée aux coins de l'élément.")

~~~ {lang="css" line="1"}
div {
    border: double orange 27px;
    border-image-source: url(simple_border.png);
    border-image-slice: 27;
    border-image-width: 27px;
    border-image-outset: 26px;
    border-image-repeat: repeat;
} 
~~~

![L'image est répétée jusqu'au coin de l'élément.](img6.png "L'image est répétée jusqu'au coin de l'élément.")

~~~ {lang="css" line="1"}
div {
    border: double orange 27px;
    border-image-source: url(simple_border.png);
    border-image-slice: 27;
    border-image-width: 27px;
    border-image-outset: 26px;
    border-image-repeat: round;
} 
~~~

![L'image est répétée jusqu'au coin de l'élément, en arrondissant le nombre d'images répétées à un nombre entier.](img7.png "L'image est répétée jusqu'au coin de l'élément, en arrondissant le nombre d'images répétées à un nombre entier.")

~~~ {lang="css" line="1"}
div {
    border: double orange 27px;
    border-image-source: url(simple_border.png);
    border-image-slice: 27;
    border-image-width: 27px;
    border-image-outset: 26px;
    border-image-repeat: space;
} 
~~~

![L'image est répétée jusqu'au coin de l'élément, en arrondissant le nombre d'images répétées à un nombre entier. Si le nombre d'images répétées n'est pas entier, ces images sont étirées.](img8.png "L'image est répétée jusqu'au coin de l'élément, en arrondissant le nombre d'images répétées à un nombre entier. Si le nombre d'images répétées n'est pas entier, ces images sont étirées.")

Cet attribut peut être déclaré de la même manière que **`slice`**, soit en déclarant une valeur pour toutes les bordures, soit en définissant une valeur à une ou plusieurs bordures en particulier.

## Compatibilité et autres joyeusetés

Après tant de merveilles, il est temps de parler de choses pénibles : la **compatibilité**.

Mauvaise nouvelle : cette propriété n'est compatible nativement qu'avec très peu de navigateurs. En fait, seulement Google Chrome. Et encore, son implémentation est encore imparfaite, vu qu'il ne gère pas le `repeat round`.  
Pour utiliser `border-image` avec Firefox, Opera et Safari, il va falloir utiliser les préfixes correspondants et faire une croix sur certains attributs de cette fonctionnalité qui ne sont pas encore implémentés par ces navigateurs, comme l'`outset`. Pour cela, il va falloir utiliser la « syntaxe abrégée » :

~~~ {lang="css" line="1"}
div {
    border: double orange 27px;
    -webkit-border-image: url(simple_border.png) 27 27 round;
    -moz-border-image: url(simple_border.png) 27 27 round;
    -o-border-image: url(simple_border.png) 27 27 round;
    border-image: url(simple_border.png) 27 27px round;
}
~~~

![Voilà le résultat !](img9.png "Voilà le résultat !")

La méthode de fonctionnement est simple quand vous connaissez tous les attributs :

~~~ {lang="css" line="1"}
border-image: source slice width repeat;
~~~

Énorme point noir au tableau, Internet Explorer 9 ne supporte pas cette fonctionnalité. On suppose que IE10 la supportera, mais cela reste une supposition. Il faudra donc [tricher](http://css3pie.com/documentation/supported-css3-features/#border-image) pour l'utiliser avec ce navigateur !

## Conclusion

Pour conclure, `border-image` est donc une propriété puissante et utilisable. Nous avons vu qu'elle permet de gérer le style des bordures de manière très pointue.  
Le W3C fournit quelques exemples pour utiliser cette propriété, allant jusqu'à intégrer un [P'tit Écolier](http://www.w3.org/Talks/2012/0416-CSS-WWW2012/Demos/borders/demo-border-all.html). On peut aussi s'en servir pour [mettre en avant certaines parties d'une image](http://www.zurb.com/playground/awesome-overlays).  
Au final, vous ne serez limité que par votre imagination si vous choisissez d'utiliser cette propriété... Votre imagination et l'intégration qu'en font les navigateurs. À vous de tester !
