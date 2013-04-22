# Connaître l'efficacité d'un site via Google Analytics

Voilà, vous avez un nouveau client, et ce dernier vous a demandé la totale : un nouveau site, des campagnes de newsletters, etc. Le projet est intéressant, tout va bien dans le meilleur des mondes.

Vous êtes prêts à vous lancer comme une locomotive, et ce client (ou son service marketing) vous pose une question de ce genre :

*« Et au fait, il sera possible de chiffrer nos gains ? »
*« Vous avez des outils pour tester l'efficacité du nouveau site ? »

Aïe ! Vous n'êtes pas très calé en statistiques, votre métier c'est de développer/intégrer et pas de cracher des chiffres pour des marketeux, surtout que le budget n'inclut pas le développement d'un module spécifique complet… Et puis, comment chiffrer simplement et rapidement le Saint-Graal des marketeux, à savoir le Retour Sur Investissement ? (ROI en anglais, *Return On Investment*).

Et bien, j'ai une bonne nouvelle ! Ce n'est pas si difficile que cela : avec l'implication de votre client et l'utilisation de Google Analytics, vous allez pouvoir produire des statistiques et évaluer le ROI de vos campagnes, voire même de certains processus.

Mise au point : même si cet article aborde divers points de marketing ou parle d'argent, **il ne s'agit PAS d'un cours de marketing** (je serais bien en peine de l'assurer, ce domaine n'étant pas du tout le mien). L'article s'intéresse uniquement aux questions techniques pour mettre en place des solutions pour faire remonter des informations.

## Les bases de Google Analytics

### Le code de *tracking*

Commençons par le commencement, pour installer Google Analytics vous devez vous inscrire sur le [site de Google Analytics](http://www.google.com/analytics/). Après quelques étapes, vous obtenez un code de *tracking* qui ressemble à cela :

~~~ {lang="javascript" line="1" highlight="1"}
<script type="text/javascript">
  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-XXXXXXX-X']);
  _gaq.push(['_trackPageview']);

  (function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
  })();
</script>
~~~

Ce code est à insérer dans le `head` de votre page, en remplaçant bien sûr le numéro de compte (`UA-XXXXXXX-X`) par celui qui vous sera donné. Une fois mis en place sur vos différentes pages, il les *trackera* selon leur URL.


### Page tracker virtuel

Le *Virtual Page Tracker* est un outil très utile qui consiste à spécifier un paramètre dans le code donné ci-dessus, par exemple :

~~~ {lang="javascript" line="1" highlight="1"}
 _gaq.push(['_trackPageview', '/mapage-virtuelle.php']);
~~~

Ce code permettra de *tracker* une page en en spécifiant le nom. Ainsi, vous pourrez chercher dans les pages *trackées* la page « /mapage-virtuelle.php ». D'apparence simple, cette possibilité très puissante va permettre de construire des URLs à votre convenance, lesquelles pourront alors être *trackées* et classées.

Vous me direz qu'idéalement il faudrait s'en passer car les URLs d'un site doivent être bien construites et aussi intelligibles que possible. Effectivement… dans le cas où l'on *tracke* les pages d'un site. Plaçons-nous dans le cas d'un formulaire d'inscription. La page de remerciement aura peu ou prou toujours la même URL, et cette dernière est peu « informative ». Par contre, selon les choix effectués dans le formulaire, nous pouvons construire une URL virtuelle plus intelligente. J'y reviendrai dans les exemples pratiques plus bas.


### Event Trackers

Il est possible aussi de tracker un événement (un clic sur un lien, une action de l'utilisateur, etc.) grâce aux *Event Trackers*. Leur structure est la suivante :

~~~ {lang="javascript" line="1" highlight="1"}
_gaq.push(['_trackEvent', 'category', 'action', 'label']);"
~~~

Exemple :

~~~ {lang="html" line="1" highlight="1"}
<a href="mailto:tchoutchou@letrainde13h37.fr" onclick="_gaq.push(['_trackEvent', 'email', 'click', 'tchoutchou@letrainde13h37.fr']);">contacter Le Train</a>
~~~

Ainsi, dans le rapport des événements, le clic sur ce lien *mailto* sera indiqué.



## Passer à la pratique

Maintenant que nous savons tracker des pages ou des événements sur le site, il est temps de passer du côté de Google Analytics pour définir des objectifs, et le cas échéant les chiffrer.


### Mettre en place un objectif simple

Sous Google Analytics, mettre en place un objectif se fait sous Admin > Profil, dans l'onglet Objectifs.

L'objectif peut être une URL, une correspondance de l'URL à une expression régulière, etc. Il peut être placé sur une URL, sur un évènement, etc.

Prenons un exemple simple : supposons que votre site comporte un formulaire de demande de devis. Après discussion avec le client, vous avez convenu qu'une demande de devis sur le site valait 100 euros. L'URL de l'objectif sera celle de la page de remerciement, celle affichée une fois le formulaire soumis. Dans notre exemple, l'URL de cette page est « /source/envoyer_message.php ».

L'objectif se définit donc comme dans l'image ci-dessous.

![Mise en place d'un objectif simple](ga_objectif_simple.jpg "Mise en place d'un objectif simple")

Une fois l'objectif défini, toutes les URLs trackées qui lui correspondront seront comptabilisées comme des conversions (= des objectifs atteints).


### Chiffrer le Retour sur Investissement (ROI) d'une campagne e-mail via des inscriptions

Supposons que nous ayons un client qui s'appelle « Le Train ». Il décide d'envoyer une newsletter pour des inscriptions pour des cours (des formations diverses et variées dans le domaine du Web) : elle contient un lien qui emmène vers un formulaire d'inscription. Il y a quatre lieux pour les cours : la Gare Montparnasse, la Gare du Nord, la Gare Saint-Lazare et la Gare de Lyon (oui, j'adore le Monopoly).

Afin de simplifier, on va coder sur trois lettres chacun des lieux des cours : GMP, GDN, GSL, GDL.

Voici le formulaire :

~~~ {lang="html" line="1" highlight="1"}
<select name="lieu" id="id_lieu">
    <option value="GMP">Gare Montparnasse</option>
    <option value="GDN">Gare du Nord</option>
    <option value="GSL">Gare Saint-Lazare</option>
    <option value="GDL">Gare de Lyon</option>
</select>
~~~

Selon le lieu du cours choisi, la page de remerciement sera trackée avec un page tracker virtuel construit ainsi : /le code du lieu>-thanks.php  
Par exemple, si la personne qui s'est inscrite a choisi un cours à la Gare de Lyon, le tracker virtuel sera « /GDL-thanks.php ».

Exemple simple de code sur la page de remerciement :

~~~ {lang="javascript" line="1" highlight="1"}
_gaq.push(['_setAccount', 'UA-XXXXXXX-X']);
_gaq.push(['_trackPageview', '/{lieu}-thanks.php']);
~~~

Revenons maintenant sous Analytics pour mettre en place les objectifs.

Dans ce cas, l'objectif sera une correspondance à une expression régulière : `^/(GMP|GDN|GSL|GDL)-thanks\.php`.

(pour les allergiques aux expressions régulières : tout ce qui commence par GMP ou GDN ou GSL ou GDL suivi de -thanks.php, le point devant être échappé par un anti-slash)

![Objectif avec expression régulière](ga_objectif_expression_reguliere.jpg "Objectif avec expression régulière")

Note : Il est bien sûr possible de savoir le nombre de personnes qui vont cliquer sur le lien dans la newsletter (par exemple pour connaître le ratio nombre de pages vues/nombre de *mails* envoyés), mais ce n'est pas ce qui nous intéresse ici. Le but est de savoir combien **rapporte** la campagne.

Passons maintenant aux résultats : sous Google Analytics, vous pouvez aller sous Conversion > Objectifs. Là, vous pouvez choisir un objectif, et voir les rapports : 

![Résultats de la campagne](ga_objectif_resultats_formulaires.jpg "Résultats de la campagne")

Dans cet exemple, « Le Train » a envoyé la newsletter à 300 prospects, il y a eu 1 cours pris à GMP et 6 cours pris à GDN.

Connaissant le prix pour avoir créé la campagne (1000 euros), celui d'un cours (400 euros), on peut en déduire que la campagne, même si elle n'a apporté que 7 inscriptions, a rapporté 2800 euros. L'investissement est rentable !

Vous pourriez me dire que pour de si petits chiffres, mettre tout cela en place était un poil compliqué, le client « Le Train » n'avait qu'à compter les inscriptions lui-même et faire la soustraction. Je vous répondrai deux choses. 

Une déjà, l'exemple était volontairement très simple. Imaginons à plus grande échelle : notre client « Le Train » a grandi, c'est une multinationale nommée « Train Tycoon » (oui, j'adore aussi Transport Tycoon). En tant que responsable du site internet, vous traitez avec la maison mère. Gardez à l'esprit ceci : votre client est la maison mère, vous ne traitez pas avec les succursales.

Si la campagne est lancée à l'échelle d'un pays (ou de plusieurs), faire remonter les informations manuellement peut être compliqué et/ou chronophage. Or, avec ce genre de système, les infos remontent toutes seules et sans effort. Mieux, la mise en place de ce genre de système ne grandit que peu de l'échelle « 4 succursales dans une ville » à « 100 succursales dans 3 pays ».

Deux, cela participe à un effort de transparence entre le client et vous. Le client ne pourra pas quémander en vous demandant de baisser vos prix car le site ne rapporte pas : vous avez des chiffres pour appuyer votre bonne foi, si par exemple la campagne d'e-mailing a coûté 1000 euros mais qu'elle en rapporté 5000. Bien entendu, cela marche aussi dans l'autre sens : vous ne pouvez pas vous gausser de 1000 inscriptions si cela éponge à peine les coûts de la campagne.

Évidemment, là, on parle de *ROI* positif. Il est également possible de chiffrer des *ROI* négatifs. Supposons par exemple qu'un formulaire de contact ait un champ `select` « Objet de votre demande » avec plusieurs choix. Certains de ces choix sont supposés être des *ROI* négatifs : des demandes d'informations à propos d'une rubrique FAQ sur le site (qui est censée être exhaustive et diminuer les appels ou les e-mails, et donc faire gagner du temps au Service Client). Là, on pourra évaluer d'une part la perte occasionnée, et surtout voir l'évolution au fur et à mesure de l'enrichissement/l'amélioration de cette rubrique. C'est un excellent outil pour travailler à l'amélioration d'un site.

Danger : il est important d'expliquer à votre client et de garder à l'esprit que même si cet outil est très puissant, il n'est ni l'alpha ni l'oméga (ne serait-ce que parce qu'il est basé sur JavaScript, qui peut être désactivé par l'agent utilisateur). Il est juste là pour sortir des informations aussi neutres que possible, l'interprétation des résultats et les hypothèses qui en découleront sont un autre problème, qui peut être délicat. Par exemple, difficile de dire à notre client « Le Train » que, même en dépit de nos efforts pour améliorer la FAQ concernant le service expédition, les ROI négatifs continuent. Certes, le site internet peut améliorer sa FAQ, mais si le service expédition n'est pas efficace et accumule les retards… bref, vous voyez le genre de problème : dans ce cas, ce n'est pas nécessairement le site qui a un problème, mais l'entreprise.

Bref, sachez rester à votre place si votre client demande des interprétations !


### Utilisation des *funnels* pour voir l'efficacité d'un processus « complexe »

Une autre possibilité de Google Analytics est de voir le chemin parcouru pour atteindre un objectif. On appelle cela les « entonnoirs de conversion » ou les « *Goal Funnels* » en langue de Shakespeare. Comme précédemment, vous définissez un objectif, et vous ajoutez des étapes (obligatoires ou non) pour atteindre cet objectif.

L'avantage de ces *funnels* est de pouvoir visualiser l'efficacité d'un processus « complexe », comprenez en « plusieurs étapes ».

Prenons un exemple très simple, notre client « Le Train » a une boutique en ligne, et il y a 5 étapes depuis le panier jusqu'à la page qui confirme que la commande a été payée :

- le panier,
- un formulaire qui demande les coordonnées du client,
- un second formulaire qui propose les différentes options d'expédition,
- la page qui propose les modes de paiement,
- et donc la page qui confirme que le paiement a été bien effectué.

Voici comment cela se met en place sous Google Analytics :

![Mise en place d'un funnel](ga_objectif_funnel.jpg "Mise en place d'un funnel")

C'est très semblable à un objectif classique : vous mettez d'abord l'adresse finale, et vous ajoutez les étapes ensuite. Une fois tout cela mis en place, il ne reste plus qu'à attendre et collecter les données… distorsion temporelle à 88 miles à l'heure… magie, deux semaines plus tard après cette mise en place, les résultats sont là !

![Les résultats du funnel](ga_resultats_funnel.jpg "Les résultats du funnel")

On peut voir que sur le schéma de l'entonnoir, un point saute aux yeux : la troisième étape montre un fort taux d'abandon. Encore une fois, le chiffre est livré tel quel, l'interprétation qui peut en être faite est un autre sport à part entière. Cette étape est-elle peu claire ? Trop compliquée ? Induit-elle en erreur au vu des URLs de sortie du *funnel* ? Les prix sont-ils prohibitifs ? Etc. Les hypothèses peuvent être très différentes. Toutefois, vous constatez qu'il se passe quelque chose sur cette page, et charge à vous de faire remonter l'information, ou d'essayer de l'analyser plus finement.



## Conclusion

J'espère avoir achevé de vous convaincre que la mise en place de ces outils est aisée. Pour ma part, même si je ne suis définitivement pas un marketeux, cela fait partie de mes habitudes de travail. Je suis resté assez simple dans les exemples, mais sachez que l'on peut combiner expressions régulières et *funnels* (et même aller bien plus loin), les possibilités sont quasi-infinies.

En tant qu'intégrateurs/développeurs, nous avons tendance à nous focaliser sur la création du site proprement dit et à délaisser ces histoires peu passionnantes de *ROI* ou d'efficacité. Toutefois, il est intéressant de s'emparer de ces questions, que ce soit de manière purement égoïste (pour voir l'efficacité de votre travail) ou plus ouverte (pour le service *marketing*).

Terminons sur un jeu de mot : n'oubliez pas que le *ROI* est roi chez les décideurs. Et qui s'occupe d'allouer du budget pour vous faire travailler ? ... À bon entendeur ! :)

