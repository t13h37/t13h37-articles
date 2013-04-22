# Introduction aux couleurs dans le Web

À chaque instant, nos yeux réceptionnent des ondes lumineuses plus ou moins intenses. Au fond de nos globes oculaires, des capteurs vont transformer ces ondes en signaux interprétables par notre cerveau pour qu'il puisse nous donner la vue et donc les couleurs. Nos capteurs responsables des couleurs n'interprètent réellement que 3 longueurs d'onde correspondant à 3 teintes : le rouge, le vert et le bleu ! C'est en additionnant l'intensité de ces trois teintes que notre cerveau va pouvoir reconstituer l'infinité des couleurs.

## Tous daltoniens !

Notre vision de différentes teintes dépend donc de deux éléments : les capteurs et l'interprétation faite par notre cerveau.

Environ 9 % des français sont daltoniens. Le daltonisme est un défaut au niveau des capteurs qui va entraîner une interprétation différente des ondes, et donc une perception différente des couleurs. Néanmoins, nous sommes tous (un peu) daltoniens ! N'étant pas des produits de série nos yeux sont uniques et, même si l'écart est infime dans la très grande majorité des cas, nous percevons tous les couleurs différemment.

![Tests de daltonisme d'Ishara](tests-ishara.png "Tests de daltonisme d'Ishara")

Et pourtant, lorsque l'on demande à un groupe de personnes de tous âges et de toutes cultures de désigner dans un nuancier la couleur rouge, la teinte choisie sera la même. Le vocabulaire des couleurs serait-il universel ? Non, par exemple le mot utilisé pour le vert et le bleu est le même pour les islandais !

Oui, j'ose le dire, l'utilisation de la couleur peut devenir un véritable cauchemar car les problématiques de langue ne sont pas les seules rencontrées !

## Des couleurs et des écrans

Nous n'avons parlé, pour le moment, que de la perception de la couleur et non de sa production. Pourtant, lors de la conception d'une interface web, il nous faut bien définir des couleurs.

Ainsi donc, choisissons une couleur correspondant à un turquoise sur le nuancier affiché sur notre écran. Nous récupérons ses coordonnées RVB, c'est à dire l'intensité du rouge, du vert et du bleu dans cette teinte (Rouge : 0, Vert 181, Bleu 204) ce qui se traduit en code hexadécimal en #00B5CC.

![Représentation visuelle de la couleur turquoise présentée dans l'article](turquoise.png "Représentation visuelle de la couleur turquoise présentée dans l'article")

Une fois insérée dans notre feuille de style la couleur s'affiche. Or, si l'on regarde notre site sur un autre écran, la couleur n'est pas tout à fait la même. Pourtant nous n'avons pas changé d'yeux entre temps ! Le problème réside donc dans les écrans, et même plutôt dans leur configuration (ou calibrage). Pour les régler, il existe des profils colorimétriques. L'objectif est que le turquoise renvoyé par notre code soit le même pour tous.

![Affichage d'une même couleur sur deux écrans différents](ecrans.png "Affichage d'une même couleur sur deux écrans différents")

Le hic, c'est que tout le monde n'est pas graphiste : tout le monde ne règle pas la colorimétrie de son écran.

## Couleurs et accessibilité

Il faut donc prendre en compte l'ensemble de ces éléments lors de la conception d'une interface utilisateur. Cela passe par l'acceptation de certains points :

- Non, tous les visiteurs ne distingueront pas ce superbe fond blanc texturé blanc cassé pâle ;
- Non, le jaune que vous avez utilisé dans le texte ne sera pas forcément lisible sur tous les écrans.

Les problématiques d'accessibilité concernent également les personnes daltoniennes (et donc nous tous). Pour nous aider, le W3C a fixé des règles concernant le contraste texte/fond en ne parlant pas de teinte mais de contraste.  
En effet, pour être lisible par tous, il ne faut pas prendre la différence de teinte entre deux couleurs, mais leur différence de luminance (ou d'intensité). La luminance d'une couleur se calcule avec les coordonnées RVB : L = 0,2126 * R + 0,7152 * G + 0,0722 * B .  
Pour un long texte, un rapport de 4,5/1 entre sa luminance et celle du fond est demandée. Ce même rapport est de 3/1 entre un titre et son fond.

Ne paniquez pas, des outils sont là pour vous aider. Je me sers beaucoup des sites : [Contrast Ratio Calculator](http://www.msfw.com/accessibility/tools/contrastratiocalculator.aspx) pour calculer les contrastes et [Check my Colours](http://www.checkmycolours.com/) pour vérifier mes couleurs. Encore mieux, [We are color blind](http://wearecolorblind.com/) vous aide à mieux comprendre ces problématiques.

## Des couleurs, des connotations et des cultures

Avant l'arrivée de la culture occidentale, le blanc était une couleur taboue en Chine où elle signifie le deuil et la tristesse.  
Il est donc important de se renseigner sur les connotations que portent les différentes couleurs principales d'un site Internet pendant son design. Ces éléments non écrits peuvent aussi bien venir de l'histoire, que de la culture ou même de la religion principale d'un pays ou d'un territoire.  
De plus, les teintes influenceraient également notre psychisme et notre organisme : 55 % des athlètes ayant remporté une médaille à Athènes portait du rouge. Un lien de cause à effet ?

Alors quelle couleur pour quel usage ?  
Voici deux infographies résumant bien les différentes connotations :

- [Une visualisation de données sur les couleurs dans la culture](http://www.informationisbeautiful.net/visualizations/colours-in-cultures/) ;
- [Une infographie sur les connotations des couleurs](http://printmediacentr.com/2011/02/infographic-the-psychology-of-color-for-web-design/).

Il ne faut pas oublier non plus que les choix de couleurs peuvent être subjectifs. « Ma couleur préférée, c'est le vert kiwi ». Ce n'est pas parce que nous (ou notre client) aimons une couleur que celle-ci sera adaptée au site. Il est donc souvent plus intelligent de laisser ses goûts et couleurs favorites de côté pour leur préférer des teintes qui véhiculent des connotations correspondant aux usages voulus pour les utilisateurs. À moins de créer des sites artistiques ou personnels.

## Associer des couleurs

Une couleur et des nuances de gris : voici le choix le plus sûr lorsque l'on choisi les teintes de son site Internet. Mais si l'on souhaite utiliser plusieurs couleurs ? Comment ne pas trop prendre de risque en choisissant deux ou trois teintes différentes ?  
Si aucune règle absolue n'existe (on a vu des alliances de rouge et de rose réussies), des outils comme les roues chromatiques permettent de minimiser ces prises de risque.

Comment fonctionne une roue chromatique ? Elle se base sur des règles d'association des couleurs physiques comme les complémentaires (le rouge et le vert, le bleu et l'orange, le jaune et le violet), les triadiques... pour créer des harmonies « conventionnelles ». 

![Aperçu d'une roue chromatique montrant des couleurs complémentaires](roue-chromatique.png "Aperçu d'une roue chromatique montrant des couleurs complémentaires")

Attention ! Aussi pratiques que soient les roues chromatiques, il ne faut pas oublier que la perception d'une couleur dépend aussi de son environnement. Le même turquoise paraîtra plus clair sur un fond noir que sur un fond blanc. 

![Perception d'une couleur en fonction de la couleur qui l'entoure](meme-couleur.png "Perception d'une couleur en fonction de la couleur qui l'entoure")

Adobe fournit des outils très pratiques dans Illustrator et Photoshop, ainsi qu'[un site dédié à la construction d'une palette](http://kuler.adobe.com).

Enfin, pour aller plus loin sur les couleurs, vous pouvez regarder la très belle conférence de David Rault à Paris Web 2011: [les goûts et les couleurs](http://www.slideshare.net/ozeb14/les-gouts-et-les-couleurs-david-rault-parisweb-2011).

## Conclusion

Les couleurs sont un des éléments qui composent un *webdesign*. Et en cela, elles ne doivent être qu'un moyen au service des objectifs du site : 

- Je souhaite mettre en valeur les images/photographies sur un site ? Mon nuancier va s'orienter dans les nuances de gris pour ne pas « jurer » avec les couleurs des photos ;
- Je réalise le site *corporate* d'une entreprise ? Les couleurs dépendront totalement des teintes présentes dans son logotype pour créer une identité visuelle : leurs connotations ne sont pas essentielles...

Au final, l'essentiel est de trouver le bon équilibre entre le contexte, les cibles, les objectifs du site, les connotations, le goût, les associabilités, la lisibilité et surtout le temps que l'on a à consacrer à ces choix.
