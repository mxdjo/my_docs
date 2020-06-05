# SQL Server #

SQL Server est un SGBD (Sytème de Gestion de Base de Données) qui permet de gérer plusieurs bases de données relationnelles. En soit SQL Server n'est donc pas une base de données mais un logiciel permettant le stockage des données de façon cohérente et organisée. Il contient donc plusieurs base de données.
Il fonctionne sous les OS Windows et Linux (depuis mars 2016), mais il est possible de le lancer sur Mac OS via Docker

## Composants de SQL Server ##

MS SQL Server est composé de plusieurs logiciels qui s'exécutent sous forme de services ou possèdent des interfaces graphiques ou accessible via une ligne de commande. MS SQL Server est composé de 5 principaux services à savoir:

* SQL SERVER :Le moteur relationnel (OLTP).
 C'est le service moteur de base données et correspond à une instance SQL Server. Ce composant s'exécute en tant service Windows et est référencé sous le nom MSSQLSERVER pour l'instance par défaut et MSSQLSERVER$nomInstance pour une instance nommée. Le nom d'une instance est défini lors de l'installation d'une nouvelle instance.

* SSIS (Sql Server Integration Service) :Un ETL (Extract Transform and Load). C'est l'outil SQL Server d'Import/Export , de transfert et de transformation de données. Il intègre des assistants pour la création d'ETL(Extraction Transformation Loading).

* SSAS(Sql Server Analysis Service) : Le moteur décisionnel (OLAP).
C'est le composant idéal pour les projets décisionnels. Ce composant est un outil d'analyse OLAP et de Data Mining de Microsoft et permet de construire des cube OLAP.

* SSRS (Sql Server Reporting Service) :Un outil de génération d'état .
C'est grâce à ce composant que nous pouvons restituer nos données provenant de notre entrepôt de données sous forme de rapports(tableau,graphique etc...), dashboard, sur divers support et facilement comprehensives par des personnes tiers Ce composant permet également de créer des rapports de type interactif,tabulaire, graphique à partir des sources de données XML, relationnelles ou multidimensionnelles

* Agent SQL : système de planification de travaux et de gestion d'alerte.
En charge de la surveillance de SQL Serve,ce composant gère également l'execution des tâches planifiées et le suivi des alertes. Il s'exécute en tant service Windows et est directement lié à une instance SQL Server. Il est référencé par défaut dans le gestionnaire de service Windows sous le nom SQL Server Agent et par SQL Server Agent(nom instance) dans le cas d'une instance nommée.

## Differentes editions de SQL Server ##

Les différentes éditions de SQL server sont:

* Entreprise: Pour les datacenter, la virtualisation
* Standard: On premise avec des ressources minimales
* Web: idéal pour les hébergements Web
* Developer: pour ceux qui construisent et testent les applications.
* Express

Après installation de SQL Server 2019 Express, on nous donne:

* le nom d'instance: SQLEXPRESS
* Administrateur SQL: WIN-V3RJBOLK514\Administrateur
* Fonctionnalités installées: SQLENGINE
* Version: 15.0.2000.5
* Chaine de connexion: Server=localhost\SQLEXPRESS;Database=master;Trusted_Connection=true

### Fichiers (extensions) ###

Les bases de données sont contenues physiquement dans des fichiers. Les fichiers portent généralement les extensions :

* MDF (Main Database File) pour le premier fichier de données, comportant certaines pages techniques vitales
* NDF (Next Database File) pour les autres fichiers de données
* LDF (Log Database File) pour les fichiers du journal de transaction

Après l'iavoir installé, on nous demande soit:

* Se connecter maintenant
* Personnaliser
* Installer SSMS (SQL Server Management Studio)

### Langage utilisé ###

Pour les requêtes, SQL Server utilise le langage SQL dans un des dialectes les plus conformes à la norme SQL, Microsoft mettant un point d'honneur à corriger de version en version quelques errements du passé hérité du moteur Sybase. Le dialecte utilisé est le T-SQL (Transact-SQL), une implémentation de SQL qui prend en charge les procédures stockées, les fonctions utilisateurs ou UDF (User Defined Function) et les déclencheurs (trigger). Les langages XQuery et XPath sont utilisés à différents niveaux pour manipuler les données XML au sein même des requêtes SQL.

#### Les bases du Transact SQL ####

Pour créer et gérer nos BDD, il nous faut évidemment SQL server (peu importe l'édition).
Les déclarations Transact-SQL peuvent être rédigées et soumises au moteur de base de données de la manière suivante :

* SQL Server Management Studio

##### Créer et interroger des objets dans la BDD #####

###### CREATE DATABASE ######

Comme beaucoup d'instructions Transact-SQL, l'instruction CREATE DATABASE a un paramètre obligatoire : le nom de la base de données. CREATE DATABASE a également de nombreux paramètres optionnels, tels que l'emplacement du disque où vous voulez placer les fichiers de la base de données. Lorsque vous exécutez CREATE DATABASE sans les paramètres optionnels, le serveur SQL utilise des valeurs par défaut pour un grand nombre de ces paramètres.

```SQL
CREATE DATABASE TestData  
GO  
```

Le mot-clé GO permet de séparer les déclarations lorsque plusieurs déclarations sont présentées dans un même lot. GO est facultatif lorsque le lot ne contient qu'une seule déclaration.

##### CREATE TABLE #####

```SQL
USE TestData  
GO  
```

Dans une fenêtre de l'éditeur de requêtes, tapez et exécutez le code suivant pour créer une **table** nommé Products. Les **colonnes** du tableau sont nommées ProductID, ProductName, Price et ProductDescription. La colonne ProductID est la clé primaire de la table. int, varchar(25), money et varchar(max) sont tous des types de données. Seules les colonnes Price et ProductionDescription ne peuvent pas contenir de données lorsqu'une ligne est insérée ou modifiée. Cette déclaration contient un élément optionnel (dbo.) appelé schéma. Le schéma est l'objet de la base de données qui possède la table. Si vous êtes un administrateur, dbo est le schéma par défaut. dbo signifie propriétaire de la base de données.

```SQL
CREATE TABLE dbo.Products  
   (ProductID int PRIMARY KEY NOT NULL,  
   ProductName varchar(25) NOT NULL,  
   Price money NULL,  
   ProductDescription varchar(max) NULL)  
GO  
```

###### INSERT AND UPDATE ######

```SQL
-- Standard syntax  
INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
    VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
GO
```

Si l'insertion a réussi,on peut passer aux autres etapes.Cependant si l'insertion échoue, on doit refaire l'action précédente *après suppression des colonnes insérés*.
Pour supprimer les colonnes, on utilise TRUNCATE

```SQL
TRUNCATE TABLE TestData.dbo.Products;
GO
```

###### READ DATA IN A TABLE ######

```SQL
-- The basic syntax for reading data from a single table  
SELECT ProductID, ProductName, Price, ProductDescription  
    FROM dbo.Products  
GO  
```

Nous pouvons utiliser un astérisque (*) pour sélectionner toutes les colonnes du tableau. L'astérisque est utilisé pour les requêtes ad hoc. En code permanent, fournissez la liste des colonnes de sorte que l'état renvoie les colonnes prévues, même si une nouvelle colonne est ajoutée au tableau ultérieurement.

```SQL
-- Returns all columns in the table  
-- Does not use the optional schema, dbo  
SELECT * FROM Products  
GO
```

##### Configurer les permissions sur une BDD #####

###### Créer un login ######

Pour accéder au moteur de base de données, les utilisateurs ont besoin d'un login. La connexion peut représenter l'identité de l'utilisateur en tant que compte Windows ou en tant que membre d'un groupe Windows, ou la connexion peut être une connexion SQL Server qui n'existe que dans SQL Server. Dans la mesure du possible, vous devez utiliser l'authentification Windows.

Par défaut, les administrateurs de votre ordinateur ont un accès complet au serveur SQL. Pour cette leçon, nous voulons avoir un utilisateur moins privilégié ; par conséquent, vous allez créer un nouveau compte d'authentification Windows local sur votre ordinateur. Pour ce faire, vous devez être un administrateur sur votre ordinateur. Ensuite, vous accorderez à ce nouvel utilisateur un accès au serveur SQL.

Créer un nouveau compte Windows:

* Cliquez sur **Démarrer**, cliquez sur **Exécuter**, dans la case Ouvrir, tapez **%SystemRoot%\system32\compmgmt.msc /s**, puis cliquez sur OK pour ouvrir le programme de gestion de l'ordinateur.

* Sous Outils système, développez Utilisateurs et groupes locaux, cliquez avec le bouton droit de la souris sur Utilisateurs, puis cliquez sur Nouvel utilisateur.

* Dans la zone Nom de l'utilisateur, tapez Mary.
Dans la zone Mot de passe et Confirmer le mot de passe, tapez un mot de passe fort, puis cliquez sur Créer pour créer un nouvel utilisateur Windows local.

###### Créer le login SQL #######

Dans une fenêtre de l'éditeur de requêtes de SQL Server Management Studio, tapez et exécutez le code précédent en remplaçant computer_name par le nom de votre ordinateur. FROM WINDOWS indique que Windows va authentifier l'utilisateur. L'argument optionnel DEFAULT_DATABASE connecte Mary à la base de données TestData, à moins que sa chaîne de connexion n'indique une autre base de données. Cette déclaration introduit le point-virgule comme terminaison optionnelle pour une déclaration Transact-SQL.

```SQL
CREATE LOGIN [computer_name\Mary]  
    FROM WINDOWS  
    WITH DEFAULT_DATABASE = [TestData];  
GO  
```

Cela autorise un nom d'utilisateur Mary, authentifié par votre ordinateur, à accéder à cette instance de SQL Server. S'il y a plus d'une instance de SQL Server sur l'ordinateur, vous devez créer le login sur chaque instance à laquelle Marie doit accéder

###### GRANT ACCESS à la BDD #######

Mary a maintenant accès à cette instance de SQL Server, mais n'a pas la permission d'accéder aux bases de données. Elle n'a même pas accès à sa base de données par défaut, TestData, tant que vous ne l'autorisez pas en tant qu'utilisateur de la base de données.

Pour accorder l'accès à Mary, passez à la base de données TestData, puis utilisez l'instruction CREATE USER pour associer sa connexion à un utilisateur nommé Mary.

```SQL
USE [TestData];  
GO  

CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
GO

```

Maintenant, Mary a accès à la fois au serveur SQL et à la base de données TestData.
