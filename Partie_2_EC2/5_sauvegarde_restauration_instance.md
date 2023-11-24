# Sauvegardez et restaurez votre instance

On va réaliser des sauvegardes d'instances EC2, pour revenir en arrière si jamais je me retrouve dans une très grosse pagaille avec mon instance à un moment donné.

Il existe deux manière de sauvegarder une instance EC2 :

- Créer une image machine Amazon (AMI) de notre serveur, ce qui est super simple mais une AMI prend de la place et peut finir par devenir payant;
- Créer un instantané EBS pour sauvegarder le disque.

## Sauvegarde et restauration d'une AMI

Sur la liste des instances, je coche celle que je veux sauvegarder, puis je clique sur Actions > Images et modèles > Créer une image. Je laisse les paramètres par défaut et clique sur "Créer une image". L'image est alors visibles dans la partie Images > ami du menu de gauche.

Dans la partie Elastic Block Store > Instantanés, on peut voir qu'AWS a créé un instantané de l'AMI.

Si je veux récupérer ce backup, je n'ai qu'à cliquer sur l'AMI de la liste, puis sur "Lancer une instance à partir d'une AMI". Une fois que ce sera fait, on peut alors supprimer l'instance cassée.

Pour "supprimer" l'AMI (si on en fait beaucoup, elles peuvent s'accumuler et devenir parasites), on doit faire "Actions > Désenregistrer une AMI" (c'est comme ça qu'on appelle une suppression d'AMI), sans oublier de supprimer l'instantané sur la pages des instantanés.

L'IP élastique doit alors pointer sur notre nouvelle instance, bien entendu, ce qui est paramétrable dans la console AWS.

## Sauvegarde et restauration d'un EBS

En réalisant des sauvegardes EBS, on réalise des **sauvegardes incrémentielles** : le premier instantané sauvegarde tout le disque, mais les suivants ne sauvegardent que les différences de mémoire (par exemple, si seulement 1 Go a changé par rapport au premier instantané, alors le deuxième ne fera qu'1 Go).

Pour réaliser une sauvegarde EBS, je vais dans Elastic Block Stores > Volumes, je coche le volume lié à l'instance que je veux sauvegarder, puis je clique sur "Créer un instantané". Je donne alors un nom à mon instantané, puis clique sur "Créer un instantané". Et c'est comme ça que je peux voir mon backup dans "Elastic Block Store > Instantanés". J'ai donc à ce moment-là créé un _instantané de mon volume_, que je peux donc restaurer sur une instance donnée.

Si je veux restaurer mon instance avec cette instantané, je coche l'instantané EBS, puis clique sur "Actions > Créer un volume à partir d'un instantané" (de volume donc).

Attention, la "zone de disponibilité" (le datacenter) doit être la même que celle de l'instance que je veux restaurer (ici donc "eu-west-3c"). Une fois que c'est vérifié / modifié, je peux laisser le reste par défaut, et cliquer sur "Créer un volume".

Je vois alors sur la page "Volumes", qu'un nouveau volume a été créé, marqué comme "disponible" (donc pas en cours d'utilisation).

Je peux maintenant arrêter le serveur (donc l'instance). Et noter alors le point de montage de mon disque, càd ici : `/dev/xvda`  (trouvable en bas des données de l'instance, dans Stockage > Nom du périphérique racine).

En revenant sur la page de volumes, je peux _détacher le volume en cours d'utilisation_ (c'est une action possible sur un volume). Le volume en cours d'utilisation devient alors "disponible".

Je peux alors prendre mon volume créé tout à l'heure, puis sélectionner l'action "attacher le volume". C'est là que je dois renseigner l'instance à attacher au volume, ainsi que le point de montage précédemment noter.

Je peux alors (re-)démarrer mon instance sur Debian. Si tout est revenu à la normale, on peut alors détacher l'ancien volume.