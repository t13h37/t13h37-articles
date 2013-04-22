# Performance web mobile, chargement de page 2/2

## Reprioriser les optimisations

On l’a vu, certaines techniques pourtant reconnues peuvent devenir contre-productives si l’on ne fait pas les tests nécessaires. Ne jetons cependant pas tout aux orties, voici les techniques que vous devrez maîtriser plus que jamais et pousser dans leurs extrêmes si vous voulez obtenir un résultat correct sur mobile ; par ordre de priorité :

### 1. Travailler le chemin critique

La notion de performance est plus un ressenti qu’une collection de chiffres. Lorsque vous devez retravailler une page pour un réseau mobile, demandez-vous ce que l’utilisateur est vraiment venu voir et dégagez le passage pour afficher au plus vite la zone ou la rendre fonctionnelle :

- pas (trop) de redirections, et surtout pas côté client ; 
- concaténation ou mise en ligne des CSS ; 
- un code HTML / CSS prêt à "marcher" sans JavaScript : pour un article, c’est facile, on affiche le texte (sans police de caractère, jamais) ; pour une vidéo, on peut utiliser HTML5 comme interface de lecture en attendant JavaScript. Si vous dépendez de JavaScript pour afficher la fonctionnalité (un *webmail* par exemple), affichez au moins un indicateur de chargement ; 
- scripts asynchrones comme vu plus haut ; 
- JavaScript chargé et exécuté par ordre de priorité : on peut très bien imaginer de charger d’abord les fichiers JavaScript concaténés qui concernent la zone principale, puis un second pack de fichiers qui concerne tout le reste de la page. 

### 2. Minimiser le nombre de requêtes HTTP

On l’a vu lors de l’exemple du *domain-sharding*, la première limite vient du réseau : le même mobile sur la même session de surf pourra passer d’un WiFi de bonne qualité à une absence complète de réseau. Vous ne pouvez jamais prévoir quand la latence va s’allonger jusqu’au *timeout* ou quand le débit passera en dessous de ce dont vous auriez besoin pour afficher une simple image. En supposant que vous serviez votre site classique sur mobile (1 Mo, 100 requêtes, 15 domaines... [source http archive](http://httparchive.org/trends.php)), il va falloir faire baisser de manière drastique le nombre de requêtes pour minimiser les effets de latence ou de *timeout* et maximiser l’utilisation de la bande passante. Cet objectif est là pour durer et la plupart des techniques classiques utilisées jusqu’ici sont non seulement à investiguer, mais à pousser dans leurs extrêmes.

#### La concaténation

Il est plus que jamais temps de faire de vos CSS et JS des fichiers uniques ou presque. De base dans [Ruby on Rails](http://rubyonrails.org/), avec des plugins divers pour [Spip](http://www.spip.net/) ou [Drupal](http://drupal.org/), avec [Assetic pour Zend 2](https://github.com/widmogrod/zf2-assetic-module), des dizaines de librairies pour d’autres projets PHP, avec [SASS](http://sass-lang.com/) côté CSS et des outils comme [YUI Compressor](http://yuilibrary.com/projects/yuicompressor/).
Il n’y a plus vraiment d’excuses pour ne pas gérer correctement vos JS et CSS, sauf peut être le coût de *refactoring* initial, mais il reste généralement négligeable par rapport aux bénéfices attendus.

À noter que les stratégies de concaténation vont varier en fonction de la taille de votre site : si il est relativement petit, mettez tous vos CSS dans une seule feuille ; si il est plus grand, mettez le CSS commun dans une première feuille et les CSS de chaque type de page dans une autre. Ne dépassez jamais 2 feuilles par page. En JavaScript, les stratégies sont plus variées du moment que vous utilisez l’asynchrone : un fichier unique pour tout le site si il est petit, un fichier par zone fonctionnelle sinon (avec chargement asynchrone).

#### Les images

Les images sont généralement petites et nombreuses, c’est donc votre seconde cible après le CSS. Vous avez forcément déjà entendu parler du *[spriting](http://www.alsacreations.com/tuto/lire/1068-sprites-css-background-position.html)* ; sur mobile, vous pouvez aller encore plus loin avec les caractères Unicode : lorsque vous avez beaucoup d’icônes, essayez de voir si vous pouvez en réutiliser (♻) qui viendraient directement des polices du système !
Attention à la compatibilité navigateur ET système d’exploitation. Pour les mobiles, c’est généralement bon ; pour IE sur XP, vous n’aurez qu’un choix limité.

Encodage des images : visez le zéro requête en encodant vos images en texte directement dans le CSS, voire dans le HTML. C'est un peu fastidieux à faire à la main mais un simple script PHP suffit :

~~~ {lang="php" line="1"}
print '<img src="data:image/png;base64,'.base64_encode(file_get_contents('/path/to/image.png')).'" />';
~~~

Qui vous donnera en sortie quelque chose de ce genre :

~~~ {lang="html" line="1"}
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAABO1BMVEX92RlCQj+7vLzvzSzmhgnXgybyz3uLj5T13mj99cDwrmWMfzXmyTz78bT1zUf++uX437bxzqzmpj/dlDdcVUbuxnjszDLq6uvqmS/43Hv99t+foaOMgl5tYDjsu1vfwT388NijlXr52Vn22Y3999Z2bmD34svhrFlQTD378ajuwWXThzH668PpsFbvw5zrtU2Vh03x0Y3MzMz73kr664qZmZnmnUblqm/7w1HokRbefBb//e324HL2z0TsuENYRC399s/343z46paYijr88s/z1KXvyIvspkzroTj81yL56cnajjLwxm9KSkLmqj1gVj+Xg2H3vkv+/tz35XL+3CD89cj45Lf88MSipab13FnvtGP224T45Yb78rr++uv3zij25Grz1Ub1yi7wxFztu2vYiTH95kfqs2v45csXvxkaAAAAAXRSTlMAQObYZgAAAMlJREFUaN5jYAACY0llQzafZFsGCAiJDvNSkJJSEEjR9wQLROvw86s4OISqxLkJgfhKYfz8/NZA4MBrnW4HFGBzkZKKAwlIxWpmCAMFRKVCQ1VUXFzCY52CpVKBAlpeKo4xUVFR7jGRJmreQAE+N2sbCRsbDhuWxCBzP5Cpcq5BHjYJCTaWnIKsYHs9dV25bIDAXY81CeIyT3WzwLQ0CyvteKhTGcQCFJ25Ve2ZGeBAJiLClN0fwWcwYBI3kpZFEuAR8WXUkGfACgC55CKssDjPhQAAAABJRU5ErkJggg==" />
~~~

Des frameworks complets comme SASS permettent de le faire dans le CSS. Vous pouvez utiliser cette technique à partir de IE8, et envisager [l’équivalent MHTML](http://www.phpied.com/the-proper-mhtml-syntax/) pour IE7.

#### Le nombre de domaines

Le site moyen a entre 10 et 15 domaines à faire résoudre et il n’y a pas eu d’études sur l’utilisation du cache DNS sur mobile. Pratiquement invisible sur ordinateur de bureau, le coût de recherche DNS est peut être dix fois plus important sur mobile à cause de la latence. Chaque recherche de domaine va bloquer une file de téléchargement en attendant la réponse. Donc, soit vous sacrifiez *trackers*, publicité, widgets et autres sources externes, soit vous les dépriorisez fortement, tout simplement en les appelant après vos propres fichiers.

### 3. Le cache et l’*offline*

Comme avant, il va falloir que vous commenciez par maîtriser absolument toutes les URLs vers les statiques de votre site pour pouvoir les servir avec des caches agressifs, sur des domaines sans cookies. Ça c’est surtout pour les navigateurs de bureau car [le cache des navigateurs mobile est une vraie calamité](http://www.guypo.com/mobile/understanding-mobile-cache-sizes/) en terme d’efficacité ! Il y a beaucoup trop de limites (nombre d’objets, taille maximale par objet, taille maximale par site et taille maximale pour tout le navigateur) pour espérer de vrais gains avec les comportements par défaut mais il ne faut pas les ignorer pour autant.

Les sites très efficaces en sont donc à utiliser HTML5 *localStorage* pour stocker des JS, des CSS et même des images (encodées en base64). C'est la technique choisie par LinkedIn mobile, Bing ou GMail, et elle demande un certain niveau de maîtrise de son application. Par exemple, imaginez-vous sur une page d’accueil : vous allez télécharger via XHR tous les objets dont vous avez ou aurez besoin, puis les stocker dans *localStorage*.

~~~ {lang="javascript" line="1"}
var loader = new XMLHttpRequest();
loader.open("GET", "http://example.com/js/main.js");
loader.onload = function(e) {
    localStorage.setItem('main.js', e.response);
}
loader.send();
~~~

Ensuite, au moment ou vous en avez besoin, vous vérifiez la présence des fichiers voulus dans votre cache maison.

~~~ {lang="javascript" line="1"}
if( localStorage.getItem('main.js') !== null ) {
    eval( localStorage.getItem('main.js') );
}
~~~

Oui, vous faites à la main le boulot du navigateur (télécharger, gérer le cache, insérer...) mais c’est avec ce genre de code un peu extrême que l’expérience utilisateur sur mobile fera la différence. En prime, les navigateurs de bureau en profiteront aussi.

Une note pour ceux qui ont entendu dire que *localStorage* était contre-performant car synchrone (lorsque vous écrivez, vous bloquez le programme le temps que le disque ait fini de travailler) :

- c’est évitable facilement en passant par un *wrapper* qui va simplement effectuer l’écriture en asynchrone ; 
- les mobiles écrivant tout en RAM / *Flash disk*, les temps d’accès sont de toute façon négligeables. 

Vous pouvez encore passer au niveau supérieur en utilisant une technique qui a autant fait ses preuves que montré ses limites : l’utilisation de la [spécification Application Cache](http://appcachefacts.info/). Native, bien supportée par tous les navigateurs modernes mobiles ou de bureau, elle permet de déclarer en un fichier (le manifeste) quels sont les fichiers à télécharger, quelles ressources doivent continuer à être servies en ligne, et quoi afficher lorsque la connexion n’est plus là. Au contraire de la gestion du cache présentée précédemment qui est personnalisée et donc très adaptée à votre application, Application Cache vous force à coder d’une certaine manière (maîtriser absolument toutes ses URLs), présente certains manques (invalider le cache de certains fichiers seulement) et il faut un petit temps d’adaptation pendant la phase de développement pour comprendre son fonctionnement intrinsèque. En revanche, en terme de performance et de mode de distribution, c’est parfait !

### 4. Réduire la taille

#### Minification et compression des JS / CSS

La minification est généralement exécutée au déploiement du site juste après la concaténation et vous pouvez généralement gagner 50 % du poids des fichiers avec des outils solides comme [YUI Compressor](http://yuilibrary.com/projects/yuicompressor/). Activez la compression gzip par-dessus et vous aurez gagné au final 90 % du poids initial de vos fichiers. Sachant qu’il n’est plus rare de trouver des sites avec 200-500 Ko de CSS et de JS, le gain est assez important.

#### Les photos

Pour les images de l’interface, comme pour les photos, vous avez beaucoup à gagner en compressant au maximum les images servies. Encore plus efficace : ne les afficher que si elles sont nécessaires. Dans le cas d’une application Web Mobile ou l’interface permet de beaucoup scroller, considérez comme une amélioration majeure de faire du *lazy-loading* sur les images, c’est à dire de ne télécharger l’image que lorsqu’elle est sur le point d’être affichée.

#### Les cookies

Là aussi, investissez du temps pour maîtriser toutes les URLs de toutes les ressources statiques de votre site , afin de les mettre sur des domaines séparés du domaine principal. Imaginez un *cookie* d’un peu moins d’un Ko qui serait envoyé à la centaine d’objets généralement appelée par une page Web classique : vous demandez à votre utilisateur d’uploader 100 Ko de données inutiles. Une autre piste pour remplacer les cookies qui sont parfois servis sur des pages statiques qui n’utilisent même pas de données personnalisées est de ne pas les utiliser du tout... pour les remplacer par HTML5 *localStorage* si vous avez tout de même besoin de persistance côté client (préférence d’affichage, historique...). Pour la compatibilité navigateur, passez par des petites librairies spécialisées.

## En résumé

Vous voilà donc paré pour arrêter de perdre vos clients dès qu’ils essayent d’accéder à votre site à partir d’un réseau mobile. Nous avons vu que :

- la performance est empirique : testez même les grands classiques avant de choisir vos solutions ; 
- la plupart des techniques déjà connues marchent mais sont à traiter dans un autre ordre ; 
- ces techniques sont à pousser dans leurs extrêmes ; 
- de nouvelles possibilités sont apparues. 

Et ne comptez pas sur l’évolution future de l’équipement réseau : sauf inversion de la tendance actuelle, non seulement vos sites vont continuer à grossir mais en plus les futurs utilisateurs des réseaux 4G voire Wimax auront toujours des doigts, des murs, des gens et de l’atmosphère à traverser avant d’arriver sur vos serveurs.

L'optimisation, c’est maintenant.

Dans un prochain article, nous parlerons des performances sur mobile une fois que la page est chargée.
