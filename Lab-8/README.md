

Lab 8: Using Azure Cognitive Services
Étape 1 : Créer une ressource Cognitive Services

    Créez une ressource Cognitive Services dans le portail Azure :
Création Cognitive service:
![alt text](<Création Cognitive service.png>)

Clé API 1 = 7f6672af0db04f42a124d955ba97d8cb

Commande Azure CLI équivalente :

az cognitiveservices account create \
  --name CognitiveLab8 \
  --resource-group <nom_du_groupe> \
  --kind TextAnalytics \
  --sku S0 \
  --location <region> \
  --yes

Étape 2 : Développer une application qui utilise l'API Text Analytics

    Utilisez l'API Text Analytics pour analyser des sentiments et des phrases clés. Le code ci-dessous montre comment appeler l'API à partir d'un script Python.

Code Python pour appeler l'API Text Analytics :

import requests
import json

# Remplacer avec votre clé API et point de terminaison
subscription_key = "7f6672af0db04f42a124d955ba97d8cb"
endpoint = "https://cognitiveservicelab8.cognitiveservices.azure.com/"

# URL de l'API pour l'analyse des sentiments
sentiment_url = endpoint + "text/analytics/v3.1/sentiment"
key_phrase_url = endpoint + "text/analytics/v3.1/keyPhrases"

# Texte à analyser
documents = {
    "documents": [
        {"id": "1", "language": "fr", "text": "J'ai acheté ce produit récemment et il fonctionne très bien ! Je suis très satisfait du service et de la qualité."}
    ]
}

# Analyser le sentiment
headers = {"Ocp-Apim-Subscription-Key": subscription_key}
response = requests.post(sentiment_url, headers=headers, json=documents)
sentiment_analysis = response.json()

print("Analyse des sentiments :")
print(json.dumps(sentiment_analysis, indent=2))

# Analyser les phrases clés
response = requests.post(key_phrase_url, headers=headers, json=documents)
key_phrases_analysis = response.json()

print("\nAnalyse des phrases clés :")
print(json.dumps(key_phrases_analysis, indent=2))


Exécution :
Installez la bibliothèque Python requests si elle n'est pas déjà installée :

pip install requests

Exécutez le script TestAnalyzer.py dans votre environnement Python pour envoyer une requête à l'API et analyser le texte :

python TestAnalyzer.py

Étape 3 : Analyser les résultats de l'API

    Utilisez l'application pour analyser des sentiments et des phrases clés à partir de textes d'exemple. Le résultat de l'API sera imprimé en JSON, contenant le score de sentiment (positif, négatif, neutre) pour chaque document analysé.

Étape 4 : Surveillance Activités API
![alt text](<surveillance API requests.png>)