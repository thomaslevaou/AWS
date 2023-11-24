# Adoptez le bon type de cloud

## Les types de Cloud

3 types de cloud:

- **IaaS** ("Infrastructure as a Service"): on loue la puissance du serveur (comme vu dans le chapitre précédent);
- **PaaS** ("Platform as a Service"): accès au IaaS + on offre des services (transferts de vidéos, service d'e-mail, etc) + adapte le nombre de serveurs en fonction du trafic. C'est ce que fait Amazon notamment;
- **SaaS** ("Software as a Service"): c'est le fait d'utiliser un logiciel en ligne sans avoir à installer le logiciel sur son PC (par exemple Google Doc, Lucy à StreamMind, etc).

Grâce à un cloud PaaS :

- Le trafic est régulé automatiquement: il "suffit" de payer un peu plus cher pour réguler automatiquement un trafic, en période de forte charge;
- une partie des problèmes techniques d'infra est prise en charge par Amazon (ce n'est pas à moi d'être un expert en inra pour faire tourner le site);
- On peut avoir des services supplémentaires genre des e-mails super vite.

Mais attention, ça demande de coder parfois des trucs spécifiquement pour un cloud : on doit écrire du code spécifique pour un cloud donné quand on est pas encore dessus, et qui pourrait changer si on change de cloud.

Amazon fournit aussi des SaaS, mais on n'en parlera pas plus dans ce cours.

AWS a été le premier à se lancer dans le cloud. D'autres existent mais ils sont moins utilisés (Azure, Google Cloud).

## Principaux services d'AWS

Amazon offre des centaines de services, chacun pouvant prendre énormément de temps à être pris en main => personne ne sait complètement comment utiliser chacun de tous ces outils.

Mais certains services sont à connaître, comme :

- **EC2** ("Elastic Compute Cloud"): c'est un service permettant de gérer des serveurs sous forme de VM dans le cloud, avec accès à une fenêtre de commande pour les piloter à distance;
- **RDS** ("Relational Database Service"), pour gérer les bases de données dans le cloud;
- **S3** ("Simple Storage Service"), pour gérer des fichiers en ligne;
- **IAM** ("Identity and Access Management"), pour assurer une gestion des droits aux utilisateurs auxquels on veut donner un accès AWS (genre pour restreindre des accès à un comptable qui a juste besoin de télécharger des factures par exemple).
- **Lambda** pour exécuter du code sans se soucier du serveur ! Je vais devoir savoir le gérer avant d'arriver à la Sacem.
