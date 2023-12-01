# Utilisez le stockage AWS de manière sécurisée

**IAM**, pour "Identification Access Management" ("Identification de gestion des accès"), est le service d'Amazon permettant à plusieurs personnes de gérer les accès et ressources de manière sécurisée (c'est-à-dire, "pas en partageant le mot de passe root avec tout le monde comme j'ai déjà vu par le passé"). Il est applicable sur tout AWS.

On va s'en servir ici pour permettre des restrictions d'accès sur les fichiers qu'on vient d'uploader dans nos buckets S3.

Dans le menu de gauche, on va surtout utiliser les liens "Utilisateurs" et "Politiques".

L'ajout d'un utilisateur se fait via le lien "Utilisateurs > Ajouter des utilisateurs".

Ici, on va créer un utilisateur qui devra avoir accès à la console AWS, donc je vais cocher cette case.
L'interface AWS a changé par rapport au tuto, mais perso je dois bien cocher le bouton radio "Je souhaite créer un utilisateur IAM".
Lors du clic sur suivant, je peux alors définir ses autorisations (càd ses permissions), que je vais mettre en place ici via l'option "Attacher directement des politiques". 