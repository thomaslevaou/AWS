# Configurez une IP élastique

Si je redémarre une instance, l'IP publique a de grandes chances d'être modifiée, ce qui n'est pas très pratique pour s'y connecter (vu que par exemple, pour se connecter à la machine Windows, j'ai saisi l'IP publique). Je ne vais pas tryhard des redémarrages juste pour vérifier ça par moi-même, mais je fais confiance à ce que dit Mathieu Nebra sur OpenClassrooms à ce moment du tuto.

Ceci est dû au fait que même si le disque dur (le volume EBS du chapitre 2) reste le même, le serveur lancé est différent (j'imagine que chez Amazon, ils ont des serveurs en pièces détachées pour gérer leur gestion de ceux-ci ?). Pour conserver la même IP statique même si celle du serveur change, on va utiliser des **IP élastiques** (un peu comme faisait Jérémi à StreamMind de mémoire).

Y a une page dédiée pour ça dans la console AWS. Si on clique dessus puis sur "Allouer une adresse IP élastique", puis sur "Allouer" en laissant les paramètres par défaut, on obtient une adresse IP publique fixe (Ici 13.37.181.173). On peut alors cliquer sur l'action "Associer cette adresse IP Elastic", sélectionner sur la page affichée notre instance à laquelle on veut l'associer, puis cliquer sur "Associer". Une fois cela fait, si on retourne sur l'instance dans la liste des instances, et qu'on clique sur celle sur laquelle on a associé une IP, on retrouve bien l'adresse IP élastique désirée.

Ainsi, la commande ci-dessous marchera aussi pour accéder à notre serveur bitnami sur Debian 11 :

```bash
ssh -i "cle_aws.pem" bitnami@13.37.181.173
```

Avec une adresse IP publique stabilisée, on peut alors changer les DNS (serveurs de noms) pour associer notre nom de domaine à l'adresse IP 13.37.181.173 en enregistrement de type A, si on veut lui donner un nom sympathique.

Notons qu'entrer `13.37.181.173` dans une barre d'adresses d'un navigateur permettra d'afficher notre site Bitnami, comme avant avec l'ancienne IP.
