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

Au fait, les gens sur Windows ont besoin de passer par PuTTY (ou MobaXTerm) pour se connecter en SSH à un serveur Linux. Ceci est du au fait que Windows ne propose pas de support natif pour les connexions en SSH (qui pour rappel, veut dire Secure SHell). Pour avoir ce support sur Windows, il est nécessaire d'installer un **client SSH** dessus, et c'est ce que font Putty et MobaXterm, par exemple. Notons au fait qu'il existe maintenant WSL pour émuler un environnement Linux sur Windows, et j'en aurai probablement besoin à la Sacem.

On peut aussi louer une instance EC2 Windows sur AWS (AMI "Microsoft Windows Server 2022 Base"), qui se crée de manière analogue à la précédente.

Une fois l'instance créée, elle est publiquement accessible sur `ec2-35-180-139-227.eu-west-3.compute.amazonaws.com` (attention à restreindre les accès RDP à mon IP, et à créer un groupe de sécurité pour cette utilisation, sinon pour une raison encore peut claire - sûrement un bug côté AWS ou un truc que je n'ai pas encore compris concernant la restriction d'IP à ce sujet pour le moment ? À voir un jour mais osef pour le moment, pour ne pas perdre trop de temps, le serveur m'est inaccessible).

Pour s'y connecter, la marche à suivre est légèrement différente.

Sur un serveur Windows, la clé SSH utilisée lors de la création de l'instance, est celle permettant de _déchiffrer_ le mot de passe du serveur Windows. Via l'option associée dans "Sécurité", on doit uploader le fichier de clé privée pour obtenir le mot de passe.

Nom: Administrator
ID instance: i-0f342957c33a8a42b
IP privée: 172.31.43.172
IP publique: 13.39.19.138

Pour se connecter sur une machine Windows depuis un serveur Debian (mon PC perso), j'utilise FreeRDP, qui est un logiciel permettant d'avoir sur Linux un client RDP, ce dernier étant le protocole pour se connecter à distance sur une machine Windows (a priori l'inverse de Putty sur Windows pour aller sur Linux):

```bash
sudo apt install freerdp2-x11
xfreerdp /v:13.39.19.138 /u:Administrator
```

Puis avec le mot de passe indiqué dans le fichier associé, ça passe !!!

Le serveur n'est pas accessible dans une barre d'adresses, mais en même temps ce n'est pas du tout configuré pour être un serveur Web, donc à la limite je peux comprendre.
