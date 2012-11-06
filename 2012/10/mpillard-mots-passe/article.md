# Le stockage des mots de passe

Quel est le point commun entre Yahoo!, Gawker, Sony et LinkedIn ? Ces entreprises ont toutes ont été victimes de vols de mots de passe à grande échelle ces deux dernières années.

Les conséquences sont désastreuses, que ça soit pour leur réputation, leurs revenus, et bien sûr pour nous-mêmes, leurs utilisateurs. Nombreux sont ceux qui réutilisent leurs mots de passe d'un site à un autre (un problème [déjà soulevé par Goulven Champenois dans un article précédent](http://letrainde13h37.fr/19/bonne-utilisation-mots-de-passe/)).

Nous allons donc voir comment un développeur peut éviter de se retrouver dans la même posture.

## Principe

Le principe fondamental du stockage de mots de passe est le suivant : une fois rentré par l'utilisateur, vous ne devez jamais être capable de le récupérer. Vous avez uniquement besoin de le comparer à la chaîne de caractères que l'utilisateur saisit pour se logguer, rien de plus. Au-delà de ça, votre but doit être de compliquer la vie de toute personne tentant de le retrouver.

Pourquoi ne jamais être capable de le récupérer ? Parce que vous n'êtes pas à l'abri d'une fuite. Et il n'y a pas que les vilains pirates qui peuvent en être à l'origine : pensez aux personnes ayant les droits administrateur sur vos machines, votre support technique, vos développeurs, etc. S'il existe un moyen de lire le mot de passe en clair, alors il existe une faille de sécurité.

Il peut être tentant de stocker le mot de passe en clair pour pouvoir le renvoyer à un utilisateur qui l'aurait perdu, mais c'est une mauvaise solution d'un point de vue sécurité : non seulement vous êtes obligé de conserver une version en clair de votre côté, mais en plus, en le renvoyant, vous augmentez les chances qu'il soit intercepté par quelqu'un d'autre. Préférez donc une solution permettant de le changer plutôt que celle qui consiste à le renvoyer automatiquement par mail.

Le seul moment où le mot de passe doit être accessible en clair dans votre code est donc celui de l'identification, dans les données POST. Idéalement, ce processus devrait être effectué en HTTPS afin que la version en clair ne circule jamais sur le réseau.

## Chiffrement symétrique

S'il paraît donc évident qu'il faille absolument éviter de stocker les mots de passe en clair, il est important de noter que le chiffrement symétrique pose le même genre de problèmes. On parle de chiffrement ou de cryptographie symétrique lorsque l'algorithme fonctionne dans les deux sens : il permet de chiffrer mais aussi de déchiffrer le mot de passe. Dans le cas qui nous occupe, cela revient à dire que vous disposez d'une clé secrète pour chiffrer le mot de passe, mais que vous pouvez utiliser cette même clé pour le déchiffrer et retrouver ainsi la version en clair pour la comparer à la chaîne de caractères que rentre l'utilisateur lorsqu'il tente de s'identifier. Le problème avec cette technique, c'est que vous vous retrouvez dans la même situation que s'il était en clair, puisqu'il finit toujours par être déchiffrable à un moment donné.  
Quelle que soit votre solution pour cacher cette clé, vous êtes potentiellement vulnérable. Certaines des entreprises mentionnées précédemment ont cru que cette solution les mettrait à l'abri. L'histoire leur a donné tort : au même titre qu'une base de données, une clé de chiffrement peut être volée. 

Pour simplifier, rappelez-vous cette règle d'or du stockage de mots de passe : toujours partir du principe que l'attaquant a déjà réussi à accéder à l'ensemble de votre architecture et à télécharger l'ensemble de vos données. Même dans ce cas de figure, vos mots de passe doivent rester inviolables.

## Chiffrement à sens unique : les fonctions de _hash_

Il faut donc utiliser un système qui ne permette pas de garder le mot de passe d'origine. Pour cela, on dispose d'algorithmes de chiffrement à sens unique. Ces fonctions dites « de hachage » sont généralement utilisées pour vérifier l'intégrité de données, calculer une empreinte unique aussi rapidement que possible, etc. Les algorithmes les plus connus dans ce domaine sont MD5 et SHA1.

Hélas, il existe deux problèmes majeurs avec ces fonctions. Le premier gros défaut vient de l'existence des [Rainbow Tables](http://fr.wikipedia.org/wiki/Table_arc-en-ciel). Ces tables, générées à l'avance, permettent à partir d'un hash de retrouver très rapidement la valeur en clair correspondante, pour un coût en puissance de calcul et un temps très faibles. Elles demandent en contrepartie une taille de mémoire conséquente... mais parfaitement accessible de nos jours (même au commun des mortels), du moins pour les mots de passe de huit caractères et moins.

Le principe du « salage » (_salt_ en anglais) a été inventé pour combattre ce problème. L'idée consiste à ajouter un préfixe aléatoire pour chaque mot de passe avant de chiffrer le tout. Stocké en clair avec le _hash_, il sera nécessaire lors de la vérification du mot de passe. On suppose que l'attaquant peut le connaître, mais ce n'est pas un problème : on veut seulement l'empêcher de prégénérer et de réutiliser une table de correspondance.

Malheureusement, cela ne suffit plus. En effet, le deuxième défaut est plus grave : les fonctions de _hash_ sont conçues et optimisées pour pouvoir fournir une réponse très rapidement. Or, pour le stockage de mots de passe, c'est exactement l'inverse qu'il nous faut. Si les processeurs modernes permettent de calculer plusieurs millions de _hash_ classiques par seconde, les _GPU_ dont sont équipés les cartes graphiques 3D peuvent carrément calculer plusieurs milliards de _hash_ par seconde ! Tester toutes les combinaisons possibles, technique connue sous le nom de « _brute force_ », est maintenant à la portée de tous.

Note : il peut être tentant d'imposer des restrictions aux utilisateurs, par exemple les obliger à mettre au minimum un chiffre ou une majuscule dans leurs choix de mots de passe. Mais en le faisant, vous donnez une arme précieuse à un attaquant, qui pourra éliminer un certain nombre de combinaisons lors de sa tentative de _brute force_. De même, il est important de ne pas limiter le nombre de caractères (ou alors à un nombre très important, pour limiter la taille du POST) : la taille est la meilleure arme dont dispose un utilisateur pour rendre son mot de passe difficile à craquer.

## Résister au _brute force_

La bonne nouvelle, c'est qu'il existe des fonctions à sens unique conçues et optimisées... pour être lentes. La plupart fonctionnent avec une boucle dont le nombre d'itérations est réglable. Le temps pris par chaque itération est constant et dépend juste de la puissance de la machine. Donc, en choississant un nombre d'itérations on choisit le délai qui sera appliqué à chaque vérification de mot de passe. En choississant un délai de l'ordre de la seconde, vous freinez considérablement un éventuel attaquant qui devra tester énormément de possibilités, mais vous ne gênez pas trop vos utilisateurs. Le nombre d'itérations sera stocké à côté du _salt_ et du mot de passe hashé. Au fur et à mesure que la puissance des machines augmente, vous pouvez augmenter ce nombre. Vos utilisateurs existants n'en bénéficieront pas immédiatement, mais vous pourrez leur générer un nouveau _hash_ lors de leur identification, puisque à ce moment-là, vous disposez _temporairement_ du mot de passe en clair.

Notez que le _salt_ reste présent. Par sécurité, la plupart des implémentations de ces algorithmes fournissent un moyen de générer un _salt_  automatiquement de manière vraiment aléatoire, et il est recommandé de passer par cette méthode plutôt que de réinventer la roue. En fait, cette recommandation s'applique à toute la chaîne de la gestion des mots de passe : en réinventant ce qui existe déjà, vous vous exposez à des failles potentielles, alors qu'en réutilisant un système éprouvé par d'autres et relu par des experts dans ce domaine, vous limitez significativement les risques de laisser subsister une faille.

## Les solutions

Il existe trois algorithmes qui répondent aux critères que nous venons de voir :

- [PBKDF2](http://en.wikipedia.org/wiki/PBKDF2PBKDF2) est l'un des plus utilisés. Il a fait l'objet d'une RFC ([RFC 2898](http://tools.ietf.org/html/rfc2898)) et est recommandé aux États-Unis par le _National Institute of Standards and Technology_ (NIST) depuis 2010. Relativement simple à implémenter, il réutilise une fonction cryptographique au choix de l'implémenteur et l'appelle en boucle. 
- [bcrypt](http://en.wikipedia.org/wiki/Bcrypt) a été inventé spécifiquement pour le stockage de mots de passe. Plus complexe à implémenter, il est aussi un peu plus difficile à craquer, notamment par les _GPU_. Également disponible dans de nombreux langages, c'est l'alternative de choix face à PBKDF2.
- [scrypt](http://en.wikipedia.org/wiki/Scrypt) est une troisième alternative encore plus vicieuse. Conçue pour consommer beaucoup plus de mémoire que les autres et ainsi gêner davantage un attaquant, elle ne dispose pas encore de beaucoup d'implémentations. Cela dit, la situation pourrait vite évoluer car il est prévu d'en faire [un standard IETF](https://datatracker.ietf.org/doc/draft-josefsson-scrypt-kdf/).

### Petit tour d'horizon des implémentations

Attention : si les implémentations présentes dans les frameworks ont normalement toutes fait l'objet de vérifications et de relectures par des experts en sécurité, ce n'est pas forcément le cas de celles qui traînent sur le net. Comme mentionné précédemment, mieux vaut réutiliser une  implémentation connue, testée et éprouvée par la communauté.

- **JavaScript** : Pour les utilisateur de NodeJS, il existe [une implémentation de bcrypt](https://github.com/ncb000gt/node.bcrypt.js/).
- **PHP** : la fonction crypt() permet depuis la version 5.3 d'utiliser bcrypt, mais demande de générer soi-même son _salt_ et la fonction n'est pas très pratique à utiliser. PHP 5.5 devrait disposer d'une [_API_ simplifiée pour résoudre ce problème](https://wiki.php.net/rfc/password_hash).
- **Python** : py-bcrypt et pbkdf2 sont disponibles sur pypi. Le framework Python le plus répandu, Django, [supporte les deux depuis la version 1.4, et utilise PBKDF2 par défaut.](https://docs.djangoproject.com/en/1.4/topics/auth/#how-django-stores-passwords).
- **Ruby** : bcrypt-ruby et pbkdf2 sont disponibles sur rubygems.
- **Java** : Le framework Spring 3.1.x implémente le support de bcrypt.
- **C#** : Une implémentation PBKDF2 est [présente de base dans .NET](http://msdn.microsoft.com/en-us/library/system.security.cryptography.rfc2898derivebytes.aspx).

