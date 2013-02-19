# Pour lire la suite, cliquez ici

L'intitulé de cet article, s'il devient un lien, aura toutes les chances d'être ambigu. En effet, qui n'a jamais croisé des liens dont l'intitulé se résume à *lire la suite*, *en savoir plus* ou *cliquer ici*, pour ne citer que ces trois tournures fréquemment employées ? Un professionnel du marketing Web les justifiera en y voyant une invitation à l'action (le fameux *call to action*). Bon nombre d'utilisateurs n'y verront rien à redire, puisqu'en découvrant ces liens, ils auront certainement lu les phrases, voire les paragraphes, qui les entourent, connaissant ainsi le contexte dans lequel ces liens se trouvent. Mais, qu'en est-il d'un utilisateur de lecteur d'écran ?


## Explicitation des liens

Un utilisateur de lecteur d'écran a la faculté de consulter une page Web de façon linéaire, mais aussi et surtout de façon non linéaire, par le biais de raccourcis clavier lui permettant de parcourir la page titre par titre, liste par liste, paragraphe par paragraphe, mot par mot… et lien par lien. Par ailleurs, les lecteurs d'écran offrent la possibilité de lister, généralement sous forme de boîte de dialogue, l'ensemble des liens présents dans la page actuellement consultée. Or, lorsque les liens sont listés ainsi, ils sont isolés du contexte, si bien que des liens comme *lire la suite*, *en savoir plus* ou *cliquer ici* ne sont plus du tout explicites.

C'est pour cette raison que de tels liens sont fortement déconseillés. Par ailleurs, les WCAG 1.0 comportaient le [point à contrôler (*checkpoint*) 13.1](http://www.w3.org/TR/WCAG10/#tech-meaningful-links), qui disait, de façon on ne peut plus explicite ([en français](http://www.la-grange.net/w3c/wcag1/wai-pageauth.html#tech-meaningful-links "Traduction en français du point à contrôler 13.1 des WCAG 1.0")) :

> Identifier clairement la cible de chaque lien. [Priorité 2]
> 
> Les liens textes devraient être suffisemment explicites pour être compréhensibles même lorsqu'on les lit en dehors de leur contexte — de manière isolée ou parmi d'autres liens. Les liens textes doivent également être concis.
> 
> Par exemple, en HTML, écrivez "Information sur la version 4.3" au lieu de "cliquez ici". En plus du lien en version texte, les développeurs pourraient spécifier la cible d'un lien à l'aide d'un lien informatif sous forme de titre (par ex. en HTML, l'attribut "title").

Autrement dit, il était recommandé de formuler les liens de façon à les rendre explicites en l'absence de tout contexte, soit dans le contenu même du lien (compris entre les balises `<a>` et `</a>`) soit via son attribut `title`.

Bien entendu, une telle règle, qui condamne l'usage solitaire des termes *lire la suite* ou *cliquer ici*, peut sembler rigide et froisser ceux qui sont attachés au *call to action* qui s'en dégage. Fort heureusement, il est désormais possible de réconcilier un lien de type *lire la suite* avec l'accessibilité.


## Explicitation des liens selon le contexte

Les WCAG 2.0, avec le [critère de succès 2.2.4](http://www.w3.org/Translations/WCAG20-fr/#navigation-mechanisms-refs), de niveau A (qui correspond à un niveau minimal d'accessibilité), ont introduit la notion de lien en contexte, en se basant sur le fait que les versions les plus récentes de certains lecteurs d'écran permettent, lorsqu'on affiche la liste des liens, d'avoir des informations du contexte dans lequel ils sont placés. Les informations de contexte susceptibles d'éclairer les liens sont les suivantes :

* le contenu de la phrase dans lequel le lien est présent,
* le contenu du titre de section (`hN`) précédant le lien,
* le contenu du paragraphe (élément `p`) dans lequel le lien est présent,
* le contenu de l'élément `li` dans lequel le lien est présent,
* le contenu de l'élément `td` dans lequel le lien est présent,
* le contenu du ou des éléments `th` associé(s) à l'élément `td` (grâce à l'attribut `scope` ou à l'utilisation conjointe des attributs `id` sur `th` et `headers` sur `td`) dans lequel le lien est présent.

À noter que **l'un de ces contextes doit à lui seul permettre d'expliciter le lien**.

Prenons l'exemple de ce bout de code :

~~~ {lang="html"}
<h2>42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes</h2>
<p>Du texte introduisant l'article</p>
<p><a href="URL-de-l-article.html">Lire la suite</a></p>
~~~

Le lien *lire la suite* est explicite parce que l'élément `h2` fournit de quoi le comprendre, en donnant à entendre que ce lien signifie lire la suite de l'article qui parle des 42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes. Une telle explicitation peut également être obtenue en ajoutant un attribut `title` au lien en question, comme suit :

~~~ {lang="html"}
<h2>42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes</h2>
<p>Du texte introduisant l'article</p>
<p><a href="URL-de-l-article.html" title="42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes, lire la suite">Lire la suite</a></p>
~~~

Ces deux exemples valident le critère de succès 2.2.4 des WCAG 2.0, ainsi que (pour ceux qui s'en tiennent aux méthodes d'application des WCAG 2.0) le [critère 6.1 du référentiel Accessiweb, de niveau Bronze](http://www.accessiweb.org/index.php/accessiweb_2.2_liste_generale.html#crit-6-1) et le [test 6.13 du RGAA, de niveau A](http://www.rgaa.net/Possibilite-d-identifier-la.html).

Prenons un autre exemple :

~~~ {lang="html"}
<p>Pour connaître toutes nos promotions sur nos billets de train, <a href="URL-des-promotions.html">cliquez ici</a>.</p>
~~~

Le lien *cliquez ici* est explicite grâce à la phrase dans laquelle il se trouve. Elle donne à entendre que, si l'on clique, c'est bel et bien pour atterrir sur une ressource parlant longuement de toutes les promotions sur les billets de train. Une fois encore, le critère de succès 2.2.4 des WCAG est validé, ainsi que les critères et tests des méthodes d'application qui s'y rapportent.

Autre exemple :

~~~ {lang="html"}
<p>Pour rester à l'affût, vous pouvez :</p>
<ul>
    <li>vous inscrire à notre <span lang="en">newsletter</span>,</li>
    <li>vous abonner à notre flux de syndication,</li>
    <li>suivre Le Train de 13h37 sur <a href="URL-du-compte-Twitter">Twitter</a> ou <a href="URL-du-compte-Facebook">Facebook</a>.</li>
</ul>
~~~

Les deux liens sont explicites grâce au contexte fourni par le contenu de l'élément `li`, qui donne à entendre que, lorsqu'on suit ces liens, on atterrira vers le compte que possède Le Train de 13h37 sur ces réseaux sociaux, et non vers la page d'accueil de ces derniers. Une fois encore, le critère de succès 2.2.4 des WCAG est validé, ainsi que les critères et tests des méthodes d'application qui s'y rapportent. À noter que, si le lien est contenu dans une liste imbriquée, l'élément `li` parent de l'élément `ol` ou `ul` imbriqué est lui aussi pris en compte dans la fourniture du contexte de lien.

Certains s'émerveilleront d'une telle prise en compte du contexte pour évaluer le caractère explicite ou non d'un lien, cependant que d'autres grinceront des dents, considérant une telle disposition comme une régression de la part des WCAG 2.0. Pourtant, il est toujours possible de sortir du contexte, si j'ose dire.

## Liens explicites hors contexte : en quête du confort maximal

Les WCAG 2.0 maintiennent la règle selon laquelle l'intitulé du lien seul doit être explicite hors contexte, l'attribut `title` étant, le cas échéant, pris en compte. Mais cette règle figure dans le [critère de succès 2.4.9](http://www.w3.org/Translations/WCAG20-fr/#navigation-mechanisms-link), qui est maintenant de niveau AAA (qui est le niveau maximal, correspondant à un niveau d'accessibilité améliorée).

À ce niveau d'accessibilité, et selon ce critère de succès, il est incontestable que, dans le bout de code suivant :

~~~ {lang="html"}
<h2>42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes</h2>
<p>Du texte introduisant l'article</p>
<p><a href="URL-de-l-article.html">Lire la suite</a></p>
~~~

Le lien *lire la suite* n'est pas du tout explicite hors contexte. Il en est de même pour le lien *cliquez ici* dans :

~~~ {lang="html"}
<p>Pour connaître toutes nos promotions sur nos billets de train, <a href="URL-des-promotions.html">cliquez ici</a>.</p>
~~~

En revanche, le lien *lire la suite* du premier exemple, s'il est accompagné d'un attribut `title="42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes, lire la suite"` (qui reprend donc l'intitulé de l'élément `h2` qui le précède), demeure explicite une fois isolé de son contexte.

Cela dit, le recours à l'attribut `title` pour rendre un lien explicite hors contexte, aussi valable soit-il, pose un problème délicat : d'une part, parce qu'un lecteur d'écran peut être configuré pour ne pas restituer le contenu de cet attribut et, d'autre part, parce que l'infobulle prévue par les navigateurs graphiques pour afficher le contenu de cet attribut ne s'affiche pas si l'utilisateur navigue au clavier. Pour pallier cet écueil, la [technique suffisante C7 des WCAG 2.0](http://www.w3.org/TR/2012/NOTE-WCAG20-TECHS-20120103/C7) propose d'insérer le complément d'information qui convient à l'attribut `title` du lien dans le contenu du lien (entre les balises `<a>` et `</a>`) et de le masquer en CSS, sachant qu'un texte masqué en CSS dans de telles conditions, pour qu'il soit restitué par les lecteurs d'écran, ne doit pas l'être au moyen d'une déclaration `display: none` ou `visibility: hidden`. Cette technique, appliquée aux exemples de code précédents, donnerait les résultats suivants :

~~~ {lang="html"}
<h2>42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes</h2>
<p>Du texte introduisant l'article</p>
<p><a href="URL-de-l-article.html"><span class="visually-hidden">42 passagers d'un TGV bloqués pendant 13 heures et 37 minutes,</span> Lire la suite</a></p>

<p>Pour connaître toutes nos promotions sur nos billets de train, <a href="promotions.html">cliquez ici <span class="visually-hidden">pour connaître toutes nos promotions sur nos billets de train</span></a>.</p>

<p>Pour rester à l'affût, vous pouvez :</p>
<ul>
    <li>vous inscrire à notre <span lang="en">newsletter</span>,</li>
    <li>vous abonner à notre flux de syndication,</li>
    <li>suivre Le Train de 13h37 sur <a href="URL-du-compte-Twitter"><span class="visually-hidden">suivre Le Train de 13h37 sur</span> Twitter</a> ou <a href="URL-du-compte-Facebook"><span class="visually-hidden">suivre Le Train de 13h37 sur</span> Facebook</a>.</li>
</ul>
~~~

Avec le code CSS pour masquer de façon accessible les portions de lien explicitant le contexte, mais incompatibles avec des contraintes éditoriales privilégiant la concision visuelle des liens et le *call to action* :

~~~ {lang="css"}
.visually-hidden {
    position: absolute;
    left: -10000em;
}
~~~

Je ne donne pas tort à ceux qui trouveront lourd un tel procédé pour rendre les liens on ne peut plus explicites hors contexte. Toutefois, il ne faut pas perdre de vue que l'exigence d'explicitation hors contexte figure dans un critère de succès des WCAG 2.0 **de niveau AAA**, niveau reflété par les méthodes d'application Accessiweb ([critère 6.3, de niveau Or](http://www.accessiweb.org/index.php/accessiweb_2.2_liste_generale.html#crit-6-3)) et RGAA ([test 6.14, de niveau AAA](http://www.rgaa.net/Possibilite-d-identifier-la,93.html)). Autrement dit, cela relève de l'amélioration de l'accessibilité, le niveau normal d'accessibilité correspondant au niveau AA des WCAG 2.0 et le niveau A constituant, quant à lui, le minimum syndical de l'accessibilité, pour ainsi dire. Par ailleurs, les WCAG 2.0 disent clairement, à propos de [l'exigence de conformité](http://www.w3.org/Translations/WCAG20-fr/#conformance-reqs) :

> il n'est pas recommandé de se fixer le niveau AAA comme objectif à l'échelle de sites entiers car il n'est pas possible de satisfaire à tous les critères de succès du niveau AAA pour certains contenus.

## Conclusion

Ainsi, grâce au contexte de lien, il est parfaitement possible de concilier des liens dont le caractère explicite ne va pas de soi (comme *lire la suite*, *cliquer ici* ou *en savoir plus*) et l'accessibilité, à partir du moment où ce contexte est correctement structuré dans des éléments ou attributs qui le rendent éligible à l'explicitation de ces liens. Même si l'idéal reste de rendre les liens explicites hors contexte, il faut savoir établir des compromis acceptables qui laissent plus de chances à la réussite d'une démarche réaliste d'amélioration progressive et continue de l'accessibilité que l'obsession d'un objectif quasi illusoire d'une accessibilité à 100 %, au niveau AAA et à tout prix, obsession porteuse du risque de se casser la figure à un moment ou à un autre, à vouloir faire les choses trop bien du premier coup.

Enfin, que vous vous basiez sur le contexte de lien ou non, ne perdez jamais de vue qu'un lien explicite permet à l'utilisateur d'en comprendre la fonction et la destination et que tout lien identique doit avoir la même fonction et la même destination. Et, même si les WCAG 2.0 en font un cas particulier auquel les règles que j'ai rappelées dans cet article ne s'appliquent pas, tâchez de ne pas cultiver de liens ambigus pour tout le monde.

