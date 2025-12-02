# Prototype Induction – Spécifications fonctionnelles (vue UI)

## 1. Vue générale
- Une seule page autonome (`induction.html`) regroupe le CSS, le HTML et le JavaScript de la maquette.
- Le parcours reste linéaire (5 étapes) avec un stepper, un bouton « Précédent / Étape suivante » et un indicateur textuel (`Étape n/5 – …`).
- Les cartes utilisent une grille responsive (2 colonnes > 860 px, 1 colonne en dessous) pour séparer les zones d’entrées et de retours métier.

## 2. Étapes et champs
- **Étape 1 – Plan long terme** : saisie ESN, type moteur, client, module ; probabilité et horizon sont regroupés dans une carte `Sorties` dédiée, et l’UI affiche une carte « Résultat (prévision créée) » + « Ajustements possibles » en colonne opposée.
- **Étape 2 à 5** : chaque étape présente ses propres champs (phase, probabilité, risk/confidence, workscope, slot, ajustement planner, confirmation finale) et renvoie un bloc de texte métier dans la colonne de droite pour expliciter le statut ou l’impact.
- Les curseurs et inputs déclenchent immédiatement les fonctions `updateStepX()` correspondantes, qui maintiennent l’objet `state` avec les valeurs numériques/texte actuelles et servent le contenu des blocs de sortie.
- La zone « Résultat » commune pour tous les blocs est stylée en jaune (`.result-block`) pour souligner visuellement les sorties, et les titres de section (`.card-section-title`) sont aussi encadrés d’un fond jaune clair pour renforcer la hiérarchie métier.

## 3. Règles métier visibles
- Tant que les champs obligatoires (ESN/type/client, date/shop confirmé, etc.) sont vides, le texte remonte une mention « En attente de données… » pour rappeler les prérequis.
- Les curseurs traduisent des labels métiers (`priorité basse/moyenne/élevée`, `flexibilité figée → très flexible`, `confiance prudente/forte`, etc.) dans les résumés textuels.
- Les ajustements planners (motif, décalage, priorité, commentaire) génèrent une phrase explicite pour documenter l’arbitrage et rester transparents pour les métiers.
- L’étape finale produit un jeu de « summary chips » et un JSON mock qui reprend l’ensemble des saisies (probabilités, horizon, slot, ajustements, confirmation) pour servir d’exemple d’export vers des API ou tickets.

## 4. Interface/UX
- Les cartes d’entrée/sortie fonctionnent comme des panneaux indépendants ; les sorties sont mises en évidence grâce aux backgrounds jaunes et aux bordures ponctuées.
- Les titres de sections utilisent un fond jaune (`#fef3c7`) et une teinte de texte chaude pour les rendre facilement repérables.
- Les badges, champs et chips utilisent des couleurs d’accent définies par des variables CSS (`--accent`, `--accent-ok`, etc.).
- Aucun appel réseau ou persistence backend n’est effectué : tout reste en mémoire (`state`) et est réévalué via le DOM (`textContent`, `innerHTML`, `.value`) dès que l’utilisateur modifie un champ.

## 5. Technos et maintenabilité
- Structure CSS/JS sans framework : un seul fichier HTML facilite l’embarquement dans une maquette rapide ou un prototype design.
- L’objet `state` centralise les données pour simplifier l’export JSON final, la mise à jour des blocs et le calcul de classes.
- Les helpers (`showStep`, `clamp`) gèrent la navigation et les limites des curseurs.
- L’approche responsive et les variables CSS permettent d’ajuster rapidement les couleurs/tokens sans toucher à la logique métier.
