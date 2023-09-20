# Créez votre premier serveur sur AWS

Sur la console AWS, dans l'onglet "Services > Calcul", on peut accéder à un service appelé **Lightsail**, qui va permettre de créer rapidement un serveur web.

En suivant le formulaire de l'interface, on va créer un serveur web Apache, avec PHP et MySQL. On va l'appeler "test".

Attention Lightsail n'est gratuit que pendant les trois premiers mois d'utilisation du service (je dois absolument m'en séparer avant décembre au plus tard).

Une fois l'instance créée, on y obtient la clé SSH, on peut se connecter dessus pour y déposer nos scripts, etc.

On a accès à son IP publique : si j'entre `13.38.26.24` dans mon navigateur, je vois bien le site tel que je viens de le créer (avec la page LAMP par défaut).

Y a un onglet pour suivre les métriques du site si besoin aussi.

On a aussi une icône de terminal (sur la page d'accueil listant les instances lightsail), pour accéder à notre serveur dans un terminal. Ce qui peut permetre d'y mettre un fichier htdocs, par exemple.

On peut créer une copie de notre disque dur à tout moment, si besoin. On appelle ça un **instantané** (ou snapshot). Attention, la création d'un instantané est payante.

Lightsail permet ainsi de créer un serveur web en quelques clics, mais n'es pas très customisable si on a besoin d'apporter des modifications précises dessus (ce qui peut vite arriver en entreprise).

Pour créer un serveur web un peu plus personnalisable, on va utiliser **Elastic Beanstalk**.
