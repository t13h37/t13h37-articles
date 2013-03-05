# La révolution fracassante et la révolution qui couve

Les images occupent une place importante sur le web et ce à double titre : elles sont souvent le support de l'identité et de la richesse visuelle d'un site, et elles représentent typiquement 40 à 60 % des données transférées entre le serveur et client web lors du premier chargement d'une page. Afin de garantir des temps d'accès acceptables, y compris en mobilité, les outils d'analyse orientés performance web comme Google PageSpeed vous proposeront de consulter leur rubrique « [Optimiser les images](https://developers.google.com/speed/docs/best-practices/payload#CompressImages) ».  
Le but du présent article n'est cependant pas de vous abreuver de techniques d'optimisations semblables à celles du chapitre 5 du *[Book of Speed](http://www.bookofspeed.com/chapter5.html)* de Stoyan Stefanov, mais plutôt de vous présenter deux révolutions récentes dans le domaine des images dont l’ampleur mérite que l’on s’y attarde.

![Répartition des données composant la page d'accueil du Train de 13h37 (édition 10)](break.png "<a href="http://www.webpagetest.org/" hreflang="en">WebPageTest</a> fournit des représentations de la répartition des données composant une page (ici la page d'accueil du Train de 13h37, lorsque l'édition n°10 était à l'affiche).")

## La révolution fracassante : JPEGmini

Il y a près d'un an, ICVT, une start-up israélienne basée à Tel Aviv, a lancé un service d’optimisation des images JPEG en ligne nommé [JPEGmini](http://www.jpegmini.com/) ; une application hors ligne est désormais disponible sur le Mac App Store. Son interface ne respecte pas exactement les canons habituels de Mac OS X mais les résultats, eux, sont assez bluffants avec des fichiers 2, 3, 4 voire 5 fois plus petits que ceux d’origine.

![Aperçu de JPEGmini](jmini.png "Aperçu de JPEGmini")

Le principe de fonctionnement de JPEGmini est de restituer une image JPEG visuellement indiscernable de celle d’origine mais dont le fichier est bien plus petit, il n’y a donc aucun réglage à effectuer. Les algorithmes brevetés par ICVT pour simuler la perception humaine et pousser la dégradation de l’image à la limite de ce qui est décelable fonctionnent visiblement très bien : n'ayons pas peur des mots, c'est révolutionnaire. C'est un peu comme si vous aviez un assistant dévoué chargé d'essayer toute une série de coefficients de compression afin de trouver le plus adapté à chaque image.  
Il y a toutefois une différence importante, outre la vitesse, entre un assistant humain et JPEGmini. En effet, la réglette graduée de 0 à 100 qui permet de choisir le niveau de compression des images JPEG est un élément d'interface bien pratique mais c'est un artifice qui cache quelque chose de légèrement plus complexe : deux matrices contenant chacune 64 coefficients de quantification. La quantification est utilisée pour réduire la précision des données enregistrées car de nombreuses petites valeurs (idéalement des suites de zéros) favorisent la compression, mais si la quantification appliquée est trop importante celle-ci dégrade significativement l'image. Lorsque le curseur de sélection de qualité est déplacé d'un cran il entraîne donc la modification de 128 coefficients d'un coup.  
Chaque logiciel est libre de faire sa propre tambouille à ce niveau, ce qui explique au passage pourquoi la qualité 80 de Photoshop n'est pas la même que celle d'XnView. JPEGmini, de son côté, peut modifier individuellement chacun des 128 coefficients de quantification, ce qui lui permet d'exploiter pleinement cet aspect de la compression JPEG et d'explorer largement plus de combinaisons qu'un malheureux assistant s'escrimant avec sa souris.

![La table de quantification utilisée pour la luminance. Photoshop (qualité 90) et JPEGmini (ad hoc).](qtables.png "La table de quantification utilisée pour la luminance. Photoshop (qualité 90) et JPEGmini (ad hoc).")

En pratique, JPEGmini fonctionne bien mieux sur les gros fichiers qui sont réellement des photographies que sur les fichiers plus petits avec un contenu plus artificiel (texte, pictogramme…) : cela reste du JPEG avec ses limites habituelles. Les images résultantes sont bien entendu directement utilisables avec n’importe quelle application ou navigateur, ce qui permet d'embarquer bien plus d'images sur une clé USB, un *SSD*, un *smartphone*, une tablette ou même… un vieux cadre photo.  
La version gratuite de l'application JPEGmini permet de réaliser jusqu'à 20 optimisations par jour, pour lever cette restriction la version payante est proposée à moins de $20 ou 16 €, le service en ligne existe toujours pour ceux qui n’ont pas de Mac et une déclinaison serveur pour réaliser des traitements par lots est disponible pour GNU/Linux (le prix de cette dernière n’est pas précisé, il est donc a priori assez élevé).

![La suppression des métadonnées et jpegrescan.](jio.png "La suppression des métadonnées et jpegrescan permettent de grapiller encore quelques octets aux images optimisées par JPEGmini.")

L'astuce du jour consiste à utiliser jpegtran et jpegrescan (on les trouve dans [ImageOptim](http://imageoptim.com/)) sur les fichiers issus de JPEGmini.  
Jpegtran ne réalise qu'une optimisation du codage de l’entropie (la façon dont les petites valeurs et les nombreux zéros provenant de la quantification sont inscrits dans le fichier pour prendre le moins de place possible) : cette opération produit des gains bien plus limités par nature, mais c'est toujours quelques centaines d'octets d'économisés.  
Jpegrescan exploite le fait qu'un JPEG progressif peut éventuellement être plus petit qu'un JPEG baseline. Les passes successives d'un JPEG progressif peuvent être configurées de quelques centaines de façons différentes, jpegrescan en essaye un certain nombre. Attention toutefois aux préférences d'ImageOptim concernant la suppression des informations EXIF, car par défaut il supprime toutes les métadonnées (prévisualisation, infos de prise de vue, données GPS...) ; ceci peut être intéressant pour du webdesign mais potentiellement désastreux pour votre bibliothèque de photos.

## La révolution qui couve : WebP

En février 2010, Google a racheté la société On2 Technologies ; de cette dernière, Google a récupéré le *codec* vidéo VP8 et l’a combiné avec le *codec* audio Vorbis pour créer WebM (Web Movie) qui devient un projet open source destiné à concurrencer H.264.  
Quelques mois après la technique de compression des images clés (*intra frame*) de VP8 est réutilisée pour [WebP](https://developers.google.com/speed/webp/) (Web Picture) qui est alors présenté comme une alternative au JPEG (même qualité d’image, fichier plus petit).  
Le problème est qu’il faut disposer de logiciels capables de décoder le format WebP pour pouvoir consulter les images, et aujourd’hui encore il n’y a que deux navigateurs (Opera et Chromium/Chrome) à même d’afficher ce format nativement sans recourir à un greffon.  
Les méthodes de comparaison utilisées par Google lors de sa présentation et le format en lui-même ont essuyé de sévères critiques : sous-échantillonnage de la chrominance limité au 4:2:0 qui était un héritage de son origine vidéo, images produites floues ce qui laissait à penser que le *codec* visait de bons résultats PSNR — *Peak Signal to Noise Ratio* — qui est une forme de mesure de distorsion largement contestée, absence de nouveautés par rapport au JPEG...  
Ces critiques ont été en partie entendues et 6 mois après, un meilleur encodeur a été présenté mais le mal était fait et l'image de WebP sérieusement ternie.

![JPEG vs WebP par Google en 2010.](webp-original.jpg "JPEG vs WebP par Google en 2010.")

Présenté de la sorte, cela semble mal engagé pour WebP… Mais depuis la fin de l’année dernière le développement autour de ce format a repris de plus belle et dans de nouvelles directions.  
Au moment où j’écris ces lignes, [la version 0.1.99 de la bibliothèque libwebp](https://code.google.com/p/webp/downloads/list) vient d'être mise à disposition des développeurs, la dernière ligne droite avant la version 0.2.0 est donc entamée. Celle-ci figera définitivement les nouveautés que je vais vous présenter.

Au niveau des nouveautés majeures, la compression sans perte d'information « *lossless* » fait son apparition ; elle est généralement bien meilleure que celle de PNG. Des fichiers 25 à 30 % plus petits ne sont pas inhabituels, l’encodeur WebP proposé par Google est encore jeune mais il tient facilement la dragée haute face aux ténors de l'optimisation PNG que sont PNGOUT ou PNGWolf.  
WebP sans perte s’affranchit non seulement de certaines limitations de PNG (taille de la fenêtre de recherche, complexité des transformations appliquées à l’image) mais apporte ses propres nouveautés (compression de la palette, exploitation de la proximité bidimensionnelle des pixels...) et a donc quelques cordes de plus à son arc que PNG. Sa complexité n'est toutefois pas excessive, le décodage d'une image WebP sans perte se fait donc en un temps similaire à celui d'une image PNG.

![Image WebP sans perte](webp-interne.png "Dans une image WebP sans perte la majorité des informations est stockée dans l'image ARGB, la sous-image d'entropie (optionnelle) contrôle la sélection des différents jeux de tables de Huffman et la sous-image de prédiction (optionnelle) contient les transformations à appliquer aux pixels pour reconstituer l'image d'origine.")

Cette compression sans perte est mise à profit pour adjoindre la transparence, sous la forme d’un canal alpha, au WebP classique, celui avec perte d'information « *lossy* », ce qui ouvre des perspectives réellement très intéressantes. Les fichiers PNG-32 (RVB+Alpha) ont une tendance certaine à l’embonpoint ; si la partie visible de l'image supporte bien la compression avec perte, on peut espérer produire des fichiers 4 ou 5 fois plus petits. Sur le forum de discussion dédié au format, ceci est parfois considéré comme étant la « *killer feature* » : la fonctionnalité très appréciée qui ferait de WebP un succès à elle seule.

![Le nouveau WebP à l'œuvre, plutôt prometteur…](png-webp.png "Le nouveau WebP à l'œuvre, plutôt prometteur…")

Au niveau du format de fichier tout est désormais en place pour supporter l’inclusion d’un profil ICC et même... l’animation. WebP dans sa déclinaison 2012 peut donc potentiellement remplacer JPEG, PNG et GIF.

Reste le problème de son adoption : pour l'instant les intégrateurs Web connaissent peu le format et ses possibilités. À défaut d'un support d'Adobe dans l'immédiat, il faudra installer un greffon d'import/export (Toby Thain devrait à nouveau être [sur le coup](http://www.telegraphics.com.au/sw/product/WebPFormat) pour produire du WebP avec les outils habituels), ou bien convertir les anciens formats en WebP avec des logiciels séparés (éventuellement directement sur les serveurs).

**Produire certes, mais pour qui ?** Chrome a beau avoir 30 % de parts de marché on peut raisonnablement se poser la question de l'intérêt de la chose, car il faudra nécessairement maintenir les formats historiques pour les navigateurs ne supportant pas WebP. Pourquoi d'autres navigateurs se mettraient-ils à supporter WebP qui n'est ni un standard W3C, ni même un standard de fait… et provenant d'un concurrent de surcroît !?

Là, je vais faire appel à ma boule de cristal (qui vaut ce qu'elle vaut...). Ce qui suit est donc à prendre avec des pincettes.  
C'est probablement de Mozilla que viendra le premier signal d'adoption ou de rejet de WebP : la fondation a jusqu'à présent été très critique envers ce format sans pour autant fermer définitivement la porte à son inclusion dans Firefox (une partie des améliorations récentes sont justement là pour répondre à ces critiques).  
Le nouveau WebP fera partie intégrante de la prochaine version d'Android (non, pas la 4.1, la suivante…) car Google supporte logiquement son propre format, et deviendra de ce fait facilement exploitable par toute application et tout navigateur fonctionnant avec, ce qui est plutôt une bonne chose et sera probablement mis en avant par le service marketing de Google.  
Apple pourrait suivre le mouvement, car disposer d'un meilleur format de compression pour les images est tout de même bien pratique quand on commercialise des écrans « *retina* » et que l'on met à disposition de ses clients des centaines de milliers d'applications depuis ses propres serveurs.
Quant à Microsoft… Hmm…

## Conclusion

Autant JPEGmini a toutes les chances d'être un succès pour son éditeur car basé sur un standard déjà en place, autant l'avenir de WebP est incertain. PNG et JPEG2000 ont montré qu'il faut des années et des années pour qu'un format en remplace un autre ou quelques mois pour totalement disparaître aux yeux du grand public.  
L'inertie qui freine l'adoption de nouveaux formats d'image est peut-être encore plus forte aujourd'hui qu'il y a dix ou quinze ans. À moins que la « *killer feature* » ne produise rapidement son effet et que des milliers d'utilisateurs réclament le support de WebP dans tout ce qui traite déjà le JPEG et le PNG, Google devra procéder à un long travail d'évangélisation plus encore que de développement technique pour assurer le succès de WebP.