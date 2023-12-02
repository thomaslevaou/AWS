# Définissez les droits d'accès à Amazon S3

Des services d'Amazon S3 permettent aussi de définir des accès, en complément de ceux proposés par IAM.

Il est particulièrement important d'être extrêmement pro et vigilant sur la gestion des accès S3. D'après ce cours, les failles de sécurité dûes à une absence de vigilance sur les backups S3 (notamment des backups de base de données avec ses mots de passe et usenames ouverts à tous) sont presque monnaie courante en entreprise.

On ne va voir ici qu'une introduction à la gestion des accès sur S3, qui servira surtout à dire "En cas d'utilisation en production, merci de RTFM bieeen plus en détail pour éviter toute bourde !".

## Stratégies de ressources

### Principe

On distingue donc deux types de règles :

- les _politiques IAM_, vues au chapitre précédent, définissant ce qu'un _utilisateur_ a le droit de faire;
- les **stratégies de ressources** (Resource Policy), qui définissent ce qu'il est possible de faire sur une _ressource d'un service AWS_, comme un bucket S3 ici.

Une stratégie de ressource appliquée à un bucket s'appelle plus simplement une **Bucket Policy**.

Notons qu'en cas de conflit entre les deux politiques, c'est la plus restreinte qui l'emporte.

En général, ce sont les politiques IAM qui permettent de gérer les accès des utilisateurs internes à AWS. Les stratégies de ressources sont surtout utilisées pour la gestion des accès vis-à-vis du reste d'Internet.

Dans une configuration en interne par exemple, une stratégie de bucket doit être employée pour dire "des utilisateurs en interne ont le droit de lire ce bucket", mais c'est la stratégie IAM qui décrit précisément qui a le droit de voir quoi (? enfin ça doit être un truc comme ça, à voir en fonction de l'implémentation technique maintenant).

### Application technique

Les stratégies de ressources sont généralement écrites au format JSON. En voici un exemple :

```JSON
{
"Version":"2012-10-17",
"Statement": [
    {
        "Effect":"Allow",
        "Principal": "*",
        "Action":["s3:GetObject"],
        "Resource":["arn:aws:s3:::examplebucket/*"]
    }
]
}
```

Attention `"Version"` correspond à un numéro de version, ici je suppose la version du "17 octobre 2012" qu'openclassrooms appelle "version 3".
Dans `Statement` sont listées dans un tableau les règles de la policy. Ici, on va autoriser à tout le monde, y compris aux gens sur le web sans compte AWS, un accès aux objets de tout le bucket `examplebucket`.

Si besoin, la liste de toutes les actions qu'on peut mettre dans `Actions` est listée [sur ce lien](https://docs.aws.amazon.com/fr_fr/AmazonS3/latest/userguide/using-with-s3-actions.html).

On peut aussi donner des noms (Id, Sid) à la policy et ses règles. La précision d'un utilisateur dans `Principal` se fait via son accès IAM, comme ci-dessous :

```JSON
{
"Version": "2012-10-17",
"Id": "ExamplePolicy01",
"Statement": [
    {
        "Sid": "ExampleStatement01",
        "Effect": "Allow",
        "Principal": { "AWS": "arn:aws:iam::Account-ID:user/Dave" },
        "Action": ["s3:GetObject", "s3:GetBucketLocation", "s3:ListBucket"],
        "Resource": ["arn:aws:s3:::examplebucket/*", "arn:aws:s3:::examplebucket"]
    }
]
}
```

Notons que mettre `{ "AWS": "*" }` dans `"Principal"`, est équivalent à mettre juste `*`. On peut combiner deux statements comme dans la stratégie de bucket ci-dessous :

```JS
{
"Version": "2012-10-17",
"Id": "ExamplePolicy02",
"Statement": [
    {
        "Effect": "Allow",
        "Principal": { "AWS": "*" },
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::my-brand-new-bucket/public/*"
    },
    {
        "Effect": "Allow",
        "Principal": { "AWS": "arn:aws:iam::Account-ID:user/Dave" },
        "Action": ["s3:PutObject", "s3:DeleteObject"],
        "Resource": "arn:aws:s3:::my-brand-new-bucket/*"
    }
]
}
```

Pour appliquer une stratégie de bucket sur AWS, je vais dans `S3 > Compartiments`, je clique sur le compartiment sur lequel je veux appliquer une stratégie, puis je clique sur "Autorisations". Ici, je vais vouloir rendre les images de mon compartiment publiquement accessibles, d'où le fait que je vais faire en sorte de décocher la case "Bloquer tous les accès publics" (en passant par le bouton "Modifier" dans la section associée).

Puis dans la partie "Stratégie de compartiment", je peux cliquer sur "Modifier". Dans le bloc "Stratégie" qui apparaît alors à l'écran, je peux renseigner le JSON suivant :

```JSON
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Sid": "LectureSeule",
   "Principal": "*",
   "Effect": "Allow",
   "Action": [
    "s3:GetObject"
   ],
   "Resource": ["arn:aws:s3:::premier-test-bucket-aws/*"]
  }
 ]
}
```

Le menu à droite aide à retrouver les actions. Maintenant, l'URL de l'objet du bucket (pour rappel, <https://premier-test-bucket-aws.s3.eu-west-3.amazonaws.com/Capture+d%E2%80%99%C3%A9cran+de+2023-11-23+21-14-52.png>) est publiquement accessible pour tout le monde, même en navigation privée.

Si maintenant je souhaite ajouter une autre polique de bucket pour que notre utilisateur bob puisse ajouter des fichiers (enfin il le peut déjà via sa politique IAM, mais c'est juste pour montrer ici comment le faire via une bucket policy), je modifie les autorisations du bucket en renseignant notamment son identifiant (arn) IAM, comme ci-dessous :

```JSON
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Sid": "LectureSeule",
   "Effect": "Allow",
   "Principal": "*",
   "Action": "s3:GetObject",
   "Resource": "arn:aws:s3:::premier-test-bucket-aws/*"
  },
  {
   "Sid": "EcritureBob",
   "Effect": "Allow",
   "Principal": { "AWS" : "arn:aws:iam::527712552468:user/bob" },
   "Action": "s3:PutObject",
   "Resource": "arn:aws:s3:::premier-test-bucket-aws/*"
  }
 ]
}
```
