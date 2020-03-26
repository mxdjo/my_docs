On souhaite bloquer les utilisateurs de certains pays ( en se basant sur leurs IP).   
Cela sera possible grâce à GeoIP.  
GeoIP permet de trouver le pays d'une adresse IP ou d'un hostname.   

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

## Debian/Ubuntu ##

### Installation des paquets ###

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
