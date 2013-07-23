# Signalétique des Hyperliens

On ne se soucie pas assez de la signalétique des liens et de leurs différents états. C’est un défaut d’ergonomie d’autant plus regrettable que l’hyperlien est le fondement de la navigation sur le Web. 

Voyons ensemble comment améliorer cela :

## Hyperlien, kezako ?

À l'origine du Web tel que nous le connaissons aujourd'hui : l'hypertexte.

Initialement, un document Web est une page de texte. Mais la nouveauté avec l'hypertexte, c'est la possibilité de lier une page à une autre, non par la reliure physique d'un livre, qui ordonne les pages de façon successive — la nouveauté donc, c'est la possibilité de les lier indépendamment de la chronologie de lecture. Au besoin, une page peut en appeler une autre, depuis l'intérieur même du texte. Ce n'est plus du texte simple, mais de l'« hypertexte ». Et ce qui permet de lier, de l'« hyperlien ».

Comment ça marche ? C'est très simple : quelques mots sont « cliquables ». Cliquer dessus a pour conséquence d'afficher la page liée. Ce concept extrêmement simple a été l'un des moteurs principaux de la réussite du Web.

L'hyperlien est la base de la navigation sur Internet. Le Web ne cesse d'évoluer, mais nous cliquons toujours sur des liens.

### Ancres et liens

Sur une page Web, des **liens** ajoutés à des mots, des phrases ou des images, peuvent être cliqués pour vous transporter à un autre endroit. Vous pouvez créer des liens vers n'importe quel point d'une page, auquel vous souhaitez pouvoir accéder d'un simple clic. C'est ce qui s'appelle une **ancre**.

#### D'abord les ancres…

L'élément HTML utilisé pour ce faire est `a`, de l'anglais *anchor*, qui signifie ancre.

![Ancre](anchor.gif) 

Pour accéder à un emplacement bien précis de la page, il faut placer une ancre juste au-dessus de l'endroit où vous souhaitez atterrir. Une ancre se code ainsi :

~~~ {lang="html" line="1"}
<a id="toto"></a>
~~~

Il s'agit donc de deux balises, `<a>` et `</a>`, avec le nom de l'ancre indiqué dans l'attribut « `id` » placé sur la balise ouvrante (et rien entre les deux balises) [^1].

#### Puis les liens : href

Pour accéder à cet emplacement, il faut ajouter, ailleurs dans la page, un **lien** vers cette ancre. Un lien se code comme suit :

~~~ {lang="html" line="1"}
<a href="#toto">Ceci est un lien vers mon ancre</a>
~~~

Il s'agit de la même balise `<a>`, mais l'attribut utilisé cette fois est « `href` ». La destination est indiquée dans cet attribut. Il s'agit de l'**adresse hypertexte de référence** à laquelle vous souhaitez vous rendre. L'attribut `href` est ce qui caractérise l'hyperlien.

Ancres et liens d'une page servent typiquement à constituer des liens d'évitement (« *skip links* ») ou un sommaire de la page. Mais les liens permettent également de pointer vers d'autres pages et toute autre ressource, interne ou externe au site. 

Exemple de lien interne :

~~~ {lang="html" line="1"}
<a href="index.html">Voici le lien de retour à l'accueil</a>
~~~

Exemple de lien externe :

~~~ {lang="html" line="1"}
<a href="http://www.toto.net">Ceci est un lien vers le site toto.net</a>
~~~

Ancre ou lien, retenons que dans tous les cas il s'agit du couple de balises `<a>` et `</a>`. Ce sont les attributs utilisés, `id` ou `href`, qui précisent leur rôle.

## Pourquoi diable sont-ils bleus soulignés ?

Il fallait trouver un moyen de distinguer les liens du reste du texte, pour rendre visibles ces mots cliquables qui sont comme autant de portes ouvertes dans le texte. Comme vous l'avez remarqué, le texte d'un lien est par défaut coloré en bleu et souligné. Pourquoi ?

![Apparence par défaut d'un lien texte](lien-hypertexte-link.gif) 

### D'où vient ce bleu ?

Saviez-vous que c'est à Sir Tim Berners-Lee, l'inventeur du Web, que nous devons la couleur par défaut des liens ? Il a probablement été le premier à signaler les liens par la couleur bleue, d'après des [captures d'écran de son premier navigateur web](http://www.w3.org/History/1994/WWW/Journals/CACM/screensnap2_24c.gif), en 1993.

À l'époque, on ne disposait pas d'un grand choix de couleurs : seulement 16 (cf.[Colors](http://www.w3.org/TR/REC-html40/types.html#h-6.5) dans la spécification HTML 4.01), car les cartes graphiques les plus courantes n'en affichaient pas davantage.

Mosaic, un des premiers navigateurs web, affichait des pages Web avec du texte noir sur un fond gris. La couleur la plus foncée disponible, lisible sur une telle teinte, hors le noir, était le bleu. Le rouge et le vert ne pouvaient être choisis, en raison de leurs fortes connotations sémantiques respectives (danger/interdit, sécurité/permis, etc.). Le jaune est trop peu contrasté. Par conséquent, pour démarquer les liens du texte brut, de façon à ce qu'ils restent toujours lisibles, c'est la couleur bleue qui a été retenue.

### Pourquoi soulignés ?

Les moniteurs en noir et blanc, ou en bichromie (souvent noir et vert), étaient encore fréquents. Pour preuve, le NeXT Cube, l'ordinateur sur lequel a été développé le premier navigateur Web par Tim Berners-Lee, en 1990, ne disposait que d'un [affichage en niveaux de gris](http://www.w3.org/MarkUp/tims_editor). Avant la couleur, c'est donc le souligné qui permettait de distinguer les hyperliens.

En typographie, le souligné n’a aucune raison d’être utilisé. Il ne s’emploie que pour pallier l’absence d’italique, lorsque celle-ci n'est techniquement pas disponible, comme c'est le cas dans l’écriture manuscrite ou dactylographique. Il sert alors à accentuer certains passages d'un texte, voire signaler les erreurs, mais aussi parfois à marquer le titre des références bibliographiques. Sur le Web, où l’usage d’italique est possible, le souligné est un enrichissement typographique inutile… disponible pour signaler autre chose, qui n’existe pas sur le papier : les hyperliens.

## Pourquoi et que changer ?

Faut-il garder les liens ainsi, bleus soulignés ? Beaucoup répondent « Évidemment non ! C’est la préhistoire du Web ! » et force est de constater qu'énormément de sites aujourd’hui appliquent un style différent à leurs liens hypertextes. Mais ce n'est pas toujours bien fait, avec pour conséquence de faire jouer l'internaute à cache-cache avec les liens de la page…

Avec les CSS, vous pouvez choisir assez librement la présentation de vos liens hypertextes. L’essentiel est qu’ils soient repérables dans la page. Il faut qu'ils ressortent visuellement, au premier coup d'œil. Pour ce faire, plusieurs solutions existent : couleur, soulignement mais aussi cartouche, pictogrammes, etc.

Voici ce qu'il faut savoir, si vous décidez d'en changer l'apparence.

### Attention au contraste

Si elle est plus jolie que le bleu d'origine, la couleur utilisée pour vos liens n'a peut être pas un contraste suffisant pour rester correctement lisible en toutes circonstances : les mots écrits dans cette teinte peuvent être difficiles à déchiffrer en dehors des conditions optimales de luminosité ambiante, par exemple quand vous surfez par temps ensoleillé, dans le train ou dans la rue, ce qui est de plus en plus fréquent. N'oubliez pas non plus que nos chers internautes n’ont pas tous une excellente acuité visuelle.

Voici comment garantir la lisibilité des liens dans le texte : après s'être assuré que le contraste est suffisant entre la couleur du texte et la couleur de son arrière-plan ([critère 3.3 Accessiweb 2.2](http://www.accessiweb.org/index.php/accessiweb_2.2_liste_deployee.html#crit-3-3)), on choisira une couleur de lien ayant un rapport de contraste supérieur ou égal à 3:1 par rapport au texte environnant ([critère 10.6 Accessiweb 2.2](http://www.accessiweb.org/index.php/accessiweb_2.2_liste_deployee.html#crit-10-6)). De nombreux outils permettent de mesurer ces contrastes, qui sont présentés dans cet article : [Contrastes de texte](http://openweb.eu.org/articles/accessibilite_contrastes_textes_sites) (OpenWeb, 2012).

D'après les critères d'accessibilité, le contraste suffit à distinguer un lien à partir du moment où « un élément de distinction autre que la couleur est visible lors du *focus* des liens (graisse, soulignement, icône,etc) » précise le [critère RGAA No 7.10](http://www.rgaa.net/Maintien-de-la-distinction.html). Et c'est ce que l'on voit souvent : des liens de couleur assortie à la charte du site, soulignés au survol… mais pas toujours au *focus*.

### Revisiter le standard

Nos dinosaures de l’Internet que sont Yahoo!, Google, eBay et Amazon, pour ne citer qu’eux, utilisent toujours cette bonne vieille recette du lien bleu, et ce n’est certainement pas le fruit du hasard. Leur besoin d'optimiser la performance et le taux de conversion président ce choix. Le bleu reste préférable, puisqu'il s'agit d'un standard : une majorité d'internautes ont acquis le concept « lien = bleu ». Utiliser cette couleur pour les liens textes, c'est donc leur faciliter la navigation.

Bien que l'accessibilité n'ait peut-être pas été la priorité de Tim Berners-Lee à l'époque, ce choix de couleur est heureux, comme le pointe Joe Clarck, cité dans cette note « [Why are Links Blue?](http://alistapart.com/blog/post/why-are-links-blue) » (A List Apart, Zeldman, 2013) : 

> « Alors que le rouge et le vert sont des couleurs souvent mal distinguées par les daltoniens, presque personne n'a de déficience de perception de la couleur bleue. Par conséquent, presque tout le monde peut voir le bleu, ou, plus exactement, presque tout le monde peut distinguer le bleu comme couleur différente des autres. C'est une vraie chance que les liens soient bleus soulignés par défaut ! »

De même, savez-vous pourquoi le site Facebook a toujours été bleu et blanc ? La raison n'est pas arbitraire, ni esthétique : son créateur, Mark Zuckerberg, souffre de daltonisme et le bleu est la couleur qu'il voit le mieux.

Des liens bleus, oui, mais pas n'importe lequel. Ces dinosaures, comme d'autres sites plus modernes, révisent le standard.  
La teinte est mise au goût du jour, pour un bleu avoisinant, souvent moins vibrant et plus foncé, et notons que le souligné n'est pas systématiquement conservé par défaut :

![Des liens bleus, oui, mais pas n'importe lequel!](bleus.png)


### La couleur ne suffit pas

Quand certains mots d’un texte sont en couleur, comment l’internaute peut en deviner la signification sans se tromper ? S’agit-il de la mise en exergue d'une expression importante ? d'un intertitre ? ou d'un hyperlien ? Prenons un exemple :

![Où sont les liens ?](hyperlinks-bouygues-1.png "Où sont les liens ?")

Pouvez-vous identifier à coup sûr les liens de l’extrait ci-dessus ? Non. Car si les liens semblent ici signalés par la couleur verte, tous les mots de cette couleur ne sont pas des liens, la bonne blague ! Ici, comme souvent, liens, exergues et titres ont la même couleur : c’est un moyen facile de personnaliser une charte graphique. Mais il faut avouer que ce n'est pas toujours assez explicite.

La différence de couleur n’est pas un élément distinctif suffisant. Cela laisse trop de place aux erreurs d’interprétation, avec le risque que certains utilisateurs passent totalement à côté. C'est ce qu'énonce le [critère 3.1 Accessiweb 2.2](http://www.accessiweb.org/index.php/accessiweb_2.2_liste_deployee.html#couleurs) : « l’information ne doit pas être donnée uniquement par la couleur ».

### Soulignez !

Si ce ne peut pas être par la couleur seule, comment distinguer un lien du texte environnant ? Les écrans monochromes des débuts d'Internet, mais aussi de nos liseuses contemporaines, nous rappellent que le souligné est le moyen à la fois le plus simple et le plus robuste de signaler les hyperliens. Reprenons notre exemple :

![Soulignés, on ne s’y trompe plus !](hyperlinks-bouygues-3.png "Soulignés, on ne s’y trompe plus !")

Comme on le voit dans l'exemple ci-dessus, souligner les liens ne laisse plus aucune place au doute et facilite d’autant la navigation. Pourquoi ? Sur le Web, le souligné est une convention forte. C’est le rendu par défaut des navigateurs pour les liens et les utilisateurs s’attendent à ce qu'un texte souligné soit cliquable.

C’est si caractéristique que, pour éviter les clics inutiles sur des contenus soulignés qui seraient perçus comme des hyperliens – comme le montre ce [contre-exemple](http://romy.tetue.net/978), on réserve le souligné aux seuls hyperliens, comme le recommande la [Bonne pratique Opquast N°42](https://checklists.opquast.com/11/criteria/541/).


### Le lien dans tous ses états

Un lien n'est pas statique. C'est une porte vers une autre ressource. Comme une porte s'ouvre et se franchit, le lien connaît plusieurs états. Il se survole, se clique et s'active pour aller de page en page. Ces différents états sont par défaut signalés par des couleurs différentes : lorsque vous cliquez sur un lien, il réagit visuellement en passant à la couleur rouge. Quand vous revenez ensuite à ce lien, il a pris une autre couleur encore, violet, pour montrer qu'il a déjà été visité.

Dès lors que l'on modifie l'apparence des liens, il ne faut pas oublier de prendre en compte tous ces états, soit plus de **15 combinaisons stylistiques à prévoir** :

![Tous les états d'un lien](combinaisons.png)

Ce n'est pas simple car un lien peut avoir plusieurs états à la fois : il peut avoir été visité et être survolé, il est donc violet et souligné… Mais quiconque a déjà utilisé une page Web comprend le principe de ces conventions très rapidement et intuitivement. Tout l'art est donc de faire aussi bien.

#### Cliquez, tabulez, surfez !

Les liens se cliquent. Mais pas seulement… En activant les liens — par un clic de souris, une entrée au clavier ou une commande vocale — l'utilisateur peut visiter ces ressources.

##### Signaler le survol (`:hover`)

Le survol (`:hover`), c'est passer au-dessus du lien, avec la souris. Il est par défaut signalé par un changement du pointeur, la fameuse petite main qui pointe du doigt (*hand*).

![Apparence du curseur "main"](mano_cursor.svg.png "clic !")

Le survol n'est pas pris en charge sur les terminaux tactiles, qui compensent de diverses façons. S'il est important de le signaler, il ne faut pas s'appuyer uniquement sur les déplacements de la souris ou la pseudo-classe CSS `:hover`, qui peuvent ne pas se comporter comme souhaité sur un appareil à écran tactile comme l'explique l'article : [Non hover](http://trentwalton.com/2010/07/05/non-hover/) (en anglais).

##### Signaler le focus améliore la navigation

Le lien (ou l’élément) qui a le **_focus_** (`:focus`) est celui que l’internaute a atteint. Rappelons qu'il peut être atteint de plusieurs façons : en positionnant le doigt sur l’écran tactile ou le curseur de la souris sur l'élément, ou encore en tabulant au clavier (avec la touche `TAB`).

Le *focus* est par défaut signalé par un contour pointillé, ou par un halo bleuté, selon les navigateurs. Cela répond à une exigence d'accessibilité clairement indiquée dans les [WCAG](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#navigation-mechanisms-focus-visible) et ainsi exprimée dans la méthode d'application française, au [Critère 10.7 Accessiweb 2.2](http://www.accessiweb.org/index.php/accessiweb_2.1_liste_generale.html#crit-10-7) : « Dans chaque page Web, pour chaque élément recevant le *focus*, la prise de *focus* est-elle visible ? »

Méfiez-vous donc des *reset* CSS qui annulent le style natif du *focus* — d’un coup de `:focus { outline: 0; }`. Cela prive les internautes naviguant au clavier de tout repère et gêne considérablement leur navigation. À ce propos, vous pouvez consulter ce site dédié : [outlinenone.fr](http://www.outlinenone.fr).

Au contraire, il est recommandé d'accentuer le *focus*, car le rendu par défaut est trop discret. Parcourir la page à coup de tabulations fait sauter le *focus* d’un coin à l’autre de l’écran de façon parfois imprévisible. Pour éviter de le perdre et de trop le chercher du regard, le *focus* doit attirer l’attention ([Signaler le *focus* améliore la navigation](http://romy.tetue.net/678)). Vous pouvez accentuer le contraste, le contour, ou lui donner une couleur de fond.

La méthode la plus simple consiste à styler la prise de *focus* comme le survol. D'une pierre deux coups. Cela évite les défauts majeurs d'accessibilité, par exemple sur les menus *dropdown*, et c'est aussi une façon de s'assurer d'un rendu homogène à la souris et au tactile.

##### Et le lien actif (`:active`) ?

Quand on le clique, le lien est dit « actif » (`:active`). Cet état est par défaut signalé en rouge. Il est nécessaire de le distinguer pour rendre perceptible que l'action est enclenchée, notamment pour les personnes ayant des difficultés à manipuler la souris. Je vous invite d'ailleurs à lire l'article [`:hover` vs `:active`](http://www.lesintegristes.net/2009/09/13/hover-vs-active/) écrit par Eric Le Bihan, et publié sur Les Intégristes en 2009.

##### N'oublions pas les liens visités (`:visited`)

N'oublions pas l'état visité (`:visited`) qui, comme son nom l'indique, est l'état d'un lien qui a déjà été suivi. Il est par défaut signalé par la couleur violette. C'était une convention autrefois bien respectée, mais qui est de moins en moins courante. À tord. Changer l’apparence des liens visités facilite l'identification des contenus restant à découvrir, comme le pointe la [Bonne pratique Opquast N°124](https://checklists.opquast.com/fr/oqsv2/criteria/623/). C'est une aide pour l'internaute, une incitation à la découverte de nouvelles pages.
<!-- Il me semble que pour des raisons de sécurité, il n'est maintenant plus possible de styler toutes les propriétés visuelles de l'état :visited, ça mériterai d'être mentionné -->

#### Un exemple ?

On ne se soucie pas assez de signaler les différents états d’un lien. C'est moins simple qu'il y paraît de prime abord, mais il est possible d'allier originalité et ergonomie.  
Voici un exemple, qui n'est certes pas parfait, mais complet :

![Personnalisation de tous les états d'un lien](combinaisons-2.png)

Difficile de se rendre compte sur une image statique… Pour se donner un bon aperçu de leur nature changeante, il est indispensable de travailler les liens dans leur environnement naturel, c'est-à-dire directement dans le navigateur, pour pouvoir les cliquer, les tabuler et les chatouiller.

## Comment styler les liens en CSS ?

Faciliter le repérage du lien pointé ou actif, permettre l’identification des contenus déjà visités… cela se fait en quelques lignes de CSS, avec les « pseudo-classes ». Mais attention à leur ordre de définition !

Les pseudo-classes constituent des classes prédéfinies en CSS. Elles s’appliquent à certains éléments dont l’état peut changer. Les plus connues et plus populaires concernent les liens hypertextes qui possèdent plusieurs états, comme vu précédemment : visité, actif et non visité, sans oublier le survol et le *focus*. À chacun correspond une pseudo-classe.

Mais attention, il est important de déclarer ces pseudo-classes dans cet ordre :

1. `:link`
2. `:visited`
3. `:focus`
4. `:hover`
5. `:active`

Par exemple, pour modifier la couleur des liens selon leur état :

~~~ {lang="css" line="1"}
a { color: blue; }
a:link {} /* lien non visité */
a:visited { color: purple; } /* lien visité */
a:focus { color: green; } /* lien tabulé */
a:hover { color: green; } /* lien survolé */
a:active { color: red; } /* lien activé */
~~~

La règle `a:hover` doit être placée après `a:link` et `a:visited`, sinon la cascade fera que la propriété `color` spécifiée sera surchargée.

Pour retenir cet ordre, l’astuce mnémotechnique est l’expression « *LoVe Fuck HAte* », où les lettres en majuscule signalent ici la première lettre de chaque pseudo-classe, dans le bon ordre. Voir : [Ordre des pseudo-classes des liens](http://romy.tetue.net/love-fuck-hate).


## Des liens stylés !

Véritable fondement de la navigation sur le Web, l'hyperlien mérite qu'on s'attarde sur son rendu graphique : c'est le point d'interaction primaire avec l'internaute, il est absolument incontournable. Les conventions sont fortes et établies, certes, mais elles peuvent être re-visitées pour personnaliser une charte graphique. Respecter les quelques règles de base que cet article rappelle permet de préserver l'ergonomie.

Amusez-vous bien !

[^1]: L'attribut `name`, initialement employé pour les ancres, en HTML 4 (cf. [12.2.1 Syntax of anchor names](http://www.w3.org/TR/REC-html40/struct/links.html#h-12.2.1)), est déprécié en XHTML et obsolète en HTML5. L'usage de l'attribut « `id` » est plus large, puisqu'on peut également l'utiliser pour créer une ancre, dans la balise ouvrante de n'importe quel élément, outre l'élément `a`. Certains vieux navigateurs ne le supportant pas, les deux attributs étaient parfois employés conjointement, comme suit : `<a name="toto" id="toto"></a>`.
