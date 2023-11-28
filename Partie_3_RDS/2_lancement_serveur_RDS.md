# Lancez votre serveur RDS

Sur la [page d'accueil du service RDS](https://eu-west-3.console.aws.amazon.com/rds/home?region=eu-west-3#), nous utiliserons seulement dans ce cours les menus "bases de données" (qui liste nos serveurs RDS), et "Instantanés" (qui gère les sauvegardes).

On peut lancer une instance RDS en allant dans "Bases de données > Créer une base de données". Après avoir sélectionné notre moteur (pour nous MySQL ici), on nous propose de choisir un modèle d'instance "de production" (qui aura des performances assez solides par défaut) ou un modèle "de dev/test" (avec un peu moins de perfs), mais on va ici juste utiliser "l'offre gratuite", qui propose juste quelques fonctionnalités (et une conf de serveur précise), mais pratique quand c'est juste pour mettre un peu la main à la pâte.

On laisse le VPC par défaut (qui pourra être utile plus tard pour connecter une instance EC2 à notre bdd). On rappelle qu'un VPC, pour Virtual Private Cloud, est un sous-réseau qui assigne des adresses IP privées à des serveurs, pour qu'ils puissent communiquer entre eux sans que les IP soient publiquement accessibles. Le "sous-réseau public" du VPC est publiquement accessible via le VPC, tandis que le sous-réseau privé ne l'est que par le sous-réseau public (voir schéma).

Sur une instance RDS, on peut aussi choisir un groupe de sécurité, et on va laisser ici celui par défaut. On évite de choisir l'accès public pour des raisons de sécurité (en entreprise, un serveur RDS doit n'être accessible que dans le VPC), mais comme ici on ne s'en sert que pour du test, on va l'autoriser pour simplifier des démarches après. On laisse ensuite tous les autres paramètres par défaut, puis on clique ensuite sur "Créer une base de données". On voit alors notre instance dans la liste de la page "Base de données".

Dès que l'instance est en statut "disponible", on peut cliquer dessus, ce qui permet d'afficher (entre autres) le "point de terminaison", c'est-à-dire l'adresse qui va nous permettre ensuite d'accéder au serveur.

Attention à ne pas confondre par la suite une instance RDS (qui reste un serveur malgré tout) et une base de données (qui est hébergée sur ce serveur).