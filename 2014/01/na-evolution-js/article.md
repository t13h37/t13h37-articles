# Dix ans de pratique Javascript à Paris

Je m’appelle Noëlie et je développe du Javascript depuis 2002. J’ai travaillé sur des sites à fort trafic, sur des outils de back-office et des applications mobile ou tablette. L’intitulé de mon poste est très difficile à définir car, bien que je fasse du développement Javascript, je me préoccupe avant tout du rendu final dans le navigateur. Ce métier est appelé développeur front-end ou front-office.   
La conception en règle générale est pour moi une vraie passion. Elle s’étend également au domaine des objets physiques : je partage toutes mes créations sur [mon blog](http://no-way.fr).

J’aimerais vous raconter l’impact qu’ont eues les évolutions de Javascript sur mon métier de développeur à Paris. Cet article n’est pas un article technique, mais plutôt un retour d’expérience sur 10 ans de pratique du métier dans différents types d’entreprises.

Le Javascript est un langage qui permet de toucher à beaucoup de domaines : du fonctionnement d’une interface à la manipulation de données, les possibilités sont multiples ! Or un certain mystère l’entoure : est-ce un langage de programmation ? Un langage front-end ou bien back-end ?

Je vais vous décrire les missions que l’on me demandait de remplir en tant « qu’intégrateur faisant du Javascript », mais surtout les tâches techniques qui les composaient : des tâches étranges et mystérieuses dignes de la magie de Javascript. Mais avant cela, j’aimerais faire un petit aparté sur les terminologies dont je vais vous parler. La création de sites web, d’outils ou d’applications nécessite la conjugaison de plusieurs métiers dont les natures sont assez différentes. Je me suis permis de faire quelques raccourcis par souci de vulgarisation.

Intégrateur
: Il travaille avec HTML et CSS mais pas avec Javascript. HTML est un langage de balisage, CSS un langage de mise en forme : ce ne sont pas des langages de programmation. Ils permettent d’organiser et de structurer des données, alors que la programmation permet de créer des algorithmes pour les manipuler, confronter, tester. Toutes ces données forment un document qui sera lu et restitué visuellement dans un navigateur web.

Développeur front-end ou front-office
: Il fait à la fois de l’intégration et du développement Javascript, et comme pour l’intégrateur son travail est centré sur le navigateur. Le Javascript permet de manipuler des balises HTML et de leur appliquer des logiques et des comportements autres que ceux prévus par le navigateur. Le Javascript peut générer des balises HTML et ajouter des mises en forme CSS, c’est pourquoi le développeur front-end doit comprendre le travail d’intégration pour exercer son métier correctement.

Développeur back-end
: Il développe des programmes pour manipuler, stocker et restituer des données. Traditionnellement, les langages utilisés sont interprétés côté serveur et permettent de générer des documents HTML qui seront interprétés par le navigateur.   
Son travail est tourné vers la restitution et le stockage des données dans la page web [^1]


## Du DHTML de fin 2003 à début 2005

Suite à un DUT Services et Réseaux de Communication (SRC), je partis pour Paris où je trouvai un poste dans une grande agence parisienne : c’est à ce moment que j’appris à connaître ce langage appelé Javascript.

On me demanda très vite de faire du DHTML pour un site de e-commerce :   
« Tu vois ces onglets ? On voudrait que lorsque l’on passe la souris au-dessus, le menu s’affiche puis qu'il disparaisse lorsqu’elle ne l’est plus. »   
« Ok » leur répondis-je tout en pensant : « Comment diable faire ça ? ».

Par chance, un collègue qui s’était déjà frotté à ce type d’exercice m’aida dans ma tâche et le peu de Java et d’ActionScript que j’avais appris à l’école m’aida pour toutes les notions d'algorithmie. Le menu fut laborieusement fini en une semaine, avec près de 1000 lignes de code. 

Ce terme assez étrange de DHTML correspondait en fait à des manipulations Javascript sur le code HTML, le « D » signifiant « Dynamic ». Le DOM HTML n’existant pas encore et les outils de debug côté navigateur non plus. La manipulation des balises était donc beaucoup plus ardue qu’elle ne l’est de nos jours car les navigateurs majoritaires à l'époque étaient IE6, IE5 ou Netscape4.

Suite à cette expérience très formatrice, je devins « l’experte » Javascript de l’agence : ce n’était pas très dur de le devenir vu que personne d’autre ne voulait se casser les dents dessus. S’en suivirent diverses demandes du même ordre, pendant près d’un an et demi. Une passion <strike>un peu contrainte</strike> était née.


## La découverte de standards ou la naissance du 2.0, dès 2005

En 2005, je changeai d’agence pour en rejoindre une autre. À cette époque arrivèrent toute une liste de nouvelles technologies qui révolutionnèrent notre façon de travailler : [XHTML](http://en.wikipedia.org/wiki/HTML#XHTML_versions), [CSS 2.1](http://en.wikipedia.org/wiki/Cascading_Style_Sheets#CSS_2.1) et DOM HTML ou [DOM2](http://fr.wikipedia.org/wiki/Document_Object_Model#DOM_2). C’est à ce moment là qu’un nouveau navigateur arriva également sur le marché : [Firefox](http://fr.wikipedia.org/wiki/%C3%89volution_de_l'usage_des_navigateurs_web), avec son fameux plugin [Firebug](http://en.wikipedia.org/wiki/Firebug_(software)).   
Mozilla commença également à publier sur son site une [documentation](https://developer.mozilla.org/fr/) sur Javascript et DOM. Ce fut pour moi une oasis en plein désert !

Ces nouveautés ont littéralement révolutionné mon quotidien : je pouvais désormais visualiser un fichier Javascript dans le navigateur et lire des messages d’erreurs explicites.   
Suite à ces avancées se développèrent des bibliothèques autour de Javascript : [JQuery](http://fr.wikipedia.org/wiki/JQuery) qui reste le plus connu, mais aussi [Prototype](http://en.wikipedia.org/wiki/Prototype_JavaScript_Framework) ou [Mootools](http://en.wikipedia.org/wiki/Mootools#History). Notre boîte à outils avait littéralement explosé, la demande aussi : [Ajax](http://fr.wikipedia.org/wiki/XMLHttpRequest), popins et carrousels devenaient des éléments d’interface incontournables.

Ainsi, le Javascript sortit peu à peu de l’ombre. Malgré tout, pour un seul et même script à produire demeurait une séparation des tâches stricte par métier : on considérait que certains développements concernaient les données et d’autres des composants graphiques. Ces deux facettes étant gérés par deux métiers différents, le travail était donc séparé : une partie pour le développeur back-end, l’autre pour le développeur front-end. 

Par exemple le cas des popins où l’affichage de la fenêtre devait être fait côté front-end, et la manipulation des données côté back-end. Or, la réalité du code était toute autre : que le développement se fasse sur des données ou du DOM, une seule solution devait être choisie, elle-même développée dans un seul langage : Javascript.   
Cette manière d’appréhender ce langage ne pouvait créer que des frustrations des deux côtés où chacun s’estimait plus légitime que l’autre.

Après quelques années, je gagnai le titre de développeur front-end : un titre de poste plus généraliste qui sous-entendait que le travail côté navigateur n’incluait pas que de l’intégration mais aussi de la programmation. Ce nouvel intitulé permettait de clarifier le métier autant pour les intégrateurs que pour les métiers attenants qui ne comprenaient pas bien l’intégration et les implications du Javascript. 


## 2009 : l’explosion de HTML5

### Intitulé métier `Undefined`

À compter de 2009, j’ai très souvent changé d’employeur, restant parfois à peine 6 mois à un poste. Le Javascript étant devenu le langage à la mode, la demande en recrutement explosa. De mon côté, je trouvais que les termes « développeur front-end » ou « intégrateur » définissaient mal mon métier et que l’intitulé « développeur Javascript » convenait davantage à mon travail.   
Je recherchais alors une entreprise qui me permettrait de faire du développement Javascript à plein temps et d’être reconnue comme un développeur en tant que tel.

Ce fut le cas entre 2007 et 2009, où j’intégrai l’équipe web d’un célèbre site de blogs français. Je pris mon poste dans une équipe de développement PHP et non dans l’équipe d’intégration, où l’on me permit de travailler sur des sujets plus complexes que ceux sur lequels j'avais travaillé jusqu’à présent. Pour ce site, pas de JQuery ! Les frameworks de manipulation du DOM étaient jugés trop lourds et donc pénalisants pour le chargement des pages. Les performances du site étaient plus importantes que les quelques effets visuels Javascript que le navigateur devait charger, interpréter et exécuter. Je dus alors travailler sur un framework « maison » de composants graphiques essentiels à notre besoin : carrousels, popins, éléments de menu, etc.

J’en avais fini avec les débats stériles : « vrais » ou « faux » développeurs. ll y avait des sujets et des personnes pour s’en occuper. Chacun prenait les sujets qu’il jugeait pouvoir gérer et ce n’était pas plus compliqué que ça.   
Suite à cette expérience professionnelle, ma vision fut complètement métamorphosée. Il m’était alors difficile de retourner en agence pour faire du Javascript « graphique ».

### Flash, la fin d’un monde

Entre temps, avec l’explosion du mobile la demande en Flash chuta. Le Javascript, ou plutôt le HTML5, devint l’alternative à toutes les demandes d’animations ou d’interfaces graphiques complexes.

En 2010, apparut également [GitHub](http://github.com) qui permit l’émergence de nombreux frameworks Javascript traitant de problématiques plus complexes non traitées par JQuery. La gestion d’environnement [MVC](http://fr.wikipedia.org/wiki/Mod%C3%A8le-vue-contr%C3%B4leur) est l'un des meilleurs exemples. La multitude de micro-frameworks apparurent également sur d’autres sites web comme [microJS](http://microjs.com/) en 2011, ou [JSDB](http://www.jsdb.io/?sort=trending) en 2012.

Cependant, même si les années passaient et que les outils évoluaient, le Web français restait divisé sur Javascript : d’un côté les problématiques liées au développement de la donnée, de l’autre la gestion d’interface faisant davantage appel à des connaissances d’intégration et donc de HTML et de CSS.

### Comment faire entrer un rond dans un carré

En 2011 j'intégrais alors une agence web qui semblait très intéressée par mon profil « mixte ». Oubliées les anciennes querelles, le monde avait changé. Pourquoi pas les agences ?
On me demanda très vite des effets « wahou » que l’on ne faisait plus via Flash mais en HTML5, à savoir : de l’animation, de la vidéo ou des mises en pages très graphiques. Dans un autre bureau, l’équipe back-end utilisait quant à elle Javascript pour créer des sites de toutes pièces via une technologie appelée [ExtJS](http://www.sencha.com/products/extjs/), qui fournissait toute une suite de composants d’interface. L’idée était que ce framework permettrait de se passer de connaissances en front-end.

Pourtant on me demanda de repasser sur ce type de projets pour rajouter des couleurs, changer la taille des textes ou bien changer les mises en pages. Malheureusement, des erreurs de conception rendaient l’outil extrêmement lourd à charger pour des raisons facilement identifiables : deux à trois fois trop de code HTML, des balises HTML cassées ou encore beaucoup trop de styles CSS qui s’annulaient eux-mêmes. Des erreurs qui auraient pu être évitées si les développeurs avaient eu des connaissances en HTML et CSS. 

Le bilan de cette expérience ? Trois ans s’étaient écoulés depuis mon dernier passage en agence, et si de multiples solutions techniques étaient sorties entre-temps, les mentalités n’avaient pas évolué avec : remplacer les compétences front-end par des outils, oui mais pour quel résultat ?   
Le développeur front-end devrait-t-il à chaque fois sauver le projet au dernier moment ?


## Développeur Mobile : vers l’apaisement

Depuis 2011, je travaille pour un grand quotidien web. J’évolue dans une petite équipe qui travaille sur le site web mais aussi sur des outils web internes et des applications mobile (ou tablette), qu’elles soient en HTML5 ou natives.   
La taille restreinte de l’équipe fait que chacun peut travailler sur des sujets variés, chose impossible dans les grosses agences. Dans cette équipe, il n’y a pas de séparation « back-end versus front-end » : nous sommes six développeurs travaillant ensemble et qui se répartissent les compétences suivantes : PHP, Python, Javascript et web design.   
Il m’est arrivé de travailler seule ou en équipe de deux ou trois ; le choix se faisait en fonction des compétences de chacun et de la complexité du projet. J’ai travaillé sur de nombreux projets qui m’auraient été d’office refusés en agence car jugés hors périmètre métier, et j’ai pourtant été capable de les gérer seule.   
Notre manager fait en sorte que chacun puisse travailler et évoluer dans son domaine d’expertise, c’est ainsi que les conflits quasi systématiques « métiers versus compétences » ont cessé.   
Cette liberté au quotidien m’a permis d’être performante en front-end, de repousser mes connaissances en Javascript tout en travaillant en harmonie avec mes collègues. J’ai pu ainsi constater qu’il était possible d’être développeur Javascript front-end et de travailler avec un développeur back-end sans lui retirer le pain de la bouche : je me suis enfin rendue compte que le problème n’était pas dans le langage mais dans la compréhension des métiers. J’ai également pu développer en Python ou en PHP, tandis que mes collègues l’ont fait en Javascript.


## Front-end, du développement et de la mise en forme

J’ai souvent eu le sentiment d’être incomprise et mal insérée dans les chaînes de production de sites web à cause de mes connaissances en intégration qui étaient perçues comme un handicap par rapport aux connaissances en développement back-end. Je n’entrais pas dans les cases métier auxquelles je voulais me conformer pour mieux m’intégrer. J’ai mis du temps à me rendre compte que cela ne résoudrait en rien une situation qui est, qu’on le veuille ou non, complexe.

Depuis que le Javascript a le vent en poupe, les protagonistes sont de plus en plus jeunes et enthousiastes. Lorsque je discute de ces conflits séparatistes avec des développeurs back-end qui n’ont pas connu ces années pionnières, ils ont toujours du mal à me croire. Cependant, il ne faut pas oublier l’origine de ce conflit : développer et manipuler du DOM côté client et non pas côté serveur. Le Javascript n’est pas comme un langage serveur banal : il faut comprendre à la fois le DOM, le HTML et le CSS pour pouvoir le manipuler efficacement.

Le Javascript est un langage inclassable et sauvage et le restera sûrement. C’est pour cette raison qu’il faut l’aborder avec l’esprit ouvert, en dehors des visions traditionnelles du développement logiciel. Javascript permet de faire à la fois du front-end et du back-end, et c’est pour cette raison qu’il faut des profils mixtes qui permettent de gérer ces deux aspects. Chaque développeur ne peut développer les deux aspects de façon parfaite, mais ces connaissances sont indispensables pour produire du code robuste.

De mon côté, je continuerai à coder des applications en Javascript, à faire des sites web ou à développer des outils. J’essaie d’apprendre des langages interprétés côté serveur pour parfaire mes connaissances et en parallèle je continue à me tenir au courant des avancées HTML et CSS.

Garder l’esprit ouvert est la meilleure façon de bien vivre son métier et d’évoluer avec. J’espère que les entreprises qui produisent du web le comprendront, car c’est autant dans leur intérêt que dans celui de leur employés : travailler les uns avec les autres est plus bénéfique <strike>productif</strike> que les uns contre les autres.

[^1]: J’ai déjà rencontré des développeurs back-end se définissant comme front-end parce qu’ils faisaient du développement web. Or, dans le milieu du développement, un site web est appelé “Front » en opposition au “Back » qui désigne l’outil d'administration de ce site. Le problème que pose cette dénomination métier, dans ce cas précis, c’est qu’elle suggère que les développeurs front-end et back-end manipulent tous les deux des données. La gestion de l’interface, soit l’intégration des données, et la manipulation du DOM en Javascript, sont complètement exclues de cette logique. Or ces métiers existent bel et bien : voilà pourquoi je considère cette vision appellation métier erronée.
