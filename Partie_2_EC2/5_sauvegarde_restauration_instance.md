# Sauvegardez et restaurez votre instance

On va réaliser des sauvegardes d'instances EC2, pour revenir en arrière si jamais je me retrouve dans une très grosse pagaille avec mon instance à un moment donné.

Il existe deux manière de sauvegarder une instance EC2 :

- Créer une image machine Amazon (AMI) de notre serveur, ce qui est super simple mais une AMI prend de la place et peut finir par devenir payant;
- Créer un instantané EBS pour sauvegarder le disque.

## Sauvegarde et restauration d'une AMI

Sur la liste des instances, je coche celle que je veux sauvegarder, puis je clique sur Actions > Images et modèles > Créer une image. Je laisse les paramètres par défaut et clique sur "Créer une image". L'image est alors visibles dans la partie Images > ami du menu de gauche.

Dans la partie EBS > Instantanés, on peut voir qu'AWS a créé un instantané de l'AMI.

Si je veux récupérer ce backup, je n'ai qu'à cliquer sur l'AMI de la liste, puis sur "Lancer une instance à partir d'une AMI". Une fois que ce sera fait, on peut alors supprimer l'instance cassée.

Pour "supprimer" l'AMI (si on en fait beaucoup, elles peuvent s'accumuler et devenir parasites), on doit faire "Actions > Désenregistrer une AMI" (c'est comme ça qu'on appelle une suppression d'AMI), sans oublier de supprimer l'instantané sur la pages des instantanés.

L'IP élastique doit alors pointer sur notre nouvelle instance, bien entendu, ce qui est paramétrable dans la console AWS.

## Sauvegarde et restauration d'un EBS

