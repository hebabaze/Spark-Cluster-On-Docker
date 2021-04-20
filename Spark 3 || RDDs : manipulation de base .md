## Création d'un RDD
* Dans le container Master j'ai placé un fichier text (un peu volumineux) pour que je puisse l'utiliser 
* J'ai procéder par  mettre le fichier dans le dossier data de la machine réel dans le même emplacement avec le fichier de config**.yml .
* Je lance le containe-compose  et j’accède au interprétateur python :
### Lancer Le Container Master 
```
    sudo docker-compose up
    sudo docker exec -it dockerspark_master_1 /bin/bash
    cd /bin
    pyspark  
```
### Créer un RDD --Resilient Distributed Dataset : 
Pour créer un RDD en utilisant **sc** (SparkContext) et une méthode de lecture de contexte **texteFile** et passer en paramétre un ou plusier fichier texte dans mon cas je passe un seul fichier nommé gt.txt.

    mrdd=sc.textFile("/tmp/data/pg.txt")

  ![](https://github.com/hebabaze/pic/blob/master/rdd0.PNG)

### Appliquer des transformations au RDDs

**la transformation** est l'appel d'une méthode sur le RDD pour le stocker dans une autre variable, dans une autre instance de RDD et on a un autre type de méthode de type **action**
lorsqu'on appliquer une transformation rien ne passe t-il Spark fonctionne en mode lazy "traitement paresseux" .

**Exemple** : application d'une transformation (fonction distinct qui évite les doublons)

    mrdc=mrdd.distinct()
la fonction a créé un nouveau RDD

   ![](https://github.com/hebabaze/pic/blob/master/rdd1.PNG)

**Exemple** : application d'une action,Fonction count()
   
    mrdc.count()
Note : dans le cas des transformation Spark il garde en mémoire tout l'historique des transformations, et c'est au moment où je veux vraiment un résultat, c'est-à-dire une action qui produit un résultat, comme count. La transformation ne se produire physiquement que lorsque je demande une action . 

### sauvagarder un RDD :Persistance 
1. garder un RDD em mémoire :
   
   `mrdc.cache()`

 Aprés cette commande si j'applique une action sur RDD : mrdc , Spark ne sera pas besoin de régénérer la transformation de RDD
## Appliquer des Actions sur un RDD
* récupérer les données(afficher le contenu) : 
    mrdc.collect()
* Autre actions :

  ![](https://github.com/hebabaze/pic/blob/master/rdd2.PNG)
*Autre Transformation de type opération relationnelle :
  mrdc.union(mrdd).count()
  mrdc.intersection(mrdd).count
  mrdd.subtract(mrdc).count
  
## Lancer spark-shell , un interprétateur scala : 
1. à partir de la ligne de commande : 
    
    ```
    spark-shell
    ```
* Pour créer un RDD sous scala le paramétre val indique la creation d'un nouveau variable en scala 

 ![](https://github.com/hebabaze/pic/blob/master/scala-rdd.PNG)
* Pour quitter interprétateur scala :

  `:quit `

2. lancer l'interface web :
 au cours de  lancement de spark-shell je remarque que l'interface web est accessible à partir de http://localhost:4040
 mais pour s’accéder à partir de ma machine réel je dois vérifier l'adresse IP de mon container pour cela soit avec 
 `ip a` ou `ipconfig` ou `cat /etc/hosts` .. 
ensuite je tape dans le navigateur l'adresse suivante : 172.18.0.2:4040
  ![](https://github.com/hebabaze/pic/blob/master/scala%20web%201.PNG)

je peux aussi visualiser les jobs à partir de cette interface ,l'historique le performance de ces actions aussi avoir des informations sur les executor: master et worker

  ![](https://github.com/hebabaze/pic/blob/master/scala%20web%202.PNG)
