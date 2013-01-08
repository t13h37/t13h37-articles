# Bonnes pratiques : connaissez votre histoire

Nous essayons tous de faire notre travail au mieux, et évidemment les sources sur internet sont plus ou moins fiables. J’ai compilé ici un certain nombre de conseils dont j’ai souvent eu besoin, en espérant que ça vous évite de chercher à votre tour.


## Mise en page

J’ai dû une fois ou deux lutter pour arriver à positionner une barre de navigation sans recourir à un `frameset` compliqué. Voici le code pour arriver à mes fins :

~~~ {lang="html" line="1"}
<table cellpadding="0" cellspacing="0">
    <tr>
        <td valign="top"> NAVIGATION </td>
        <td valign="top"> TEXTE </td>
    </tr>
</table>
~~~

Attention à bien prendre en compte le fait que l’attribut `valign` (alignement vertical) doit être présent sur chacune des cellules de ce tableau, sans quoi si jamais votre texte est court et votre navigation longue, le texte ne sera plus calé en haut de la page au même endroit que la navigation !

Les attributs `cellpadding` et `cellspacing` servent à bien rapprocher les cases du tableau pour que ce soit plus joli. Si vous souhaitez espacer un peu la navigation et le contenu, vous pouvez ajouter une cellule entre les deux, dans laquelle il sera commode d’insérer une image « vide » dont on fixera la taille. Habituellement on utilise un gif transparent de 1*1 pixel. Rassurez-vous, son poids est très raisonnable (50 octets environ), il devrait donc s’afficher assez vite en toutes circonstances. Voilà un exemple pour une marge de 10 pixels entre la navigation et le contenu de la page :

~~~ {lang="html" line="1"}
<table cellpadding="0" cellspacing="0">
    <tr>
        <td valign="top"> NAVIGATION </td>
        <td valign="top"><img src="img.pixel.gif" width="10" height="1"></td>
        <td valign="top"> TEXTE </td>
    </tr>
</table>
~~~

Cette méthode d’alignement vertical marche avec tous les navigateurs.


## Navigation : un effet de survol

Pour que votre barre de navigation soit un peu plus jolie, nous allons maintenant faire un « effet de survol ». Une barre de navigation, quand c’est une liste de liens textuels, c’est triste : ça ne bouge pas et la typographie laisse souvent à désirer. Nous pourrions donc les remplacer par des images, et en même temps ajouter un effet dynamique quand notre souris passe dessus. Attention c’est un peu technique, mais vous pourrez directement copier-coller le code que je vous propose, n’ayez pas peur !

Tout d’abord allons dans Adobe Image Ready (ou Paint Shop Pro si vous l’avez, mais je préfère Image Ready pour les découpes d’images, vous allez voir plus loin) et dessinons notre barre de navigation :

![Figure 1 : une navigation statique dans Image Ready](fig1.gif)

Une fois cela fait, préparons aussi des versions « survol » :

![Figure 2 : le lien « Accueil » est bleu marine et comporte un ombré](fig2.gif)

Attention, ce script ne marche pas partout ! Internet Explorer ne le permet pas, nous allons donc devoir **filtrer** le script pour ne pas générer de message d’alerte. Heureusement c’est assez simple, il suffit de demander au navigateur s’il s’appelle Netscape :

~~~ {lang="javascript" line="1"}
if(navigator.appName=="Netscape")
~~~

Ensuite pour simplifier le travail, nous allons charger d’avance les images dont nous aurons besoin au survol grâce à une ruse de Javascript : si on crée un nouvel « objet image », son contenu sera téléchargé. (Note : ne me demandez pas ce qu’est un « objet image », l’important vous allez le voir est que ça marche, très très facilement.)

Le HTML est assez simple, il suffit de nommer chaque image à l’aide de l’attribut `name` (d’où son nom). Par exemple pour le lien « Accueil », ça nous donne :

~~~ {lang="html" line="1"}
<a href="accueil.htm"><img src="accueil.gif" alt="Accueil" name="accueil"></a>
~~~

Ensuite dans notre Javascript nous allons créer un nouvel « objet image » au chargement de la page, et aller chercher le fichier correspondant pour le mettre d’avance dans le cache du navigateur, donnant ainsi l’illusion de l’immédiateté :

~~~ {lang="javascript" line="1"}
if(navigator.appName=="Netscape") {
    imgaccueil = new Image();
    imgaccueil.src = "accueil_survol.gif";
}
~~~

Maintenant il ne nous reste plus qu’à ajouter le comportement dans notre lien :

~~~ {lang="html" line="1"}
<a href="accueil.htm" onmouseover="document['accueil'].src='accueil_survol.gif'"  onmouseout="document['accueil'].src='accueil.gif'"><img src="accueil.gif" alt="Accueil" name="accueil"></a>
~~~

Facile, non ?

Vous devez vous demander d’où vient cette notation bizarre, `document['accueil']` ? C’est assez simple, en fait : on appelle ça le DOM de niveau 0 (ne me demandez pas ce que ça veut dire), et ça permet de dire « Je veux faire quelque chose à l’objet dont le `name` est “accueil”. »

Simple, non ?

Note : vous pouvez trouver une leçon complète de substitution d’images sur [http://www.ryerson.ca/JavaScript/lectures/newIndex.html](http://www.ryerson.ca/JavaScript/lectures/newIndex.html)


## Images lourdes

La bande passante de la personne qui consulte le site que vous avez développé n’est pas forcément la vôtre. Vous avez la chance de travailler dans une agence dont le web est le métier, ne l’oubliez pas ! Pensez donc à découper vos grosses images en plusieurs morceaux, vous donnerez ainsi à votre visiteur l’illusion d’un chargement plus rapide.

Pour ce faire, c’est simple : découpez plusieurs morceaux dans votre éditeur d’images. Vous n’avez pas besoin d’être hyper précis, vous pouvez y aller à la louche, l’important étant de faire des morceaux qui se chargeront plus vite qu’une gigantesque image. Par exemple, pour le site du parfumeur Simone nous allons, sur la page d’accueil, mettre en avant la nouvelle fragrance « Entre hommes ». L’image est assez grosse (564*343), faisons 4 tranches.

![Figure 3 : une découpe d’images pour la page d’accueil](decoupe_grosse_image.png)

Il nous suffit alors de mettre ces images dans un petit tableau discret, sans bordures ni padding :

~~~ {lang="html" line="1"}
<table cellpadding="0" cellspacing="0" border="0">  
    <tr>  
        <td><img src="parfum_01.jpg" width="263" height="160" border="0"></td> 
        <td><img src="parfum_02.jpg" width="270" height="160" border="0"></td> 
    </tr>  
    <tr>  
        <td><img src="parfum_03.jpg" width="263" height="142" border="0"></td> 
        <td><img src="parfum_04.jpg" width="270" height="142" border="0"></td> 
    </tr>  
</table>
~~~

Pensez bien à mettre les balises de cellule (`td`) et les balises d’images (`img`) sur la même ligne, sans quoi le calage ne sera pas parfait : il restera un espace entre chaque ligne d’images.


## Revoyons l’action au ralenti

Arrêtons là les dégâts : arrivé à ce niveau d’avancement dans votre lecture, vous penserez vous être trompé de site ou que j’ai abusé de foie gras et de champagne hier soir pendant le réveillon alors que j’aurais dû les consommer avec modération et/ou manger cinq fruits et légumes, et vous n’auriez pas tort, mais nous nous égarons.

Qu’est-ce que nous venons de lire ? Des bonnes pratiques, des conseils sincères qui étaient dans l’ensemble assez solides quand j’ai commencé à travailler comme « intégrateur Web » (dénomination générique et approximative qui date de l’époque où on n’était pas vraiment sûr de ce que faisaient les développeurs qui transformaient un dessin dans Photoshop en code dans un navigateur).

Pour la bonne bouche (c’est Noël, après tout), reprenons ces conseils et détaillons ce qui ne va pas (si vraiment vous savez déjà tout, passez directement à la section suivante, « Des bonnes pratiques et de la façon de s’en servir »).

* Les tables de mise en page. Je vous entends d'ici partir d'un grand rire, la tête en arrière, en me prenant pour un fou : c'est tellement dépassé, comme concept ! Détrompez-vous. Ah ça, mais, qui donc ose encore en produire encore de nos jours, me demanderez-vous ? Comme je suis un gentil garçon, je ne donnerai pas de nom, et ce n'est même pas le fait de débutants : certains progiciels très implantés sur le marché de l’entreprise présentent encore toute leur interface dans des tables imbriquées, elles-mêmes dans des tables imbriquées, etc. Oui, moi aussi j’ai mal (le foie, peut-être ?).
* Nous étions persuadés que l’attribut `valign` fonctionnait partout, ce qui rassurait les designers et les intégrateurs. Mais à l’époque où cette pratique était systématique, peu de gens savaient que l’alignement vertical était inopérant dans Opera 3 tandis qu’il ne posait aucun souci à Internet Explorer 4 et à Netscape 4. Il y aurait un article à écrire sur le lâcher prise, et ça tombe bien, c’est déjà fait : [Le Tao du Web design](http://www.pompage.net/traduction/dao) de John Allsopp, est un article fondateur dont il faut s’imprégner encore et encore, même aujourd’hui.
* Les gifs d'espacement (ou <em lang="en">spacer gifs</em> comme on disait à l'époque). Là, ouf, nous sommes tirés d'affaire.  
* Les barres de navigation en image avec des rollovers hideux. Là, c'est vous qui éviterez de donner des noms (c’est la trêve des confiseurs, faisons preuve de bonté), mais ça existe encore.  
* `if(navigator.appName=="Netscape")` : ne jamais, au grand jamais, tester le nom d'un navigateur. Il faut systématiquement tester sa capacité à manipuler les objets. (Au passage, ce test renvoie « vrai » avec un Firefox tout récent, et vous avouerez qu'il y a pourtant peu de points communs entre le Firefox de 2012 et le Netscape 4 de 2002.)  
* `onmouseover="document['accueil'].src='accueil_survol.gif'"` : triple faute !  
    - premièrement, ne mélangeons pas le comportement (action de survol) avec le contenu (le HTML).  
    - deuxièmement, on n’a pas testé la capacité du navigateur à faire l'action demandée : comprend-il le DOM de niveau 0 ?`document['accueil']` ? Sait-il que c'est une image ? A-t-il accès à la propriété `src` de l'objet image ? Après tout, comme je le disais plus haut, ce code ne marchait effectivement pas à l’époque avec Internet Explorer 3 ou 4 (j’avoue que j’ai oublié la version, depuis le temps).  
    - troisièmement, on oublie la navigation au clavier (et donc les événements associés au `focus` et au `blur`) ; c’est moins grave, mais tant qu’à bien faire les choses, soyons exhaustifs.  
* Quant à l'image lourde que nous avons découpée en quatre plus petites images pour donner l'illusion de rapidité : ha ha ha ! Comme vous, j'éclate d'un rire lancé vers le ciel, plein de la superbe que nous confèrent les années passées. On ne fait plus ça, malheureux ! Ce que nous ne pouvons pas réduire, on le sait bien maintenant, c'est toute la couche de négociation HTTP. Dans notre exemple, il a fallu quatre requêtes HTTP pour une seule image finale, et sur la plupart des combinaisons serveur/navigateur actuelles, on ne peut faire que deux requêtes simultanées vers le même serveur.
* Faut-il répéter que j’ai fait exprès d’oublier les `summary` sur les `table` et les `alt` sur les `img` ? Et me faut-il vous avouer que j’ai fait des dizaines de sites sans l’un ni l’autre attribut, ne les connaissant pas encore, à la grande époque où les serveurs web marchaient encore à la vapeur ?

## Des bonnes pratiques et de la façon de s’en servir

Alors, pourquoi ai-je égrené tant d’exemples et de code pour finir par tout démonter dans le paragraphe précédent ? Ai-je finalement perdu hier soir les rares neurones que mon grand âge avait épargnés ?

Non, c’est pire que ça : toutes les pratiques que j’ai détaillées ont un jour été de **bonnes** pratiques. Si, si. Évidemment, la moitié du lectorat du Train de 13h37 n’était pas là avant guerre (je parle de la guerre des navigateurs, n’exagérons rien), mais toutes ces pratiques ont un jour fait loi. Nous les recommandions aux nouveaux, les échangions sur les sites de partage et dans les listes de discussion, et les appliquions quotidiennement.

J’ai personnellement massacré de nombreuses grosses images pour en faire des petits morceaux plus faciles à charger, passé des heures à chasser l’espace indésirable entre une balise `img` et la `td` qui l’encadrait tout en omettant le texte alternatif qui aurait permis de comprendre ce qu’était ce saucissonnage, minutieusement découpé des barres de navigation à deux états, normal et survol, maniaquement copié des bouts de Javascript qui demandaient leur nom aux navigateurs plutôt que de s’assurer de leurs capacités.

Où est-ce que je veux en venir, me demanderez-vous, tandis que, Noël passé, vous devez maintenant commencer à penser à tartiner les petits fours du Premier de l’An et qu’on n’a pas que ça à faire ?

La morale de cette histoire est assez simple :

1. **Les bonnes pratiques sont relatives**. Le recul que nous confère l’histoire, quand on la connaît un tant soit peu, nous force à rester très méfiants : la bonne pratique d’aujourd’hui peut devenir la mauvaise pratique de demain. (Un autre exemple ? Très récemment encore, on continuait à dire qu’il valait mieux conserver les appels aux fichiers Javascript dans le `head` pour bien séparer les choses, avant de réaliser qu'il valait mieux, pour des raisons de performance, les appeler une fois la majorité du code de la page chargée, tout en bas du `body`.)
2. **Votre veille technique doit être permanente**. Il nous faut sans arrêt rester aux aguets, sous peine de manquer le train des nouvelles pratiques – qui à leur tour pourront un jour être supplantées, mais dans un médium aussi volatil que le Web, c’est le présent qui gouverne notre travail : appliquons donc au mieux un maximum de bonnes pratiques récentes, et restons très attentifs.  
Par ailleurs, votre veille doit être protéiforme, et couvrir de nombreux domaines (optimisation de code, méthodes de minification, commentaires conditionnels ou pas, observation des parts de marché des navigateurs selon le parc que vous ciblez, nouveaux périphériques, nouveaux modes de consommation des sites Web, accessibilité évidemment, et j’en oublie). Rassurez-vous tout de même : personne ne sait tout, personne n’a la science infuse, et ceux qui regardent d’un air condescendant les quelques erreurs que vous avez faites ici ne savent pas encore qu’ils se trompent là.

En résumé : ne nous reposons jamais sur nos acquis et soyons toujours capables de savoir d’où vient une pratique. Connaître l’histoire du médium, même sur une période aussi courte, nous permet autant de comprendre ce que nous faisons que de le questionner pour toujours faire mieux.

Vous me direz que j’enfonce une porte ouverte ; reparlons-en dans dix ans.

