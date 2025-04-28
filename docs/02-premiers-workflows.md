# 🎯 Créer son premier vrai workflow GitHub Actions

Maintenant que vous avez vu un premier exemple simple, nous allons créer un workflow un peu plus complet pour vous familiariser avec la structure de base.

---

## 🚀 Objectif

Créer un workflow qui :

- S'exécute à chaque `push`
- Vérifie que le dépôt contient un fichier `README.md`
- Affiche un message personnalisé dans les logs

---

## 🛠️ Le code complet

Voici le fichier à créer dans `.github/workflows/premier-workflow.yml` :

```yaml
name: Premier vrai workflow
on: push

jobs:
  verifier-fichiers:
    runs-on: ubuntu-latest
    steps:
      - name: Vérifier la présence d'un README
        run: |
          if [ -f README.md ]; then
            echo "✅ Le fichier README.md est bien présent !"
          else
            echo "❌ Attention : aucun README.md trouvé."
            exit 1
          fi
      - name: Afficher un message final
        run: echo "🎉 Fin du workflow avec succès."
```
