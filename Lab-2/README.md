
Lab 2 : Implémentation de réseaux virtuels Azure (VNet)
Étape 1 : Création d'un VNet avec plusieurs sous-réseaux


    Lab-2/Déploiement VNET.png

Commande équivalente (Azure CLI)

bash

az network vnet create \
  --name VNet-Lab2 \
  --resource-group Lab_FINOPS \
  --address-prefix 10.1.0.0/16 \
  --subnet-name Sous-reseau-1 \
  --subnet-prefix 10.1.1.0/24

az network vnet subnet create \
  --vnet-name VNet-Lab2 \
  --name Sous-reseau-2 \
  --address-prefix 10.1.2.0/24 \
  --resource-group Lab_FINOPS

Étape 2 : Configuration des Groupes de Sécurité Réseau (NSG)

    Créez un Groupe de Sécurité Réseau (NSG) et configurez les règles pour autoriser le trafic SSH (port 22) et RDP (port 3389).

    Lab-2/Création NSG.png
    Lab-2/Règles.png

    az network nsg create \
  --resource-group <nom_du_groupe> \
  --name NSG-Lab2

az network nsg rule create \
  --resource-group <nom_du_groupe> \
  --nsg-name NSG-Lab2 \
  --name Autoriser-SSH \
  --priority 1000 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --destination-port-ranges 22

az network nsg rule create \
  --resource-group <nom_du_groupe> \
  --nsg-name NSG-Lab2 \
  --name Autoriser-RDP \
  --priority 1001 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --destination-port-ranges 3389

Étape 3 : Déploiement de machines virtuelles dans des sous-réseaux spécifiques

    Déployez une première machine virtuelle dans le Sous-reseau-1 et une deuxième dans le Sous-reseau-2.

az vm create \
  --resource-group <nom_du_groupe> \
  --name VM-SousReseau1 \
  --image UbuntuLTS \
  --admin-username <votre_nom_d_utilisateur> \
  --authentication-type ssh \
  --ssh-key-value <votre_clé_publique_ssh> \
  --vnet-name VNet-Lab2 \
  --subnet Sous-reseau-1

az vm create \
  --resource-group <nom_du_groupe> \
  --name VM-SousReseau2 \
  --image UbuntuLTS \
  --admin-username <votre_nom_d_utilisateur> \
  --authentication-type ssh \
  --ssh-key-value <votre_clé_publique_ssh> \
  --vnet-name VNet-Lab2 \
  --subnet Sous-reseau-2

Étape 4 : Configuration du peering entre deux réseaux virtuels (VNets)

    Configurez le peering entre VNet-Lab2 et un autre réseau virtuel :
        Sélectionnez le VNet cible et configurez les options telles que Autoriser le transit de passerelle et Autoriser le trafic transféré si nécessaire.

        Lab-2/Lien peering.png

    az network vnet peering create \
  --name VNet2toVNet1 \
  --resource-group <> \
  --vnet-name VNet-Lab2 \
  --remote-vnet <vnet-id-de-l-autre-VNet> \
  --allow-vnet-access

  ![alt text](<Suppression ressources lab 1&2.png>)
