# Signalétique des Hyperliens

## Hyperlien, kezako ?

À l'origine du Web tel que nous le connaissons aujourd'hui : l'hypertexte.

Initialement, un document Web, c'est une page de texte. Comme pour un livre, un index (ou table des matières) les recense toutes.  
Mais la nouveauté avec l'hypertexte, c'est la possibilité de lier une page à une autre, non par la reliure physique d'un livre, qui les ordonne de façon successive -- la nouveauté donc, c'est la possibilité de les lier indépendamment de la chronologie de lecture. Au besoin, une page peut en appeler une autre, depuis l'intérieur même du texte. Ce n'est plus du texte simple, mais de l'« hypertexte ». Et ce qui permet de lier, de l'« hyperlien ».

Comment ça marche ? C'est très simple : quelques mots sont « cliquables ». Cliquer dessus a pour conséquence d'afficher la page liée.  
L'hyperlien est la base de la navigation sur Internet. Le Web ne cesse d'évoluer, mais nous cliquons toujours sur des liens.

Le concept en lui-même est extrêmement simple : le lien représente une connexion d'une ressource Web à une autre, et il a été l'un des moteurs principaux de la réussite du Web.


### L'invention de l'hyperlien

L'hypertexte est issu de nombreuses années de recherche dans plusieurs disciplines.

La première description du concept est probablement due à Vannevar Bush. En 1945, dans un article du *Atlantic Monthly* intitulé « [As We May Think](http://www.w3.org/History/1945/vbush/vbush-all.shtml) », il décrit un bureau électromécanique futuriste appelé Memex, acronyme de *MEmory EXtender*. Ce bureau devait contenir des microfilms et les retrouver automatiquement à partir d'un index.

![MeMex](memex.gif)

Mais ce qui distinguait Memex d'une bibliothèque automatique était la possibilité de créer un index pour toute paire de microfilms, ce qui revient à créer des hyperliens[^1]. Le mot lui-même, « *hypertext* », est apparu plus tard, en 1965, sous la plume de Ted Nelson.

Le World Wide Web, conçu par Tim Berners-Lee en 1989, est aujourd'hui le système hypertexte le plus vaste et le plus utilisé : il compte des milliards de documents répartis dans le monde entier, lesquels sont consultés par des millions de personnes à travers le réseau Internet.

Les hyperliens du Web sont contenus dans des documents hypertextes généralement écrits en langage HTML (*HyperText Markup Language*), présentés sous la forme de pages Web. L'important, dans le sigle « HTML », sont les deux premières lettres, c'est-à-dire « HyperText ».

### Ancres et liens

Sur une page Web, des **liens** ajoutés à des mots, des phrases ou des images, peuvent être cliqués pour vous transporter à un autre endroit. Vous pouvez créer des liens vers n'importe quel point d'une page, auquel vous souhaitez pouvoir accéder d'un simple clic. C'est ce qui s'appelle une **ancre**[^ancre].

#### D'abord les ancres…

L'élément HTML utilisé pour ce faire est `a`, de l'anglais *anchor*, qui signifie ancre.

![Ancre](anchor.gif) 

Pour accéder à un emplacement bien précis de la page, il faut placer une ancre juste au-dessus de l'endroit où vous souhaitez atterrir. Une ancre se code ainsi :

`<a name="toto"></a>`

Il s'agit donc de deux balises, `<a>` et `</a>`, avec le nom de l'ancre indiqué dans l'attribut « `name` » placé sur la balise ouvrante (et rien entre les deux balises).[^3]

#### Puis les liens : href

Pour accéder à cet emplacement, il faut ajouter, ailleurs dans la page, un **lien** vers cette ancre. Un lien se code comme suit :

`<a href="#toto">Ceci est un lien vers mon ancre</a>`

Il s'agit de la même balise `<a>`, mais l'attribut utilisé cette fois est « `href` ». La destination est indiquée dans cet attribut. Il s'agit de l'**adresse hypertexte de référence** à laquellevous souhaitez vous rendre. L'attribut `href` est ce qui caractérise l'hyperlien.

Ancres et liens d'une page servent typiquement à constituer des liens d'évitement (« *skip links* ») ou un sommaire de la page. Mais les liens permettent également de pointer vers d'autres pages et tout autre ressource, interne ou externe au site. 

Exemple de lien interne :

`<a href="index.html">Ceci est un lien retournant en page d'accueil</a>`

Exemple de lien externe :

`<a href="http://www.toto.net">Ceci est un lien vers le site toto.net</a>`

Il est même possible de pointer l'ancre d'une page externe :

`<a href="http://www.la-grange.net/w3c/html4.01/struct/links.html#h-12.2.1">Lien vers le chapitre traitant de la syntaxe des noms d'ancre, dans la spécification HTML</a>`

Ancre ou lien, retenons que dans tous les cas, il s'agit du couple de balises `<a>` et `</a>`. Ce sont les attributs utilisés qui caractérisent leur usage.

## Mais pourquoi diable sont-ils bleus ? ##

Il fallait trouver un moyen de distinguer les liens du reste du texte, pour rendre visibles ces mots cliquables qui sont comme autant de portes ouvertes dans le texte.

Comme vous le savez, les liens d'une page Web sont indiqués en les rendant visuellement différents du texte environnant. Par défaut, le texte du lien est colorié en bleu et souligné. 

### D'où vient ce bleu ?

Saviez-vous que c'est à Sir Tim Berners-Lee, l'inventeur du Web, que nous devons la couleur par défaut des liens ?
Et... pourquoi le bleu ? Nous allons voir que ça tient beaucoup au hasard et que c'est pourtant un très bon choix.

Tim Berners-Lee a probablement été le premier à signaler les liens par la couleur bleue, d'après des captures d'écran en 1993 de son premier navigateur web : 

![Capture d'écran du premier navigateur web de Tim Berners-Lee - Source : http://www.w3.org/People/Berners-Lee/WorldWideWeb.html](screensnap2_24c.gif "Capture d'écran du premier navigateur web de Tim Berners-Lee -  (<a href="http://www.w3.org/People/Berners-Lee/WorldWideWeb.html">Source</a>)")

À l'époque, on ne disposait pas d'un grand choix de couleurs. La spécification HTML d'alors définit 16 couleurs (cf. [W3C color names](http://www.morecrayons.com/palettes/colorNames/w3c.php) et [Colors](http://www.w3.org/TR/REC-html40/types.html#h-6.5) dans la spécification HTML 4.01), car les cartes graphiques les plus courantes n'en affichaient pas plus (en 640 x 480 pixels).

![Les 16 couleurs ](colorNames-16.png)

Mosaic, un des premiers navigateurs web (1993-1997), affichait des pages Web avec du texte noir sur un fond gris. La couleur la plus foncée disponible, lisible sur un tel fond gris, hors le noir, était le bleu. Le rouge et le vert ne pouvaient être choisis, en raison de leurs connotations sémantiques respectives.  Le jaune est trop peu contrasté.  
Par conséquent, pour démarquer les liens du texte brut, de façon à ce qu'ils restent toujours lisibles, c'est la couleur bleue qui a été choisie, plus précisément `#0000FF`[^4]. 

![Préférences des couleurs des liens dans Mosaic](colors-mosaic.png "Préférences des couleurs des liens dans Mosaic")

Bien que l'accessibilité n'ait peut-être pas été la priorité de Tim à l'époque, ce choix de couleur est heureux, comme le pointe Joe Clarck (cité dans cette note « [Why are Links Blue?](http://alistapart.com/blog/post/why-are-links-blue) », A list apart, Zeldman, 2013) : 

> « Alors que le rouge et le vert sont des couleurs souvent mal distinguées par les daltoniens, presque personne n'a de déficience de perception de la couleur bleue. Par conséquent, presque tout le monde peut voir le bleu, ou, plus exactement, presque tout le monde peut distinguer le bleu comme couleur différente des autres. C'est une vraie chance que les liens soient bleus soulignés par défaut ! »

De même, savez-vous pourquoi le site Facebook a toujours été bleu et blanc ?   
La raison n'est pas arbitraire, ni esthétique : son créateur, Mark Zuckerberg, souffre de daltonisme et le bleu est la couleur qu'il voit le mieux.

![Daltonisme](daltonismes.jpg)

### Pourquoi soulignés ?

Les moniteurs en noir et blanc, ou en bichromie (souvent noir et vert), étaient encore fréquents. Pour preuve, le NeXT Cube, l'ordinateur sur lequel a été développé le premier navigateur Web, appelé WorldWideWeb (plus tard rebaptisé Nexus), par Tim Berners-Lee, en 1990, ne disposait que d'un affichage en niveaux de gris. Avant la couleur, c'est le souligné qui permettait de distinguer les hyperliens.

![Capture d'écran de l'éditeur de Tim Berners-Lee - Source : http://www.w3.org/People/Berners-Lee/WorldWideWeb.html](tims_editor.jpeg "Capture d'écran de l'éditeur de Tim Berners-Lee -  (<a href="http://www.w3.org/People/Berners-Lee/WorldWideWeb.html">Source</a>)")

En typographie, le souligné ne s’emploie que pour pallier l’absence d’italique, lorsque celle-ci n'est techniquement pas disponible, comme c'est le cas dans l’écriture manuscrite ou dactylographique. Il sert alors à accentuer certains passages d'un texte, voire signaler les erreurs, mais aussi parfois à marquer le titre des références bibliographiques. <!-- Remarque : souligner pour marquer l’importance est une mauvaise habitude héritée de l’ère dactylographique, mais qui n’a aucune raison de persister sur les supports numériques ; sur le Web, où l’usage d’italique est possible, le soulignement utilisé comme mise en exergue est une erreur typographique. -->

![Italique, gras, souligné…](italic_bold_underline.png)

Le soulignement sur le Web signale autre chose, qui n’existe pas sur le papier : les hyperliens. C’est une convention forte : les internautes s’attendent à ce qu’un texte souligné soit cliquable. Pour éviter les clics inutiles sur des contenus soulignés qui seraient perçus comme des hyperliens, on réserve le souligné aux seuls hyperliens.

### Faut-il les garder ainsi ?

<!-- à approfondir -->
Beaucoup répondent « Évidemment non ! c’est la préhistoire du Web ! » et constatent qu'énormément de sites aujourd’hui appliquent un style différent à leurs liens hypertextes.

Sauf que nos dinosaures de l’internet que sont Yahoo!, Google, eBay et Amazon, pour ne citer qu’eux, utilisent toujours cette bonne vieille recette, et ce n’est certainement pas parce que cela correspond à leur charte graphique et c’est encore moins le fruit du hasard. Le guide de style du gouvernement américain, « [Research-based Web Design & Usability Guidelines](http://www.usability.gov/guidelines/guidelines_book.pdf) » (PDF, 20.64MB), qui s'appuie sur de nombreuses études d'utilisabilité (mais ne dispense aucune donnée chiffrée), préconise d’employer la couleur par défaut des liens.<!-- DATE ? 2003 ?
Leavitt M. O., Shneiderman B., U.S. Government Printing Office
PDF à télécharger depuis cette page : http://www.usability.gov/guidelines/
+ les 209 recommandations de ce guide traduites en français par Nicole Lompre :
http://web.univ-pau.fr/~lompre/documents/209Guidelines.pdf -->

Les liens doivent être très reconnaissables. Il faut qu'ils ressortent visuellement. Pour ce faire, plusieurs solutions existent (soulignement, pictogramme, couleur spécifique…)

Seulement, le bleu est préférable, puisqu'il s'agit d'un standard. Une majorité d'internautes ont acquis le concept « lien = bleu ». Utiliser la couleur bleue pour les liens textes, c'est donc faciliter la navigation. De même, le moindre texte souligné à l'écran est interprété comme un lien. Ce sont des conventions fortes, dont il est dommage de perdre le bénéfice.

Mais si vous décidez d'en changer l'apparence, voici comment faire.

#### La différence de couleur ne suffit pas

Vous pouvez choisir assez librement la présentation de vos liens hypertextes. L’essentiel est qu’ils soient repérables dans la page. Cependant, la différence de couleur n’est pas un critère distinctif suffisant, et ce pour plusieurs raisons :

Quand certains mots d’un texte sont en couleur, comment l’internaute peut-il en deviner la signification sans se tromper ? S’agit-il de mettre en exergue une expression importante ? de valoriser un intertitre ? ou de signaler un hyperlien ?

![Où sont les liens ?](figure/hyperlinks-bouygues-1.png "Où sont les liens ?")

Pouvez-vous identifier à coup sûr les liens de l’extrait ci-dessus ? Non. Car si les liens semblent ici signalés par la couleur verte, tous les mots de cette couleur ne sont pas des liens, la bonne blague ! Ici, comme souvent, liens, exergues et titres ont la même couleur : c’est un moyen facile de personnaliser une charte graphique. Mais qui n'est pas assez explicite.

Utiliser la couleur seule ne suffit pas, car ça laisse trop de place aux erreurs d’interprétation. Seul le corps de texte ou la graisse distingue titre et exergue des liens : c’est trop peu pour distinguer les liens des autres éléments mis en valeur.

Autre souci, la couleur utilisée dans cet exemple, `#759937`, est très jolie mais n’a pas un contraste suffisant pour rester correctement lisible en toutes circonstances : les mots écrits dans ce vert sont difficiles à déchiffrer hors des conditions optimales de luminosité ambiante, par exemple quand vous surfez par temps ensoleillé, dans le train ou dans la rue, ce qui est de plus en plus fréquent.   
Enfin, nos chers internautes n’ont pas tous une excellente acuité visuelle. S’appuyer uniquement sur la couleur pour différencier visuellement les liens du texte qui les entoure ne suffit pas : certains utilisateurs passeront totalement à côté. N’oubliez pas les daltoniens !

Bref, la signalétique des liens ne doit pas passer uniquement par la couleur.

#### Soulignez les liens par défaut !

Puisque ce ne peut pas être par la couleur seule, comment distinguer un lien du texte environnant, si ce n’est en le soulignant par défaut ?   
Grâce à un picto ? complexe à mettre en œuvre, en plus de surcharger graphiquement la page…   
En gras ? intéressant, mais cela réserve cet enrichissement typographique à ce seul usage, en plus de détourner de son rôle initial d'insistance, pour lequel il faudra donc trouver une alternative.

![Soulignés, on ne s’y trompe plus !](figure/hyperlinks-bouygues-3.png "Soulignés, on ne s’y trompe plus !")

Comme on le voit dans l'exemple ci-dessus, souligner les liens ne laisse plus aucune place au doute et facilite d’autant la navigation. Pourquoi ? Sur le Web, le soulignement est une convention forte.

C’est le comportement standard des navigateurs et les utilisateurs s’attendent à voir les liens soulignés. Retirer le soulignement rend leur identification plus difficile, comme nous venons de le voir. C’est si caractéristique qu’il est recommandé de réserver le souligné aux seuls hyperliens.

Pour laisser les liens soulignés par défaut, il suffit… de ne toucher à rien, puisque c’est le comportement naturel de tous les navigateurs ! Plus précisément, et par sécurité, on préférera les définir comme dans [feuille de style par défaut pour HTML](http://www.w3.org/TR/CSS21/sample.html), c’est-à-dire :

`:link, :visited { text-decoration: underline }`


## Le lien dans tous ses états

Un lien n'est pas statique. C'est une porte vers une autre ressource. Comme une porte s'ouvre et se franchit, le lien connaît plusieurs état. Il se survole, se clique, se suit et permet d'aller de page en page. Ces états sont signalés graphiquement par des couleurs différentes.

Lorsque vous cliquez sur un lien, il réagit visuellement en passant à la couleur rouge. Quand vous revenez ensuite à ce lien, il a pris une autre couleur encore, le violet, pour montrer qu'il a déjà été visité.

Quiconque a déjà utilisé une page Web comprend le principe de ces conventions très rapidement et intuitivement.

### Cliquez, tabulez, surfez !

Les liens se cliquent. Mais pas seulement… En activant les liens -- par un clic de souris, une entrée au clavier ou une commande vocale -- l'utilisateur peut visiter ces ressources.

Navigation au clavier => besoin de signaler le *focus*. Qu'est-ce donc que le « *focus* » ?

#### Signaler le survol (:hover)

Le survol (`:hover`), c'est passer au-dessus du lien (avec la souris).  
Par défaut signalé par un changement du pointeur (*hand*).  
Personnalisable : souligné au survol, etc.

#### Signaler le focus améliore le confort de navigation

Le lien (ou l’élément) qui a le **_focus_** est celui que l’internaute a atteint. Rappelons qu'il peut être atteint de plusieurs façons : en positionnant le doigt sur l’écran tactile ou le curseur de la souris sur l'élément, ou encore en tabulant au clavier.

Essayez donc de tabuler sur un site, en pressant plusieurs fois la touche « `TAB` » de votre clavier. Si ce site est bien fait, vous verrez « s’allumer », les uns après les autres, les éléments que vous atteignez ainsi : liens, champs de saisie des formulaires, boutons, etc. Sinon, pleurez.

##### Qu'est-ce que ce contour pointillé ?

Normalement, aussitôt qu'il est atteint, le lien se voit doté d'un contour en pointillés.

![Illustration : ceci est un lien ayant le focus](??.png "illustration : ceci est un lien ayant le focus")

Ce rendu n'est pas systématique, mais c'est celui recommandé dans la [feuille de style par défaut pour HTML](http://www.w3.org/TR/CSS21/sample.html), soit très précisément :

`:focus          { outline: thin dotted invert }`

Cela répond à une exigence d'accessibilité, clairement indiquée dans les [WCAG](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#navigation-mechanisms-focus-visible) :

> *2.4.7 Focus Visible: Any keyboard operable user interface has a mode of operation where the keyboard focus indicator is visible. (Level AA)*

et ainsi exprimée dans la méthode d'application française Accessiweb :

> Critère 10.7 [Bronze] Dans chaque page Web, pour chaque élément recevant le focus, la prise de focus est-elle visible ?

##### Ne masquez pas la prise de focus !

Cette bordure pointillée autour des liens, notamment des images-liens et autres boutons-liens, paraît esthétiquement insupportable à de nombreux webdesigners qui cherchent à la supprimer. Malheureux !

Ce rendu visuel signale les liens qui reçoivent le *focus* lorsque vous naviguez dans la page Web en utilisant la touche `TAB` (ou équivalent). C'est particulièrement utile pour les personnes qui ont une déficience visuelle ou qui ne peuvent pas utiliser une souris. En supprimant ce contour, vous risquez de rendre votre site inaccessible pour ces personnes.

Méfiez-vous donc des *reset* CSS qui annulent le style natif du *focus* — d’un coup de `:focus { outline: 0; }`. Cela prive les internautes naviguant au clavier de tout repère et gêne considérablement leur navigation. Voir ce site dédié : [outlinenone.fr](http://www.outlinenone.fr).

Si vraiment vous deviez supprimer le style natif du *focus*, n’oubliez pas de le redéfinir, comme le recommande d’ailleurs Eric Meyer en commentaire de son [fameux reset](http://meyerweb.com/eric/thoughts/2008/01/15/resetting-again/) : « *remember to define focus styles!* ». Il est même conseillé **d'accentuer** le *focus*, comme nous allons le voir.

##### Focus et survol, même combat ?

La méthode la plus simple consiste à styler la prise de *focus* comme le survol. D'une pierre deux coups. Si vraiment vous n'avez pas le temps de faire mieux, faites au moins cela : ajoutez systématiquement `:focus` à chaque règle CSS définissant `:hover`. Par exemple, remplacez :

`a:hover { text-decoration: underline; }`

par

`a:focus, a:hover { text-decoration: underline; }`

Focus et survol se démarquent alors exactement de la même façon. C'est ce que recommande Roger Johansson : [Whenever you use :hover, also use :focus](http://www.456bereastreet.com/archive/201004/whenever_you_use_hover_also_use_focus/). Cela évite les défauts majeurs d'accessibilité, par exemple sur les menus *dropdown*.

Ce n’est cependant pas idéal, car si le soulignement suffit souvent à confirmer le survol du pointeur que l’on suit des yeux à l’écran, le *focus*, qui n’est quant à lui pas précédé du regard, a besoin d’être signalé de façon beaucoup plus forte que le survol.

##### Renforcez plutôt le *focus*

Parcourir la page à coup de tabulations fait sauter le *focus* d’un coin à l’autre de l’écran de façon parfois imprévisible. Pour éviter de le perdre et de trop le chercher du regard, le *focus* doit attirer l’attention.

Le contour pointillé recommandé reste insuffisant, trop discret. Parvenez-vous vraiment, avec ça, à suivre le *focus* des yeux, lorsque vous tabulez dans la page ? Non. Le pointillé par défaut est souvent difficile à repérer, voire impossible (sur une image, par exemple, ou quand il se trouve hors champ). Sans doute est-ce la raison pour laquelle les navigateurs webkit (et donc Safari, Chrome, etc.) ont renforcé ce rendu par un halo autour des liens et des champs de formulaire qui reçoivent le *focus*.

![Prise de focus dans différents navigateurs, de gauche à droite et de haut en bas : Firefox, Chrome, Safari, IE et Opera](focus-navigateurs.png "Prise de focus dans différents navigateurs, de gauche à droite et de haut en bas : Firefox, Chrome, Safari, IE et Opera")

Pour faciliter la navigation au clavier, mieux vaut accentuer la prise de *focus*. Plusieurs moyens stylistiques sont utilisables :

- Donnez-lui une couleur de fond
- Changez la couleur du texte
- Personnalisez le contour
- Accentuez le contraste pour une meilleure visibilité

Le mieux, c'est-à-dire le plus satisfaisant pour les utilisateurs et le plus simple à mettre en œuvre, reste encore de ne pas toucher au style natif et laisser chaque navigateur prendre en charge le rendu du *focus*.


#### Et le lien actif (`:active`) ?

Quand on le clique, le lien est dit « actif ».
Cet état est par défaut signalé en rouge.
Il est personnalisable via la pseudo-class CSS `:active`.

#### Liens visités !

> [BP N°124](https://checklists.opquast.com/fr/oqsv2/criteria/623/) : Le site n'applique pas le même style aux liens visités et non visités.
 
Ne pas changer l’apparence des liens visités empêche de savoir quels liens ont déjà été suivis.


### Le lien dans tous ses états

Récapitulons. Un lien peut être visité ou non, survolé, avoir le *focus*, être actif… et tout ça à la fois. Soit **20 combinaisons possibles**… à prévoir graphiquement !

<!-- A COMPLETER !!! -->
Ici, tableau des rendus par défaut des différents états.  
+ plusieurs exemples de personnalisations graphiques intéressantes.

- lien
- lien au focus
- lien survolé
- lien cliqué
- lien visité

Voici quel est le rendu par défaut de ces différents états :

- lien : bleu
- focus : bordure en pointillé
- survolé : souligné
- actif : rouge
- visité : violet

Ce n'est pas simple, car un lien peut être à la fois déjà visité au moment où il est survolé, il est donc violet et souligné.

### Et sur les terminaux tactiles ?

Le survol n'est pas pris en charge sur les terminaux tactiles, etc.
// petite nuance : iphone/ipad interprètent et affichent le focus (en remplacement du :active je crois) mais c'est à vérifier //
<!-- A COMPLETER !!! -->

## Comment styler vos hyperliens ?

### Ordre des pseudo-classes des liens : LoVe Fuck HAte

Pour styler les liens, l’ordre dans lequel sont déclarées les pseudo-classes est important. Pour le retenir, dites : « *LoVe Fuck HAte* » !

On ne se soucie pas assez de signaler les différents états d’un lien. C’est un défaut d’ergonomie d’autant plus regrettable que l’hyperlien est le fondement de la navigation sur le Web et qu’il est facile d’améliorer cela. Faciliter le repérage du lien pointé ou actif, faciliter l’identification des contenus déjà visités... cela se fait en quelques lignes de CSS, avec les « pseudo-classes ». Mais attention à l’ordre !

Les pseudo-classes constituent des classes prédéfinies en CSS. Elles s’appliquent à certains éléments dont l’état peut changer. Les plus connues et plus populaires concernent les liens hypertextes qui possèdent plusieurs états : visité, actif et non visité, sans oublier le survol et le *focus*. À chacun correspond une pseudo-classe.

Il est important de déclarer ces pseudo-classes dans cet ordre :

1. link
2. visited
3. focus
4. hover
5. active

Par exemple, pour modifier la couleur des liens selon leur état :

        a { color: blue; }
        a:link {} /* lien non visité */
        a:visited { color: purple; } /* lien visité */
        a:focus { color: green; } /* lien tabulé */
        a:hover { color: green; } /* lien survolé */
        a:active { color: red; } /* lien activé */

En pratique, on commence par styler de manière générique a { ... } et on s’en contente souvent. Quand on veut bien faire, on précise chaque état, distinctement : les liens visités avec a:visited { ... } puis les liens ciblés, avec ces trois pseudo-classes d’un coup : a:focus, a:hover, a:active { ... }.

La règle a:hover doit être placée après a:link et a:visited, sinon la cascade fera que la propriété color spécifiée sera cachée. Il est excessivement rare d’avoir à définir a:link.

Pour retenir cet ordre, l’astuce mnémotechnique habituelle est l’expression « *LoVe HAte* », — deux mots fameux que le terrifiant pasteur du film *La Nuit du chasseur* avait tatoués sur les phalanges de ses doigts —, où les lettres en majuscule signalent ici la première lettre de chaque pseudo-classe, dans le bon ordre... *but what of :focus?* Pour s’en rappeler, n’oublions pas ce qui trouve naturellement sa place entre l’amour et la haine : « *LoVe Fuck HAte* ».

//  je rajouterai une partie sur les propriétés qu'il est possible de styler. De mémoire, elles sont relativement restreintes du fait d'une faille de sécurité découverte sur [`:visited`](https://developer.mozilla.org/en-US/docs/CSS/:visited) //


## Conclusion
<!--
RDV : (là, que dire ?)
CS : qu'il est possible de faire plein de choses (sympas) avec les liens, mais que l'essentiel c'est de faire en sorte que tout un chacun puisse les utiliser pleinement. Et que cela passe par une mise en exergue judicieuse et appropriée ?
-->

## Références
Ce livre s'appuie sur les documentations techniques de référence sur le sujet, c'est-à-dire les spécifications W3C des langages concernés, mais aussi sur les bonnes pratiques et critères d'accessibilité qui garantissent un confort d'utilisation optimal de l'interface Web.

### Spécifications W3C

Relire les spécifications du W3C, ici traduites en français :   

- [12 Les liens](http://www.la-grange.net/w3c/html4.01/struct/links.html), spécification HTML 4.01, W3C, 1999
- [5.11.2 Les pseudo-classes d'ancre : :link et :visited](http://www.yoyodesign.org/doc/w3c/css2/selector.html#link-pseudo-classes), Spécification CSS2, W3C, 1998
- [5.11.3 Les pseudo-classes dynamiques : :hover, :active et :focus](http://www.yoyodesign.org/doc/w3c/css2/selector.html#dynamic-pseudo-classes), Spécification CSS2, W3C, 1998

### Bonnes pratiques Opquast

[Bonnes pratiques Opquast V2](https://checklists.opquast.com/fr/opquastv2?q=hyperliens)

- [BP N°42](https://checklists.opquast.com/fr/oqsv2/criteria/541/) : Le soulignement est réservé aux hyperliens.
- [BP N°43](https://checklists.opquast.com/fr/oqsv2/criteria/542/) : Les hyperliens sont visuellement différenciés du reste du contenu.
- [BP N°124](https://checklists.opquast.com/fr/oqsv2/criteria/623/) : Le site n'applique pas le même style aux liens visités et non visités.
- [BP N°188](https://checklists.opquast.com/fr/oqsv2/criteria/687/) : Les hyperliens internes et externes sont différenciés.

### Critères Accessiweb

[Référentiel Accessiweb 2.1](http://www.accessiweb.org/index.php/accessiweb_2.1_liste_deployee.html), liste déployée

- Critère 10.7 [Bronze] Dans chaque page Web, pour chaque élément recevant le *focus*, la prise de *focus* est-elle visible ?
        - Test 10.7.1 : Pour chaque élément recevant le *focus*, l'indication visuelle du navigateur ne doit pas être supprimée (propriété CSS *outline*, *outline-color*, *outline-width*, *outline-style*). Cette règle est-elle respectée ?
        - Test 10.7.2 : Pour chaque élément recevant le *focus*, l'indication visuelle du navigateur ne doit pas être dégradée (propriété CSS *outline-color*). Cette règle est-elle respectée ?
        - Test 10.7.3 : Chaque lien dans un texte signalé par la couleur uniquement vérifie-t-il ces conditions ?
                - Une indication visuelle autre que la couleur permet de signaler la prise de *focus* au clavier.
                - Une indication visuelle autre que la couleur permet de signaler le survol du lien à la souris.

### Autres articles de référence :

- [CSS from the Ground Up -6](http://www.wpdfd.com/editorial/basics/cssbasics6.html), by Joe Gillespie, 2004, ici traduit en français : [CSS : on reprend tout à zéro ! (épisode 6)](http://www.pompage.net/traduction/cssdezero-6), Pompage, 2005.
- [Liens hypertextes : le style bleu souligné est-il encore un incontournable ?](http://www.superfiction.net/blog/index.php?2008/01/28/200-liens-hypertextes-le-style-bleu-souligne-est-il-encore-un-incontournable), par Eric Di Pol, 2008
- [:hover vs :active](http://www.lesintegristes.net/2009/09/13/hover-vs-active/), par Eric Le Bihan, Les Intégristes, 2009


## NOTES :

[^1]: Sources : [Hypertexte](http://fr.wikipedia.org/wiki/Hypertexte) Wikipédia et [The Most Important Software Innovations](http://www.dwheeler.com/innovation/innovation.html), David A. Wheeler

[^2]: Cf. spécification HTML 4.01, W3C, 1999 : [12 Les liens](http://www.la-grange.net/w3c/html4.01/struct/links.html)

[^3]: on peut également utiliser l'attribut « `id` » pour créer une ancre, dans la balise ouvrante de n'importe quel élément, y compris l'élément `a`. `<h2 id="section2">Section deux</h2>`
L'usage de l'attribut « `id` », plus large et compatible XHTML, s'est généralisé ces dernières années. Certains vieux navigateurs ne le supportant pas, les deux attributs étaient parfois employés conjointement, comme suit :
`<a name="toto" id="toto"></a>`

[^4]: Source : [http://www.quora.com/Web-Browsers/Why-are-hyperlinks-blue](http://www.quora.com/Web-Browsers/Why-are-hyperlinks-blue)
[^5]: 
[^6]: 
[^7]: 
[^8]: 
[^9]: 
[^10]: 
