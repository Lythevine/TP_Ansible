# **TP Ansible 2**

## **Énoncé de l’exercice:**
Créer des dockerfiles pour 4 containers dans deux réseaux, il faut déjà pouvoir vous connecter en ssh sur les 4 containers avec clé ssh privées.

Ensuite vous allez me créer un playbook ansible qui affiche en mode debug les facts de chaque containers

Ensuite votre playbook devra ensuite créer un fichier IP.txt dans le home de vos utilisateur et le fichiers devra contenir les facts des adresses ip de vos conteneurs
non, vous allez créer plutôt après une tâche fact qui affiche les interfaces réseaux de chaque containers (informations contenus dans les facts)
annuler cette demande

Ensuite vous allez créer un script shell qui récupère tous les containers docker qui tournent, ensuite il les parcours pour afficher l'adresse ip de chaque container.

## **Résolution:**

**docker-compose -d build**

**docker images**

tp-01_containeraa                  latest    952cfe8c34be**   
tp-01_containerbb                  latest    952cfe8c34be**   

**docker ps**

CONTAINER ID   IMAGE               COMMAND                  CREATED             STATUS             PORTS            NAMES
361bf0edf8c0   tp-01_containeraa   "/docker-entrypoint.…"   About an hour ago   Up About an hour   22/tcp, 80/tcp   container-aa
205447a82465   tp-01_containerbb   "/docker-entrypoint.…"   About an hour ago   Up About an hour   22/tcp, 80/tcp   container-bb


**docker exec -it 361bf0edf8c0 bash**

Afin de vérifier la copie effective de ma clé publique (key.pub) dans le fichier authorized_keys 

**sshuser@361bf0edf8c0: Connexion réussie !🙂**

**cd /home/sshuser/.ssh**
**ls -l**

J’obtiens, 
**-rw-r--r-- 1 root root 573 Apr 27 14:40 authorized_keys**

Ce qui signifie que sshuser ne peut que lire car c’est le root qui est propriétaire.
Je change donc le propriétaire du groupe root par sshuser afin de pouvoir écrire également avec la commande suivante:
**sudo chown -R sshuser:sshgroup /home/sshuser/.ssh**

**docker inspect 361bf0edf8c0** 

Cette commande me permet de récupérer l’adresse IP de mon container.

**ssh -i public-key-2 Lina2@192.168.48.3**

Cette commande me permet de me connecter  en ssh à mon container2

Et bimmmm…

**sshuser@361bf0edf8c0:~$ Connexion réussie !!!!! 😀 👏**
