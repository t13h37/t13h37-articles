# Aide-toi, le Web t’aidera
    
Dans ce milieu d’autodidactes ultra-connectés qu’est le Web, rester bloqué sur un problème technique ne dure jamais longtemps. Il existe mille et une façons de trouver un coup de pouce quand on sèche. Malgré tout, cet article n’a pas pour objectif de dresser une liste complète des ressources à consulter en cas de coup dur – tâche interminable s’il en est, et surtout, ô combien subjective.

Je crois fondamentalement que les retours d’expérience les plus utiles sont ceux qui font la part belle aux difficultés rencontrées. Dans cet article, je vais donc partager avec vous la démarche personnelle que j’utilise lorsque je suis confrontée à un problème technique dans mon activité professionnelle quotidienne.

## Le coup de flip initial

Que la vie est belle quand on exerce un métier qu’on a choisi et qui nous plaît encore, tant d’années après ! 

Il était une fois la délicieuse routine de l’intégrateur web : commencer à intégrer un site, se donner corps et âme à un code clair, sémantique et accessible, tester de nouveaux outils, expérimenter de nouvelles méthodes de codage, améliorer ce qu’on a moins bien fait la fois d’avant, participer à un Web plus ouvert et plus utile.

Et tout à coup, crac ! Ici, un bug velu ; là, une embuscade technique. Les coups de flip font partie du jeu ; les cheveux arrachés de rage, les larmes de sang et les insultes proférées à voix haute dans l’*open space*, aussi.

Si mes coups de flip ont tendance à se raréfier, l’expérience aidant, ils sont également devenus plus sournois et plus intenses : en effet, les défis qu’on me propose sont à chaque fois plus énormes et plus impressionnants que les précédents. J’ai à peine le temps de savourer ma précédente réussite que je retombe au niveau 1 de la mission suivante.

Ainsi, quand on m’a annoncé que j’allais devoir transformer des tableaux de données dynamiques en diagrammes circulaires SVG pour un de nos plus gros clients, j’ai flippé. J’ai flippé car je ne savais pas du tout dans quoi je mettais les pieds. Les démos monstrueuses à base de SVG que j’avais vues passer sur Twitter m’avaient donné l’impression que tout ça était compliqué et que j’allais forcément galérer.   
Le SVG, je voyais en gros ce que c’était : un format de formes et d’images vectorielles, qui permettait enfin de s’affranchir de la dictature du *Bitmap* et de concilier en un tour de main illustration, données et écrans à densité variable de pixels. Un outil surpuissant, prometteur mais encore peu utilisé. Je sentais que j’allais galérer, et je concède un sérieux coup de flip quand j’ai appris que c’était à moi que revenait la tâche de s’en occuper.

Mes coups de flip sont reconnaissables entre mille : indétectable sur le moment puis rapidement embarrassant, un masque de sueur commence à recouvrir mon visage, mes joues s’empourprent en un éclair, et mon regard, soudain absent, s’obstine à fixer le Velux devant moi, cherchant désespérément une issue.   
Et, comme si la décomposition physique ne suffisait pas, le cerveau en rajoute une couche, en se répétant en boucle : « Je ne vais pas savoir faire, ils vont découvrir que je suis *nulle* ! » – autant de phrases démotivantes qu’auront reconnues ceux parmi vous qui, comme moi, sont atteints du syndrome de l’imposteur.

Cette fois-ci, il s‘agissait de générer du SVG avec du JavaScript. Mais il aurait tout aussi bien pu s’agir de parallaxe, d’animations CSS ou bien d’AJAX, autant de domaines dans lesquels je ne me sens pas très à l’aise, pour que je flippe aussi. Et que dire des odieux bugs que nous servent sans se lasser Internet Explorer, Opera ou encore iOS, qui n’aiment rien tant que de se produire pile quand les circonstances ne s’y prêtent pas (*deadline* dépassée, accès à Internet en berne, démo à un client, etc.) ?

## Ne pas rester bloqué

29 août 2011 : on y est. La grosse refonte pour l’énorme client commence. Les jours passent, l’intégration avance, et je compte les jours qui me séparent de mes premiers pas en SVG. Je stresse à mort. 

Pour me calmer les nerfs, j’ai pensé que ça serait une bonne idée d’aller lire quelques tutoriels sur SVG et de voir un peu comment sont construites les démos qui me font rêver. Peine perdue : découragée par le déluge de code abscons, je referme d’un clic nerveux tous les onglets concernés. Outre le fait que cela m’a découragée, j’ai aussi perdu un temps précieux à lire des tutoriels trop compliqués pour ce que j’ai à réaliser.

Le vrai premier réflexe à avoir, c’est de faire part de ses doutes au chef de projet. C’est une étape importante, tout d’abord car il peut vous orienter vers un collègue plus expérimenté que vous dans ce domaine précis, ou bien vous présenter une méthode ou un outil auxquels vous n’aviez pas pensé. Mais cela va aussi vous permettre de l’avertir que vous allez sans doute avoir besoin d’un peu plus de temps que prévu pour réaliser ce qui est attendu de vous (surtout si vous n’avez pas été consulté(e) en terme de charge, ce qui m’arrive, personnellement, assez souvent).

En l’occurrence, en avoir parlé d’emblée au chef de projet m’a ôté une énorme épine du pied. Par chance, ce collègue est calé en SVG et me conseille d’utiliser une librairie JS pour générer mes diagrammes. C’est une excellente idée, à plus d’un titre : d’une part, parce que les éléments que je dois intégrer s’y prêtent bien, et d’autre part, parce qu’il est inutile de réinventer la roue, surtout quand on débute dans une discipline. En plus, cette librairie – [Raphaël](http://raphaeljs.com), en l’occurrence – repose sur des démos sympas  qui titillent l’imagination de la créative que je suis. La documentation, quant à elle, est claire et je démarre, un peu plus sereine. 

Je réalise qu’aller lire le code de démos hyper-compliquées n’était peut-être pas la chose la plus intelligente à faire et que, quand on débute avec un langage, il faut avoir l’humilité de commencer par apprendre le B.A.-BA. Si le métier d’intégrateur Web concerne historiquement HTML et CSS, il s’est enrichi au fil des années d’autres langages *front-end*, qui ne sont pas forcément aussi faciles à maîtriser.

En l’occurrence, les choses se compliquent pour moi quand il faut faire des maths, imaginer des équations et transcrire tout ça en JavaScript. Sueur, tachycardie, auto-dépréciation : j’ai le sentiment de revivre les heures sombres de mes années collège. Non seulement je suis bloquée, mais en plus, aucun de mes collègues n’est disponible pour en discuter. C’est dommage, car verbaliser le problème aide bien souvent à trouver une ébauche de solution. À la place, je dessine rapidement un petit schéma, ce qui me permet de cerner plus facilement le problème.

Puis, j’enfourche mon fier destrier et pars en quête d’un paquet de tutoriels, copiant-collant des lignes de JS, rafraîchissant la fenêtre de mon navigateur environ un demi-million de fois. J’expérimente, j’échoue, j’essaie encore. Entre abandonner et déclarer forfait, je préfère m’entêter.

Ces difficultés me feraient presque regretter de ne pas être une matheuse, dites donc. Impressionnée, négativement, par le challenge technique, ma motivation ne tient qu’à un fil. Et puis je me raisonne : j’ai à ma disposition tellement de ressources, je vais *forcément* y trouver une piste à suivre.   
Et je finis par la trouver, cette piste. Mes lectures nourrissent ma réflexion, et j’emprunte quelques idées le temps de terminer l’exercice.

Le soir, avant de m’endormir, j’attrape un manuel de JavaScript afin de réviser un peu et de me rafraîchir les idées. Comme je n’ai pas un esprit toujours très logique, lire le raisonnement d’un expert m’aide à conceptualiser plus précisément ce que j’essaie de faire. Et ça marche, j’ai de nouvelles idées que je suis impatiente de mettre en pratique.

Le lendemain, j’en discute sur Gtalk avec un autre collègue, plus matheux que moi, qui me donne un lien vers un tutoriel génial qu’il avait lu une semaine auparavant, et qui pourrait m’aider.   
J'expose également le problème sur Twitter, au cas où.

L’essentiel, c’est de ne pas rester bloqué, car l’heure tourne et les *deadlines* sont rarement négociables. Il faut donc activer tous les moyens qu’on a à sa disposition pour surmonter l’obstacle.

Face à une difficulté, solliciter ses collègues – ceux avec qui on travaille mais aussi ceux qui font le même métier que soi – n’est pas une option, c’est une obligation. Sur le mode du « 1 + 1 = 3 », les problèmes de l’un se nourrissent de l’expérience de l’autre pour donner naissance à une troisième approche, propre au projet. Le savoir collectif est précieux, il faut en user et en abuser, surtout dans un domaine mouvant comme le Web, où il existe toujours plusieurs méthodes pour aboutir au même résultat : la méthode d’autrui contiendra sûrement l’élément qui manquait pour que notre méthode à nous fonctionne, parce que son regard est différent du nôtre, et que nos cerveaux ne fonctionnent pas tout à fait de la même façon.

Par orgueil, il m’arrive de m’acharner sur un bug en particulier, pour lequel je peux sacrifier deux heures de travail, sans forcément aboutir à un résultat probant. C’est une démarche stérile. Passer deux heures sur un bug, c’est deux heures de trop. Il faut savoir lâcher prise et revenir sur le problème plus tard, par exemple après avoir laissé passer une nuit de sommeil. Il arrive que l’affreux bug velu qui me traumatisait la veille ne soit plus qu’un petit moucheron inoffensif que j’atomise en deux minutes le lendemain. 

Après des heures d’entêtement, il m’est aussi souvent arrivé que le problème soit résolu en cinq minutes, mais pas par moi : simplement en montrant le problème à un de mes collègues. Son regard frais neuf sur le projet lui a permis d’avoir le recul nécessaire pour débusquer la cause du bug, là où moi j’avais trop la tête dans le guidon pour m’en apercevoir. Si je l’avais sollicité tout de suite, et si je n’avais pas attendu d’avoir perdu mon temps, j’aurais économisé des heures précieuses, et aurais sans doute terminé l’intégration du projet de façon plus sereine (économiser une heure par-ci, une heure par-là permet de constituer une soupape de sécurité bien appréciable en fin de projet).

Quatre-vingts pour cent de mes coups de flip sont liés à mon inattention. Pour les 20 % restants, l’essentiel pour moi est d’identifier le plus précisément possible le problème, afin d’en tirer quelques mots-clés qui vont me permettre de lancer une recherche sur le Web. La bonne nouvelle, c’est qu’il y a toujours quelqu’un d’autre que moi qui a eu exactement le même souci ou dont la situation a été très similaire à la mienne, et qui a posé la question avant moi sur un forum, ou, mieux, qui y a consacré un article de blog.

L’essentiel, ce n’est pas tant le nombre de ressources dont on dispose : c’est surtout de savoir formuler son problème, sa question, de la manière la plus simple et la plus générique possible, afin d’augmenter les chances de trouver *le* message qui va nous sauver la vie.

Je n’ai jamais été aussi reconnaissante à la communauté des professionnels du Web de prendre le temps de partager leurs connaissances sur leurs blogs, sur les forums, mais aussi en écrivant de la documentation, en animant des ateliers, en donnant des conférences – le tout bénévolement.

Récemment, j’ai commencé à prendre le temps, à mon tour, d'écrire un article sur mon blog dès que je trouve la solution à un gros problème technique, comme ça m’arrive de temps en temps avec WordPress. Au moment de rédiger ces articles cependant, je me demandais si, vraiment, cela allait servir à quelqu’un (le syndrome de l’imposteur, vous vous souvenez ?). Des doutes bien inutiles puisque, en six ans de blog, ces articles-là m’ont ramené plus de visites, plus de *backlinks* et plus de commentaires que j’en ai jamais eu. Moralité : partager ses connaissances n’est jamais une perte de temps. Laisser une trace des difficultés qu’on a rencontrées servira forcément, un jour ou l’autre, à quelqu’un – ne serait-ce qu’à soi-même, quand on aura besoin de se rafraîchir la mémoire.

## Un pas de géant
En me relisant, des mois plus tard, je constate le chemin parcouru. N’avez-vous jamais atteint cet optimum, cet instant-clé, où vous réalisez tout à coup les progrès énormes que vous avez faits ? Ce sain sentiment de satisfaction qui vous étreint pendant quelques minutes, où, tout orgueil mal placé mis à part, vous comprenez que vous avez fait un immense pas en avant, techniquement, graphiquement, humainement ? 

Les diagrammes SVG dont je vous parlais ont été un pas de géant pour moi. Pas parce qu’ils représentaient une réussite technique extraordinaire, mais parce que, sur le moment, j’ai saisi avec réalisme que j’avais franchi une étape, que ma réflexion ne serait plus jamais la même et que, désormais, je saurais m’en sortir toute seule comme une grande face à une problématique similaire.

Nous tous avons la chance de bénéficier d’une communauté active et viscéralement passionnée. L’entraide est au cœur de nos métiers, car nous avons tous été plus ou moins autodidactes, et nous avons tous apprécié, à un moment donné, d’avoir bénéficié des lumières de nos semblables pour avancer.

Aucun d’entre nous n’a la science infuse : tâtonner, se tromper, voire paniquer, est *normal*. Et c’est plutôt bon signe : c’est la preuve que nous continuons à apprendre, et que nous ne nous reposons pas sur nos acquis.   
Et, lorsque nous avons appris quelque chose, partageons-le à notre tour. Documentons nos réussites *et* nos échecs. Ne privons pas autrui de nos connaissances, en particulier si nous avons rencontré des difficultés. Nous ne sommes pas les premiers, ni les derniers, à devoir les affronter.


## Conclusion

Ainsi, quel que soit le problème technique auquel on se retrouve confronté, l’essentiel est de ne pas rester paralysé. Il est nécessaire d’activer plusieurs canaux d’information pour s’informer et trouver une solution. Nos aïeux avaient à leur disposition des bibliothèques pour puiser leur savoir ; nous, en plus des livres, nous avons le web à notre portée, cet océan infini de connaissances, dans lequel les bouteilles à la mer arrivent toujours à bon port, et où nous pouvons à tout instant poser nos questions avec la quasi-certitude qu’une bonne âme nous répondra.

Dans l’adversité, cette citation de Lao Tseu m’aide toujours à prendre du recul et à garder le sourire : « Si tes résultats ne sont pas à la hauteur de tes espérances, dis-toi que le Grand Chêne aussi, un jour, a été un gland. »  
CQFD.
