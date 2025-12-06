## 🧠 Mini RAG

Ce projet présente un système RAG (Retrieval-Augmented Generation) complet permettant d'interroger un document PDF via un chatbot intelligent.
Il combine LangChain, FAISS, BGE embeddings, reranking et une génération locale via Ollama.

### 🚀 Fonctionnalités

- Chargement automatique d’un PDF (ex : Syntec Conseil – Métiers de la Data)

- Découpage intelligent du texte en chunks

- Vectorisation avec le modèle BAAI/bge-m3

- Recherche sémantique via FAISS

- Reranking des passages avec BAAI/bge-reranker-v2-m3

- Génération locale avec mistral:instruct (Ollama)

- Interface Streamlit simple pour poser des questions

- Pipeline optimisé : MMR + Reranker + Prompt anti-hallucination

### Structure du projet :

MiniRAG/

│── My_Sreamlit_app.py           # Interface Streamlit

│── MiniRAG_Djebril_LAOUEDJ.ipynb # Notebook du projet

│── requirements.txt             # Versions exactes testées

│── README.md                    # Documentation

│── .gitignore                   # Fichiers ignorés

└── data/                        # (Optionnel) PDF d'exemple

### 📘 Exemple de pipeline RAG

Voici la logique générale du projet :

- Charger le PDF

- Chunking du texte

- Génération des embeddings (BGE-M3)

- Indexation FAISS

- Retrieval (MMR)

- Reranking (BGE-Reranker)

- Génération via Mistral:instruct (Ollama)

### ⚙️ Installation

1️⃣ Cloner le projet

git clone https://github.com/djbrl-laouedj/MiniRAG.git
cd MiniRAG

2️⃣ Installer les dépendances

⚠️ Les versions sont exactes pour éviter les conflits LangChain. Merci d'utiliser requirements.txt.

pip install -r requirements.txt

3️⃣ Installer Ollama (si pas déjà installé)

➡️ https://ollama.com/download

Puis télécharger le modèle utilisé :

ollama pull mistral:instruct

▶️ Lancer l'application Streamlit

streamlit run app.py

L’interface s’ouvre automatiquement dans le navigateur.

### Sur Google Colab :

Téléchargez tous les fichiers.

🔧 Configuration ngrok

Si vous voulez exposer votre interface Streamlit :

Créer un compte : https://ngrok.com

Récupèrez votre clé : https://dashboard.ngrok.com/get-started/your-authtoken

Puis ajoutez-cela à la fin d evotre code :

from pyngrok import ngrok
ngrok.set_auth_token("<VotreClé>")

!streamlit run My_Sreamlit_app.py &>/dev/null &

public_url = ngrok.connect(8501)
public_url

Et ce code pour relancer le streamlit :

// stop tous les tunnels ngrok pour repartir propre
from pyngrok import ngrok
try:
    ngrok.kill()
except:
    pass

### Voilà pour finir un mini user-guide :

1. Uploader un PDF :

<img width="230" height="174" alt="image" src="https://github.com/user-attachments/assets/68d63482-dab0-4fd7-9da6-eb2c532127a1" />

2. Puis lancer la pipeline :

<img width="228" height="73" alt="image" src="https://github.com/user-attachments/assets/1283f0f6-4c97-4e82-8e59-24a076c70c15" />

3. Une fois fini, poser une question (exemple : Quelle est le rôle d'un Data Engineer)

<img width="1599" height="809" alt="image" src="https://github.com/user-attachments/assets/ecf844b9-4725-402d-8bd0-124febe23a01" />

4. Résultat (les sources peuvent être vues ou non)

<img width="1550" height="694" alt="image" src="https://github.com/user-attachments/assets/ba5e04cc-467a-40ae-8506-52ae47a5799f" />

5. Malheureusement, si la question posé ne peut pas être répondu (par manque d'informations dans les données jointes), le chatbot retournera cela :

<img width="1028" height="154" alt="image" src="https://github.com/user-attachments/assets/fb838479-3c1a-4307-97ba-a94f3b706254" />

💡 Améliorations possibles

Ajouter plusieurs PDF (multi-corpus RAG)

Améliorer l’UI Streamlit

Support des images / tableaux

Passage à un LLM plus puissant (ex : Llama 3.1 8B)

👤 Auteur

Projet réalisé par Djebril Laouedj
Étudiant en 5ème année en Big Data & IA – ECE Paris.
