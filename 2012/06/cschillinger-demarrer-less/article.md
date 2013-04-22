# Bien démarrer avec LESS #

D’un développeur à l’autre le choix du préprocesseur varie : suivant le profil et les affinités de chacun, telle solution peut sembler plus appropriée que telle autre.
Cependant, quel que soit l’outil finalement retenu, vient inévitablement ce petit moment de flottement où il faut sauter le pas et commencer à l’utiliser. Or, ce n’est pas toujours facile, faute de ressources appropriées permettant d’en appréhender correctement le fonctionnement.

Cela fait maintenant plus d’un an que je travaille avec LESS. Voici une compilation de ressources qui, je l’espère, devrait vous permettre de commencer à l’utiliser sans difficulté.

## Les applications

LESS est un langage qui nécessite d’être compilé pour pouvoir être interprété par les navigateurs.  Il existe plusieurs compilateurs disponibles dans différents langages : JavaScript, PHP ou Ruby, pour ne citer que ceux-là.

Cependant ils ne présentent pas tous les même avantages : le compilateur JavaScript est certainement le moyen le plus facile de tester LESS en situation réelle. Mais, il ne doit en aucun cas être utilisé en production côté client [^1], pour des questions de performance.
En effet, le code est compilé à la volée, ce qui rend impossible toute mise en cache de la feuille de styles et impose au code LESS d’être re-compilé à chaque chargement de page. De plus, si —pour une raison ou pour une autre— le JavaScript n'est pas activé, le code CSS n'est tout simplement pas généré, ce qui a pour conséquence de priver le contenu de toute mise en forme.  
L'utilisation du compilateur JS côté serveur est beaucoup moins problématique, puisque le fichier généré peut être mis en cache. Cependant, dans la majeure partie des cas, il est préférable d'éviter au serveur toute tâche inutile en lui livrant directement le code CSS. [^1]

À la place, il est préférable de se tourner vers une application desktop, qui est sans nul doute la solution la plus simple pour intégrer LESS à la chaîne de développement. Elle compile automatiquement le code CSS et rend son utilisation complètement transparente : le fichier CSS est généré et mis à jour à chaque fois que le fichier LESS est sauvegardé. Pratique, non ?

Fait appréciable, il existe au moins une application pour chaque système d’exploitation :

- [SimpleLESS](http://wearekiss.com/simpless) pour Windows, Mac et Linux.
- [WinLESS](http://winless.org/) pour Windows.
- [LESS.app](http://incident57.com/less/) et [Codekit](http://incident57.com/codekit/) pour Mac. Contrairement aux applications précédemment évoquées, Codekit présente l’avantage de pouvoir compiler plusieurs langages, tels que SASS, Stylus, HAML ou CoffeScript. Le [prix de la licence d’utilisation](https://incident57.com/codekit/buy.php) varie entre 20 et 28 $ : à vous d’en estimer sa juste valeur.
- [LiveReload](http://livereload.com/) est un bon équivalent à Codekit, dans le sens où il est, lui aussi, capable de compiler plusieurs langages. Son petit “plus” réside dans le confort d’utilisation qu’il offre, puisqu’il met automatiquement la page à jour dans le navigateur : s’il s’agit d’une modification qui impacte le code CSS ou les éléments tiers telles que les images, seuls les composants impactés sont redessinés. À l’inverse pour toutes les autres modifications (HTML, PHP ou JS par exemple), l’ensemble de la page est rafraîchie.  
Pour permettre à Livereload de fonctionner correctement, il suffit d’installer l’une des extensions disponibles, ou d’insérer un petit *snippet* JavaScript juste avant la balise `<body>` de la page.
	- Actuellement, seule la version Mac est réellement fonctionnelle. [Elle est proposée au tarif de  7.99€](http://itunes.apple.com/fr/app/livereload/id482898991?mt=12)
	- [La version Windows](http://download.livereload.com/LiveReload-0.0.4-Setup.exe) n’en est, pour sa part, qu’au stade pre-alpha.</li>
	- Enfin pour les utilisateurs de Linux, [le projet guard-livereload](https://github.com/guard/guard-livereload) semble constituer une alternative intéressante.

![Copie d'écran du site de SimpleLess](simpleless.png "SimpleLESS, l'une des rares applications qui soit disponibles sur Windows, Mac et Linux")

Ceci étant dit, il me semble important de mentionner que si certaines applications proposent de regrouper la compilation et la minification du code en une seule et même étape, cela n’est pas nécessairement une bonne idée. Il peut, bien souvent, s’avérer utile de faire une passe de vérification et de nettoyage sur le code CSS obtenu : il arrive que certaines portions de code soient inutilement détaillées. Bien sûr, il convient de re-vérifier l'intégralité du fichier à chaque nouvelle compilation, puisque les modifications apportées au code CSS sont écrasées à chaque fois que ce dernier est re-compilé. [^1]

## Le guide de démarrage

![Extrait de l'atelier LESS à la Kiwi Party 2011](guide-demarrage-less.png "Extrait de l'atelier LESS à la Kiwi Party 2011")

Donné mi-2011 à l’occasion de la Kiwiparty, l’atelier « LESS : moins de CSS, plus de fun ! » a été pensé comme une introduction au langage et à ses subtilités. [Le support de présentation](http://www.slideshare.net/inseo/less-css-avril-2011) n’a pas vocation à être exhaustif sur le sujet, loin de là. Cependant, il met en situation les différentes fonctionnalités de LESS et permet de comprendre rapidement l’intérêt que présente son utilisation.

## La documentation officielle

![Aperçu du site lesscss.org](doc-officielle-less.png "Aperçu du site lesscss.org")

Agrémenté de nombreux exemples illustrants les différentes possibilités de LESS, [le site officiel](http://lesscss.org/) constitue une excellente source de documentation. Maintenue par le concepteur du langage et mise à jour au gré des versions, elle permet de se tenir informé des évolutions apportées.

## La boîte à outils

![Extrait du code fourni par lesselements.com](outils-less-elements.png "Extrait du code fourni par <a href="http://lesselements.com">lesselements.com</a>")

[LESS Elements](http://lesselements.com/) est une collection de classes LESS prédéfinies et prêtes à l’emploi. Elle constitue un excellent support pour comprendre et approfondir le mécanisme du préprocesseur. Son principal intérêt est d’inclure, pour chaque classe, l’ensemble des propriétés préfixées adéquates, ce qui permet de simplifier grandement leur mise en place.  
Cependant plutôt que de les utiliser telles quelles, il est préférable de s’en inspirer et de les adapter en fonction des besoins réels. Car, suivant les cas, elles peuvent parfois être bien plus verbeuses que nécessaire.

## Le service en ligne

![Aperçu de l'outil en ligne CSS2LESS](css2less-online.png "Aperçu de l'outil en ligne CSS2LESS")

Cette dernière ressource est un outil qui permet de transformer un code CSS en LESS : [CSS2LESS](http://css2less.cc/) permet de ré-agencer le contenu d’une feuille de styles pour qu’elle adopte le format LESS. Malheureusement cet outil n’est pas magique et atteint bien vite ses limites : il ne prend en charge que la réorganisation du code sous forme de déclarations imbriquées.  
Il s’avère donc particulièrement utile dans un contexte donné, qui est la reprise de code en vue d’un passage à LESS.

Voilà, j’espère que ces quelques outils vous permettront de sauter le pas plus facilement.  
N’hésitez pas à partager vos ressources !

**Notes :**

[^1]: Mise à jour du 19/06/2012
