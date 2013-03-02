# L’accessibilité et le responsive : un certain conflit d’intérêt ?

Si vous vous considérez webdesigner/intégrateur au top de votre art, vous êtes sans doute habitué à contempler les constantes nouvelles tendances que l'on voit défiler dans nos métiers. Évidemment, j'imagine que vous ne vous autorisez pas à embrasser ces nouvelles tendances sans en remettre en cause les impacts sur les axes habituels de la qualité web (que ce soit par les dégradations apportées par la technologie en elle-même, ou parce que nous en sommes encore au stade de peaufinage des bonnes pratiques).

Dans tous les cas, la "mode" du *Responsive Web Design* ne peut pas avoir échappé à votre radar, et vous vous êtes peut-être même trouvés en situation de tenter d'en décortiquer les usages pour vous faire un avis critique. Vous avez entendu à droite et à gauche "Le *responsive*, ça fait mal aux performances !", alors vous avez peut-être décidé que le responsive, c'est bien, mais c'est sans doute mal aussi un peu parfois !

Aujourd’hui je vais aller trifouiller dans une autre de ces directions, et vous montrer comment le responsive (ou en tout cas, l’utilisation balbutiante qu’on en fait), ça peut aussi parfois faire mal à l'accessibilité !

## L’accessibilité : restons pragmatiques !

À tous ceux qui osent dire que l'expertise en accessibilité est souvent un sujet de puriste, je répondrais… “Bon, pas faux”. Mais au quotidien, vous serez d'accord, votre purisme dépendra du pragmatisme que vous mettrez dans la réalisation de votre projet.

Disons qu'une définition qui me semble pragmatique et efficace pour l'application de l'accessibilité sur des vrais projets serait : "effectuer un maximum **raisonnable** d'améliorations fines permettant à certaines minorités **raisonnables** d'utilisateurs d'avoir accès d'une manière ou d'une autre à tous les contenus et tous les services **raisonnablement** utiles de votre site". Et par minorité "raisonnable", j'entends : dont la taille vous semble suffisamment intéressante pour valoir le coût de l'effort de réalisation et l'effort de maintenance amené par cette amélioration.

En gros, et en honteusement stéréotypé : en vrai projet, quand vous allez devoir choisir entre 2 heures de développement pour rendre un service indispensable de votre site accessible à 5 % de vos utilisateurs, ou 3 jours de développement pour rendre un service que vous jugez peu essentiel accessible à 0,001 % de vos utilisateurs, le choix sera bien vite fait. Et, sur des échelles moins stéréotypées, les opportunités de faire ce type de choix sont presque quotidiennes sur un projet en cours.

![Niveaux d'accessibilité](niveaux_d_accessibilite.png "Niveaux d'accessibilité")

Je n'invente ici rien de neuf avec cette définition, je dis juste que l'accessibilité, c'est du pragmatisme, et je suis loin d'être le premier ! Je me sentais juste pousser l'envie de la poser là quelque part avant de passer à la suite…

## La fureur du "Responsive"

Définition 2, plus évidente cette fois-ci : *Responsive Web Design* = "design de site web dont l'affichage sera **conditionné par la largeur d'écran ou d'affichage**". Si vous n'êtes pas d'accord, [plus de détails s'achètent très bien, distribués par Eyrolles en français](http://www.amazon.fr/Responsive-Web-design-Ethan-Marcotte/dp/2212133316/ref=sr_1_1?ie=UTF8&qid=1340298616&sr=8-1).

Ensuite, lorsque l'on parle de design *responsive*, plusieurs très mauvaises questions se posent !
Notamment : "Maintenant que j'ai fait tout mon design *desktop*, comment est-ce que je vais compresser tout ça pour le faire rentrer sur une page mobile ?" Hou, la mauvaise question…

La réponse habituelle étant : "Bon, mon utilisateur mobile, on va dire qu'il a pas besoin de telle ou telle fonctionnalité qui prend beaucoup de place, hein…"

Ahem.

La confusion est la même qu'entre "*responsive*" et "*adaptive*". Le fait de considérer que l'utilisateur à largeur d'écran mobile (= qui a peu de place) est en mouvement / n'a pas le temps / se contentera de l'information et du service les plus simples, est légèrement borgne : **vous oubliez votre utilisateur qui, assis sur son canapé, sort son smartphone en ayant plein de temps, un bon WiFi**, et potentiellement une forte envie d'utiliser cette fameuse fonctionnalité que vous avez estampillée de "desktop".

Vous allez me dire : "Oui mais, il y a certaines fonctionnalités qui sont techniquement incompatibles avec certains terminaux !" Et auquel cas, je vous dirai que l'adaptation d'un design aux **capacités** du navigateur, **c'est justement la définition de “l'*Adaptive Web Design*"**. Et la différence est de taille : bien évidemment, ce qui a démarré votre réflexion sur la suppression de cette fameuse fonctionnalité qui ne fonctionnera pas sur certains terminaux, **ce n'est pas votre tentative de gagner de la place, hein ?** Non, non, surtout pas !

Donc : sacrifier une fonctionnalité sur l'autel de l'*Adaptive Web Design* = je suis 100 % d'accord ! Si c'est fait correctement, vous débarrassez l'utilisateur de ce à quoi il ne peut de toute façon pas avoir accès !
Par contre : sacrifier une fonctionnalité sur l'autel du *Responsive Web Design* (et donc, dans l'unique objectif de gagner de la place sur la largeur d’écran) = hmmm…

## Et donc, l’accessibilité ?

La raison pour laquelle il nous faut trouver des meilleures pratiques tient dans la définition de votre utilisateur-sur-canapé, celui qui sort son *smartphone* avec du temps et du WiFi. Je parle en connaissance de cause, je suis souvent moi-même un utilisateur-sur-canapé ; et je suis d’ailleurs convaincu qu'une grande quantité de designers prenant ce même type de libertés font aussi parfois partie du club.

Du coup, ne laissez plus un designer dire qu'il "pense que cette fonctionnalité n'est pas pertinente pour l'utilisateur mobile tel qu'il l'imagine", et dans une phrase suivante, qu'il "prête une attention pragmatique à l'accessibilité" ; à la place, prenez délicatement ce nouveau graphique, et tapez-lui sur le sommet du crâne avec !

![Niveaux d'accessibilité, la suite](niveaux_d_accessibilite-2.png "Niveaux d'accessibilité, la suite")

## Des gens bouuuuuuhh !

Les exemples de mauvaise utilisation du *responsive* en ce sens sont foison sur le Web, surtout sur des sites dont la vocation est de proposer un nombre élevé de fonctionnalités (les sites de contenus ont tendance à mieux s’en tirer, juste en réorganisant leur mise en page).

Par exemple, si vous faites un tour sur le site de vente de T-shirts [United Pixelworkers](http://www.unitedpixelworkers.com/) sur un écran suffisamment large, vous serez bien aise de découvrir que vous avez la possibilité de vous tenir au courant par une inscription à leur *newsletter*… que vous verrez totalement disparaître en version mobile, le constructeur ayant préféré se focaliser uniquement sur les fonctionnalités e-commerce et de contact direct.
Si votre ami vous conseille les bons plans de *United Pixelworkers* au détour d’une conversation de bar, et que vous souhaitiez vous inscrire immédiatement depuis votre *smartphone*… vous repasserez donc demain !!!

![Aperçu du site United Pixelworkers, version desktop](pixelworkers-desktop1.png "La colonne de gauche du site <a href="http://www.unitedpixelworkers.com/" hreflang="en">United Pixelworkers] en version <em>desktop</em>. Regardez avec intérêt cette boîte d’inscription <em>newsletter</em>, parce que si vous êtes sur un <em>smartphone</em>, vous ne la trouverez pas sur le site !")

De manière similaire, le site [Remodelista](http://remodelista.com/) propose une quantité de services dans son *footer*… qui est totalement zappée en version mobile !
Vous remarquerez volontiers que l’inscription <emlang="en">newsletter*, décidément considérée superflue par les sites e-commerce, fait à nouveau partie des heureux gagnants.

![Aperçu du site Remodelista, version desktop](modelista-desktop.png "Abracadabra, ce <em>footer</em> va disparaître ! Et hop !")

Enfin, puisque je me sens d’humeur taquine, le site <a href="http://www.google.com/news">Google News] propose lui aussi son inaccessibilité de services (oui, j’ose !) :

![Aperçu du site Google News, version desktop](google-news-desktop.png "De bien belles fonctionnalités encadrées en rouge : “Recent”, “Nouvelles géolocalisées”, et “Editors’ Picks”…")

![Aperçu du site Google News, version tablette](google-news-tablet.png "… introuvables en version tablette et mobile !")

Ainsi, si vous étiez intéressé par les nouvelles géolocalisées de Google News, mais êtes dans les transports en commun avec votre *smartphone*… attendez patiemment que l’envie vous passe !

## Des solutions ? Des bonnes pratiques ?

Heureusement, rien n’est perdu : si une fonctionnalité prend beaucoup trop de place à vos yeux pour une certaine version, rien ne vous empêche tout simplement d'**en affaiblir l'affordance tout en la laissant accessible** ; et il existe toute une quantité d’astuces possibles, qui vont parfois au-delà de la variation de la taille des éléments.

### La solution la plus simplissime : une autre page !

Le site “<a href="http://loveandluxesf.com/">Love & Luxe]”, par exemple, part d’un problème similaire : sa zone de contact (contenant horaires d’ouverture, adresse postale, téléphone, …) disparaît mystérieusement lorsqu’un bloc à sa droite en version *desktop* vient se positionner au-dessous en version tablette :

![Aperçu du site Love &amp; Luxe, version destkop](love-luxe-destkop.png "Deux colonnes de gauche en version <em>desktop</em>, et…")

![Aperçu du site Love &amp; Luxe, version tablette](love-luxe-tablet.png "… plus qu’une seule en version tablette, avec des morceaux disparus entre temps.")

La solution est la plus simple qui soit : si l’utilisateur mobile/tablette va dans la section “*About*”, il retrouvera toutes les informations disparues, directement dans le corps de page, disponible pour toutes les versions.

![Aperçu de la solution adoptée par le site Love &amp; Luxe, version tablette](love-luxe-tablet-solution.png "Un clic plus loin… et tout est là !")

Évidemment, le contenu n’est donc pas autant mis en avant qu’en version *desktop*, mais l’utilisateur mobile **y a tout de même accès s’il le souhaite**, même si l’affordance du contenu est dramatiquement diminuée (il faut quand même penser à aller chercher sur le “*About*”…). L’information est disponible d’une manière ou d’une autre : c’est là toute la définition de l’accessibilité !!
Vous me ferez remarquer bien évidemment qu’en version *desktop*, ce contenu est donc dupliqué en deux endroits de deux affordances différentes. Soit ! Heureusement donc qu’il existe d’autres solutions si celle-ci vous embarrasse…

### Affaiblissement du contenu sur la même page : enterrement en bas de page

C’est un besoin typique pour les menus de navigation : on les aime imposants en haut de page sur les versions *desktop*, et discrets en bas de page sur les versions mobiles. À cela, le site de la [George Mason University School of Law](http://www.law.gmu.edu/) répond : et alors, pourquoi pas !

![Aperçu de l'entête du site George Mason University School of Law, version desktop](mason-desktop.png "Une navigation complète sur le desktop…")

![Aperçu de l'entête du site George Mason University School of Law, version mobile](mason-mobile-bottom.png "… que l’on retrouve entière en bas de page en version mobile, et comble de l’élégance…")

![Aperçu de l'entête du site George Mason University School of Lax, version mobile](mason-mobile-top.png "… un lien (encadré en rouge) en haut de page est en réalité une ancre vers le menu de bas de page !")

Pour accomplir ce tour de force technique, il existe des outils ayant pour vocation de ne pas dupliquer le code HTML (par exemple l’outil [CSS3 flexbox](http://dev.w3.org/csswg/css3-flexbox/), qui est très bien expliqué [en anglais sur Smashing Magazine](http://coding.smashingmagazine.com/2011/09/19/css3-flexible-box-layout-explained/)), mais aucun de ces outils n’est véritablement mature et utilisable aujourd’hui en production. Sur ce site, l’intégrateur utilise une astuce : le menu est en bas de flux HTML, et est positionné en absolu en haut de page en version desktop. Il existe notamment une autre facétie [où l’on utilise illégalement les propriétés des légendes de tableaux](http://jsfiddle.net/rudyrigot/B8ewD/) ; mais il faudra accepter que parfois, vous n’aurez pas d’autre solution que de dupliquer honteusement !

### Affaiblissement du contenu sur la même page : une petite aide de monsieur Javascript ?

À partir de la même problématique de menu, le site [Personnel de Santé](http://personneldesante.fr), appartenant aux assurances MACSF apporte une autre réponse : le menu, volumineux, est en version “dépliable au clic” pour les largeurs réduites, permettant de conserver un accès aux sous-rubriques.

![Aperçu de l'entête du site Personnel de Santé, version desktop](hospi-menu-desktop.png "En version <em>desktop</em>, les deux niveaux de navigation du site prennent beaucoup de place…")

![Aperçu de l'entête du site Personnel de Santé, version mobile](hospi-menu-mobile.png "… réduite au minimum en version mobile ! Tout est là : le bouton “Menu” affiche le premier niveau, et le bouton au titre de la rubrique de niveau 1 affiche le deuxième niveau.")

Ici, l’intégrateur a fait le choix de ne pas utiliser d’astuce, et de simplement dupliquer le code HTML, remarquant que la perte liée à cette duplication était très légère (343 octets avant GZip, pour le cas de la page ci-dessus). Une seule des deux versions sera affichée simultanément grâce au CSS, et la perte de performance est excusable.
(si vous n’êtes pas d’accord, vous pouvez <a href="http://twitter.com/htmlzg">aller le taquiner], puisque l’intégrateur en question n’est autre que Vincent Valentin, qui avait d’ailleurs co-signé [l’article à la Une de la première édition du train de 13h37](http://letrainde13h37.fr/1/pour-ou-contre-html-5-en-production/) !)

### Un combo pour la route : autre page + Javascript

Sur le même site <a href="http://personneldesante.fr">Personnel de santé], on trouve un autre cas intéressant puisque, de la même manière que pour certains de nos contre-exemples, le footer perd du contenu en passant en version mobile.

![Aperçu du footer du site Personnel de Santé, version tablette](hospi-footer-tablet.png "Tout le plan de site est disponible en version desktop + tablette…")

![Aperçu du footer du site Personnel de Santé, version mobile](hospi-footer-mobile.png "… dont un niveau disparaît en version mobile !")

Ici, la perte n’a pas été jugée très gênante, puisqu’en un clic vers l’une de ces rubriques de niveau 1, on se retrouve, au chargement de la page, sur les menus “dépliables” décrits ci-dessus, lesquels une fois dépliés retrouvent toute l’information disparue. Toute l’information est donc bien accessible !

Pour être plus visuel, le parcours d’un utilisateur qui regarde le *footer* et veut atteindre une sous-rubrique ressemble à ça :

![Aperçu du parcours d'un utilisateur du footer du site Personnel de Santé version mobile](hospi-footer-menu-ouvert-mobile.png "Aperçu du parcours d'un utilisateur du <em>footer</em> du site Personnel de Santé version mobile")

Vous reconnaîtrez que le parcours de l’utilisateur mobile est plus fastidieux : l’affordance est effectivement diminuée, tout en conservant un parcours ergonomiquement logique. Mais avant tout : les liens initiaux ont disparu, mais les contenus restent toujours tous accessibles, pour toutes les versions.

### Et quand rien ne va plus ?

Dans le cas malheureux où j’arrive trop tard et où votre design responsive pas fabuleusement accessible est déjà en ligne, il y a toujours le bon vieil échappatoire que j'aime appeler le "***coward switch***" : un petit lien "Version desktop" peut s'ajouter en pied de page pour désactiver le code CSS contenu dans les *media-queries*. Une méthode technique sûre et simple consiste à recharger la page, mais avec seulement le lien d’un fichier CSS ne contenant que les règles pertinentes pour le desktop (opération également surchargeable en Javascript pour plus de fluidité).
Ça prend très peu de temps à réaliser, et même si ce n’est pas l’idéal (rien ne vaut une vraie conception bien faite !), ça a pour avantage de fonctionner pour tous les cas. Votre utilisateur retrouve alors tous ses contenus et services disparus, qui ne se trouvent alors jamais bien loin, puisqu’ils sont toujours à peine à un clic de là…

## En conclusion…

Vous en conviendrez, le Web est un domaine où trouver la meilleure pratique pour un cas particulier est à la fois continuellement passionnant et très fastidieux. Et comme pour toute “bonne pratique”, rien ne s’applique de manière manichéenne, et il faut savoir parfois outrepasser les conseils pour mieux servir l’utilisateur et la qualité Web.
Mon discours ici n’échappe pas à la règle : il peut être de bon ton de remettre en question mon propos dans certains cas. Toutefois, je considérerai avoir atteint mon but si, à la conception de votre prochain site *responsive*, vous vous poserez, comme tout passionné Web qui se respecte, la question de l’accessibilité de vos contenus et de vos services ainsi que celle de votre connaissance véritable (ou non) du profil-type de votre utilisateur mobile.

En appliquant les solutions simples exposées dans cet article, ou en trouvant vous-même les astuces qui rendent vos contenus et services accessibles en jouant sur leur affordance, vous prenez le parti éclairé de donner à votre utilisateur toute accessibilité s'il le souhaite. Ainsi, quelles que soient les circonstances de connexion de l’utilisateur qui tombe dans vos filets, **il ne sera pas prisonnier d'une vision potentiellement biaisée qu'un designer aura eu de lui**, et vous l’aurez compris : c’est ça, aussi, l’accessibilité !