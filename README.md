# 🛡️ Defense-AI

Un système intelligent de défense et contre-attaque basé sur IA avec réseau de neurones et brute force contrôlé.

## 📋 Description

**Defense-AI** est un système de sécurité automatisé qui:

1. **Détecte les menaces** via un réseau de neurones entraîné sur des données Kaggle
2. **Défend le système** en temps réel (blocage IP, isolation connexions)
3. **Contre-attaque** une fois sécurisé (identification attaquant, analyse)

### Caractéristiques principales:
- ✅ Analyse des logs réseau en temps réel (local uniquement)
- ✅ Réseau de neurones TensorFlow/Keras pour prédiction
- ✅ Base de données SQLite chiffrée (données sensibles locales)
- ✅ Défense automatique prioritaire
- ✅ Contre-attaque intelligente (brute force contrôlé)
- ✅ Entraînement avec datasets Kaggle

---

## 🏗️ Architecture

```
┌─────────────────────────────────────┐
│    PHASE 1: ENTRAÎNEMENT (Kaggle)   │
│  NSL-KDD / CICIDS2017 → Modèle IA   │
└─────────────┬───────────────────────┘
              ↓
┌─────────────────────────────────────┐
│   PHASE 2: PRODUCTION (Local)       │
│  Logs → IA → Défense → Contre-Attack│
└─────────────────────────────────────┘
```

---

## 📁 Structure du Projet

```
Defense-ai/
│
├── data/
│   ├── raw/                    # Données brutes Kaggle
│   ├── processed/              # Données nettoyées
│   ├── database/               # SQLite chiffré (PRODUCTION)
│   ├── logs/                   # Logs réseau temps réel
│   └── models/                 # Modèles entraînés (.h5)
│
├── modules/
│   ├── training/               # Entraînement (Kaggle)
│   │   ├── download_kaggle.py
│   │   ├── preprocess.py
│   │   ├── feature_engineering.py
│   │   └── train_model.py
│   │
│   ├── production/             # Production (Local)
│   │   ├── collector/          # Capture logs réseau
│   │   ├── ai/                 # Prédictions
│   │   ├── defense/            # Actions défense
│   │   └── counterattack/      # Contre-attaque
│   │
│   └── utils/
│       ├── database.py         # Gestion SQLite
│       ├── encryption.py       # Chiffrage données
│       └── helpers.py
│
├── scripts/
│   ├── train.py               # Lancer entraînement
│   └── run_defense.py         # Lancer production
│
├── config/
│   ├── settings.py            # Configuration
│   └── logger.py              # Logging
│
├── requirements.txt           # Dépendances Python
├── .gitignore                # Fichiers ignorés
└── README.md                 # Ce fichier
```

---

## 🚀 Installation

### Prérequis
- Python 3.8+
- pip
- Git

### Étape 1: Cloner le repo

```bash
git clone https://github.com/alenberyl-ship-it/Defense-ai.git
cd Defense-ai
```

### Étape 2: Créer un environnement virtuel

```bash
# Linux/Mac:
python3 -m venv venv
source venv/bin/activate

# Windows:
python -m venv venv
venv\Scripts\activate
```

### Étape 3: Installer les dépendances

```bash
pip install -r requirements.txt
```

### Étape 4: Configurer Kaggle (pour entraînement)

```bash
# Télécharger token depuis: https://www.kaggle.com/settings/account
mkdir -p ~/.kaggle
mv ~/Downloads/kaggle.json ~/.kaggle/
chmod 600 ~/.kaggle/kaggle.json
```

---

## 📊 Phase 1: Entraînement (Une seule fois)

### Télécharger les données Kaggle

```bash
python scripts/train.py --download-kaggle
```

### Prétraiter les données

```bash
python scripts/train.py --preprocess
```

### Entraîner le modèle IA

```bash
python scripts/train.py --train
```

### Évaluer le modèle

```bash
python scripts/train.py --evaluate
```

**Résultat:** Un fichier `data/models/threat_model.h5` est créé.

---

## 🛡️ Phase 2: Production (En continu)

### Lancer le système de défense

```bash
python scripts/run_defense.py
```

Le système va:
1. ✅ Capturer les logs réseau locaux
2. ✅ Utiliser le modèle IA pour prédictions
3. ✅ Stocker les données dans SQLite (local)
4. ✅ Défendre automatiquement si menace
5. ✅ Contre-attaquer après sécurisation

---

## 🧠 Datasets Kaggle Disponibles

| Dataset | Lien | Utilisation |
|---------|------|-------------|
| NSL-KDD | https://www.kaggle.com/datasets/hassan06/nslkdd | Intrusion Detection |
| CICIDS2017 | https://www.kaggle.com/datasets/cicdataset/cicids2017 | Trafic réel + Attaques |
| CICIDS2018 | https://www.kaggle.com/datasets/solarmainframe/ids-intrusion-csv | Plus récent |
| UNSW-NB15 | https://www.kaggle.com/datasets/mrinallohan/unswnb15 | Cybersécurité complet |

---

## 🔒 Sécurité des Données

- ✅ Base de données **SQLite chiffrée** localement
- ✅ Aucune donnée **ne quitte le système**
- ✅ Logs sensibles **jamais en mémoire**
- ✅ Modèle IA **stocké localement seulement**
- ✅ **Permissions restrictives** sur fichiers sensibles

---

## 📋 Flux de Travail Complet

```
1. ENTRAÎNEMENT
   Kaggle Dataset → Feature Engineering → Réseau Neuronal
   → Modèle sauvegardé (.h5)

2. PRODUCTION
   Logs Réseau → Parser → Features → Prédiction IA
   → Décision (Normal/Vigilance/Menace)
   → Défense (Si menace détectée)
   → Contre-attaque (Une fois sécurisé)
   → BD SQLite (Enregistrement)
```

---

## 🛠️ Configuration

Éditer `config/settings.py` pour:
- Seuils de menace (30/70)
- Paramètres modèle IA
- Chemins fichiers
- Logging

---

## 📝 Logs et Monitoring

Les logs sont stockés dans:
- `data/logs/` - Logs réseau bruts
- `data/database/defense_ai.db` - Base de données incidents

```bash
# Voir les logs en temps réel
tail -f data/logs/defense.log
```

---

## 🤝 Contribution

Les contributions sont bienvenues! Pour contribuer:

1. Fork le projet
2. Créer une branche (`git checkout -b feature/Nom-Feature`)
3. Commit vos changes (`git commit -m 'Add feature'`)
4. Push vers la branche (`git push origin feature/Nom-Feature`)
5. Ouvrir une Pull Request

---

## 📄 Licence

Ce projet est sous licence MIT - voir `LICENSE` pour détails.

---

## 👤 Auteur

**alenberyl-ship-it**

- GitHub: [@alenberyl-ship-it](https://github.com/alenberyl-ship-it)

---

## 📞 Support

Pour des questions ou problèmes:
1. Vérifiez la [Documentation](./docs/)
2. Ouvrez une [Issue GitHub](https://github.com/alenberyl-ship-it/Defense-ai/issues)
3. Consultez le [Wiki](https://github.com/alenberyl-ship-it/Defense-ai/wiki)

---

## 🎯 Roadmap

- [ ] Phase 1: Collecteur logs réseau
- [ ] Phase 2: Feature extraction
- [ ] Phase 3: Réseau de neurones
- [ ] Phase 4: Défense automatique
- [ ] Phase 5: Contre-attaque intelligente
- [ ] Phase 6: Dashboard web
- [ ] Phase 7: API REST

---

**Fait avec ❤️ pour la cybersécurité**
