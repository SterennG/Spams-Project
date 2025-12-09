# AT&T - Détection automatisée de spams SMS

## Contexte et objectif
AT&T, géant des télécommunications, fait face à une problématique majeure : l'exposition constante de ses utilisateurs aux SMS indésirables (spams). L'objectif de ce projet est de développer une solution d'intelligence artificielle capable de **détecter et filtrer automatiquement les spams** en se basant uniquement sur le contenu textuel des messages.

## Données
Le projet utilise un jeu de données de SMS étiquetés :
* **Ham (légitime) :** ~87% des messages (sphère privée, conversationnelle).
* **Spam (indésirable) :** ~13% des messages (urgence, incitation à l'achat, commercial).
* *Observation clé :* Les spams sont structurellement plus longs et utilisent un vocabulaire spécifique (ex: "FREE", "Call", "URGENT").

## Méthodologie technique
Nous avons adopté une approche progressive pour valider la complexité nécessaire du modèle :

1.  **Preprocessing & EDA :**
    * Tokenization (via `tiktoken` puis `DistilBERT tokenizer`).
    * Analyse de la distribution des longueurs et des fréquences de mots.
2.  **Modèle Baseline (Word Embedding) :**
    * Réseau de neurones simple (Embedding + Pooling + Dense).
    * *But :* établir une performance de référence rapide.
3.  **Modèle Intermédiaire (CNN 1D) :**
    * Réseau convolutif pour capter les motifs locaux (n-grammes).
4.  **Modèle Avancé (Transfer Learning) :**
    * Utilisation de **DistilBERT** (Transformer pré-entraîné).
    * *But :* compréhension sémantique et contextuelle profonde.

## Résultats et Performance
Le modèle **DistilBERT** (Fine-tuned) a été retenu pour le déploiement.

| Modèle | Accuracy | Précision Spam | Rappel Spam | F1-Score |
| :--- | :--- | :--- | :--- | :--- |
| **Baseline** | 98.9% | 0.97 | 0.93 | 0.95 |
| **CNN 1D** | 99.0% | 0.99 | 0.93 | 0.96 |
| **DistilBERT** | **100%** | **1.00** | **0.97** | **0.99** |

*Note : DistilBERT a réalisé un score parfait de 0 Faux Positifs sur le jeu de test, garantissant qu'aucun message légitime n'est bloqué par erreur.*

## Installation et Prérequis
Le projet a été réalisé sous Python avec les librairies principales suivantes :
* `torch` (PyTorch)
* `transformers` (Hugging Face)
* `sklearn`
* `pandas` / `numpy`
* `plotly` (Visualisation)


Pour lancer le notebook :
```bash
pip install torch transformers scikit-learn pandas plotly tiktoken spacy torchinfo
```

---
Auteure : Stérenn GÉLÉOC 

Projet réalisé dans le cadre de la certification CDSD (Concepteur Développeur en Science des Données) \
Bloc 4 - Analyse prédictive de données non-structurées par l'intelligence artificielle

JEDHA | Fullstack Data Science - Deep Learning Project | 2025