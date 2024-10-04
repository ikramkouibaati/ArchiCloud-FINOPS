
# Lab 10 : Configuration des services de sauvegarde et de récupération Azure



### 1. Créer un Recovery Services Vault

#### Via le portail Azure

![alt text](<Déploiement Rcovery Srvice.png>)

![alt text](<Déploiement de la VM à Backup.png>)

#### Via Azure CLI

```bash
az backup vault create \
    --resource-group <Nom-du-groupe-de-ressources> \
    --name <Nom-du-Recovery-Vault> \
    --location <Région>
```

### 2. Configurer la sauvegarde pour les machines virtuelles et les fichiers Azure

#### Sauvegarde pour les machines virtuelles

##### Via le portail Azure



##### Via Azure CLI

1. Configurer une politique de sauvegarde pour les VM :
![alt text](<Backu^Policy Custom.png>)


```bash
az backup policy create \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --name <Nom-de-la-politique> \
    --backup-management-type AzureIaasVM \
    --policy <Fichier-JSON-de-la-politique>
```

2. Associer une machine virtuelle à la politique de sauvegarde :

![
    
](<Enabling Backup for VM10.png>)
```bash
az backup protection enable-for-vm \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --vm <Nom-de-la-VM> \
    --policy-name <Nom-de-la-politique>
```

#### Sauvegarde pour les fichiers Azure

##### Via le portail Azure
![alt text](<Storage Space to be Backed up.png>)


##### Via Azure CLI

1. Configurer une politique de sauvegarde pour les fichiers :

```bash
az backup policy create \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --name <Nom-de-la-politique> \
    --backup-management-type AzureStorage \
    --policy <Fichier-JSON-de-la-politique>
```

2. Activer la protection pour une part de fichier Azure :

```bash
az backup protection enable-for-azurefileshare \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --storage-account <Nom-du-compte-de-stockage> \
    --azure-file-share <Nom-de-la-part> \
    --policy-name <Nom-de-la-politique>
```

### 3. Effectuer une sauvegarde et une restauration

#### Effectuer une sauvegarde

##### Via le portail Azure


![alt text](<Backup Successfully triggered.png>)
##### Via Azure CLI

1. Lancer une sauvegarde pour une machine virtuelle :

```bash
az backup protection backup-now \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --item-name <Nom-de-la-VM> \
    --backup-management-type AzureIaasVM
```

2. Lancer une sauvegarde pour une part de fichiers Azure :

```bash
az backup protection backup-now \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --item-name <Nom-de-la-part-de-fichier> \
    --backup-management-type AzureStorage
```

#### Effectuer une restauration

##### Via le portail Azure

1. Dans le **Recovery Services Vault**, accédez à **Éléments de sauvegarde**, puis sélectionnez **Machines virtuelles Azure** ou **Azure File Shares**.
2. Sélectionnez la ressource à restaurer, puis cliquez sur **Restaurer VM** ou **Restaurer les fichiers**.
3. Suivez l'assistant pour sélectionner le point de restauration.

##### Via Azure CLI

1. Restaurer une machine virtuelle :

```bash
az backup restore restore-disks \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --container-name <Nom-du-conteneur> \
    --item-name <Nom-de-la-VM> \
    --restore-config <Fichier-JSON-de-configuration-de-restauration>
```

2. Restaurer une part de fichiers Azure :

```bash
az backup restore restore-azurefileshare \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --item-name <Nom-de-la-part-de-fichier>
```

### 4. Mettre en œuvre des politiques de sauvegarde et des rétentions

#### Créer une politique de sauvegarde personnalisée

##### Via le portail Azure

1. Dans le **Recovery Services Vault**, accédez à **Politiques de sauvegarde**.
2. Cliquez sur **+ Ajouter** pour créer une nouvelle politique de sauvegarde.
3. Configurez les éléments suivants :
   - **Fréquence de sauvegarde** : Configurez la fréquence des sauvegardes (quotidienne, hebdomadaire, etc.).
   - **Durée de rétention** : Définissez la durée pendant laquelle chaque sauvegarde doit être conservée.
4. Cliquez sur **OK** pour enregistrer la politique.

##### Via Azure CLI

1. Créez la politique en définissant la configuration dans un fichier JSON, puis exécutez la commande suivante :

```bash
az backup policy create \
    --resource-group <Nom-du-groupe-de-ressources> \
    --vault-name <Nom-du-Recovery-Vault> \
    --name <Nom-de-la-politique> \
    --backup-management-type AzureIaasVM \
    --policy <Fichier-JSON-de-la-politique>
```

Backed Up Items 
![alt text](<Backued up Items.png>)
![alt text](<Backup Items.png>)

---

