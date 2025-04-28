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

---

## ✍️ Exercice : Créer un workflow avec plusieurs jobs, secrets et variables d'environnement

### Objectifs :
- Créer un workflow avec **deux jobs**.
- Utiliser un **secret** pour protéger une clé API (par exemple, `MY_API_KEY`).
- Utiliser une **variable d'environnement** pour afficher un message personnalisé dans les logs.

### 🛠️ Instructions :

1. Créez un fichier workflow dans `.github/workflows/exercice-avance.yml` avec le contenu suivant :

```yaml
name: Exercice avec jobs, secrets et variables d'environnement
on: push

jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout du code
        uses: actions/checkout@v4
        
      - name: Vérifier que le fichier README.md est présent
        run: |
          if [ -f README.md ]; then
            echo "✅ Le fichier README.md est bien présent !"
          else
            echo "❌ Attention : aucun README.md trouvé."
            exit 1
          fi

  job2:
    runs-on: ubuntu-latest
    needs: job1
    env:
      MESSAGE: "N'oubliez pas : ne laissez jamais vos secrets visibles dans vos workflows !"
    steps:
      - name: Afficher un message personnalisé avec la variable d'environnement
        run: echo "$MESSAGE"
      
      - name: Utiliser un secret dans les logs
        run: echo "La clé API est : ${{ secrets.MY_API_KEY }}"
```

2. **Ajoutez le secret `MY_API_KEY` dans la section "Secrets" de votre dépôt :**

   - Allez dans **Settings** > **Secrets and Variables** > **Actions** > **New repository secret**.
   - Nommez-le `MY_API_KEY` et entrez une valeur (exemple fictif pour un token ou clé API).
   
   🛠️ **Exemple de valeur pour un secret** :  
   ```text
   1234567890abcdef
   ```
3. **Effectuez un push** pour tester le workflow

---

4. **Resultats attendus**

## Job 2 : Affichage du message personnalisé et du secret dans les logs

Dans **Job 2**, nous allons afficher deux éléments dans les logs :

1. **Message personnalisé** : Affichage du message défini par la variable d'environnement `MESSAGE`.

2. **Secret dans les logs** : Utilisation du secret `MY_API_KEY`.  
   **Note importante** : Les secrets ne sont **pas affichés en clair** dans les logs. GitHub remplace le contenu réel par `***` pour protéger les informations sensibles.

### Exemple de résultat dans les logs :

```text
✅ Le fichier README.md est bien présent !
La clé API est : ***
```







