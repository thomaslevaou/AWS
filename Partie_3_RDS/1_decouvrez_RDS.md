# Découvrez RDS

Amazon RDS (pour Relational Database Service) correspond au service de base de données d'Amazon.
L'idée est de simplifier une gestion de base de donnait qui serait plus traditionnellement faite avec un service du type MySQL.

RDS est ce qu'on appelle un PaaS (Platform as a Service), et même plus précisément un DBaaS (DataBase as a Service). Louer un serveur RDS implique donc de déjà louer un serveur IaaS.
Un serveur RDS n'est pas directement accessible via SSH, mais la base de données est déjà installée pour nous dessus. Et le matos du serveur est optimisé pour gérer une bdd. Amazon fait automatiquement les màj dessus, sans qu'on aie besoin d'y penser. Les sauvegardes sont bien plus simples avec RDS qu'en les faisant manuellement.
Et puis ça permet d'énormément optimiser les traitements nécessaires si on a besoin d'encore plus de taille de bdd.

On peut utiliser les moteurs de base de donnés connus avec RDS (MySQL, PostgreSQL, Microsoft SQL Server, etc).
On peut aussi utiliser Amazon Aurora, qui est le moteur de base de données créé spécifiquement pour les serveurs d'Amazon.
Ce qui le rend plus rapide dans ce contexte, mais attention au fait que le code d'Amazon Aurora soit propriétaire.

Et si on a besoin un jour de base en NoSQL, Amazon DynamoDB fait bien le taff askip.
