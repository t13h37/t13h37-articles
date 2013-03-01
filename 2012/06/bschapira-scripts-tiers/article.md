# Scripts tiers & appels induits : ne perdez pas le contrôle de votre site

Parlons un peu de contenus tiers, et plus particulièrement de scripts tiers.
Allons, allons, ne me dites pas que vous ne savez pas de quoi je parle... Le bouton “J’aime” de Facebook ? Le bouton “Google +1” ? Le code javascript de Google Analytics ou de Xiti ? Tous des scripts tiers, et presque tous présents sur la grande majorité des sites Web français.
Du contenu peut-être présent également sur votre site, que vous le sachiez ou non, et qui peut nuire à votre performance technique et commerciale comme à la sécurité de l’information que vous détenez sur vos visiteurs. 
Comment ? C’est ce que nous allons analyser ensemble.

## Paroles, paroles, paroles

Tout commence toujours par une promesse :

<blockquote class="speaker1">Bonjour, nous sommes la société XXX et nous aimerions vous proposer nos services qui [description enchanteresse à base de poneys volants sur Mars].</blockquote>
<blockquote class="speaker2">- Écoutez, oui, mais je reste sceptique. J’aimerais inclure votre logiciel dans mon site mais j’imagine que tout cela a un coût technique... ?</blockquote>
<blockquote class="speaker1">- Pas du tout, car *une simple ligne de Javascript suffit*.</blockquote>

Des pays entiers sont tombés pour cette simple ligne de Javascript ([au moins sur cette carte](http://xkcd.com/802/)). Car cette discussion est en général suivie d’accords commerciaux et de cinq minutes de développement montre-en-main et paf ! Vous venez d’inclure un script tiers dans votre site. Fantastique ? Pas forcément.
Qu’avez-vous réellement fait ? Vous avez conclu un accord avec un intervenant extérieur à votre S.I., lui proposant d’inclure dans votre site un espace d’exécution Javascript que vous ne contrôlez pas. Même si vous avez défini contractuellement les conditions d’utilisation de cet espace, vous n’avez que très peu de moyens à votre disposition pour le surveiller. Vous venez de transformer votre site en porte-avions, sans avoir aucun contrôle sur les engins qui en décollent et y atterrissent. Et votre prestataire en est bien souvent conscient...

![Image animée tirée du film The Shining](jack.gif "Quand on essaie de me convaincre en me disant qu’une simple ligne de Javascript suffit")

## Viens chez moi, j’habite chez une copine

Les services fournis par ces prestataires sont légion : publicité (régie, reciblage, publicité comportementale), échanges de données, mesures analytiques, fournisseurs de données tierces, mesures de performance... Tous ont cependant le même défaut : ils ouvrent votre site à des éléments extérieurs, hors de votre portée et très souvent, hors de la leur.

Prenons l’exemple d’une régie publicitaire qui vous propose d’inclure dans vos pages une iFrame qui ressemble à ça :

~~~ {lang="javascript" line="1"}
<iframe src="https://maregie.com/0/4563/ad.htmlAccueil=0&Comportemental=1&urlsrc=monsite.com/about"></iframe>
~~~

Que se passe-t-il après que vous l’ayez inclue dans votre site ? Elle ouvre une porte, et vous n’avez aucun contrôle sur ce qui va rentrer. Cette régie travaille peut-être en relation avec d’autres régies. Ainsi, lorsque vous appelez maregie.com, une redirection est faite vers regiepartenaire.fr sans que vous le sachiez. Au passage, notez que vous avez appelé la première régie en SSL, ce qui a un impact significatif sur le temps de chargement. Or rien ne vous assure que la redirection est sécurisée, ce qui est déjà un problème, mais surtout ce premier appel ne sert à rien, puisqu’il ne contacte pas la régie qui vous livre la publicité finale. C’est ce que j’appelle la problématique des appels induits : sans que vous ne les ayez invités, ces éléments sur lesquels vous n’avez aucune information peuvent porter atteinte à l’intégrité de votre site.

## L’appel de tous les dangers

Ces appels de ressources induits peuvent avoir plusieurs effets négatifs sur la qualité technique de votre site, ou sur son efficacité commerciale.

### Performance Web dégradée

L’exemple de script tiers précédent avait une vocation pédagogique et simplifiait énormément la problématique. D’expérience, le nombre d’appels inutiles peut être bien plus important, de l’ordre de plusieurs dizaines, voire de plus d’une centaine de redirections, scripts, images... Ces appels ont différentes conséquences sur la performance Web :

- Les redirections, toutes inutiles, qui gâchent un temps précieux ;
- Les appels sécurisés, qui impliquent le chargement des différents certificats attenants et leurs interprétations souvent coûteuses ;
- La multiplication des domaines différents qui induit un nombre important de résolutions <abbr title="Domain Name System">DNS</abbr> nécessaires à leur appel.

Peu importe comment vous attaquez le problème : l’inclusion d’un script tiers et les appels qu’il induit dégradent l’expérience de vos visiteurs. La seule question qu’il vous reste  à vous poser est de savoir quel en sera l’impact sur votre efficacité opérationnelle. Sur un site e-commerce, un site plus lent peut signifier un taux de rebond plus important, et une diminution du chiffre d’affaire. Sur d’autres types de sites, cela pourra avoir divers impacts dont le plus simple : nuire à la perception qu’ont vos clients de votre marque. Mais la performance ne doit pas être votre seule crainte...

### Exposition aux risques encourus par le partenaire

Entre le 31 mai et le 1er juin 2012, de nombreux sites ont subi des ralentissements conséquents, certains étant même indisponibles. Pour les utilisateurs, il était tout simplement impossible de se rendre sur ces sites, leur chargement ne se terminant jamais.

![Temps de réponse d’un important site e-commerce, image issue d’un excellent article de CathPoint sur ce problème](impact-facebook.png "Temps de réponse d’un important site e-commerce, image issue <a href="http://blog.catchpoint.com/2012/06/01/facebook-outage-wake-up-call-for-websites/">d’un excellent article de CathPoint</a> sur ce problème")

Leur point commun : avoir intégré le bouton “J’aime” de Facebook en mode “inline”. Manque de chance, le géant du réseau social avait quelques problèmes avec sa plate-forme à ce moment précis, rendant impossible la connexion sur “www.facebook.com” mais également sur le domaine sur lequel repose l’API sur laquelle repose le widget. Ce widget, présent sur de très nombreux sites, est devenu soudain impossible à charger, et la page avec. Inutile de vous dire que tous ces sites n’avaient jamais été prévenus d’une telle possibilité. Certains se demandent d’ailleurs probablement toujours pourquoi leur business a été si mauvais ce jour-là...

Bien sûr, il existe plusieurs techniques pour ne pas être affecté par les performances d’un contenu tiers, il faut juste être conscient que l’implémentation par défaut fournie par le prestataire n’est pas toujours la plus favorable (même quand on s’appelle Google ou Facebook) et tester régulièrement votre site afin de vérifier qu’aucun partenaire tiers n’est un “*SPOF*” (*Single Point Of Failure*), c’est-à-dire un élément qui à lui seul peut faire tomber votre site.

### Perte de données et conséquences sur la protection de la vie privée

La diminution de votre performance et les risques qui pèsent sur la disponibilité de votre site sont des inconvénients fâcheux mais techniques. Plus inquiétante encore est l’intrusion dans votre site d’étrangers qui n’ont qu’un intérêt : collecter des données sur vous ou vos visiteurs. Vous n’avez pas connaissance de ces ressources chargées lors d’appels issus de script tiers. Pourtant, elles peuvent voir et capturer des informations sur vos visiteurs sans votre consentement. Et la variété des informations qu’elles peuvent collecter est impressionnante. 
Prenons l’exemple du reciblage. Le reciblage consiste à afficher à un visiteur de la publicité basée sur ses précédentes actions sur Internet. Par exemple, vous visitez un site vendant des barbecues, mais êtes interrompus et vous quittez le site. Quelques minutes plus tard, un autre site affichera une publicité vous invitant à revenir sur le premier site pour acheter un barbecue. Le prestataire vous a “reciblé” sur une catégorie de produit.

Pour bénéficier de ce service, le vendeur de barbecue comme le site qui affichera la publicité ultérieurement échangent avec le partenaire de reciblage un nombre important d’informations sur l’utilisateur, son historique de navigation et les produits qu’il a consulté. Or ce prestataire de reciblage peut lui-même faire appel à des acteurs différents, qui se retrouveront de facto en possession d’informations privées sur vous. Pire, ils pourront les altérer ou les enrichir avant de les fournir eux-mêmes à d’autres entreprises, pour d’autres services. 
Et vous qui aviez peur des réseaux sociaux peu soucieux de la protection de votre vie privée ! En réalité, des milliers d’informations circulent chaque jour sur vos goûts, votre personnalité, vos relations, et vous n’avez absolument jamais souscrit à aucun de ces services tout comme vous ne pouvez pas vous y soustraire. Tout cela à cause de scripts tiers inclus dans des sites auxquels vous faites confiance...

## La confiance n’exclut pas le contrôle

Afin de vous prémunir de problèmes liés à l’inclusion de script tiers - et des appels afférents - il est nécessaire de mettre en place un certain niveau de contrôle. Suivant l’importance que vous accordez à ce point, et les moyens à votre disposition, vous opterez pour un diagnostic manuel répété ou pour une automatisation des tests de dépendance. Dans les deux cas, le processus d’analyse est le même.

### Waterfall mon amour

Nombreux sont ceux pour qui l’outil est familier sans pour autant savoir vraiment comment l’utiliser. Le *Waterfall* est une représentation des téléchargements opérés lorsqu’on visite une page, de la perspective du navigateur. Vous voyez le code HTML renvoyé par le serveur ou parfois un fournisseur de contenu et ultérieurement, le chargement des ressources (scripts, feuilles de style, images et autres médias). Pour chaque élément, vous disposez d’un découpage du temps nécessaire à son chargement : la résolution DNS, le temps nécessaire à la connexion TCP, le temps entre cette connexion et le premier octet de donnée renvoyé, et enfin le temps nécessaire à l’ensemble du chargement.

![Morceau du WaterFall du train de 13h37](waterfall-t13h37.jpg "Morceau du WaterFall du train de 13h37 (<a href="http://www.webpagetest.org/result/120610_SP_B17/1/details/#waterfall">Voir la source</a>)")

Prenons l’[exemple du train de 13h37](http://www.webpagetest.org/result/120610_SP_B17/1/details/#waterfall). Au moment où j’écris ces lignes, le train a un *Waterfall* assez simple et facile à comprendre : on y voit le temps de chargement du code HTML (1050ms), puis le chargement des ressources JS et CSS quand soudain un élément sort du lot : un .gif appartenant au domaine www.google-analytics.com. S’en suivent diverses autres ressources. Ici, l’élément étranger est facilement identifiable car il y a peu de ressources dans l’absolu : on sent qu’un soin particulier a été apporté à la réduction de leur nombre et des dépendances du site à leur égard. Il est même assez aisé de valider que l’indisponibilité éventuelle de Google Analytics n’est pas bloquante pour le site en se servant de WebPageTest et de l’option “*Block*” permettant de verrouiller un ou plusieurs éléments durant le chargement. Comme l’atteste [ce Waterfall](http://www.webpagetest.org/result/120610_99_B20/1/details/#waterfall), Google Analytics n’est pas, pour le Train, un *Single Point Of Failure*.

![Morceau du WaterFall de lexpress.fr](waterfall-lexpress.jpg "Morceau du WaterFall de lexpress.fr (<a href="http://www.webpagetest.org/result/120610_H3_BAX/1/details/#waterfall">Voir la source</a>)")

Prenons un second exemple : [le *Waterfall* de lexpress.fr](http://www.webpagetest.org/result/120610_H3_BAX/1/details/#waterfall). La problématique est différente au premier coup d’oeil. Le découpage des appels du *Waterfall* met en avant [plus de vingt-six domaines](http://www.webpagetest.org/result/120610_H3_BAX/1/domains/) différents nécessaires au rendu de la page. Soit a minima 26 résolutions DNS et 26 connexions TCP (en réalité, il y a davantage de connexions). Il suffit de bloquer un certain nombre de script tiers pour se rendre compte que la performance du site souffre de leur présence : sans Facebook, Twitter, CotePerso.com, RealMedia et Xiti, [le site gagne 2 secondes](http://www.webpagetest.org/result/120610_EV_BCN/1/details/), soit près de 25% de sa performance au *Document Complete*. Si cela confirme que le site est bien développé au sens où il ne souffre pas d’éventuels dénis de services de ces partenaires, cela indique tout de même une certaine problématique de performance. À corréler évidemment avec les résultats commerciaux car pour beaucoup de sites de Presse, la publicité via des appels tiers est la seule et unique source de revenus.

## Conclusion : il faut changer la donne

Comme vous l’aurez compris, ces appels ne sont pas que de simples lignes de Javascript. Leur impact est bien plus important qu’on veut souvent vous le faire croire et peut nuire à l’expérience de vos utilisateurs, la disponibilité de votre site ou même votre politique de collecte et de manipulation des informations concernant vos visiteurs.

Le problème de ces appels tiers est qu’il n’existe finalement aucun consensus autour de leur impact sur le Web. Chaque entreprise, si tant est qu’elle en soit consciente, réalise ses propres analyses mais il n’existe globalement pas de "Bonnes Pratiques" ou d’organismes chargés de l'établissement d’un protocole ou d’une évaluation. C’est un *no man’s land* sur lequel l’absence de contrôle laisse libre champ à des comportements dignes du *Far West*.

![Capture du tableau récapitulatif du projet P3PC](projet-p3pc.jpg "Capture du tableau récapitulatif du projet P3PC (<a href="http://stevesouders.com/p3pc/">Voir la source</a>)")

Certains commencent à organiser la contre-offensive. [Patrick Meenan](http://blog.patrickmeenan.com/), via son outil WebPageTest, est un de ces acteurs majeurs de la performance Web dans le monde, et nombreux sont les projets qui reposent sur WPT. Concernant les appels de scripts tiers, on pourra plus particulièrement souligner l’initiative remarquable de Steve Souders, auteur des excellents “*[High Performance Web Sites](http://www.amazon.fr/gp/product/0596529309/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=letraide13h3-21&linkCode=as2&camp=1642&creative=6746&creativeASIN=0596529309)*” et “*[Even Faster Web Sites](http://www.amazon.fr/gp/product/0596522304/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=letraide13h3-21&linkCode=as2&camp=1642&creative=6746&creativeASIN=0596522304)*”, qui via son [projet P3PC](http://stevesouders.com/p3pc/) donne une ébauche de ce que pourrait être une analyse systématique des performances de script tiers. Malheureusement, très peu de scripts sont aujourd’hui présents dans ce panel.

Espérons qu’un test standard émerge rapidement, et que chaque nouveau script se voit découpé, jugé, évalué non plus uniquement sur son apport commercial direct, mais également sur les risques qu’il fait encourir au site l’appelant ou au visiteur qui, sans en avoir jamais conscience, l’exécute.

**Ressources :**

- *[SPOF](http://www.webperformancetoday.com/2011/10/13/how-vulnerable-is-your-site-to-third-party-failure/)*
- *[Facebook Outage](http://blog.catchpoint.com/2012/06/01/facebook-outage-wake-up-call-for-websites/)*
