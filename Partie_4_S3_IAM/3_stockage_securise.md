#  Utilisez le stockage AWS de manière sécurisée

**IAM**, pour "Identification Access Management" ("Identification de gestion des accès"), est le service d'Amazon permettant à plusieurs personnes de gérer les accès et ressources de manière sécurisée (c'est-à-dire, "pas en partageant le mot de passe root avec tout le monde comme j'ai déjà vu par le passé"). Il est applicable sur tout AWS.

On va s'en servir ici pour permettre des restrictions d'accès sur les fichiers qu'on vient d'uploader dans nos buckets S3.

Dans le menu de gauche, on va surtout utiliser les liens "Utilisateurs" et "Politiques".

## Création d'un utilisateur

L'ajout d'un utilisateur se fait via le lien "Utilisateurs > Ajouter des utilisateurs".

Ici, on va créer un utilisateur qui devra avoir accès à la console AWS, donc je vais cocher cette case.
L'interface AWS a changé par rapport au tuto, mais perso je dois bien cocher le bouton radio "Je souhaite créer un utilisateur IAM", qu'on va appeler bob.
Lors du clic sur suivant, je peux alors définir ses autorisations (càd ses permissions), que je vais mettre en place ici via l'option "Attacher directement des politiques".

Comme je vais souhaiter donner à bob tous les accès sur IAM, je vais sélectionner la politique d'autorisation _AmazonS3FullAccess_, qui est une politique **gérée par AWS** (elle est de base présente et permet rapidement d'attribuer des droits aux utilisateurs). Si j'en ai besoin un jour, je sais que je peux lui créer des balises.

Ensuite, je peux cliquer sur "Créer un utilisateur", et je dois faire attention à bien enregistrer **son URL d'accès**, en plus de son nom d'utilisateur et de son mot de passe, c'est-à-dire ici les informations que j'ai enregistrées là où je sais.

Ce bob connecté a ainsi accès à mes buckets comme celui que j'ai créé l'autre jour "premier-test-bucket-aws".

Par contre, si je commence à regarder les instances EC2, je me retrouve avec une erreur d'autorisation.

Au passage, même si là on est en formation donc on s'en balek, dans un contexte professionnel il vaut mieux avoir une MFA (~=2FA) pour le compte root AWS.

## Configurations de politiques IAM

On souhaite maintenant créer des règles plus spécifiques à notre besoin : par exemple, je souhaite que bob n'ait accès qu'à un seul bucket S3 précis, et pas aux autres.

Si je regarde dans les détails de l'utilisateur bob, puis dans les détails de sa politique "AmazonS3FullAccess", puis sur le service "S3", je vois bien les 158 actions possibles pour mon utilisateur bob.

Je souhaite maintenant que bob puisse lister et lire les fichiers, mais pas en créer. Pour ce faire, je clique sur le lien "Politique" du menu de gauche, puis sur "Créer une politique". Après avoir sélectionné le Service S3, je sélectionne les deux cases à cocher "Toutes les actions de la liste" et "Toutes les actions de lecture" (visibles juste en dessous des titres "Liste" et "Lire").

Comme on veut restreindre les accès de bob qu'à un seul bucket, dans la partie "Ressources", je dois sélectionner le bouton radio "spécifique", puis sélectionner "ajouter des ARN" près de "bucket", et renseigner le nom de mon bucket dans le champ "resource bucket name" (donc ici "premier-test-bucket-aws").
Un ARN, c'est un identifiant unique d'une ressource dans AWS.

bob devra avoir accès à tous les objets du bucket premier-test-bucket-aws. C'est pourquoi près de "object", je vais aussi sélectionner "ajouter des ARN", renseigner le nom du bucket, puis cliquer sur la case "N'importe quel object name", avant de cliquer sur "Ajouter des ARN".

Je peux alors cliquer sur "Suivant", puis renseigner le nom "premier-test-bucket-aws-bob-lecture-seule", puis cliquer sur "Créer la politique".

Pour attacher cette politique à bob, je la sélectionner dans la liste des politiques (le filtre "Gérées par le client" aidant bien), puis sur "Actions > Attacher". Je peux alors sélectionner bob dans la liste qui apparaît à l'écran, puis sur "Attacher la politique". La politique sera alors visible dans les politiques de bob (cliquer dessus dans la liste des utilisateurs, puis voir la partie "Autorisations" des détails).

On peut retirer une politique d'un utilisateur en la sélectionnant puis en cliquant sur "Supprimer".