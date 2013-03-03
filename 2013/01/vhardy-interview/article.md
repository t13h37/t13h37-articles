#Interview : Vincent Hardy

## Peux-tu te présenter en quelques lignes ? Qui es-tu, que fais-tu?

Je travaille chez Adobe depuis Avril 2011 et je suis passionné par le Web, le graphisme, l'animation et la qualité logicielle. Chez Adobe, je suis le directeur du développement du groupe « [*Web Platform*](http://html.adobe.com) ». C'est un groupe où nous concentrons nos efforts *open source* sur [WebKit](http://www.webkit.org) et [Cordova](http://cordova.apache.org) (la base *open source* de PhoneGap). Nous participons aussi activement à la standardisation des formats Web tels que HTML, CSS et SVG. Enfin, nous nous efforçons de créer des contenus basés sur les nouvelles fonctionnalités que nous apportons aux standards W3C afin de valider leur mise en oeuvre, et de donner du *feedback* aux équipes de standardisation et de développement *open source*. Nous créons également des exemples que nous pouvons partager avec la communauté. Par exemple, « [The Quest for the Graphical Web](http://thegraphicalweb.com) » a été développé dans cet esprit. Notre groupe s'attache aussi à la qualité et l'interopérabilité des formats Web avec l'initiative « [Test The Web Forward](http://testthewebforward.org) » que nous avons démarrée cette année et que nous menons avec plusieurs partenaires.


## Tu as une longue histoire professionnelle avec le format SVG, et Adobe est actuellement très actif dans le processus de standardisation de nouvelles fonctionnalités CSS. Avec l'arrivée prochaine de la norme SVG2 et de ces nouveaux modules CSS, comment vois-tu la convergence actuelle des standards HTML, CSS et SVG et quel sont ces nouveaux modules CSS exactement ?

Je pense que SVG s'impose de plus en plus pour ajouter  du contenu graphique à HTML. En plus des `<div>`, `<p>` et autres `<h1>`, nous avons les balises `<rect>`, `<circle>` et `<path>`, par exemple, et l'intégration est de plus en plus au point. SVG et HTML partagent une même base syntaxique et peuvent être mis en forme via les feuilles de styles CSS grâce aux mêmes mécanismes.

Historiquement, les formats ont été séparés et développés par des groupes différents. Mais il y a eu une grande influence entre les formats. Par exemple, les dégradés, les effets d'ombrage, la typographie professionnelle, le contrôle des polices de caractères ont tous émergé d'abord dans SVG avant d'être disponibles plus largement dans HTML grâce à CSS qui les a intégrés. Cette intégration et cette synergie se sont accélérées à l'aide d'une meilleure coordination des efforts, grâce à une *task-force* appelée "FX" (pour *effects*) qui réunit les groupes de travail CSS et SVG du W3C. Ensemble, ces groupes unifient des fonctionnalités graphiques essentielles telles que [les transformations 2D et 3D](http://www.w3.org/TR/css3-transforms/) qui permettent de manipuler les éléments dans l'espace (par exemple pour faire des rotations) ou [les effets de filtres](https://dvcs.w3.org/hg/FXTF/raw-file/tip/filters/index.html) qui permettent d'altérer le rendu des éléments (par exemple en appliquant un effet de flou ou d'ombrage). D'autres modules tels que [les masques CSS](http://dvcs.w3.org/hg/FXTF/raw-file/tip/masking/index.html) ou [le module CSS de composition et fusion](https://dvcs.w3.org/hg/FXTF/rawfile/tip/compositing/index.html) sont dans la lignée d'efforts de coordination et d'amélioration des fonctionnalités graphiques de la plate-forme Web qui s'appliquent à HTML et à SVG, par le biais de CSS.


## Et sinon, en vrai, on pourra les utiliser quand ?

Cela dépend des fonctionnalités ! Par exemple, les effets de filtres sont maintenant disponibles, pour les plus simples, dans Chrome et Safari. Les effets un peu plus sophistiqués, basés sur les définitions de filtres SVG, devraient arriver dans les navigateurs Web dans les 12 mois qui viennent, du moins pour ceux basés sur WebKit et pour Gecko.

L'adoption des nouveaux modules est difficile à prédire de façon précise. Par exemple, nous contribuons à l'implémentation de [CSS Regions](http://dev.w3.org/csswg/css3-regions/) et [CSS Exclusions](http://dev.w3.org/csswg/css3-exclusions/) dans WebKit. Mais c'est à Google ou Apple qu'il revient d'autoriser l'utilisation de ces nouvelles fonctionnalités dans leurs navigateurs. Microsoft a déjà mis ces fonctionnalités à disposition dans Internet Explorer 10, et j'espère donc que les autres navigateurs suivront bientôt.

Pour qu'une fonctionnalités nouvelle devienne disponible, il faut en général une bonne spécification, une suite de tests et plusieurs implémentations. Cela demande la coordination de beaucoup d'entités différentes (organisme de standardisation, différentes sociétés) et cela explique que ça prenne parfois plus de temps qu'on le souhaiterait en tant que développeurs web !


## Ton équipe travaille activement sur de nouveaux outils de développement très orientés sur les standards du Web (Edge, Inspect). Cependant, ceux-ci restent encore très orientés vers Chrome. Comment ces outils vont-il s'ouvrir à d'autres navigateurs afin de pouvoir répondre aux besoins d'industrialisation des développeurs Web ?

Adobe supporte l'*Open Web* et bien que nous utilisions WebKit dans nos produits (WebKit est le moteur de rendu des surfaces de composition de nombre de nos outils), le code généré par nos outils n'est pas spécifique à un navigateur particulier. Par exemple, [*Edge Code*](http://html.adobe.com/edge/code/) ou [*Edge Animate*](http://html.adobe.com/edge/animate/) fonctionnent pour tous les navigateurs.

[*Edge Inspect*](http://html.adobe.com/edge/inspect/) dépend effectivement de WebKit pour une raison technique simple : il n'y a actuellement pas de standard pour brancher des outils de *debug* sur tous les navigateurs. Cette possibilité qui existe dans d'autres environnements (par exemple en Java) n'existe pas encore pour les navigateurs Web. Nous avons donc choisi de travailler avec le navigateur le plus demandé par nos utilisateurs, en particulier dans le monde du mobile. Nous avons également essayé de travailler avec d'autres navigateurs web mais sans succès pour l'instant. J'espère que cette situation évoluera pour permettre un meilleur outillage des navigateurs Web.


## *Test The Web Forward* est un évènement qui a été organisé dans plusieurs villes en 2012 par Adobe. Peux-tu nous dire de quoi il s'agit et quelles suites vont y être données ?

Beaucoup de développeurs sont passionnés par la plateforme web qu'ils veulent supporter. [Le mouvement du bonnet bleu](http://www.webstandards.org/2009/11/24/be-a-true-blue-beanie-supporter-of-web-standards/) était un symbole que nombre de développeurs ont adopté pour montrer leur support aux standards du Web. Suite à ce mouvement, l'idée de faire plus que montrer son support et de participer activement à l'amélioration du Web est née avec « [Move the Web Forward](http://movethewebforward.org) » que Paul Irish, Divya Manian et d'autres ont initié. 

« *[Test the Web Forward](http://testthewebforward.org)* » est dans cette lignée : aidons ceux qui veulent améliorer le Web à participer à un effort qui a un impact direct et important – les suites de tests. Durant les événements *Test The Web Forward*, les développeurs web peuvent apprendre à écrire des tests qui s'intègrent dans les suites officielles des spécifications et à créer un rapport de bug qui aura le plus de chance d'être pris en compte par les éditeurs de navigateurs. Des experts participent, et notre désir est de construire une communauté et une culture autour des tests pour le Web.

Les trois premiers événements nous ont permis d'apprendre quel intérêt existe pour cette approche, de recevoir des suggestions et de concevoir une suite naturelle. Nous sommes en pleine définition de la suite du mouvement dont nous discutons avec nos partenaires au W3C, mais il y aura de nouveaux événements et probablement une infrastructure pour soutenir un effort continu entre des rencontres majeures.

J'espère que ces quelques lignes encourageront vos lecteurs à s'impliquer dans cette communauté émergente !


## Merci pour ces éclaircissements. Un dernier mot pour la route ?

Je pense que nous sommes à un tournant pour le Web et HTML5. La plateforme est en pleine maturation et les possibilités sont de plus en plus nombreuses. Il est très important pour la communauté de s'impliquer et de participer à l'amélioration du Web. Contrairement aux autres plateformes, la plateforme Web n'est la propriété de personne en particulier et donc la responsabilité de chacun d'une certaine façon. La documentation en particulier est importante, et j'encourage tous les passionnés à contribuer autant qu'ils le peuvent à l'effort « [*Web Platform Docs*](http://www.webplatform.org) », le "Wikipedia des formats Web". Je pense que c'est un effort sans précèdent pour les formats techniques, et très important pour les formats Web, qui capture l'information que notre génération produit et que les générations à venir produiront !

