
1. Créer un compte de stockage avec différentes options de réplication

    Créer un compte de stockage :
    ![alt text](<Création Compte de Stockage.png>)

2. Télécharger et gérer des blobs avec le portail Azure et Azure CLI
    
    Avec Azure CLI :
        Ouvrez un terminal avec l'Azure CLI installé.
        Connectez-vous à votre compte Azure avec az login.
        Créez un conteneur avec la commande suivante :

        bash

az storage container create --name <nom_conteneur> --account-name <nom_compte_stockage> --auth-mode login

Téléchargez un fichier blob avec cette commande :
    ![alt text](<Rajout du premier blob au conteneur.png>)
bash

        az storage blob upload --container-name <nom_conteneur> --file <chemin_fichier> --name <nom_blob> --account-name <nom_compte_stockage>

3. Configurer les signatures d'accès partagé (SAS) pour un accès sécurisé
    ![alt text](<Géneration key et SAP.png>)
    Dans le portail Azure :
        
    Avec Azure CLI :
        Utilisez la commande suivante pour générer un SAS pour un conteneur :

        bash

        az storage container generate-sas --name <nom_conteneur> --account-name <nom_compte_stockage> --permissions rwdl --expiry <YYYY-MM-DDTHH:MM:SSZ> --auth-mode login

4. Mettre en place des politiques de gestion du cycle de vie
    ![alt text](<règle cycle de vie.png>)


