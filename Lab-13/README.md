
# Lab 13 : Implémentation d'Azure Key Vault

## Étapes

### 1. Créer un Key Vault
![alt text](<Déploiement Key Vault.png>)
```bash
az keyvault create \
    --name <Nom-du-key-vault> \
    --resource-group <Nom-du-groupe-de-ressources> \
    --location <Région>
```

### 2. Ajouter un secret au Key Vault
[text](Key_Use.py)
```bash
az keyvault secret set \
    --vault-name <Nom-du-key-vault> \
    --name <Nom-du-secret> \
    --value <Valeur-du-secret>
```

### 3. Récupérer un secret depuis le Key Vault
[text](Récupérer_Key.py)
```bash
az keyvault secret show \
    --vault-name <Nom-du-key-vault> \
    --name <Nom-du-secret>
```

### 4. Ajouter une clé au Key Vault
![alt text](<Erreur -Impossible de créer un new secret.png>)
```bash
az keyvault key create \
    --vault-name <Nom-du-key-vault> \
    --name <Nom-de-la-clé> \
    --protection software
```

### 5. Récupérer une clé depuis le Key Vault

```bash
az keyvault key show \
    --vault-name <Nom-du-key-vault> \
    --name <Nom-de-la-clé>
```

### 6. Ajouter un certificat au Key Vault

```bash
az keyvault certificate create \
    --vault-name <Nom-du-key-vault> \
    --name <Nom-du-certificat> \
    --policy "$(az keyvault certificate get-default-policy)"
```

### 7. Accorder l'accès à un utilisateur ou une application

```bash
az keyvault set-policy \
    --name <Nom-du-key-vault> \
    --resource-group <Nom-du-groupe-de-ressources> \
    --upn <Adresse-e-mail-utilisateur> \
    --secret-permissions get list \
    --key-permissions get list \
    --certificate-permissions get list
```

### 8. Visualiser les secrets, clés et certificats

```bash
az keyvault secret list --vault-name <Nom-du-key-vault>
az keyvault key list --vault-name <Nom-du-key-vault>
az keyvault certificate list --vault-name <Nom-du-key-vault>
```

### 9. Supprimer un secret, une clé ou un certificat

```bash
az keyvault secret delete --vault-name <Nom-du-key-vault> --name <Nom-du-secret>
az keyvault key delete --vault-name <Nom-du-key-vault> --name <Nom-de-la-clé>
az keyvault certificate delete --vault-name <Nom-du-key-vault> --name <Nom-du-certificat>
```

---
