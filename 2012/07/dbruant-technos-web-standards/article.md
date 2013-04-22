# Les technologies web et leurs standards

Demandez à presque n'importe quel développeur web français qui régit les technologies web et il/elle vous répondra sûrement « le W3C ». Le W3C, il est vrai, écrit les standards. Pourtant, le W3C n'écrit pas les standards de toutes les technologies web (ECMAScript et WebGL ne sont pas standardisés au sein du W3C, par exemple).  
Aussi, le paysage des technologies web s'étend bien au-delà des standards. Cet article a pour but de décrire ce paysage, ses différents acteurs et leurs interactions. J'étudierai notamment le cas des préfixes webkit qui ont fait beaucoup de bruits il y a quelques mois.

## Les acteurs

Voici une liste exhaustive des acteurs du web par « catégorie » ainsi que les motivations de chacun de ces acteurs :

- **Les Développeurs web** (identifiés en tant que « *authors* » dans les standards web) :
	- Ils veulent créer des sites ou applications web qui marchent pour le plus grand nombre ;
	- Ils ont des contraintes de temps et de budget ;
	- Ce sont des êtres humains.
- **Les Navigateurs** (identifiés en tant que « *user agents* » ou « *implementors* » dans les standards web) :
	- Ils veulent permettre aux développeurs de créer les sites web qu'ils veulent ;
	- Ils ne veulent pas perdre de parts de marché en terme de nombre d'utilisateurs (**le point le plus important de cet article !**) et s'ils le peuvent, ils grignoteront la part de marché des autres navigateurs ;
	- Ils sont fabriqués par des êtres humains.
- **Les organismes de standardisation** :
	- Ils coordonnent la rédaction des spécifications qui représentent une forme de contrat moral entre les développeurs web et les fabricants de navigateurs : les spécifications sont censées décrire les fonctionnalités qui existent dans les moindres détails ;
	- Des êtres humains écrivent les spécifications.

## Le scénario idéal qui n'existe que dans nos rêves

Quand on parle de technologies, on aimerait tous que le fonctionnement soit le suivant :

1. Une spécification parfaite est rédigée ;
2. Des navigateurs implémentent parfaitement la spécification (parfaite, je le rappelle) ;
3. Les développeurs peuvent développer des sites en supposant que tous les navigateurs suivent la même spécification à la lettre...

## Quand la réalité nous rattrape

### « La perfection est atteinte... »

Commençons en douceur la critique du scénario idéal en disant que les technologies en question sont tellement complexes et couvrent tellement de cas d'utilisation que rédiger une spécification parfaite n'est pas possible. Il faut commencer à l'implémenter pour se rendre compte des cas auxquels on n'avait pas pensé.  
De par sa complexité, le processus de standardisation des technologies webs (langages, API) ne peut pas être fait strictement avant l'implémentation, mais au mieux pendant la phase d'implémentation. On verra qu'elle a souvent lieu après.

### The root of all evil

On a très vite compris que le web était une plateforme à fort potentiel, notamment pour le e-commerce. Il fallait des sites de meilleure qualité, plus performants, plus brillants que celui du voisin, des sites à l'expérience utilisateur plus agréable, etc.  
Il a fallu très vite des technologies qui permettent l'émergence de sites plus interactifs du côté des navigateurs.  
Qu'on le veuille ou non, c'est cette raison qui est la cause de toutes les conséquences que je vais détailler. C'est une raison économique, humaine, sociale, mais sûrement pas une raison technique.

En effet, pour un navigateur, le risque de ne pas innover est de voir les développeurs se mettre à créer de meilleurs sites seulement à destination des navigateurs qui implémentent les nouvelles technologies. Ces meilleurs sites inciteraient les utilisateurs à changer de navigateurs pour avoir la meilleure expérience possible (on se souvient tous des bannières « ce site a été conçu pour Internet Explorer 6 »).

Ainsi, les navigateurs, dont la principale préoccupation tournait (et tourne encore) autour de leur part de marché, ne pouvaient pas se permettre d'attendre l'émergence d'une spécification parfaite. Non. Il fallait innover (comprendre : avancer sans spécifications), parce que si un navigateur n'innovait pas, un autre innoverait à sa place.

Vu qu'il n'y avait pas de spécifications, mais que chaque navigateur voulait faire fonctionner les sites populaires, ils n'ont pas eu d'autres choix que de faire de la rétro-ingénierie sur les autres navigateurs pour implémenter les technologies qui les intéressaient. C'est notamment ce qu'a fait Microsoft pour supporter le langage JavaScript (ou « JScript » pour les intimes d'Internet Explorer).

### Et les standards dans tout ça ?

En **1998-99** sortent ECMAScript 3, CSS2 et HTML4. ECMAScript 5 (il n'y a pas de version 4) sort en **2009**, CSS2.1 il y a quelques mois et HTML5... est loin d'être terminé.

Ce trou de 10 ans s'explique par plusieurs facteurs. Le premier est l'idée saugrenue du W3C de remplacer le web HTML imparfait par un web fait de XML où tout le monde fermerait ses balises et mettrait bien ses attributs entre *double-quotes*. Le XHTML 1 sort en **2000** et le travail sur XHTML2 commence.  
En **2004**, Mozilla, Opera et Apple forment le [WHATWG](http://wiki.whatwg.org/wiki/FAQ#What_is_the_WHATWG.3F). Ils comprennent la nécessité de standardiser les technologies web et ne croient pas à la direction du W3C avec XHTML. Leur effort est ce qui deviendra plus tard « HTML5 ». En **2009**, le [W3C abandonnera finalement XHTML2 au profit de HTML5](http://www.w3.org/News/2009.html#entry-6601).

Plus généralement, les différents acteurs des technologies web ont eu besoin de se rencontrer et d'acquérir ensemble l'expérience nécessaire à la rédaction de standards web avec une contrainte majeure forte : ne jamais casser un site web existant (« *break the web* » comme on dit).

Une énorme partie de standardisation de HTML5, CSS2.1 et ECMAScript 5 a été de standardiser les technologies web. Les prochaines bien sûr, mais surtout celles qui existent déjà ! Contrairement au scénario idéal évoqué plus haut, HTML4, CSS2 et ECMAScript 3 étaient très très loin d'expliquer exhaustivement comment implémenter lesdites technologies. On trouve d'ailleurs encore aujourd'hui des bugs dans les spécifications. Bugs qui sont souvent corrigés pour aller dans le sens des implémentations (« de facto standard » comme on dit dans le jargon).  
Spécifiquement pour HTML5, une grosse partie du travail a été un travail de rétro-ingénierie. Le *doctype* n'a pas cette tête sans raison. C'est après un certains nombre de tests qu'on s'est rendu compte que les navigateurs ne lisaient pas entièrement les *doctypes* et que réduire un *doctype* à `<!doctype html>` suffisait à déclencher le mode standard de tous les navigateurs. Idem pour `<meta charset="utf-8">` qui n'est que la standardisation du fait que les navigateurs se contentent seulement d'aller chercher le *charset* dans `<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />` et d'ignorer le reste.

## Le cas des préfixes -webkit-

Pour celles et ceux qui n'ont pas vu l'incendie démarrer, tout a commencé par une déclaration lors d'une rencontre face à face du CSSWG : [certains fabricants de navigateurs ont annoncé qu'ils envisageaient d'implémenter le support du préfixe -webkit- pour certaines propriétés CSS](http://lists.w3.org/Archives/Public/www-style/2012Feb/0313.html).  
Cette annonce a déclenché beaucoup de réactions ainsi qu'un certain nombre d'accusations. Ça serait la faute de Webkit d'avoir gardé les préfixes trop longtemps ; ou la faute du CSSWG de n'avoir pas standardisé assez vite les technologies ; ou la faute des développeurs web d'avoir utilisé en production des préfixes présents à fin d'expérimentation ; ou la faute des autres navigateurs d'être faibles au point d'implémenter les préfixes -webkit-.

Prenons plutôt un instant pour comprendre la situation à l'échelle systémique plutôt que du point de vue partiel de certaines parties.

### Les préfixes CSS

L'idée des préfixes CSS découle des précédentes expériences d'innovations sur les technologies web. En effet, avant cette idée de préfixe, chaque navigateur rajoutait ses propriétés un peu comme il le voulait et si l'idée était bonne, les autres navigateurs copiaient la propriété — bugs, irrégularités et inconsistances compris — donnant souvent lieu à des standards de facto.  
Rajouter un préfixe devant le nom d'une propriété permettrait d'innover sans donner de nom définitif. Le préfixe serait aussi une convention avec les développeurs web pour qu'ils jouent avec la propriété et fassent des retours avant sa standardisation, mais ne l'utilisent pas sur des sites en production.  
Une bonne idée sur le papier, mais [largement décriée par Henri Sivonen](http://hsivonen.iki.fi/vendor-prefixes/) (notamment connu pour son travail sur le *parser* HTML5 dans Firefox) quelques mois avant la rencontre du CSSWG.

### « Je veux un site plus beau que celui du voisin »

Ainsi Webkit, le moteur de rendu de Safari et Chrome, a implémenté des propriétés CSS avec préfixes à foison, s'autorisant beaucoup d'innovations « protégées » par les préfixes.  
Certaines innovations étaient très bonnes et permettaient en quelques lignes de réaliser des effets visuels améliorant grandement les sites. Les développeurs se sont alors mis à utiliser ces propriétés. Certains de ces développeurs ne cherchant qu'à faire des sites mobiles où WebKit est roi, pourquoi s'embêter à mettre les préfixes des autres navigateurs ou même la version sans préfixe ?

### « Sur tel navigateur, tel site est cassé »

Comme on l'a vu, aucun navigateur n'a envie de perdre des parts de marché ni que des sites apparaissent cassés. Dès lors les navigateurs n'ont plus le choix. Il leur faudra comprendre les préfixes webkit. Certes pas tous, mais les fabricants de navigateurs étudient les contenus sur le web pour faire le choix le plus judicieux.  
Inutile de dire que les [efforts de communication](http://www.glazman.org/weblog/dotclear/index.php?post/2012/02/09/CALL-FOR-ACTION%3A-THE-OPEN-WEB-NEEDS-YOU-NOW) en [direction des développeurs web](http://codepo8.github.com/prefix-the-web/) sont vains. Il n'est pas possible de tous les joindre ni d'obtenir leur accord pour changer leur site. Ainsi va la vie des systèmes décentralisés à grande échelle.

### Alors, à qui la faute ?

À tout le monde, à personne, ça n'a aucune importance. Du contenu avec des préfixes est là, [les navigateurs commencent à *aliaser* certaines propriétés](http://dev.opera.com/articles/view/opera-mobile-emulator-experimental-webkit-prefix-support/). Il faudra, le moment venu, codifier cela dans un standard de facto.  
Ce qui est à retenir de tout cela est la relation entre les développeurs web, leur contenu, les navigateurs web et les standards, qui, presque par nécessité, se contentent de codifier une réalité qui les précède plutôt que d'imposer cette réalité.

## Conclusion

Les technologies web ne sortent pas de la tête d'inventeurs bienveillants qui les codifient dans des standards parfaits. Les technologies web sont le fruit de l'histoire de l'interaction entre ceux qui implémentent ces technologies et ceux qui les utilisent. Les standards sont seulement la conséquence de cette histoire, pas la cause.  
On ne pourra pas revenir en arrière, on ne pourra pas tout jeter et tout recommencer. L'accepter permet d'éviter rides et cheveux blancs :-)
