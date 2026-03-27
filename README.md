# ⚡ QuizLive — Quiz interactif type Kahoot

Application web de quiz en temps réel : un professeur lance des questions chronométrées, les étudiants répondent sur leurs téléphones, les résultats s'affichent instantanément pour tout le monde.

---

## 🚀 Démarrage rapide

### Prérequis
- Python 3.9+
- pip

### Lancement (Windows)
Double-cliquez sur `run.bat`  
**ou** depuis le terminal :

```bash
pip install -r requirements.txt
cd backend
python app.py
```

Le serveur démarre sur **http://localhost:5000**

---

## 🌐 Accès

| Rôle        | URL                              |
|-------------|----------------------------------|
| Accueil     | http://localhost:5000            |
| Professeur  | http://localhost:5000/prof       |
| Étudiant    | http://localhost:5000/student    |

> Pour que les étudiants se connectent depuis leurs téléphones, remplacez `localhost` par l'adresse IP de votre PC sur le réseau local (ex : `192.168.1.42:5000`).

---

## 🎮 Workflow

### Côté Professeur
1. Aller sur `/prof`
2. Importer un fichier CSV ou Excel de questions
3. Partager le **code de session** avec les étudiants
4. Choisir la durée du chrono (10 / 20 / 30 secondes)
5. Attendre que les étudiants rejoignent, puis lancer
6. Après chaque question : voir le graphique des réponses + classement
7. Passer à la question suivante jusqu'au classement final

### Côté Étudiant
1. Aller sur `/student` depuis le téléphone
2. Saisir le **code de session** + prénom
3. Attendre la question → cliquer sur une des 4 réponses
4. Voir si c'était correct + le classement
5. Répéter jusqu'à la fin

---

## 📋 Format des fichiers de test

### CSV ou Excel (.xlsx / .xls)
Colonnes obligatoires :

| Colonne        | Description                          |
|----------------|--------------------------------------|
| `question`     | Texte de la question                 |
| `reponse_1`    | Réponse A (rouge ▲)                  |
| `reponse_2`    | Réponse B (bleu ◆)                   |
| `reponse_3`    | Réponse C (orange ●)                 |
| `reponse_4`    | Réponse D (vert ★)                   |
| `bonne_reponse`| Numéro de la bonne réponse (1, 2, 3 ou 4) |
| `cours`        | Nom du cours (affiché comme badge)   |
| `sujet`        | Sujet / chapitre                     |

Un fichier exemple se trouve dans `data/exemple_test.csv`.

---

## 🗂 Structure du projet

```
Competitor/
├── backend/
│   └── app.py          ← Serveur Flask + WebSocket (SocketIO)
├── frontend/
│   ├── index.html      ← Page d'accueil
│   ├── prof.html       ← Interface professeur
│   ├── student.html    ← Interface étudiant
│   └── style.css       ← Styles partagés
├── data/
│   └── exemple_test.csv
├── requirements.txt
└── run.bat
```

---

## 🛠 Stack technique

- **Backend** : Python · Flask · Flask-SocketIO (WebSockets temps réel)
- **Parsing** : pandas · openpyxl · xlrd
- **Frontend** : HTML5 · CSS3 · JavaScript vanilla · Socket.IO (CDN)
- **Pas de base de données** : tout est en mémoire (sessions perdues au redémarrage)
