# Un pixel n'est pas un pixel

En cette époque moderne qui voit un changement technologique majeur tous les six mois sur le Web (j'exagère à peine), il est une vieille notion qui devient de plus en plus confuse : le pixel.

Ah, le pixel ! Une unité de mesure simple, stable et fiable. Euh... vraiment ? C'est qu'en ce moment, ce pixel est bien malmené. Entre les écrans _retina_ et les capacités de zoom des navigateurs mobiles, on a bien du mal à retrouver ses repères. Des images qui deviennent floues, des fenêtres qui ne font pas vraiment la taille qu'elles devraient faire... mon Dieu ! Mais qu'est-ce qu'ils ont fait à mon beau pixel ? Bon, pas de panique, nous allons prendre le temps d'expliquer tout ça en détail.

## Un peu d'histoire des technologies

Revenons sur les dernières évolutions technologique de ces dernières années pour comprendre un peu ce qui ce passe. En fait, il y a deux grand changements techniques qui ont modifié la notion de pixel :

### Le mobile et la notion de _viewport_

En 2007, un téléphone d'un nouveau genre fait sont apparition : l'iPhone. Ce nouvel appareil redistribue complètement les cartes de l'univers du mobile avec un changement majeur : il permet d'accéder au Web dans des conditions de confort et de qualité de rendu visuel inédites, proches de ce que l'on trouve sur desktop. Quelle magie vaudou se cache donc derrière ce tour de force ? La grande idée d'Apple a été d'amener la notion de _viewport_ sur le Web. Safari mobile a un comportement assez surprenant. Sur un appareil qui fait 320 pixels de large, il affiche un site web comme si la fenêtre du navigateur faisait en réalité 1024 pixels de large. Eh oui, la grande force de Safari mobile, c'est de mentir au site web qu'il affiche et de lui faire croire qu'il est dans une fenêtre plus grande que ce qu'elle est en réalité. De cette manière, par un habile jeu de transformation mathématique, un site qui n'avait jamais été pensé pour mobile s'affiche à peu près proprement sur un écran minuscule.

Ainsi avec cette notion de _viewport_, nous nous retrouvons tout d'un coup avec deux sortes de pixel : les pixels physiques qui définissent la résolution de l'écran d'un côté, et les pixels CSS qui sont utilisés par les développeurs web pour mesurer les dimensions des éléments dans la page affichée.

### L'arrivée des écrans _retina_

En 2010, Apple récidive en sortant l'iPhone 4 et son fameux écran "_retina_". Et là, c'est le drame ! En une nuit, des millions d'images deviennent floues. L'écran de l'iPhone 4 fait 640 x 980 pixels de large mais sur une taille d'écran qui n'a pas changé (elle fait toujours 3,5 pouces de diagonale). Or, si toutes les images sont devenues floues, les textes, eux, font toujours la même taille et, pire, ils apparaissent beaucoup plus nets et précis. Qu'est-ce que c'est que cette histoire ?

Eh bien, le truc c'est que si la densité de pixel physique a augmenté, le nombre de pixels qu'utilise le système iOS pour mesurer les dimensions et afficher les éléments à l'écran n'a pas changé, lui, et est toujours de 320 x 480 pixels. Dès lors, les textes sont dessinés à l'écran comme s'ils faisaient leur taille habituelle, et comme les textes sont des formes dites "vectorielles", elles bénéficient de la haute résolution de l'écran et sont donc affichées de manière beaucoup plus précises (plus de pixels physiques sont utilisés pour dessiner une même lettre). Les images, de leur coté, n'ont pas cette chance. Les formats les plus utilisés sur le Web sont des formats dits "_bitmap_" où l'image est définie pixel par pixel. Résultat, les images sont affichées à leur taille "normale" du point de vue du système d'exploitation (OS) mais, du point de vue de l'écran, c'est comme si on avait multiplié leur taille par 2 ou 3 sans rajouter de pixels supplémentaires pour compenser ce changement de taille. Résultat des courses, les algorithmes de changement de taille essaient de compenser ce manque de pixels physiques comme ils peuvent et très souvent... c'est flou.

Ainsi, avec ces nouveaux écrans haute densité, nous nous retrouvons là encore avec deux notions de pixel différentes. D'un côté nous avons toujours les pixels physiques qui représentent véritablement les petits points de lumière affichés par l'écran, et de l'autre côté nous voyons apparaitre la notion de pixel affiché (ou pixel OS) qui représente l'unité de référence du système d'exploitation pour calculer la taille des éléments à afficher à l'écran.

## Le côté obscur du pixel

Comme on vient de le voir, le mot pixel peut donc en réalité recouvrir trois notions assez différentes :

- Le pixel physique : il correspond à la définition historique du pixel et représente la plus petite tache de lumière qui peut être affichée sur un écran ;
- Le pixel OS : il correspond à la taille que va utiliser le système d'exploitation pour mesurer les dimensions des objets sur l'écran ;
- Le pixel CSS : il correspond à la taille que va utiliser un navigateur pour calculer les dimensions d'affichage d'un site Internet.

Pour faire simple : en coulisses, le navigateur va convertir les pixels CSS en pixel OS et le système d'exploitation va transformer ces pixels OS en pixels physiques pour concrétiser l'affichage.

### De quel pixel parle-t-on selon le contexte ?

Bon, OK, on a trois sortes de pixels. Le problème qui reste, c'est que lorsqu'on parle de pixel, personne ne dit duquel des trois il parle.
Voyons comment éviter la confusion

#### Le pixel CSS

C'est de lui dont il est question quand on parle de pixels dans le cadre d'un développement web. Dans de très, très nombreux cas, la taille du pixel CSS correspond à la taille du pixel OS. Mais il faut se méfier car ce n'est pas toujours vrai. En effet, un développeur web peut décider de changer la taille du pixel CSS. Pour cela, il y a deux outils possibles :

- [La balise ``meta viewport``](https://developer.mozilla.org/fr/docs/Mobile/Viewport_meta_tag), pour l'instant uniquement disponible sur les navigateurs mobiles, mais rien ne dit qu'elle ne fera pas son apparition un jour sur les navigateurs de bureau, sachant que [Opera à fait une proposition au W3C](http://dev.w3.org/csswg/css-device-adapt/) pour améliorer le concept ;
- [La propriété CSS ``transform``](https://developer.mozilla.org/fr/docs/CSS/transform#scale) qui permet, avec la fonction ``scale``, de changer la taille d'un élément et donc la taille des pixels CSS à l'intérieur de cet élément.

#### Le pixel OS

Très souvent, lorsqu'on évoque la résolution d'un écran (« mon écran à une résolution de 1900 x 1200 pixels ») on parle en fait du nombre de pixels qui sont utilisés par l'OS pour définir la taille de l'écran et donc pour calculer l'affichage des éléments.

#### Le pixel physique

Alors là, il y a un piège. Quand on parle de la taille d'une image dans un logiciel comme Photoshop, en fait, il s'agit de pixels physiques. C'est une des plus grosses sources de confusion que je connaisse chez les développeurs web que j'ai eu l'occasion de rencontrer.

La confusion vient du fait que très souvent, on définit la taille d'affichage d'une image via une feuille de style ou via des attributs HTML. À ce moment-là, l'unité qu'on utilise, le ``px`` représente bien sûr le pixel CSS. Ensuite, on va passer sur Photoshop pour préparer l'image et là, Photoshop nous demande quelle est la taille à donner à l'image **en pixels**. Le problème c'est que, pendant des années et des années, la taille du pixel CSS correspondait à la taille du pixel physique. Malheureusement, aujourd'hui ce n'est plus le cas, d'où les confusions fréquentes.

## Conclusion

À titre d'anecdote, je viens de l'univers du _print_, un univers où la taille des points est complètement dissociée de la taille des images. Ainsi, dans le _print_ il existe des notions comme la résolution (qui représente la densité de points par pouce). Eh bien, quand j'ai commencé sur le Web, le fait de ne plus avoir cette notion de densité de points était quelque chose de très difficile à appréhender. Je trouve donc très amusant de voir que des notions similaires sont en train de faire leur apparition en informatique et je comprends bien le désarroi des développeurs qui n'ont jamais eu à faire face à cette question.

Avec cet article, j'espère que vous y verrez maintenant plus clair et que l'utilisation du mot pixel (surtout dans le cadre du *responsive web design*) ne sera plus source de confusion ni de problème, voire de bugs.


