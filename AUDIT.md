# Audit 03 — Simulation / présentation

**Question :** un test de règles de simulation doit-il dépendre du rendu graphique ?

**Réponse vérifiable dans la présentation publique :** l'architecture décrite sépare l'état et les règles de simulation des scènes et de la présentation Godot. Cela rend envisageables des tests sans affichage.

**Limite :** le code de simulation et les résultats de tests ne sont pas publics. La séparation est décrite, non démontrée par une suite exécutable accessible.

**Trace d'audit :** `03 / SEPARATION / responsabilité identifiée`

Les trois traces forment un parcours : PERCEPTION → VALIDATION → SEPARATION. Pour vérifier ce que signifiait ce parcours, consulter le [rapport de clôture de l'audit](https://github.com/christophercrahay-cmyk/christophercrahay-cmyk/blob/main/AI_REVIEW_SEQUENCE.md).
