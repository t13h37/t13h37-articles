L'importance de la rapidité des sites web dans le ressenti des visiteurs et leurs comportements est une prise de conscience assez récente. Le sujet a émergé il y a déjà quelques temps, mais n'a commencé à se démocratiser que depuis peu.

Aussi, bien souvent, la question se pose d'optimiser un site existant pour qu'il soit ressenti plus rapide (ou moins lent) par ses visiteurs.

# Des bonnes pratiques tu n'abuseras point…

Parmi les techniques généralement préconisées pour améliorer la performance d'un site web, certaines peuvent avoir des effets pervers ou indésirables si on les utilise mal ou à l'extrême.  
Voyons ensemble un certain nombre d'exemples.

## Domain-sharding

Cette technique consiste à distribuer les fichiers (images, scripts, feuilles de styles) chargés dans la page entre plusieurs domaines (ou sous-domaines) différents.

L'origine de cette pratique remonte aux anciens navigateurs (Internet Explorer 6 en tête, mais aussi IE7) qui se limitaient à deux téléchargements paralèlles par domaine (c'était justifiable à l'époque de la conception de IE6 et des connexions internet par RTC, mais ça n'a pas été amélioré dans IE7). Il s'en suivait une file d'attente de téléchargements qui ralentissait beaucoup l'affichage complet de la page sans exploiter la bande passante disponible sur le réseau.

En distribuant les fichiers sur plusieurs domaines, on peut contourner le défaut de ces navigateurs et permettre d'avoir 4 files d'attentes avec 2 domaines, 6 files avec 3 domaines, etc.  
L'optimisation du temps de chargement pour ces navigateurs peut donc conduire à multiplier le nombre de domaines.

Mais les navigateurs récents et modernes ont considérablement amélioré ce comportement, et gèrent d'eux-même de 6 à 8 files de téléchargements parallèles par domaines.

Avec un domain-sharding agressif (3 domaines ou plus) les navigateurs modernes doivent alors gérer le téléchargement parallèle de plus de 18 fichiers. Outre que ce nombre de téléchargement parallèle n'améliore plus l'utilisation de la bande passante par rapport au fonctionnement par défaut de ces navigateurs, cela les oblige à lancer plus de requêtes DNS qui ralentissent la récupération des fichiers. Il s'en suit généralement [un ralentissement](http://www.ravelrumba.com/blog/domain-sharding-tests-in-ie7-ie8-firefox-and-safari/).

Aussi il faut bien se garder ici de pousser cette technique à l'extrême, même si elle a une efficacité certaine sur les vieux navigateurs, et se contenter en général de 2 domaines pour la répartition des fichiers de la page.

## Sprites

L'utilisation des sprites vise à réduire le nombre de fichier à télécharger pour afficher la page web. Le principe est de réunir plusieurs images en une seule (en les séparant éventuellement par des zones de marges), puis d'utiliser cette image dans les feuilles de style, avec la propriété `background-image`, en utilisant les propriétés de positionnement du sprite pour n'afficher que la portion désirée.

Cette technique est très efficace puisqu'elle permet au navigateur de télécharger une grosse image au lieu de plusieurs petites ; le téléchargement d'un fichier nécessite plusieurs échanges d'information entre le serveur et le navigateur avant que le serveur n'envoie vraiment les données, et le téléchargement d'un petit fichier est d'autant moins efficace que [la latence (le temps d'un aller-retour entre navigateur et serveur) est grande](http://calendar.perfplanet.com/2010/know-your-enemy-latency/ ). En mettant en commun plusieurs fichiers en un seul, on économise beaucoup d'aller-retour, et le serveur peut envoyer le fichier avec un débit effectif plus important. Pour une taille totale identique, le navigateur récupère donc l'image plus rapidement.

Cependant, utilisée sans discernement elle peut avoir des inconvénients :

### Dégradation avec le temps

Maintenir un sprite est lourd : si le sprite est modifié et que les images se trouvent déplacées dans le sprite, il faut ré-écrire toutes les règles CSS associées, ce qui peut être assez pénible pour un gros sprite. En conséquence on évite en général ce scenario là, au prix d'une dégradation progressive de l'efficacité du sprite si on n'y prête pas attention.

Lors de la suppression d'une image dans le sprite (en fait une image dont on a plus besoin), on se contente en général d'ignorer la zone du sprite sans la reconstruire, pour éviter de modifier toutes les règles CSS de positionnement qui l'utilisent. Avec le temps le sprite peut grossir excessivement, chargé d'images qui ne servent plus.

De même, si une image change de taille et doit être plus grande dans une des dimensions, il faut alors la réaffecter dans une nouvelle zone du sprite, sauf à recomposer l'ensemble du sprite et ré-écrire toutes les règles CSS associées, et on se retrouve avec une place perdue.

L'ajout  ou la modification d'une image dans le sprite oblige à l'invalider (modification de l'url) et oblige à recharger tout le sprite, beaucoup  plus gros que la simple image modifiée. Dans ce cas, le chargement de la  page sera plus lent pour un visiteur régulier de la page web par rapport à une situation où les sprites n'auraient pas été utilisés.

Pour limiter l'impact de ces cas courants au cours de la vie du site, il est souvent judicieux de n'associer dans un même sprite que des images qui forment un ensemble logique, ou correspondant à un élément d'interface précis. Il est ainsi plus facile d'évacuer toute l'image quand l'ensemble n'est plus utilisé, ou de recomposer le sprite et les règles associées, en nombre plus limité, si nécessaire.

### Dégradation de l'accessibilité

Les sprites sont initialement recommandées pour regrouper des images CSS. Mais dans le soucis d'une optimisation plus agressive, il est souvent tentant d'utiliser cette technique pour regrouper des images normalement embarquées dans la page.

Mais dans ce cas, la technique entraîne directement une perte d'accessibilité : une image de décoration en CSS est purement visuelle, alors qu'une image référencée dans le HTML de la page porte un sens via son attribut `alt`. Même si certains artifices peuvent êtres utilisés (image transparente avec un attribut `alt` sur laquelle est appliquée la directive CSS), le visiteur peut se retrouver dans certains cas avec un élément d'interface incompréhensible (affichage de la page sans style par exemple, ou avec des styles personnalisés).

Pour cette raison, il ne faudrait pas utiliser les sprites pour remplacer une balise `<img>`.

C'est malheureusement une pratique que l'on rencontre très souvent dans l'intégration des menus de navigation de type onglets. On y utilise des images à la place du texte, pour éviter le débordement lors du grossissement de la police par l'utilisateur (ce qui est en soi une pratique discutable). Pour éviter le chargement d'un grand nombre d'image pour ce menu, on en vient alors à utiliser un sprite au prix d'une dégradation de l'accessibilité.

## Concaténation des fichiers JS et CSS

La concaténation des fichiers javascript et des feuilles de styles est une autre technique recommandée pour réduire le nombre de fichiers à télécharger pour une page.

C'est une technique simple à mettre en oeuvre, et de nombreux outils sont disponibles pour simplifier cette opération, en la combinant en général avec une opération de compression/minification.

Dans le cadre de l'optimisation d'une page, il est évident qu'il faut concaténer tous les fichiers javascripts en un seul, et toutes les feuilles de style en une seule.

Mais lorsqu'on optimise un site complet, composé d'une multitude de pages, il convient d'être plus prudent : toutes les pages n'appellent pas forcément la même liste de scripts et/ou de feuilles de styles.

En l'absence de concaténation, seuls les scripts et/ou les feuilles de styles pas encore en mémoire sont chargés lorsqu'on affiche une nouvelle page du site. Mais si on concatène tous les scripts de la page, alors le fichier complet concaténé est différent de la page précédente, et il est intégralement rechargé. La concaténation fait perdre le chargement modulaire des scripts et des feuilles de styles.

Pour prendre en compte ce point, deux stratégies sont possibles :

- Concaténer en un seul fichier tous ceux qui apparaissent sur au moins une page du site. Cette stratégie est simple à mettre en oeuvre et s'applique bien sur un petit site mais elle peut avoir des impacts négatifs : si une des pages utilise un script qui ralentit la page par la connexion à un service externe par exemple (cartographie), alors tout le site se trouve ralentit par cet appel au service externe ;
- L'alternative est de regrouper la partie commune à toutes les pages en un seul fichier concaténé, puis pour chaque page où cela est nécessaire, d'ajouter un second fichier qui regroupe tous les composants spécifiques à cette page.

La situation se complique lorsque par exemple une page A contient un lecteur vidéo, une page B une cartographie reposant sur un service externe, et une page C contient les deux composants. Il y a alors de nouvelles combinaisons possibles, et le choix dans la combinaison des fichiers favorisera le chargement de certaines pages au détriment de certaines autres.

Dans ce cas, il convient d'arbitrer en fonction des volumétries : la proportion des pages dans chaque cas pondérées par le traffic (on privilégiera a priori la configuration la plus fréquente).

On se rend compte que ce type d'abitrage pose aussi des problèmes potentiels de maintenabilité.

## Javascript en pied/bas de page

Une autre pratique recommandée est l'insertion des appels javascript à la fin du HTML, juste avant la balise de fermeture `</body>`. Cette pratique permet :

* D'éviter des blocages de chargement d'autre composants provoqués par les scripts (lorsque le navigateur rencontre un script, il stoppe le chargement des composants qui suivent et la construction de la page tant que le script n'a pas été chargé ni executé) ;
* De libérer le processeur pour le travail de rendu de la page, en évitant de le charger avec l'interprétation du javascript.

Cependant cette technique peut-être assez problématique. Dans le cadre d'une page unique, il est assez simple de déplacer tout le javascript en bas de page.

Dans le cadre d'un site complet, dont les pages sont souvent fabriquées à partir de composants différents (blocs de page, inclusion, plugin… selon le système utilisé côté serveur), il peut être plus compliqué de gérer cette contrainte.

Tous les fichiers javascripts devant être regroupés en bas de page, cela oblige à les séparer des composants de coeur de page pour lesquels ils servent, et la maintenance s'en trouve fortement compliquée. En particulier lors du retrait d'un composant qui utilisait un fichier javascript spécifique, il devient assez facile d'oublier de retirer ce script associé, et on peut se retrouver assez facilement à avoir des scripts en pied de page qui ne servent plus.


## La course au scoring

Enfin, le dernier piège que nous aborderons ici concerne l'utilisations des scores comme [PageSpeed](https://developers.google.com/speed/pagespeed/) ou [YSlow](http://developer.yahoo.com/yslow/). Ces outils d'évaluation ont été mis en place pour aider les développeurs à avoir une vision d'ensemble de l'optimisation de leurs pages et synthétisent l'ensemble des tests sous forme d'un score global.

Il devient alors tentant de chercher à optimiser ce score à tout prix, et de le comparer avec d'autres sites pour apprécier la qualité de sa propre optimisation.

Cependant il y a là deux pièges :

- Toutes les règles prises en compte dans ces outils ne sont pas forcément pertinentes pour votre site (l'utilisation des CDN par exemple), et il conviendrait au moins de pondérer certaines des pratiques notées en fonction de la typologie des visiteurs de votre site (localisation géographique, parc navigateur…) ;
- Ces outils ne font qu'évaluer le travail d'optimisation, pas la rapidité du site.

Ce dernier point est à mon sens un des plus gros pièges de l'optimisation de la performance web : à se focaliser sur la technique, sur les outils, on oublie vite que quelle que soit l'énergie que l'on dépense, une page lourde même optimisée, restera plus lente à charger qu'une page légère à la base.

Ce à quoi est confronté le visiteur du site, ce n'est pas au manque d'optimisation du site, c'est à sa lenteur.

Ainsi, la première et plus importante optimisation consiste à se poser la question de ce qui pèse dans la page, ce qui provoque plein de chargements de fichiers, ou le chargement de fichiers lourds, et de la nécessité de ces élements, ou encore de la façon dont il serait possible de les aménager pour réduire à la source le temps de chargement de la page.


# La performance Web : une démarche continue, sur toute la durée de vie du site

La tendance générale est à [l’inflation de la taille des page web](http://gigaom.com/2012/05/23/the-growing-epidemic-of-page-bloat/), et il en sera sûrement ainsi tant que la rapidité d'un site sera considéré comme une prestation secondaire, loin derrière l'aspect visuel ou la disponibilité de moults gadgets fonctionnels à la mode.

## À la conception

L'accessibilité des sites a longtemps été considérée comme une annexe, un plus que l'on faisait si on avait le temps, à la fin de la réalisation. L'expérience a montré que ça ne marchait pas et ne donnait que de piètres résultats. Peu à peu l'accessibilité est prise en compte dès le début du projet, ce qui permet d'orienter les choix techniques, visuels… et de prédisposer le site pour une bonne accessibilité.

Il devra en aller de même pour la performance web et la rapidité d'affichage des sites web : ce n'est qu'en prenant en compte cette prestation dès la conception que l'on peut obtenir, in fine, un bon résultat qui permettra au site d'être perçu comme rapide et agréable à utiliser par les internautes. Car le temps de réaction contribue lui aussi au ressenti du visiteur, au même titre que l'aspect visuel ou l'ergonomie du site.

Le parallèle avec l'accessibilité est d'autant plus pertinent que la rapidité de service d'un site contribue également à son accessibilité en rendant sa consultation possible y compris dans des conditions de connexion dégradée (que l'on éprouve de plus en plus souvent en situation de mobilité avec les accès wifi publics et/ou partagés).

## Lors du développement

Si les choix de conception prédisposent la rapidité d'un site en évitant d'embarquer de nombreux gadgets techniques et/ou une charte visuelle qui nécessite de nombreux éléments graphiques, c'est ensuite lors du développement technique que les bonnes pratiques devront être appliquées.

Pour cela il est primordial que les équipes techniques soient a minima sensibilisées au problème et aient en tête en permanence les quelques techniques les plus importantes qui doivent être bien appliquées.

Dans le cadre du développement il est très utile de recourir à une [liste de bonnes pratiques](http://checklists.opquast.com/webperf/workshops/status/validate) et des outils comme PageSpeed ou YSlow pour suivre la qualité de la réalisation et mettre en lumière les points faibles à améliorer. Cependant on veillera bien à utiliser une liste de pratiques et points techniques adaptée au projet !

En procédant ainsi, il sera possible d'aboutir à un site rapide et bien né.  Ensuite, en fonction des compétences internes (ou externes) disponibles il est toujours possible d'aller plus loin avec des stratégies plus agressives, en fonction des objectifs du projet.

## Lors de la vie du site

La gestion de la performance web ne s'arrête pas à la livraison du site :

- Le comportement des navigateurs évoluent au fil des nouvelles versions, et il peut être nécessaire de modifier certains choix d'optimisation en fonction du taux d'utilisation de chaque version par vos visiteurs ;
- Mais surtout le site continue à vivre : il subit régulièrement des petites évolutions techniques qui sont autant d'occasion de dégrader la performance du site.

En effet l'expérience montre que les gros sites lents sont souvent la conséquence malheureuse des multiples évolutions techniques réalisées par des intervenants différents. Pour ne pas risquer de casser le site, on procède par ajout sans jamais rien enlever (scripts ou feuilles de style), ce qui aboutit in fine à un millefeuille de plus en plus compliqué à maintenir et qui ralentit de plus en plus le chargement des pages.

Aussi il est important de continuer à suivre la performance du site en cours de vie. Pour cela il peut être très pertinent de mettre en place un monitoring automatique qui lève des alertes dès que le temps de chargement des pages se dégrade ou dépasse un seuil objectif.   
Il sera alors possible de détecter la dégradation de la performance causée par une évolution et de faire corriger par l'intervenant.

Mieux encore, en étant mesurée en continue, et énoncée comme un livrable, la non-dégradation de la performance peut-être prise comme une contrainte lors des interventions techniques et évolutions du site.

# Automatiser pour démocratiser et aller encore plus loin

Il faudra sans doute encore un peu (soyons optimistes !) de temps avant que la performance web soit prise en compte dès le début du projet et tout au long de sa vie.

J'ai tendance à penser qu'un des leviers de démocratisation de la performance web est son automatisation.   
Il n'est pas question de prétendre que l'expertise d'un bon développeur peut être remplacée par quelques scripts, mais un certains nombre de pratiques peuvent être automatisées : l'optimisation des images, la concaténation et la minification des scripts et feuilles de styles, le domain-sharding, etc.

Que ce soit par des outils internes au projet et mis en place dès le début du développement, ou par un service externe (attention toutefois à la dépendance technique vis à vis d'un service externe), l'automatisation permet de garantir un niveau minimum de performance, et de libérer les développeurs des tâches techniques simples mais parfois fastidieuses pour se concentrer sur les points techniques plus complexes qui permettront au site d'être encore plus rapide.

Cependant, le piège dans lequel il ne faudrait pas tomber serait de faire croire que ces outils "automagiques" // néologisme volontaire ? ;) oui // fonctionnant en boite noire s'occupent de tout et évitent de faire le choix de la légèreté au moment de la conception !