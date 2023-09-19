# Qu'est-ce que le Cloud

À la base, il y a une vingtaine d'années, le site Amazon avait acheté une blinde de serveurs pour gérer les périodes de forte charge (genre les fêtes de fin d'année).

Et ils ont compris qu'en achetant des serveurs partout dans le monde, ils pourraient en louer à d'autres et faire en sorte que des gens puissent louer des serveurs en ajustant leur puissance en fonction de la charge pendant certaines périodes ou non. Eux ils pilotent plein de serveurs dans le monde, tandis qu'un développeur avec son site web n'a plus besoin d'acheter de nouveaux serveurs juste pour gérer certaines périodes de fort trafic (et donc inutile le reste de l'année): tout le monde y trouve son intérêt.

L'idée est de pouvoir louer _la puissance de la machine_ qui n'est pas utilisée hors période de charge, pour qu'elle ne serve pas à rien chez Amazon quand leurs ingénieurs n'en ont pas besoin. On loue bien la puissance de la machine (pas la machine elle-même) : si un disque dur grille ou qu'il y a un autre problème sur une machine, c'est Amazon qui se charge de le régler, pas nous.
Le fait de louer une _puissance de machine_, c'est ici ce qu'on appelle **le cloud**.

Alors qu'en étant _on-premise_ (ici dans ce contexte, à ne pas confondre avec le vocabulaire employé à StreamMind pour ces mêmes termes), on loue une machine.

On va ici étudier le cloud d'Amazon (le plus populaire), mais Google et Microsoft ont aussi un système de cloud au fonctionnement similaire.

La responsabilité en cas de problème technique est dite **partagée** : en fonction de la nature du problème, c'est soit à AWS, soit à nous de corriger (comme en entreprise avec les gens qui gèrent l'infra).
