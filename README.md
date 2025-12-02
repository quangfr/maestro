# Prototype Induction – Spécifications fonctionnelles métier
(Lien)[induction.html]

## 1. Contexte
Maquette expert de l’Induction Planning : on déroule les cinq phases métier qui vont de la prévision long terme à la demande confirmée. L’objectif est de faire visualiser chaque arbitrage sans intégration système, en accompagnant le pilote ou le planner au travers des décisions clés (probabilité, slot, ajustement). Le parcours reste purement démonstratif et pédagogique.

## 2. Données (champ par champ)
- **ESN moteur** (liste déroulante) : code moteur, ex. `ESN-728394 – LEAP-1A – Client A`.  
- **Type de moteur** (liste déroulante) : `LEAP-1A`, `LEAP-1B`, `CFM56-7B`.  
- **Client** (liste déroulante) : acteurs comme `Client A`, `Client B`, `Client C`.  
- **Module / visite** (liste déroulante) : `Full Engine`, `Module Fan`, `Module HPC`.  
- **Probabilité long terme** (curseur 10–90 %) : affichage immédiat en pourcentage.  
- **Horizon (mois)** (champ numérique) : intervalle 3–18 mois.  
- **Priorité client** (curseur 1–5) : interprété “basse / moyenne / élevée”.  
- **Shop préféré** (liste déroulante) : `Shop X (Europe)`, `Shop Y (Amériques)`, `Shop Z (Asie)`.  
- **Phase opérationnelle** (liste) : `Induction Plan`, `Initial Request`, `Final Request`.  
- **Mois restants** (nombre) : estimation de l’écart en mois.  
- **Probabilité phase** (curseur 50–100 %).  
- **Risque opérationnel** (curseur 1–5).  
- **Confiance planner** (curseur 1–5).  
- **Workscope** (champ texte libre) : description métier du scope.  
- **Shop window start / end** (mois) : début et fin de la fenêtre atelier ciblée.  
- **Durée (jours)** (nombre) : ex. 45 jours.  
- **Shop final** (liste) : confirmation du site atelier.  
- **Flexibilité slot** (curseur 1–5).  
- **Motif ajustement** (texte) : justification planner (urgences, contraintes).  
- **Décalage de date (semaines)** (nombre) : e.g. +2 semaines ou -1 semaine.  
- **Priorité ajustée** (curseur).  
- **Commentaire libre** (texte).  
- **Date confirmée** (mois) : induction month.  
- **Confiance finale** (curseur 50–100 %).

Toutes ces données sont maintenues dans une fiche interne (`state`) et restent en session navigateur : aucune persistance, aucun appel API.

## 3. Interface (entrées / sorties étape par étape)
- **Étape 1 – Plan long terme** : saisie ESN, type, client, module, probabilité/horizon ; la colonne de droite présente le texte métier “Création d’une entrée Induction Plan…” ainsi que les ajustements de priorité/shop.  
- **Étape 2 – Horizon & probabilités** : sélection de la phase, mois restants, curseurs risque/confiance ; sortie textuelle décrit la phase actuelle, le statu et la probabilité.  
- **Étape 3 – Workscope & window** : fields workscope, fenêtre (début/fin), durée, shop cible, flexibilité ; retour synthétise la proposition de slot et son impact capacitaire.  
- **Étape 4 – Ajustements planner** : motif, décalage, priorité, commentaire ; la colonne droite rend compte de la décision (“slot décalé de +1 semaine, priorité à 4”).  
- **Étape 5 – Confirmation** : date finale, shop validé, confiance ; la sortie affiche des chips métiers (ESN, magasin, induction, confiance) et un bloc JSON qui reprend toutes les informations pour alimenter les référentiels (simulé).  
- **Navigation** : stepper numéroté (5 pastilles), boutons « Précédent » / « Étape suivante » + hint textuel “Étape X/5 – …”.

## 4. Règles métiers
- Le parcours reste guidé : `showStep()` bascule l’affichage sans validation bloquante.  
- Chaque champ déclenche `updateStepX()` et met immédiatement à jour les textes métier, pour que l’utilisateur voie l’impact d’un ajustement en temps réel.  
- En l’absence d’un champ critique, un message indique “En attente de données…”.  
- Les curseurs traduisent des échelles métiers (“priorité élevée”, “flexibilité très forte”, “confiance prudente”).  
- Les ajustements planner (motif, décalage, priorité, commentaire) produisent un libellé clair reflétant la décision.  
- Le JSON final est un export visuel pour alimenter un ticket/manual entry : il n’est pas envoyé automatiquement.

## 5. Technique
- Prototype autonome : tout est contenu dans un seul fichier HTML avec CSS/JS inline, pas de framework.  
- Toutes les valeurs sont stockées dans un objet `state` global, partagé par les fonctions `updateStep1` à `updateStep5`.  
- L’interface utilise le DOM classique (select, input, buttons) et met à jour les contenus via `innerHTML`, `textContent` et `querySelector`.  
- La mise en page repose sur des cartes et une grille responsive qui passe de deux colonnes à une seule sous 860px.  
- Le design repose sur des variables CSS pour les couleurs, bordures, rayons et ombres, afin de garder un rendu léger et professionnel.
