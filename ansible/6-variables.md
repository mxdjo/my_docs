Avant d'utiliser les variables, nous devons savoir comment les déclarer.  
Les noms de variables doivent être des lettres, des chiffres et des traits de soulignement(underscores). Les variables doivent toujours commencer par une lettre.    
foo_port est une excellente variable. foo5 est très bien aussi.
foo-port, foo port, foo.port et 12 ne sont pas des noms de variables valables.
Nous pouvons faire référence à un champ spécifique du dictionnaire en utilisant soit la notation par parenthèses, soit la notation par points :

```
foo['field1']
foo.field1

```
Cependant, si nous choisissons d'utiliser la notation par points, sachons que certaines clés peuvent poser des problèmes car elles entrent en collision avec les attributs et les méthodes des dictionnaires python. il faut donc utiliser la notation par parenthèses au lieu de la notation par points si on veut utiliser des clés qui commencent et se terminent par deux traits de soulignement (ceux-ci sont réservés aux significations spéciales en python) ou si vous utilisez l'un des attributs publics connus :

```
add, append, as_integer_ratio, bit_length, capitalize, center, clear, conjugate, copy, count, decode, denominator, difference, difference_update, discard, encode, endswith, expandtabs, extend, find, format, fromhex, fromkeys, get, has_key, hex, imag, index, insert, intersection, intersection_update, isalnum, isalpha, isdecimal, isdigit, isdisjoint, is_integer, islower, isnumeric, isspace, issubset, issuperset, istitle, isupper, items, iteritems, iterkeys, itervalues, join, keys, ljust, lower, lstrip, numerator, partition, pop, popitem, real, remove, replace, reverse, rfind, rindex, rjust, rpartition, rsplit, rstrip, setdefault, sort, split, splitlines, startswith, strip, swapcase, symmetric_difference, symmetric_difference_update, title, translate, union, update, upper, values, viewitems, viewkeys, viewvalues, zfill.

```

### Declarer des variables dans la commande ###
On peut déclarer les variables dans un playbook

```
- hosts: webservers
  vars:
    http_port: 80
```

#### Utiliser les variables dans un YAML ####

La syntaxe YAML exige que si vous commencez une valeur par {{ foo }} vous citez la ligne entière, car elle veut être sûre que vous n'essayez pas de démarrer un dictionnaire YAML. Cette question est traitée dans la documentation sur la syntaxe YAML.  
Cela ne marchera pas :
```
- hosts: app_servers
  vars:
      app_path: {{ base_path }}/22
```

ça par contre, oui:

```
- hosts: app_servers
  vars:
       app_path: "{{ base_path }}/22"

```

#### Variables découvertes à partir des systèmes : Facts ####

Les Facts sont des informations obtenues en parlant avec vos systèmes à distance.
Pour voir quelles informations sont disponibles,on insère cette ligne dans un playbook

```
- debug: var=ansible_facts
```
C'est aussi possible d'avoir toutes les informations via la ligne de commande:
```
ansible nom_du_slave -m setup
```

```

ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "192.168.56.101",
            "10.0.2.15"
        ],
        "ansible_all_ipv6_addresses": [
            "fe80::a00:27ff:fea2:c4c1",
            "fe80::a00:27ff:fe76:b909"
        ],
        "ansible_apparmor": {
            "status": "enabled"
        },
        "ansible_architecture": "x86_64",
        "ansible_bios_date": "12/01/2006",
        "ansible_bios_version": "VirtualBox",
        "ansible_cmdline": {
            "BOOT_IMAGE": "/boot/vmlinuz-4.15.0-91-generic",
            "biosdevname": "0",
            "net.ifnames": "0",
            "quiet": true,
            "ro": true,
            "root": "/dev/mapper/vagrant--vg-root"
        },
        "ansible_date_time": {
            "date": "2020-05-26",
            "day": "26",
            "epoch": "1590517748",
            "hour": "18",
            "iso8601": "2020-05-26T18:29:08Z",
      
        },
        "ansible_default_ipv4": {
            "address": "10.0.2.15",
            "alias": "eth0",
            "broadcast": "10.0.2.255",
            "gateway": "10.0.2.2",
   ,
        "ansible_device_links": {
            "ids": {
                "dm-0": [
                    "dm-name-vagrant--vg-root",
                    "dm-uuid-LVM-sS0EJZQTwXSvhoFnWwf7lv1JcQuOchGOWDoNTZGIdJPHHG37kP4YoKkMeZyj0PPJ"
                ],
                "dm-1": [
                    "dm-name-vagrant--vg-swap_1",
                    "dm-uuid-LVM-sS0EJZQTwXSvhoFnWwf7lv1JcQuOchGOhFIJQkviYA7lncGwkvaxw4VNGnRiMb0E"
                ],
                "sda": [
                    "ata-VBOX_HARDDISK_VBff8977b6-2ff8395d"
                ],
                "sda1": [
                    "ata-VBOX_HARDDISK_VBff8977b6-2ff8395d-part1",
                    "lvm-pv-uuid-1y8Xkn-DRRA-Wsvd-yajR-Og8j-MCPp-xu15u5"
                ]
            },
            "labels": {},
            "masters": {
                "sda1": [
                    "dm-0",
                    "dm-1"
                ]
            },
            "uuids": {
                "dm-0": [
                    "be3fea6c-07f8-4e98-a808-61ae170da1a2"
                ],
                "dm-1": [
                    "03fd706d-b458-40e6-8b83-078ad9aa9b58"
                ]
            }
        },
        "ansible_devices": {
            "dm-0": {
                "holders": [],
                "host": "",
                "links": {
                    "ids": [
                        "dm-name-vagrant--vg-root",
                        "dm-uuid-LVM-sS0EJZQTwXSvhoFnWwf7lv1JcQuOchGOWDoNTZGIdJPHHG37kP4YoKkMeZyj0PPJ"
                    ],
                    "labels": [],
                    "masters": [],
                    "uuids": [
                        "be3fea6c-07f8-4e98-a808-61ae170da1a2"
                    ]
                },
                "model": null,
                "partitions": {},
                "removable": "0",
                "rotational": "1",
                "sas_address": null,
                "sas_device_handle": null,

            },
            "dm-1": {
                "holders": [],
                "host": "",
                "links": {
                    "ids": [
                        "dm-name-vagrant--vg-swap_1",
                        "dm-uuid-LVM-sS0EJZQTwXSvhoFnWwf7lv1JcQuOchGOhFIJQkviYA7lncGwkvaxw4VNGnRiMb0E"
                    ],
                    "labels": [],
                    "masters": [],
                    "uuids": [
                        "03fd706d-b458-40e6-8b83-078ad9aa9b58"
                    ]
                },
                "model": null,
                "partitions": {},
      
                "vendor": null,
                "virtual": 1
            },
            "loop0": {
                "holders": [],
                "host": "",
                "links": {
       
                },
                "model": null,
                "partitions": {},
                "removable": "0",
     
            },
            "loop1": {
                "holders": [],
                "host": "",
                "links": {
                    "ids": [],
                    "labels": [],
                    "masters": [],
                    "uuids": []
                },
                "model": null,
                "partitions": {},
                "removable": "0",
                "rotational": "1",
                "sas_address": null,
                "sas_device_handle": null,
                "scheduler_mode": "none",
                "sectors": "0",
                "sectorsize": "512",
                "size": "0.00 Bytes",
                "support_discard": "0",
                "vendor": null,
                "virtual": 1
 
                "support_discard": "0",
                "vendor": "ATA",
                "virtual": 1
            }
        },
        "ansible_distribution": "Ubuntu",
        "ansible_distribution_file_parsed": true,
        "ansible_distribution_file_path": "/etc/os-release",
        "ansible_distribution_file_variety": "Debian",
        "ansible_distribution_major_version": "18",
        "ansible_distribution_release": "bionic",
        "ansible_distribution_version": "18.04",
        "ansible_dns": {
            "nameservers": [
                "127.0.0.53"
            ],
            "options": {
                "edns0": true
            }
        },
        "ansible_domain": "",
        "ansible_effective_group_id": 1000,
        "ansible_effective_user_id": 1000,
        "ansible_env": {
            "HOME": "/home/vagrant",
            "LANG": "C",
            "LANGUAGE": "en_US:",
          
        },
        "ansible_eth0": {
            "active": true,
            "device": "eth0",
            "features": {
                "esp_hw_offload": "off [fixed]",
                "esp_tx_csum_hw_offload": "off [fixed]",
                "fcoe_mtu": "off [fixed]",
                "generic_receive_offload": "on",
                "generic_segmentation_offload": "on",
                "highdma": "off [fixed]",
        
                "vlan_challenged": "off [fixed]"
            },
            "hw_timestamp_filters": [],
            "ipv4": {
                "address": "10.0.2.15",
                "broadcast": "10.0.2.255",
                "netmask": "255.255.255.0",
                "network": "10.0.2.0"
            },
            "ipv6": [
                {
                    "address": "fe80::a00:27ff:fe76:b909",
                    "prefix": "64",
                    "scope": "link"
                }
            ],
            "macaddress": "08:00:27:76:b9:09",
            "module": "e1000",
            "mtu": 1500,
            "pciid": "0000:00:03.0",
            "promisc": false,
            "speed": 1000,
            "timestamping": [
                "tx_software",
                "rx_software",
                "software"
            ],
            "type": "ether"
        },

###Suite en bas ####

   "ansible_nodename": "slave1",
        "ansible_os_family": "Debian",
        "ansible_pkg_mgr": "apt",
        "ansible_proc_cmdline": {
            "BOOT_IMAGE": "/boot/vmlinuz-4.15.0-91-generic",
            "biosdevname": "0",
            "net.ifnames": "0",
            "quiet": true,
            "ro": true,
            "root": "/dev/mapper/vagrant--vg-root"
        },
```

Pour avoir accès au nodename(ansible_nodename) on fait ceci:

```
{{ ansible_facts['nodename'] }}
```

#### Les variables magiques ####

Que vous définissiez ou non des variables, vous pouvez accéder à des informations sur vos hôtes grâce aux variables spéciales fournies par Ansible, y compris les variables "magiques", les Facts et les variables de connexion. Les noms des variables magiques sont réservés - ne définissez pas de variables avec ces noms. La variable environment est également réservée.    

Les variables magiques les plus couramment utilisées sont *hostvars*, *groups*, *group_names* et *inventory_hostname*.

*hostvars* nous permet d'accéder aux variables d'un autre hôte, y compris les *Facts* qui ont été recueillis sur cet hôte. Vous pouvez accéder aux variables d'un hôte à n'importe quel moment dans un livre de jeu. Même si vous ne vous êtes pas encore connecté à cet hôte dans une pièce du playbook ou d'un ensemble de playbooks, nous pouvons toujours obtenir les variables, mais vous ne pourrez pas voir les Facts.    

Pour accéder à la variable d'un autre node:   

```
{{ hostvars['test.example.com']['ansible_facts']['distribution'] }}
```

Dans un playbook, on peut définir les variables mais aussi les définir dans un fichier YAML



```
- hosts: all
  remote_user: root
  vars:
    favcolor: blue
  vars_files:
    - /vars/external_vars.yml

  tasks:

  - name: this is just a placeholder
    command: /bin/echo foo
```

Il faut cependant tenir compte de l'ordre de preference d'Ansible dans l'exécution.

https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#ansible-variable-precedence
Ce qui veut dire que si on définit dans notre Inventory: ansible_user: albert et qu'on exécute

```
ansible -u super_user host 
```

On va se connecter en tant que "albert".    

On peut donner une valeur à une variable via la ligne de commande

```
- name: pass a message on the command line
  hosts: localhost
  vars:
    greeting: "you didn't specify a message"
  tasks:
   - name: output a message
     debug: msg="{{ greeting }}"
```

La commande ansible-playbook est:
```
ansible-playbook greet.yml -e greeting=hiya
```

Liens intéressants: https://blog.ruanbekker.com/blog/2020/01/24/environment-variables-with-ansible/
