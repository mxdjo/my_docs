## SQL Server ##

SQL Server est un SGBD (Sytème de Gestion de Base de Données) qui permet de gérer plusieurs bases de données relationnelles. En soit SQL Server n'est donc pas une base de données mais un logiciel permettant le stockage des données de façon cohérente et organisée. Il contient donc plusieurs base de données.
Il fonctionne sous les OS Windows et Linux (depuis mars 2016), mais il est possible de le lancer sur Mac OS via Docker

### Composants de SQL Server ###

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

### Langage utilisé ###

Pour les requêtes, SQL Server utilise le langage SQL dans un des dialectes les plus conformes à la norme SQL, Microsoft mettant un point d'honneur à corriger de version en version quelques errements du passé hérité du moteur Sybase. Le dialecte utilisé est le T-SQL (Transact-SQL), une implémentation de SQL qui prend en charge les procédures stockées, les fonctions utilisateurs ou UDF (User Defined Function) et les déclencheurs (trigger). Les langages XQuery et XPath sont utilisés à différents niveaux pour manipuler les données XML au sein même des requêtes SQL. 

### Differentes editions de SQL Server ###

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