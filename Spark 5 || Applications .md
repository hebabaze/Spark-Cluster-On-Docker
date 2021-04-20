## Calculer des occurrences de mots:
> Note ==> le RDD :tr est déjà créer dans le chapitre précédent et on est dans le shell de pyspark
* **faltmap** : rendre une liste deux dimensions en un seul dimension 
* **map** : pour faire retourner chaque mot avec un clé 

   **`tr.flatMap(lambda x:x.split()).map(lambda x:(x,1)).take(4)`**
* Pour ajouter un filtre ,n'affiche que les mots qui contient Gutenberg par exemple : 
  
   **`  tr.flatMap(lambda x:x.split()).map(lambda x:(x,1)).filter(lambda x: 'Gutenberg' in x ).take(4)`**

![]( https://github.com/hebabaze/pic/blob/master/app0.PNG)
* **reduceByKey** : transformation réduire , c'est une méthode d'un RDD spécifique qui est un RDD de paire clé/valeur
    
**`tr.flatMap(lambda x:x.split()).map(lambda x:(x,1)).filter(lambda x: 'Gutenberg' in x ).reduceByKey(lambda a,b:a+b)`**

![](https://github.com/hebabaze/pic/blob/master/app01.PNG)

# Céeation des Variables de BroadCast(Global non modifiable):
 un objet de type Broadcast[Int] sera envoyé à tous les nœuds de traitement, une seule fois sera conservé, il est donc partagé, il est dupliqué sur chaque nœud de traitement, et il peut être réutilisé.c'est l'équivalent d'une constante de votre programme qui doit être accessible sur tous les nœuds.cette valeur ne peut pas être modifiée, ça, ça n'a pas de sens. 

              X=sc.broadcast(123)


# Création d'un Accumulateur (Global Modifiable):
l'accumulateur est un objet qui va être distribué également, qui va s'accumuler sur chaque machine, et ensuite qui sera regroupé et réduit directement par Spark. Pour créer cet accumulateur,

![](https://github.com/hebabaze/pic/blob/master/accu.PNG)

### Calculer le nombre des mots avec l'accumulateur : 
                      tr.flatMap(lambda line:line.split()).foreach(lambda x : acc.add(1))
![](https://github.com/hebabaze/pic/blob/master/acc1.PNG)
