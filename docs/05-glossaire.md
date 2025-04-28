# 📚 Glossaire GitHub Actions

Bienvenue dans ce glossaire des principaux termes utilisés dans GitHub Actions.

---

## 📄 Workflow

Un **workflow** est un fichier de configuration (format YAML) qui décrit une ou plusieurs tâches automatiques à exécuter sur GitHub.

➡️ **Exemples** : lancer des tests, compiler un projet, envoyer une notification.

---

## 🔔 Événement (event)

Un **événement** est une action qui déclenche l'exécution d'un workflow.

➡️ **Exemples** : un push de code, l'ouverture d'une pull request, la création d'une issue.

---

## 🛠️ Job

Un **job** est un ensemble d'étapes (steps) qui s'exécutent dans un environnement donné.

➡️ Tous les steps d'un même job s'exécutent sur le même runner.

---

## 📋 Étape (step)

Une **étape** est une action individuelle au sein d'un job.

Elle peut :
- Exécuter une commande (`run:`)
- Utiliser une Action GitHub existante (`uses:`)

➡️ **Exemples** : `run: npm install`, `run: echo "Hello"`

---

## ⚙️ Action GitHub

Une **Action** est un outil réutilisable (créé par GitHub ou la communauté) que vous pouvez intégrer dans vos steps.

➡️ **Exemples** : action pour envoyer des notifications Slack, déployer sur AWS.

---

## 🚀 Runner

Un **runner** est la machine virtuelle fournie par GitHub pour exécuter vos workflows.

➡️ **Exemples** : Ubuntu, Windows, MacOS (`runs-on: ubuntu-latest`).

---

## 🔒 Secret

Un **secret** est une valeur sécurisée (mot de passe, clé API...) utilisée dans vos workflows sans être exposée publiquement.

➡️ **Exemple** : `${{ secrets.MY_SECRET_KEY }}`

---

# ✅ Comment utiliser ce glossaire ?

- Revenir ici dès qu'un terme vous semble flou.
- Comprendre chaque notion avant d'aller plus loin dans la création de workflows.

---
