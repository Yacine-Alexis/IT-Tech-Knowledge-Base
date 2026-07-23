# MFA et Conditional Access — bases de soutien

## MFA

L'authentification multifacteur combine au moins deux catégories :

- quelque chose que l'utilisateur connaît;
- quelque chose qu'il possède;
- quelque chose qu'il est.

Un mot de passe plus un autre mot de passe n'est pas réellement deux facteurs.

## Méthodes courantes

- application d'authentification avec notification ou code;
- clé de sécurité FIDO2/passkey;
- méthode sans mot de passe;
- jeton matériel;
- SMS ou appel, selon politique et niveau de risque.

Toutes les méthodes ne présentent pas la même résistance au phishing.

## Conditional Access

Une politique évalue des signaux comme :

- utilisateur ou groupe;
- application ciblée;
- emplacement et adresse IP;
- état de l'appareil;
- risque de connexion;
- plateforme;
- type de client;
- fréquence de session.

Elle peut autoriser, bloquer ou exiger des contrôles comme MFA ou appareil conforme.

## Aider un utilisateur qui change de téléphone

1. vérifie son identité avec la procédure officielle;
2. confirme les méthodes encore disponibles;
3. ne contourne pas MFA en partageant un code;
4. réinitialise ou exige la réinscription selon ton rôle;
5. utilise un Temporary Access Pass uniquement si l'organisation l'autorise;
6. vérifie l'enregistrement du nouvel appareil;
7. retire l'ancienne méthode si approprié;
8. teste une nouvelle connexion;
9. documente.

## Boucle de notifications MFA

Si l'utilisateur reçoit des demandes qu'il n'a pas initiées :

- lui dire de refuser, ne pas approuver « pour faire arrêter »;
- traiter cela comme un signal potentiel de mot de passe compromis;
- réinitialiser le mot de passe selon procédure;
- révoquer les sessions si autorisé;
- examiner les journaux de connexion;
- escalader à la sécurité.

## Diagnostiquer un blocage

Recueille :

- heure exacte et fuseau;
- utilisateur et application;
- message et code d'erreur;
- identifiant de corrélation;
- appareil, navigateur et réseau;
- résultat depuis un autre contexte approuvé;
- journaux de connexion et onglet Conditional Access, si ton rôle le permet.

Ne désactive pas une politique globale pour résoudre le cas d'une personne.

## Causes courantes

- appareil non conforme;
- méthode MFA absente ou non permise;
- emplacement bloqué;
- client ancien utilisant un protocole non autorisé;
- utilisateur hors du groupe prévu;
- politique multiple avec exigences combinées;
- heure incorrecte pour les codes;
- enregistrement de méthode incomplet.

## Principes de sécurité

- moindre privilège administratif;
- comptes d'urgence fortement protégés et surveillés;
- déploiement pilote et mode rapport avant activation large;
- exclusion minimale et justifiée;
- protection contre la fatigue MFA;
- ne jamais demander à l'utilisateur son code à usage unique.

## Exercice

Écris une procédure de cinq minutes pour un utilisateur qui a perdu son téléphone, puis une procédure différente pour un utilisateur qui reçoit des demandes MFA non sollicitées. Explique pourquoi le second cas est un incident potentiel.
