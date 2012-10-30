# Toi aussi, fais avancer le Web

Contrairement à une idée reçue, le Web n'est pas quelques chose de figé sur lequel vous n'avez aucune influence, au contraire. Tout créateur de contenu ou d'application Web participe à la création et à l'invention permanente de ce média... Vous aussi, eh oui !

Faisons un rapide retour en arrière : 1990, laboratoire du CERN, Genève ; [Tim Berners-Lee](http://fr.wikipedia.org/wiki/Tim_Berners-Lee) et [Robert Cailliau](http://fr.wikipedia.org/wiki/Robert_Cailliau) bricolent un petit projet visant à mettre en place la notion d’hypertexte sur un réseau TCP/IP pour se partager plus facilement quelques documents de travail entre collègues. Vingt ans plus tard, ce petit bricolage s'est transformé pour devenir notre quotidien, où nous essayons tant bien que mal de réaliser des sites Web beaux, efficaces et respectueux de tout un tas de règles appelées "standards".

Pendant cette magnifique ellipse de vingt ans, que s'est-il passé exactement ?  
Pour faire simple, différents acteurs privés ont trouvé l'idée géniale et ont cherché à la développer à leur profit. Ces acteurs privés sont grossièrement de trois natures différentes : 

- Tout d'abord, il y a les éditeurs de logiciels permettant d'utiliser les technologies Web : Apple, Google, Microsoft, Opera et Mozilla pour ne citer que les plus connus, mais on trouve également Adobe, IBM, Nokia, etc. ;
- Ensuite, on trouve tous les éditeurs de sites Web : là, la palette est large puisque ça va de Facebook jusqu'à... vous ! ;
- Et enfin, on trouve tous les organismes de normalisation qui essaient tant bien que mal de mettre tout le monde d'accord : le [W3C](http://fr.wikipedia.org/wiki/W3C) évidemment, mais également [l'IETF](http://fr.wikipedia.org/wiki/IETF), [l'ECMA](http://fr.wikipedia.org/wiki/ECMA), [l'OASIS](http://fr.wikipedia.org/wiki/Organization_for_the_Advancement_of_Structured_Information_Standards), etc.

Ces différents acteurs ont donc toujours cherché à développer ce nouveau média, mais tout en essayant de tirer la couverture à eux (n'oublions pas qu'il s'agit principalement d'acteurs économiques privés qui sont en recherche de profits). Microsoft a d'ailleurs failli réussir son coup au début des années 2000 avec la prédominance de IE6 sur le marché. Alors, oui, quand on voit de gros poissons comme Apple, Google, Microsoft ou IBM se tirer la bourre sur les évolutions technologiques du Web au sein des organismes de standardisation, on est en droit de se dire que nous, humbles petites fourmis, nous ne somme bons qu'à passer sous le rouleau compresseur de leur intérêts.  
Oui, mais non, car nous avons nous aussi notre mot à dire, et cela de plusieurs façons différentes !

## « Je fais de la qualité, moi, Monsieur. »

Notre première arme de bataille, c'est le respect de notre propre travail. Cela passe entre autres par le respect des standards et le suivi d'un certain nombre de [bonnes pratiques](http://opquast.com/). Anthony Ricaud nous ayant déjà largement [expliqué l'importance du respect des standards pour l’innovation](http://letrainde13h37.fr/21/tu-te-tires-une-balle-dans-le-pied/) et Élie Sloïm ayant de son côté rappelé [comment il est possible de vendre la qualité Web](http://letrainde13h37.fr/9/justifier-le-prix-de-la-qualite/), je ne m'étendrai pas plus sur la question, allez relire l'excellente prose de ces messieurs.

Il est cependant bon de rappeler que les éditeurs de navigateurs ont un intérêt particulier à voir leur produit afficher le plus de pages Web possible. Pour cette raison, si une majorité de développeurs Web créent des pages en suivant une mauvaise pratique évidente, soyez sûrs que ces éditeurs feront en sorte que leurs produits affichent ces pages malgré tout. Ainsi, si vous respectez les standards dans votre travail, vous contraignez les navigateurs à suivre ces standards. C'est exactement ce qui s'est passé en 2004 quand, avec la sortie de Firefox, de nombreux développeurs se sont mis à utiliser massivement les standards. Aujourd'hui, Microsoft vient de sortir Internet Explorer 10 qui est un navigateur extrêmement respectueux des standards, et nous ne pouvons que nous féliciter de cette victoire.

On prête au Mahatma Gandhi cette citation : « Quasiment tout ce que tu fais semblera dérisoire, mais il est essentiel que tu le fasses ».  
Force est de constater que, sur le Web, c'est le cas et que ça marche.

## « Rhaaaa ! Mais pourquoi ce truc ne marche pas pareil partout ? »

Combien de fois avons nous pesté contre les différents navigateurs quand, après des heures de labeur acharné pour mettre sur pied un design magnifique, une simple vérification dans Chrome, Firefox, Internet Explorer ou Opera (rayez les mentions inutiles) nous a fait hurler tels des possédés parce que l'affichage était complètement déstructuré ici ou là.

Eh bien, là aussi, nous avons une arme : nous pouvons nous plaindre. Seulement, attention, il y a deux façon de se plaindre : la bonne et la mauvaise.

La **mauvaise** façon de se plaindre consiste à vociférer, insulter, conspuer, dénigrer le navigateur fautif... bref, vous transformer en troll. Sur le coup, ça soulage (un peu comme pousser un grand cri quand, vers trois heures de matin au retour des toilettes, on se cogne le petit orteil sur le coin du lit), mais ça ne résoudra jamais votre problème.

La **bonne** façon de se plaindre consiste à contacter l'éditeur du navigateur et à lui expliquer gentiment que son produit a un problème, et pour ça il vous faut ouvrir un rapport de bug.  
Contrairement à ce que l'on croit, ouvrir un rapport de bug est très simple et se déroule en trois étapes :

### Qualifier le bug

Pour que l'éditeur du navigateur puisse corriger le bug, il a besoin que vous lui expliquiez quel est le problème et comment le reproduire. Pour cela, écrivez le plus précisément possible comment se produit le bug.  
Si c'est en faisant certaines actions, décrivez précisément ces actions : "je clique là, j’*upload* un fichier, je fait un salto arrière... et paf, le navigateur plante".  
Si c'est lié à du code, créez une petit fichier qui ne contient que le code qui pose problème. En effet, bien souvent, vous voyez un problème noyé dans une page que vous avez intégrée. Si l'éditeur doit fouiller lui-même dans une page cassée pour comprendre le problème, il ne le fera que si la page en question draine des millions de visiteurs... autant dire que c'est assez rare. Cependant, si vous lui donnez juste le strict minimum pour résoudre le problème, vous augmentez très significativement les chances qu'il résolve le problème rapidement.  
Enfin, dernier point important, vérifiez toujours que votre bug est reproductible dans les dernières versions de développement des navigateurs. En effet, il arrive parfois que des bugs que vous avez identifiés dans la version stable d'un navigateur soient déjà corrigés dans la prochaine version. Concrètement, ça veut dire que vous devez toujours vérifier vos bugs au moins dans les versions de navigateurs suivants :

* [Chrome Canari](https://tools.google.com/dlpage/chromesxs) si c'est un bug lié à Chrome,
* [Firefox Nigthly](http://nightly.mozilla.org/) si c'est un bug lié à Firefox,
* [Opera Next](http://www.opera.com/browser/next/) si c'est un bug lié à Opera,
* IE Plateforme Preview si c'est un bug lié à Internet Explorer.

### Signaler le bug

Une fois que vous avez bien isolé et qualifié votre bug, vous pouvez le signaler à l'éditeur du navigateur concerné. Pour cela, ils ont tous des systèmes permettant de faire un rapport de bug :

* Pour Firefox : [https://bugzilla.mozilla.org/](https://bugzilla.mozilla.org/) ;
* Pour Chrome : 
  * [http://code.google.com/p/chromium/issues/entry](http://code.google.com/p/chromium/issues/entry) (pour les bugs liés à l'interface) ;
  * [https://bugs.webkit.org/](https://bugs.webkit.org/) (pour les bugs liés à l'affichage des pages, valable aussi pour Safari) ;
* Pour Opera : [https://bugs.opera.com/wizard/](https://bugs.opera.com/wizard/) ;
* Pour Internet Explorer : [http://connect.microsoft.com/IE](http://connect.microsoft.com/IE).

Le seul problème, c'est qu'il s'agit d'outils où le signalement des bugs se fait en anglais. Si vous n'êtes pas à l'aise avec l'anglais, pas de panique, il y a quelques personnes francophones que vous pouvez contacter et qui pourront vous aider : 

- Pour Firefox et WebKit : [Antony Ricaud](https://twitter.com/rik24d) ;
- Pour Opera : [Karl Dubost](https://twitter.com/karlpro) ;
- Pour Microsoft : [David Rousset](https://twitter.com/davrous).

### Suivre le bug

Une fois que vous avez signalé votre bug, il est important de le suivre et de faire du *lobbying* autour. Concrètement, ça veut dire que vous allez devoir répondre aux éventuelles questions qui vous seront posées par les développeurs. Ça veut également dire qu'il faut vous assurer d'avoir un éventuel délai pour la résolution de votre bug. Pour ça, il n'y a pas 36 000 solutions, il faut aller discuter avec les différentes équipes de ''relation avec les développeurs''. Tous les éditeurs de navigateurs en ont une (parfois bien cachée !) ; n'hésitez pas à solliciter leurs membres, ils sont payés pour ça.

Voici une petite liste de sites et de comptes Twitter qu'il est bon d'avoir sous la main si on veut savoir « Où est-ce que ça en est ? »

#### Mozilla
* Toute l'équipe [Developer Engagement](https://wiki.mozilla.org/Engagement/Developer_Engagement) de Mozilla ;
* [HMO](http://hacks.mozilla.org/), le blog de l'équipe ;
* Anthony Ricaud : [@rik24d](https://twitter.com/rik24d) ;
* Paul Rouget : [@paulrouget](https://twitter.com/paulrouget) ;
* Tristan Nitot : [@nitot](https://twitter.com/nitot).

#### Opera
* [Le blog de l'équipe DevRel d'Opera](http://my.opera.com/ODIN/blog/) ;
* [@ODevRel](https://twitter.com/ODevRel) ;
* Karl Dubost : [@kralpro](https://twitter.com/karlpro) ;
* Andreas Boven : [@andreasbovens](https://twitter.com/andreasbovens).

#### Chrome
* [HTML5Rocks](http://www.html5rocks.com/en/), le blog de l'équipe DevRel de Chromium ;
* [@ChromiumDev](https://twitter.com/ChromiumDev) ;
* Paul Irish : [@paul_irish](https://twitter.com/paul_irish).

#### Microsoft
* [Le blog de l'équipe IE](http://blogs.msdn.com/b/ie/) ;
* David Rousset : [@davrous](https://twitter.com/davrous).

## « Non, mais c'est n'importe quoi ton truc, là ! »

Se plaindre auprès des éditeurs c'est bien, mais il y a encore mieux : se plaindre auprès des organismes de spécification. 

En effet, plutôt que de subir des navigateurs mal fichus, vous pouvez aussi agir à la source pendant le processus de spécification des standards. Certes, je reconnais volontiers que c'est moins facile que de signaler un bug, mais c'est infiniment plus gratifiant de se dire que l'on a pu avoir une petite influence sur des pans entiers de l'avenir (ouais, rien que ça !). Sachez que toutes les discussions sur la plupart des standards sont publiques. C'est le cas des spécifications [CSS](http://lists.w3.org/Archives/Public/www-style/), [HTML](http://lists.w3.org/Archives/Public/public-html/) ou [ECMAScript](http://www.ecmascript.org/community.php) par exemple. Si vous arrivez avec des suggestions constructives et si vous êtes prêts à répondre à des questions assez pointues, vous serez toujours le bienvenu dans les discussions.

Si discuter frontalement des standards avec des gens parfois très, très, expérimentés vous intimide, vous pouvez tout à fait rédiger des tests permettant de vérifier l'interopérabilité des standards. Vous pouvez le faire via les organismes de standardisation (là encore, il n'est pas rare que le processus soit ouvert et accessible à tous, c'est par exemple le cas de [la suite de test CSS](http://wiki.csswg.org/test)), ou bien le faire dans votre coin comme a pu le faire [le WASP avec les tests ACID](http://www.acidtests.org/).

L’intérêt de cette démarche est double : fournir des retours d’expérience et signaler vos besoins afin que les différents éditeurs puissent prendre les décisions les plus utiles pour vous ; faire progresser l'interopérabilité avant de vous retrouver avec des navigateurs qui font n'importe quoi. Bref, c'est tout bénef’ pour tout le monde.

## Conclusion

Pour finir, je voudrais attirer votre attention sur l'initiative « [Move The Web Forward](http://movethewebforward.org/) » qui vous donnera toutes les clés pour vous impliquer activement dans la création du Web de demain.

Cependant, quoi que vous fassiez, le futur du Web dépend de vous, que ce soit en étant simplement en train de créer un site ou que ce soit en vous impliquant dans la création et la rédaction des standards. Toutes vos actions, aussi petites soient-elles, auront une incidence sur le futur du Web, faites donc attention et sachez que vous avez des responsabilités.

