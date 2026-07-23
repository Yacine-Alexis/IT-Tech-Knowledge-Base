# Microsoft Entra ID comparé à Active Directory local

## Résumé

Active Directory Domain Services est un annuaire de domaine traditionnel, conçu pour les réseaux Windows, Kerberos, LDAP, GPO et la jonction de postes au domaine. Microsoft Entra ID est un service d'identité cloud pour les applications SaaS, Microsoft 365, OAuth/OIDC/SAML, MFA et politiques d'accès.

Ce ne sont pas deux versions identiques du même produit.

## Comparaison

| Sujet | AD DS local | Microsoft Entra ID |
|---|---|---|
| Hébergement | Contrôleurs de domaine gérés par l'organisation | Service cloud Microsoft |
| Authentification typique | Kerberos, NTLM | OAuth 2.0, OpenID Connect, SAML |
| Annuaire | LDAP | API et services cloud |
| Gestion postes | Domain Join + GPO | Entra join/register + Intune/MDM |
| Ressources | Fichiers, imprimantes, applications locales | Microsoft 365 et applications cloud |
| Réseau | Dépend du DNS et de la connectivité aux DC | Dépend d'Internet et des services cloud |
| Politiques | GPO | Conditional Access, Intune, règles cloud |

## États d'un appareil

- **Entra registered** : souvent appareil personnel enregistré pour accéder à des ressources.
- **Entra joined** : appareil joint directement à l'identité cloud.
- **Hybrid Entra joined** : appareil joint à AD local et représenté dans Entra.

La terminologie exacte et les capacités dépendent de la configuration de l'organisation.

## Identité hybride

Un outil de synchronisation relie souvent AD DS et Entra ID. Il peut synchroniser utilisateurs, groupes et attributs, avec différentes méthodes d'authentification. La « source d'autorité » détermine où modifier un attribut.

Conséquences pour le soutien :

- un changement local prend du temps à apparaître dans le cloud;
- une erreur de synchronisation peut bloquer une création ou mise à jour;
- deux objets similaires peuvent créer un conflit;
- le mot de passe et le compte peuvent avoir des états différents selon la méthode;
- un technicien doit vérifier la source avant de modifier.

## Authentification vs autorisation

- authentification : prouver qui tu es;
- autorisation : déterminer ce que tu peux utiliser.

Une connexion réussie n'implique pas que la licence, le groupe, le rôle ou la permission est correct.

## Scénarios

### Accès au portail réussi, partage local échoue

L'identité cloud fonctionne peut-être, mais le poste n'accède pas au domaine, au DNS local, à Kerberos ou aux permissions SMB.

### Mot de passe changé dans le cloud mais pas sur le poste domaine

Dans un environnement synchronisé, le changement doit suivre le flux prévu. Vérifie la source d'autorité et la fonction de réécriture éventuelle au lieu de supposer une synchronisation bidirectionnelle.

### Nouvel utilisateur sans boîte

L'objet peut exister, mais la licence, le service Exchange, la synchronisation ou le provisionnement n'est pas terminé.

## Ce qu'il faut savoir expliquer en entrevue

« AD DS gère surtout l'identité et les ressources d'un domaine local avec Kerberos, LDAP et GPO. Entra ID gère l'identité cloud et l'accès aux applications modernes. Une entreprise hybride synchronise souvent les identités, donc je vérifie toujours quelle plateforme est la source avant de faire un changement. »

## Exercice

Dessine un schéma avec un poste domaine, un contrôleur de domaine, DNS, un outil de synchronisation, Entra ID, Microsoft 365 et une application SaaS. Trace le chemin de connexion pour chaque ressource.
