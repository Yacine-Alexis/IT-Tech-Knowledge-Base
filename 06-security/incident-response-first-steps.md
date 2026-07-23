# Premières étapes lors d'un incident de sécurité

## Priorité

Protéger les personnes, limiter l'impact, préserver les preuves et contacter rapidement l'équipe responsable. Un technicien de soutien ne doit pas improviser une enquête complète hors de son rôle.

## Actions générales

1. reste calme et note l'heure;
2. écoute le récit sans blâmer;
3. détermine si le danger est actif;
4. applique le playbook de l'organisation;
5. isole l'appareil ou le compte seulement avec la méthode approuvée;
6. préserve courriels, journaux, captures et identifiants;
7. contacte sécurité, gestionnaire ou astreinte;
8. évite toute communication externe non autorisée;
9. documente chaque action et personne contactée.

## Ce qu'il ne faut pas faire

- éteindre ou redémarrer automatiquement un appareil compromis;
- supprimer des fichiers ou vider les journaux;
- exécuter soi-même un fichier suspect;
- lancer un « nettoyage » avant collecte;
- communiquer des détails sensibles dans un canal public;
- promettre qu'aucune donnée n'a été touchée;
- contacter l'attaquant;
- mener une analyse médico-légale sans mandat ni outils appropriés.

## Scénarios

### Courriel de phishing

Préserve le message original et les en-têtes, recueille les actions de l'utilisateur, sécurise le compte si nécessaire et escalade.

### Malware ou comportement étrange

Note alertes, processus visibles, heure, utilisateur, réseau et périphériques. Isole via EDR ou réseau selon procédure. Ne continue pas à utiliser le poste.

### Perte ou vol d'appareil

Confirme l'identité de l'appareil, dernière localisation connue, chiffrement, compte et données. Lance le processus de verrouillage/effacement seulement si autorisé. Informe sécurité et gestion.

### Compte compromis

Bloque ou sécurise le compte, réinitialise le secret, révoque sessions, vérifie MFA et accès, puis fais examiner les actions effectuées.

### Données envoyées au mauvais destinataire

Ne demande pas simplement au destinataire de supprimer. Escalade selon politique de confidentialité; note données, destinataire, heure et possibilité de rappel ou révocation.

## Préservation minimale

- captures avec date/heure;
- message original;
- nom d'hôte et utilisateur;
- adresse IP si pertinente;
- identifiant d'alerte;
- chronologie;
- actions déjà effectuées;
- personnes informées.

## Chaîne de possession

Pour un appareil ou support potentiellement utilisé comme preuve, documente qui l'a manipulé, quand, où il a été stocké et quelles actions ont été prises.

## Critères d'urgence

Escalade immédiatement pour ransomware, exfiltration possible, compte privilégié compromis, plusieurs appareils, perte de données sensibles, interruption majeure ou menace physique.

## Exercice

Simule un appel : « J'ai approuvé une notification MFA que je n'avais pas demandée. » Écris les cinq premières actions, les données à préserver et la phrase utilisée pour rassurer l'utilisateur.
