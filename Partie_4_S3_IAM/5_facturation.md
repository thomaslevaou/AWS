# Maîtrisez les outils de facturation sur AWS

## Présentation des pages de facturation

Il existe un service de facturation sur AWS, dont la maîtrise est surtout utile car une tarification non maîtrisée d'AWS par rapport à une tarification maîtrisée, peut faire varier les prix de facturation du simple au double, ce qui peut avoir des répercussions sur les prix qu'on fait payer aux clients par exemple (pour lesquels il est évidemment hyper important de réduire le plus possible les coûts tout en étant bon pour les intérêts de l'entreprise).

Pour maîtriser ses coûts de facturation, sur la console AWS on peut cliquer sur son nom d'utilisateur en haut à droite, puis sur "Gestion de la facturation et des coûts". L'interface a changé par rapport au tuto OpenClassrooms, mais comme dans le tuto, je retrouve les récap des dépenses mensuelles du compte sur la page d'accueil de cette partie.

On peut aller regarder plus en détail les modes de consommation sur la page "Explorateur de coûts", dans le menu de gauche. On peut voir les coûts dépensés pour chaque service utilisé. Les instances EC2 sont bien souvent les dépenses coûtant le plus cher. On peut filtrer les coûts par types d'instance avec un filtre à droite.
Dans le menu de droite, on peut aussi changer la granularité de "Mensuel" en "Quotidien", pour afficher les dépenses par jour au lieu des dépenses par mois.

Sur la page de gestion de facturation et des coûts, il est important de savoir que :

- on peut accéder aux factures sur la page "**Factures**", avec pas mal de divers détails;
- les paiements dus et transactions effectuées sur la page "**Paiements**";
- l'**explorateur de coûts** déjà sus-cité.

De toute façon je sais très bien qu'en entreprise, ça commencera surtout par de l'improvisation sur les interfaces.

## Techniques de réduction des coûts

1. [Cette page](https://aws.amazon.com/fr/savingsplans/compute-pricing/) permet de savoir ce qu'on pourrait économiser si notre serveur était en _Savings Plans_, au lieu de la tarification à la demande choisie dans le chapitre 2 de la partie 2. Un saving plan ne demandant que le fait de s'engager à laisser un serveur allumé pendant un an, cette page permet de clairement voir ce qu'une entreprise peut avoir à gagner avec cette option de tarification.

2. Sur la page "Instances réservées" du service RDS, je peux cliquer sur le bouton "acheter des instances de base de données réservées", ce qui me donne accès à un formulaire simulant les économies que je pourrais faire en m'engager à réserver une instance pendant une durée déterminée (quand je ne suis pas sur l'offre gratuite comme ça a été le cas actuellement pour ce tuto). Pour rappel, l'instance réservée est aussi une option de tarification vue dans le chapitre 2 de la partie 2. Que ce soit pour RDS ou EC2, l'instance réservée engage l'utilisateur à louer une machine physique pendant la durée (il faut donc être sûr des capacités de celle-ci).

3. Quand je vais dans la partie "Gestion" d'une page de détails d'un bucket AWS, je peux ajouter une règle de cycle de vie pour déplacer les objets entre classes de stockage, puis sélectionner une transition entre les classes de stockage selon une "Hiérarchie intelligente". Ce qui me permet de déplacer les fichiers non ou peu utilisés automatiquement dans des classes de stockage S3 qui coûtent beaucoup moins cher que le coût de la classe de stockage standard.

Y a évidemment pleeeeein d'autres techniques de réduction de coûts, à creuser dès qu'on a besoin.
