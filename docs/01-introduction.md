# Introduction à GitHub Actions

Bienvenue dans ce premier chapitre d'**initiation à GitHub Actions** !

---

## 🛠️ Avant de commencer

Avant de suivre ce tutoriel, assurez-vous de :

1. **Créer un nouveau dépôt GitHub**  
   👉 Nom recommandé : `initiation-github-actions`  
   👉 Choisissez Public ou Privé selon votre préférence.  
   👉 Initialisez avec un fichier README.

2. **Créer le dossier **wokflows** dans votre dépôt** : .github/workflows/

ℹ️ **Note :** Le dossier `.github` est un **dossier caché**.  
Il est **visible sur la plateforme GitHub**, mais si vous travaillez en local via la CLI (terminal), pensez à utiliser la commande suivante pour l'afficher : ls -la

3. **Travailler soit directement sur GitHub, soit en clonant votre dépôt en local.**

---

## 🤔 Qu'est-ce que GitHub Actions ?

GitHub Actions est une plateforme d'automatisation directement intégrée à GitHub.  
Elle permet d'exécuter des scripts ou des processus automatiquement en fonction d'événements, comme un push de code, une création de pull request, ou un nouveau tag.

Quelques exemples d'utilisation :
- Compiler et tester votre code à chaque push
- Déployer une application automatiquement
- Gérer des workflows personnalisés (label automatique, messages de bienvenue, etc.)

---

## 🛠️ Comment fonctionne GitHub Actions ?

Un workflow est défini dans un fichier **YAML** (extension `.yml`) placé dans le dossier spécial `.github/workflows/` de votre projet.

Un workflow est composé :
- D'un ou plusieurs **événements déclencheurs** (exemple : un push, une pull request)
- De **jobs** qui contiennent
  - **steps** (étapes) qui effectuent des actions spécifiques
  - **actions** (des scripts réutilisables, créés par GitHub ou la communauté)

---

## 📋 Exemple ultra simple

Voici un mini exemple de workflow qui s'exécute à chaque `push` :

```yaml
name: Exemple simple
on: push

jobs:
  dire-bonjour:
    runs-on: ubuntu-latest
    steps:
      - name: Message de bienvenue
        run: echo "Bonjour GitHub Actions ! 🚀"
```

---

## 🚀 Tester cet exemple

Vous pouvez essayer cet exemple vous-même !

1. Créez un dossier `.github/workflows/` dans votre dépôt GitHub.
2. Créez un fichier nommé `exemple-hello.yml` dans ce dossier.
3. Copiez-collez le code YAML ci-dessus dans ce fichier.
4. Faites un `commit` et poussez vos modifications sur GitHub.

👉 Résultat attendu : une action s'exécutera automatiquement et affichera "Bonjour GitHub Actions !" dans l'onglet **Actions** de votre dépôt.

---

## 🔎 Explication rapide du fichier

- **name** : donne un nom visible au workflow.
- **on: push** : le workflow se déclenche à chaque `push` sur le dépôt.
- **jobs** : définit les différentes tâches à exécuter.
- **dire-bonjour** : le nom donné à ce job.
- **runs-on: ubuntu-latest** : GitHub utilise une machine virtuelle Ubuntu pour exécuter le job.
- **steps** : liste des actions à réaliser.
- **Message de bienvenue** : le nom donné à cette étape (step).
- **run: echo "Bonjour GitHub Actions !"** : affiche un message dans les logs.

---
