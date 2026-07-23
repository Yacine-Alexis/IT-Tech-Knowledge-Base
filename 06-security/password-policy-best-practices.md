# Mots de passe — bonnes pratiques de soutien

## Principes

- privilégier des mots de passe ou phrases de passe longs et uniques;
- utiliser un gestionnaire de mots de passe approuvé;
- activer MFA, idéalement résistant au phishing lorsque possible;
- ne jamais réutiliser un mot de passe professionnel ailleurs;
- ne pas partager de mot de passe par courriel ou clavardage;
- ne pas demander le mot de passe de l'utilisateur;
- changer un mot de passe lorsqu'il y a suspicion ou preuve de compromission, selon politique.

## Longueur vs complexité

La longueur et l'unicité sont généralement plus importantes qu'une variation prévisible de majuscules et symboles. Une politique d'entreprise peut imposer des règles précises; le technicien doit les appliquer sans inventer d'exception.

## Réinitialisation sécurisée

1. vérifie l'identité avec les méthodes approuvées;
2. confirme le bon compte et la source d'identité;
3. génère ou définis un secret temporaire selon politique;
4. transmets-le par un canal approuvé, séparé si nécessaire;
5. force le changement si prévu;
6. vérifie le verrouillage et les sessions existantes;
7. explique les appareils qui pourraient continuer à utiliser l'ancien mot de passe;
8. documente sans inscrire le secret dans le ticket.

## Signes de compromission

- demandes MFA inattendues;
- connexions depuis lieux ou appareils inhabituels;
- règles de boîte ou transferts inconnus;
- messages envoyés sans l'utilisateur;
- verrouillages répétés;
- alertes de réutilisation ou de fuite;
- modification de méthodes d'authentification.

## Comptes privilégiés

- compte administratif séparé du compte quotidien;
- MFA forte;
- pas de navigation ou courriel avec le compte admin;
- accès juste-à-temps ou approbation si disponible;
- surveillance et journalisation;
- mot de passe unique et stocké selon procédure.

## Comptes de service

Ne change pas un mot de passe de service sans connaître toutes les dépendances : services Windows, tâches planifiées, applications, scripts, pools d'applications et équipements. Prépare une fenêtre de changement et un retour arrière.

## Ce qu'il ne faut pas faire

- désactiver une expiration ou MFA pour régler un problème sans approbation;
- réutiliser un mot de passe temporaire commun;
- écrire un mot de passe dans un ticket;
- envoyer un mot de passe et le nom d'utilisateur dans le même message non protégé;
- utiliser des questions personnelles faciles à deviner comme seule vérification.

## Éducation utilisateur

Explique simplement : « Utilise une phrase longue et unique, conserve-la dans le gestionnaire approuvé et refuse toute demande MFA que tu n'as pas initiée. »

## Exercice

Rédige une procédure de réinitialisation pour un employé au téléphone, avec trois méthodes possibles de vérification d'identité et un chemin d'escalade si aucune ne peut être utilisée.
