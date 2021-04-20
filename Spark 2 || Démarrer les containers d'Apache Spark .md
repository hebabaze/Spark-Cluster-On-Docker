## Démarrer les containers d'Apache Spark

1. Pour démarrer Spark ,je dois être  dans le même répertoire que **docker-compose.yml**, et je vais lancer lancer le docker-compose pour lui dire, prends ce qu'il y a dans le yml et crée moi les containers qui sont indiqués avec la commande suivante : 
    
    sudo docker-compose up

![](https://github.com/hebabaze/pic/blob/master/docker-compose%20up.PNG)

2. Dans le reste de log ,On voit que le serveur a démarré ici et que le worker ensuite a démarré. Il s'est connecté au master.  les deux dernières informations qui sont les plus importantes. Le master qui annonce, j'ai enregistré un worker avec deux cœurs et un Giga de RAM. Et le worker dit, moi, j'ai été enregistré par le master.

![](https://github.com/hebabaze/pic/blob/master/docker-compose%20up%20R%C3%A9sult%20.%20PNG.PNG)

* si il vous affiche un message d'erreur que le docker service est masqué ,veuillez exécuter la commande suivate :
    
   `sudo systemctl unmask docker.service`

3.  Donc, ensuite, je vais ouvrir une nouvelle session, de façon à pouvoir conserver mes containers de cœurs démarrés et puis travailler sur une autre session(termminal). 

4.  Se connecter au master via le bash : 
     on remarque déjà dans l'imprime écran précédentes que le nom de master est : dockerspark_master_1 ,alors la commande est la suivante  : 
    
    `sudo docker exec -it dockerspark_master_1 /bin/bash`

> **voilà,je suis sur mon master, dans un répertoire dans lequel je vais trouver mon installation de Spark.dans le répertoire bin j'ai plusieurs  moyens pour accéder au spark soit avec pyspark (python) ou spark-shell (scala) ..**
 5. Accéder au dossier bin et lancer pyspark 
   
     `cd bin`

      `./pyspark`
dans interprétateur de commande :
* spark : pour ouvrir une session spark 
* sc :qui est une SparkContext qu'on peut utiliser pour créer des objets
Note : selon le fichier docker-compose.yml dans le même répertoire que lui , il y a un répertoire nommé data qui est monté sur le master et le worker dans le point /tmp/data



