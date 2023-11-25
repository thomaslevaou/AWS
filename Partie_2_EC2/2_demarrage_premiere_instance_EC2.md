# Démarrez votre première instance EC2

## Choix du Type d'instance et du type de serveur

Lorsqu'on veut créer une instance, AWS en propose plusieurs types. Pour lancer notre première instance EC2, on doit commencer par choisir son bon type.
La liste des types d'instances EC2 disponibles est accessible dans `Instances > Types d'instances`.

Des types d'instances, il y en a plein. C'est pourquoi on les regroupe dans 5 grosses _catégories de types d'instance_ :

- **usage général**: équilibrés entre le processeur, la mémoire vive et le disque dur, on les utilise pour le Web;
- **calcul optimisé**: les "monstres de calcul", pour des grosses stats ou grosses perfs quoi;
- **mémoire optimisée**: pour les cas où on a besoin de plusieurs To de mémoire vive (oui ça existe);
- **calcul accéléré**: autres "monstres de calcul", cette fois dans le GPU pour faire du Machine Learning;
- **stockage optimisé**: pour avoir un disque dur sur lequel il est particulièrement rapide d'accéder aux données (oui des fois, ce besoin existe aussi).

Pour faire du web, on va utiliser un type d'instance t2, dans la catégorie d'openclassrooms "usage général" quoi.

Et pour chaque type d'instance, on a un _type de serveur_ associé. Ici en gros on va utilisé le type de serveur micro.

D'où le fait qu'ici dans le cadre de ce cours, nous allons utiliser l'instance **t2.micro**, qui est gratuite pendant un an, pour faire du web "de base" (ce qu'AWS appelle "éligible à l'offre gratuite"). Les autres types de serveur existent pour répondre à des besoins spécifiques qui ne nous concernent pas ici.

## Choix du type de tarification

En plus des types de serveurs, il existe aussi plusieurs types de _tarification_ de serveurs. Les types de tarification sont listés et détaillés [sur ce lien](https://aws.amazon.com/fr/ec2/pricing/). Nous on utilisera la tarification à la demande. Mais d'autres types de tarification existent, à choisir en fonction de l'engagement et du besoin qu'on aura du serveur en production, pour des utilisations plus professionnelles. Ils sont quand même à connaître, donc les voici :

- **tarification à la demande**: celle prise dans le cadre de ce cours, où je suis tarifé en fonction du serveur que je prends et de sa durée de location. Comme je prends au maximum des serveurs "éligibles à l'offre gratuite", ça ne devrait pas me coûter très cher dans le but pédagogique du cours ici;
- **instances spots**: je fais tourner des machines consommant les capacités non utilisées d'AWS. Ce qui peut faire baisser les prix jusqu'à 90% d'autres tarifs, mais AWS peut ici les réquisitionner de manière unilatérale à tout instant;
- **instance réservées**: je m'engage pendant une durée déterminée à utiliser les machines (genre un an), et j'ai en échange des réducs pouvant aller jusqu'à 72% (par rapport à la tarification à la demande je suppose);
- **savings plans**: je m'engage pendant une durée déterminée (genre un an) à souscrire à une offre qui coûte X centimes de l'heure, ce qui me permet d'avoir une réduction d'environ 30% sur ce prix (genre 10 centimes de l'heure au lieu de 15 centimes de l'heure, juste en échange de dire "je me suis engagé à utiliser cette offre pendant un an). Je pense que c'est histoire d'avoir une réduction en échange d'une forme d'engagement quand même (peut-être comme ça qu'Amazon encourage à utiliser un peu plus leurs services en mode "dans un an ce sera plus cher" ?);
- **hôtes dédiés** : je réserve la machine physique entière, si je suis vraiment contraint de ne pas pouvoir la partager (genre politique de la boîte, ou licence logicielle demandant obligatoirement un serveur physique).

## Paramétrages et lancement de l'instance

Le lancement d'une instance s'effectue sur la page `Instances > Instances`, en cliquant sur le bouton "Lancer des instances".

Lors du lancement d'une instance, on doit choisir une **AMI** (Amazon Machine Image), qui est globalement une grosse configuration logicielle qu'on veut de notre serveur (OS, applications, etc). C'est obligatoire (on ne peut pas avoir une instance sans choisir une AMI), bien qu'on puisse choisir une AMI quasiment vierge (genre juste un OS).

Ici, on suppose qu'on a besoin de monter un serveur web exécutant un site en PHP. Pour gagner du temps, on va installer une AMI préconfigurée.

AWS propose également une _marketplace_ vendant (parfois gratuitement) des AMI gratuites, notamment l'AMI _LAMP packaged by Bitnami (on la trouve en utilisant le MDR de la page de choix d'AMI sur AWS, puis en cliquant sur "AMI d'AWS Marketplace").
Cette AMI étant gratuite et permettant de fournir les outils pour avoir un serveur web pour notre instance EC2, on va s'en servir ici.

Ensuite, l'interface que j'ai sur AWS est différente du tuto. Je pense qu'on peut retrouver chaque truc affiché sur OpenClassrooms sur un endroit de la page AWS, à condition de chercher.

Comme on peur voir dans la section "Configurer le stockage", on peut voir que je peux prendre jusqu'à 10 Go de disque dur SSD (par défaut, mais on peut prendre un "dique magnétique", càd un HDD, si on en a besoin un jour, ou augmenter l'espace disque). La puissance de calcul reste malléable, mais pas l'espace disque (ce sont deux choses distinctes pour EC2). On appelle ce disque dur un **volume EBS** (c'est un sous-service d'EC2).

On peut ajouter des tags pour mieux retrouver notre instance si on en a beaucoup à l'avenir, mais osef pour le moment (c'est en haut de la page après le nom, en cliquant sur "ajouter des balises supplémentaires" sur mon interface AWS).

Je peux configurer mon pare-feu dans la partie "Paramètres réseau". Par défaut, il est possible d'accéder au réseau SSH depuis n'importe quel réseau. Pour optimiser la sécurité, je vais restreindre l'accès SSH à seulement mon IP (modifiable par la suite en retournant dans les paramètres de mon instance EC2). Comme indiqué, changer un des paramètres crée automatiquement un groupe de sécurité (applicable à plusieurs instances en même temps si j'en ai besoin un jour), avec comme nom automatique "LAMP packaged by Bitnami-8.1.25-4-r09 on Debian 11-AutogenByAWSMP--1".

On peut aussi créer une paire de clés SSH. Attention, la clé privée est envoyée dans un fichier que je dois absolument garder sur mon PC.

Une fois que c'est fait, je peux alors lancer la création de l'instance.

Une fois qu'elle est lancée, je peux la voir dans mon navigateur (parce que j'ai choisi une AMI Lamp configurée), à l'adresse <http://ec2-35-181-151-129.eu-west-3.compute.amazonaws.com/>.
