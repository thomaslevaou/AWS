# Sauvegardez et restaurez la base de données

Les instances RDS sont automatiquement sauvegardées toutes les semaines. Si besoin, on peut toujours réaliser une sauvegarde manuelle, en cliquant sur "Actions > Prendre un instantané". Les instantanés sont alors listés sur la page "Instantanés".

Si on veut restaurer l'instantané, on clique sur celui-ci dans la liste, puis on sélectionne "Actions > Restaurer l'instantané". On se retrouve alors devant le formulaire de création d'instance RDS (le même qu'au chapitre précédent), qui permet alors de créer une instance RDS à partir de cet instantané. Une nouvelle instance RDS avec la base de donnée telle qu'indiquée dans l'instantané, sera alors créée. Attention au fait que le point de terminaison de l'instance RDS aura alors changé.

On peut aussi restaurer l'instantané en allant dans "Instances", puis en sélectionnant l'action "Restaurer à un moment donné", si on a besoin de récupérer un backup à un moment vraiment très précis, parmi ceux continuellement faits par AWS.
