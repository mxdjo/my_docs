Le but d'un programme est de faire quelque chose avec des données ou, en d'autres termes, avec les choses que vous mettez dans votre programme. Souvent, votre programme utilisera une ou plusieurs variables pour manipuler les données.   
une variable peut être vue comme une boîte qui contient une valeur. Cette boîte est stockée sur une étagère dans un entrepôt gigantesque. L'emplacement de chaque boîte de cet entrepôt est soigneusement enregistré, tout comme votre ordinateur enregistre l'emplacement de votre variable en mémoire.   
Pour savoir à quoi sert chaque boîte, vous devez les étiqueter. Avec la programmation, c'est la même chose : vous attribuez un nom à votre variable.

Le nom d'une variable doit refléter la signification de son contenu, comme des étiquettes sur une boîte.     
   * utilisez des noms descriptifs tout au long de votre code.
   * Ça risque d'être un peu long ! Cependant, les noms descriptifs sont bien pratiques à long terme pour vous et pour votre équipe, car ils offrent une meilleure lisibilité et facilitent ainsi la compréhension du code pour les autres développeurs. Par exemple, si vous voulez stocker des cookies sans sucres, l'utilisation d'un nom descriptif comme  cookiesSansSucres  est bien plus précis que, disons,  cookies  ou  cookiesSains.

   * Soyez complet.
    Évitez si possible d'abréger ou de raccourcir les mots, même si une version plus courte semble évidente. Par exemple,  chiffreDAffairesAnnuel  est préférable à  chifAfAnn.

    * Suivez une convention d'appellation commune.
    L'une des conventions d'appellation les plus populaires est le Camel Case : une phrase composée de plusieurs mots sans espaces ni ponctuation. Le premier mot est écrit en minuscules et tous les autres mots commencent par une majuscule. Par exemple,  monBudget.


### Declarer une variable ###

En Java, il faut toujours déclarer une variable avant de pouvoir l'utiliser.   
Pour la déclarer, il faut commmencer par le type, puis le nom, et enfin la valeur.Si vous n'avez pas de valeur à assigner à la variable au moment de la déclaration, vous devez quand même utiliser le mot clé definissant le type.Par exemple, si vous voulez compter des mots dans une phrase, mais que vous ne savez pas encore de quelle phrase il s'agit, indiquez le type et déclarez la variable pour une utilisation future. Cependant, lorsque vous déclarez une variable en spécifiant uniquement son type, celle-ci ne peut pas être utilisée tant qu'on ne lui a pas attribué une valeur. En programmation, il est souvent nécessaire de déclarer une variable en sachant que vous lui attribuerez une valeur plus tard.     

*Si je ne peux pas utiliser une variable sans valeur, pourquoi donc j'ai besoin de spécifier le type ? Pourquoi pas uniquement la valeur ? 🧐*      
Pendant l'exécution d'un programme, votre CPU (unité centrale de traitement) a besoin de savoir combien d'espace réserver à votre variable. Utiliser un type pour déclarer une variable permet à votre CPU de lui allouer un espace mémoire adapté.   

### Les types numériques ###

Les types numériques sont :

   * les nombres entiers, comme les nombres que vous utilisez pour compter (1, 2, 3) ;

    * les nombres décimaux, que vous pouvez utiliser pour stocker les valeurs monétaires (2,50 ou 5,99 par exemple).     

#### Les entiers ####
Les entiers sont déclarés comme n'importe quelle autre variable, avec un type, puis un nom, puis, si vous l'avez, une valeur :

```
int count = 10;
```

#### Les décimales #### 
Pour les décimales, Java utilise deux types différents:
* float
* double

*Pour une précision jusqu'à 7 décimales après la virgule, vous pouvez utiliser  float.  Au-delà, ce sera  double.*
Ces types sont déclarés de la façon suivante:  

```
float length = 1876.79;
double width = 1876.79797657;
```
Ces deux types ont le même but. La différence est que  double  est deux fois plus précis que  float, ce qui signifie qu'il propose plus de décimales d'un nombre après la virgules.    


#### Mélangez des types numériques ####

Dans vos programmes, vous pouvez être amené à faire des opérations mathématiques. Cependant, les variables utilisées ne seront pas forcément de même type (tant qu'elles restent des valeurs numériques). C'est pourquoi  il est important de garder à l'esprit la façon dont les types se mélangent et les conséquences que cela peut avoir.  
Passons en revue quelques exemples dans Java:   
```
int a = 10;
int b = 4;
int c = a/b;
```
Devinez quel sera le résultat de la division ?   
Eh bien, c'est  2  – pas forcément ce à quoi on s'attendait, n'est-ce pas ?
Cela est dû au fait que les variables  a  et  b  se sont vu assigner des nombres entiers (int). Ainsi, l'opération de division ne peut fournir qu'un nombre entier comme réponse.    

Mais que se passera-t-il avec le code ci-dessous ?
```
int a = 10;
int b = 4;
double c = a/b;
```

Zut...Cela ne fonctionne toujours pas. 😫

Pour obtenir un résultat avec des décimaux, il va falloir combiner deux types.
```
int a = 10;

double b = 4;

int c = a/b;
```
Vous voyez comment la variable  a  été déclarée avec  int  et la variable  b  avec  double ?

Dans cet exemple, le résultat de l'expression  a/b  sera bien un nombre décimal,  2,5.

Cependant,  c  est déclaré comme un  int  et ne peut pas se voir attribuer une valeur décimale. Cette affectation n'est pas possible !

Vous pouvez faire en sorte qu'une variable d'un type agisse comme un autre type. C'est ce qu'on appelle le type casting (ou la conversion d'une valeur dans un autre type). Pour résoudre le problème que nous avons eu dans le dernier exemple, faites croire à la variable  b  que c'est un entier en l'assignant à  c  comme ci-dessous :
```
int a = 10;

double b = 4;

int c = a/ (int) b; //-> c contient 2, car a /(int) b est une division entière
```
Vous voyez comment nous avons fait pour que la variable  b  agisse comme un nombre entier ? Vous pouvez aussi faire en sorte qu’une variable entière  b fasse comme si sa valeur était  double  :
```
int a = 10;

int b = 4;

double c = a/(double) b; //-> c contient 2.5, car la valeur de b est transformée en double
```

Convertir une variable en  double  vous permet d'effectuer une division en virgule flottante, même si vous utilisez des variables avec un type entier  int.


#### Découvrez les chaînes de caractères (strings) ####

Passons maintenant à un type plus complexe, les strings. Les strings (ou chaînes de caractères) permettent de stocker du texte, ou en d'autres termes, un ensemble de caractères. Voici comment déclarer une variable string dans Java :
```
String city = "New York";

String movie = "Best ever";

String pet;

String emptyString = "";
```
Vous pouvez fusionner une ou plusieurs d'entre elles. Rassemblons quelques  strings  :

```
String firstFavoriteCity = "New York";

String secondFavoriteCity = "Buenos Aires";

String favorites = firstFavoriteCity + secondFavoriteCity; // -> "New YorkBuenos Aires"
```

 Mais, il n'y a pas d'espace entre les deux. C'est bizarre, non ?

Rendons ce code plus lisible en concaténant, c'est-à-dire en mettant bout à bout des chaînes de caractères et des variables :
```
String firstFavoriteCity = "New York"

String secondFavoriteCity = "Buenos Aires"


String favorites = "My favorite cities are " +firstFavoriteCity+ " and "+secondFavoriteCity; // -> "My favorite cities are New York and Buenos Aires"
```

C'est beaucoup mieux maintenant ! Vous pouvez également concaténer d'autres types de données avec des chaînes de caractères, telles que des nombres.

Ah oui ? Mais comment je procède ?
```
String favoriteCity = "Buenos Aires";

int numberOfTrips = 5;


String story = "I've traveled to " +favoriteCity+ " " +numberOfTrips+ " times!"; // -> "I've traveled to Buenos Aires 5 times!"
```
Juste avant, nous avons utilisé l'opérateur  +  pour ajouter deux nombres. Ici, avec des chaînes de caractères, l'opérateur  +  peut être utilisé pour concaténer des chaînes et des nombres entiers. La concaténation fait référence à l'assemblage de chaînes de caractères ou de nombres, et de chaînes de caractères


Sources: https://openclassrooms.com/fr/courses/6173501-debutez-la-programmation-avec-java/6313896-utilisez-les-variables-en-programmation
