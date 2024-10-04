Lab 5: Implementing Azure SQL Databases
Étape 1 : Déployer une instance SQL Azure

![alt text](<Déploiement BDD SQL validé.png>)
![alt text](<Déploiement BDD SQL validé.png>)

Commande équivalente (Azure CLI)

az sql db create \
  --resource-group <nom_du_groupe> \
  --name sqlDBLab5 \
  --server <nom_du_serveur> \
  --edition Basic

Étape 2 : Configurer les paramètres de pare-feu

    Configurez les paramètres de pare-feu pour autoriser l'accès depuis des adresses IP spécifiques dans le portail Azure.

![alt text](<Configuration Pare-Feu SQL Server.png>)
Commande équivalente (Azure CLI)

az sql server firewall-rule create \
  --resource-group <nom_du_groupe> \
  --server <nom_du_serveur> \
  --name AllowYourIP \
  --start-ip-address <votre_adresse_IP> \
  --end-ip-address <votre_adresse_IP>

Étape 3 : Importer des données dans la base de données

    Importez des données dans la base de données via Azure Data Studio ou SQL Server Management Studio (SSMS).



bcp <database.schema.table> in <file.csv> -S <server>.database.windows.net -d <database> -U <username> -P <password> -c -t ,

Étape 4 : Implémenter la géo-réplication

    Activez la géo-réplication pour assurer une haute disponibilité dans une région secondaire.

![alt text](<Création Réplica Réussi .png>)
Commande équivalente (Azure CLI)

az sql db replica create \
  --name sqlDBLab5 \
  --resource-group <nom_du_groupe> \
  --server <nom_du_serveur> \
  --partner-server <nom_serveur_replication> \
  --partner-resource-group <nom_du_groupe>

