Pendant que j'écrivais et testais le playbook qui doit installer le wordpress, j'ai appris un petit truc sur la connexion à MariaDB.
J'utilisais pour mon exemple debian 10 avec MariaDB 10.3.X  
J'ai découvert après erreur de mon playbook qu'il a plusieurs plugins d'authentification à MariaDB/MySQL.

### Plugins coté client ####
Les plugins supportés sont les suivants:   
* mysql_native_password
* mysql_old_password
* mysql_clear_password
* sha256_password
* dialog
* client_ed25519

Et bien d'autres ...

### Plugins coté serveur ###
Ce sont:
* mysql_native_password
* mysql_old_password
* ed25519
* gssapi
* pam (Unix seulement)
* unix_socket (Unix seulement)
* named_pipe (Windows uniquement)

Sous Debian 10 (avec MariaDB 10.3.2), par défaut le plugin est unix_socket.
Il est possible de savoir quel utilisateur utilise un plugin ou un autre via la CLI MySQL
```
select User,Password,Plugin from user where User='root'
```
