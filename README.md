# Prototype Induction – Spécifications fonctionnelles

## 1. Contexte
Cette page présente un parcours de planification d’induction en cinq étapes. On commence par poser la prévision long terme puis on affine l’horizon, on définit le workscope et la fenêtre atelier, on ajoute les ajustements du planner et on finit par confirmer la demande. C’est une maquette destinée à illustrer le flux sans faire de traitement réel.

## 2. Données
- L’utilisateur renseigne les éléments essentiels : le moteur (ESN), le type de moteur, le client, le module ou la visite, la probabilité, l’horizon (en mois), le shop préféré et la priorité.  
- Ensuite on complète les informations sur la phase en cours, les risques, la durée et la fenêtre du slot, et les ajustements à apporter (motif, décalage de date, commentaires).  
- À la fin, des éléments validés s’affichent : date et shop confirmés, niveau de confiance, liste de petites “puces” résumé et un bloc texte qui reprend toutes les données de façon structurée.

Les données restent uniquement dans la page : rien n’est enregistré sur un serveur.

## 3. Interface
- Une seule page, centrée sur un panneau blanc avec un bandeau en haut qui montre les cinq étapes numérotées.  
- Chaque étape contient deux colonnes de cartes : la colonne de gauche avec les champs à remplir et la colonne de droite avec les retours ou ajustements.  
- Les champs sont simples (listes déroulantes, curseurs, champs numériques ou texte) pour que tout le monde comprenne ce qu’il faut saisir.  
- Les zones de résultat décrivent ce que la saisie produit (“Proposition de slot pour …”, “Décision planner : …”).  
- En bas, des boutons “Précédent” / “Étape suivante” permettent d’avancer ou revenir, avec un texte qui rappelle l’endroit où l’on se trouve.  
- La dernière étape affiche aussi des pastilles synthétiques et un encadré texte prêt à être réutilisé dans un autre outil.

## 4. Règles
- Chaque étape s’affiche ou se cache : il n’y a pas de validation bloquante, c’est un déroulé guidé.  
- Dès qu’un champ est modifié, les textes de retour se mettent à jour pour expliquer ce que cela change.  
- Si une information manque, un message l’indique clairement (“En attente de données…”).  
- Les curseurs de priorité ou de flexibilité produisent aussi des phrases simples (ex. “slot décalé de +1 semaine”, “confiance forte”).  
- L’objet “payload” affiché à la fin est une suggestion : rien n’est envoyé automatiquement, c’est juste pour copier-coller.

## 5. Technique
- Le prototype tient en un seul fichier : du HTML pour la structure, un style intégré pour les couleurs, et un script pour mettre à jour les textes en direct.  
- Une petite “fiche” interne rassemble toutes les informations saisies : ça permet de réutiliser les mêmes données dans toutes les étapes sans complexité.  
- Les éléments visuels sont basés sur des composants standards (cartes, champs, boutons) et la mise en page s’adapte aux petits écrans en passant de deux colonnes à une seule.  
- La palette reste très claire pour que la lecture soit facile, avec des contours doux et quelques ombres pour détacher chaque bloc.
