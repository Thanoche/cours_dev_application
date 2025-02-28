# Comment tout mettre en péril

En utilisant **un programme mal configuré**, il a été possible d’**exécuter des commandes avec des privilèges élevés**, obtenant ainsi un accès au système.

L'exécutable `exec` a été compilé à partir d'un script, puis configuré pour s'exécuter avec les **permissions de son propriétaire**, quel que soit l'utilisateur qui le lance.

___

### Identification de la vulnérabilité
Le script `compile.sh` configure l'exécutable avec le **bit SUID** via la commande `chmod 4755 exec`. Cela signifie que le fichier hérite des privilèges de son propriétaire, même s'il est lancé par un **utilisateur sans privilèges**. Ainsi, toute personne exécutant ce fichier le fera **avec les mêmes droits que son propriétaire**.
L'exécutable utilise la fonction `execvp` pour exécuter des commandes système. Permettant à un **attaquant d'exécuter n'importe quelle commande**, y compris des commandes malveillantes qui pouvant ainsi nuire à la sécurité du système.

> Flag => compile.sh.3