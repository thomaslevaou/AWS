# Qu'est-ce que Simple Storage Service (S3) ?

Amazon S3 est, comme son nom l'indique, un service de stockage de fichiers.
Son but est d'héberger des images, parfois des fichiers HTML, un peu à la manière de pixr ou cloudfront.

Ça ressemble un peu à un FTP, mais sans utiliser le protocole FTP.

Airbnb s'en sert pour stocker les images, Netflix, ses films et séries, Openclassrooms pour les images de ses cours, etc. Pas mal de boîtes s'en servent aussi pour récupérer les backups de leurs bases de données.

Techniquement, on _pourrait_ créer un accès FTP sur une instance EC2, au lieu de s'enquiquiner avec le S3. Mais S3 offre quelques avantages accessibles sur demande, comme :

- une gestion précise et facilement réalisable des droits d'accès utilisateur;
- un versioning des fichiers;
- un chiffrement des fichiers;
- une réplication des fichiers dans plusieurs datacenters (si on veut qu'ils soient copiés dans plusieurs régions du monde à l'occase);
- une configuration de la date d'expiration des fichiers.
- pas de limite de place: dès qu'on dépasse la taille d'un disque dur, Amazon en rajoute un autre en soum soum (alors que si on stockait sur une instance EC2, on pourrait se retrouver bloqué par la limite de stockage du volume EBS).

De plus, à stockage équivalent, S3 coûte moins cher qu'un volume EBS.

Avec S3, on place nos données dans ce qu'on appelle des _buckets_ ("seaux"), dans lesquels on peut mettre des fichiers et des sous-dossiers.
Et les fichiers sont ici appelés des _objets_.

S3 peut prévoir la facturation en fonction de la fréquence de récupération de l'objet: moins un objet est récupéré souvent, moins sa gestion sera chère (c'est pratique pour ne pas avoir à payer le même prix pour un backup de bdd que pour des images à récupérer toutes les heures, par exemple).

Le temps d'accès d'un fichier qu'on n'a besoin de récupérer qu'une fois par an sera plus long aussi (tout en échange du fait d'être moins cher).