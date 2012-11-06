# Les microdonnées par l'exemple
    
Introduites en HTML5, les microdonnées sont de simples attributs qui se greffent à la structure HTML. Elles ont pour objet de décrire la nature du contenu à l'instar du RDFa et des microformats. Enrichir le contenu d'une surcouche qui puisse être comprise et interprétée par les différents programmes n'est bien sûr pas une nouveauté : ça fait bien longtemps que la question s'est posée et que des solutions ont été proposées.   
Malheureusement, elles n'ont jamais été totalement satisfaisantes : RDFa n'a jamais été utilisé à grande échelle du fait de sa complexité supposée, et si les microformats ont rencontré un vif succès, ils présentent l'inconvénient de détourner la nature de certains composants pour marquer le contenu et d'être difficilement extensibles.

Intégrées au HTML, les microdonnées constituent une solution native pour enrichir le contenu. Elles se présentent sous la forme de cinq nouveaux attributs : `itemscope`, `itemtype`, `itemprop`, `itemref` et `itemid`. Et si leur utilisation peut sembler assez complexe de prime abord, sachez qu'il n'en est rien : voyons ensemble comment les appliquer à une page HTML.   
Pour cela, je vous propose de prendre comme cas d'étude cette [page-ci](http://letrainde13h37.fr/23/debit-latence-france-bien-calibrer-tests-performance/). Elle contient de nombreuses informations qu'il pourrait être intéressant d'enrichir comme le nom de l'article, le nom de l'auteur, le résumé, le nombre de commentaires et la note moyenne qui lui a été donnée.

Une fois les différentes données à marquer identifiées, il suffit juste de se lancer !

##Créer un objet sémantique
Si vous regardez le code source de la page, vous remarquerez que l'ensemble de l'article est contenu dans la balise `	article` portant l'identifiant `postSingle`. Elle est donc tout indiquée pour accueillir l'attribut booléen `itemscope`. Ce dernier n'accepte aucune valeur et sert juste à créer un nouvel objet sémantique. Pour cela, il suffit simplement de l'ajouter à notre balise sans autre forme de procès :

~~~ {lang="html" line="1" highlight="1"}
<article id="postSingle" itemscope>
…
</article>
~~~

Une fois que notre objet est créé, il faut maintenant l'identifier grâce à l'attribut `itemtype`. L'URL passée en valeur permet aux programmes de connaître la nature de l'objet et des propriétés qui lui sont attachées.  

##Identifier l'objet
Pour spécifier qu'il s'agit d'un article, on fait alors référence à l'URL [http://schema.org/Article](http://schema.org/Article). Cette page liste les différentes propriétés pouvant être attachées à ce type d'objet. Elle sert de « mode d'emploi » aux programmes pour qu'ils puissent comprendre et interpréter correctement la nature du contenu.

~~~ {lang="html" line="1" highlight="1"}
<article id="postSingle" itemscope itemtype="http://schema.org/Article">
…
</article>
~~~

Dès lors, il ne reste alors plus qu'à marquer les données en ajoutant des propriétés à l'objet.

##Doter l'objet de propriétés
Pour cela on ajoute l'attribut `itemprop` à la balise contenant le texte à identifier. La valeur de l'attribut permet d'indiquer la nature du contenu marqué. Par exemple, `name` permet de définir le nom de l'article, `author` le nom de l'auteur, `description` le résumé et `aggregateRating` la note moyenne qui lui a été donnée.   
Si aucune balise n'encadre la portion de texte visée, il faut alors ajouter une balise vide de sens, comme `span` par exemple.

~~~ {lang="html" line="1" highlight="2,4,8,15"}
<article id="postSingle" itemscope itemtype="http://schema.org/Article">
  <h1 class="pageTitle" itemprop="name">Débit et latence en France : bien calibrer ses tests de performance</h1>
  <div class="summary">
    <p itemprop="description">Internet, le réseau des réseaux… et un paradoxe : obtenir des mesures fiables et pertinentes sur les performances de ce réseau est incroyablement difficile. À quelle vitesse s’affiche un site ? Jean-Pierre nous propose de voir comment mener des tests efficaces et utiles en la matière.</p>
  </div>
  <a href="#">
    <img width="54" height="54" alt="" src="..." />
    <br/><span itemprop="author">Jean-Pierre Vincent</span>
  </a>
  <ul>
    <li class="number">
      <a href="#">2</a>
    </li>
    <li class="note">
      <a title="Note de l'article : 4/5" href="#" itemprop="aggregateRating">
        <img alt="4/5" src="...">
      </a>
    </li>
  </ul>
</article>
~~~

Pour indiquer le nombre de commentaires, les choses sont légèrement différentes. Il faut en effet utiliser l'attribut `itemprop="interactionCount"` conjointement à l'attribut `content` pour définir précisément la nature de la donnée (on parle du nombre de commentaires et pas du nombre de *retweets* par exemple) :  

~~~ {lang="html" line="1" highlight="12"}
<article id="postSingle" itemscope itemtype="http://schema.org/Article">
  <h1 class="pageTitle" itemprop="name">Débit et latence en France : bien calibrer ses tests de performance</h1>
  <div class="summary">
    <p itemprop="description">Internet, le réseau des réseaux… et un paradoxe : obtenir des mesures fiables et pertinentes sur les performances de ce réseau est incroyablement difficile. À quelle vitesse s’affiche un site ? Jean-Pierre nous propose de voir comment mener des tests efficaces et utiles en la matière</p>
  </div>
  <a href="#">
    <img width="54" height="54" alt="" src="..." />
    <br/><span itemprop="author">Jean-Pierre Vincent</span>
  </a>
  <ul>
    <li class="number">
      <a href="#" itemprop="interactionCount" content="UserComments:2">2</a>
    </li>
    <li class="note">
      <a title="Note de l'article : 4/5" href="#" itemprop="aggregateRating">
        <img alt="4/5" src="...">
      </a>
    </li>
  </ul>
</article>
~~~

Grâce à ces ajouts, les programmes sont maintenant en mesure d'identifier le titre de l'article, le nom de son auteur et sa description. Malheureusement, ce balisage n'est pas suffisant pour qu'il soient capables de comprendre la note qui lui est attribué : en l'état, ils savent uniquement que la note donnée à l'article correspond à la chaîne de caractères « 4/5 » spécifiée en alternative à l'image.

Pour qu'ils puissent interpréter correctement la note, il va falloir créer un nouvel objet de type évaluation auquel on pourra attacher les propriétés nécessaires à sa compréhension.

##Imbriquer des objets

On va procéder exactement de la même façon que précédemment en prenant comme base de référence la balise sur laquelle se trouve l'attribut `itemprop="aggregateRating"` et en y créant un nouvel objet de type évaluation :

~~~ {lang="html" line="1" highlight="1"}
<a href="#" itemprop="aggregateRating" itemscope itemtype="http://schema.org/AggregateRating">
  <img alt="4/5" src="...">
</a>
~~~

À partir de là, il ne reste plus qu'à ajouter les attributs `itemprop="ratingValue"` et `itemprop="bestRating"` pour que les programmes puissent distinguer la note donnée à l'article de la note maximale. Malheureusement, au vu du code ci-dessus, il est rigoureusement impossible de les placer autour du contenu visé puisqu'il se trouve à l'intérieur de l'attribut `alt`.   
Afin de contourner ce problème, nous allons donc créer deux nouveaux éléments (il faut en effet un élément HTML par attribut à renseigner). Et pour éviter que ces derniers n'interfèrent avec le contenu, on va utiliser la balise `meta` comme support d'informations.

~~~ {lang="html" line="1" highlight="3,4"}
<a href="#" itemprop="aggregateRating" itemscope itemtype="http://schema.org/AggregateRating">
  <img alt="4/5" src="...">
  <meta itemprop="ratingValue" />
  <meta itemprop="bestRating" />
</a>
~~~

Une fois les balises `meta` en place, il ne reste alors plus qu'à indiquer la valeur de deux notes au moyen de l'attribut `content` :

~~~ {lang="html" line="1" highlight="3,4"}
<a href="#" itemprop="aggregateRating" itemscope itemtype="http://schema.org/AggregateRating">
  <img alt="4/5" src="...">
  <meta itemprop="ratingValue" content="4" />
  <meta itemprop="bestRating" content="5" />
</a>
~~~

Et voilà, les programmes sont maintenant en mesure d'interpréter correctement le titre de l'article, le nom de son auteur, sa description, le nombre de commentaires qui on été faits, mais aussi la note moyenne qui lui a été donnée.

Cela dit, il est relativement fréquent que les données relatives à un même objet soient disséminées dans la page, comme c'est le cas de notre page d'exemple : les  informations liées à l'article et celles liées à l'auteur ne se trouvent pas dans le même élément. Il serait pourtant intéressant d'établir une relation entre ces différentes informations.

~~~ {lang="html" line="1"}
<article id="postSingle" itemscope itemtype="http://schema.org/Article">
…
</article>
<section id="authors">
  <a href="#">Jean-Pierre Vincent</a>
  <a href="#">
    <img alt="" src="#">
  </a>
  <div class="author-description">
    <p>12 ans à coder pour le Web, ça marque un homme. Depuis 2011 Jean-pierre VINCENT est expert technique indépendant sur les performances Web et HTML5, mais également auteur du livre <a href="#">"HTML5" chez Dunod</a>, conférencier multi-récidiviste et formateur. Avant ça ? du PHP depuis 2000, puis de l'intégration et du gros JavaScript en 2005-2008 chez Yahoo!, avant de tenter l'expérience startup en tant que lead technique.</p>
  </div>
</section>
~~~

Fort heureusement, c'est possible grâce à l'attribut `itemref`.

##Associer des données distantes
`itemref` permet de créer facilement un lien entre des données qui ne se trouvent pas dans un élément commun. Il suffit de placer l'attribut à la racine de l'objet sémantique (la balise qui accueille l'attribut `itemscope`) en lui donnant comme valeur l'identifiant de l'élément muni de la propriété que l'on souhaite ajouter à l'objet.   
Si jamais plusieurs propriétés étaient concernées, il suffirait alors de mettre tous les identifiants en valeur d'attribut.

~~~ {lang="html" line="1" highlight="1,7"}
<article id="postSingle" itemscope itemtype="http://schema.org/Article" itemref="photo">
…
</article>
<section id="authors" itemscope itemtype="http://schema.org/Person">
  <a href="#">Jean-Pierre Vincent</a>
  <a href="#">
    <img alt="" src="#" id="photo" itemprop="image">
  </a>
</section>
~~~

Dans ce cas précis, on souhaite lier une donnée qui est relative à l'auteur et non à l'article lui-même. C'est pourquoi il est impératif de créer un nouvel objet personne : cela permet aux programmes de comprendre que l'image est bien celle de l'auteur de l'article et non celle de l'article.

##Et itemid alors ?
Vous aurez certainement remarqué que jusqu'à présent, nous n'avons pas abordé l'attribut `itemid`.   
La raison est toute simple : ce dernier n'est d'aucune utilité dans ce cas de figure particulier.

À vrai dire, il est d'une utilité relativement restreinte... Car à la différence des autres attributs qui permettent de marquer du contenu varié, `itemid` ne sert qu'à marquer un type de contenu bien précis : une donnée (valeur numérique ou chaîne de caractères) qui permette aux programmes d'identifier sans aucun doute possible l'objet en question. Il peut par exemple s'agir d'un visa d'exploitation, puisque la mention de cette seule information suffit à déterminer précisément de quel film il s'agit.  

Sur la page de présentation du [Petit Précis de Créativité](http://envoitu.re/ligne-essai/petit-precis-creativite/) écrit par Virgine Caplet, l'attribut `itemid` serait donc tout à fait indiqué pour spécifier le numéro ISBN.   
Mais avant de procéder à l'ajout, il convient de prendre connaissance de la particularité de cet attribut : `itemid` doit en effet être accompagné de `itemscope` et `itemtype` pour être fonctionnel. Ainsi pour marquer un numéro ISBN en utilisant `itemid`, il convient d'utiliser trois attributs :

~~~ {lang="html" line="1"}
<p itemscope itemtype="http://schema.org/Book" itemid="urn:isbn:979-10-91997-00-3">N° ISBN : 979-10-91997-00-3</p>
~~~

La solution alternative étant d'utiliser l'attribut `itemprop` avec la valeur `isbn` :

~~~ {lang="html" line="1"}
<p>N° ISBN : <span itemprop="isbn">979-10-91997-00-3</span></p>
~~~

Et voilà...   
J'espère que les microdonnées n'ont maintenant plus aucun secret pour vous et que vous les intégrerez à votre code HTML dès que la situation s'y prêtera.
En ce qui nous concerne c'est en bonne place sur la *todo list*... ;)