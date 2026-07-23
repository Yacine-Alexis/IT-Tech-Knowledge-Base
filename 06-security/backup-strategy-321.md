# Sauvegardes — stratégie 3-2-1 et restauration

## Règle 3-2-1

- au moins **3 copies** des données;
- sur **2 types de supports ou systèmes** différents;
- avec **1 copie hors site**.

Une version moderne ajoute souvent une copie hors ligne ou immuable et des vérifications régulières.

## Sauvegarde vs synchronisation

La synchronisation réplique souvent les suppressions et corruptions. OneDrive, RAID ou réplication ne sont pas automatiquement une sauvegarde complète. Une vraie sauvegarde offre rétention, versions, isolation et restauration testée.

## Objectifs

- **RPO** : quantité maximale de données qu'on accepte de perdre, exprimée en temps.
- **RTO** : délai maximal acceptable pour restaurer le service.

Exemple : RPO 4 h et RTO 8 h signifie que la sauvegarde doit limiter la perte à quatre heures et permettre un retour en service en huit heures.

## Ce qu'il faut sauvegarder

- données utilisateur et partages;
- bases de données avec méthode cohérente;
- configurations réseau et systèmes;
- secrets et clés selon une méthode sécurisée;
- états nécessaires à la reprise;
- documentation et procédures;
- SaaS selon les besoins et responsabilités.

## Vérifier une sauvegarde

Une tâche « Success » ne garantit pas une restauration utilisable. Vérifie :

- intégrité;
- rétention;
- chiffrement;
- accès aux clés;
- espace;
- alertes;
- restauration de fichier;
- restauration complète périodique;
- temps réel par rapport au RTO.

## Procédure de restauration

1. confirme le demandeur et la portée;
2. identifie le bon point de restauration;
3. évite d'écraser les données actuelles sans copie;
4. restaure dans un emplacement temporaire si possible;
5. valide avec le propriétaire;
6. analyse la cause de la perte;
7. documente temps, source, destination et résultat.

## Protection contre ransomware

- comptes de sauvegarde séparés;
- MFA et moindre privilège;
- copie immuable ou hors ligne;
- réseau segmenté;
- alertes sur suppressions et modifications;
- tests de récupération;
- sauvegardes non montées en permanence sur tous les postes.

## Erreurs fréquentes

- sauvegarder sur le même disque;
- ne jamais tester;
- oublier les appareils hors réseau;
- conserver trop peu de versions;
- ne pas protéger la console de sauvegarde;
- ignorer les bases de données et applications cohérentes;
- confondre snapshots et sauvegardes indépendantes.

## Exercice

Conçois une stratégie pour ton serveur Ollama/OpenWebUI : configuration Docker, volumes, modèles volumineux, données d'application et secrets. Définis ce qui doit être restauré rapidement et ce qui peut être retéléchargé.
