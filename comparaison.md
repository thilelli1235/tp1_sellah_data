# Comparaison MVC / MVP / MVVM

| Critère | MVC | MVP | MVVM |
|---|---|---|---|
| Couplage entre la vue et la logique | Moyen : la View est reliée au Controller, qui pilote le Model | Faible : la View est passive, toute la logique est dans le Presenter | Très faible : la vue ne fait que des liaisons avec le ViewModel |
| Ce qu'on peut tester sans navigateur | Le Model (règles et données) | Le Presenter, avec une fausse vue | Le ViewModel (état et commandes) |
| Où valider une saisie | Dans le Model | Dans le Presenter | Dans le ViewModel ou le Model |
| Cas d'usage typique | Petite application web simple, comme une todo-list | Formulaires et écrans avec beaucoup de logique de contrôle, comme une connexion | Interfaces réactives où l'affichage suit l'état, comme un panier (Angular, Vue) |

## Question Data

Les données de la Todo-list vivent dans le Model (TodoModel.js), dans le champ privé #todos. Seul le Model peut les modifier, grâce au # qui empêche tout accès depuis l'extérieur. La méthode all() renvoie une copie de la liste, donc la View et le Controller ne peuvent pas la modifier directement : ils doivent passer par les méthodes du Model (add, toggle...), qui appliquent les règles.

Quand on recharge la page, les tâches disparaissent, car elles ne sont stockées qu'en mémoire.

Pour les conserver, il faut ajouter de la persistance dans le Model : par exemple enregistrer la liste dans le localStorage du navigateur à chaque changement, et la recharger au démarrage. On peut aussi passer par une API et une base de données. Dans les deux cas, on ne change ni la View ni le Controller.