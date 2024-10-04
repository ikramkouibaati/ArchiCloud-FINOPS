Lab 18: Configuring Azure Virtual Desktop
Étape 1 : Configurer l'environnement Azure Virtual Desktop

    Créez un Host Pool dans le portail Azure pour gérer les sessions utilisateur.

    ![alt text](<Création Host Pool.png>)
    Commande équivalente (Azure CLI)

    az desktopvirtualization hostpool create     --resource-group <nom_du_groupe>     --name <nom_du_hostpool>     --location <region>     --friendly-name "Host Pool Lab18"     --description "Host Pool for Azure Virtual Desktop Lab"

Étape 2 : Configurer les pools d'hôtes, les hôtes de session, et les espaces de travail

    Ajoutez des Session Hosts (machines virtuelles) pour héberger les sessions utilisateur.
    Créez un Workspace pour regrouper les bureaux et applications publiés.

    ![alt text](<Adding VM error.png>)
    Commande équivalente (Azure CLI)

    az desktopvirtualization applicationgroup create     --resource-group <nom_du_groupe>     --host-pool-name <nom_du_hostpool>     --name <nom_du_workspace>     --location <region>     --friendly-name "Workspace Lab18"     --description "Workspace for Virtual Desktop Applications"

Étape 3 : Publier des applications de bureau à distance

    Publiez des applications dans Azure Virtual Desktop pour les rendre accessibles aux utilisateurs.

Étape 4 : Se connecter aux bureaux virtuels en tant qu'utilisateur

    Connectez-vous à Azure Virtual Desktop via le client Remote Desktop ou un navigateur Web.

Je n 'ai pas pu réaliser les deux dernières étapes car j'ai atteint le quota limite et je n'ai alors pas pules créer