# Conseils pour mieux gérer des projets complexes

## Introduction

Des milliers de pages, un changement de CMS, d’innombrables templates à rationaliser, des besoins très précis, un changement de CRM avec lequel le site doit discuter, d’innombrables modules à refondre ou à adapter, une restructuration importante des contenus existants, des objectifs ambitieux en SEO/expérience utilisateur/etc., des besoins avancés sur Google Analytics, une refonte qui s’étale sur une très longue période mais dont le calendrier est extrêmement serré, etc., et… tout cela en même temps.

Ce sont là les caractéristiques des projets complexes: de fortes exigences, des demandes difficiles à satisfaire, une vision d’ensemble difficile à avoir et une quantité innombrable de pièges plus ou moins vicieux qui peuvent vite rendre fou. Je vous propose un retour d’expérience et quelques conseils pour survivre dans ce monde impitoyable :)

## Un projet complexe

Le propre de ces projets est d’avoir des implications dans tous les sens. Une simple décision peut vite tourner au vinaigre si elle ne passe pas par les bonnes personnes. Un exemple simple : le département marketing du client décide de lancer un concours qui offrira un petit cadeau sur le site. Le responsable des contenus donne son aval et oublie d’avertir le responsable du CRM.

Le formulaire est développé par l’équipe du site Web, tout va bien et, juste après la mise en ligne, le responsable du CRM reçoit une demande qui lui stipule de faire une moulinette sur ledit CRM pour sortir des statistiques. Tout étonné, il se rend compte que le formulaire ne prend pas la moitié des informations nécessaires pour que les informations rentrent correctement dans le CRM ! En plus de cela, il a plein de demandes urgentes, et il se retrouve à improviser en catastrophe quelque chose pour faire l’import de données. Il contacte l’équipe Web, elle aussi surchargée de demandes, elle improvise, le département marketing n’est pas content car il voit son petit concours sympathique transformé en formulaire bien plus compliqué, etc., vous voyez le tableau. Si vous multipliez cela par le nombre d’intervenants et leur éclatement géographique, des décisions très simples peuvent vite prendre des proportions dantesques.

Même si l’exemple est un poil caricatural – ce type de couac ne devrait JAMAIS arriver (qui a toussé au fond de la salle ?) – , il représente bien les dégats collatéraux qui surviennent souvent sur ce genre de projets. Il arrive même fréquemment que les situations soient bien plus dramatiques : un changement de CRM en douce sans prévenir l’équipe Web (qui du coup passe pour le méchant car elle soulève des problèmes sans en être à l’origine), des décisions politiques irrationnelles, etc.

## De bons réflexes, des enseignements

Plus que la technique pure, c’est principalement votre manière de fonctionner sur ces projets qui garantira leur succès ou votre trépas. Voyons donc quelques aspects importants.

### Tuer ou limiter l’inconnu

Il ne s’agit pas d’occire un inconnu, rassurez-vous. Les deux gros soucis dans ce genre de projets sont de mettre d’accord tout le monde et d’arriver à respecter le planning. Pour cela, il existe plein d’outils : des maquettes, des prototypes, du *wireframing*, du *card sorting*, etc., et ces outils permettent de bien définir et cadrer un projet en amont, ce qui est capital pour la réalisation.
Néanmoins, pour pouvoir créer un planning (et *a fortiori* en tenir les délais), il faut pouvoir quantifier le temps que va mettre par exemple le développement d’un module. Question bête : comment quantifier ce que l’on n’a jamais fait et/ou ce que l’on ne maîtrise pas ? Vous n’avez jamais fait de développement avec tel CRM qu’on vous impose, vous n’avez aucune idée de comment vous en sortir.

Là, **il n’y a malheureusement pas de miracle, seulement des solutions**. Si votre équipe est capable de résoudre le problème, il faut lui laisser au minimum le temps de faire un *proof of concept*, qui comme son nom l’indique prouve que la demande est possible à réaliser. Ensuite, il sera possible d’extrapoler et d’en déduire le temps nécessaire pour faire le tout. Si votre équipe seule ne peut pas régler le problème, il faudra aller chercher la compétence, soit par une ressource extérieure, soit en la faisant acquérir par votre équipe.

D'expérience, les zones d’ombres ont la sale manie de grandir proportionnellement au manque de temps, donc il faut foncer sur ces bombes à retardement pour vite les désamorcer.

Si l’on parle souvent d’impliquer le client dans la conception du site, l’inverse est tout aussi important : le client doit impliquer le prestataire dans son mode de fonctionnement. Plus le prestataire Web sera au fait des besoins, des problèmes, bref de la vie de son client à propos de ce projet, plus il sera à même d’y répondre de la manière la plus juste.

Tuer ou limiter l’inconnu est important pour la réalisation, mais également pour la transmission de la connaissance : ce qui est évident pour vous ne l’est pas forcément pour vos collègues, donc assurez-vous de permettre à ces derniers de pouvoir reprendre votre travail.

### Anticiper la qualité

Si vous gérez ou si vous vous intéressez à la qualité Web, vous devez sûrement avoir une liste de points à contrôler à la fin du projet, et c’est une très bonne chose. Toutefois, pour survivre sur des projets de grande ampleur, **je vous conseille de ne plus suivre cette checklist à la fin du projet mais au tout début**.

Prenons un exemple : plein d’entrain sur un projet ambitieux qui démarre, l’intégrateur commence les *templates* du site. Le premier bon réflexe : prendre la checklist qualité, et faire tout de suite les points qui peuvent être faits, ou ne serait-ce que les « pré-mâcher » pour la suite.

Le premier avantage est tout simplement… de ne plus à avoir à y penser quand ce sera le stress absolu de la mise en ligne. Je peux vous certifier que quand il y a dix demandes à la minute qui doivent être traitées pour avant-hier dernier délai, ne pas avoir à se soucier en prime de certains points de qualité est un avantage indéniable.

Un autre avantage est de limiter la complexité de résolution d’un problème. Reprenons l’exemple de l’intégrateur : conscienceusement, au moment de faire ses *templates*, il s’est rappelé que le point numéro 13 de sa checklist est d’avoir une version imprimable correcte des contenus. Le mauvais intégrateur se serait dit « bon, on n’a pas de contenus, je m’en fous, je verrai ça plus tard ». Le bon intégrateur n’a pas attendu et a déjà pré-mâché cette étape avec par exemple des contenus factices : comme la structure est déjà adaptée pour une version *print*, les problèmes éventuels qui se présenteront auront déjà été limités et viendront très probablement du contenu, et non de la structure de base.

Un avantage supplémentaire de fonctionner ainsi est de voir la checklist de fin de projet comme une simple vérification qui ne prend pas beaucoup de temps, une formalité en somme, plutôt qu’une punition horriblement chronophage. Pour reprendre le discours de l’accessibilité agile : **la checklist de fin de projet doit être un constat de succès et non d’échec**.

Le dernier avantage de penser à la qualité en amont est de limiter la dégradation au long de la vie du projet : les choix du début ne limitent pas l’avenir du site. En intégration : plus le *template* de base a été testé à l’épreuve des balles et conçu avec la plus haute qualité au début du projet (performances, etc.), plus le site partira de haut (et se donnera les moyens d’y rester). On peut utiliser une analogie : si vous mettez des pneus corrects sur une voiture haut de gamme, même légèrement limitée, elle reste une voiture haut de gamme ; par contre, mettre des pneus hautes performances sur une voiture pourrie n’en fera jamais une voiture haut de gamme.

### Dette technique/qualitative, « l’empilage de couches »

Sur ce genre de projets, le concept de **dette technique/qualitative** peut sommairement se résumer ainsi :


- Tout truc fait à l’arrache va, dans le meilleur des cas, vous faire perdre du temps plus tard, au pire vous exploser à la figure en plein stress.
- La vie et le bruit du projet peuvent très vite faire baisser la qualité globale du site Web : ajouts, décisions, changements, retours en arrière, etc.


Ces dangers sont particulièrement présents lors des refontes de sites/systèmes qui ont subi de nombreux ajouts ou modifications. Prenons à nouveau un exemple : le client a changé de CRM plusieurs fois, le site Web a suivi cette évolution ainsi que la sienne. Il en résulte un empilage de couches successives. Entre-temps, les développeurs ont changé, la documentation n’a pas forcément suivi… et le dernier développeur se retrouve avec un énième changement de CRM ou une demande de changement qui est incompatible avec les postulats de base du système (que tout le monde a oubliés entre temps).

Même si devoir tout casser et refaire au propre peut faire peur quand les délais sont tendus, il faut savoir parfois profiter de ce genre de refonte pour – excusez l’expression – « nettoyer le moisi du frigo ». Ces grandes refontes très ambitieuses doivent permettre de faire repartir le site Web sur des bases saines … et non de le diriger vers une impasse à cause d’une partie devenue impossible à manœuvrer.

Un autre aspect lié : il arrive fréquemment qu’un innocent petit bout de script développé pour un besoin précis se retrouve réutilisé à l’insu du plein gré de son auteur sur d’autres parties. Méfiez-vous énormément des scripts faits à la va-vite en période de stress et ne vous dites JAMAIS, même si c’est trèèès tentant, « Je le fais à l’arrache, ça ne sera jamais utilisé ailleurs », car vous pouvez être certain que cela sera le cas. Vous vous retrouvez plus tard avec un script déployé massivement qui va montrer ses limites. Et bien entendu, gérer un existant déployé est compliqué et chronophage.

### Gérer le volume

Vu l’ampleur du projet, vous vous retrouvez avec des quantités de données très importantes à gérer. Évidemment, il n’est pas souhaitable de gérer ces données à la main, donc **(semi-)automatisez le plus possible**, particulièrement sur les tâches ingrates ou peu intéressantes.

Même si votre chef de projet ou votre client vous casse les pieds avec une autre demande bien plus importante à ses yeux, il faut (leur faire) accepter de « perdre » du temps pour en gagner ensuite. Je mets « perdre » entre guillemets car **ce n’est PAS du temps perdu mais du temps investi**, le gain viendra après.

Pour utiliser une analogie économique : privilégiez les investissements à moyen et long termes. Chercher le bénéfice immédiat n’est pas nécessairement mauvais, mais fonctionner uniquement ainsi vous mènera droit dans le mur sur ce genre de projets.

D'ailleurs, même si l’automatisation d’un aspect est faite de manière rudimentaire, n’en rougissez pas une seconde ! Pour prendre un exemple pratique tout simple : lors d’une refonte, un des premiers points de qualité est de rediriger les points d’entrées importants vers les nouvelles adresses. Cela bénéficie au SEO et à l’utilisateur. Sur des sites ayant beaucoup de pages, il n’est pas envisageable de faire cela de manière manuelle. Souvent, le/la responsable SEO me fournit un simple fichier Excel avec les anciennes et nouvelles URLs, je le transforme en CSV, et via un petit traitement, cela me génère mes redirections 301 (redirections permanentes) pour mon htaccess.

### Le syndrome du vieux couple

Un aspect potentiellement problématique est le « briefing post-it » : trois coups de crayons affublés d’un « OK, tu vois ce que je veux dire ? ». Vous travaillez depuis longtemps avec la personne, pas besoin de perdre une heure à tergiverser !

J'appelle cela le « syndrome du vieux couple » : l’un commence la phrase et l’autre la finit. Non, non, non, cent fois non, et particulièrement sur ce genre de projets !

Sans tomber dans la « psychorigidité » ou l’excès de méthodologie, même une jolie maquette peut être interprétée différemment selon la personne. En pleine urgence, le briefing post-it peut se retrouver chez une personne extérieure au vieux couple  : elle va interpréter différemment la demande… en supposant qu’elle puisse l’interpréter. Personnellement, je prends toujours un exemple pratique en me mettant à la place de l’internaute : «OK, je suis la société bidule qui doit s’inscrire ou utiliser telle partie du site, donc je dois faire quoi, comment ça se passe ?». Cela force à sortir la tête du guidon et à poser un regard critique sur ce qui nous semble évident. J'appelle cela faire le « très-bêta » testeur : ça aide l’équipe à comprendre parfaitement les rouages de ce qu’on lui demande, et toute chose bien comprise sera mieux retranscrite.

Le syndrome du vieux couple est dangereux pour la communication interne, mais il est également problématique pour la relation avec le client. Vous pouvez être tenté de court-circuiter la décision du client, vous avez peut-être déjà entendu : « C'est bien, mais on ne va pas leur proposer ça, ils vont refuser, on va argumenter pendant des jours pour arriver à rien comme d’habitude ». Encore une fois, cent fois non ! Votre rôle et votre intégrité en tant que professionnel ne doivent pas être outrepassés par un choix de facilité. Si votre client décide d’ignorer vos recommandations, c’est son problème. Mais vous l’aurez averti et vous n’aurez rien à vous reprocher.

Si vous faites le choix de la facilité, d’abord vous basculerez du côté obscur de la force, et surtout : si votre client soulève plus tard ce que vous avez remarqué mais choisi d’esquiver ou d’ignorer, vous risquez de perdre en crédibilité.

### Dire merci aux petits projets

Les grands projets se réussissent aussi… grâce aux projets plus simples, et ce pour une raison toute bête : les expérimentations ou les nouveautés sont beaucoup plus faciles à faire sur des projets moins complexes.

Passer à l’échelle supérieure est déjà une épreuve en soi, elle sera facilitée si les choses qu’on va vous demander à grande échelle ont déjà été faites sur des petits projets. Ne pas avoir tout à apprendre ou à inventer sur des projets difficiles est une chance, donc saisissez-la. J'ai rarement vu des investissements en connaissances ne pas rapporter à moyen ou long terme.

Donc, utilisez les petits projets pour faire des essais, des *proof of concept*, voir ce que telle technique implique, ses avantages, ses inconvénients, etc. Vous devez avoir des armes pour savoir réagir à toutes les situations, même celles qui vous paraissent improbables.

### L'attitude

L'entrain suscité par ces projets complexes (qui « font bien sur le CV ») à leur démarrage se calme souvent au long cours : une certaine frustration ou même un écœurement peut apparaître ; vous avez peut-être déjà entendu dans votre équipe :


- On devait refondre cette partie et faire un truc génial, et on l’a à peine améliorée !
- J'en ai marre, ça fait deux mois que je ne fais que ça !
- Etc.


Dites-vous bien une chose : c’est une course de fond sur laquelle vous êtes engagé. Même si vous pouvez avoir des sprints violents à certains moments, cela se gagne sur la durée. C'est pour cette raison qu’il faut accepter parfois de revoir ses ambitions à la baisse ou d’accepter des objectifs raisonnables : ce n’est pas uniquement pour vous frustrer ou vous empêcher de montrer l’étendue de votre talent, mais bien pour finir la course… si possible en bon état. Ajoutez à cela :


- que même si vous avez envie d’aller plus loin que ce qui est demandé, vous ou un membre de votre équipe pouvez vite vous retrouver submergé(s) par cette envie de surqualité, ou plus simplement par un autre aspect du projet,
- que ce genre de projets peut avoir une certaine inertie qu’il faut prendre en compte au moment de faire le planning,
- et que ce travail de longue haleine a un fort potentiel d’usure sur le moral, et parfois même sur le physique quand les heures supplémentaires commencent à s’amonceler.


Certes le niveau de compétences est important: sur ce genre de projets, il vaut mieux avoir des gens qui connaissent bien leur métier ! Cela dit, je pense que l’attitude personnelle est au moins aussi importante: sur du long cours avec de bonnes périodes de stress, la capacité à penser plus loin que le bout de son clavier est primordiale. Dites-vous également que le temps que vous passez à vous plaindre, à freiner des quatre fers ou à expliquer pourquoi telle demande est débile… vous pouvez l’utiliser pour trouver une solution ou faire autre chose.

Entretenir une bonne ambiance au plus haut point de stress est capital. Ma technique secrète: j’amène régulièrement des croissants bien chauds le matin, c’est un petit geste anodin mais qui rappelle à mon équipe pourquoi on aime bien bosser ensemble, même et surtout quand tout le monde est sous tension.

## Conclusion

Comme vous avez pu le voir, ces projets recèlent des pièges et ces derniers peuvent être difficiles à voir car ils touchent souvent au mode de fonctionnement propre à votre équipe ou à vous-même. Une remise en question permanente est importante et le travail en équipe est indispensable.

Si vous souffrez un peu sur ce genre de projets, gardez en tête que *celui qui peut le plus peut le moins*: les bonnes pratiques pour survivre à des projets complexes vous serviront beaucoup sur des projets plus facilement abordables: au pire pour les achever correctement, au mieux pour améliorer la qualité de votre travail. Ce qui nourrira vos connaissances pour réussir d’autres projets, etc., et vous voilà partis pour un cercle vertueux !
