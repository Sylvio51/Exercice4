Voici une procédure détaillée pas à pas pour réaliser l'exercice de collaboration sur un dépôt distant avec GitHub. Vous pouvez adapter ces commandes et explications selon vos besoins et vos environnements locaux (Adam et Eve).

1. Créer un dépôt GitHub
Connectez-vous à GitHub et cliquez sur "New repository".
Donnez un nom (ex. collaboration-exo), choisissez la visibilité (publique ou privée) et initialisez (ou non) avec un README.
2. Cloner le dépôt dans deux destinations différentes (Adam & Eve)
Sur la machine d’Adam :

bash
Copier
git clone https://github.com/votre-utilisateur/collaboration-exo.git ~/adam-collaboration
Sur la machine d’Eve (ou dans un dossier différent sur la même machine pour simuler la collaboration) :

bash
Copier
git clone https://github.com/votre-utilisateur/collaboration-exo.git ~/eve-collaboration
3. Adam effectue un commit et pousse sur le dépôt distant
Sur le répertoire d’Adam :

Créez ou modifiez un fichier, par exemple README.md ou un fichier de test.
Ajoutez les modifications et effectuez le commit :
bash
Copier
cd ~/adam-collaboration
echo "Première modification d'Adam" >> fichier.txt
git add fichier.txt
git commit -m "Commit d'Adam : ajout de fichier.txt"
Poussez le commit sur le dépôt distant :
bash
Copier
git push origin main
4. Eve récupère le commit d’Adam
Sur le répertoire d’Eve :

Vérifiez l’historique (optionnel) :
bash
Copier
git log --oneline
Récupérez les modifications du dépôt distant :
bash
Copier
git pull origin main
5. Eve crée une branche feature/login et effectue un commit, puis pousse
Sur le répertoire d’Eve :

Créez et basculez sur la branche :
bash
Copier
git checkout -b feature/login
Modifiez ou créez un fichier (par exemple login.html) et effectuez un commit :
bash
Copier
echo "<!-- Nouvelle fonctionnalité de login -->" > login.html
git add login.html
git commit -m "Ajout de la page login dans feature/login"
Poussez la branche sur le dépôt distant :
bash
Copier
git push -u origin feature/login
6. Afficher les branches locales et distantes
Pour voir l’ensemble des branches sur Eve :

bash
Copier
git branch -a
Cela affichera les branches locales (ex. main, feature/login) et les branches distantes (ex. origin/main, origin/feature/login).

7. Adam synchronise son dépôt et récupère la branche feature/login
Sur le répertoire d’Adam :

Affichez les logs de manière graphique et condensée (si vous avez un alias lga ou directement avec git log) :
bash
Copier
git log --graph --oneline --all
Notez la présence de la branche origin/feature/login.
Créez une branche locale qui suit la branche distante :
bash
Copier
git checkout -b feature/login origin/feature/login
Vérifiez ensuite les branches locales et distantes :
bash
Copier
git branch -a
8. Eve fait un nouveau commit et pousse sur la branche feature/login
Sur le répertoire d’Eve :

Effectuez une modification (par exemple, modifiez login.html) :
bash
Copier
echo "<!-- Modification supplémentaire -->" >> login.html
Ajoutez et commitez les changements :
bash
Copier
git add login.html
git commit -m "Mise à jour de login.html : modification supplémentaire"
Poussez le commit sur la branche distante :
bash
Copier
git push
9. Adam récupère les modifications d’Eve dans feature/login
Sur le répertoire d’Adam (en étant sur la branche feature/login) :

Récupérez les changements depuis le dépôt distant :
bash
Copier
git pull
Vérifiez l’historique des commits pour confirmer la présence du nouveau commit :
bash
Copier
git log --oneline --graph
10. Mettre à jour la branche main distante via une Pull Request
Connectez-vous à GitHub et allez sur votre dépôt.
Vous verrez généralement une notification indiquant que la branche feature/login propose des changements par rapport à main.
Cliquez sur "Compare & pull request".
Rédigez un commentaire si nécessaire, puis cliquez sur "Create pull request".
Une fois la PR validée, cliquez sur "Merge pull request" pour fusionner les changements dans main.
11. Supprimer la branche distante et la branche locale
Sur GitHub (pour supprimer la branche distante) :

Cliquez sur "Delete branch" dans l’interface de la pull request après le merge.
Ou en ligne de commande :
bash
Copier
git push origin --delete feature/login
Sur le dépôt local (sur Adam ou Eve) :

bash
Copier
git branch -d feature/login
12. Eve synchronise ses sources et met à jour sa branche main locale
Sur le répertoire d’Eve :

Récupérez les dernières sources du dépôt distant :
bash
Copier
git fetch --all
Passez sur la branche main :
bash
Copier
git checkout main
Intégrez les changements de origin/main dans votre branche locale :
bash
Copier
git pull origin main
Vérifiez l’historique pour confirmer que main et origin/main sont synchronisés :
bash
Copier
git log --oneline --graph
13. Supprimer définitivement la branche feature/login (si elle existe encore)
Si la branche feature/login existe toujours sur Eve (ou ailleurs), supprimez-la localement et sur le distant :

Supprimer la branche locale (si nécessaire) :
bash
Copier
git branch -d feature/login
Supprimer la branche distante (si ce n’est pas déjà fait) :
bash
Copier
git push origin --delete feature/login
Conclusion