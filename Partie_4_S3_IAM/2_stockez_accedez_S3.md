# Stockez et accédez à des fichiers sur Amazon S3

## Suppression des buckets existants

Sur la console AWS, on peut trouver S3 dans "Services > Stockage > S3".

Deux buckets ont été créés par Elastic Beanstalk, pour une raison encore inconnue. Je peux les supprimer.

Pour les supprimer, ça a été un peu galère. Pour le premier j'ai improvisé une création d'utilisateur dans IAM, lui accorder tous les droits sur les buckets, puis me connecter avec lui et supprimer le bucket.
Mais ça n'a pas marché pou l'autre, donc à la place je suis allé dans ses autorisations, et j'ai supprimé sa stratégie de compartiment (Bucket Policy) avant de pouvoir l'utiliser. Je ne sais pas encore exactement à quoi ça sert, donc par précaution, en voici ci-dessous une copie :

```JS
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "eb-af163bf3-d27b-4712-b795-d1e33e331ca4",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::527712552468:role/role-pour-elastic-beanstalk"
            },
            "Action": [
                "s3:ListBucket",
                "s3:ListBucketVersions",
                "s3:GetObject",
                "s3:GetObjectVersion"
            ],
            "Resource": [
                "arn:aws:s3:::elasticbeanstalk-eu-west-3-527712552468",
                "arn:aws:s3:::elasticbeanstalk-eu-west-3-527712552468/resources/environments/*"
            ]
        },
        {
            "Sid": "eb-58950a8c-feb6-11e2-89e0-0800277d041b",
            "Effect": "Deny",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:DeleteBucket",
            "Resource": "arn:aws:s3:::elasticbeanstalk-eu-west-3-527712552468"
        }
    ]
}
```

## Création d'un bucket

Je peux donc à présent me rendre sur [la page listant les compartiments](https://s3.console.aws.amazon.com/s3/buckets?region=eu-west-3), en constatant bien qu'au moment où j'écris ces lignes, je ne vois pas de compartiment dans la liste.

Attention, un nom de bucket sur AWS ne doit être utilisé par personne d'autre sur AWS entier (id unique). Le mien va s'appeler `premier-test-bucket-aws`.

On peut laisser les autres paramètres par défaut (AWS s'occupe par défaut, comme indiqué dans le formulaire, de chiffrer les fichiers en toute transparence pour nous).

Les informations renseignées dans le formulaire de création sont indiquées dans les détails du compartiment, partie "Propriétés".

Comme on peut voir dans la partie "Autorisations", le compartiment entier n'est pas ouvert au public. En gros un random sur Internet ne pourra pas venir y toucher.

## Ajout et modification d'objets

On peut voir les objets (fichiers) du bucket dans la partie "Objets" des détails de celui-ci (pour l'instant, il n'y en a aucun).
On peut ajouter un objet via le bouton "Charger", puis "Ajouter des fichiers". On peut y mettre n'importe quel type de fichier (là j'ai mis une image png).

On laisse la classe de stockage proposée par défaut ("standard"), mais c'est important que c'est là qu'on la choisit, si on a besoin de fichiers rapidement accessibles par exemple.

Attention, l'URL de l'image n'est pas publique : si je clique sur l'URL sur les détails de l'image, je n'aurai aucun résultat. Pour afficher mon image, je dois cliquer sur le bouton "Ouvrir" en haut à droite de la page.

Ici on passe par l'interface, mais en général on passe par l'API AWS pour télécharger des fichiers en utilisant le S3.

## Ajout d'une règle de cycle de vie

Avec S3, on peut configurer des **règles de cycle de vie**, qui nous permettent de supprimer automatiquement certains fichiers au bout de quelques jours.
Pour ce faire, je vais dans la partie "Gestion" des détails du bucket, ce qui me permet de cliquer sur le bouton "Créer un règle de cycle de vie".
On peut alors s'amuser avec le formulaire pour faire des actions régulières, sachant qu'on peut appliquer un préfixe pour appliquer l'action sur les fichiers commençant par "Capt" (pour les captures d'écran), etc. Attention à ne pas se tromper lors de la création du préfixe, ce qui entraînerait des suppressions d'objets potentiellement inattendues.
