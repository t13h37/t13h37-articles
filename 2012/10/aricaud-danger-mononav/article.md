# Tu te tires une balle dans le pied

Comment, en voulant créer la meilleure expérience possible, les travailleurs du
Web sont en fait en train de limiter le champ des possibles. Celui qui ne
connaît pas l'histoire est condamné à la revivre. Remontons donc un peu dans le
temps pour voir ce qui nous attend…

## Le mieux est l'ennemi du bien

<blockquote class="speaker1">
Ça y est, ce nouveau site est fini. J'en suis
fier, on a bien intégré la version mobile. En plus, j'ai évité d'utiliser des
images grâce aux dégradés CSS, j'ai pu faire de jolis titres avec [-webkit-
mask](https://developer.mozilla.org/en-US/docs/CSS/-webkit-mask), et les images
sont magnifiques avec leur subtil effet de réflexion, en particulier sur les
écrans _Retina_. Tout ça est stocké dans une base WebSQL sur le client pour une
meilleure réactivité, et puis j'ai rajouté quelques "_gestures_". Y a pas à
dire, j'en suis bien fier de ce projet.
</blockquote>

<blockquote class="speaker1">
Trois mois plus tard, je reviens tranquillement
des fêtes de fin d'année. C'était sympa de revoir la famille et puis Brice avait
organisé un sacré réveillon ! Par contre, le chef a dû passer de mauvaises
vacances pour envoyer un mail aussi enflammé dès le lundi, et nous convoquer
dans son bureau. Il est furieux, notre site vieux de trois mois ne fonctionne
pas sur les tablettes Microsoft qui se sont très bien vendues comme cadeau de
Noël.
</blockquote>

<blockquote class="speaker1">
Quand on lui a annoncé que ça allait nous prendre
trois mois avant de pouvoir tout corriger, le mug avec la photo de ses enfants a
failli traverser la pièce. Parce que oui, il faudra bien trois mois à mon équipe
pour adapter le code qui ne marchait que sous WebKit. Pourtant c'est lui qui
avait insisté pour que ce soit plus fluide et agréable à utiliser… Et quand on
lui avait dit qu'il nous faudrait quelques jours de plus pour que ça marche sous
Firefox pour Android, il avait répondu : « On s'en fiche, y a que trois crétins
qui l'utilisent ». Je vous jure, les chefs ne savent pas ce qu'ils veulent…
</blockquote>

Oh que j'aimerais que ce scénario soit possible. Mais il y a un truc qui cloche
dans cette histoire : les tablettes Microsoft ne pourront pas se vendre en
quantité dans trois mois. Pas parce que le produit est mauvais, au contraire il
a l'air prometteur. Mais bien parce qu'avec les articles parus dans la presse et
les tests des acheteurs en boutiques, tout le monde se rendra compte que
beaucoup de sites sont actuellement inutilisables. Et cela fait partie des
critères d'achat et de succès d'une plateforme. On a d'ailleurs déjà vu des cas
similaires.

## Sans Firefox, pas d'iPhone

Nous sommes en 2004, Internet Explorer domine le marché des navigateurs,
Netscape n'est plus. Après une compétition acharnée, la fameuse *Browser Wars*,
le navigateur avec les fonctionnalités les plus intéressantes a gagné. <span class="pullquote">Oui,
c'était bien Internet Explorer le meilleur navigateur à ce moment-là</span>.

Les développeurs web sont vraiment ravis de pouvoir utiliser tous les
raffinements d'Internet Explorer 6 : font-face, AJAX, innerHTML.
Malheureusement, la plupart de ces fonctionnalités sont inopérantes dans les
navigateurs alternatifs de l'époque (Mozilla Suite, Opera, etc.), ce qui limite
forcément leurs parts de marché : les utilisateurs pensent qu'ils sont
défaillants et retournent donc dans le confort du navigateur dominant.

Imaginons maintenant que l'iPhone sorte dans ce contexte de 2004. Un [téléphone
mobile révolutionnaire](http://www.apple.com/fr/pr/library/2007/01/09Apple-Reinvents-the-Phone-with-iPhone.html), un iPod à écran panoramique doté de
commandes tactiles et un appareil de communication sur Internet innovant. "
Appareil de communication sur Internet innovant " ?  
Avec si peu de sites compatibles ? Je ne crois pas : la plupart des sites incluent du code spécifique
à Internet Explorer, rendant Safari iPhone bien inintéressant. Et franchement,
un iPod qui passe des coups de fil sans un vrai navigateur, ça n'aurait pas valu
ce prix-là. Et toute la révolution de l'internet mobile qui a suivi aurait été
bien retardée.

Heureusement, entre la domination d'Internet Explorer et la sortie de l'iPhone,
il y a eu un nouvel arrivant qui a changé la donne : Firefox. On ne sait pas
trop pourquoi Firefox a réussi là où les autres navigateurs alternatifs avaient
échoué, mais le cercle vertueux s'est installé. Les développeurs web se sont
intéressés au navigateur et ont donc corrigé leurs sites pour qu'ils
fonctionnent avec Firefox. Du coup, moins d'utilisateurs ont été déçus par les
premiers sites qu'ils visitaient, et quand ils l'étaient ils le signalaient aux
développeurs de ces derniers. Ces sites furent corrigés et ainsi de suite : au
fur et à mesure, nous avons obtenu un Web de plus en plus basé sur les
standards.

C'est dans ce contexte d'un Web respectueux des standards (que l'on croit
souvent sources de restrictions), qu'Apple a pu inventer une nouvelle façon de
consulter le Web. Vous me direz qu'Apple aurait aussi pu adapter Safari pour
qu'il se comporte comme Internet Explorer. Oui, mais…

## Implémenter des fonctionnalités propriétaires est très coûteux, pour tout le monde

Pour les navigateurs, cela s'appelle le *reverse engineering*. Les implémenteurs
regardent comment se comporte le navigateur à copier et ils recopient ce
comportement. C'est comme si vous deviez réinventer une montre sans pouvoir
l'ouvrir. Vous imaginez la complexité de la tâche ?

Le *reverse engineering* coûte donc de l'argent et du temps aux implémenteurs.
Déroulons un peu le procédé. Il vous faut d'abord découvrir comment agit cette
fonctionnalité. Donc vous testez plein de scénarios, vous découvrez des cas que
vous n'aviez pas envisagés. Vous devez ensuite écrire plein de tests pour
vérifier que vous avez bien tout compris de cette fonctionnalité ;  Ces tests
serviront d'ailleurs à vérifier votre implémentation. On peut maintenant passer
à l'implémentation proprement dite. La première version est la partie simple.  
Une fois cette première passe terminée, avec tous vos tests au vert, vous allez
vérifier que les sites qui nécessitaient cette fonctionnalité se comportent
correctement. Ah non, celui-ci a encore une différence. Ah oui, ce cas
particulier n'avait pas été pris en compte. Oh, mais c'est qu'il faut changer
l'algorithme entièrement pour pouvoir répondre à ce besoin. On retourne en
arrière…  
Au bout d'un moment, vous obtiendrez peut-être quelque chose qui
correspond plus ou moins à l'implémentation originale. Vous avez enfin
implémenté une fonctionnalité populaire d'un concurrent. Les développeurs web
sont donc ravis de votre travail. Eh bien non : votre version est plus lente ;
ou ne fonctionne pas en combinaison avec telle autre technologie ; en plus,
c'est franchement compliqué à utiliser comme fonctionnalité…

En temps normal, tout ce travail est partagé au sein des instituts de
standardisation (W3C, ECMA, IETF, …). Quelqu'un arrive avec une idée (et peut-
être une implémentation). L'idée est discutée pour voir si c'est la meilleure
façon de résoudre le problème. La syntaxe aussi est discutée pour qu'elle soit
la plus facile à utiliser. On réfléchit en outre à l'interaction avec les autres
technologies. Et puis des tests sont écrits pour vérifier la conformité. Les
coûts sont partagés entre tous les participants, la fonctionnalité est plus
intéressante pour les développeurs et un nouvel entrant pourra s'appuyer sur ce
travail déjà effectué.

Mais de quels nouveaux entrants parle-t-on ?

## La mobilité, ce nouveau champ de bataille

Regardez l'évolution des technologies disponibles dans nos navigateurs. Depuis
que la concurrence a été rétablie, d'abord par Firefox puis par Chrome, il n'y a
jamais eu autant d'innovations dans les navigateurs de bureau. Mais <span class="pullquote">du côté des
appareils mobiles, l'innovation n'est pas encore au rendez-vous</span>. C'est parce
qu'il y a une énorme barrière pour les nouveaux entrants. Toi qui me lis, tu ne
testes que les navigateurs par défaut d'iPhone et d'Android lorsque tu
travailles sur un site mobile ? Et tu ne détectes que les navigateurs similaires
pour servir une version mobile ? Donc les nouveaux navigateurs se tapent du
contenu de merde. Et l'on retombe dans le cycle de 2004. Les plateformes
dominantes se renforcent, ce qui diminue l'innovation dans le secteur. Depuis
quand Safari sur iPhone n'a-t-il pas fait de progrès ? Et ne parlons pas du
navigateur par défaut d'Android… [1] Pourtant, il y a de l'innovation à revendre
sur le mobile. Regardons quelques exemples :

### Opera

Depuis longtemps, Opera est présent sur le mobile. Ses deux
navigateurs, Opera Mini et Opera Mobile, sont très bien adaptés à ce contexte
d'utilisation. Ils permettent d'économiser énormément de bande passante lorsque
l'on consulte un site web. Cela a deux avantages énormes : on accède aux sites
plus rapidement (je suis par exemple un utilisateur ravi d'Opera Mini lorsque je
me retrouve en 2G) ; et bien sûr, si on dispose d'un quota de navigation
restreint, on peut alors visiter plus de sites.

### Mozilla

Mozilla souhaite fournir un environnement de développement pour les
applications basé uniquement sur les technologies web (notamment à travers
Firefox OS). Cela passe par un concept d'applications web. Mais aussi par de
nouvelles APIs permettant d'accéder aux mêmes capacités que les applications
natives : l'accès à la caméra, aux contacts, aux SMS, etc. Imaginez les
possibilités qu'ouvriraient ces APIs si elles étaient disponibles partout… Et ce
ne sont pas Apple ou Google qui fourniront ce genre d'APIs rapidement, ils
préfèrent que les développeurs préparent des applications natives. Ainsi,
lorsque vient le moment de racheter un mobile, on se sent obligé de rester sur
la même plateforme pour ne pas avoir à racheter toutes les applications.

### Microsoft

L'innovation ne se trouve pas forcément dans le navigateur mais
plutôt dans l'OS proposé. On peut dire beaucoup de choses de Windows Phone, mais
il a le mérite de ne pas suivre les conventions de design d'iOS et d'Android. Et
la perspective d'une tablette avec clavier intégré est fort intéressante.
Cependant, il a du mal à être un choix crédible, entre autres à cause de la
compatibilité des sites.

## Conclusion

Des navigateurs plus rapides, plus complets et qui repensent
l'interaction avec l'utilisateur. De l'innovation, quoi. Mais celle-ci est
bloquée par notre paresse. Car avant de pouvoir proposer leurs innovations, ces
compétiteurs doivent fournir le service minimum, à savoir rendre correctement la
majorité des sites web. Sans cela, ils ne peuvent prétendre à une part de marché
suffisante pour pouvoir imposer leurs innovations… Dommage, non ?

Comment corriger le tir ? On en revient aux fondamentaux : dégradation gracieuse
ou amélioration progressive. Lorsque vous utilisez une fonctionnalité peu
répandue, prévoyez le cas pour les navigateurs ne l'implémentant pas. Il est
possible d'offrir une fonctionalité légèrement dégradée ou d'utiliser [des
polyfills](http://remysharp.com/2010/10/08/what-is-a-polyfill/), ces librairies
qui comblent un manque. Il faut aussi faire attention à n'utiliser que ce qui
est en voie de standardisation. Comme le dit Léa Vérou, [tout ce qui est
disponible via des préfixes en CSS n'est pas forcément en voie de
standardisation](http://www.alistapart.com/articles/every-time-you-call-a-proprietary-feature-css3-a-kitten-dies/). Vérifiez aussi que vous supportez la
méthode standard en plus de l'implémentation propriétaire (comme pour [le cas
des résolutions doublées](http://www.w3.org/blog/CSS/2012/06/14/unprefix-webkit-device-pixel-ratio/)). Si nous ne corrigeons pas le tir collectivement, nous
ralentirons l'innovation sur cette belle plateforme qu'est le Web. Au boulot !


[1] Heureusement, il va bientôt être remplacé par Chrome.

