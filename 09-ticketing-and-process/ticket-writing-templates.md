# Rédaction de tickets — modèles réutilisables

## Pourquoi un bon ticket compte

Un ticket doit permettre à une autre personne de comprendre le problème, reprendre le travail et prouver ce qui a été fait. « Réglé » ou « redémarré le PC » n'est pas une documentation suffisante.

## Structure minimale

### Titre

Utilise : **service ou appareil + symptôme + portée**.

Bon : `Outlook — demandes répétées de mot de passe pour une utilisatrice`  
Faible : `Problème Outlook`

### Description initiale

- utilisateur et emplacement;
- appareil/actif;
- service touché;
- comportement observé;
- comportement attendu;
- message exact;
- heure de début;
- fréquence;
- portée;
- changement récent;
- impact métier.

### Notes de travail

Écris chaque test avec son résultat :

```text
09:12 — Confirmé que Outlook sur le web fonctionne.
09:15 — Test-NetConnection outlook.office.com:443 réussi.
09:18 — Outlook démarre correctement en mode sans échec.
09:22 — Complément Contoso désactivé dans le profil test; Outlook normal.
```

### Résolution

- cause confirmée;
- changement appliqué;
- autorisation;
- validation technique;
- validation utilisateur;
- action préventive;
- suivi ou article de base de connaissances.

## Modèle — incident résolu

```text
Résumé :
[Utilisateur/service] ne pouvait pas [action] depuis [heure/date].

Impact :
[Une personne / équipe / site], [fonction métier touchée].

Environnement :
Appareil :
OS/version :
Réseau/emplacement :
Application/version :

Symptômes et message exact :

Tests effectués :
1. [Test] → [Résultat]
2. [Test] → [Résultat]
3. [Test] → [Résultat]

Cause :

Solution :

Validation :
[Tests finaux + confirmation utilisateur]

Suivi :
[Aucun / surveillance / problème connu / changement à planifier]
```

## Modèle — escalade

```text
Objet de l'escalade :

Impact et priorité :

Heure de début et chronologie :

Portée confirmée :

Données recueillies :
- erreurs/codes;
- captures/journaux;
- utilisateurs et appareils;
- tests réseau/application;
- changements récents.

Hypothèses éliminées :

Hypothèse actuelle :

Actions déjà tentées et résultats :

Ce qui est demandé à l'équipe suivante :

Contact utilisateur et disponibilité :
```

## Modèle — demande de service

```text
Demande :
Justification métier :
Utilisateur ou groupe :
Ressource :
Niveau d'accès :
Durée :
Approbateur :
Date nécessaire :
Vérification d'identité :
Action effectuée :
Validation :
Date de retrait prévue, si temporaire :
```

## Informations sensibles

Ne mets pas dans le ticket : mot de passe, code MFA, clé privée, jeton, numéro complet sensible ou fichier malveillant. Utilise les mécanismes sécurisés prévus.

## Fermeture

Avant de fermer :

- utilisateur informé;
- service réellement testé;
- cause et solution écrites;
- temps et priorité corrects;
- matériel/accès mis à jour;
- article lié ou créé;
- suivi planifié.

## Exercice

Transforme « imprimante réparée après redémarrage » en un ticket complet qui explique portée, tests, cause probable, changement et validation.
