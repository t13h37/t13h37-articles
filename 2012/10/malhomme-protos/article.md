# S’il-te-plait, dessine-moi un prototype

## C’est quoi un prototype ?

La semaine dernière, les 18-19-20 octobre, avait lieu l’édition 2012 de [Paris Web](http://www.paris-web.fr/), pendant laquelle j’ai eu l’opportunité de pouvoir co-présenter un atelier sur le processus créatif avec l'une de nos auteurs, Virginie Caplet.  
J’y parlais principalement de *prototypage*, cette étape de la conception d’un projet web qui vient après le brief créatif et le brainstorming, et qui consiste à réaliser un « exemplaire incomplet et non définitif de ce que pourra être le produit ou l'objet final. », généralement un site ou une application Web (source [Wikipedia](http://fr.wikipedia.org/wiki/Prototypage)).

En gros, il s’agit de représenter aussi simplement que possible la structure des pages ou écrans principaux de votre site ou application web, sous la forme visuellement la plus sobre possible (généralement en « fil de fer ») et avec un minimum d’interactions (liens entre pages par exemple, mais j’y reviendrai plus loin).

## Pourquoi tu me demandes ça à moi ?

Le problème du prototype, c’est qu’en fonction des contextes des projets, ce n’est pas toujours la même (voire la bonne) personne qui s’en occupe.  
Quand on a de la chance et qu’on a un ergonome rompu à cet exercice, c’est la panacée. Mais dans tous les autres cas, qui doit le faire ? Le graphiste, le développeur *front*, le chef de projet… ?  
À tout le moins, il faut quelqu’un avec une bonne connaissance du sujet, des notions de design ET des notions techniques, une grande curiosité, un moral d’acier… et rien d’autre à faire.  
J’entends par là qu’en l’absence d’un poste spécifiquement prévu à cet effet et occupé il faut assigner à cette étape une personne unique, dont ce sera la responsabilité et l’unique tâche sur le projet concerné.

Cela permet plusieurs choses :

- réaliser cette étape en prenant le temps nécessaire et avec un recul salvateur ;
- responsabiliser la personne en charge de cette étape, afin de faciliter son implication ;
- s’assurer de la cohérence des décisions qui sont prises ;
- « décomplexer » les autres membres de l’équipe d’un projet : ils savent que si la décision finale est prise par le prototypeur-référent et non eux, elle est aussi sa « pénitence » car il en porte la responsabilité. Cela facilite les échanges et la prise de décisions.

En faisant « tourner » cette responsabilité régulièrement entre les différents intervenants capable de s’en occuper au fur et à mesure des différents projets, on y gagne d’autant plus :

- chacun apprend de cette étape et en comprend mieux les tenants et les aboutissants ;
- chacun a l’opportunité de vivre personnellement la position de prototypeur-référent en elle-même et de mieux l’apprécier quand ce n’est pas son tour ;
- chacun ayant participé à des projets différents peut apporter son expérience personnelle pour enrichir le processus.

## À quoi ça va servir ?

Le prototype en lui-même a tout un tas d’applications utiles.

### Éviter les impasses

Que ce soit dans le cadre d’une page ou entre les pages, il permet de concrétiser un tunnel et des principes de navigation. Il est ainsi plus aisé de voir qu’on a oublié ou sous-représenté les accès à une rubrique donnée, ou que ceux-ci ne sont pas cohérents d’une page à l’autre.

### Ne rien oublier sur le bord de la route

Il n’y a pas grand-chose de plus difficile, chronophage, et donc coûteux, à implémenter qu’une fonctionnalité ou un élément de contenu qu’il faut insérer après coup au chausse-pied dans une arborescence ou un gabarit qui n’a pas été conçu pour.

### S’épargner les *moonboots* à la plage

Avoir une vision d’ensemble des principaux gabarits d’un projet web et de leur fonctionnalités et organisation interne permet d’assurer une cohérence à ces différents éléments et principes de structure.

### Des triangles dans des carrés

Cela permet aussi de s’assurer de la pertinence d’un choix fonctionnel ou structurel par rapport à un contenu donné, les prototypes étant généralement le bon moment d’un projet pour tester le contenu réel (futur ou déjà existant) d’un site ou d’une application web.

### Chasser les chimères

Rien ne sert de faire valider des choix techniques ou ergonomiques si ceux-ci ne sont pas pertinents ou même possibles. En impliquant toutes les parties concernées dans sa conception (développeurs *front* et *back*, client, graphiste…) on s’assure que ces choix auront été faits en toute connaissance de cause.

### Traduction universelle

Le prototype, de par sa forme, sert de socle de langage commun aux personnes impliquées, et permet ainsi d’éviter les confusions et les mauvaises surprises.  
L’incapacité à faire preuve de l’abstraction nécessaire, parfois ressentie par certaines parties prenantes, est gommée, ce qui facilite une plus grande implication et la participation des différents intervenants.

## À quoi ça ne doit pas servir ?

Il ne faut cependant pas se tromper, le prototype n’est pas un outil de travail sans faille.
Ainsi, le plus grand danger est de le pousser « trop loin » et d’en faire un "presque-site" ou une "presque-application".  
Il est donc important d’en éliminer autant que possible les notions de couleur, de graphisme, de police… et de limiter les interactions au minimum : liens entre les pages, éventuellement quelques accordéons. Mais il faudrait éviter les carrousels, popups, etc.

### « J’aimais bien le Comic Sans » (*true story*)

Une première raison est qu’en ayant un prototype trop abouti on créée des attentes, et donc on augmente les risques de déceptions.  
Il faut aussi éviter de trop contraindre le travail du graphiste qui n’a même pas encore eu vraiment l’occasion de s’impliquer concrètement dans la conception.

### Un coup de peinture et c’est bon, non ?

Il est aussi possible qu’un prototype trop avancé donne l’impression que le reste du travail à faire pour aboutir au produit fini est trivial.  
Non seulement vous allez créer de la frustration chez votre client, mais vous risquez aussi de dévaloriser l’importance des étapes suivantes et le travail nécessaire pour y arriver.

### Trois heures après, le canard… 

Enfin, réaliser un prototype très abouti peut s’avérer chronophage, oui, même avec des outils comme [Axure](http://www.axure.com) ou des *frameworks* comme [Bootstrap](http://twitter.github.com/bootstrap/) ou [Foundation](http://foundation.zurb.com/).  
Il est facile de perdre du temps sur des détails, parce que le client a du mal à faire la différence entre le prototype et le produit fini par exemple. À chercher à reproduire trop fidèlement le résultat final, on en oublie un des premiers rôles du prototype : permettre une vue d’ensemble.

## Comment je m’y prends ?

Il n’existe pas (à ma connaissance) de méthode officielle pour « bien faire un prototype » ni même de « bonnes pratiques », mais voici quelques conseils de méthodologie et d’outils issus de mes années d’expérience tant en tant que productrice de prototypes que d'utilisatrice de prototypes créés par d’autres.

### Je commence par la tête ou par le corps ?

Commencer par lister les différents gabarits et leurs relations, en s’aidant de l’arborescence prévue, est généralement le plus simple.  
Pour chaque gabarit, il faudra ensuite lister les différents contenus et fonctionnalités prévus, ce qui permettra de différencier ce qui doit être commun à toutes les pages et ce qui est spécifique à certaines.

Une fois ces listes faites, il est utile de les ordonner selon l’importance sémantique et fonctionnelle des différents éléments, c’est-à-dire selon leur priorité pour la compréhension et l’utilisation, ainsi que le poids en ressources qu’ils impliquent.  
Il faut d’ailleurs noter qu’il est plus simple de faire cet ordonnancement quand on travaille dans une démarche *mobile first* que l’inverse.

Vient alors le moment de construire concrètement vos gabarits. Quels que soit les outils choisis (cf. partie suivante), cela consiste à représenter visuellement mais de manière simpliste les différents éléments constitutifs d’un gabarit de page ou d’un écran d’application.  
Il est généralement convenu de commencer « flou » pour dégrossir au fur et à mesure. On débutera donc avec des rectangles ou des carrés pour signifier les principaux blocs, des lignes droites pour les textes de travail et des lignes ondulées pour les titres, des blocs « barrés » pour les images, etc.

On peut choisir de reproduire ce processus pour chaque page/écran, puis de passer tous ces gabarits à l’étape suivante ; ou bien de faire les premiers gabarits, les passer à l’étape suivante décrite ci-après et, quand ils sont validés, faire les gabarits suivants en reprenant depuis la version « floue », et ainsi de suite…  
Cela dépendra de vos contraintes techniques ou client et de la typologie de projet : la première méthode est ainsi *probablement* plus pertinente dans le cas d’une application que celle d’un site web.

L’étape suivante, donc, est de passer à une représentation plus réaliste, même si il n’est pas encore forcément temps d’utiliser de vrais contenus partout : pour une liste d’actualités par contre, du *lorem ipsum* peut suffire tant qu’est bien déterminée la nature des contenus voulus - titre, date, catégorie, chapô, etc.

Enfin, si nécessaire (par exemple afin de trancher sur des structures d’éléments ou pages ou sur des types d’interaction), utiliser du « vrai » contenu sur certains gabarits complets peut par exemple permettre de mieux évaluer le volume d’une page complète ou l’utilisation à faire des médias disponibles.

Petit conseil final : pour chaque élément interactif identifié, il est bon d’en expliciter le comportement (*click*, *rollover*, etc.) et de faire apparaître les différents états résultant de l’interaction.

### Un bon ouvrier a de bons outils

Selon vos préférences, la typologie de projet, le niveau de maîtrise de votre client, l’étape du prototypage où vous vous trouvez, voire les processus internes préétablis qui vous sont imposés, plusieurs types d’outils s’offrent à vous.

#### Qui peut le plus peut le moins

Inspirons-nous de la vague « back to basics » : les éléments d’interface en [post-its](http://uxpin.com/products.html) ou (mieux ?) en [magnets](http://www.guimagnets.com/), les grilles [avec *breakpoints* intégrés](http://sneakpeekit.com) ou [sans](http://www.raincreativelab.com/paperbrowser/), voire un simple cahier à petits carreaux et un crayon.

Ces outils sont idéaux en début de projet pour itérer rapidement sans devoir sortir l’artillerie lourde ou même un ordinateur portable, ainsi que pour impliquer le client qui pourra alors lui-même s’essayer à l’exercice et ainsi mieux en appréhender à la fois la difficulté et l’importance.

#### De la charrue au tracteur

Pour des prototypes plus précis, il faut se tourner vers des applications, en ligne ou non, les premières ayant l’avantage de permettre la collaboration à plusieurs.
Parmi les plus connues et les plus largement disponibles :

- [Axure](http://www.axure.com), 225 €, PC/Mac ;
- [Balsamiq](http://www.balsamiq.com), 60 € sur PC/Mac/Linux, ou à partir de 9 € par mois en <abbr title="Software as a Service" lang="en">SaaS</a> ;
- [MockFlow](http://mockflow.com), gratuit pour PC/Mac sans compte en ligne associé, gratuit en basique ou 61 € par an en premium pour la version <abbr>SaaS</a> avec synchro vers le logiciel ;
- [UXPin](http://uxpin.com), à partir de 5,3 € par mois, <abbr>SaaS</abbr> ;
- [Pencil](http://pencil.evolus.vn), Open Source et gratuit, PC/Mac/Linux et extension Firefox;

#### Soyez créatifs

Une simple solution bureautique comme Powerpoint ou Impress peut aussi très bien faire l’affaire si c’est ce qui vous est le plus facile d’accès, surtout si vous l’agrémentez d’éléments d’interface en png comme le [kit Dragnet](http://www.dragnet.se/webbdesign/wireframes.png).

Et quelle que soit l’application (ou le service) que vous choisissez, vous pouvez décider d’y créer vos prototypes statiques et de gérer leur interactivité et les retours clients avec des applications dédiées, comme par exemple :

- [invision](http://www.invisionapp.com), gratuit pour un projet, à partir de 7,6 € au delà, <abbr>SaaS</a> ;
- [cageapp](https://cageapp.com), à partir de 11 €, <abbr>SaaS</a>.

## Conclusion

Le prototype est à la fois un outil et une étape indispensable et pourtant parfois négligée, qui permet d’avoir une vision à la fois globale et précise d’un projet et d’impliquer les différentes parties dans un processus de conception collaboratif.  
Le travail de prototypeur est lui aussi souvent négligé quand il n’y a pas déjà une personne dédiée en interne, et pourtant il y aurait beaucoup à gagner à systématiser sa présence : pont entre différents domaines, un pied « dans chaque pré », il a un rôle de médiateur et de facilitateur, tout en étant garant de la cohérence d’un projet.
