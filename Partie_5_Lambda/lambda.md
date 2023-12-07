# Service Lambda

Vidéos intéressantes sur le sujet:
<https://www.youtube.com/watch?v=JEv8_tMdgNk>
<https://www.youtube.com/watch?v=1toe9_82dZo>

Le but du service Lambda est de laisser à AWS complètement la main sur l'infra qui exécute le code qu'on lui envoie.
Le développeur envoie juste le code qu'il souhaite exécuter, et Lambda s'occupe de son exécution.

On n'a donc pas besoin de gérer nous-mêmes des serveurs, ni la scabilité. La tarification évolue en fonction du nombre d'exécutions du code.
On dit que le code est **serverless** : les serveurs existent mais ce n'est pas nous qui nous en occupons. L'expression est à comprendre dans le sens "comme si les serveurs n'existaient pas".

Exemples d'utilisation:

- un traitement sur des fichiers sur S3
- nettoyer des données avant de les insérer dans une DB RDS
- du backend d'applis web, IoT ou mobiles qui se joignent à une API: les lambda permettent alors d'exécuter du code en intermédiaire.

Après la formation sera en freestyle, et je demanderai quelles docs ont aidé celleux qui travaillent déjà dessus
