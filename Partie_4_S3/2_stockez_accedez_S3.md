# Stockez et accédez à des fichiers sur Amazon S3

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

