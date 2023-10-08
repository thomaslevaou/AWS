# Découvrez les services d'Amazon EC2

Amazon EC2, ou Elastic Compute Cloud, est le premier service d'Amazon (celui qui permet de commander la _puissance_ d'un serveur).

Comme d'hab, on retrouve ce service dans la section Services > Calcul. Je suis ensuite littéralement le tuto du cours.

La page **Instances** affiche la liste des serveurs EC2 qui tournent en ce moment.

Sur le lien `Images > AMI`, on peut voir la liste des **images** des instances EC2.

Un AMI, pour "Amazon Machine Image", est une fonctionnalité permettant de lancer un serveur préconfiguré. Ainsi, on peut éviter d'avoir à faire plusieurs fois les mêmes réglages de manière redondante, au lancement d'un serveur. On peut récupérer (de manière gratuite ou payante), des AMI sur la marketplace d'Amazon, ou créer nos propres AMI pour éviter d'avoir à faire plusieurs fois les mêmes paramétrages.

Sur AWS, la puissance de calcul du processeur est appelée _Instance_, et c'est ce qu'on voit sur la page de liste des Instances. Mais dans la partie `Elastic Block Store > Volumes`, on peut voir la liste de tous les disques durs utilisés par les instances AWS que j'utilise. On appelle ces disques durs des **Elastic Block Stores** ou **EBS**.
Dans `Elastic Block Stores > Instantanés`, on peut sauvegarder des disques EBS, ce qui peut être un autre moyen de faire des backups.

Dans `Réseau et Sécurité > adresses IP élastiques`, on va pouvoir attribuer une IP statique à nos serveurs, ce qui va lui permettre de garder la même IP.

Dans `paire de clés`, on va pouvoir gérer les clés SSH pour accéder aux serveurs, comme avec GitLab.

Dans `Équilibrage de charge`, on va pouvoir gérer l'Elastic Load Balancer, pour que le trafic soit partagé entre plusiseurs serveurs, et dirigé vers le serveur le moins occupé.

Dans `Auto Scaling`, on va pouvoir ajouter un serveur pour gérer le trafic, seulement pendant les périodes de forte charge.

Avec Elastic BeanStalk vu précédemment, le load balancer, l'auto scaling et les machines EC2 à partir d'AMI sont créées d'un coup automatiquement.
