# Les CSS spaghettis, c'est fini

CSS est formidable… Sérieusement ! Vous connaissez beaucoup d'outils de conception de couche graphique (car c'en est un) capables de modifier aussi radicalement l'interface que vous présentez à vos utilisateurs ? - Presque - tout est modifiable à souhait. Oui, mais… CSS reste un langage déclaratif, verbeux, et qui nécessite parfois de se contorsionner pour aboutir à ses fins. Seulement voilà, un site ou – à plus forte raison – une application web, ce ne sont pas quelques lignes de CSS. Ce sont plusieurs centaines, voire plusieurs milliers de lignes de CSS. Et rapidement, sans même vous en apercevoir, vous vous retrouvez plongés jusqu'aux yeux dans un magma de règles impossibles à maintenir correctement.

Comme beaucoup d'entre-vous (ne vous cachez pas), j'ai été confronté à ces feuilles de styles immenses, désorganisées (ou presque), où il devenait impossible de retrouver quoi que ce soit. À ma grande honte, j'en ai même produit… Et tout comme vous, je me suis rapidement dit qu'il allait s'avérer nécessaire de trouver des solutions, et que je ne voulais plus jamais travailler comme ça.

Ce qui va suivre n'est ni l'ultime méthode magique pour organiser vos CSS ; ni même une bonne pratique. C'est uniquement la somme de mes dernières années de travail, de mes expérimentations, tentatives, erreurs… Cette méthode est largement inspirée de la [méthode Daisy](http://romy.tetue.net/methode-daisy) mise au point par Romy Duhem-Verdière ; du travail de Chris Eppstein, auteur de la library [Compass](http://compass-style.org/) et développeur sur le projet [SASS](http://sass-lang.com/) ; des recommandations éditées par Jonathan Snook dans son ouvrage [SMACSS](http://smacss.com/) ; et de beaucoup de bon sens, finalement…

## CSS, oui, et ensuite…?

CSS a largement progressé depuis son premier brouillon en 1996. On en redécouvre même le plein potentiel aujourd'hui, sortis de l'obscurantisme des années noires IE6 (et très prochainement d'IE7) et de son support plus que médiocre de nombreux sélecteurs et propriétés.

L'avènement de CSS3 nous prouve que le langage sait plus que jamais s'adapter, évoluer, muter pour répondre aux besoins diversifiés des développeurs _front-end_. Il nous offre aujourd'hui toujours plus de sélecteurs (béni sois-tu `:nth-child()`), toujours plus de propriétés à personnaliser à volonté (comme `CSS-Gradient` : plus de png sur-dimensionnés, et des boutons toujours beaux "même en grande taille"). Et le futur est encore devant nous : CSS nous permet par exemple, dans certaines conditions, de nous affranchir du passage "Photoshop", avec les méthodes de design dans le navigateur pour le prototypage ; les filtres CSS nous promettent encore de belles choses à venir très rapidement, avec les modes de fusion notamment.

Seulement, même si CSS avance vite, et dans de nombreuses directions (propriétés, filtres, FX…), il reste un langage purement déclaratif, difficilement factorisable sans devoir entremêler la structure de données à la couche présentation, et n'encourage pas la construction de librairies partageables entre différents projets.

Fondamentalement, il manque 3 choses à CSS pour devenir un vrai langage "dynamique" :

- le support des variables : qui n'a jamais conclu à l'issue d'un développement CSS que la structure en cascade est formidable, mais la factorisation difficile ? On ne peut pas toujours facilement regrouper ensemble tous les sélecteurs d'éléments ayant la même couleur de bordure, par exemple. On se retrouve alors à réaliser des séries de copier-coller pour aller chercher la bonne couleur `#fc5da4` absolument impossible à mémoriser… Et quand il s'agit de finalement modifier cette valeur, on s'engage dans de formidables parties de _rechercher-remplacer_™ (samedis soir endiablés garantis). Si nous avions la possibilité de stocker cette valeur à un unique endroit, dans une unique variable, les choses se verraient grandement simplifiées ;
- le support des _mixins_ / fonctions : plus complexes, l'utilisation des _mixins_ peut se révéler d'un grand secours. Admettons que nous ayons différents éléments partageant un même style de bordure (type, couleur, etc.) modulo leur largeur et le rayon d'arrondi des angles. Les variables ne nous seront pas suffisantes ici : leur usage est limité au stockage de valeurs. En revanche, la _mixin_ apporte une réponse : elle nous permet de définir différentes règles à appliquer à l'élément l'utilisant, en prenant en entrée différents paramètres permettant de spécifier, par exemple, la largeur de notre bordure, et le `radius` de nos arrondis ;
- le support de la directive `@extend` pour gérer un héritage entre les composants : complémentaire des _mixins_, `@extend` étend les notions d'héritage. Admettons qu'un élément partage plusieurs styles avec d'autres éléments. Les _mixins_ sont pratiques pour générer des portions de codes ayant une ou plusieurs valeurs variables. En revanche, elle ne permettent pas de mutualiser plusieurs styles, ou difficilement. C'est le rôle d'`@extend`. Cette directive va nous permettre de spécifier qu'un élément utilise les mêmes styles de bordures qu'un élément A, et les mêmes réglages de typo qu'un éléments B, et ainsi de suite… On peut comparer son usage à celui des classes HTML, directement intégré à nos feuilles de style.

Certaines sont en cours de discussion au sein du CSS Working Group au W3C. D'autres, comme `@extend` se montrent clairement dignes d'intérêt, mais sont encore dans les cartons…

Les plus vigilants auront déjà repéré que les lacunes que je souligne ici sont avantageusement comblées par les pré-processeurs CSS : SASS, Less et Stylus pour ne citer qu'eux. Ils nous offrent cette souplesse du développement procédural dans un environnement déclaratif pour simplifier et faciliter notre usage de CSS.

### Pré-processeurs à la rescousse ?

Ils sont de plus en utilisés au quotidiens par nombre d'intégrateurs. Ils nous offrent ce que nous attendions de CSS depuis plusieurs années. Ils repoussent les limites du langage vers de nouveaux horizons…

Ils sont **les pré-processeurs CSS** !

Pour reprendre l'introduction de la page d'accueil de [SASS](http://sass-lang.com) :

> Sass est une extension à CSS3, ajoutant l'encapsulation des règles, les variables, les _mixins_, l'héritage de propriétés, et plus encore…

Quelle promesse !

Alors oui, sans les pré-processeurs, la méthode que je vous présente ici ne peux pas fonctionner, car elle repose sur les 3 éléments précités (variables / _mixins_ / @extend) que n'offre pas encore le langage nativement. Mais il serait abusif de penser que les pré-processeurs sont une réponse ultime. Le problème de désorganisation des CSS ne vient pas de CSS. Le problème ne vient pas du manque de fonctionnalités…

**Le problème vient de vous.**

L'organisation de votre code repose uniquement sur votre propre organisation, et sur votre faculté à respecter une structure, des règles, un nommage précis et une cohérence donnée. Les pré-processeurs et les _frameworks_ CSS ne sont que des outils dans les mains de l'intégrateur. Ils nécessitent également une grande vigilance : comme tout _process_ automatisé, et même s'ils sont optimisés pour limiter les effets de bord, un usage inconsidéré des pré-processeurs provoquera une prise de poids inconsidérée de votre CSS en sortie, notamment à cause de la redondance de certaines règles. Attention donc à ne pas les considérer comme la réponse ultime.

### _We are legions_

Car au début de la conception de cette méthode, il n'y avait pas la volonté de mettre au point la _nouvelle librairie dont personne n'allait pouvoir se passer_®. Il n'y avait même pas la volonté de trouver _une méthode qui fonctionne sans se prendre les pieds dans le tapis_™. Au début, il y avait simplement la frustration de constater que, quand on passe derrière un autre intégrateur, ou à plus forte raison qu'on travaille à plusieurs sur le développement _front-end_, on n'est jamais d'accord.

Bien souvent, chacun y va de sa petite recommandation, de sa petite habitude de nommage, de ses petites _fonctions super-pratiques-qui-font-gagner-du-temps-tu-vas-voir_©®™. Si ce n'est pas une recette efficace pour travailler ensemble sur la durée, c'est en tout cas une recette formidable pour pondre un plat de spaghettis.

Je développe des sites web depuis 1996 (la première fois via Publisher. Vous pouvez rire, mais quand on y connaît rien, c'était un bon moyen d'obtenir une structure HTML de départ à peut près compatible avec Internet Explorer… et je n'en suis pas fier, à chacun ses casseroles). Je fais partie de ces développeurs travaillant autant en _front_ qu'en _back_. Et au quotidien, il m'arrive fréquemment de constater que des problèmes rencontrés en développement côté serveur (nommages, développement de librairies, architecture, etc.) et qui finissent par trouver des solutions, se posent souvent en _front_ également mais sont malheureusement souvent plus difficiles à résoudre. Généralement, il s'agit surtout de problèmes structurels, ou d'organisation. Mais là ou les développements sont souvent issus d'un travail collaboratif entre plusieurs développeurs, les intégrations sont souvent le fait d'un unique intervenant.

Lorsque nous sommes amenés à travailler sur des projets où plusieurs personnes ont la charge du design et de l'intégration, maintenir à plusieurs une unique feuille de style désorganisée, c'est l'assurance d'effets collatéraux indésirables (vous savez, cette journée entière perdue à tenter de réparer un style qui avait sauté suite à l'intervention d'un collègue).

L'idée de découper la structure de présentation en entités modulaires minimise ces risques. Chaque élément d'interface est isolé, fonctionnant comme un élément autonome. Ce découpage va conjointement faciliter la maintenance et l'évolution des styles du-dit composant ; isoler son fonctionnement du reste des éléments de la page pour limiter ses impacts sur la feuille de style globale ; et même permettre aux différents intervenants de se focaliser sur un élément donné plutôt que sur l'ensemble des composants.

C'est également un très bon moyen d'appliquer une philosophie DRY (_Don't Repeat Yourself_ - Ne vous répétez pas) à vos projets. Derrière cet acronyme se cache une idée simple : chaque portion de code est unique. Si vous ressentez le besoin de dupliquer votre code quelque part à grands coups de _copier-coller_, alors vous devez pouvoir mutualiser votre code en un unique endroit pour le réutiliser à plusieurs reprises (via l'utilisation de fonctions / _mixins_). Vous vous faciliterez ainsi la maintenance, en n'ayant plus qu'un point d'intervention lors d'une modification, plutôt que de devoir rechercher chaque occurrence du code dans l'ensemble du projet.

Car dans le cas d'une équipe d'intégrateurs, on peut pousser le fonctionnement de la méthode suffisamment loin pour que les différents collaborateurs puissent dédier leur efforts à un composant à un instant donné sans avoir nécessairement besoin de connaître le fonctionnement des autres composants de la page. Une vue d'ensemble peut suffire.


