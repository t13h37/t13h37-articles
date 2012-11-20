# Les *User Agents*, c'est le mal

Jean-Bichon est un développeur Web senior aguerri, 15 ans d'expérience en Web 2.0, qui développait du HTML sous vim avant même d'avoir eu l'idée d'utiliser un éditeur graphique ; Nicolet est un développeur Web junior innocent, tout droit sorti de l'ENDGQFDW (École Nationale Des Gens Qui Font Du Web, bien sûr), débarqué depuis peu dans le petit monde tranquille de Jean-Bichon. Cette scène se passe dans tous les open spaces des boîtes à Web en 2012.

Nicolet est en train de déboguer le fin travail de Jean-Bichon, en le passant à la moulinette des navigateurs les plus exotiques pour s'assurer de son bon fonctionnement universel. Mais cela va faire deux heures que Nicolet tente de trouver une solution à cette méthode Javascript qui ne veut pas fonctionner sur Firefox 1.666 pour BeeOS (comme vous le constatez, nous sommes dans un cas typique !)

"Jean-Bichon !", crie Nicolet, "Jean-Bichon ! Je ne m'en sors pas avec cette méthode Javascript ! Que faire ?"  
"Ahah ! Cherche encore, cherche encore !", répond Jean-Bichon.  
"Mais Jean-Bichon ! Je ne fais que ça de chercher ! Ne peut-on pas juste détecter ce cas précis côté serveur, en regardant discrètement dans le User Agent ?"  
"NOOOON !"

Tout l'open space retient sa respiration. Les mouches s'arrêtent de voler. La machine à café s'arrête de couler, attendant nerveusement la suite.

"Mais…" chuchote timidement Nicolet "Mais pourquoi on ne peut pas, en fait ?"  
"Tu ne sais pas ? Ahah, il ne sait pas !"

Guillaumet baisse les yeux timidement. La machine à café laisse involontairement s'échapper une goutte. Une développeuse juste à côté lui chuchote bruyamment : "Chut !"

"Mais c'est tellement simple ! C'est tout simplement parce que tout le monde dit qu'il ne faut pas ! Ahah !"

Jean-Bichon se tournant à nouveau vers son écran, la vie de l'open space reprend son cours strictement là où elle en était restée. Frustré, Nicolet se plonge à nouveau dans son code, se jurant que lui aussi, lorsqu'il aura tout vécu, il se permettra d'émettre bruyamment des réponses insatisfaisantes à des jeunots en détresse au sujet des *User Agents*.

Mesdames, Mesdemoiselles, Messieurs, je vous souhaite la bienvenue sur cet article qui a pour but que cette scène ne se reproduise plus.


## C'est quoi un ziouzeur èdjente ?

Vous allez me demander : puisque les *User Agents* sont un instrument du mal, et que cette information est connue et reconnue, pourquoi donc l'Humanité leur a-t-elle permis de voir le jour ? La réponse est simple : les *User Agents* répondent efficacement à une problématique précise et ont une véritable valeur ajoutée pour un besoin toujours aussi courant aujourd'hui qu'il l'était dans les années 90 (et peut-être même plus).

Aujourd'hui, et depuis quelques mois/années seulement, le nombre de contextes logiciels côté client utilisés pour accéder au Web est en multiplication ; et par contextes logiciels côté client, j'entends OS et version du navigateur. Jusqu'il y a quelques années, l'équation était plutôt simple : il y avait tout plein de Windows (dont une ou deux versions étaient en permanence fortement prépondérantes sur le marché) et très peu du reste ; et il y avait tout plein d'Internet Explorer 6 ou 7 et très peu du reste. En 4 ou 5 contextes clients, vous représentiez une écrasante majorité de ce qui se passait devant les yeux de vos internautes.  
Puis, les navigateurs alternatifs ont fait une percée avec en tête Firefox, Chrome et Opera (oui oui, Opera, un peu partout sauf chez nous en France !). Et sur le plan des OS, MacOSX a fait une percée et Linux aussi (dans une moindre mesure).  
Et au-dessus de tout ça, les plateformes mobiles sont arrivées, qui sont encore plus largement diversifiées…

L'existence potentielle côté client de très, très nombreux contextes est une possibilité déjà considérée dans les protocoles Web dès leur design. C'est pourquoi, très tôt, il a été considéré qu'il fallait, lors de la réception de la requête HTTP par le serveur, que celui-ci puisse savoir quel est le contexte de l'autre côté du nuage.

![Le serveur web peut savoir quel est le User Agent](Schema1.png)

La décision a donc été prise : parmi les *headers* HTTP (ensemble de chaînes de caractères attaché à chaque requête, qui contient beaucoup d'informations sur le client, comme la langue du navigateur, les paramètres de la requête, les dates d'expiration des caches, etc.), on en trouvera un qui identifiera le contexte logiciel côté client, et il s'appellera *User Agent*. Magique !

Et jusqu'à aujourd'hui, il a toujours très bien rempli ce rôle (sauf [cas récents très particuliers](http://www.clever-age.com/veille/reactions/ipad-mini-le-debut-des-ennuis.html)) Si vous souhaitez tester si deux requêtes que vous recevez sont faites avec le même navigateur et le même OS, le fait d'utiliser le *User Agent* vous assure de pouvoir le déterminer convenablement.

Mais alors, me direz-vous, …


## … quel est donc le problème ?

Le premier problème du *User Agent* est sa lourde histoire, composée de lourds choix historiques faits par les navigateurs.

Il existe un excellent article, "*[History of the browser user-agent string](http://webaim.org/blog/user-agent-string-history/)*", par Aaron Andersen, mais pour les anglophobes voici un résumé rapide.

Au tout début, il n'y avait qu'un navigateur graphique, et ses créateurs (qui travaillaient pour le NCSA) l'avaient appelé Mosaic. C'est pourquoi un *User Agent* typique était "NCSA_Mosaic/2.0 (Windows 3.1)".  
Puis le projet Mozilla est arrivé (au passage, Mozilla = *Mosaic Killer*), et à sa sortie il a été renommé Netscape Navigator, d'où son *User Agent*, toujours fort logique : "Mozilla/1.0 (Win3.1)".  
Comme le disent les cinéphiles, « jusqu'ici tout va bien ».

Mais les développeurs Web étaient bien tristes car Netscape était arrivé avec son lot d'innovations spectaculaires et futuristes, telles que les extraordinaires *frames* ! Mosaic se retrouvait alors bien incapable de comprendre et d'interpréter ces innovations... Les développeurs Web de l'époque se sont posés la question : comment vais-je donc différencier les deux navigateurs pour leur envoyer le meilleur contenu ? Réponse évidente : les *User-Agents* ! Je vais regarder s'il commence par "Mozilla/" et seulement si c'est le cas, je lui enverrai la version moderne de mon site !

C'est dans cet environnement bipolaire qu'Internet Explorer a fait son entrée ; et comme Internet Explorer désirait absolument pouvoir afficher les versions modernes des sites, il a ironiquement décidé de choisir le *User Agent* : "Mozilla/1.22 (compatible; MSIE 2.0; Windows 95)". Nous avons donc un Internet Explorer qui fait semblant d'être un Mozilla. Hum.

Puis, pour tenter de frapper un coup décisif dans la guerre des navigateurs, Netscape a fait un choix (qu'il a regretté d'ailleurs car de retard de planning en retard de planning pour la sortie du nouveau Netscape, IE est du coup passé d'environ 50% à près de 98% de part de marché, remportant le combat pour de nombreuses années), de refondre la totalité du code source de Netscape, en la séparant en deux parties : le moteur de rendu Web (Gecko), et l'interface d'interaction. Le moteur de rendu Gecko a été distribué en *open source* et a donné naissance à plusieurs navigateurs au-delà de Firefox, notamment Camino et Seamonkey, dont les *User Agents* ressemblaient à ça :

- Mozilla/5.0 (Windows; U; Windows NT 5.1; sv-SE; rv:1.7.5) Gecko/20041108 Firefox/1.0 ;
- Mozilla/5.0 (Macintosh; U; PPC Mac OS X Mach-O; en-US; rv:1.7.2) Gecko/20040825 Camino/0.8.1 ;
- Mozilla/5.0 (Windows; U; Windows NT 5.1; de; rv:1.8.1.8) Gecko/20071008 SeaMonkey/1.0.

Nous avons donc trois navigateurs qui font tous semblant d'être Gecko (ce qu'ils sont partiellement, nous sommes d'accord), lequel fait semblant d'être Mozilla (dont il est le fils, nous sommes d'accord). Double-hum.

Oui mais voilà, avec son super-Gecko, Netscape reproduisait une deuxième fois le super-exploit historique de fournir des fonctionnalités plus modernes que son concurrent, cette fois-ci Internet Explorer. Les développeurs ont donc une nouvelle fois voulu tester le *User Agent*.

C'est dans ce contexte à nouveau bipolaire qu'une certaine petite société du nom d'Apple Computers a souhaité reprendre le code *open source* d'un moteur de rendu qui s'appelait KHTML pour construire son propre moteur de rendu WebKit sur lequel faire reposer son navigateur qui s'appelait Safari. Du coup : "Mozilla/5.0 (Macintosh; U; PPC Mac OS X; de-de) AppleWebKit/85.7 (KHTML, like Gecko) Safari/85.5".  
Nous avons donc maintenant un navigateur Safari, qui fait semblant d'être AppleWebKit (ce qu'il est partiellement, nous sommes d'accord), lequel fait semblant d'être KHTML (dont il est le fils, nous sommes toujours d'accord), mais qui fait aussi semblant d'être Gecko, lequel fait semblant d'être Mozilla. Multiple-hum.

Et Google sort Chrome : "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/525.13 (KHTML, like Gecko) Chrome/0.2.149.27 Safari/525.13".  
Nous avons donc un navigateur qui s'appelle Chrome, qui fait semblant d'être un autre navigateur qui s'appelle Safari, lequel fait semblant d'être un moteur de rendu qui s'appelle AppleWebKit, lequel fait semblant d'être un autre moteur de rendu qui s'appelle KHTML, mais qui fait aussi semblant d'être un moteur de rendu qui s'appelle Gecko, lequel fait semblant d'être un navigateur du passé qui s'appelle Mozilla.
Exponentiello-hum !

En résumé, les rebondissements historiques ont incité les navigateurs à mentir dans leurs *User Agents*, et de petit mensonge en petit mensonge, les *User Agents* sont devenu des mini-orgies de noms de navigateurs.


## De la complexité à parser une chaîne de caractères

Le problème pourrait s'arrêter là, et vous auriez déjà compris que le *User Agent* est progressivement devenu d'une fiabilité très décevante… mais, hélas, ce n'est pas tout !  
Même dans un monde alternatif où les navigateurs auraient mis autant de zèle à maintenir un *User Agent* pertinent qu'à retirer leurs préfixes propriétaires de CSS à temps (Firefox, [je regarde dans ta direction](https://bugzilla.mozilla.org/show_bug.cgi?id=693510) !), le *User Agent* n'en resterait pas moins un outil imprécis et générateur d'erreurs, de par sa condition de chaîne de caractères.  
Rappelez-vous de vos cours à la fac (ou des conseils de votre Jean-Bichon, si vous en avez un), fouiller dans des données structurées, c'est bien ! Extirper des données en parsant des chaînes de caractères, c'est mal !

Un exemple concret de catastrophe ?… Fort bien !

J'imagine que vous n'êtes pas sans savoir que la détection (le *parsing*) de *User Agent* est redevenu à la mode depuis que l'on voit la nécessité de réaliser des instances de sites séparés entre site "mobile" et site "desktop" ? (je reviendrai sur la pertinence de ce cas d'utilisation !)

Sur le plan technique, la question se pose : que dois-je parser ?

Dois-je *parser* les mots "Android", "iOS", et "WP7" ? Et pour les autres ? Je dois sans doute *parser* le mot "Mobile", non ? Il y a d'autres anciens navigateurs mobiles toujours utilisés dont le nom ne contient pas "Mobile" : je devrais donc, pour être exhaustif, *parser* aussi "WebOS" ? Et potentiellement "PalmOS" ? "Pre" ? "Pocket" ?…  
La solution amenée par la plupart des développeurs aujourd'hui est : "Ne soyons pas cheap ! Parsons tous ces mots !"

~~~ {lang="java" line="1" highlight="1"}
boolean isMobile = useragentInLowercase.matches(".*(android|ios|wp7|mobile|webos|palmos|pre|pocket).*");
~~~

Splendide ! Cas résolu !

Et sur ce, inopinément, un utilisateur sous Opera arrive sur votre site depuis un ordinateur : "Opera/9.8 (Windows NT 6.0; U; en) Presto/2.2.0"  
Votre script parse cette chaîne, et en déduit que puisqu'Opera *desktop* utilise le moteur de rendu "Presto", il est donc un Pre, et est donc mobile. Très logique.

Oh, ne riez pas ! Le problème a existé un temps sur le site du Département d'État des États-Unis d'Amérique !  
Oui, oui, nous parlons bien de ce fameux ministère américain en charge des rapports avec l'International, et donc avec les pays qui ont, eux, une forte majorité de navigateur Opera ! Les gens de ces pays-là n'avaient qu'à bien se tenir : lorsqu'ils arrivaient sur ce site avec leur ordinateur, on leur présentait un glorieux site mobile…

![Captures d'écrans desktop et mobile du site du Département d'État des États-Unis d'Amérique](Schema2.png)

Donc retenez bien : *parser* des *User Agent*, c'est parser une chaîne de caractères, et c'est très mal. J'aimerais pouvoir vous dire que le cas ci-dessus est unique, mais dans la vraie vie [ils sont multiples](http://dev.opera.com/articles/view/opera-ua-string-changes/).


## Des solutions ?

Maintenant que nous savons que le *User Agent* est votre ennemi le plus vicieux, il nous faut surtout nous demander comment l'éviter.

La réponse simple est (trop ?) simple : concentrez-vous sur de la détection *front-end*.

![Laissez le serveur web envoyer un seul contenu et concentrez-vous sur de la détection front-end](Schema3.png)

Dans un monde parfait, le serveur, lorsqu'il recevra la requête HTTP, ne s'intéressera pas du tout à ce qui se trouve dans le *User Agent*, et renverra du code *front-end* qui sera capable de détecter les capacités du navigateur.  
Du code *front-end* capable de détecter des capacités navigateurs ? Mais c'est exactement la définition de l'*Adaptive Web Design* !  
(Je me fâche tout rouge avec le premier qui me confond ça avec le *Responsive Web Design* !)

Pour le détail des techniques et méthodes d'*Adaptive Web Design* / d'amélioration progressive, je vous renvoie vers [le très complet livre du même nom](http://easy-readers.net/books/adaptive-web-design/) ; toutefois, notez que vous avez une certaine quantité d'outils clés-en-main qui vont très largement vous aider dans votre quête :

* les *media-queries*, qui ne se limitent pas à la propriété `width`, vont vous permettre de vous concentrer sur du style CSS conditionné par des caractéristiques de l'environnement d'affichage utilisé (et ça fonctionne très bien chez beaucoup de navigateurs modernes) ;
* les *support-queries* vont vous permettre de produire du style CSS conditionné par les spécifications appliquées par le navigateur : par exemple, "Si tu sais géolocaliser, alors exécute ces règles CSS" (et malheureusement, c'est plutôt très récent, donc quand ça marche c'est top, mais ça n'est pas encore très répandu) ;
* les *API*s Javascript permettent de détecter des capacités du navigateur pour conditionner l'exécution de morceaux de codes JS, et les outils comme Modernizr vous fournissent des *API*s clés-en-main encore plus utilisables.

Malheureusement, la réponse simple est tellement simple qu'elle est incomplète ; et je suis désolé si je vous l'apprends, mais le monde n'est pas parfait !

Dans les rares cas où la détection *front-end* n'est pas une solution à votre problème, il ne vous reste alors qu'une solution : tolérer, dans votre design, les faux positifs, et permettre à l'utilisateur de rattraper l'erreur.  
Par exemple, dans le cas de la redirection vers le site mobile, une solution souvent appliquée (et indispensable !) est de permettre à l'utilisateur redirigé par erreur de revenir sur le site desktop, et inversement pour l'utilisateur qui aurait dû être redirigé, mais ne l'a pas été.  
C'est d'ailleurs une solution de rattrapage qui a permis à notre cher Département d'État de sauver la face !

![Amélioration du site du Département d'État des États-Unis d'Amérique, lien depuis la version mobile vers la version desktop](Schema4.png)


### Un premier cas problématique : la redirection vers le périphérique

Déjà, il y a le cas typique, celui qui nous pose le plus problème en ce moment : le client me demande un site mobile et un site desktop. Avec une redirection, comment puis-je lui forcer un site en *Responsive Web Design*, et sauver la face du monde *front-end* ?  
Ma réponse : *BULLSHIT* !

Si vous réalisez un petit blog, ou un petit site au nombre restreint de fonctionnalités, je ne doute pas que la solution du *Responsive Web Design* soit une solution pour être élégamment *cross-platform* ; et il existe d'ailleurs une multitude de cas plus complexes où le *Responsive Web Design* reste une solution des plus satisfaisantes. Toutefois, la vérité est que les usages ne sont pas toujours les mêmes d'un type d'interaction à l'autre, et que parfois, pour des raisons fonctionnelles, vous ne voulez pas du *Responsive Web Design*.

L'exemple typique vient du livre *[Responsive Web Design](http://www.eyrolles.com/Informatique/Livre/responsive-web-design-9782212133318)* lui-même : Ethan Marcotte voulait organiser une soirée karaoke. Il a créé un site permettant aux utilisateurs sur *desktop* de consulter la date et le lieu de l'événement et de s'y inscrire, et à ceux sur smartphone de consulter l'itinéraire jusqu'à ce lieu s'ils étaient perdus ainsi que le nom de la chanson en cours pendant la soirée ; et il a créé tout ça en *Responsive Web Design*. Puis, il s'est aperçu que ses deux contextes d'interaction étaient vraiment différents : dans son cas, tout justifiait la création de deux sites différents, aux utilités différentes.

C'est un choix fonctionnel, et c'est un choix qui existe aujourd'hui parce que les appareils de mobilité ont une usabilité alternative aux ordinateurs, et que leur popularité monte en flèche. Peut-être que demain, nous inventerons un nouveau mode d'interaction (par exemple : les toilettes connectées !), et qu'il y aura alors du sens à créer des sites adaptés à ce mode d'interaction ! (par exemple : navigueriez-vous vraiment sur Facebook de la même manière depuis vos toilettes ? Oui, OK, bon, moi aussi, je le fais déjà…)

Clairement, il est possible de ne pas être d'accord et de préférer faire du *Responsive* à tout prix. Toutefois, ce qui est interdit par la loi du Web bien fait, c'est de résoudre les cas justifiant plusieurs enveloppes fonctionnelles en masquant des fonctionnalités sur certaines largeurs d'écran, [comme j'en parlais sur un certain autre article de ce même magazine](http://letrainde13h37.fr/7/accessibilite-et-responsive-un-certain-conflit-d-interet/) (oui, je m'auto-lie (parce que comme L'Oréal je le vaux bien) et comme je suis gentil, je vous ajoute même un lien plus récent sur le même sujet sur [A List Apart](http://www.alistapart.com/articles/your-content-now-mobile/)).

Bref : deux sites différents pour deux utilités différentes, c'est parfois souhaitable ; deux *devices* différents qui impliquent deux utilités différentes, il se trouve que ça arrive. Tout est permis tant qu'on laisse la possibilité à l'utilisateur d'aller où il veut sur les deux sites, bien entendu.  
Et dans ce cas (lorsqu'il est fonctionnellement justifié), et ce surtout dans le cadre de la mobilité, faire en sorte que l'utilisateur soit redirigé - avant de charger l'intégralité de la page qui ne correspond pas à son cas - reste une solution élégante qui ne peut être mise en application qu'avec ces vils *User Agents* !


### Les rares cas où le *front-end* vous abandonne

Vous souvenez-vous de ces moments, lors de cette épreuve traditionnelle qu'est l'école maternelle, où toutes les mamans étaient venues chercher leurs enfants, sauf très précisément la vôtre ?  
Eh bien sachez que parfois, être développeur Web, c'est un peu ça…  
Il peut arriver que votre confiance aveugle en ce monde magnifique qu'est le *front-end* vous amène à affronter le mépris occasionnel que le *front-end* a parfois de vous !

Par exemple, sachez que le *front-end* vous ment !  
Saviez-vous que certains téléphones, dont notamment certains *smartphones* Nokia, certains Androids pas si âgés que ça (version 2.1, notamment), et une quantité d'autres terminaux, se permettent, lorsque vous leur demandez en JS s'ils sont capables d'interpréter des *font-face*, de vous répondre "oui"... [alors qu'en fait, non](http://blog.kaelig.fr/post/33373448491/testing-font-face-support-on-mobile-and-tablet) !  
Comment alors allez-vous rédiger une amélioration progressive décente, si ces navigateurs se permettent d'agir tels des effrontés ?  
Gardez la tête froide : rappelez-vous que lorsque Chrome se faisait passer pour Gecko, les *User Agents* vous mentaient largement plus systématiquement.

Mais aussi, par exemple, sachez que le *front-end* se moque de vous !  
Et ce, pas toujours dans les interprétations côté navigateur mais aussi directement dans les spécifications !  
Connaissez-vous, par exemple, la méthode JS `canPlayType` ?  
Le fonctionnement est simple : vous prenez un élément HTML `<video>` en JS (appelons-le videoElem), et pour savoir s'il sera capable ou non de lire de l'Ogg Theora, vous lui demandez comme ceci : `videoElem.canPlayType("video/ogg")` ;  
Contrairement à vos attentes, le résultat de cette méthode n'est pas un booléen, mais une chaîne de caractères, qui prend parfois la valeur "*yes*" si vous êtes chanceux, parfois la valeur "" pour exprimer que votre élément vidéo ne saura pas s'en sortir ; mais la méthode vous exprimera aussi parfois un franc et honnête "*maybe*" !  
Vous vous imaginez, en pleine tentative d'amélioration progressive, devoir demander l'autorisation à un navigateur avant de vous engager dans une piste d'interaction, et gaillardement il vous répond "*maybe*" ?  
Et parfois, vous pouvez même tomber sur un navigateur qui se sent en veine, qui le sent bien aujourd'hui, et qui se permettra de vous taper gentiment dans le dos en vous répondant la quatrième valeur autorisée par la spécification : "*[probably](http://www.w3schools.com/tags/av_met_canplaytype.asp)*" !  
Encore une fois, gardez la tête froide ! Rappelez-vous que les *User Agents* aussi, en prétendant être chacun tous les autres, se moquaient de vous sur la base-même de leur identité…


# En conclusion, je fais quoi, moi, avec mon site ?

Les cas "*border-line*" que je vous présente dans le paragraphe précédent sont marginaux, et vous pouvez les considérer comme tels. Aussi, pour moi, il existe deux types d'attitude face à ce problème :

* la solution simple et pérenne, appliquer le lâcher-prise du Web qui consiste à accepter que vous aurez des faux positifs, et à tenter au mieux de proposer à l'utilisateur de les rattraper manuellement. Pour le cas de la détection de types de périphériques, un lien sur chaque version peut sauver la vie ; et je ne doute pas que vous trouverez des solutions simples sur mesure dans votre manière d'utiliser la détection de *font-face* ou les encodages vidéos supportés.
* la solution perfectionniste qui consiste à mettre sur pied des *server-side components*, qui s'adonnent à la détection précise d'*User Agents* pour tous les cas *border-line*.

Évidemment, cette dernière solution est largement plus coûteuse, car pour être réalisée convenablement il va vous falloir un exemplaire de tous les périphériques significatifs du marché (y compris certains marginaux, qui sont d'ailleurs souvent les plus intéressants), et il va vous falloir beaucoup, beaucoup, beaucoup de temps pour tester tous vos *server-side components* et maintenir une détection de *User Agents* qui ne produit aucun faux positif, malgré l'arrivée constante de nouveaux terminaux.

C'est toutefois la solution qu'a choisi d'appliquer la BBC, en mettant en place une équipe dédiée à un outil embarquant ces *server-side components* (au doux nom de "DEMI").

Je vous conseille vivement la lecture de l'article de Kaelig Deloumean-Prigent sur [sa résolution du cas détection de *font-face*](http://blog.kaelig.fr/post/33373448491/testing-font-face-support-on-mobile-and-tablet) ; et je vous la conseille d'autant plus fortement que c'est lui qui m'a sensibilisé à une énorme partie des informations que je viens de vous exposer (et je l'en remercie au passage !).

Dans votre cas, la solution est entièrement dépendante de vos contraintes budgétaires ou/et temporelles, mais rappelez-vous une chose : il n'est pas toujours constructif de vouloir tout contrôler sur le Web, et face à tant d'adversité il s'avère même bien souvent que le lâcher-prise reste l'attitude la plus constructive à long terme.


