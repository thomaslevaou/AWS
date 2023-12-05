# Découvrez RDS

## Présentation globale

Amazon RDS (pour Relational Database Service) correspond au service de base de données d'Amazon.
L'idée est de simplifier une gestion de base de donnait qui serait plus traditionnellement faite avec un service du type MySQL.

RDS est ce qu'on appelle un PaaS (Platform as a Service), et même plus précisément un DBaaS (DataBase as a Service). Louer un serveur RDS implique donc de déjà louer un serveur IaaS.
Un serveur RDS n'est pas directement accessible via SSH (contrairement à une IaaS comme EC2 tout à l'heure, où on pouvait taper directement dessus), mais la base de données est déjà installée pour nous dessus. Et le matos du serveur est optimisé pour gérer une bdd. Amazon fait automatiquement les màj dessus, sans qu'on ait besoin d'y penser. Les sauvegardes sont bien plus simples avec RDS qu'en les faisant manuellement.
Et puis ça permet d'énormément optimiser les traitements nécessaires si on a besoin d'encore plus de taille de bdd.

## Types de base de données louables

On peut utiliser les moteurs de base de donnés connus avec RDS (MySQL, PostgreSQL, Microsoft SQL Server, etc).
On peut aussi utiliser _Amazon Aurora_, qui est le moteur de base de données créé spécifiquement pour les serveurs d'Amazon, et compatible (comprendre, "avec rétropédalage possible") avec MySQL ou PostgreSQL.
Ce qui le rend plus rapide dans ce contexte, mais attention au fait que le code d'Amazon Aurora soit propriétaire (et coûte plus cher que MySQL gratuit).

Le service RDS, comme son nom l'indique, s'occupe des bases de données **relationnelles**.
Si on a besoin un jour de base en NoSQL (non-relationnelles), le service _Amazon DynamoDB_ fait bien le taff askip.
Si on a besoin de traiter de grosses stats, d'un "PostgreSQL sous stéroïdes", on peut aller faire un tour du côté du service _RedShift_.
Et si on a besoin de migrer une bdd d'un autre serveur vers RDS, il existe même un service appelé _AWS Database Migration Service_.
