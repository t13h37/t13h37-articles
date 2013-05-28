# jQuery, c'est bien, le DOM moderne, c'est mieux !

Lors de [mon intervention à Paris Web 2012](http://www.paris-web.fr/2012/conferences/faire-du-web-moderne-a-destination-de-tous.php#video), j'expliquais combien il était facile de faire une application qui marche aussi bien dans les anciens navigateurs que dans les nouveaux.  
Aujourd'hui, je vais prendre une direction toute différente: vous montrer que les navigateurs modernes[^modernes] fournissent des outils puissants pour créer des applications Web, à tel point qu'on peut aujourd'hui se passer de l'omniprésent jQuery.

jQuery n'est pas magique: il ne peut que tirer partie de ce que lui
permet l'API DOM. Dès lors, même si l'on choisit cette bibliothèque, bien connaitre l'API DOM permet de bien utiliser jQuery.

jQuery est aujourd'hui décrié en raison de son côté monolithique. En effet, il fournit un ensemble de fonctions orthogonales, qui étaient toutes nécessaires àun certain point de l'histoire du Web. Mais comme nous allons le voir, elles ont peu à peu été intégrées dans les nouveaux standard du Web.

Peut-être est-ce surtout ça, l'héritage de jQuery.

Passons à présent en revue les grands champs d'action de cette bibliothèque.

## Gestion des évènements

### Au commencement
Il n'y a pas si longtemps, pour avoir des gestionnaires d'évènements, nous utilisions un attribut :

~~~ {lang="html" line="1" highlight="1"}
<a href='#' onclick='return appelleFonction();'>mon lien</a>
~~~

Puis le concept d'amélioration progressive a pris son essor, et nous avons commencé à ajouter des gestionnaires d'événements en JavaScript :

~~~ {lang="javascript" line="1" highlight="1"}
document.getElementById('un-lien').onclick = onClickFunction;
~~~

Mais cette manière ne permet pas d'attacher plusieurs gestionnaires pour un même évènement sur un seul élément. C'est pourquoi, bien rapidement, nous avons vu apparaître des bibliothèques qui permettent de le faire facilement, à commencer par jQuery :

~~~ {lang="javascript" line="1" highlight="1"}
$('#un-lien').click(onClickFunction);
~~~

Là encore, l'API DOM n'est pas en reste, et propose la méthode `addEventListener`:

~~~ {lang="javascript" line="1" highlight="1"}
document.getElementById('un-lien').addEventListener('click', onClickFunction, false);
~~~

C'est certes plus verbeux, mais aussi plus près du navigateur, et à ce titre plus efficace.

Il est important de noter que `addEventListener` n'est présent que dans les navigateurs modernes. Internet Explorer propose sa propre gestion des évènements, avec beaucoup de choses très différentes. jQuery, ainsi que d'autres bibliothèques, simplifie beaucoup la gestion des évènements en aplanissant les différences entre Internet Explorer et les autres navigateurs.

### La délégation d'évènements
Il s'agit là d'une fonction qui existe depuis toujours dans les navigateurs, mais que jQuery a véritablement aidé à démocratiser en proposant, au fil du temps, plusieurs API de plus en plus simples à utiliser.

#### Explication sommaire
Lorsqu'un évènement doit être envoyé sur un élément-cible (par exemple, l'utilisateur a cliqué sur un bouton), un mécanisme de propagation se déclenche.

On se rappelle que la page est représentée comme un arbre, l'arbre DOM. L'évènement déclenche sa course à partir de l'élément racine de la page et parcourt l'arbre jusqu'à arriver à l'élément-cible. C'est la phase dite de *capture*.

Puis l'évènement remonte jusqu'à l'élément racine de la page : c'est  ce qu'on appelle la phase de *propagation*[^bubbling].

Ce mécanisme permet de traiter l'évènement à n'importe laquelle de ces étapes, au niveau de n'importe quel élément traversé. Dans le
gestionnaire de l'évènement, on peut décider de laisser d'autres gestionnaires jouer, ou bien au contraire d'annuler tout traitement supplémentaire.

On pourra lire la Source, c'est-à-dire [la spécification du W3C, qui montre un schéma très clair](http://www.w3.org/TR/DOM-Level-3-Events/#event-flow).

#### Les intérêts
Ce mécanisme est très utile dans une page Web très dynamique, où des
éléments sont ajoutés et enlevés en réponse à diverses actions. En effet, cela va permettre d'ajouter un gestionnaire d'évènements une bonne fois pour toutes, au démarrage de l'application, en le positionnant sur un élément qui n'évolue pas et qui est le parent des éléments qui seront ajoutés et/ou supprimés.

On peut lire [l'article de 37signals](http://37signals.com/svn/posts/3137-using-event-capturing-to-improve-basecamp-page-load-times) sur le sujet, qui montre également les intérêts liés à la performance de votre page Web.

#### L'apport de jQuery
Lorsque l'on cherche à implémenter de la délégation, le plus pénible
est de vérifier que l'événement concerne bien l'élément que l'on veut traiter.
Les outils du DOM "historique" sont assez limités : vérification de l'attribut *id*, de la classe[^classList] et du nom de l'élément lui-même. Il faut donc mettre en place une série de `if`, ou un bloc `switch`, pour traiter cet évènement.

jQuery a amené une API très simple à utiliser pour résoudre ce problème. Très facilement, nous décidons de l'élément auquel attacher le gestionnaire, ainsi que les éléments concernés par l'évènement :

~~~ {lang="javascript" line="1" highlight="1"}
$('.liste').delegate('li > a', 'click', eventHandlerFunction);
~~~

ou, depuis jQuery 1.7 :

~~~ {lang="javascript" line="1" highlight="1"}
$('.liste').on('click', 'li > a', eventHandlerFunction);
~~~

N'oublions pas que l'API de jQuery est plus riche que cela : elle permet notamment d'attacher plusieurs évènements en un seul appel.

#### Dans le DOM présent en natif
Nous avons vu précédemment la méthode `addEventListener`, mais nous n'avons pas insisté sur le troisième argument[^useCapture]. Il permet de choisir la phase où l'évènement sera traité : `true` dans la phase de *capture*, `false` dans la phase de *bubbling*.

Par ailleurs, la nouvelle méthode `matches` permet (enfin) d'utiliser un sélecteur CSS pour vérifier si un élément lui correspond. Tous les navigateurs modernes (à part Internet Explorer 8) le supportent sous son ancienne forme `matchesSelector` et un préfixe.

~~~ {lang="javascript" line="1" highlight="1"}
// on peut être plus intelligent que ça mais ça fera l'affaire :)
var body = document.body,
    matches = body.matches || body.mozMatchesSelector ||
              body.webkitMatchesSelector || body.oMatchesSelector ||
              body.msMatchesSelector;
// ces lignes permettent d'appeler facilement matches :
// matches(element, selecteur);
matches = matches.call.bind(matches);
// bien sûr, vous pouvez tout à fait réutiliser le code précédent dans une de vos bibliothèques maison
document.getElementById('liste').addEventListener('click', onClickHandler, false);
function onClickHandler(e) {
  // e.target correspond à l'élément clické
  if (matches(e.target, 'a.external')) {
    e.preventDefault();
    // faisons quelque chose avec l'attribut href. Ici on va l'afficher dans la console
    var href = e.target.href;
    console.log(href);
  }
}
~~~

C'est donc facile de le faire avec les outils natifs. Si, cependant, vous préférez l'API de jQuery, mais ne voulez pas utiliser l'ensemble de la bibliothèque, [la micro-bibliothèque Gator](http://craig.is/riding/gators) propose une API similaire tout en s'appuyant sur ces mécanismes modernes.

## Récupération d'éléments DOM basée sur les sélecteurs CSS
C'est sans doute l'une des grandes avancées apportées par jQuery : la possibilité de sélectionner des éléments DOM en utilisant un sélecteur CSS. Avant ça, les deux seules possibilités de l'API DOM étaient :

* `getElementById` pour sélectionner un élément par son ID 
* `getElementsByTagName` pour sélectionner des éléments par leurs noms de balise.

Cela signifie que ces deux méthodes représentaient les seules manières rapides d'accéder à un objet. Mais jQuery a apporté une grande facilité dans la sélection des éléments et leur manipulation, comme nous le verrons plus loin.

Aujourd'hui, l'API DOM propose des méthodes bien plus puissantes :

### `getElementsByClassName`
Cette méthode retourne les éléments qui ont cette ou ces classes (la méthode accepte plusieurs classes). Elle est supportée par tous les navigateurs modernes.

~~~ {lang="javascript" line="1" highlight="1"}
// récupère tous les éléments qui ont la classe 'menu'
var elementsList = document.getElementsByClassName('menu');
~~~

### `querySelector` et `querySelectorAll`
Beaucoup plus intéressantes, ces méthodes acceptent, au même titre que jQuery, un sélecteur CSS, et sont supportées par tous les navigateurs modernes, Internet Explorer 8 inclus.

Ces méthodes n'acceptent que les sélecteurs CSS supportés par le moteur CSS. Cela signifie que Internet Explorer 8 ne reconnait que les sélecteurs CSS 2.1, et que les sélecteurs "magiques" de jQuery (tels que `:has()`, `:visible`...) ne sont pas supportés.

Par ailleurs, on l'oublie assez souvent : toutes ces méthodes peuvent s'appeler directement sur un élément DOM. Dans ce cas, elles vont rechercher des éléments dans le sous-arbre DOM issu de cet élément, à la manière d'un `find()`.

#### `querySelector`
Cette méthode retourne le premier[^premier] élément qui correspond au sélecteur passé en argument.

~~~ {lang="javascript" line="1" highlight="1"}
document.querySelector('.nav p').textContent = 'Introduction';
~~~

#### `querySelectorAll`
Elle retourne tous les éléments qui correspondent au sélecteur.

La plupart des méthodes du DOM retournant une liste d'éléments (une `NodeList`) retournent une liste que l'on qualifie de *vivante* (*live*). Il s'agit d'une vue à jour du document : si le document est changé, la liste le sera également. `querySelectorAll`, au contraire, retourne une liste *non-live*, c'est-à-dire qu'elle ne sera pas modifiée si l'arbre DOM évolue.

~~~ {lang="javascript" line="1" highlight="1"}
// container est un élément qui contient des cases à cocher
var inputs = container.querySelectorAll('input[type="checkbox"]');
// on les déselectionne tous
for (var i = 0, l = inputs.length; i < l; i++) {
  inputs[i].checked = false;
}
~~~

## Manipulation DOM : création, modification, suppression
Au-delà de la sélection de noeuds DOM, jQuery permet également de créer facilement du contenu. Nous verrons cependant que l'API DOM a, là encore, de nouvelles possibilités en la matière.

### Rappel sur `innerHTML`
Depuis toujours, on peut créer des éléments DOM et les ajouter à l'arbre DOM chargé. Cela se fait de la manière suivante :

~~~ {lang="javascript" line="1" highlight="1"}
var lien = document.createElement('a');
lien.href = 'http://google.fr';
lien.appendChild(document.createTextNode('go to Google');
document.querySelector('p').appendChild(lien);
~~~

On voit que c'est bien verbeux...

Il y a maintenant quelques années, Internet Explorer a introduit la propriété très intéressante `innerHTML`. En effet, le code suivant est équivalent au précédent:

~~~ {lang="javascript" line="1" highlight="1"}
var para = document.querySelector('p');
para.innerHTML += '<a href="http://google.fr">go to Google</a>';
~~~

Cette écriture est beaucoup plus concise, et c'est par ailleurs une
manière très performante d'ajouter du contenu. Mais elle présente tout de même un inconvénient : puisqu'on doit ajouter des éléments à l'arbre existant, il faut d'abord récupérer l'existant, et ensuite seulement concaténer ce qu'on veut y ajouter. Or, récupérer l'existant nécessite de sérialiser l'arbre DOM en HTML, ce qui est potentiellement lent[^serialisation].  
Par ailleurs, ces opérations sont faites de manière synchrone, c'est-à-dire qu'elles doivent toutes s'effectuer avant que l'instruction JavaScript suivante puisse s'exécuter. Pendant ce temps, l'utilisateur ne peut pas interagir avec la page Web !

Évidemment, cet inconvénient n'existe plus (ou moins) dès lors que l'on  remplace la totalité du contenu. Dans ce cas, on va traiter en une seule fois l'ensemble de l'entrée HTML, comme le navigateur le fait au chargement d'une page[^parsing].  
Attention tout de même à bien vérifier ce que l'on ajoute, car on
s'expose facilement aux problèmes de *Cross-Site Scripting*. À ce sujet, on pourra consulter [l'excellent article de Ben Vinegar](http://benv.ca/2012/10/4/you-are-probably-misusing-DOM-text-methods/)
pour apprendre comment vérifier correctement ses entrées utilisateurs en JavaScript.

### Des méthodes méconnues

#### `DocumentFragment`, pour préparer un morceau de document en mémoire
Je vous propose de voir dans un premier temps `DocumentFragment`.
Globalement, cette méthode permet de disposer d'un document en mémoire et de le manipuler facilement, et surtout, efficacement.

En effet, lorsque l'on manipule directement le document affiché, chaque modification doit être restituée à l'utilisateur, ce qui est coûteux en performance. Le `DocumentFragment` permet de contourner facilement ce problème. Et, cerise sur le gâteau, cette méthode est supportée par tous les navigateurs, même Internet Explorer 6 !

~~~ {lang="javascript" line="1" highlight="1"}
// ce tableau doit évidemment être récupéré par diverses méthodes, par exemple en Ajax
var texts = ['foo', 'bar', 'baz'];
function createContent() {
  // crée le document fragment
  var fragment = document.createDocumentFragment();
  // texts est un tableau JS contenant les textes à ajouter au DOM
  texts.forEach(function(text) {
    var li = document.createElement('li');
    li.textContent = text;
    // on ajoute des éléments à un fragment comme si c'était un noeud
    fragment.appendChild(li);
  });
  return fragment;
}
// cet élément est préexistant dans la page
var ul = document.querySelector('ul');
// createContent retourne un document fragment
ul.appendChild(createContent());
~~~

Dans cet exemple, on voit que le `DocumentFragment` permet aussi d'ajouter des éléments pêle-mêle, c'est-à-dire sans élément racine. Le `DocumentFragment` joue ce rôle, tout en disparaissant lorsqu'il est ajouté au DOM.

#### `insertAdjacentHTML`, pour ajouter facilement du contenu HTML
On l'a vu plus haut, `innerHTML` est très intéressant pour remplacer
complètement le contenu d'un élément. En revanche, pour ajouter du contenu, cela devient moins efficace.

`insertAdjacentHTML` est une réponse à ce problème, puisque cette API va permettre d'ajouter du contenu à un contenu existant.

Elle s'appelle sur l'élément à modifier. Ce qui est particulièrement
intéressant, c'est que l'on peut modifier le contenu de cet élément,
mais aussi ajouter des éléments avant ou après l'élément-cible.

~~~ {lang="javascript" line="1" highlight="1"}
var container = document.getElementById('container');
// insertion de contenu à la fin du container
container.insertAdjacentHTML('beforeend', '<span><strong>fin</strong> du container</span>');
// insertion de contenu au début du container
container.insertAdjacentHTML('afterbegin', '<span><strong>début</strong> du container</span>');
// insertion de contenu avant le container
container.insertAdjacentHTML('beforebegin', '<span><strong>avant</strong> le container</span>');
// insertion de contenu après le container
container.insertAdjacentHTML('afterend', '<span><strong>après</strong> le container</span>');
~~~

Ce qui donne:

~~~ {lang="html" line="1" highlight="1"}
<span><strong>avant</strong> le container</span>
<div id="container">
<span><strong>début</strong> du container</span>
// contenu préexistant de container
<span><strong>fin</strong> du container</span>
</div>
<span><strong>après</strong> le container</span>
~~~

## Ajax et autres fonctions utilitaires
Le DOM est une partie importante des fonctions de jQuery, mais la bibliothèque a également amené d'autres fonctions utilitaires, pour aider à la programmation d'une application. Par chance, les navigateurs d'aujourd'hui proposent là aussi des APIs plus modernes.

### Ajax : requêtes HTTP asynchrones
C'est une partie très importante du développement Web moderne : pouvoir requêter un serveur sans avoir à recharger l'ensemble de la page.

#### L'API de jQuery
jQuery est arrivé à une époque où l'on commençait tout juste à découvrir les intérêts de `XMLHttpRequest`. À ce moment-là, la manière d'obtenir cet objet différait beaucoup selon les navigateurs. Internet Explorer utilisait un contrôle ActiveX (différent suivant les versions). Au contraire, dans les navigateurs qui avaient adopté cet objet, on l'instanciait comme un objet classique, avec le mot-clé `new`, comme aujourd'hui en somme.

Son API initiale n'est pas des plus pratiques : on doit écouter un évènement `readystatechange` pour suivre la propriété `readyState`, qui prend une valeur particulière lorsque la requête est achevée avec succès.

Il était donc logique, vu l'importance que commençait à prendre cette
fonctionnalité, que jQuery propose une API simplifiée pour utiliser cet objet.  
Cette API était dessinée autour des usages de l'époque : des requêtes GET pour récupérer des informations XML ou textuelles, et des requêtes POST pour soumettre des formulaires sans avoir besoin de recharger la page. Aujourd'hui encore, si on ne donne pas d'option supplémentaire, envoyer un POST avec un objet JSON en argument sérialise cet objet à la manière d'un formulaire. Il est
bien sûr possible de débrayer ce comportement, mais ça reste le comportement par défaut, par souci de garder la compatibilité ascendante.

#### L'API native des navigateurs
Regardons à présent ce que proposent les navigateurs en natif.

Tout d'abord, vous serez heureux d'apprendre (si vous ne le savez pas encore) que tous les navigateurs permettent aujourd'hui d'instancier `XMLHttpRequest tel un objet normal:

~~~ {lang="javascript" line="1" highlight="1"}
var request = new XMLHttpRequest(url);
~~~

Seul Internet Explorer 6 peut encore poser problème. Si vous devez supporter cette version du navigateur, il conviendra donc de tester la présence de cet objet avant de l'utiliser, et par exemple d'afficher un message à l'utilisateur s'il est absent.

L'API a vu par ailleurs un certain nombre d'ajouts.

Tout d'abord, pour mimer l'utilisation initiale de jQuery, à savoir l'envoi asynchrone de formulaires, l'objet `FormData` est proposé.  
On peut l'initialiser avec les données d'un formulaire existant, on peut ajouter des données (y compris des fichiers auxquels on aurait eu accès via du glisser-déposer par exemple) et on peut enfin l'envoyer avec un objet `XMLHttpRequest` :

~~~ {lang="javascript" line="1" highlight="1"}
var data = new FormData(document.getElementById('myForm'));
var request = new XMLHttpRequest(url);
request.send(data);
~~~

On a donc là une API orientée objet bien intéressante !  
Fait appréciable, elle est aujourd'hui supportée par tous les navigateurs, hormis Internet Explorer 9 et inférieurs.

Par ailleurs, `XMLHttpRequest` de niveau 2 a amené de nouveaux évènements à écouter, plus sympathiques que le traditionnel `readystatechange` : `progress`

### Programmation fonctionnelle
Pour beaucoup (et c'est mon cas !), jQuery a permis une première approche de la programmation fonctionnelle. Sa méthode utilitaire `$.each` en a séduit plus d'un en permettant d'itérer facilement sur un tableau ou un objet avec une fonction.  
Grâce à cela, l'action réalisée sur l'élément du tableau ou de l'objet est bien cerné.

~~~ {lang="javascript" line="1" highlight="1"}
// itérer un tableau
var tableau = ['foo', 'bar', 'baz'];
$.each(tableau, function(i, value) {
  console.log(i, ':', value);
});
// itérer un objet
var objet = {
  foo: 'bar',
  foz: 'baz
};
$.each(objet, function(key, value) {
  console.log(key, ':', value);
});
// itérer un résultat de méthode DOM
$.each(document.getElementsByTagName('a'), function(i, elt) {
  console.log(i, 'href:', elt.href);
});
~~~

EcmaScript 5 amène justement un certain nombre de méthodes utilitaires pour réaliser des actions sur les éléments d'un tableau : `forEach`, `map`, `some`, `every`, `reduce`, `reduceRight`, `filter`. Je ne vais pas rentrer dans les détails car ce n'est pas le but de cet article, mais un développeur JavaScript gagnerait à savoir précisément comment elles fonctionnent et quand les utiliser.

Voici un exemple d'utilisation de `reduce`, sans doute l'une des méthodes les plus intéressantes :

~~~ {lang="javascript" line="1" highlight="1"}
var elementNames = ['foo', 'bar', 'baz'];
// elements est un tableau d'éléments dont les ids sont dans le tableau elementNames
var elements = elementNames.reduce(function(result, name) {
  result[name] = document.getElementById(name);
}, {});
/* elements est maintenant :
{
    foo: document.getElementById('foo'),
    bar: document.getElementById('bar'),
    baz: document.getElementById('baz')
}
*/
~~~

Pour itérer sur un objet, il faut d'abord passer par la méthode `Object.keys` qui permet de récupérer l'ensemble des clés d'un objet sous forme d'un tableau.  
Dès lors, il est possible d'utiliser les méthodes vues ci-dessus. Dans le cas d'un objet issu d'héritage, on peut aussi utiliser si besoin `Object.getOwnPropertyNames` qui retournera uniquement les noms des propriétés définies dans la sous-classe.

Par exemple, pour transformer un objet en tableau, on peut utiliser :

~~~ {lang="javascript" line="1" highlight="1"}
var pomme = { type: 'Chantecler', couleur: 'jaune', traitement: false };
var values = Object.keys(pomme).map(function(key) { return pomme[key]; });
~~~

On peut rendre cette fonction générique :

~~~ {lang="javascript" line="1" highlight="1"}
function values(object) {
  return Object.keys(object).map(function(key) { return object[key]; });
}
~~~

## Conclusion
J'espère que si vous êtes arrivés jusque là, vous êtes maintenant convaincus que le DOM natif a un potentiel bien réel. Il est peut-être encore un peu tôt pour utiliser certaines méthodes mais, en faisant attention à la compatibilité ascendante, il est tout à fait possible de s'appuyer sur ces nouvelles possibilités pour de nouveaux projets. Pour aller encore plus loin, [Raphaël Gougeron présentera une conférence sur le même sujet à Paris-Web 2013](http://www.paris-web.fr/2013/conferences/jquery-sans-jquery.php).

JQuery s'en va aussi sur la voie de la modernisation, poussé par les nombreuses micro-bibliothèques[^microjs], et les développeurs travaillent sur sa modularisation. La version 2.0 n'est plus compatible avec Internet Explorer inférieur ou égal à 8. Je le déplore d'une part, car l'universalité de jQuery était une force, et en quelque sorte un présupposé. Mais d'autre part je l'apprécie car cela ne peut qu'améliorer ses performances.

Utilisez donc le DOM une fois de temps en temps, il en vaut la peine, et vous ferez des sites plus efficaces !

[^modernes]: Le terme de "_navigateur moderne_" peut avoir
plusieurs significations. Dans cet article, il désignera tous les navigateurs actuels, Internet Explorer inférieur ou égal à 8 exclus. Dans les cas contraires, nous le préciserons.

[^bubbling]: On retrouve aussi le terme de *bubbling* en anglais.

[^classList]: Et encore, il faut parser la propriété `className` avec
des expressions rationnelles, car `classList.contains` n'existe pas encore.

[^useCapture]: Il est aujourd'hui devenu optionnel et vaut `false` s'il est absent. Toutefois, certaines vieilles versions des navigateurs (avant Firefox 6 et Opera 11.60) envoient une exception si on ne le met pas, il est donc préférable de continuer à le mettre
systématiquement pour l'instant.

[^premier]: Pour être plus précis, on parle du premier élément dans l'ordre du document. Le document étant un arbre (l'arbre DOM), l'ordre du document est l'ordre des éléments que l'on rencontre lorsque l'on parcourt l'arbre en profondeur, en traitant un élément avant ses enfants (_depth first preorder_).

[^serialisation]: Il faut se rappeler que le document est conservé en
mémoire sous la forme d'un arbre. Ainsi, au chargement de la page le document téléchargé en HTML est lu et converti sous cette forme. Ce que j'appelle sérialisation, c'est l'action de transformer l'arbre en HTML, et la désérialisation est l'action inverse. On utilisera le même terme lorsqu'on traduit un objet JavaScript en JSON, et inversement.  
Pour en savoir plus, je vous conseille d'aller voir le [code utilisé dans Firefox pour sérialiser](https://mxr.mozilla.org/mozilla-central/ident?i=Serialize&tree=mozilla-central&filter=%2FElement.cpp%24).

[^parsing]: Voir [le code utilisé dans Firefox pour gérer l'action de modification de la propriété](https://mxr.mozilla.org/mozilla-central/ident?i=SetInnerHTML&tree=mozilla-central&filter=%2FElement.cpp%24). Dans ce code, On voit bien que les fonctions internes liées au *parsing* HTML sont appelées directement.

[^microjs]: Voir le site [microjs](http://microjs.com/) pour découvrir le monde des micro-bibliothèques.
