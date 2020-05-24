Nous allons voir ici certains mots-clé dans la programmation en Java

### Package ###
Un package ressemble à la structure des dossiers de votre ordinateur. Il organise les différents fichiers de votre programme. Un nom de package doit être unique car il existe des millions d'autres programmes et vous ne voulez pas avoir le même nom de fichier de programme que quelqu'un d'autre. Le code Java étant fortement partagé, les packages sont utilisés pour éviter les conflits de noms. Si deux fichiers de code différents dans un programme ont le même nom, y compris le nom de leur package, un seul d'entre eux sera chargé et l'autre fichier de code sera complètement ignoré, ce qui entraînera généralement des erreurs.    

Pour garantir qu’un package est unique, il est courant d’inclure son nom de domaine dans le package. Habituellement, le dossier supérieur ou racine d'une structure de package est le nom de domaine de l'organisation dans l'ordre inverse. L'utilisation d'un nom de package n'est jamais requise, mais elle est fortement recommandée, même dans les programmes les plus élémentaires. Lorsque vous déclarez un package, vous devez le déclarer dans la première ligne de votre programme. Les noms minuscules et singuliers sont couramment utilisés pour chaque partie du nom de votre package. Dans mon exemple, je commence le nom du package avec mon domaine de premier niveau, com, suivi de mon nom de domaine, marcusbiel, puis java8course, car c'est le projet sur lequel nous travaillons.  
Comme je l'ai dit plus tôt, l'exemple de code de cet article est lié à un garage, donc nous terminerons le nom du package par «garage». Notre nom complet de package sera donc:

```
package com.marcusbiel.javacourse.lesson1
```

Dans la mesure du possible, utilisez des termes que le client peut comprendre et qui se rapportent à l'entreprise (garage dans mon cas) plutôt que des termes techniques comme «frontend» ou «backend».

### import ###
Pour simplifier les programmes et réduire la redondance, de nombreux fichiers de programme réutilisent le code existant. Pour ce faire, vous pouvez utiliser le nom complet du fichier de code, y compris le nom complet de son package. Cependant, pour rendre votre code plus lisible, vous ajouterez généralement le fichier à la liste des importations, ce qui vous permettra d'adresser le code par son nom de fichier simple, sans avoir à le référencer constamment par son emplacement complet de package.

L'instruction ou les instructions d'importation sont écrites directement après la déclaration de package. Lorsque vous importez du code, vous incluez le nom de package du fichier. Vous pouvez importer des fichiers spécifiques à partir du package, ou du package entier, en utilisant un symbole étoile.
Commençons notre code en important la première voiture dans notre garage, une Bmw.    
```
package com.marcusbiel.lesson1.garage

import.com.marcusbiel.lesson1.car.Bmw
```   

## Class ##
Les programmes peuvent facilement comprendre des milliers, voire des dizaines de milliers de lignes de code. Lorsque vous avez autant de texte au même endroit, il est facile de se perdre. Pour rendre le code plus clair, les programmeurs Java classent leur code en différentes unités, appelées classes.

En tant que programmeur, vous êtes libre de nommer vos packages et vos classes comme bon vous semble, mais votre objectif doit toujours être clair. Lorsque vous travaillez avec un client commercial, le client définit ce qu'il veut; c'est votre travail de savoir comment l'exprimer. Si vous pouvez créer un langage commun pour combler l'écart entre les deux, il sera plus facile pour votre client de comprendre le code sans beaucoup de connaissances en codage. Pour cette raison, les programmeurs ont tendance à nommer leurs classes en utilisant un nom qui décrit la classe, en commençant par une majuscule.

Par exemple, nous pourrions créer une classe Car, qui contiendra plus tard tout le code lié à une voiture (exemple 2). Au début d'une classe, il y a une accolade ouvrante et à la fin de notre code il y a une accolade fermante qui montre la fin de la classe.
Les cours ne devraient être axés que sur un seul sujet, et vous devriez essayer de les rendre aussi petits que possible pour des raisons de lisibilité et de maintenabilité.   

```
class Car {

}
```
### Method ###
Une classe comprendra une ou plusieurs méthodes. Une méthode définit comment une certaine tâche sera effectuée à l'aide de code. Par exemple, une méthode timesTwo pourrait doubler la quantité d'une entrée donnée. Les méthodes sont aussi parfois appelées fonctions. Bien que ce terme ne soit pas totalement correct d'un point de vue académique, vous pouvez l'utiliser. Par convention, une méthode est généralement nommée d'après un verbe qui décrit les actions qu'elle effectue. Les méthodes peuvent fonctionner sur n'importe quoi: nombres, couleurs, sons - vous l'appelez.  

```
timesTwo(2) => 4
add("ab", "c") => "abc"
print("Hello") => will print "Hello"
```

Imaginez votre code comme un livre. Un livre contient des chapitres (les packages), des paragraphes (classes) et des phrases (méthodes). Les méthodes peuvent également appeler d'autres méthodes, créant une chaîne de méthodes. En tant que programmeur, vous voulez structurer votre code en pensant au niveau d'abstraction actuel, tout comme écrire un livre. Votre code devrait finir par être lisible comme un livre!

Un exemple de méthode appelant d'autres méthodes serait une méthode "prepareDinner ()" appelant en interne une méthode "prepareAppetizer ()", suivie par une méthode appelée "prepareMainCourse ()", suivie d'une méthode appelée "prepareDessert ()".

Si notre méthode prepareAppetizer () doit alors appeler trois autres méthodes, "washLettuce ()", "addTomatoes ()" et "tossSalad ()", nous avons créé une hiérarchie lisible et compréhensible dans notre code. Nous pourrions, bien sûr, avoir prepareDinner () appeler directement ces trois méthodes, au lieu de prepareAppetizer (), mais cela encombrerait notre code et le rendrait difficile à lire.    
Il est important de trouver une structure propre et de faire parler votre code. Plus il est difficile de comprendre ce que fait votre programme, plus il sera facile d'introduire une erreur. En règle générale, essayez de limiter vos méthodes à moins de vingt lignes. Personnellement, je vise une longueur de méthode de seulement 1 à 3 lignes.
Les méthodes sont définies de la même manière que les classes. Vous définissez d'abord le nom de la méthode, généralement un verbe commençant par une lettre minuscule. Les méthodes sont normalement des verbes parce qu'elles font quelque chose. Les classes sont généralement des noms parce qu'elles sont les objets sur lesquels les méthodes agissent. Le nom de la méthode est suivi d'une paire de parenthèses. À l'intérieur de ces parenthèses, vous pouvez définir un nombre de champs de saisie allant de zéro à un nombre illimité. Lorsque vous appelez une méthode, vous devez envoyer des valeurs spécifiques, appelées arguments, aux champs spécifiques, appelés paramètres de la méthode. Les arguments sont les valeurs réelles que vous envoyez à la méthode. Dans le contexte de la méthode, les valeurs générales qu'elle recevra sont appelées paramètres de méthode. Je recommande un maximum absolu de trois à cinq paramètres de méthode, car plus que cela nuit à la lisibilité. Moins il y a de paramètres, mieux c'est. Après vos paramètres, vous commencez votre définition de méthode par une accolade ouvrante et la terminez par une accolade fermante. Entre les deux, vous mettez le code de votre méthode. Revenons à notre classe de voiture :

```
package com.marcusbiel.java8course.garage;
 
import com.marcusbiel.java8course.car.Bmw;

class Car {

     drive(speed) {

     }
}
``` 

### Object ###
Comme je l'ai déjà dit, une classe est utilisée pour structurer le code en Java sous la forme d'unités de code. Cependant, ce n'est qu'une partie de l'histoire. Une classe est comme un plan de ce que vous voulez faire lorsque le programme est en cours d'exécution. La classe Voiture définit comment une voiture se comportera. Cependant, au moment de l'exécution (lorsque le programme est en cours d'exécution), il y aura un certain nombre de voitures, chacune ayant son propre ensemble de valeurs.

Une classe ne sert donc que de modèle pour les objets qui sont créés dans votre programme. Chaque objet a le même ensemble de comportements, tel que défini par la classe, mais il existe aussi comme son propre ensemble de valeurs dans le programme qui pourrait changer au fur et à mesure de l'exécution du programme. Par exemple, vous pouvez avoir deux objets de la classe Voiture qui conduisent tous les deux, mais ils peuvent avoir des valeurs différentes pour leurs vitesses respectives.   

### Point ###

En Java, un "." n'est pas utilisé pour indiquer la fin d'une phrase. Au lieu de cela, un "." est utilisé par une variable pour exécuter ou appeler une méthode. Par exemple, nous pourrions avoir une variable car appeler la méthode drive ().

### Point virgule ###

Depuis le "." est utilisé pour indiquer une méthode appelée, le «;» est utilisé pour indiquer la fin d'une commande, d'une instruction ou d'une déclaration.    

Avant de pouvoir utiliser une variable, nous devons la définir. Vous déclarez une variable en écrivant le type de la variable, suivi de son nom, suivi d'un «;».    

### Allocation d'objets ###

Une fois que vous avez déclaré une variable, vous pouvez l’allouer à un objet spécifique. Vous pouvez également effectuer ces deux opérations sur une seule ligne. Tout d'abord, vous pouvez créer une variable de type Car, appelée myPorsche, puis, à l'aide d'un signe égal, l'affecter à un nouvel objet Car, avec une première valeur de 1 et une deuxième valeur de 320.    

```
Car myPorsche = new Car(1, 320);
```

Après avoir déclaré la variable et l'avoir affectée à l'objet, chaque fois que nous utilisons myPorsche, nous référençons cet objet créé dans la mémoire. Vous remarquerez peut-être aussi que nous avons mis deux valeurs dans le constructeur de Car, mais sans regarder réellement le constructeur de Car, nous ne saurions pas ce qu'elles signifient. C'est l'une des raisons pour lesquelles il faut avoir le moins de champs possibles dans les méthodes et les constructeurs.    

### Public ###

public est un modificateur d'accès qui définit que la classe ou la méthode marquée comme public peut être utilisée par n'importe quelle autre classe à partir de n'importe quel autre package. Outre public, il existe également d'autres modificateurs d'accès tels que privé, par défaut et protégé, que je couvrirai plus en détail plus tard.
