# Connectez-vous à votre instance

On va ici se connecter à notre instance EC2 en SSH.

Pour ce faire, on doit cliquer sur l'ID de l'instance dans la liste des instances, puis cliquer sur le bouton "Se connecter" en haut à droite, puis sur "Client SSH".

Je peux alors ouvrir un terminal en local, et ouvrir les commandes indiquées sur le tuto :

```bash
cd ~/Documents/Informatique/AWS/
chmod 400 cle_aws.pem # 100 000 000 en binaire, pour rappeler que le fichier n'est accessible qu'en lecture seule, et que par l'utilisateur courant
ssh -i "cle_aws.pem" bitnami@ec2-35-181-151-129.eu-west-3.compute.amazonaws.com # Attention on utilise bitnami et pas admin en nom d'utilisateur avec notre AMI
```

Notons que lors de la connexion SSH, l'option `-i` est utilisée ici pour `identify_file`, c'est-à-dire dans le fait d'utiliser un fichier contenant la clé privée de l'utilisateur, pour son authentification.

Et nous voilà connecté en SSH sur le serveur Debian 11 (on peut récupérer le numéro de version en faisant un `cat /etc/os-release`).
