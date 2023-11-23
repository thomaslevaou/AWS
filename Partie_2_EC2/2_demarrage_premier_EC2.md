# Démarrez votre première instance EC2

Plusieurs types d'instances sont proposés par AWS. Pour lancer notre première instance EC2, on doit commencer par choisir son bon type.
La liste des types d'instances EC2 disponibles est accessible dans `Instances > Types d'instances`.

Ici dans le cadre de ce cours, nous allons utiliser l'instance **t2.micro**, qui est gratuite pendant un an, pour faire du web "de base" (ce qu'AWS appelle "éligible à l'offre gratuite"). Les autres types de serveur existent pour répondre à des besoins spécifiques qui ne nous concernent pas ici.

En plus des types de serveurs, il existe aussi plusieurs types de _tarification_ de serveurs. Les types de tarification sont listés et détaillés [sur ce lien](https://aws.amazon.com/fr/ec2/pricing/). Nous on utilisera la tarification à la demande. Mais d'autres types de tarification existent, à choisir en fonction de l'engagement et du besoin qu'on aura du serveur en production, pour des utilisations plus professionnelles.

Le lancement d'une instance s'effectue sur la page `Instances > Instances`, en cliquant sur le bouton "Lancer des instances".

Lors du lancement d'une instance, on doit choisir une **AMI** (Amazon Machine Image), qui est globalement une grosse configuration logicielle qu'on veut de notre serveur (OS, applications, etc). C'est obligatoire, bien qu'on puisse choisir une AMI quasiment vierge (genre juste un OS).

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
