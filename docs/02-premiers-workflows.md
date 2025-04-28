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
      - name: Checkout du code
        uses: actions/checkout@v4
    
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

💡 **Attention :**  
Le fichier `README.md` doit être placé **directement à la racine du dépôt**.  
Si vous placez le `README.md` dans un sous-dossier (par exemple `docs/README.md` ou `readme/README.md`),  
le workflow **ne le trouvera pas** et l'étape de vérification échouera.  
Assurez-vous que le fichier `README.md` est visible dès l'accueil du dépôt GitHub.

---

🚀 Déclencher le workflow
Maintenant que votre fichier premier-workflow.yml est en place, il faut déclencher le workflow pour le tester.

Pour cela, vous devez provoquer un événement push.

🛠️ Que faire pour déclencher le workflow ?
Par exemple, ajoutez un simple fichier vide (comme test.txt) à la racine de votre dépôt.

Ou modifiez un autre fichier existant (autre que README.md si possible).

Faites un commit et poussez votre changement.

👉 Dès que GitHub détecte un push, votre workflow se déclenchera automatiquement.


Après avoir effectué un push :

Allez dans l'onglet Actions de votre dépôt GitHub.

Vous verrez votre nouveau workflow "Premier vrai workflow" en cours ou terminé.

Dans les logs :

✅ Un message vous indique si le README.md est présent.

🎉 Un message confirme la fin du workflow.

📸 Résultat attendu

![Résultat du workflow réussi](../assets/workflow-success-premier.png)


🔎 Explication des lignes importantes du workflow
🛠️ uses: actions/checkout@v4
Cette étape permet de télécharger (cloner) votre dépôt GitHub dans la machine virtuelle du runner.
Sans elle, la machine est vide et ne peut pas accéder à vos fichiers (README.md, etc.).

📋 Vérification du README

if [ -f README.md ]; then
Cette commande vérifie si le fichier README.md existe à la racine du dépôt.

Si oui ➔ ✅ Message de succès

Si non ➔ ❌ Message d'échec et le workflow échoue (exit 1)







