#@font-face : astuces et outils pour bien l’utiliser

La déclaration CSS `@font-face` permet d’utiliser n’importe quelle police de caractères sur le web. Mais ce qui peut paraître un changement mineur dans l’apparence d’un site peut le rendre illisible pour une partie de l’audience, alourdir le poids des pages au-delà du raisonnable, voire vous coûter un procès !

Voici donc une liste de conseils, astuces et techniques pour utiliser cette possibilité sans risques et dans les règles de l’art, ainsi qu’un aperçu des utilisations alternatives de cette fonctionnalité.

## Choisir une police
Les polices apportent une touche de personnalité au texte, mais un accent peut être perçu comme charmant ou élégant, ou irritant voire même distrayant… Choisissez la police adaptée à la *personnalité* souhaitée pour le site.

Par ailleurs, les polices systèmes sont conçues pour une lisibilité optimale à l’écran ; ce n’est pas forcément le cas des polices plus audacieuses ou destinées à l’impression. Sur un titre gras et de grande taille cela ne posera pas problème, mais n’utilisez une police non standard pour le corps de texte qu’avec beaucoup de précautions.

À titre personnel, je vous recommande le “[Guide de choix typographique](http://www.amazon.fr/gp/product/2911220269/ref=as_li_ss_tl?ie=UTF8&tag=letraide13h3-21&linkCode=as2&camp=1642&creative=19458&creativeASIN=2911220269)”, publié aux Ateliers Perrousseaux : ce livre détaille l’histoire, les particularités et les usages typiques d’une soixantaine de polices classiques.

##Licence
L’un des freins à l’explosion des polices web a été la peur du piratage pour les fonderies. Heureusement, de plus en plus de polices sont maintenant gratuites, gratuites pour un usage non-commercial, ou proposées avec une licence web… Mais pas toutes !

Vérifiez donc dès le début du projet que la ou les polices retenues disposent d’une licence autorisant son usage sur le web, et que vous avez acquis cette licence (et pas seulement celle pour l’impression).

Pour certaines polices, la seule solution consiste à passer par un service en ligne. Mais chaque service a des exclusivités sur les polices proposées, et certaines polices ne sont tout bonnement pas proposées pour le web. Bon courage pour trouver le service hébergeant la police du projet… J’ai listé les services hébergeant les polices étudiées dans le Guide pratique de choix typographique dans le tableau suivant.

![Aperçu du tableau des services hébergeant les polices les plus classiques](Tableau-collaboratif-des-polices-web-hebergees.png "Aperçu du tableau (<a href="https://docs.google.com/spreadsheet/pub?key=0AieQukMuNXYxdEMxcllPUndvSjVEU3ZTRUpib2lLZ3c&output=html" title="Accéder au document complet">télécharger</a>) indiquant quels services hébergent les polices les plus classiques")

##Polices préinstallées
Si la police choisie est inclue par le système d’exploitation ou par une suite logicielle installée sur le poste, et que vous acceptez que vos visiteurs ne voient pas tous le site avec la même police, alors une option intéressante s’ouvre à vous.

Vous pouvez tout simplement indiquer le nom d’une de ces polices non standards dans la déclaration `font-family`, suivi bien sûr d’une ou plusieurs polices web-safe (celles qui sont disponibles quasiment partout), et en finissant comme toujours par un type de police (*serif* ou *sans-serif* le plus souvent). Si le visiteur possède cette police elle sera utilisée sans que vous ne vous embarrassiez avec `@font-face`, sans que vous n’ayez besoin d’acheter de licence, et sans téléchargement de fichier supplémentaire pour votre visiteur. Jackpot !

Oui, enfin, pas si simple. Il faut trouver le nom de police tel qu’il est utilisé sur les ordinateurs de vos visiteurs, et il existe des centaines de variations pour une police aussi classique qu’Helvetica. En pratique, essayez de lister le nom tel quel (“Helvetica Neue”) suivi par le nom du fichier Postscript (“HelveticaNeue”). Vous trouverez ce dernier en utilisant Font Book (livré avec Mac OS, capture ci-après) et dans le dossier Fonts sur Windows (en vue détail).

![Capture montrant le nom Postscript dans Font Book](nom-postscript-helvetica-neue-fontbook.png "Capture montrant le nom Postscript dans Font Book")

Vous devrez néanmoins tester votre site avec les polices de substitution pour éviter que l’affichage ne diffère trop. Surveillez en priorité les éléments textuels dont les dimensions influencent le positionnement d’autres éléments. Exemples : le nom du site qui vient toucher un formulaire de recherche positionné en absolu, le titre d’un billet qui passe sur 2 lignes, du texte placé sur un fond de dimensions fixes… Le bookmarklet [ffffallback](http://ffffallback.com/) permet de superposer l’affichage des 2 polices pour simplifier la comparaison.

![Capture écran du bookmarklet ffffallback en action sur le site dédié](capture-ffffallback.png "Capture écran du bookmarklet ffffallback en action sur le site dédié")

##Lissage
L’affichage d’une police dépend du système d’exploitation et du logiciel utilisé. Photoshop en particulier lisse le texte très différemment des navigateurs, et une police tout à fait normale sur votre écran peut faire pleurer vos visiteurs… Ne vous fiez pas aux maquettes, testez toujours le rendu de votre police dans plusieurs navigateurs et systèmes d’exploitation.

![Comparaison de Myriad Pro sur Mac et Windows via Web Font Specimen](comparaison-myriad-par-os.png "Comparaison de Myriad Pro sur Mac et Windows via Web Font Specimen (<a href="https://typekit.com/fonts/myriad-pro/n3/wfs" title="Accéder à Web Font Specimen" hreflang="en">Voir la source</a>)")

Pour éviter des déconvenues, désactivez le lissage et les effets de texte (ligatures, césure intelligente) de Photoshop avant d’envoyer les propositions, pour que le site final ressemble le plus possible aux maquettes validées par le client.

![Capture écran des réglages à appliquer dans Photoshop](reglages-texte-pour-web-sur-photoshop.png "Capture écran des réglages à appliquer dans Photoshop")

##1… 2… 3… 22 v’là la police !

Quand un site utilise une police particulière, il peut se produire ce que les anglophones appellent un *FOUT*, un “*Flash Of Unstyled Text*”. Kézako ? Petit jeu de rôle : que feriez-vous si vous étiez un navigateur ayant reçu le HTML et les CSS mais pas encore les fichiers de police ?

1. J’affiche la page avec les polices système. Le visiteur voit quelque chose dès que possible, mais il faut recalculer la mise en page à l’arrivée des polices ce qui peut faire sauter l’affichage.
2. J’attends d’avoir tout reçu. Suivant le poids des polices et la vitesse du réseau (et en priant pour que tous les fichiers soient disponibles), le visiteur risque de regarder une page blanche pendant un long moment.
3. J’attends quelques instants, puis je fais avec ce qui est arrivé d’ici là et je recalcule la mise en page à mesure que les polices arrivent.

Aucune solution n’est parfaite, mais les navigateurs s’orientent vers la troisième car la vitesse d’affichage d’un site est plus importante que son apparence initiale (quoi qu’en disent les graphistes, l’impact marketing des performances est indubitable).

Le *WebFont loader* (disponible sur [Typekit](http://help.typekit.com/customer/portal/articles/6787-font-events) et [Google web fonts](https://developers.google.com/webfonts/docs/webfont_loader)) permet d’avoir des règles CSS qui ne s’appliquent que quand les polices sont chargées, ce qui peut être utile quand les polices de substitution ont des métriques très différentes, ou pour remplacer un texte par une image si vous y tenez. A vous de voir s’il est indispensable de pouvoir contrôler cette situation en CSS, et si un fichier JavaScript de plus n’alourdit pas le chargement et l’exécution de la page pour rien.

##Poids des polices

Un fichier de police pèse lourd, très lourd. D’une police à l’autre, on peut aller jusqu’à des centaines de ko pour un fichier ! Et rappelez-vous que chaque corps (gras, italique, gras et italique, condensé, etc.) représente un fichier distinct.

![Poids des polices sur une page du site Smashing Magazine](font-weight-in-chrome-inspector-on-smashing-magazine.png "Poids des polices sur une page du site Smashing Magazine")

Cette capture montre que les polices utilisées sur Smashing Magazine ajoutent 200ko au poids total de la page pour un navigateur supportant le format optimisé WOFF, et nécessitent 5 requêtes HTTP distinctes.

Une optimisation possible pour les sites en anglais consiste à supprimer les caractères accentués, mais c’est malheureusement impossible en français. Vous pouvez en revanche alléger vos fichiers en éliminant les accents qui ne risquent pas d’être utilisés sur votre site (les accents exotiques des langues slaves par exemple) grâce au site [http://www.subsetter.com/](http://www.subsetter.com/) —voire retirer les ligatures qui sont encore très peu supportées par les navigateurs, avec l’accord du graphiste.

![Aperçu de l’outil Subsetter de fontfont](fontfont-subsetter-etape-2.png "Aperçu de l’outil Subsetter de fontfont")

Pour éviter que le navigateur ne re-télécharge une police à chaque chargement de page, et même lui éviter de vérifier si sa version en cache est encore à jour, voici quelques règles pour `.htaccess` indiquant aux navigateurs (et *proxies* intermédiaires) une durée de validité des fichiers de police.

~~~ {lang="apache" line="1"}
ExpiresActive on
# Configuration des durees de validite des fichiers de police
ExpiresByType application/vnd.ms-fontobject "access plus 1 month"
ExpiresByType font/truetype         	"access plus 1 month"
ExpiresByType font/opentype         	"access plus 1 month"
ExpiresByType application/x-font-woff   "access plus 1 month"
~~~

##Utilisation

*Vous êtes encore là ? Alors accrochez-vous, ça devient tordu…*

Pour assigner une police en CSS, il faut passer par `font-family` (ou la syntaxe raccourcie `font`). N’oubliez pas d’inclure une police standard et un type (`serif` ou `sans-serif`) en fin de déclaration pour que le site s’affiche lisiblement en attendant que la police soit téléchargée.

~~~ {lang="css" line="1"}
h1, h2 {
    font-family: MyWebFont, "Futura PT", Futura, "Trebuchet MS", Arial, sans-serif;
}
~~~

Les formats normal, gras, italique, et gras italique sont autant de fichiers séparés, vous devrez donc indiquer l’adresse de chaque combinaison utilisée. Pour simplifier l’utilisation de cette police dans la CSS, déclarez le même nom de police et indiquez graisse et style dans chaque déclaration `@font-face`.

~~~ {lang="css" line="1"}
@font-face {
	font-family: 'MyWebFont';
	src: url('webfont.eot');
	src: url('webfont.eot?#iefix') format('embedded-opentype'),
	url('webfont.woff') format('woff'),
	url('webfont.ttf') format('truetype');
font-weight: normal;
font-style: normal;
}
@font-face {
	font-family: 'MyWebFont';
	src: url('webfont_bold.eot');
	src: url('webfont_bold.eot?#iefix') format('embedded-opentype'),
		url('webfont_bold.woff') format('woff'),
		url('webfont_bold.ttf') format('truetype');
font-weight: bold;
font-style: normal;
}
~~~

Outre qu’il est plus simple de retenir un seul nom de police, le navigateur ne simulera pas le gras et l’italique, et la police de substitution (si elle est utilisée) s’affichera avec la graisse et le style demandé.

Source : [Simplifiez vos CSS en déclarant graisse et style dans @font-face](http://www.456bereastreet.com/archive/201012/font-face_tip_define_font-weight_and_font-style_to_keep_your_css_simple/), de Roger Johansson

Je parlais de polices préinstallées un peu plus tôt, vous pouvez dire au navigateur qu’il ne doit télécharger la police que s’il ne la trouve pas sur le poste. Pour cela, ajoutez `local('nom-local.extension')` juste avant `url()`. Ici encore, il faut utiliser le nom complet et le nom Postscript.

Certaines polices sont proposées par différentes fonderies sous le même nom mais avec des mesures différentes. C’est rare, mais suffisamment angoissant pour que certains cherchent à s’en prémunir. Pour cela, il suffit d’indiquer au navigateur un fichier local avec un nom impossible (un smiley par exemple) : ne trouvant aucun fichier de ce nom, il se rabattra forcément sur le fichier à télécharger. Dans ces cas-là, la syntaxe sera :

~~~ {lang="css" line="1"}
@font-face {
	font-family: 'MyWebFont';
	src: url('webfont.eot');
	src: src: local('☺'),
		url('webfont.eot?#iefix') format('embedded-opentype'),
	url('webfont.woff') format('woff'),
	url('webfont.ttf') format('truetype');
font-weight: normal;
font-style: normal;
}
~~~

##Format(s)

Chaque navigateur et système d’exploitation nécessite un format de police particulier. Vous ne disposerez souvent que du format de votre système, ou de celui du graphiste. Heureusement, FontSquirrel propose un convertisseur en ligne gratuit pour obtenir les fichiers dans tous les formats nécessaires, en optimisant le poids, et le code CSS qui va bien dans la foulée.


![Aperçu de l’outil @font-face kit generator de Font Squirrel](fontsquirrel-font-face-generator1.png "Aperçu de l’outil @font-face kit generator de <a href="http://www.fontsquirrel.com/fontface/generator" title="Accéder à FontSquirrel" hreflang="en">Font Squirrel</a>")

Comme rappelé en rouge sur l’outil, n’utilisez que des polices pour lesquelles vous avez acquis la licence nécessaire !

Ouvrez ensuite le fichier CSS du site et collez le code indiqué par l’outil de FontSquirrel. Il devrait ressembler au code indiqué ci-après.

Les développeurs de FontSpring, aidés par la communauté, ont écrit, réécrit et testé dans tous les sens pour trouver la syntaxe la plus courte et la plus compatible à la fois (comme d’habitude, Internet Explorer nous fait des misères). Voici ce qu’ils préconisent depuis avril 2011 :

~~~ {lang="css" line="1"}
@font-face {
	font-family: 'MyWebFont';
	src: url('webfont.eot'); /* IE9 Compat Modes */
	src: url('webfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
	url('webfont.woff') format('woff'), /* Modern Browsers */
	url('webfont.ttf')  format('truetype'); /* Safari, Android, iOS */
}
~~~

Note : Il est possible de déclarer plusieurs sources (en indiquant l’URL), mais le parseur d’IE ne le gère pas, le code `?#iefix` sert donc à lui masquer les sources alternatives (en lui faisant croire qu’il s’agit d’un fragment d’URL non significatif).

Dans un avenir relativement proche, [le format WOFF sera supporté par la majorité des navigateurs les plus utilisés](http://caniuse.com/#search=woff), il n’y aura plus à s’encombrer de formats exotiques sauf à vouloir à tout prix supporter les vieux navigateurs (IE inférieur à 9 et WebKit sur Android).

##Configuration du serveur

Encore un point à surveiller : le type MIME. Certains serveurs refusent de servir les fichiers de polices car l’extension leur est inconnue, IIS en particulier. Vérifiez donc que chaque fichier est correctement renvoyé par le serveur en tapant l’adresse de chaque fichier dans un navigateur. En cas de souci, voici comment configurer les différents différents serveurs du marché.

###Apache

Mettre les règles suivantes dans le fichier `.htaccess` (ou mieux, dans la configuration des hôtes si vous y avez accès).

~~~ {lang="apache" line="1"}
# Configuration de type MIME pour les polices
AddType application/vnd.ms-fontobject eot
AddType application/x-font-ttf        ttf ttc
AddType font/opentype                 otf
AddType application/x-font-woff       woff
~~~

###Nginx

Ouvrir le fichier `mime.types` et y ajouter la configuration suivante :

~~~ {lang="text" line="1"}
application/vnd.ms-fontobject     	eot;
application/x-font-ttf            	ttf;
font/opentype                     	otf;
font/x-woff                       	woff;
~~~

###Lighttpd (Lighty)

Ouvrir le fichier `lighttpd.conf` et chercher la section `mimetype.assign` pour y inclure la configuration suivante :

~~~ {lang="text" line="1"}
application/vnd.bw-fontobject        eot
application/x-font-ttf               ttf
font/opentype                        otf
application/x-font-woff              woff
~~~

###IIS

1. Ouvrir le gestionnaire IIS
2. Dans l’onglet IIS, ouvrir “Configuration des types MIME”
3. Dans “Actions”, cliquer sur “Ajouter…”
4. Saisir `.otf` comme extension, et `application/octet-stream` dans le champ Type MIME puis valider
5. Recommencer avec l’extension `.woff`, à nouveau mettre `application/octet-stream` dans le champ Type MIME et valider

Les extensions `.ttf` et `.eot` devraient être déjà configurées, sinon répétez la manœuvre.

###Ressources sur domaine tiers

Si le domaine utilisant les polices n’est pas celui qui les héberge (sous-domaine sans cookies ou CDN par exemple), il faut l’autoriser spécifiquement via l’en-tête `Access-Control-Allow-Origin`. Sans cet en-tête ou s’il n’est pas configuré pour autoriser la requête, certains navigateurs refusent de récupérer les polices. Il arrive également qu’il soit supprimé par un pare-feu mal configuré, d’où l’importance d’indiquer des polices de substitution adaptées.

Pour indiquer que d’autres domaines sont autorisés à utiliser les polices hébergées par un serveur, modifiez le nom de domaine du code suivant et ajoutez-le dans le fichier `.htaccess` ou dans la configuration de l’hôte virtuel :

~~~ {lang="apache"}
Header add Access-Control-Allow-Origin "http://www.example.org"
~~~

##Autres usages possibles

###Substitution de caractères

Nous l’avons vu, il est possible de retirer des caractères d’une police. En l’associant au mécanisme de substitution des polices définies en CSS (si “Mapolice” n’est pas trouvée, rabats-toi sur “Helvetica”, à défaut sur une `sans-serif`) et à [unicode-range](http://www.w3.org/TR/css3-fonts/#unicode-range-desc) (qui indique quels caractères doivent être pris dans une police donnée), il est possible d’utiliser une police uniquement pour un certain nombre de caractères. Un article de *24 ways* explique en détail [comment afficher les esperluettes dans une police dans un texte utilisant une autre police](http://24ways.org/2011/unicode-range).

###Polices d’icônes

On commence à voir apparaître des polices d’icônes, qui sont finalement des sprites d’images vectorielles. Il est possible d’appliquer à ces icônes tout ce qui peut s’appliquer à du texte via CSS : taille, couleur, ombre portée, et CSS3 nous promet encore plus de possibilités (`text-stroke`, `background-clip`).

Chris Coyer a mis en place une [démo montrant les avantages de cette technique](http://css-tricks.com/examples/IconFont/). Un autre article de *24 ways* montre [comment utiliser les attributs arbitraires pour afficher des pictogrammes](http://24ways.org/2011/displaying-icons-with-fonts-and-data-attributes) pris dans une police d’icônes.

Attention, comme le souligne Florent Verschelde [l’accessibilité des polices d’icônes n’est pas garantie](http://fvsch.com/code/icon-font-a11y/) et vous introduisez une dépendance : si le navigateur ne supporte pas les *webfonts* ou que le fichier ne se charge pas correctement, le site ou l’application peut devenir inutilisable.

##Conclusion

Vous voilà parés pour donner à vos sites la personnalité qu’ils méritent, en déjouant les pièges tendus par les navigateurs et les serveurs, et en optimisant le temps de chargement du site. Sacré programme !

Mais sur le web tout fini par être détourné de son usage premier. On trouve une [typographie dont les ligatures correspondent aux smileys et autres pictogrammes](https://www.fontfont.com/fonts/piclig), une autre permettant de [générer des graphiques](http://www.behance.net/gallery/FF-Chartwell/4001387). Impossible de dire aujourd'hui jusqu'où on peut aller… Peut-être ouvrirez-vous la voie pour un nouveau détournement créatif de cette technologie ? <del datetime="2012-05-31T08:18:31+00:00">Si ça se trouve, il y a peut-être un marché pour les polices dont les ligatures correspondent aux emoticons et autres smileys…</del> A vous d’explorer !

*(Article mis à jour le 31 mai 2012 pour intégrer les liens vers PicLig et ChartWell)*

##Quelques liens pour prolonger

###En français

* [Historique et support navigateur d’@font-face](http://www.alsacreations.com/astuce/lire/630-fonte-personnalisee-site-web.html)
* [Un avis sur l’avènement des *webfonts*](http://typographisme.net/post/Un-avis-sur-@font-face)
* [Informations sur l’utilisation des *webfonts* et avis sur Typekit](http://vincent.bernat.im/fr/blog/2011-typekit.html)
* [Forcer le lissage de texte via CSS sur Mac et Windows](http://darklg.me/2012/03/font-face-avec-anti-aliasing-windows/)

###En anglais

* [Polices installées par OS et suite applicative](http://media.24ways.org/2007/17/fontmatrix.html) et [Comment s’appuyer sur les polices installées](http://24ways.org/2007/increase-your-font-stacks-with-font-matrix)
* [Polices disponibles sur iOS](http://iosfonts.com/) (sur Android, il n’y a qu’une police avec empattements, une sans, et une police à châsse fixe)
* [Listes de substitution pour polices courantes](http://cssfontstack.com/)
* [Noms complets et Postscript de polices courantes](http://blog.webink.com/p-s-i-love-you-including-postscript-font-names-in-your-font-stacks/)
* [Les différents formats de polices](http://www.smashingmagazine.com/2011/03/02/the-font-face-rule-revisited-and-useful-tricks/)
* [Comment on en est arrivé à la syntaxe @font-face actuelle](http://paulirish.com/2009/bulletproof-font-face-implementation-syntax/)
* [Pourquoi déclarer la graisse et le style en même temps que la source d’une police](http://www.456bereastreet.com/archive/201012/font-face_tip_define_font-weight_and_font-style_to_keep_your_css_simple/)
* [Etude des différentes solutions et explications du FOUT en vidéo](http://www.artzstudio.com/2012/02/web-font-performance-weighing-fontface-options-and-alternatives/)
* [Evolution des techniques anti-FOUT](http://paulirish.com/2009/fighting-the-font-face-fout/)
* [Gestion des en-têtes pour le chargement de polices hébergées par des tiers](http://sixrevisions.com/css/font-face-web-fonts-issues/)
* [Différence de rendu des polices sur Mac et Windows](http://www.codinghorror.com/blog/2007/06/font-rendering-respecting-the-pixel-grid.html)
* [Liste d’outils sur les *webfonts* et polices d’icônes](http://anselm-hannemann.com/blog/special-roundup-1-new-webfont-technologies-and-tools.html)
* [Comparaison des différents services d’hébergement de polices web](http://www.smashingmagazine.com/2010/10/20/review-of-popular-web-font-embedding-services/)
* [HTML5 Boilerplate, avec exemples d’utilisation en CSS et de configuration htaccess](http://html5boilerplate.com/)
