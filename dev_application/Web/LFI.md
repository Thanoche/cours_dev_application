# LFI
En exploitant **une mauvaise gestion des fichiers sur le site web**, il a été possible d’**accéder à un fichier confidentiel du serveur**, obtenant ainsi des informations sensibles.

Le site web permet de charger dynamiquement des fichiers, mais aucun contrôle n'est appliqué, ce qui peut permettre à un attaquant d’accéder à des fichiers situés en dehors du répertoire prévu.

___

### **1. Identification de la vulnérabilité**

Lors de la navigation sur le site, l’URL change et inclut un paramètre `view` :
```
http://13.38.24.60/index.php?view=
```
Cela indique que le site charge des fichiers dynamiquement en fonction de la valeur donnée.
Cependant, cette fonctionnalité est vulnérable à une **LFI (Local File Inclusion)**. Un attaquant pourrait alors tenter d’accéder à un fichier sensible en remontant l'arborescence du système.

___

### **2. Exploitation**

En testant des chemins relatifs, il est possible de récupérer un fichier situé dans `/var/www/flag.txt` en injectant :
```
http://13.38.24.60/index.php?view=../../../var/www/flag.txt
```

Le flag récupéré est :
> **Flag** => secrets{p~hAT@]<"qU67z8%}
