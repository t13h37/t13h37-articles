# Introduction

Pendant que vous batifoliez dans l'eau cet été, un [journaliste a perdu toutes ses données et l'accès à tous ses moyens de communication](http://www.zdnet.fr/actualites/apple-et-amazon-fautifs-dans-le-piratage-d-un-compte-icloud-39774976.htm), des [entreprises renommées se sont fait piquer des millions de mots de passe](http://www.lukew.com/ff/entry.asp?1590), et le [marché des cartes de crédit volées](http://www.lemondeinformatique.fr/actualites/lire-une-cotation-du-prix-des-cartes-bancaires-volees-disponible-sur-cloudeyez-49960.html) se porte bien, merci pour lui…

Il est pourtant simple d'éviter ce genre de problèmes ou au moins de limiter la casse !

# Éduquer votre entourage

Trop de gens choisissent des mots de passe mal sécurisés, [même parmi les geeks](http://blogs.wsj.com/digits/2010/12/13/the-top-50-gawker-media-passwords/). Sachant que rien n'est plus simple que de trouver le login de quelqu'un sur Internet, le mot de passe est votre seule véritable défense.

Choisissez-en donc un bon pour ne pas laisser n'importe qui se faire passer pour vous, vous ridiculiser publiquement, supprimer vos photos en ligne, voire réclamer de l'argent à vos proches ou effacer à distance vos téléphones et ordinateurs, comme c'est arrivé à ce pauvre journaliste…

- Apprenez aux gens autour de vous à **ne jamais utiliser le mot de passe de leur email pour un autre compte** (surtout s'ils utilisent leur adresse mail comme login) ;
- Montrez-leur [comment inventer un mot de passe sécurisé facile à retenir](http://xkcd.com/936/) ;
- Incitez-les à utiliser une *passphrase* plutôt qu'un  simple mot, c'est plus difficile à pirater, plus facile à retenir, et pas moins rapide à saisir s'ils tapent vite ;
- Conseillez-leur de clôre les comptes qu'ils n'utilisent plus et de mettre un mot de passe sûr pour les comptes importants (ceux où sont enregistrées leurs coordonnées bancaires et leur compte mail principal).

# Sécuriser les sites

Un test simple : si un utilisateur d'un des sites que vous gérez peut demander à recevoir son mot de passe **actuel** par email, vous avez un gros problème. En effet, quiconque accède au compte mail de votre utilisateur peut récupérer ses codes d'accès sans laisser aucune trace, et si votre site se fait pirater les attaquants peuvent s'identifier sur tous les autres sites où vos visiteurs ont utilisé le même mot de passe.

Lisez donc [La cryptographie et le Web : hachage, salage et autres recettes](http://www.pompage.net/traduction/la-cryptographie-et-le-web-hachage) et appliquez ce qui y est expliqué : 

- ne demander que le minimum d'informations ;
- ajouter une pincée de sel avant d'enregistrer les mots de passe ;
- utiliser un algorithme sécurisé (SHA-1 ou AES) plutôt que MD5 qui est largement dépassé  ;
- utiliser HTTPS pour les données sensibles.

Par ailleurs, si vous voulez que vos utilisateurs mettent un vrai mot de passe bien sécurisé… Ne les empêchez pas de le faire ! N'imposez pas de longueur maximum, et n'obligez pas à respecter un format particulier. Toute contrainte oblige ceux qui ont de bonnes pratiques à les mettre de côté et simplifie le travail pour quiconque essaie de deviner un mot de passe !

# Aller plus loin

Plusieurs solutions permettent de contourner les limites actuelles des mots de passe : logicielles comme [1Password](https://agilebits.com/onepassword) qui permet de créer et retenir des mots de passe ultra-sécurisés à votre place et [Firefox Sync](http://support.mozilla.org/fr/kb/firefox-sync-emporter-infos-perso) qui permet de synchroniser les mots de passe enregistrés par votre navigateur d'un poste à l'autre, ou bien matérielles comme les lecteurs d'empreintes digitales.

D'ailleurs, saviez-vous qu'il existe une solution pour ne pas avoir à demander à vos utilisateurs de choisir un login, un mot de passe, voire même de ressaisir des informations courantes ? Vous ne rêvez pas, c'est possible !

Avec [OpenID](http://fr.wikipedia.org/wiki/OpenID), l'identification de vos utilisateurs est effectuée par un fournisseur que votre site interroge à chaque fois que le visiteur veut se connecter. Le seul mot de passe nécessaire sera donc celui du fournisseur. Parmi les fournisseurs principaux se trouvent Google, Yahoo, Flickr, MySpace, Wordpress et même AOL (ça existe encore ça ?) : vos visiteurs ont sûrement déjà un compte chez l'un d'entre eux.

Pour contourner certains problèmes d'OpenID, la fondation Mozilla propose BrowserID (qui s'appelle maintenant [Persona](https://login.persona.org/)). Persona nécessite un script JS dans vos pages et du développement côté serveur mais, au lieu d'ouvrir le site certifiant dans une popup, l'identification s'effectue dans une fenêtre du navigateur. Le phishing devient impossible, le processus est plus rapide, le multi-compte est plus facile à gérer, et votre fournisseur d'authentification n'est plus informé de vos moindres faits et gestes…

Enfin, si votre site doit accéder à des données hébergées sur un autre site ou interagir avec celles-ci au nom de votre utilisateur, utilisez [OAuth](http://fr.wikipedia.org/wiki/OAuth). Ce système très pratique permet à 2 *APIs* de dialoguer entre elles, et vous l'utilisez sûrement déjà si vous écrivez vos tweets depuis une application plutôt que sur le site Twitter.com.

# Conclusion

La sécurité informatique est l'affaire de tous mais, en tant que professionnels de l'informatique, nous avons des responsabilités en plus :

* Éduquer sur les enjeux et les solutions existantes ;
* Sécuriser les sites et les applications que nous développons ;
* Nous tenir au courant de l'état de l'art.

Eh bien, vous êtes encore là ? Allez donc plutôt vérifier [qui a accès à votre compte Twitter](https://twitter.com/settings/applications) !