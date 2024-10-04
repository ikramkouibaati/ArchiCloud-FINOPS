## Étape 1: Créer un plan Azure App Service

   **Créer un groupe de ressources** :
   ![alt text](<Création app plan.png>)
   ```bash
   az group create --name Lab3ResourceGroup --location "Noth Europe"
   az appservice plan create --name Lab3AppServicePlan --resource-group Lab3ResourceGroup --sku B1 --is-linux

##   Étape 2: Déployer une application web sur Azure App Service
   ![alt text](<Déploiement réussi Ikram APP.png>)

    **Créer une application web** :
    az webapp create --resource-group Lab3ResourceGroup --plan Lab3AppServicePlan --name Lab3WebApp --runtime "PYTHON|3.8"

        Déployer le code depuis GitHub :
        Assurez-vous que votre code est sur GitHub et utilisez Azure App Service pour le déploiement continu.

##Étape 3: Configurer des domaines personnalisés et des certificats SSL

    Ajouter un domaine personnalisé :
   ![alt text](<Domaine personnalisé.png>)

    az webapp config hostname add --webapp-name Lab3WebApp --resource-group Lab3ResourceGroup --hostname yourcustomdomain.com

    Lier un certificat SSL au domaine (en supposant que vous avez déjà un certificat SSL) :
    az webapp config ssl bind --certificate-thumbprint yourCertThumbprint --ssl-type SNI --name Lab3WebApp --resource-group Lab3ResourceGroup


## Étape 4: Implémenter des slots de déploiement pour le staging et la production
    Créer un slot de déploiement pour le staging :
  
![Erreur Slots](https://github.com/user-attachments/assets/b3689e7a-1ba3-4077-8588-c2dff7801d2c)

    

    
