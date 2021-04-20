
**requirement :**
>    
     sudo apt update
     sudo apt install curl

1.  J'ai récupéré ici avec « curl » une clé pour la signature des dépôts de Docker.
   
       `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
 
* Pour vérifier ma signature : 

     `sudo apt-key fingerprint 0EBFCD88`

2. Ensuite, j'ai ajouté, à l'aide de add-apt-repository ces dépôts dans ma liste de dépôts sur Ubuntu.

   ` sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`

3. Ensuite j'ai fait un sudo-apt-get-update pour mettre à jour la liste de ces dépôts:

    `sudo apt-get update`
4. installation de service docker engine et containerd:
   
   `sudo apt-get install docker-ce docker-ce-cli containerd.io`

5. Démarrer la service et activer docker : 
   ``` 
    sudo service docker start
    service docker status
    sudo systemctl enable docker
   ```
6.  Afficher la version installer de Docker 

    `docker --version`
7. Tester l'installation :

    `sudo docker run hello-world`

    ![](https://github.com/hebabaze/pic/blob/master/dock.PNG)

8.  Installer **docker-composer** qui est un système basé sur des script qui permet de lancer, grâce à un fichier de configuration "yml, plusieurs container, donc de composer peut être un environnement de Cluster simulé sur cette machine à l'aide d'un fichier de configuration qui va dire « Lance un premier container et puis un deuxième avec telle ou telle propriété ». 

    `   apt-get install docker-compose `
9.  Ajouter votre utilisateur actuel au group docker :
    `sudo usermod -aG docker your-user`
***

## Installation de l'image Spark 
1.  Récupérer l'image avec la commande docker pull à partir de dépôts de Docker :

    `   sudo docker pull gettyimages/spark`
2.  Importer le fichier de configuration de docker composer 
>  Que fait ce yml ? Il indique qu'il faut lancer deux containers. Un container nommé master, un container nommé worker. Deux containers qui sont en fait des instances de la même image si vous voulez. En exposant un certain nombre de ports, 

    `git clone https://github.com/gettyimages/docker-spark.git`










