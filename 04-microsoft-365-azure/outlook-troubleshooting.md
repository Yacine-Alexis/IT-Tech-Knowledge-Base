# Dépannage Outlook

## Déterminer la portée

- Outlook de bureau seulement?
- Outlook sur le web fonctionne-t-il?
- Un seul dossier, une boîte partagée ou toute la boîte?
- Un utilisateur ou plusieurs?
- Envoi, réception, recherche, calendrier, authentification ou performance?

Cette comparaison sépare souvent client local, profil, réseau, service et boîte aux lettres.

## Collecte

- message exact et heure;
- version Outlook et canal de mise à jour;
- mode classique ou nouveau client selon l'environnement;
- taille et espace libre;
- type de compte;
- compléments installés;
- changement récent;
- état du service Microsoft 365;
- fonctionnement sur le web.

## Ordre de dépannage

1. teste Outlook sur le web;
2. vérifie l'état du service;
3. confirme connectivité, heure et authentification;
4. lance Outlook en mode sans échec si pertinent;
5. désactive un complément suspect de façon contrôlée;
6. vérifie le profil, le mode cache et le fichier de données;
7. utilise les outils de réparation approuvés;
8. crée un nouveau profil plutôt que de supprimer l'ancien immédiatement;
9. réinstalle seulement après avoir éliminé les causes plus probables.

## Commandes et outils

```cmd
outlook.exe /safe
outlook.exe /profiles
control mlcfg32.cpl
```

Le nom de l'applet peut varier selon installation. Utilise le Panneau de configuration et Mail pour gérer les profils.

## Symptômes

### Demande répétée de mot de passe

- compte verrouillé ou mot de passe changé;
- jeton d'authentification ou cache d'identifiants;
- MFA/Conditional Access;
- ancien client ou protocole;
- heure incorrecte;
- problème de découverte automatique;
- profil corrompu.

### Outlook lent

- gros fichier OST ou nombreux dossiers;
- compléments;
- antivirus/EDR;
- recherche/indexation;
- synchronisation de boîtes partagées;
- stockage lent ou presque plein;
- réseau/VPN.

### Recherche incomplète

Compare recherche web et locale. Vérifie état d'indexation, portée, mode cache et santé du profil. Ne reconstruis pas l'index global sans mesurer l'impact.

### Boîte partagée absente

- permission non propagée;
- automapping;
- mauvais compte ou profil;
- licence ou configuration particulière;
- ajout manuel nécessaire selon conception.

### Courriel bloqué dans Outbox

- pièce jointe trop grande;
- mode hors connexion;
- connexion;
- complément;
- message endommagé;
- limite ou politique de transport.

## Fichiers de données

- OST : copie mise en cache d'une boîte serveur; peut souvent être recréée, mais confirme la nature du compte.
- PST : peut contenir des données locales uniques; sauvegarde avant toute manipulation.

Ne supprime jamais un PST ou OST sans comprendre où résident les données.

## Escalade

- incident touchant plusieurs utilisateurs;
- suspicion de compromission ou règle de transfert malveillante;
- données manquantes ou rétention;
- erreurs de transport nécessitant traces administratives;
- politiques d'accès ou conformité.

## Exercice

Crée une matrice « Outlook web fonctionne / ne fonctionne pas » et « autre appareil fonctionne / ne fonctionne pas », puis indique la couche la plus probable dans chaque case.
