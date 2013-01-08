# Des cartes sur vos sites : quelques bonnes pratiques

Le numérique n'a pas remis en question la puissance des cartes comme support de représentation de l'information géographique ou géolocalisée. Au contraire, avec l'interactivité, il leur a apporté une dimension supplémentaire qui a encore accru leur intérêt et fait apparaître de nouveaux usages. Sur le Web, les cartes sont maintenant des éléments communs de l'expérience de navigation, rencontrées dans une multitude de contextes.

Les cartographes considèrent comme vertus cardinales la lisibilité et la pertinence de l'information portée par une carte, sans négliger son aspect esthétique. Des valeurs proches de celles du développement Web ! Pourtant, le plus souvent, la problématique des cartes sur le Web concerne assez peu la cartographie à proprement parler. La question de comment représenter l'information spatiale peut se poser, mais elle est en grande partie résolue par les outils utilisés et le suivi raisonné des conventions. Les choix du développeur Web sont bien plus liés à la place donnée aux cartes dans un projet, et aux implications en termes d'ergonomie.

Dans cette optique, cet article est une collecte de conseils, issus de retours d'expériences et de ma veille sur les pratiques en cours. Il ne prétend pas être exhaustif, mais traiter suffisamment de points concrets pour vous aider à proposer sur vos sites des cartes belles, utiles et bien intégrées.


## Quelles cartes et quels outils ?

Prenons les exemples suivants : 

* [le plan d'accès à une conférence](http://www.paris-web.fr/lieux/) ;
* [une carte de résultats électoraux](http://www.lemonde.fr/election-presidentielle-2012/infographie/2012/05/08/carte-les-333-circonscriptions-ou-m-hollande-est-arrive-en-tete_1698093_1471069.html) ;
* [la météo du jour](http://france.meteofrance.com/) ;
* [l'information de trafic routier en temps-réel](http://v-traffic.com) ;
* [un réseau social bien connu basé sur la géolocalisation](http://foursquare.com).

Autant de cartes et de situations qui diffèrent en termes d'__information représentée__, de __degré d'interactivité__ et de __dynamique du contenu__.

Bien placer son projet par rapport à ces trois axes permet de choisir le type d'outil le plus adapté au contexte. Les mots "cartographie Web" évoquent inévitablement les _"slippy maps"_ , le modèle de cartes interactives  introduit par Google Maps et reproduit par de nombreux outils (Bing Maps, Nokia Maps, de nombreux projets liés à OpenStreetMap, etc.). Mais il existe bien d'autres façons d'intégrer une carte à un site, comme :

* une image statique, dessinée par un cartographe ou un graphiste ;
* une image statique, mais générée à la volée via une API REST comme [Google Maps Static](https://developers.google.com/maps/documentation/staticmaps/) ;
* des outils vectoriels, comme Kartograph [Kartograph](http://kartograph.org), ou les outils de cartographie basiques inclus dans des _toolkits_ de visualisation de données, tels que [D3](https://github.com/mbostock/d3/wiki/Gallery) ou [Google Charts](https://google-developers.appspot.com/chart/interactive/docs/gallery/geochart) ;
* des globes 3D tels que [WebGL Globe](http://www.chromeexperiments.com/globe), qui sont aussi une forme de cartographie.

Cependant, par sa capacité à afficher rapidement le monde entier à de nombreuses échelles différentes, l'approche la plus polyvalente et la plus adaptée à de nombreux projets est sans conteste celle des cartes interactives à la Google Maps. Sa popularité et sa facilité de programmation font aussi qu'elle est souvent préférée aux approches plus ciblées citées ci-dessus, même dans des cas où le résultat est moins pertinent d'un point de vue cartographique.

## Personnalisez !

Rien de plus triste que ces mêmes cartes Google Maps qu'on rencontre partout sur le Web, avec leurs couleurs trop vues et leurs boutons par défaut ! Mais surtout, leur message est affaibli.

Toute carte possède un contexte, qui recouvre son usage, la nature des informations portées, son époque, etc. Sur le Web, on peut y ajouter tous les traits du site dans lequel elle s'intègre. L'apparence et le comportement de la carte se doivent de refléter ce contexte, et aider ainsi à faire passer l'information. De plus, comme tout le monde ou presque utilise le même outil, la simple différenciation est un enjeu.

![Un exemple d'utilisation de carte à ne pas suivre](bad_example.png)

Une utilisation non personnalisée de Google Maps pour de la visualisation de données. Le fond de carte par défaut n'est pas adapté au contenu et nuit à sa lisibilité (routes, toponymie, etc.). De nombreux élements sont superflus (Street View, la vue satellite, voire le déplacement et le zoom). (Source : [Rue89](http://www.rue89.com/rue89-politique/2012/10/09/carte-votre-prefet-t-il-ete-nomme-sous-hollande-ou-sous-sarkozy-236002))

* __Personnaliser l'apparence de la carte__. Si vous gérez vos propres fonds de carte ou si vous utilisez Google Maps (via les _[styled maps](http://gmaps-samples-v3.googlecode.com/svn/trunk/styledmaps/wizard/index.html)_), vous pouvez (presque) tout changer. Faites-le à bon escient, en masquant le superflu. Vous pouvez introduire de la personnalisation via les contrôles, les icônes des points d'intérêts, les pop-up d'information, etc. Ne vous contentez pas du défaut !

* __Désactiver les options inutiles__. Ne proposez pas d'options ou de composants superflus. Par exemple, avez-vous besoin d'activer Street View ou la vue d'images aériennes dans votre application ? Pour un site d'annonces immobilières, ce sont des options pertinentes, mais si ça n'a aucun intérêt pour vos utilisateurs, allez au plus simple.

* __Limiter les échelles et zones disponibles__. Adaptez-vous au contexte géographique de l'information que vous présentez. Limitez le spectre des zooms disponibles pour le resteindre à ceux qui sont réellement pertinents pour votre usage. Si votre solution technique le permet[^fn:limit-bounds], vous pouvez même limiter la région visualisable à une zone rectangulaire définie.

![Un bien meilleur exemple, avec le même outil (Google Maps)](good_example.png)

Une utilisation personnalisée de Google Maps, dans un cas similaire au précédent (visualisation de données sur un journal en ligne). Le fond de carte simplifé et la symbologie sont à la fois adaptés à la charte graphique du site et au contenu. Les éléments inutiles ne sont pas affichés. (Source : [Owni](http://owni.fr/2011/12/07/prison-carte-surpopulation-carcerale-france/))


## Navigation et accès à l'information 

Une carte est un __support de représentation__ pour l'information géographique, rarement une fin en soi. Elle peut aussi être un __outil de découverte de l'information__ à part entière, axé sur la nature spatiale du contenu, au même titre qu'un moteur de recherche thématique explorera d'autres aspects (ex : "restaurants japonais").

L'importance de ce rôle de navigation sera proportionnel à l'importance de la localisation de vos données pour l'utilisateur, mais __ne devrait pas occulter d'autres moyens plus classiques d'accès à l'information__, souvent plus efficaces. Par exemple, dans de nombreux scénarios, le caractère spatial du contenu sera mieux exploité par une recherche par adresse (ex : "restaurants japonais à Paris 13e"), la carte pouvant être utilisée en second lieu pour la découverte de contenu local supplémentaire.

De plus, si le paradigme de navigation des _slippy maps_ est depuis longtemps bien connu par la plupart des utilisateurs, il peut vite devenir lent, voire pénible, surtout si l'information est fortement éclatée dans l'espace (nombreux _drag & drop_ et zooms à effectuer). On gagnera donc à simplifier au maximum la manipulation de la carte :

* __Permettre la recherche par adresse__, via un champ texte. Les principales API cartographiques propriétaires fournissent des moteurs de [géocodage](http://fr.wikipedia.org/wiki/G%C3%A9ocodage) performants, prenant en compte les inévitables inexactitudes de saisie. Dans le cas de l'API Google Maps, il est même possible d'activer l'autocomplétion pour une saisie très simplifiée ressemblant à celle du portail Google Maps[^fn:gmaps-autocomplete].

* __Fournir des raccourcis directs__. Si les données géolocalisées que vous présentez sont limitées dans l'espace à certaines zones bien définies, ou si vous savez que la majorité de vos utilisateurs seront intéressés par certaines régions seulement, n'hésitez pas à afficher en dehors de la carte des liens directs vers ces zones d'intérêts, qui modifieront dynamiquement le _viewport_ de la carte. Ils peuvent prendre la forme de liens textuels, d'une carte miniature avec des zones réactives, d'une liste déroulante, etc.

* __Initialiser la carte en fonction de l'utilisateur__. C'est le moyen le plus radical de limiter les interactions de l'utilisateur avec la carte : "deviner" la région la plus intéressante pour lui. Ceci peut se faire en géolocalisant son IP au chargement de la page ou en utilisant l'API de géolocalisation HTML5 (qui demande une validation de sécurité de la part de l'utilisateur). Si vos visiteurs sont connectés à un compte, vous pouvez y enregistrer explicitement leur région d'intérêt. Même sans cela, vous pouvez stocker[^fn:view-storage] le triplet `{latitude;longitute;zoom}` à chaque déplacement de la carte, pour restaurer la dernière vue à la visite suivante.

Bien sûr, ces pratiques ne sont à utiliser que si réellement pertinentes dans votre contexte. Dans le doute, mieux vaut éviter les risques de la "sur-personnalisation", et présenter la même vue correctement choisie à tous les utilisateurs.

![Raccourcis directs sur le site V-Traffic.com](vtraffic_shortcuts.png "Raccourcis graphiques et textuels sur <a href="http://v-traffic.com/">V-Traffic.com</a>")


## Sur mobile

En lisant le point précédent, concernant la géolocalisation, vous avez probablement pensé à la situation sur un terminal mobile, où cette option peut s'avérer primordiale. Mais l'adaptation d'un site Web cartographique au contexte mobile ne s'arrête pas là, car elle doit prendre en compte toutes les spécificités de cet environnement :

* Géolocalisation (très) précise et évoluant dans le temps (mobile !) ;
* Ressources matérielles et réseau restreintes ;
* Petits écrans ;
* Interface tactile, intuitive pour la manipulation des cartes, mais globalement peu précise pour l'interaction avec des éléments graphiques ;
* Cohabitation avec des applications natives. C'est un acquis : tous les OS mobiles disposent d'une application cartographique embarquée, elle-même exploitable via une API dans le cadre d'applications natives.

Mauvaise nouvelle : si les API cartographiques Web modernes ont été conçues pour prendre en compte ces particularités[^fn:api-mobile-refactoring], l'expérience utilisateur qu'elles proposent reste encore en deça de ce qu'on obtient sur les applications natives. Nul doute que la situation va continuer à s'améliorer, mais pour l'instant la réactivité est à la traîne, et le support de certains navigateurs imparfait. Même dans les meilleurs cas, on se heurte très vite à des problèmes d'ergonomie : les petites résolutions rendent peu utilisable une _slippy map_ sur une page mobile, dès qu'elle n'occupe pas l'écran entier.

J'aime bien les principes du _responsive design_, mais ils me paraissent inadaptés dans le contexte de la cartographie. Mieux vaut finalement adopter une approche plus radicale, en développant une version réellement adaptée aux contraintes du mobile, plutôt que de tenter de reproduire l'expérience _desktop_.
  
* Si votre carte prend tout son sens dans un contexte local (ex : météo, recherche de commerces, etc.), __utilisez la géolocalisation__ comme vecteur principal d'accès à l'information. C'est une pratique commune et évidente sur mobile, qui ne surprendra pas les utilisateurs. Au contraire, ils vous en voudront si l'option est absente !
* Plus que jamais, simplifiez les cartes et leur manipulation au maximum. Si cela a du sens, __privilégiez des cartes statiques__, non interactives.
* Si, par son usage, votre site doit absolument reposer sur une carte interactive, optez pour un design qui lui laisse le maximum d'espace, quitte à vous inspirer du _layout_ commun à la plupart des applications natives (une carte en plein écran et des panneaux escamotables pour l'affichage d'informations). Adaptez aussi la taille des contrôles aux "gros doigts" des utilisateurs.
* __Exploitez l'application de cartographie native__, en lui déléguant l'affichage de certaines vues. Par exemple, des points d'intérêts, des itinéraires ou encore une vue Street View. Ainsi, vous profiterez de la puissance de l'application et de la familiarité de l'utilisateur avec celle-ci, tout en vous concentrant sur la valeur ajoutée de votre site (qui n'est probablement pas la cartographie). Ce passage du Web au natif se fait facilement par des liens HTTP de format spécifique[^fn:mobile-maps-uri-scheme], que la plateforme saura reconnaître pour aiguiller l'utilisateur vers l'application dédiée.


## Quelques mots d'accessibilité

On s'en doute, de par leur mode d'interaction particulier, les cartes interactives peuvent vite devenir des cauchemars en termes d'accessibilité. Le sujet est complexe et mériterait d'être traité à part. Globalement, un certain nombre de conseils précédents ont un impact positif, mais des efforts plus ciblés peuvent se concentrer sur deux axes :

1. __La manipulation de la carte__, par exemple en fournissant des contrôles personnalisés (plus grands, avec un meilleur _feedback_ visuel, et facilement activables au clavier) et en activant le déplacement de la carte avec les touches directionnelles.
2. __La lisibilité du contenu__. Graphique d'une part, en simplifiant la cartographie et en utilisant au mieux les couleurs et l'iconographie. Textuel d'autre part, en fournissant systématiquement à chaque contenu significatif (adresse et description d'un point d'intérêt, itinéraire, etc.) une alternative lisible par les lecteurs d'écrans, non "captive" de la carte, donc extérieure à celle-ci. 

Les ressources sur ce sujet sont assez rares, mais si vous souhaitez aller plus loin, vous pouvez commencer par cette [étude de John Ramon](http://www.johanramon.fr/google-maps-accessibilite).


## En résumé 

La cartographie Web est un sujet vaste et passionnant, qui comporte de multiples niveaux. En axant cet article principalement sur l'ergonomie, j'ai dû laisser de côté bon nombre de facettes plus spécifiques. Par exemple, aborder des bonnes pratiques de performance ou des stratégies d'affichage de gros volumes d'information. Mais les ressources techniques sont faciles à découvrir par soi-même, je suis sûr que vous vous en sortirez très bien !

Il était à mon sens plus intéressant de réfléchir aux implications de l'emploi d'un outil aussi puissant et complexe qu'une carte interactive au sein d'un site, pour ne pas se contenter d'être un simple utilisateur d'API. Sur ce principe, n'hésitez pas à remettre en question mes conseils, car comme toute "bonne pratique", leur pertinence a ses limites.



[^fn:limit-bounds]: Assez étrangement, les API propriétaires comme Google Maps et Bing Maps n'exposent pas d'option pour réaliser facilement ce comportement. Il reste possible de l'implémenter soi-même, en vérifiant à chaque déplacement si la vue est bien dans la zone voulue, et en la corrigeant au besoin. Sur d'autres API, comme Leaflet par exemple, c'est une option native.
[^fn:gmaps-autocomplete]: Cette fonction requiert l'activation explicite de l'extension `places` au chargement de l'API Maps.
[^fn:view-storage]: par exemple en cookies ou en DOM storage.
[^fn:api-mobile-refactoring]: l'adaptation aux plateformes mobiles était l'une des priorités de la refonte de l'API Google Maps lors du passage à la version 3, en 2009. Du côté des API libres, c'est la principale raison d'être de Leaflet, et de la grande modernisation entreprise dernièrement par OpenLayers.
[^fn:mobile-maps-uri-scheme]: Schémas d'URLs cartographiques, pour [iOS](http://developer.apple.com/library/ios/#featuredarticles/iPhoneURLScheme_Reference/Articles/MapLinks.html) et [Android](http://developer.android.com/guide/appendix/g-app-intents.html). Apparemment, une fonction semblable mais non documentée existe aussi sous [Windows Phone](http://stackoverflow.com/questions/4598189/url-conventions-for-maps-on-windows-phone-7).

