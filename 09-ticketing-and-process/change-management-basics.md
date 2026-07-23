# Gestion des changements — bases

## Incident vs demande vs changement

- **incident** : interruption ou dégradation non planifiée;
- **demande de service** : besoin standard, par exemple logiciel ou accès;
- **changement** : ajout, modification ou retrait susceptible d'affecter un service.

Une correction urgente peut tout de même être un changement et nécessiter une procédure d'urgence.

## Types courants

- **standard** : faible risque, répétable, préautorisé avec procédure;
- **normal** : évalué et approuvé avant exécution;
- **urgent** : nécessaire rapidement pour réduire un impact majeur, avec approbation adaptée et revue après coup.

## Contenu d'un changement

- objectif et justification;
- systèmes et utilisateurs touchés;
- propriétaire;
- date, durée et fenêtre;
- prérequis;
- étapes détaillées;
- tests avant/après;
- risques;
- dépendances;
- communication;
- plan de retour arrière;
- approbations;
- preuve de succès.

## Plan de retour arrière

Il doit préciser :

- condition qui déclenche le retour;
- étapes exactes;
- sauvegarde ou configuration précédente;
- temps requis;
- personne autorisée;
- test après retour.

« Remettre comme avant » n'est pas un plan.

## Exemple — mise à jour d'un service

1. confirmer sauvegarde;
2. vérifier espace et version actuelle;
3. informer utilisateurs;
4. arrêter proprement;
5. appliquer la mise à jour;
6. vérifier configuration et démarrage;
7. tester santé, port et fonction métier;
8. surveiller journaux;
9. si échec, restaurer version/configuration;
10. communiquer et fermer.

## Séparation des tâches

Dans un environnement mature, la personne qui demande, approuve et exécute peut ne pas être la même. Cela réduit erreurs et abus.

## Changements simples de soutien

Même une modification locale peut mériter une trace : registre, pilote, permission, logiciel, firewall ou configuration VPN. Documente l'ancien et le nouvel état.

## Après changement

- compare aux critères de succès;
- surveille une période adaptée;
- confirme avec les utilisateurs;
- vérifie effets secondaires;
- mets à jour documentation et inventaire;
- fais une revue si problème.

## Erreurs fréquentes

- fenêtre trop courte;
- dépendance oubliée;
- sauvegarde non testée;
- pas de communication;
- changement de plusieurs variables;
- retour arrière impossible;
- réussite technique mais flux métier non testé.

## Exercice

Rédige un changement pour mettre à jour Docker Compose sur ton serveur personnel, incluant sauvegarde des volumes, interruption, tests et rollback.
