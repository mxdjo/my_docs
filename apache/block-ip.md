On souhaite bloquer les utilisateurs de certains pays ( en se basant sur leurs IP).   
Cela sera possible grâce à GeoIP.  
GeoIP permet de trouver le pays d'une adresse IP ou d'un hostname.   




## Debian/Ubuntu ##

###Installation des paquets ###

```
sudo apt install geoip-bin libapache2-mod-geoip libgeoip1
```

### Activation de GeoIP dans la configuration de Apache ####

Pour activer le module, il faut utiliser l'outil a2enmod
```
sudo a2enmod geoip
```
La configuration du module est dans le fichier _/etc/apache2/mods-available/geoip.conf_. Nous allons le modifier

```
 <IfModule mod_geoip.c>
   GeoIPEnable On
   #GeoIPDBFile /usr/share/GeoIP/GeoIP.dat
 </IfModule>
```

Ensuite, on y insère le block Directory ( voir utilité de Directory)

```
<IfModule mod_geoip.c>
GeoIPEnable On
GeoIPDBFile /usr/share/GeoIP/GeoIP.dat


<Directory />
SetEnvIf GEOIP_COUNTRY_CODE AN BlockCountry
SetEnvIf GEOIP_COUNTRY_CODE BL BlockCountry
SetEnvIf GEOIP_COUNTRY_CODE CN BlockCountry

# ajouter les pays ici selon le code
# La liste des codes pays est disponible sur le site de Geo IP

Deny from env=BlockCountry
</Directory>

</IfModule>


```

Telecharger GeoIP.dat et le mettre dans son dossier  
```
wget https://mirrors-cdn.liferay.com/geolite.maxmind.com/download/geoip/database/GeoIP.dat.gz
```
```
gzip GeoIp.dat.gz
```
```
mv GeoIP.dat /usr/share/GeoIP
```
## CentOS ##

### Installation des paquets ####

```
yum install epel-release
```
```
yum install GeoIP GeoIP-GeoLite-data geoipupdate mod_geoip
```
Cela installe la bibliothèque GeoIP, la base de données GeoIP, le module Apache GeoIP et le script de mise à jour de GeoIP. 

### Activation de GeoIP dans la configuration de Apache ###

La configuration du module est dans le fichier _/etc/httpd/conf.d/geoip.conf_. Nous allons le modifier

```
 <IfModule mod_geoip.c>
   GeoIPEnable On
   #GeoIPDBFile /usr/share/GeoIP/GeoIP.dat
 </IfModule>
```

Ensuite, on y insère le block Directory ( voir utilité de Directory)

```
<IfModule mod_geoip.c>
GeoIPEnable On
GeoIPDBFile /usr/share/GeoIP/GeoIP.dat


<Directory />
SetEnvIf GEOIP_COUNTRY_CODE AN BlockCountry
SetEnvIf GEOIP_COUNTRY_CODE BL BlockCountry
SetEnvIf GEOIP_COUNTRY_CODE CN BlockCountry

# ajouter les pays ici selon le code
# La liste des codes pays est disponible sur le site de Geo IP

Deny from env=BlockCountry
</Directory>
</IfModule mod_geoip.c>
```
NB: Pour des raisons de performance, il faut activer GeoIP dans un block <Directory> ou un block <Location>    

https://www.cloudibee.com/geoip-based-country-blocking-for-apache/

**Il faut aussi voir la possibilité de bloquer un ASN et une plage d'IP**


## !!! Maxminddb ####
Utiliser mod_maxminddb au lieu de mod_geoip (en cours de test)


### La base de données GeoIP ###

Il faut déja installer geoipupdate 
https://github.com/maxmind/geoipupdate/releases   

Il faut bien noter la version installé car elle nous sera utile pour générer une clé de licence.  

Ensuite, on crée un compte sur https://www.maxmind.com/en/geolite2/  
Après création, nous recevons un lien dans notre boite mail pour définir le mot de passe de notre compte MaxMind.

Une fois reconnecté, on configure le fichier GeoIp.conf ( normalement dans /etc ).  
On devra remplacer les champs AccountID, LicenseKey et EditionIDs par les valeurs qui nous ont été attribuées.  

```
# `AccountID` is from your MaxMind account.
AccountID MON_SUPER_ID

# Replace YOUR_LICENSE_KEY_HERE with an active license key associated 
# with your MaxMind account.
LicenseKey YOUR_LICENSE_KEY_HERE

# `EditionIDs` is from your MaxMind account.
EditionIDs GeoLite2-ASN GeoLite2-City GeoLite2-Country

```
Une fois effectuée, il faut lancer la commande geoipupdate   
Les fichiers créés sont d'extensions mmdb   
Pour faire des requetes sur ces fichiers, il faut installer le module mod_maxminddb qui utilise la bibliotheque libmaxminddb.

### Le module mod_maxminddb ###


#### Installation du module mod_maxminddb ####

sudo apt install libmaxminddb0 libmaxminddb-dev mmdb-bin

Si cela ne marche,il faut ajouter le repo et refaire:
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:maxmind/ppa
sudo apt update
sudo apt install libmaxminddb0 libmaxminddb-dev mmdb-bin apache2-dev


### COnfiguration Apache pour utiliser le module ###

Après avoir installé ce module et obtenu une base de données, nous devons maintenant configurer le module dans notre fichier de configuration Apache (par exemple, /etc/apache2/apache2.conf) ou dans un fichier .htaccess. Vous devez définir MaxMindDBEnable pour activer le module, MaxMindDBFile pour spécifier la base de données à utiliser et MaxMindDBEnv pour lier le résultat de recherche souhaité à une variable d'environnement. Vous pouvez également activer MaxMindDBSetNotes si vous souhaitez que les variables d'environnement soient également définies en tant que notes Apache.  

Toutes les directives peuvent apparaître dans la configuration de notre serveur ou dans un fichier .htaccess. Les directives dans les blocs <Location> et <Directory> s'appliqueront également aux sous-emplacements et sous-répertoires. La configuration sera fusionnée avec la priorité la plus spécifique. Par exemple, une directive conflictuelle définie pour un sous-répertoire sera utilisée pour le sous-répertoire plutôt que la directive définie pour l'emplacement parent.

De même, la configuration du serveur principal peut définir des valeurs par défaut qui seront fusionnées dans la configuration fournie par les hôtes virtuels individuels. Cependant, veuillez noter qu'actuellement aucune fusion de configuration n'est effectuée entre les configurations serveur/vhost et répertoire.   
Les directives sont les suivantes:
* MaxMindDBEnable : Cette directive active ou désactive la recherche de base de données MaxMind. Les paramètres valides sont On et Off.
```
MaxMindDBEnable On
```
* MaxMindDBFile: Cette directive associe un espace réservé de nom à un fichier DB MaxMind sur le disque. Vous pouvez spécifier plusieurs bases de données, chacune avec son propre  *
```
MaxMindDBFile COUNTRY_DB /usr/local/share/GeoIP/GeoLite2-Country.mmdb
MaxMindDBFile CITY_DB    /usr/local/share/GeoIP/GeoLite2-City.mmdb
```
* MaxMindDBEnv: Cette directive affecte le résultat de la recherche à une variable d'environnement. Le premier paramètre après la directive est la variable d'environnement. Le deuxième paramètre est le nom de la base de données suivi du chemin d'accès aux données souhaitées à l'aide de clés de mappage ou d'index de tableaux basés sur 0 séparés par /.
```
MaxMindDBEnv COUNTRY_CODE COUNTRY_DB/country/iso_code
MaxMindDBEnv REGION_CODE  CITY_DB/subdivisions/0/iso_code
```
##### Exemples données dans la documentation #####

**ASN Database**

```
<IfModule mod_maxminddb.c>
    MaxMindDBEnable On
    MaxMindDBFile ASN_DB /usr/local/share/GeoIP/GeoLite2-ASN.mmdb

    MaxMindDBEnv MM_ASN ASN_DB/autonomous_system_number
    MaxMindDBEnv MM_ASORG ASN_DB/autonomous_system_organization

    MaxMindDBNetworkEnv ASN_DB ASN_DB_NETWORK
</IfModule>
```

**City Database**
```
<IfModule mod_maxminddb.c>
    MaxMindDBEnable On
    MaxMindDBFile CITY_DB /usr/local/share/GeoIP/GeoLite2-City.mmdb

    MaxMindDBEnv MM_COUNTRY_CODE CITY_DB/country/iso_code
    MaxMindDBEnv MM_COUNTRY_NAME CITY_DB/country/names/en
    MaxMindDBEnv MM_CITY_NAME CITY_DB/city/names/en
    MaxMindDBEnv MM_LONGITUDE CITY_DB/location/longitude
    MaxMindDBEnv MM_LATITUDE CITY_DB/location/latitude

    MaxMindDBNetworkEnv CITY_DB CITY_DB_NETWORK
</IfModule>
```

**Bloquer par pays**

```
<IfModule mod_maxminddb.c>
MaxMindDBEnable On
MaxMindDBFile DB /usr/local/share/GeoIP/GeoLite2-Country.mmdb
MaxMindDBEnv MM_COUNTRY_CODE DB/country/iso_code

SetEnvIf MM_COUNTRY_CODE ^(RU|DE|FR) BlockCountry
Deny from env=BlockCountry
</IfModule>
```

Nb: On peut toujours utiliser le GeoIP.dat mais il n'est pas mis à jour par Maxwind  






