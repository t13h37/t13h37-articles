#Introduction à WebGL

Le 11 février 2011, la spécification  [WebGL 1.0](http://www.khronos.org/webgl/) a été publiée par le [Khronos Group](http://www.khronos.org/) − association d'industriels des domaines de l'informatique, du graphisme et du web. Basée sur l'API OpenGL ES 2.0 (Open Graphics Library for Embedded Systems), elle ouvre aujourd'hui aux navigateurs de dernière génération l'animation 3D en temps réel directement intégrée dans les pages web de façon ouverte, standard et performante.

Ajouter de l'image 3D au sein du navigateur a été depuis longtemps une gageure ou un mythe.
Des tentatives de création de moteurs 3D en Javascript ont été faites dans les années 2000, mais cela est resté proche de la démonstration technologique ou du tour de force technique : ni Javascript ni les navigateurs n'étaient vraiment taillés pour ce genre de performance et permettre une réalisation en production.

La seule alternative viable, performante et véritablement utilisable est restée dans le giron des plugins propriétaires. Le grand vainqueur dans ce domaine est Flash qui a permis grâce à ActionScript de voir apparaître des moteurs de rendu 3D très performants et d'une qualité graphique indéniable. Ainsi de nombreux jeux en ligne ou applications interactives ont vu le jour.   
Mais bien sûr, pour l'utilisateur, cela nécessite toujours l'installation d'un plugin, ce qui est souvent un frein à l'utilisation de ces technologies.


##Aujourd'hui l'arrivée de WebGL change la donne

WebGL est le portage du standard OpenGL ES 2.0 pour les navigateurs web.   
Le Khronos Group a mis au point la spécification pour créer une nouvelle API Javascript pour les navigateurs, afin de leur permettre d'atteindre directement les capacités matérielles des cartes graphiques 3D. Cette API permet de bénéficier de toute la puissance de traitement de ces cartes graphiques pour obtenir des images et des animations en temps réel directement dans la balise `<canvas>` d'HTML5.  
Le rendu s'effectue plusieurs dizaines de fois par seconde sans surcharger le processeur de l'ordinateur puisque c'est le GPU qui fait tout le travail.


##Bien sûr, il y a quelques contraintes et pré-requis

Pour que WebGL soit activé il y a trois conditions à réunir :

- posséder une carte graphique 3D compatible OpenGL ;
- des drivers – ou pilotes – à jour ou récents pour cette carte, eux aussi, compatibles OpenGL ;
- et un navigateur web de dernière génération qui soit le plus récent possible, car à chaque nouvelle version, les constructeurs de navigateur implémentent de plus en plus de spécifications de WebGL.

Pour vous faire une idée de l'étendue de la prise en charge par navigateur, consultez la [rubrique WebGL de *Can I Use*](http://caniuse.com/webgl).

Selon [WebGL Stats](http://webglstats.com) il y a potentiellement 64 % des utilisateurs qui ont WebGL activé. C'est un très bon début pour une spécification qui a moins de 2 ans, et cela permet d'ores et déjà d'envisager des mises en production à l'aide de cette technologie. Le monde du jeu vidéo ne s'y est d'ailleurs pas trompé !

![HexGL, jeu de course futuriste en HTML5](HexGL.jpg "<a href="http://hexgl.bkcore.com/">HexGL</a> est un portage de <a href="http://fr.wikipedia.org/wiki/WipEout_(série)">WipeOut</a> avec les technologies Web")


##Que faire si WebGL ne s'active pas ?

Un ou plusieurs pré-requis ne sont pas satisfaits ? Aucun souci : comme nous manipulons du JavaScript il est très facile de prévoir un fallback.  
Cette solution de remplacement peut être un message d'erreur ou comme dans le cas d'[EvE Online](http://www.eveonline.com/universe/spaceships/), que je trouve très bien fait, d'afficher une image qui montre le modèle de façon statique. Ainsi on reste accessible et si WebGL est activé on gagne en information et en interactivité.

![Vaisseau spatial dans le jeu EvE Online](EvE-Online_Spaceships.jpg "<a href="http://www.eveonline.com/universe/spaceships/">Vaisseau spatial dans le jeu EvE Online</a>")

À noter qu'Internet Explorer ne supporte toujours pas WebGL. Le seul moyen pour contourner le manque d'implémentation est d'installer le plugin [IEWebGL](http://iewebgl.com/)...


##Comment est constituée une image en 3 dimensions ?

WebGL s'appuyant directement sur le standard [OpenGL](http://www.opengl.org/), il en reprend la forme d'écriture du code, mais adaptée pour Javascript.  
Le but étant de définir tous les éléments composant une image en 3 dimensions.

Les éléments principaux sont :

- une scène ;
- des vertex (ou points) ;
- des arêtes ;
- des faces ;
- des matériaux ;
- des lumières ;
- et au moins une caméra virtuelle qui servira de point de vue pour le calcul du rendu de l'image.

Tous ces éléments sont définis mathématiquement selon un modèle vectoriel.   
Ils peuvent être mis en place, par exemple à l'aide d'un logiciel de modélisation 3D tel que [Blender](http://www.blender.org/), [3D Studio Max](http://www.autodesk.fr/3dsmax), [Maya](http://www.autodesk.fr/maya), [Lightwave 3D](https://www.lightwave3d.com/), [Modo](http://www.luxology.com/modo/), [Cinema 4D](http://www.maxon.net/fr/products/cinema-4d-studio.html), etc.

![Blander meshes de base](blander_meshes_de_base_fildefer.png "Blander meshes de base chez <a href="http://sebsauvage.net">sebsauvage.net</a>")

Les vertex ou points vont définir les sommets du contour des volumes modélisés que l'on souhaite représenter. C'est le matériel de base qui va permettre la génération des faces qui donneront du volume aux modèles.  
Plus les points seront nombreux plus le modèle sera précis. Par contre, les calculs de rendu seront également plus compliqués et plus longs.

Pour habiller le tout et donner une consistance qui soit la plus réelle possible, les modèles vont être « habillés » de [shaders](http://fr.wikipedia.org/wiki/Shader). Ainsi on va simuler le métal, la pierre, le verre, etc. Un langage particulier de définition des shaders existe également au sein de WebGL. Il s'agit de [GLSL](http://fr.wikipedia.org/wiki/GLSL) qui est entrain de s'imposer afin de définir des shaders au delà de `<canvas>` pour tous [les autres éléments HTML](http://www.w3.org/TR/filter-effects/).

Comme dans la réalité pour voir un objet, il faut qu'il soit éclairé et donc que la scène 3D comporte au moins une source lumineuse.   
Car pour l'instant elle n'existe que dans la mémoire de l'ordinateur !

![Rendu final avec l'application de shaders différents](HDRI_render.jpg)

C'est le processus de rasterization qui va interpoler l'image vectorielle en volume, dans notre cas, pour en faire une version 2D pixelisée.   
Ce calcul est effectué plusieurs dizaines de fois par seconde pour obtenir une animation fluide et agréable qui sera affichée dans `<canvas>` !

![Rasterization](rasterization.png)


##Qu'est ce que WebGL a sous le capot ?

Pour vous donner une idée de ses performances, voici quelques exemples... il y en a encore bien d'autres !

- [Metaballs](http://www.ro.me/tech/metaball-playground)
- [WebGL Water](http://madebyevan.com/webgl-water/)
- [Performance merging geometry](http://learningthreejs.com/data/performance-merging-geometry/)

##Et le code dans tout ça ?

Je ne rentrerai pas dans le détail du code pour cet article, car ce n'est pas le sujet. Si vous vous intéressez à l'écriture du code pour WebGL, je vous recommande l'excellent site [Learning WebGL](http://learningwebgl.com/) qui permet de s'initier à cette technologie. Il propose également [des leçons d'apprentissage](http://learningwebgl.com/blog/?page_id=1217).

Nous allons quand même voir un petit exemple pour comprendre le principe.

Je vous invite à aller consulter l'exemple indiqué dans le lien qui suit et qui a été réalisé par Jérome Etienne.  
Il présente pas à pas de façon commentée (en anglais) un exemple de code pour la bibliothèque Three.js afin de générer et d'animer un cube.

- Let's do a cube : [code commenté](http://learningthreejs.com/data/lets_do_a_cube/docs/lets_do_a_cube.html)
- Let's do a cube : [démonstration du résultat](http://learningthreejs.com/data/lets_do_a_cube/lets_do_a_cube.html)

![Let's do a cube](Lets_do_a_cube.jpg "<a href="http://learningthreejs.com/data/lets_do_a_cube/lets_do_a_cube.html">Let's do a cube</a>")


##S'aider de bibliothèques Javascript pour WebGL

Le code pour WebGL devenant rapidement complexe, long et fastidieux, des bibliothèques Javascript (sans cesses plus nombreuses) ont été conçues et mises en œuvre pour aider les programmeurs.  
Voici une liste non exhaustive de celles qui sont le plus couramment employées. Selon votre projet, l'une ou l'autre sera plus adaptée.

- [ThreeJS](http://mrdoob.github.com/three.js/)
- [PhiloGL](http://www.senchalabs.org/philogl/)
- [GLGE](http://www.glge.org/)
- [J3D](https://github.com/drojdjou/J3D)
- [SceneJS](http://scenejs.org/)
- [o3d](http://code.google.com/p/o3d/)
- [C3DL](http://www.c3dl.org/)

À noter que ThreeJS est une bibliothèque légère et très performante qui permet de générer un rendu WebGL dans les balises `<canvas>` et `<svg>`. Elle connait une des plus forte adhésion auprès des programmeurs.   
Attention toutefois, je vous déconseille de générer le rendu dans une balise `<svg>` car les performances ne sont pas au rendez-vous et il y a encore de sévères restrictions sur les shaders applicables.

Le site du Khronos group fournit [une liste répertoriant la plupart des frameworks pour WebGL](http://www.khronos.org/webgl/wiki/User_Contributions).


##WebGL en production ?

Aujourd'hui l'utilisation de WebGL dépasse la simple expérimentation technologique et de plus en plus de projets l'utilisent en production.

![Car Visualizer](Carvisualizer.jpg "<a href="http://carvisualizer.plus360degrees.com/threejs/">Car Visualizer 360 degrés</a>")

Voici quelques uns des domaines où l'on peut voir WebGL en action :


###Jeu vidéo

- [Lego – Mecabricks](http://www.mecabricks.com/) : Une façon sympathique, mais technique d'aborder le monde Lego. La prise en main demande un certain temps d'adaptation ;
- [HexGL](http://hexgl.bkcore.com/) : Vous pouvez directement jouer en ligne en deux clics. C'est encore en beta mais déjà très efficace ! L'esprit de WipeOut se retrouve bien dedans, et qui plus est, c'est un projet français !
- [Trigger Rally](http://triggerrally.com/) : Une course de rallye ludique où les effets du terrain sont reproduits grâce à un moteur physique. Je vous recommande vivement de l'essayer ;
- [Zombies vs Cow](http://yagiz.me/zombiesvscow/) : Petit jeu avec une ambiance BD fort sympathique ;
- [WebGL Pool](http://o3d.googlecode.com/svn/trunk/samples_webgl/o3d-webgl-samples/pool.html) : Un billard très bien fait où il ne manque que le son. Pour une démonstration, il est très abouti ;
- [Quake WebGL Demo](http://media.tojicode.com/q3bsp/) : Un petit coup de nostalgie avec cette reproduction d'un [FPS](http://fr.wikipedia.org/wiki/Jeu_de_tir_en_vue_subjective) mythique. Cela donne idée de l'avenir de WebGL dans le jeu vidéo…


###Visualisation de données

- [Universeries](http://cinema-series.orange.fr/evenement/universeries/) : Un parcours de decouvertes et de redécouvertes des séries américaines dans un environnement 3D original. Le concept vaut le détour ;
- [Cloud globe](http://workshop.chromeexperiments.com/cloudglobe/) : Visualiser dans le temps les grosses tempêtes qui ont parcouru la Terre. Ça a le mérite d'être très instructif en seul coup d'œil ;
- [Arms trade](http://workshop.chromeexperiments.com/projects/armsglobe/) : Très beau design pour représenter les flux d'armes entre les pays. L'utilisation de la 3D  apporte un plus saisisant très bien mis en œuvre ;
- [Real time color 3D histogram analysis](http://www.senchalabs.org/philogl/PhiloGL/examples/histogram/) : Très fort. Génération de l'histogramme des couleurs en volume à partir de la bande annonce d'un film. On a le choix entre 3 représentations et tout est interactif ;
- [World temperature changes from 1880 to 2011](http://www.senchalabs.org/philogl/PhiloGL/examples/temperatureAnomalies/) : Simple mais très pédagogique. Cette représentation dans le temps de l'évolution des températures sur la Terre parle d'elle même. La 3D donne ici une dimension pédagogique qui donne tout son sens.

![Représentation de la population mondiale](World_Population.jpg "<a href="http://workshop.chromeexperiments.com/globe/">Représentation de la population mondiale</a>")


###Cartographie

- [Google MapsGL](https://maps.google.fr/) : Il faut avoir WebGL d'activé pour que l'option soit proposée. Le gain se mesure au niveau de la fluidité ;
- [WebGL Earth](http://www.webglearth.com/) : Portage d'Open Street Maps vers une version en volume qui se présente comme une alternative à Google Earth. Le projet en est à ses débuts.


###Art – Design

- [Little Sun Sunlight Graffiti](http://lightgraffiti.littlesun.com/) : Des Graffitis lumineux collaboratifs qui s'animent ;
- [Ellie Goulding Lights](http://lights.elliegoulding.com/) : Une expérience interactive faite de couleurs, de lumière et de musique ;
- [Sintel Goes Boom](http://alteredqualia.com/three/examples/webgl_materials_video.html) : Une bande annonce est projetée sur les faces de cubes qui forment un mur qui s'anime. La vidéo est un peu difficile à suivre mais l'effet obtenu vaut le détour ;
- [Nucleal](http://nucleal.com/) : Un diaporama de photos se transforme en explosion de particules animées. Un spectacle à voir ;
- [Anaemia](http://litewerx.dk/anaemia/demo/demo.html?s=max) : La scène *demo* s'est bien entendu emparée de WebGL. Regardez, le détour vaut le coup d'oeil !


###Représentation de lieux – Tourisme

- [Château de Versailles – Chaos to perfection](http://www.chaostoperfection.com/) : Une immersion et une visite guidée des parties les plus remarquable du Château de Versailles. Une très belle réalisation qui nécessite Chrome pour être utilisée ;
- [Visite virtuelle 3D de la Cathédrale St Jean de Lyon](http://patapom.com/topics/WebGL/cathedral/intro.html) : Une visite virtuelle de ce très beau monument.


###Présentation de produits ou d'objets

- [Car visualizer](http://carvisualizer.plus360degrees.com/threejs/) : Choisissez votre prochaine voiture, sa couleur de carroserie, de jantes, etc. Vous pouvez zoomer et tourner autour de chaque modèle. Une très belle réalisation qui existait en Flash et montre que l'alternative ne fait plus aucun doute aujourd'hui ;
- [Pump](http://mrdoob.github.com/three.js/examples/webgl_loader_collada_keyframe.html) : Plus technique, une pompe se monte pièce par pièce sous vos yeux ;
- [Sketchfab](http://sketchfab.com/) : Un projet français ingénieux qui propose une galerie de modèles 3D pour être parcourus et partagés. Une très belle vitrine pour WebGL.

![Voiture en 3D depuis SketchFab](SketchFab.jpg "<a href="http://sketchfab.com/">Voiture en 3D depuis SketchFab</a>")


###Enseignement

- [Open Worm](http://browser.openworm.org/) : Un projet ambitieux qui s'appuie sur WebGL pour la visualisation de tous les organes d'un ver ;
- [Jellyfish demo](http://aleksandarrodic.com/p/jellyfish/) : La précision des modèles de cette démonstration permet d'imaginer des applications interactives pour découvrir des espèces animales ;
- [Planetoweb size comparison](http://planetoweb.net/app/planetView.html) : Un moyen intéressant de comprendre notre univers et de visualiser la taille des planètes qui composent notre système solaire ;
- [Microscopix](http://litewerx.dk/microscopix/) : Cette animation issue de la scène *demo* est, en dehors de sa beauté graphique, un modèle de précision dans la représentation et la simulation d'élèments microscopiques composants notre organisme.

###Représentation mathématique et scientifique

- [Fractal morphing](http://david.alloza.eu/WebGL/morphing.html) : Animation de fractales en temps réel ;
- [Google easteregg](https://www.google.fr/#hl=fr&sugexp=frgbld&gs_nf=1&cp=93&gs_id=i&xhr=t&q=1.2+(sqrt(1-(sqrt(x^2+y^2))^2)+++1+-+x^2-y^2)+*+(sin+(10+*+(x*3+y/5+7))+1/4)+from+-1.6+to+1.6&pf=p&output=search&sclient=psy-ab&oq=1.2+(sqrt(1-(sqrt(x^2+y^2))^2)+++1+-+x^2-y^2)+*+(sin+(10+*+(x*3+y/5+7))+1/4)+from+-1.6+to+1.6&aq=f&aqi=&aql=&gs_l=&pbx=1&fp=1&biw=1100&bih=596&bav=on.2,or.r_gc.r_pw.r_qf.&cad=b) : Google s'amuse à cacher des œufs de Pâques générés à l'aide de WebGL et d'une fonction... très complexe ;
- [The X Toolkit: WebGL™ for Scientific Visualization](http://www.goxtk.com/) : Un ensemble d'outils s'appuyant sur WebGL pour la visualisation scientifique du corps  humain.


###Clip vidéo interactif

- [RO.ME](http://www.ro.me/) : Un projet musical et graphique qui permet de vivre et d'interagir avec ce très beau clip vidéo. Le spectateur influe sur le déroulement du clip et peut parcourir le monde de la vidéo à la fin. Une expérience à faire !

![Scène du clip RO.ME](ROME.jpg "<a href="http://www.ro.me/">RO.ME</a>")


##Conclusion

Bien qu'elle soit encore jeune, WebGL est robuste et surtout pleine de promesses. C'est une technologie qui est très attendue car elle permet de s'affranchir du frein imposé par l'ajout de plugin. C'est également une API Javascript basée sur un standard éprouvé. Elle va donc communiquer directement avec le navigateur, ce qui est un atout de premier ordre pour son adoption.

La preuve de cette attente forte est l'implémentation rapide par les navigateurs. Le monde du jeu vidéo ne s'y est pas trompé non plus, car de nombreux projets l'utilisant sortent ou sont sur le point de sortir tel que [HexGL](http://hexgl.bkcore.com/) ou [Trigger Rally](http://triggerrally.com/).

Maintenant, c'est à vous d'inventer le futur qui va avec !


## Liens et ressources pour aller plus loin

- [Une autre introduction à WebGL par Opera](http://dev.opera.com/articles/view/an-introduction-to-webgl/) ;
- [Des ressources pour apprendre à coder WebGL](http://learningwebgl.com) ;
- [Learning Three.js](http://learningthreejs.com/) ;
- [Boilerplate Builder pour Three.js](http://jeromeetienne.github.com/threejsboilerplatebuilder/) ;
- [Three.js editor](http://mrdoob.github.com/three.js/editor/) ;
- [HTML editor](http://mrdoob.com/projects/htmleditor/) ;
- [Tutoriaux WebGL Fundamentals](http://www.html5rocks.com/en/tutorials/webgl/webgl_fundamentals/) ;
- [ThreeNodes.js](http://idflood.github.com/ThreeNodes.js/public/index.html).

