# Démarrez votre première instance EC2

Plusieurs types d'instances sont proposés par AWS. Pour lancer notre première instance EC2, on doit commencer par choisir son bon type.
La liste des types d'instances EC2 disponibles est accessible dans `Instances > Types d'instances`.

Ici dans le cadre de ce cours, nous allons utiliser l'instance **t2.micro**, qui est gratuite pendant un an, pour faire du web "de base". Les autres types de serveur existent pour répondre à des besoins spécifiques qui ne nous concernent pas ici.

En plus des types de serveurs, il existe aussi plusieurs types de _tarification_ de serveurs. Les types de tarification sont listés et détaillés [sur ce lien](https://aws.amazon.com/fr/ec2/pricing/). Nous on utilisera la tarification à la demande. Mais d'autres types de tarification existent, à choisir en fonction de l'engagement et du besoin qu'on aura du serveur en production, pour des utilisations plus professionnelles.

Le lancement d'une instance s'effectue sur la page `Instances > Instances`, en cliquant sur le bouton "Lancer des instances".

Lors du lancement d'une instance, on doit choisir une AMI (Amazon Machine Image), qui est globalement une grosse configuration logicielle qu'on veut de notre serveur (OS, applications, etc).

