# Bien calibrer ses tests : débit et latence

À quelle vitesse s'affiche un site ? La question est importante tant le confort d'utilisation et les revenus d'un site peuvent dépendre de cette réponse. Vous intégrez probablement déjà des pratiques visant à améliorer le rendu des pages et leur réactivité, et si vous êtes en phase d'industrialisation, vous faites peut-être du _monitoring_ de la performance. Au moment de paramétrer votre solution, une question a dû vous poser problème : quelle est la connexion type en France ? Et pour les mobiles ?  
Nous allons non seulement répondre à ces deux questions, mais en plus nous apercevoir qu'il y a une question plus pertinente à se poser.

## Pourquoi et comment calibrer ses tests ?

Les solutions de _monitoring_ du marché testent les pages généralement sans vous dire avec quel navigateur (probablement des Webkit headless, pour accélérer les tests), et le font depuis des _datacenters_ qui sont beaucoup trop proches des nœuds principaux du Web. Potentiellement, les sondes sont exécutées à partir de machines hébergées physiquement dans le même _datacenter_ que votre hébergeur ou avec un _peering_ privilégié avec le CDN.

Autant dire que les tests standards ne sont pas représentatifs de ce qu'endurent vos utilisateurs et c'est la raison pour laquelle on limite volontairement débit et latence, par exemple sur l'indispensable [WebPageTest](http://www.webpagetest.org/ ) ou chez certaines solutions payantes. WebPageTest a le mérite d'être transparent car vous avez une liste de connexions pré-paramétrées mais nous allons voir qu'elles ne représentent pas du tout la France.

![Paramètres par défaut de WebPageTest.org](parametre-WPT-org)

Côté transit réseau, il y a essentiellement quatre données qui influencent l'affichage d'un site :

- la latence ou ping, qui est le temps d'un aller-retour entre un navigateur et le serveur qui lui répond. Pour le [site moyen](http://httparchive.org/trends.php ), en HTTP 1.1, basé sur TCP, c'est [la mesure la plus importante](http://performance.survol.fr/2008/03/impact-de-la-latence-reseau/ ). C'est aussi la plus difficile à obtenir ;
- le download ou bande passante descendante, qui reste importante pour récupérer de gros objets. On nous vend des ADSL à plus de 20 Mb/s ([1](http://adsl.sfr.fr/toutes-nos-offres/ ), [2](http://abonnez-vous.orange.fr/residentiel/accueil/accueil.aspx ), [3](http://www.free.fr/adsl/internet.html )) et des mobiles à 5 Mb/s ; qu'en est il vraiment ?
- l'upload qui est rarement pertinent dans la performance web ;
- la perte de paquets : pratiquement inexistante sur des connexion filaires, mais omniprésent sur mobile. Là, par contre, impossible de trouver des chiffres, en supposant qu'ils signifient quelque chose.

Idéalement, il faudrait récupérer ces métriques de vos propres utilisateurs, grâce à du [Real User Monitoring](http://yahoo.github.com/boomerang/doc/use-cases.html) (RUM), mais la mise en œuvre est moins aisée que de récupérer les informations de sources externes, telle que nous allons le faire ici.
Si vous êtes pressé ou si vous me faites aveuglément confiance (et je vous comprends), vous pouvez sauter directement à "En résumé"

## À la pêche aux chiffres

En cherchant [dans mes archives](http://delicious.com/braincracking) et sur Google, je me suis rendu compte qu'il existait très peu de rapports rendus publics. J'en liste ici six en extrayant des données brutes. N'hésitez pas à m'en indiquer d'autres ou à décortiquer plus avant les sources.

### [Étude Akamai / Pingdom de 2010](http://royal.pingdom.com/2010/11/12/real-connection-speeds-for-internet-users-across-the-world/ )

Akamai est le leader mondial des CDNs, autant dire qu'ils voient passer du trafic et ont une bonne idée de ce qui se fait à l'échelle mondiale. L'étude de cette année-là comprend la répartition des débits en France.

- Débit moyen : 3,3 Mb/s
- Répartition :
    - 25 % moins de 2 Mb/s
    - 60 % entre 2 et 5 Mb/s
    - 15 % plus de 5 Mb/s

### [Akamai 2012](http://www.akamai.com/stateoftheinternet/ )

Chiffres plus récents, mais l'échelle de répartition a changé.

- Débit moyen : 4,6 Mb/s
- Débit moyen des réseaux mobiles : 2,8 Mb/s
- Répartition :
    - 0,1 % moins de 256 Kb/s
    - 45 % plus de 4 Mb/s
    - 4 % plus de 10 Mb/s


### DegroupTest, [2012](http://www.degrouptest.com/publications/6/barometre-debit-internet-s1-2012/1 ) et [2011](http://www.degrouptest.com/publications/5/barometre-debit-internet-s2-2011/6 )

La population des utilisateurs de DegroupTest est probablement biaisée, car on a affaire à des gens qui au minimum s'inquiètent de leur débit. Ce qui exclut ma mère et probablement la vôtre. Mais ils ont l'avantage de mesurer le ping, et d'isoler les extrêmes comme la fibre, le mobile et l'outre-mer.

- Débit moyen : 8,27 Mb/s (5,4 Mb/s hors fibre )
- Débit moyen des réseaux mobiles : 2,5 Mbps (chiffres 2011)
- Ping moyen : 80 ms (86 ms hors fibre)
- Ping moyen réseaux mobiles : 200 ms
- Débit montant moyen : 1,3 Mb/s ( 641 Kbp/s hors fibre)
- Répartition :
    - 13 % à 27 Mb/s de débit moyen
    - 87 % à 5,4 Mb/s
- à noter :
    - Meilleur latence possible : la fibre Orange avec 19 ms. Les opérateurs ADSL se situent entre 70 ms (Free) et 100 ms (SFR)
    - de 1 à 1,5 s de latence sur satellite
    - 270 ms de latence depuis l'outre-mer, 3 Mb/s de débit moyen

À noter que le débit et la latence moyenne ont baissé entre 2011 et 2012. J'imagine que le public a du s'élargir à des zones moins bien couvertes.

### [60 millions de consommateurs, 2012](http://www.60millions-mag.com/actualites/archives/la_verite_sur_le_debit_des_connexions_internet )

Leur testeur de débit a tourné pendant un an en 2011 et leur public est probablement plus proche du français moyen que DegroupTest. De plus, on y quantifie les variations périodiques de débit.

- Débit moyen : 5,6 Mb/s
- Répartition :
-- 11,8 % moins de 1 Mb/s
-- 12,8% de 1 à 2 Mb/s
-- 31,8% de 2 à 5 Mb/s
-- 30 % de 5 à 10 Mb/s
-- 12 % plus de 10 Mb/s
- À noter :
    - moins 20 % de débit à 21 h
    - moins 10 % le dimanche

### [Étude ARCEP](http://www.arcep.fr/fileadmin/reprise/observatoire/4-2011/obs-marches-t4-2011.pdf )

De cette étude sur les chiffres d'affaire des FAI et opérateurs mobile, j'ai extrait les volumes de population pour confirmer ou requalifier les chiffres des autres :

- 22 millions d'abonnements ADSL et fibre
- 0,6 million d'abonnement fibre et câble
- 0,3 million abonnés RTC
- 32 millions d'abonnés mobile "data"
- plus 80 % de volume de data mobile par an

### [Statistiques Cedexis](http://www.cedexis.com/fr/country-reports/ )

Les statistiques de "l'aiguilleur du net" mesurent le temps d'aller-retour moyen entre un utilisateur de FAI et un CDN afin de choisir le meilleur. Les valeurs de latence y sont plus hautes qu'ailleurs car les CDN ne font pas que servir des fichiers statiques, il y a beaucoup d'intelligence lorsqu'une requête arrive chez eux. Je les prends car elles donnent une bonne idée de la vitesse avec laquelle les fichiers arrivent chez l'internaute qui visite des sites utilisant les CDN.

- 118 ms de latence pour des fichiers hébergés sur Akamai (leader)
- 134 ms de latence pour des fichiers sur Amazon EC2 Europe

Après les chiffres bruts, passons à l'analyse.

## Quelle analyse ?

Il faut bien se dire que l'on compare des études avec des buts différents : mesurer l'efficacité des CDNs, des FAI ou avoir un vision plus globale oriente les méthodologies. C'est pour cela que j'explicite ma réflexion, pour que vous utilisiez les commentaires pour critiquer ma tentative de compréhension.

### Le débit moyen

Les statistiques d'abonnement de l'ARCEP montrent 2,7 % d'abonnés à la fibre par rapport au nombre total d'abonnement, alors que Degrouptest reçoit 13 % de ses mesures depuis la fibre. Nous pouvons donc requalifier le débit moyen de DegroupTest : __5,01 Mb/s__ (97,3 % * 5,4 Mb/s + 2,7 % * 27,3 Mb/s = 5,01 Mb/s).  
Cette nouvelle moyenne se situe entre celle d'Akamai pour la France (4,6 Mb/s), et celle de 60 millions de consommateurs (5,6 Mb/s). Akamai ne détaille pas sa méthode mais on suppose qu'elle est plus représentative, car non volontaire. Elle ne mesure cependant que la connexion entre Akamai et un internaute et Cedexis nous indique qu'Akamai n'est pas le plus performant. Il faudrait donc légèrement remonter ce chiffre. D'un autre côté, 60 millions de consommateurs a fait son étude en 2011, et entre-temps DegroupTest semble indiquer une baisse de débit ADSL de 600 Ko/s. Il faudrait donc revoir leur moyenne à la baisse. Les chiffres convergent vers la valeur DegroupTest, que j'estime légèrement surestimée (population trop "aware").

Pour arrondir, on peut donc __situer un débit moyen à 4,8 Mb/s__ sur ligne fixe. Concernant le débit mobile moyen, Akamai et DegroupTest ont, à 30 Kb/s près, la même moyenne. On peut l'arrondir à __à 2,5 Mb/s__.

### La latence

On applique la correction des statistiques ARCEP sur les statistiques DegroupTest et on obtient cette valeur arrondie : __85 ms__. Cependant en regardant les données Cedexis, on voit des temps de réponse bien supérieurs, de 110 ms par exemple pour récupérer un statique sur un CDN populaire comme Akamai. Cela est assez cohérent avec le fait qu'un CDN rajoute forcément un peu de latence (temps de routage supplémentaire, mise en cache, etc.) et que la population DegroupTest est surement un peu moins représentative que celle mesurée par Cedexis.

Concernant le ping sur mobile, on manque cruellement de données ; la seule qu'on ait trouvé pour la France est celle de DegroupTest, soit 200 ms. Dans des études bien moins larges dans d'autres pays, les chiffres varient de [200 ms](http://www.webperformancetoday.com/2012/04/02/mobile-versus-desktop-latency/ ) à [300 ms](http://www.webperformancetoday.com/2011/10/26/interesting-findings-3g-mobile-performance-is-up-to-10x-slower-than-throttled-broadband-service/ ).

Pour la latence, nous nous fixons donc une moyenne arrondie de __95 ms sur ligne fixe__ et __200 ms sur mobile__.

### Le cas du mobile

Le débit moyen sur réseau mobile (2,5 Mb/s) est donc plus élevé que 25 % des ADSL de France. La latence y reste tout de même deux à trois fois plus élevée. Mais même en calibrant vos tests avec ces données et en supposant que vous les exécutiez depuis [un vrai mobile](http://mobitest.akamai.com/m/index.cgi ), vous réalisez vite que quelque chose cloche : le ressenti utilisateur n'est pas du tout le même. En fait, il manque une dernière composante, assez rare en ADSL : __la perte de paquets TCP__. Constamment les connexions ouvertes entre votre téléphone et l'antenne relais sont interrompues par des obstacles physiques, électromagnétiques ou un changement d'antenne. Je n'ai pas trouvé d'étude avec un taux moyen de perte de paquet, aussi c'est un peu au pifomètre que __j'utilise la valeur 25 %__. À débattre.

Il manque également le côté aléatoire de la connexion qui fait tout le charme des réseaux mobiles : parfois vous téléchargez une image en une demi-seconde, parfois vous n'arrivez pas à avoir un octet pendant plusieurs minutes.

Exécutez régulièrement les applications [speedtest](http://speedtest.net/mobile.php ) ou DegroupTest ([iOS](http://links.fhsarl.com/pplipple ), [Android](http://links.fhsarl.com/applendroid )) pour halluciner sur la variabilité des caractéristiques réseau.

![Test débit mobile](test-debit-mobile.png)

Sur quelques tests ci-dessus, avec deux tests effectués à moins d'une minute d'intervalle et sans bouger, vous pouvez voir une différence de latence d'un facteur 4. En bas et en haut, vous pouvez également voir des tests qui vont de 14 Kb/s à 9 Mb/s. Et bien sûr, je vous ai masqué les tests qui n'aboutissent pas.
Mais non seulement il n'existe pas d'étude sur les trous réseau (en supposant qu'une telle étude puisse être représentative), mais en plus __nous ne voulons pas introduire d'aléa dans le cadre du monitoring__, ou alors comment savoir si une alerte en est vraiment une ? Nous devons malheureusement choisir des mesures dégradées mais fixes.

### En résumé

<table><caption>Les connexions moyennes françaises en 2012</caption>
<tbody>
<tr>
<th></th>
<th scope="col">Lignes Fixes</th>
<th scope="col">Réseau mobile</th>
</tr>
<tr>
<th scope="row">Débit descendant</th>
<td>4,8Mb/s</td>
<td>2,5Mb/s</td>
</tr>
<tr>
<th scope="row">Latence</th>
<td>95ms</td>
<td>200ms (plus 25 % de perte de paquets)</td>
</tr>
</tbody>
</table>

### Il n'y a pas de connexion type

Mon professeur de statistiques me tirerait les oreilles si on s'arrêtait là. En effet, une moyenne seule est à peu près inutile sans [l'écart-type](http://fr.wikipedia.org/wiki/%C3%89cart_type ) qui permet de juger de la représentativité de cette moyenne. En fait, une moyenne est certes pratique à manipuler, et il est utile de surveiller son évolution, mais __elle est particulièrement trompeuse__ si la répartition des mesures n'est pas concentrée autour de la moyenne. Et justement, les études d'Akamai, de l'ARCEP et de 60 millions de consommateurs montrent qu'il y a __de fortes disparités dans l'équipement des utilisateurs__.

- L'ARCEP nous dit qu'il reste 1,4 % de gens en RTC (56 Kb/s), soit à l'échelle de la France 300 000 personnes ; dur de savoir si c'est leur unique moyen d'accéder au Web, mais c'est un débit 500 fois inférieur aux mobiles ! Akamai signale également un faible taux de débits inférieurs à 256 Kb/s ;
- DegroupTest nous avertit du fait que depuis la France d'outre-mer, on a du 250 ms de ping en moyenne, l'équivalent du mobile, et un débit 40 % inférieur à celui de la métropole ;
- 60 millions de consommateurs et Akamai montrent que __50 % des utilisateurs ont moins de 5 Mb/s__, avec une répartition qui a l'air à peu près égale par tranche de 1 Mb/s : 10 % ont moins de 1 Mb/s, __20 % moins de 2 Mb/s__, etc. ;
- les tuyaux du Web français sont embouteillés le soir, avec une __perte de 20 % de débit entre 21 h et 22 h__.

![Il n'y a pas d'ADSL type en France](repartition-debits.png)

Nous nous sommes donc posés la mauvaise question : calibrer vos tests sur LA moyenne française est à peine moins trompeur que de mesurer depuis votre poste avec votre navigateur récent, sur votre réseau d'entreprise branché à la fibre (oui tout le monde le fait, et c'est MAL).

## Enfin : quelle stratégie de test ?

Tous ces chiffres vont nous permettre de définir une vraie stratégie de test de la performance perçue. Cela commence par définir des objectifs de réactivité raisonnables en terme de confort d'utilisation, par exemple :

- afficher quelque chose avant une seconde (start render) ;
- promesse / fonction principale de la page affichée avant deux secondes ;
- fonction principale interactive avant cinq secondes.

Note : les valeurs que j'indique ici sont un peu génériques, et sont à définir entre les équipes "produit" (marketing, ergonomie) et les équipes techniques (développeurs, sysadmins).

Vous devez maintenant être cruel et déterminer quelle proportion d'utilisateurs n'aura pas droit à cette rapidité. C'est un peu rude dit comme ça, mais une page rapide pour "tout le monde" coûte très cher. Généralement on vise à satisfaire par exemple 80 % de la population.

Voici un petit tableau qui devrait vous aider à prendre vos décisions :

<table><caption>Calibrage des tests pour ligne fixe</caption>
<tbody>
<tr>
<th scope="col">Un débit de <strong>X</strong> Mb/s</th>
<th scope="col">et une latence de <strong>Y</strong> ms</th>
<th scope="col">laissent de côté <strong>Z</strong> % des visiteurs</th>
</tr>
<tr>
<td>5.0Mb/s</td>
<td>95ms</td>
<td>50%</td>
</tr>
<tr>
<td>4.0Mb/s</td>
<td>100ms</td>
<td>40%</td>
</tr>
<tr>
<td>3.0Mb/s</td>
<td>110ms</td>
<td>30%</td>
</tr>
<tr>
<td>2.0Mb/s</td>
<td>120ms</td>
<td>20%</td>
</tr>
</tbody>
</table>

Remarques :

- Les débits et pourcentages semblent joliment arrondis. C'est de la chance.
- Pour le ping, on n'a aucune statistique sur la répartition réelle, ce sont donc des suppositions personnelles (basées sur des années de jeu en ligne...) que je vous invite à critiquer.

Pour le réseau mobile, on est bien embêté car on n'a aucune idée de la répartition ! On sait juste qu'elle est très volatile, ne serait-ce que pour le même utilisateur. Donc, soit on joue ça au doigt mouillé avec la certitude de se tromper, soit on utilise la moyenne qui est pratiquement un mensonge. Mmmm. Choix cornélien mais, à choisir, autant partir sur une valeur un tout petit peu objective, c'est-à-dire la moyenne constatée, et y rajouter de la perte de paquets.

Je mettrais donc ces trois valeurs par ordre de priorité :

1. 3 Mb/s avec une latence de 110 ms pour représenter 70 % de vos utilisateurs sur lignes fixes ;
2. 2,5 Mb/s avec une latence de 200 ms et __une perte de paquets de 25 %__ pour l'ensemble des utilisateurs de réseau mobile ;
3. 4,80 Mb/s avec une latence de 95 ms pour "la moyenne" des connexion filaires.

La moyenne reste là surtout parce que c'est un chiffre que tout le monde (croit) comprend(re) et pour comparer mobile et bureau.

Si vous avez une population particulière (outre-mer, visiteurs à 21 h, habitant une grande ville, professionnelle, très mobile, etc.), il va vous falloir fouiller dans les chiffres ci-dessus pour trouver ce qui se rapproche le plus de vos utilisateurs. Ou, bien sûr, monter votre propre monitoring des capacités de vos utilisateurs.

## Résultats

Pour conclure, comparons les valeurs DSL par défaut de WebPageTest.org avec celles que nous avons déterminées pour représenter 70 % des français. J'ai lancé un test sur un site moyennement complexe, qui n'a pas (encore) été optimisé et qui fait partie des sites à forte audience de France : Pluzz.fr.

![Comparaison valeurs par défaut et personnalisées](pluzz-comparaison-valeurs-defaut-et-custom.png)

Pour plus de détails, voir [le détail du déroulé](http://www.webpagetest.org/video/compare.php?tests=121014_2994e714a56d3b251702fd9e2dcf43c0%2C121014_aa3557eec96550f644cc462b1d3647bb&thumbSize=200&ival=100&end=visual ).
Avec les valeurs par défaut, ce site s'affiche en moins d'une seconde, donnant l'impression que l'optimisation n'est pas nécessaire. Avec nos valeurs plus réalistes prenant en compte 70 % de la population, le start render se situe à 1,4 seconde, confirmant le besoin d'entamer des travaux si l'on veut atteindre les objectifs de performance perçue.

Et vous, savez-vous quelles sont les valeurs utilisées par votre solution de monitoring ?

