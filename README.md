# Dumb Task Manager

## Phase 1

### 1.1 - Test manuel de l'app individuel

| Element testé        | Observations                                                                                                                                                                                                                                                                                                      | Bug                                                                                                                                                                                                                                                                                | Piste d'amélioration                                                                                                                                                                                                |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Page d'accueil       | - Fond cyan uni très vif<br>- Un seul lien "go to login page"<br>- Interface minimaliste                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                    | - Améliorer le design général de la page<br>- Utiliser des couleurs moins agressives<br>- Styliser un bouton de connexion et d'inscription à la place du lien                                                       |
| Page de connexion    | - Même fond cyan vif que la page d'accueil<br>- Bouton "Login" non stylisé<br>- Pas de message d'erreur si le mot de passe est incorrecte                                                                                                                                                                         | - Crash de l'application si l'utilisateur n'existe pas                                                                                                                                                                                                                             | - Styliser le formulaire et les champs de saisie<br>- Ajouter des validations visuelles<br>- Améliorer le design du bouton Login<br>- Résoudre le problème de crash si l'utilisateur n'existe pas                   |
| Page d'inscription   | - Même fond cyan vif que la page d'accueil<br>- Formulaire basique avec champs Username, email et Password<br>- Bouton "Register !" non stylisé<br>- Aucune validation visuelle des champs<br>- Pas d'indication sur les critères de mot de passe<br>- Le champ du mot de passe n'est pas caché                   | - Pas de message d'erreur visible<br>- Pas de validation des champs en temps réel                                                                                                                                                                                                  | - Styliser le formulaire et les champs de saisie<br>- Ajouter des validations visuelles<br>- Améliorer le design du bouton Register <br>- Indiquer les critères de mot de passe                                     |
| Page après connexion | - Même fond cyan vif<br>- Un seul lien "click on the link" pour accéder aux tâches<br>- Aucune indication visuelle de connexion réussie<br>- Pas de menu de navigation<br>- Absence de bouton de déconnexion <br>- Navigation peu intuitive<br>- Pas de feedback de connexion réussie<br>- Pas de session visible | - Il est possible d'accéder à cette page pour n'importe quelle utilisateur via l'url et sans connexion                                                                                                                                                                             | - Ajouter un menu de navigation principal<br>- Afficher le nom de l'utilisateur connecté<br>- Ajouter un bouton de déconnexion<br>- Empecher d'accèder à cette page si on n'est pas connecté, et avec le bon compte |
| Page des tâches      | - Même fond cyan vif<br>- Affichage basique : numéro, titre, description<br>- Lien "supprimer" pour chaque tâche<br>- Formulaire d'ajout de tâche en bas de page<br>- Case à cocher "task completed" dans le formulaire d'ajout de tache<br>- Bouton "Add Task!" non stylisé                                      | - Pas de confirmation avant suppression<br>- Pas de filtres ou de tri<br>- Pas de feedback lors de l'ajout/suppression<br>- Pas de validation des champs du formulaire<br />- Il est possible d'accéder à cette page pour n'importe quelle utilisateur via l'url et sans connexion | - Ajouter un système de filtres et de tri<br>- Ajouter une confirmation de suppression<br>- Permettre la modification des tâches<br>- Améliorer le design des cartes de tâches                                      |

### 1.2 - Tentative d'attaque de l'app individuel

| Type d'attaque testé | Emplacement | Brèche                                         | Piste d'amélioration                                                                                                   |
| -------------------- | ----------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Force Brut           | Login       | Il n'y a pas de limite au nombre de tentatives | - Ajouter des délais entre chaque tentative<br>- Ajouter des limites de connexion<br>- Ajouter des limites de requêtes |

### 1.3 - Etat de la codebase Individuel

| Fichier         | Points faibles                                                                                                                                                                                             | Pistes d'amélioration                                                                                                                                                            |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| models/user.js  | - Pas de gestion d'erreur dans authenticate<br>- Comparaison non sécurisée des mots de passe (==)<br>- Injection SQL possible dans findById<br>- Pas de hachage des mots de passe<br>- Callbacks imbriqués | - Utiliser bcrypt pour le hachage des mots de passe par exemple<br>- Ajouter une gestion d'erreur complète<br>- Utiliser des requêtes préparées<br>- Moderniser avec async/await |
| models/task.js  | - Injection SQL dans la méthode create<br>- Gestion d'erreur incomplète<br>- Pas de validation des entrées                                                                                                 | - Utiliser des requêtes préparées<br>- Ajouter une validation des données<br>- Compléter la gestion d'erreur                                                                     |
| routes/auth.js  | - Pas de validation des entrées<br>- Pas de gestion des erreurs<br>- GET utilisé pour l'inscription au lieu de POST                                                                                        | - Ajouter une validation avec express-validator<br>- Implémenter une gestion d'erreur robuste<br>- Utiliser POST pour l'inscription                                              |
| routes/tasks.js | - Pas de validation des entrées<br>- Injection possible via userId                                                                                                                                         | - Renforcer l'authentification<br>- Ajouter une validation des paramètres<br>- Sécuriser les requêtes avec des tokens                                                            |
| app.js          | - Secret de session en clair<br>- Pas de configuration de sécurité                                                                                                                                         | - Utiliser des variables d'environnement                                                                                                                                         |
