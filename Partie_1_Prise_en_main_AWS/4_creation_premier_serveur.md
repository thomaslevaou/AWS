# Créez votre premier serveur web sur AWS

## Création d'un serveur Web via LightSail

Sur la console AWS, dans l'onglet "Services > Calcul", on peut accéder à un service appelé **Lightsail**, qui va permettre de créer rapidement un serveur web.

En suivant le formulaire de l'interface, on va créer un serveur web Apache, avec PHP et MySQL. On va l'appeler "test".

Attention Lightsail n'est gratuit que pendant les trois premiers mois d'utilisation du service (je dois absolument m'en séparer avant décembre au plus tard).

Une fois l'instance créée, on y obtient la clé SSH, on peut se connecter dessus pour y déposer nos scripts, etc.

On a accès à son IP publique : si j'entre `13.38.26.24` dans mon navigateur, je vois bien le site tel que je viens de le créer (avec la page LAMP par défaut).

Y a un onglet pour suivre les métriques du site si besoin aussi.

On a aussi une icône de terminal (sur la page d'accueil listant les instances lightsail), pour accéder à notre serveur dans un terminal. Ce qui peut permetre d'y mettre un fichier htdocs, par exemple.

On peut créer une copie de notre disque dur à tout moment, si besoin. On appelle ça un **instantané** (ou snapshot). Attention, la création d'un instantané est payante.

Lightsail permet ainsi de créer un serveur web en quelques clics, mais n'est pas très customisable si on a besoin d'apporter des modifications précises dessus (ce qui peut vite arriver en entreprise).

## Création d'un serveur Web via Elastic Beanstalk

Pour créer un serveur web un peu plus personnalisable, on va utiliser **Elastic Beanstalk**.

Le service est toujours trouvables dans la partie Services > Calcul de la console AWS.

Après faut juste suivre ce qu'il y a en vidéo (après un clic sur le CTA "Créer une application" de mon côté).

Oui, on peut créer un sous-domaine comme ça avec ce service gratos (pour le moment) !

À partir de ce moment-là, on peut directement charger un code tout prêt !

Mais ici dans ce cours, on n'en a pas. On va juste se servir de ce serveur pour exécuter un script PHP de test.

Après j'ai laissé tous les autres paramètres par défaut.

Et au bout de quelques minutes, l'instance devrait avoir été créée.

Enfin en fait j'ai du suivre le tuto [sur ce lien](https://docs.aws.amazon.com/fr_fr/elasticbeanstalk/latest/dg/using-features.environments.html), car une manip à suivre en plus doit être suivie avant de créer une appication Elastic Beanstalk. Si une instance EC2 a été créée, penser à la supprimer ensuite. Ça évite de devoir la payer.

Une fois l'environnement créé, je peux y accéder sur le lien <http://monapplicationtlv-env.eba-mm3gaabm.eu-west-3.elasticbeanstalk.com/>.

Certaines interfaces ne sont plus homogènes avec celles présentées par Openclassrooms. Y a pas mal d'informations sur diverses pages, à creuser à la manière d'un New Relic, mais ce sera pour plus tard si besoin.
