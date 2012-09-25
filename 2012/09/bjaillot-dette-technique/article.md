La dette technique est l'accumulation de risques impliqués par les choix techniques effectués tout au long de la vie d’un projet. Ces choix peuvent être volontaires ou non, et plus ou moins assumés.

Cet article sera l’occasion d’aborder les notions de gestion de projet agile, de qualité et, surtout, de documentation.

# Historique

Le terme de [dette technique](http://fr.wikipedia.org/wiki/Dette_technique) – selon wikipedia – provient initialement de la logique d’intérêts que l’on retrouve dans le calcul d’une dette dite financière : il s'agit de son application dans la vie d’un projet de développement logiciel.  
L’analogie illustre la notion d’intérêts : s’ils ne sont pas remboursés rapidement, le coût de la dette augmente jusqu’à un point où il n’est plus possible de la rembourser intégralement, et où tout paiement ne sert qu’à rembourser ces intérêts. Le projet n’est donc plus évolutif : tout ce qu’il est possible de faire est d’essayer de réparer les pots cassés au fur et à mesure de leur apparition.

La littérature disponible sur le sujet traite principalement des systèmes d'informations de grands comptes, sur des problématiques bien éloignées du quotidien des "acteurs du Web". Prenez votre moteur de recherche favori et faites une recherche, vous vous en rendrez compte par vous-même. Mon activité quotidienne m'emmène sur des dizaines de projets qui ont tous leurs historiques et qui ont souvent pour point commun d'être dans une situation relativement inextricable ou qui souhaitent éviter de l'être. C’est pour cela que j’en arrive à écrire cet article sur la dette technique, à destination des acteurs du web (nous) car nous subissons au quotidien des projets exposés à de nombreux aléas, sur des périmètres très mouvants et dans un contexte où les technologies et les usages avancent très vite.

Ces contraintes font que notre secteur d’activité est particulièrement propice à l’expansion de la dette technique dans les projets. Selon le rôle que l’on joue dans le projet, la perception que l'on en a varie du tout au tout. Pour caricaturer : le client peut mettre la pression pour que le projet sorte rapidement sans comprendre les enjeux techniques, le développeur sous-traitant en retard ne souhaite qu’une chose : en finir avec ce projet, le repreneur du projet  se demande ce qu’il va pouvoir faire avec cette horreur après un audit.

Dans cet article, nous allons distinguer trois types de dette technique : la volontaire assumée, celle qui est non assumée, et la dette technique involontaire.  
Passons-les en revue, en commençant par les plus préjudiciables.

## La dette involontaire

Résulte d’un mauvais choix technique de n’importe quel ordre (ergonomique, algorithmique, stratégique, etc.). Ses sources sont multiples : mauvais choix du framework, redondance de code, script copié/collé depuis un forum, etc. Le manque de connaissances (technique ou métier) ou la mauvaise communication au sein d’une équipe en sont les causes plus répandues.

## La dette volontaire non assumée

Résulte d’un choix technique pris en connaissance de cause mais dont le choix ou la mise en œuvre sont perfectibles. Les intervenants se renvoient la “patate chaude” au moment de l’apparition des problèmes dont on repousse la résolution à “plus tard”. Cette dette est la plus courante et est souvent due aux délais de réalisation très courts des projets, dans un périmètre  fonctionnel rarement fixé au préalable.

## La dette volontaire assumée

Résulte de tous les choix techniques n’appartenant pas aux deux premiers types de dette. En effet, tout choix implique des conséquences, et ce qui peut paraître la meilleure option à l’instant T, ne le sera peut-être plus à T+1, voir T+10, et il faudra malgré tout faire avec.


# Exemples anecdotiques

## Exemple 1 – la cuisine de Mme Michu ?

Il m'est arrivé de me retrouver dans une situation où l’illustration de la dette technique était parfaite : une cuisine aménagée, en place depuis quelques années, semblait en parfait état ; un jour, la cuisine s’est écroulée tout d’un coup, brisant tout ce qu’elle contenait et le carrelage qui l’entourait. Après analyse, il est apparu clairement que le poseur avait remarquablement bien travaillé : bonne préparation des murs et des meubles... Mais la jonction entre les deux était assurée par les fameuses vis et chevilles [Molly®](http://en.wikipedia.org/wiki/Molly_%28fastener%29) mal enclenchées. Un contrôle croisé de la pose et/ou une mini-formation sur l'utilisation de telles fixations aurait évité ce désastre.

Nous sommes là en présence d’une conséquence d’une dette technique involontaire. Un artisan a voulu faire son travail correctement, a rendu un chantier en parfait état, mais la situation n’en était pas moins catastrophique, avec une bombe à retardement non identifiée.

## Exemple 2  – les nouvelles balises de structure HTML5

Avec la sortie de la spécification HTML5 et son implémentation plus ou moins homogène dans les navigateurs modernes, se pose le choix de l’utilisation des balises de structure HTML5 pour votre nouveau site. (Non, je ne vous ferai pas de recommandation de choix, je préfère vous renvoyer à [cet excellent échange](http://letrainde13h37.fr/1/pour-ou-contre-html-5-en-production/) par Vincent Valentin et Christophe Andrieu).

Ce choix est déterminant sur tout le développement du site et implique des conséquences à tous les niveaux : développeurs, intégrateurs, compatibilité avec les navigateurs, etc.
Il faut établir une balance entre avantages et inconvénients, et justifier le choix d’une technologie sur l’autre.

C'est donc un exemple de dette volontaire assumée : la compatibilité ne peut que s'améliorer avec le temps.

## Exemple 3 – la contrainte IE6

Pendant longtemps, les sites intranet des grandes entreprises et administrations n’étaient conçus que pour Internet Explorer 6. On a coutume de majorer de 20 % le coût du projet. Mais le coût de la dette technique est bien supérieur au différentiel financier impliqué dans le coût de développement initial du site !  
Les limites techniques d’Internet Explorer 6 impliquaient quasi obligatoirement de *MAL* coder le HTML et le CSS pour qu’ils soient correctement interprétés, à ajouter des niveaux de balises supplémentaires, etc.

Aujourd’hui, les coûts de maintenance sont colossaux et les migrations de sites si complexes qu’ils en arrivent à empêcher de mettre à jour les systèmes d’exploitations des postes utilisateurs et qu'ils entraînent des complications dépassant le cadre de la maintenance du site ([source sur slashdot](http://tech.slashdot.org/story/10/10/29/149218/IE6-Addiction-Inhibits-Windows-7-Migrations)).

Ce dernier exemple est un cas de dette volontaire non assumée : les décideurs du moment n'avaient aucune idée des conséquences sur l'environnement complet des utilisateurs, développeurs et administrateurs.

# Méthodologies proposées

Quels sont les remèdes ? Attention, il n’y a, ici, rien de magique. Les premiers ne sont pas techniques (le comble), les suivants le sont un peu plus.

## Avant d’arriver à une situation de crise

### La prise de conscience

Le premier élément, le plus vital, est la **prise de conscience** que tout ce qui est fait a des conséquences, et qu’une fois en production les retours en arrière sont très difficiles, les deux seules possibilités étant de maintenir ou de réécrire. La prise de conscience et le partage de celle-ci dans des réunions quotidiennes permettent souvent d’améliorer la vision d’ensemble des participants, et donc d’arriver à des choix techniques plus adaptés.

Les méthodes agiles essayent de prendre en compte cette problématique autour de quatre valeurs fondamentales mettant en avant les individus et les interactions pour répondre de la meilleure manière possible aux besoins du client et du projet dans une logique itérative. Traiter de ce sujet nécessiterait un livre à part entière donc je vous propose [ce point de vue de Claude Aubry sur l'agilité comme réponse à la dette technique](http://www.aubryconseil.com/post/Dette-technique,-nique-nique).

### La documentation

Le deuxième point est la **documentation**. Je sais, c’est pénible, et moi aussi je **déteste** en écrire. Cependant, mes activités professionnelles m’amènent régulièrement sur de nouveaux projets où les choix techniques varient beaucoup, où je me dois de comprendre l’existant et de répondre à la question “comment en est-on arrivé là ?” avant de pouvoir critiquer et de faire un état des lieux adapté.

Il existe trois types de documentation, chacune servant son propos et dont le plus difficile est d'estimer comment les tenir à jour :

- la documentation purement technique qui explique comment et surtout pourquoi ça marche (exemple : commentaire dans le code) ;
- la documentation des choix techniques (très importante pour l’historique du projet, celle dont je vais reparler) ;
- et enfin, la documentation métier, qui est la vision de la maîtrise d’ouvrage.

Ces trois documentations sont essentielles, mais la deuxième est souvent méconnue et peu employée. C’est regrettable, car au-delà de la valeur des choix effectués, il est très intéressant de savoir *pourquoi* ce choix est fait, et les conséquences positives et négatives envisagées. Cela permet, une fois en situation plus douloureuse, de s’en remettre aux explications de l’époque, et de vérifier qu'elles soient toujours justifiées et d'actualité.

Les deux idées maîtresses autour de la documentation sont, d'une part qu'il est préférable de documenter le pourquoi plutôt que le comment, et d'autre part que bien que la documentation soit nécessaire, il faut documenter suffisamment mais pas trop ; c'est dans cet équilibre que réside toute la difficulté. Autrement, la documentation peut devenir une dette à elle toute seule.

Outils possibles : un document partagé et versionné : un README.txt, un wiki, un google doc, un etherpad.

### Clairement définir les critères de choix technique

Nous avons beaucoup parlé des choix effectués. Mais quels sont les critères à prendre en compte ? Que puis-je vous dire ? Tout dépend.  
Mais voici quelques pistes d'aide à la prise de décision :

- privilégier les composants dont les dépendances (y compris les numéros de version) sont clairement définies, et qui sont fournis avec des tests et/ou des démonstrations et de la documentation ;
- prendre le temps de vérifier la pérennité des composants choisis : un blog / un fil d'actualité à jour, un compte twitter actif, un dépôt de code actif, etc., sont autant de bons signes pour l'avenir de celui-ci. Dans le cas contraire, réfléchissez-y à deux fois : ce sera à vous de maintenir un composant (ou ses dépendances) abandonné(es) ;
- la communauté compte également pour beaucoup dans l'évaluation d'un composant. Plus elle est active, plus elle sera à même de s'adapter aux nouvelles problématiques et d'apporter des solutions aux problèmes que vous n'avez pas encore rencontré ;
- se tenir à jour : la veille technique est primordiale – mais je ne vous apprends rien puisque vous lisez aujourd’hui cet article.

Et enfin, tout au long du projet, il y a un certain nombre de bonnes pratiques à suivre pour éviter de crouler sous les intérêts : 

- _Release early, release often_ : Itérer, tester, publier, itérer, tester, publier, itérer, tester, publier. Pour cela, utiliser les méthodes agiles, comme nous avons pu le voir dans la section sur la prise de conscience.
- Impliquer un technicien dans toutes les phases du projet car il sera à même de prévenir et d'anticiper un certain nombre de risques en amont du projet, tout en augmentant sa compréhension du projet et des réels besoins fonctionnels. On constate aussi régulièrement des choix plus appropriés car la vision d’ensemble permet de ne se pas se focaliser sur les problèmes de l’instant présent, mais d’anticiper ceux à venir plus tard.
- Utiliser un gestionnaire de version et mettre en place un processus de _commits_ et de _merge_, qui permettent de séparer intelligemment les développements (on ne doit pas être empêché de corriger un bug quand on est en cours de développement d’une nouvelle fonctionnalité). Cette séparation des branches permet également de mettre en place des revues de code, avant tout _merge_, et donc d’augmenter sa qualité et la compréhension globale de celui qui valide le code. Il existe de nombreux outils, tels que git, mercurial, bazaar ; il y a aussi subversion mais la gestion des branches y est moins aisée.
- Mettre en place des tests, de plusieurs natures : unitaire, d'intégration, fonctionnels, en automatisant leurs exécutions afin qu'ils soient lancés à chaque changement de code à fusionner, notamment à travers des outils d'intégration continue. Comme la documentation, les tests peuvent se révéler comme une dette à part entière s'ils ne sont pas pris en compte avec rigueur.
- Automatiser les processus dans une optique d’industrialisation permet, avec une plus grande confiance, d’effectuer des opérations sensibles comme les déploiements en pré-production et production. L’utilisation d’outils de déploiement permet également de prévoir des retours en arrière sur une simple commande. 
- Tracer toute action effectuée, afin de pouvoir identifier le plus rapidement possible la cause d’un plantage.

## Des conseils plus spécifiques

Je distingue une idée maîtresse au sujet de la gestion des projets : établir une architecture modulaire et découper en composants. Une brique séparée peut-être testée individuellement, tracée, refactorisée, itérée.  L'utilisation de composants logiciels éprouvés (framework ou CMS) permet de s'abstraire d'une grande partie des problématiques courantes (pilotes d'accès aux base de données, accès au DOM, gestion complète d'HTTP, d'ajax). Cependant, ils ont souvent un **coût** (aussi bien en tant que dette technique, qu'en termes de performance et de support) et peuvent s'avérer une surcouche trop épaisse en fonction des besoins.

Le but étant de construire un projet, évaluer les briques fonctionnelles, définir leur périmètre, itérer. C'est un des fondements des méthodes agiles et un très bon support pour un projet réussi.

### Intégration côté client

Le code CSS est considéré – à raison – comme beaucoup plus difficile à appréhender dans un contexte de dette technique car il n'est pas testable, le principe de cascade (son principal atout) pouvant rapidement mener à des surcharges atroces quand le code est mal pensé. 
La question de sa professionnalisation a longtemps fait débat et, pour avoir échangé avec des intégrateurs de tous niveaux, la différence est monumentale. Je vais me répéter, mais ce qui fait la différence, c'est de comprendre le site dans sa globalité, de se tenir à jour de toutes les techniques, de mettre en place [des règles globales](http://www.stubbornella.org/content/2011/04/28/our-best-practices-are-killing-us/), puis d'établir les [spécialisation par composants](http://www.stubbornella.org/content/2010/06/21/css-granularity-architecture/). 

Des outils comme des pré-processeurs aident beaucoup dans la lisibilité, la maintenance et l'organisation du code, mais ils ont leurs propres inconvénients : se baser sur un compilateur rend votre code dépendant de celui-ci, ce qui est un ajout supplémentaire à votre dette technique.

Le code javascript côté client est souvent pris à la légère, alors qu'il fait maintenant partie intégrante de la conception d'application enrichie. Il doit donc être considéré comme du développement, et donc testé et industrialisé.

### Accessibilité

L'accessibilité est un sujet souvent pris à la légère en fin de projet, alors que si la prise en compte de cette problématique est effectuée dès la conception du projet, il n'y a quasiment pas de surcoût ([Elle peut même aider à mieux le vendre](http://letrainde13h37.fr/9/justifier-le-prix-de-la-qualite/)). Si elle n'est pas anticipée, on contracte alors une dette technique involontaire s'il faut la prendre en compte vers la fin du projet.

Les [checklists](http://checklists.opquast.com/) d'[Opquast](https://www.opquast.com/) peuvent vous aider à appréhender ces sujets dès les premières planches du projet.

### Code serveur

Le code serveur pose des problèmes de sécurité et de performance, en plus de devoir s'intégrer avec des gestionnaires de base de données, des outils de cache, etc. Le choix du framework / CMS / composants compte beaucoup, et surtout la valeur de son écosystème (extensions, intégration avec les éditeur de code, documentation).

Au-delà du code et du choix des outils, l'aspect intégration continue reliée aux tests me paraît primordial ; je vous propose donc ces ressources sur [le principe de l'intégration continue](http://www.geek-directeur-technique.com/2009/03/18/tests-unitaires-et-integration-continue/) et une [intégration élégante d'excellents outils](http://tech.m6web.fr/integration-continue-avec-jenkins-et-atoum).

### Infogérance

Qui n’a jamais vécu un dialogue de sourds entre les développeurs et les sysadmins, conduisant à des processus mal définis, des blocages à l’infini, des factures monstrueuses ? L’effort pour réduire ces effets de bord a donné le jour au mouvement [DEVOps](http://fr.wikipedia.org/wiki/Devops).

De nombreuses bonnes pratiques sont à recommander et elles vont toutes dans le même sens : rendre la notion d'environnements et de serveurs la plus transparente possible, afin de pouvoir se concentrer sur l'applicatif lui-même. Le choix d'un bon infogérant, et son intégration dans votre système d'information, vous permettra la mise en place d'outils d'intégration continue, la mise en production en un clic, la possibilité de retour en arrière, un monitoring complet des serveurs et de l'applicatif, mais aussi d'être à la pointe dans les logiques de cache.

### Face à une situation de crise

Autant le dire tout de suite, parfois, la solution est de tout reprendre à zéro : 

> I do think any complex enough project should at some time & for it's own sake be redone from scratch 
> – Nicolas Perriault (https://twitter.com/n1k0/status/237975635392360448)

Mais avant d’en arriver là (car ce n’est pas toujours nécessaire, ni envisageable), il faut adopter [des procédures](http://bitsquid.blogspot.fr/2012/08/cleaning-bad-code.html) qui permettent simultanément de corriger les bugs, de préparer de nouvelles fonctionnalités et de réduire la dette en nettoyant le code. 

Les étapes sont donc :

- l’évaluation de l’existant (il y a des méthodes, des outils et des experts pour ça) ;
- c’est là qu’un accès à la documentation et au gestionnaire de versions aide beaucoup. S'ils n'existent pas encore, il est alors primordial de le créer et de documenter tout le processus à venir ;
- par [rétroingénierie](https://fr.wikipedia.org/wiki/R%C3%A9tro-ing%C3%A9nierie) (ou [profilage](https://fr.wikipedia.org/wiki/Profilage_de_code)), documenter ce qui semble être le plus utilisé, supprimer le code et les commentaires trop anciens qui ne sont pas adaptés (c’est la non-réalisation de cette tâche qui a causé le bug informatique le plus coûteux de l’histoire avec l’échec du premier lancement de la fusée Ariane V, dû à la réutilisation du code inutile d’Ariane IV. [Source](https://fr.wikipedia.org/wiki/Vol_501_d%27Ariane_5)).
- figer l’existant (et ses dépendances, on l'oublie trop souvent), avec :
	- sauvegarde du contenu,
    - tag de la version, et création de branche pour la refonte,
    - pré-production spécifique,
    - tests fonctionnels sur les processus clés,
    - tests unitaires sur les méthodes clés,
- une migration impose souvent l’exécution d’un “script de migration” changeant la structure de la base de données, du nettoyage, des ajouts de clés. L’essentiel sur ce point est de prévoir des scénarios rejouables et, idéalement, réversibles ;
- identifier tous les points réellement bloquants et effectuer des quicks-win pour réparer la situation.

Une piste trop souvent ignorée est la possibilité de mettre en place un "pont" entre l'applicatif en l'état et la future version, ce qui permet des sorties itératives et qui est bien plus efficace qu'une réécriture depuis zéro et une migration en un coup. 


# Conclusion

J’imagine bien que votre vie n’a pas changé à la lecture de cet article, mais j’espère qu’elle vous aura au moins donné un peu de recul sur une (des) situation(s) que vous rencontrerez forcément dans un projet, que vous soyez à l’origine des choix ou tributaire de leurs conséquences.

Mettre en place les outils et méthodologies citées peut effectivement avoir un coût financier et humain supérieur à celui de votre méthode actuelle, mais il faut prendre en compte la satisfaction globale augmentée, un code plus propre et mieux maintenu vous permettant de travailler dans le futur plus efficacement et potentiellement à moindres coûts.

Pour résumer : 

- tout choix a des conséquences ;
- effectuez vos choix en connaissance de causes ET justifiez-les par écrit dans un fichier README.txt ou votre wiki préféré ;
- les choix techniques que vous effectuez peuvent être contraints aux limites de vos connaissances : échangez avec d’autres professionnels, instruisez-vous avec des livres, blogs, tweets... ;
- devant une situation en difficulté, procédez par étapes dans une logique agile, vous pouvez également vous aider d'outils ;
- parfois, la solution pertinente est de recommencer à zéro ;
- … mais mieux vaut éviter d’en arriver là.

Si vous souhaitez avoir des fiches méthodologiques par secteur d’activité (hébergement, infogérance, intégration, design, développeur framework, développeur CMS, etc., n’hésitez pas à l’indiquer dans les commentaires ou par mail / twitter).