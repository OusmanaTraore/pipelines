Ce repo contient les Pipelines utilisés pour le projet.

Il contient également le Dockerfile de base utilisé pour la construction des 
images, en test ou en prod.

Enfin, il contient les deux playbook Ansible pour déployer les versions sur les
serveurs test ou prod.

Plus en détail:

Dockerfile : fichier de base pour construire une image docker. Il contient centos et java.

Inventory.ini : fichier permettant d'identifier les serveurs de prod et de test;
Ils seront différenciés par le port ouvert pour la connexion ssh.

pipe_build_prod : fichier jenkins scripté pour tracker la branche Master du
projet, la builder, créer une image Docker contenant java et le war du projet, 
pusher cette image sur Docker Hub et enfin déployer et faire tourner un 
conteneur basé sur notre image sur le serveur de prod.

pipe_build_test : fichier jenkins scripté pour tracker la branche Develop du 
projet. Ensuite, même démarche que pour la prod mais sur le servuer de test.

pipe_rollback : fichier jenkins scripté pour faire un rollback de version 
sur la prod. Le job jenkins associé demande un paramètre "version" lors de son lancement.

playbook_prod.yml : fichier ansible pour déployer et faire tourner 
l'appli (branche master) dans un container sur le serveur de prod.

playbook_test.yml : fichier ansible pour déployer et faire tourner 
l'appli(branche develop) dans un container sur le serveur de test.


La branche Master est déployée sur le serveur de prod et est exposée sur le port 8080.

La branche Develop est déployée sur le serveur de test et est exposée sur le port 8081.

Un hook permet le lancement des jobs jenkins test et prod en cas de changement du code source
, au plus 1 minute plus tard ...

