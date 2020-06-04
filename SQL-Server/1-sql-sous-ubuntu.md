## Installation de SQL Server sous Ubuntu ##

1. Importer la clé publique GPG du dépôt

```
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

2. Enregistrer le dépôt Ubuntu de Microsoft SQL Server pour SQL Server 2019

```bash
sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
```

3. Exécuter les commandes suivantes pour installer le serveur SQL

```bash
sudo apt-get update
sudo apt-get install -y mssql-server
```

4. Une fois l'installation du paquet terminée, lancer mssql-conf setup et suivez les instructions pour définir le mot de passe SA et choisir votre édition

```bash
sudo /opt/mssql/bin/mssql-conf setup
```

5. Une fois la configuration effectuée, vérifiez que le service fonctionne

```bash

systemctl status mssql-server --no-pager
```

6. Si vous prévoyez de vous connecter à distance, vous devrez peut-être aussi ouvrir le port TCP du serveur SQL (par défaut 1433) sur votre pare-feu.

## Installer les outils en ligne de commande du serveur SQL##
Pour créer une base de données, vous devez vous connecter à un outil qui peut exécuter des instructions Transact-SQL sur le serveur SQL. Les étapes suivantes permettent d'installer les outils de ligne de commande du serveur SQL : sqlcmd et bcp.

1. Importer les clés GPG du dépôt public.

```bash
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

2. Enregistrez le dépôt Ubuntu de Microsoft

```
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
```

3. Mettez à jour la liste des sources et lancez la commande d'installation avec le paquet de développement unixODBC. Pour plus d'informations

```bash
sudo apt-get update
sudo apt-get install mssql-tools unixodbc-dev
```

## Se connecter localement ##

Les étapes suivantes utilisent **sqlcmd** pour se connecter localement à votre nouvelle instance de serveur SQL.
