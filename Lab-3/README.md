## Étape 1: Créer un plan Azure App Service

   **Créer un groupe de ressources** :
   ![alt text](<Création app plan.png>)
   ```bash
   az group create --name Lab3ResourceGroup --location "Noth Europe"
   az appservice plan create --name Lab3AppServicePlan --resource-group Lab3ResourceGroup --sku B1 --is-linux

##   Étape 2: Déployer une application web sur Azure App Service
   Lab-3/Déploiement réussi IkramAPP.png

    **Créer une application web** :
    az webapp create --resource-group Lab3ResourceGroup --plan Lab3AppServicePlan --name Lab3WebApp --runtime "PYTHON|3.8"

        Déployer le code depuis GitHub :
        Assurez-vous que votre code est sur GitHub et utilisez Azure App Service pour le déploiement continu.

##Étape 3: Configurer des domaines personnalisés et des certificats SSL

    Ajouter un domaine personnalisé :
    Lab-3/Domaine personnalisé .png

    az webapp config hostname add --webapp-name Lab3WebApp --resource-group Lab3ResourceGroup --hostname yourcustomdomain.com

    Lier un certificat SSL au domaine (en supposant que vous avez déjà un certificat SSL) :
    az webapp config ssl bind --certificate-thumbprint yourCertThumbprint --ssl-type SNI --name Lab3WebApp --resource-group Lab3ResourceGroup


##Étape 4: Implémenter des slots de déploiement pour le staging et la production
    Créer un slot de déploiement pour le staging :
    Lab-3/Erreur Slots.png

    