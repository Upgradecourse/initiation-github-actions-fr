# Concepts avancés

## 🚀 Objectif

Comprendre et utiliser des concepts plus avancés dans GitHub Actions, tels que :

- Les **jobs multiples**
- L'**ordre d'exécution** entre jobs
- L'utilisation de **secrets** pour sécuriser des informations sensibles
- La **définition de variables** (`env`)

---

## 🛠️ 1. Les jobs multiples

Un **workflow** peut contenir **plusieurs jobs** qui s'exécutent :

- **En parallèle** (par défaut)
- **Ou de manière dépendante** (si on définit un ordre avec `needs:`)

---

### Exemple de workflow avec plusieurs jobs :

```yaml
name: Workflow avec plusieurs jobs
on: push

jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
      - name: Premier job
        run: echo "Ceci est le job 1"

  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - name: Deuxième job (attend job1)
        run: echo "Ceci est le job 2"
```

🛠️ Ici :

job2 attend que job1 soit terminé avant de s'exécuter.

Sinon, les jobs sont parallèles par défaut.

---

## 🛡️ 2. Utiliser des secrets GitHub

Pour **protéger des informations sensibles** (mot de passe, clé API...), GitHub permet d'utiliser des **secrets**.

### Exemple :

```yaml
name: Utiliser un secret
on: push

jobs:
  afficher-secret:
    runs-on: ubuntu-latest
    steps:
      - name: Afficher un secret
        run: echo "La clé secrète est ${{ secrets.MA_CLE_API }}"
```

💬 **Attention :**  
Ne jamais écrire directement vos mots de passe dans les fichiers YAML !  
Utilisez toujours `${{ secrets.NOM_DU_SECRET }}`.

---

## 🌍 3. Définir des variables d'environnement (`env`)

Vous pouvez définir des **variables** pour éviter de répéter du code ou pour faciliter la maintenance.

### Exemple :

```yaml
name: Variables d'environnement
on: push

jobs:
  afficher-env:
    runs-on: ubuntu-latest
    env:
      MON_MESSAGE: "Bonjour à tous !"
    steps:
      - name: Afficher le message
        run: echo "$MON_MESSAGE"
```

🛠️ **Ici** :  
La variable `MON_MESSAGE` est définie dans l'environnement du job.  
Vous pouvez accéder à cette variable dans toutes les étapes du job en utilisant `$MON_MESSAGE`.

## ✅ Résumé du chapitre

| Concept          | Utilité                                                  |
|:-----------------|:---------------------------------------------------------|
| Jobs multiples   | Organiser plusieurs tâches dans un même workflow        |
| Secrets          | Sécuriser des mots de passe et des clés API              |
| Variables `env`  | Rendre les workflows plus lisibles et maintenables       |




