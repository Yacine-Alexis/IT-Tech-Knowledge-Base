# Centre d'administration Microsoft 365 — tâches de soutien

## Portée

Les interfaces et noms de menus peuvent évoluer. Apprends surtout le raisonnement : identité, licence, service, rôle administratif, données, sécurité et audit.

## Tâches courantes

### Créer ou gérer un utilisateur

- vérifier l'autorisation et la convention de nom;
- créer l'identité dans la source appropriée : cloud ou AD local synchronisé;
- attribuer les licences par le mécanisme prévu;
- ajouter les groupes nécessaires;
- configurer l'usage location si requis;
- transmettre l'accès temporaire par canal approuvé;
- vérifier MFA et méthodes d'authentification;
- documenter l'heure et les changements.

Dans un environnement hybride, ne modifie pas un attribut cloud qui est maîtrisé par l'AD local; le changement peut être écrasé.

### Réinitialiser un mot de passe

1. vérifie l'identité;
2. confirme si le compte est cloud-only ou synchronisé;
3. utilise le portail ou le système source approprié;
4. révoque les sessions seulement si le risque ou la procédure le demande;
5. explique la propagation aux applications;
6. surveille les échecs de connexion.

### Attribuer une licence

- confirme le produit réellement nécessaire;
- vérifie disponibilité et usage location;
- préfère l'attribution par groupe si l'organisation l'utilise;
- comprends que la licence active plusieurs service plans;
- attends la propagation et vérifie le service;
- retire les licences selon le processus de départ et de rétention.

### Gérer une boîte aux lettres

Selon les rôles et procédures :

- boîte utilisateur vs boîte partagée;
- alias et adresse principale;
- permissions Full Access, Send As et Send on Behalf;
- transfert et règles;
- restauration d'éléments;
- conservation, litige ou eDiscovery réservés aux rôles autorisés.

### Groupes

Distingue :

- groupe Microsoft 365;
- liste de distribution;
- groupe de sécurité;
- groupe de sécurité avec messagerie;
- équipe Teams liée à un groupe.

Choisis selon collaboration, courriel et contrôle d'accès.

## Diagnostic d'un service

1. vérifie l'étendue : utilisateur, groupe, organisation;
2. consulte l'état du service et les messages administratifs;
3. vérifie identité, licence et méthodes d'accès;
4. vérifie les journaux de connexion si autorisé;
5. compare web et application de bureau;
6. vérifie les politiques d'accès et de sécurité;
7. collecte identifiants de corrélation et heure UTC si l'application les fournit.

## Moindre privilège

Les rôles administratifs doivent être spécifiques. Un technicien ne devrait pas recevoir un rôle global uniquement pour réinitialiser des mots de passe ou gérer des licences.

## Offboarding

Le départ peut inclure : blocage de connexion, réinitialisation, révocation de sessions, récupération de données, conversion de boîte, transfert OneDrive, retrait de groupes, appareils et licences, selon les obligations de l'entreprise.

## Documentation

Pour chaque action : demandeur, approbateur, identité cible, ancien état, nouvel état, heure, rôle utilisé, validation et suivi.

## Exercices

- Explique pourquoi un compte synchronisé doit souvent être modifié dans AD local.
- Compare une boîte partagée et un compte utilisateur licencié.
- Écris une checklist d'arrivée et une checklist de départ.
