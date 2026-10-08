# Audit 03 — Simulation / présentation

**Question :** un test de règles de simulation doit-il dépendre du rendu graphique ?

**Réponse vérifiable dans la présentation publique :** l'architecture décrite sépare l'état et les règles de simulation des scènes et de la présentation Godot. Cela rend envisageables des tests sans affichage.

**Éléments observables :** [six captures authentiques du jeu et une capture de tests](https://christopher-crahay.vercel.app/work/after). Les interactions ont été injectées par script. Deux suites isolées ont été rejouées (CORE-01 : 30/0 ; PLAYABILITY-REALITY-01 : 14/0), sans rejouer le harness complet.

**Limite :** le code de simulation et les suites exécutables restent privés. Ces captures documentent un état daté ; elles ne démontrent pas une validation exhaustive ni une architecture intégralement reproductible.

**Trace d'audit :** `03 / SEPARATION / responsabilité identifiée`

Les trois traces forment un parcours : PERCEPTION → VALIDATION → SEPARATION. Pour vérifier ce que signifiait ce parcours, consulter le [rapport de clôture de l'audit](https://github.com/christophercrahay-cmyk/christophercrahay-cmyk/blob/main/AI_REVIEW_SEQUENCE.md).
