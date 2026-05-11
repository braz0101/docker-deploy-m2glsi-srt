# 🐳 Déploiement Docker — Application M2-GLSI-SRT

**ESP Dakar · UCAD — Master 2 GLSI / SRT | 2025–2026**  
**Auteur : Ibrahima FALL**  
Cours : Infrastructure de virtualisation — Dr Mandicou Ba

Déploiement Dockerisé d'une application Full Stack (React + Node.js + MySQL) dédiée à l'analyse d'images par intelligence artificielle.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────┐
│           Docker Compose                │
│                                         │
│  ┌──────────────┐   ┌────────────────┐  │
│  │  ibrahimafall│   │ ibrahimafall   │  │
│  │     _app     │──▶│     _db        │  │
│  │ Node.js:3000 │   │  MySQL 8.0     │  │
│  │ port 7865    │   │  dic2iabd_db   │  │
│  └──────────────┘   └────────────────┘  │
└─────────────────────────────────────────┘
```

- **Frontend** : React + Vite (build statique servi par Express)
- **Backend** : Node.js / Express
- **Base de données** : MySQL 8.0 avec persistance via volume Docker

---

## 📁 Fichiers

| Fichier | Description |
|---|---|
| `Dockerfile` | Build multi-stage (build React + production Node.js) |
| `docker-compose.yml` | Orchestration des deux conteneurs |
| `historique_commandes.txt` | Historique complet des commandes exécutées sur le serveur |

---

## 🚀 Déploiement

```bash
# Cloner le dépôt dans le dossier de l'application
git clone <repo-url>

# Lancer les conteneurs
docker compose up -d --build

# Vérifier que tout tourne
docker compose ps
docker compose logs app
```

L'application est accessible sur : **http://localhost:7865**

---

## 🔧 Dockerfile — Build multi-stage

```
Stage 1 (builder) : node:18-alpine
  → npm install + npm run build (compile le frontend React/Vite)

Stage 2 (production) : node:18-alpine
  → npm install --omit=dev
  → copie du dist/ compilé
  → node server.js (sert le frontend + API)
```

---

## ⚙️ Variables d'environnement

| Variable | Valeur par défaut |
|---|---|
| `DB_HOST` | `db` |
| `DB_USER` | `root` |
| `DB_PASSWORD` | `rootpassword` |
| `DB_NAME` | `dic2iabd_db` |
| `PORT` | `3000` |

---

## 📋 Commandes utiles

```bash
# Arrêter les conteneurs
docker compose down

# Arrêter et supprimer les volumes
docker compose down -v

# Voir les logs en temps réel
docker compose logs -f app

# Inspecter la base de données
docker exec -it ibrahimafall_db mysql -u root -prootpassword dic2iabd_db
```

---

## 👤 Auteur

**Ibrahima FALL** — Master 2 SRT / GLSI  
ESP Dakar · UCAD · 2025–2026
