# Signature

En utilisant **un outil de cryptographie**, il a été possible de **valider l'authenticité des messages**, obtenant ainsi le seul fichier légitime contenant le flag.

Le **fichier de signature**, ainsi que la clé publique fournie par le challenge, permettent de vérifier **quel message correspond à la signature donnée**. En utilisant l'outil de **OpenSSL**, il est possible de déterminer le message pour lequel la signature est valide avec la clé publique.
___
### 1. Vérification des signatures
Un script Bash sera utilisé pour **tester chaque fichier du répertoire et vérifier la validité de sa signature avec la clé publique**.
```
PUBLIC_KEY="alice.pub"
SIGNATURE="alice-ecdsa-sha256-signature.bin"

for file in ./*; do
    if openssl dgst -sha256 -verify "$PUBLIC_KEY" -signature "$SIGNATURE" "$file" 2>/dev/null; then
        echo "✅ => Signature valide trouvée dans : $file"
        exit 0
    fi
done

echo "❌ Aucun fichier valide trouvé"
exit 1
```
Après l'exécution du script, le programme indique que la signature correspond au fichier `message-777.txt`.

Ce fichier contient le flag recherché :
> **Flag** = lvgnqcjsnhlaqcrdghfrgrgya
