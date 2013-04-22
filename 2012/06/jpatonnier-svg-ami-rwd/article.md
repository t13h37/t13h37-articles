# SVG, l’ami du Responsive Web Design

Depuis le temps qu'on vous en parle, vous devez commencer à savoir ce qu'est le "*Responsive Web Design*" (que j'appellerai ici très abusivement design adaptatif). Une des plus grosses difficultés liées à cette approche de la conception Web, ce sont les images. Entre les différents "break points" qui vont nécessiter des images de tailles différentes et les super écrans haute densité qui requièrent des images parfois deux fois plus grandes que celle de leur taille d'affichage réel, ce n'est pas simple.  
Sans parler qu'on ne sait pas de quoi demain sera fait en la matière.

Parmi toutes les solutions plus ou moins pertinentes pour gérer cette question, peu de gens pensent à utiliser le format d'image SVG. Voyons un peu cela en détail.

## Qu'est-ce que SVG

SVG est un format d'image vectoriel reposant sur une syntaxe XML. Cela lui confère deux avantages spécifiques sur le Web :

- En tant que format d'image vectoriel, il permet de redimensioner une image sans aucune perte de qualité ;
- En tant que format XML, il permet de bénéficier de toute la puissance de JavaScript et surtout de CSS.

Plutôt qu'un long et fastidieux discours, voilà à quoi ressemble une image SVG.

<object data="http://letrainde13h37.fr/wp-content/uploads/2012/06/cupcake.svg" width="110" height="110" type="image/svg+xml">
    <!-- Une solution de repli pour les navigateurs qui ne comprennent pas SVG -->
    <img src="http://letrainde13h37.fr/wp-content/uploads/2012/06/cupcake.png" width="110" height="110" alt="" />
</object>

Côté code :

~~~ {lang="svg" line="1"}
<svg xmlns="http://www.w3.org/2000/svg" 
     xmlns:xlink="http://www.w3.org/1999/xlink" 
     width="110px" 
     height="110px" 
     viewBox="-5 -5 110 110">
<path class="cake" 
      fill="#583702" 
      d="..."/>
<path class="cream"  
      fill="#FCFAF2" 
      stroke="#F7E9AA" 
      stroke-width="3" 
      d="..."/>
</svg>
~~~

Notez que je vous épargne la valeur de l'attribut `d` des balises `<path>` qui est sans aucun doute la partie la plus difficile de SVG, mais pas d'inquiétude, comme nous allons tout de suite le voir, il y a de nombreuses façons de s'en passer.

## Produire une image SVG

Il y a deux grandes façons de produire une image au format SVG, la méthode des développeurs et celle des designers :

### La méthode des développeurs

SVG reposant sur XML, il est tout à fait possible de produire du SVG à la main. Ce n'est pas très difficile mais nécessite tout de même d'apprendre un nouveau langage en plus de HTML, CSS et JavaScript. C'est une bonne idée, mais cela prend toujours un peu de temps.

Si vous voulez vous lancer dans cette aventure, je vous invite à [consulter les ressources présentes sur le Developer Mozilla Network](https://developer.mozilla.org/en/SVG) pour de plus amples informations.

Il existe également quantité de bibliothèques permettant de générer du code SVG.  
À titre d'exemple, vous avez :

- [Raphael en JavaScript](http://raphaeljs.com/)
- [Batik en Java](http://xmlgraphics.apache.org/batik/)
- [SharpVectors en C#](http://sharpvectors.codeplex.com/)

Il existe également des bibliothèques plus spécialisées comme celles dédiées à la création de graphiques :

- [HighCharts en JavaScript](http://www.highcharts.com/)
- [Zingchart en JavaScript](http://www.zingchart.com)
- [SVGGraph en PHP](http://www.goat1000.com/svggraph.php)
- [SVG::Graph en Ruby](http://www.germane-software.com/software/SVG/SVG::Graph/)

### La méthode des designers

Pour les gens qui ne veulent pas mettre les mains dans le code (et il y en a beaucoup dès qu'il est question d'images), il existe des logiciels de dessin qui permettent de produire facilement des images SVG.  
Parmi les plus connus, on trouve :

- [Adobe Illustrator](http://www.adobe.com/fr/products/illustrator.html)
- [Inkscape](http://inkscape.org/?lang=fr)
- [SVG Edit](http://svg-edit.googlecode.com/svn/branches/2.5.1/editor/svg-editor.html)
- [Aviary Raven](http://advanced.aviary.com/tools/vector-editor)

La qualité du code SVG produit par ces différents logiciels est assez inégale et dépend beaucoup du soin que vous prendrez à utiliser ces outils.

À titre d'exemple, Illustrator est un cas d'école de cette question. Le code qu'il produit est assez propre si vous faites très attention à faire des choses "simples". Faire des choses simples ne signifie pas que l'image doit être basique et toute moche, que nenni. Cela signifie que vous devez prendre soin de n'utiliser que des fonctionnalités du logiciel compatibles avec SVG.

Pour ne pas vous laisser seul face à l'inconnu, voici une petite liste de bonnes pratiques pour produire du SVG utilisable dans les meilleures conditions avec Illustrator :

- Nommez systématiquement vos calques mais aussi vos groupes de formes ;
- N'utilisez que les dégradés linéaires et radiaux (en clair, cela signifie qu'il ne faut jamais utiliser le filet de dégradé d'Illustrator) ;
- N'utilisez jamais les effets de filtre Photoshop disponibles dans Illustrator, et de manière générale, essayez d'éviter les effets Illustrator ;
- Si vous utilisez, la "distorsion d'enveloppe", transformez toujours le résultat en une forme définitive (avec l'option "Décomposer") ;
- Si vous utilisez les fonctions de "*Pathfinder*", assurez vous toujours que le résultat est une forme définitive.

Enfin, sachez qu'il existe nombre de ressources en ligne qui proposent des images vectorielles (et donc facilement convertibles en SVG) prêtes à l'emploi et d'excellente qualité, en particulier pour tout ce qui touche à la création d'icônes.

À titre d'exemple, on peut citer :

- [The Noun Project](http://thenounproject.com)
- [Open Clip Art](http://openclipart.org)
- [DryIcons](http://dryicons.com/free-graphics/)
- [MediaLoot](http://medialoot.com/browse/all/date/all/vector/free/)

## Inclure une image SVG dans une page HTML

À présent que vous savez produire des images SVG, voyons comment les exploiter concrètement. Au sein d'HTML, il y a quatre grandes méthodes pour intégrer du SVG.

### La méthode historique : la balise `<object>`

La façon la plus sûre et la plus fiable d'intégrer une image SVG dans un document HTML passe par l'utilisation de la balise `<object>` :

~~~ {lang="html" line="1"}
<object data="cupcake.svg" width="110" height="110" type="image/svg+xml">
    <!-- Une solution de repli pour les navigateurs qui ne comprennent pas SVG -->
    <img src="cupcake.png" width="110" height="110" alt="" />
</object>
~~~

Le très gros avantage de cette méthode c'est qu'elle permet très facilement de gérer les solutions de repli dans le cas où un navigateur ne supporte pas le format SVG (Internet Explorer 8 et le navigateur natif de Android 2.x pour ne pas les nommer). En effet, si un navigateur ne comprend pas l'objet référencé par la balise `<object>`, il affichera alors le contenu HTML présent à l'intérieur de la balise.

### La méthode naturelle : la balise `<img>`

SVG étant un format d'image, tous les navigateurs le supportant permettent d'afficher une image de ce format via la balise `<img>` :

~~~ {lang="html" line="1"}
<img src="cupcake.svg" width="110" height="110" alt="" />
~~~

La principale différence entre cette méthode et l'utilisation de la balise `<object>` tient en deux points :

- Premièrement, la gestion des solutions de repli autres qu'un simple texte alternatif est bien plus compliquée avec la balise `<img>` (et souvent à base de JavaScript ce qui peut parfois être considéré comme une mauvaise pratique).
- Deuxièmement, certaines fonctionnalités avancées de SVG ne seront pas disponibles via la balise `<img>` (i.e. l'utilisation des scripts).

### La première méthode moderne : SVG dans du HTML

L'arrivée de HTML5 offre une nouvelle façon d'inclure du SVG dans un document HTML : mettre directement du SVG dans le HTML ! Oui, tout simplement :

~~~ {lang="html" line="1"}
<body>
    <svg width="110" height="110">
        <!-- le reste du code SVG ici -->
        <foreignObject width="0" height="0" overflow="hidden">
            <!-- Une solution de repli pour les navigateurs qui ne comprennent pas SVG -->
            <img src="cupcake.png" width="110" height="110" alt="" />
        </foreignObject>
    </svg>
</body>
~~~

Cette technique, pour appétissante qu'elle soit, est encore très jeune et souffre de quelques problèmes :

- Le premier d'entre eux est que les navigateurs n'implémentent pas encore cette fonctionnalité exactement de la même façon.
- Le deuxième tient à la gestion des solutions de repli qui nécessite des contorsions assez contre-intuitives via [la balise SVG `<foreignObject>`](https://developer.mozilla.org/en/SVG/Element/foreignObject).
- Enfin, cela nécessite forcément de connaître SVG ce qui, comme on l'a vu ci-avant, n'est pas le cas de tout le monde.

### La deuxième méthode moderne : CSS

Enfin, tout comme pour l'utilisation de la balise `<img>`, tous les navigateurs qui supportent SVG acceptent d'utiliser les images de ce format partout où l'on peut mettre une image en CSS, en particulier avec la propriété `background-image`.

~~~ {lang="css" line="1"}
div {
    background-image: url(cupcake.svg);
}
~~~

Cette solution est une des plus utiles mais est elle aussi très jeune et souffre encore de quelques petits bugs. Les différents navigateurs n'en sont qu'au début de l'implémentation de cette solution et il existe encore quelques cas où l'on constate qu'un arrière-plan redimensionné va apparaître pixellisé comme s'il s'agissait [d'une image rasterisée](http://fr.wikipedia.org/wiki/Rast%C3%A9risation) alors qu'en fait, non. Et pour corser les choses, les cas où l'image va se comporter de cette étrange manière changent d'un navigateur à l'autre. Bon, certes, ce n'est pas parfait, mais les choses s'améliorent très vite (en particulier avec Firefox et Chrome qui sont tous les deux en cycle de développement rapide avec une nouvelle version toutes les 6 semaines).

À noter que cette dernière technique est une des plus difficile à gérer en matière de solution de repli. En effet, si pour les vieux Internet Explorer il est toujours possible de proposer une feuille de style alternative grâce aux commentaires conditionnels, rien n'existe pour les navigateurs Android. La seule solution consiste éventuellement à faire appel à JavaScript pour détecter les fonctionnalités du navigateur comme avec [Modernizr](http://modernizr.com/).

## Et le "responsive design" dans tout ça

On y vient. Maintenant que vous avez une image SVG et que vous savez comment l'inclure dans votre document HTML, voyons en quoi cela peut nous servir dans le cadre d'un design adaptatif.

### Redimensionnement

Le principal intérêt du SVG, c'est sa capacité à être redimensionné sans perte de qualité directement au sein du navigateur. Ainsi, que ce soit pour des logos, des icônes ou toutes les images pouvant bénéficier d'un traitement vectoriel (c'est-à-dire à peu près toutes sauf les photos), vous n'aurez qu'une seule image à gérer quelles que soient les capacités de vos terminaux.

Pour gérer le redimensionnement, vous avez deux méthodes possibles :

#### HTML

Avec les balises HTML `<img>` et `<object>`, il vous suffit de leur spécifier une taille en pourcentage (via les attribut HTML ou mieux, via CSS) pour qu'ils s'adaptent automatiquement à la taille de leur conteneur :

~~~ {lang="html" line="1"}
<div id="monContenu">
    <img src="cupcake.svg" width="100%" alt="" />
</div>

<style>
@media all {
    #monContenu {
        width: 220px;
    }
}

@media all and (max-width: 800px) {
    #monContenu {
        width: 110px;
    }
}

@media all and (max-width: 480px) {
    #monContenu {
        width: 55px;
    }
}
</style>
~~~

Bien évidemment, vous pouvez également directement cibler votre image avec CSS si vous préférez. Un exemple de cas d'usage parfait pour ce genre d'utilisation : ce sont tous les cas où vous voulez mettre des images en ligne dans un texte, des *smileys*, des flèches, des icônes, etc.  
Réalisez vos images avec SVG et mettez-les dans votre code de la manière suivante :

~~~ {lang="html" line="1"}
<p>Un peu de texte <img src="mon-smiley.svg" class="smiley" alt="" /> et encore du texte</p>

<style>
.smiley {
    height: 1em;
    vertical-align: middle;
}
</style>
~~~

Notez que si vous voulez utiliser directement du SVG dans du HTML, la qualité des implémentations ne permet pas de spécifier des tailles en pourcentage. Tout simplement parce que les différents navigateurs ne sont pas d'accord sur la façon dont il faut calculer ces valeurs relatives.

#### CSS

Avec CSS, nous disposons également d'outils nous permettant de contrôler finement la taille de nos images SVG. En particulier, la propriété CSS3 `background-size` nous permet de contrôler la taille des images d'arrière-plan.

~~~ {lang="html" line="1"}
<div id="monConteneur">
    Un peu de texte pour bien voir l'effet...
</div>
~~~

~~~ {lang="css" line="1"}
#monConteneur {
    background-image: url(mon-image.svg);
    background-size: 90px auto;
    background-position: left top;

    padding: 0 0 0 100px;
}

@media all and (max-width: 480px) {
    #monConteneur {
        background-size: contain;
        background-position: center bottom;

        padding: 0 0 100px 0;
    }
}
~~~

La propriété `background-size` prend deux types de valeur : soit une paire de nombres valeurs indiquant explicitement la largeur puis la hauteur de l'image, soit un mot-clé "`contain`" ou "`cover`".

- "`contain`" signifie que l'image d'arrière-plan va être redimensionnée pour être aussi grande que possible tout en s'assurant que ses largeur et hauteur restent toujours plus petites ou égales à celles de son conteneur (bref, l'image fera toute la taille du conteneur mais sans dépasser).
- "`cover`" signifie que l'image d'arrière-plan va être redimensionnée pour être aussi petite  que possible tout en s'assurant que ses largeur et hauteur sont toujours supérieures ou égales aux dimensions de son conteneur (cela signifie que l'image couvrira toute la surface visible et sera vraisemblablement coupée dans l'une ou l'autre de ses dimensions).

Ce que nous venons de voir concernant le redimensionnement est également envisageable avec des images *bitmap* (JPEG, PNG). Malheureusement, cela se paie souvent au prix d'une démultiplication du nombre d'images pour éviter de ne travailler qu'avec des images haute définition extrêmement lourdes. Cela aura donc un impact sur la maintenablité du design tout au long du cycle de vie de votre projet. Grâce à SVG, vous pourrez simplifier les choses de ce point de vue en n'utilisant qu'une seule image pour tous les cas de figure.

### Encore plus loin avec les média CSS

Ce que nous allons voir à présent est véritablement spécifique au format SVG. Comme nous l'avons dit, ce format repose sur une syntaxe XML. Grâce à cela, ses concepteurs ont pu lui donner la capacité de comprendre et d'utiliser CSS directement à l'intérieur du format lui-même.

Cette capacité va nous permettre de réaliser un tour de force unique en matière de design adaptatif : modifier l'apparence même de l'image, bien au-delà d'un simple changement de taille. Un bon exemple valant mieux qu'un long discours, voici ce que cela permet :

~~~ {lang="svg" line="1"}
<svg xmlns="http://www.w3.org/2000/svg" 
     xmlns:xlink="http://www.w3.org/1999/xlink" 
     width="110px" 
     height="110px" 
     viewBox="-5 -5 110 110">

    <style>
    .cake {
        fill: #583702;
    }

    .cream {
        fill: #FCFAF2;
        stroke: #F7E9AA;
        stroke-width: 3px; 
    }

    @media print {
        .cake {
            fill: #000;
        }

        .cream {
            fill: #FFF;
            stroke: #000;
        }
    }
    </style>

    <path class="cake" d="..."/>
    <path class="cream" d="..."/>
</svg>
~~~

Avec cette feuille de style directement au sein de l'image, celle-ci va s'afficher en couleur dans votre navigateur mais si vous lui demander de l'imprimer, elle sera alors imprimée en N&B avec les contrastes de votre choix.

Ainsi, selon le contexte dans lequel sera rendue l'image, vous allez pouvoir définir précisément comment elle sera vue. 

De très nombreuses applications sont possibles :

- Changer les couleurs pour l'impression ;
- Masquer des textes trop petits sur les mobiles ;
- Afficher des détails supplémentaires sur les grands écrans ;
- Ajuster les contrastes ;
- Repositionner ou distordre les éléments…

La seule limite, c'est votre imagination.

## Conclusion

Comme on le voit, même avec ses fonctionnalités de dessin les plus basiques, SVG est un format idéal pour résoudre nombre de problèmes liés au design adaptatif tel qu'on le pratique aujourd'hui.

Pas de fausse promesse non plus, les techniques évoquées ici ne sont pas (encore) la panacée.  
Cela tient à deux facteurs qu'il est important de garder en tête :

- Premièrement, SVG est un format particulier qui a ses propres mécanismes parfois radicalement différents de HTML (tout ce qui touche au texte par exemple, car SVG ne connait pas la notion de flux de  texte). Cela lui donne un côté contre-intuitif et implique un temps d'apprentissage qui n'est pas anodin si vous voulez être efficace rapidement avec cette technologie.
- Deuxièmement, l'usage "grand public" de cette technologie est beaucoup plus récent que celui de HTML. Concrètement, ça veut dire que les  constructeurs de navigateurs l'ont mise en œuvre beaucoup plus récemment et que  vous serez donc plus facilement confrontés à des bugs ou à des incohérences d'interprétation, surtout si vous sortez de la zone bien maîtrisée du dessin (les animations, les filtres, les masques, les  fontes, etc.)

Mais pas d'affolement non plus, commencez par des choses simples : un cercle par-ci, un graphique autogénéré par-là. Ensuite, vous pourrez passez à des icônes de-ci de-là et puis un jour vous ne vous rendrez même plus compte que vous l'utilisez partout. Tous les collègues à qui j'ai fait découvrir ces techniques ont compris que c'est tout un horizon graphique et technique qui s'ouvre devant eux. Certains m'ont même dit qu'ils retrouvaient le plaisir qu'ils avaient eu à découvrir CSS.

À vous désormais de partir explorer ce nouveau monde pour en tirer le meilleur et rajouter ainsi une corde à votre arc.

**Vous pouvez [télécharger les fichiers de démo](http://letrainde13h37.fr/wp-content/uploads/2012/06/120612-exemples-article-SVG-patonnier) reprenant les exemples de cet article.**
