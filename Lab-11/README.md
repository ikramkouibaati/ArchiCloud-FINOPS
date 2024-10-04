
# Lab 11 : Implémentation d'Azure Monitor et des Alertes


## Étapes

### 1. Créer un groupe d'action pour les alertes
![alt text](<Alerts Cration .png>)

```bash
az monitor action-group create \
    --resource-group <Nom-du-groupe-de-ressources> \
    --name <Nom-du-groupe-d'action> \
    --action email \
    --email-receiver <Nom-de-l'e-mail> \
    --email-address <Adresse-e-mail>
```

### 2. Créer une règle d'alerte basée sur une métrique
![alt text](<Monitoring Enabled for VM10.png>)
```bash
az monitor metrics alert create \
    --name <Nom-de-l'alerte> \
    --resource-group <Nom-du-groupe-de-ressources> \
    --scopes <ID-de-la-ressource-à-surveiller> \
    --condition "avg Percentage CPU > 80" \
    --description "Alerte si le CPU dépasse 80%" \
    --action-group <Nom-du-groupe-d'action>
```

### 3. Créer une règle d'alerte basée sur les journaux

```bash
az monitor activity-log alert create \
    --name <Nom-de-l'alerte> \
    --resource-group <Nom-du-groupe-de-ressources> \
    --scopes <ID-de-la-ressource> \
    --condition category=Administrative operationName=StartVirtualMachineEvent \
    --action-group <Nom-du-groupe-d'action>
```

### 4. Créer une règle d'alerte pour les métriques avec une condition personnalisée

```bash
az monitor metrics alert create \
    --name <Nom-de-l'alerte> \
    --resource-group <Nom-du-groupe-de-ressources> \
    --scopes <ID-de-la-ressource-à-surveiller> \
    --condition "avg Transactions > 1000 where BlobType == 'BlockBlob'" \
    --description "Alerte si les transactions sur les blobs dépassent 1000" \
    --action-group <Nom-du-groupe-d'action>
```

### 5. Visualiser les alertes existantes
![alt text](<Dashboard Used Capacity VM.png>)
![alt text](<My geeral Dashboard.png>)
```bash
az monitor metrics alert list \
    --resource-group <Nom-du-groupe-de-ressources>
```

### 6. Supprimer une alerte

```bash
az monitor metrics alert delete \
    --name <Nom-de-l'alerte> \
    --resource-group <Nom-du-groupe-de-ressources>
```

---

