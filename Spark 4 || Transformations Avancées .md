## Créer une transformation MapReduce :
Avant de commencer : 

 créer un RDD : `tr=sc.textFile("/tmp/data/antg.txt")`
### Transformation map:
**map** ça veut dire on envoie une fonction aux données. Une fonction de type « map » qui va traiter notre RDD, élément par élément, et retourner une liste d'éléments transformés. 
* **afficher la longueur de chaque ligne dans le  fichier** : 
   
   ```
   cnln=tr.map(lambda x:len(x))
   cnln.collect()
   cnln.take(8)
### Transformation reduce :
**reduce** : le RDD **cnln** contient toutes les longueurs, je voudrais avoir la longueur totale, le nombre de caractères finalement de tout mon RDD d'origine. Et donc je vais appliquer un reduce qui va retourner une valeur.
Je vais donc avoir une expression lambda qui prendre des paires et les additionner à chaque fois, en continuant à additionner avec la valeur suivante.
   ``` 
   cnln.reduce(lambda a,b:a+b) 
   ```
### Transformation mapreduce : 
on peut combiner les deux étapes dernieres en une seule instruction : 
   ``` 
   tr.map(lambda x:len(x)).reduce(lambda a,b:a+b) 
  ```
![](https://github.com/hebabaze/pic/blob/master/mpredc0.PNG)

### Transformation flatMap:
si on applique la foncttion split sur chaque Ligne de RDD on aura une table de deux dimension mais ,Grâce au FlatMap, je vais aplatir ces deux dimensions en une seule. Je vais me retrouver avec un RDD un seul RDD qui va contenir les mots. On a pris la deuxième dimension du tableau et puis on en a fait un tableau complet.

    `tr.flatMap(lambda line:line.split())`
    `tr.flatMap(lambda line:line.split()).take(5)`
Pour connaitre le nombre de mots :    **`tr.flatMap(lambda line:line.split()).count()`**
Aussi , nombre de mots distincts :    **`tr.flatMap(lambda line:line.split()).distinct().count()`**   
     
