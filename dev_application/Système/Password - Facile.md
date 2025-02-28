# Password - Facile

En utilisant **un outil de craquage de mots de passe**, il a été possible de **récupérer le mot de passe d'un compte administrateur**, obtenant ainsi l'accès aux informations sensibles du système.

Les fichiers `passwd` et `shadow` fournis par le challenge permettent de retrouver les **informations d'authentification** des différents profils présents sur le système.
___
### 1. Identification d'un profil privilégié 
Dans le fichier `passwd`, il est possible d'identifier un profil privilégié, le profil **root**, pour lequel un hash du mot de passe est associé dans le fichier `shadow`. Il ne reste plus qu'à préparer ces fichiers pour une utilisation avec **John the Ripper**, un outil de craquage de mot de passe, avec la commande suivante :
```
unshadow passwd shadow > unshadow.txt
```
___
### 2. Craquage du mot de passe
Après cette étape, **John the Ripper** peut être lancé pour effectuer **une attaque par force brute**, sans utiliser de wordlist :
```
john unshadow.txt
john --show unshadow.txt
```
Cette opération permet d'afficher le mot de passe trouvé.

Le mot de passe du compte **root** récupéré est :
> **Flag** => buliyal