# Critères d'escalade

## Escalader n'est pas échouer

Une bonne escalade protège l'entreprise et réduit le temps de résolution. Le technicien doit résoudre ce qui relève de son rôle, mais éviter de deviner lorsque le risque, l'impact, les permissions ou le temps dépassent ses limites.

## Escalade immédiate

- incident de sécurité actif;
- données sensibles exposées ou perdues;
- ransomware ou plusieurs postes compromis;
- panne majeure ou plusieurs équipes touchées;
- risque physique ou électrique;
- compte privilégié compromis;
- système critique ou production;
- action nécessitant un rôle non autorisé;
- obligation légale, confidentialité ou conformité;
- changement sans retour arrière fiable.

## Escalade après diagnostic de niveau 1

- problème reproductible mais cause hors de ton périmètre;
- réseau, serveur ou application centrale en cause;
- bug ou limitation produit;
- besoin de modification GPO, pare-feu, Conditional Access ou architecture;
- matériel sous garantie;
- analyse de dump ou forensique;
- dépassement du temps raisonnable ou du SLA;
- problème récurrent nécessitant une correction permanente.

## Avant d'escalader

Sauf urgence, recueille :

- impact, portée et priorité;
- heure de début;
- message exact;
- utilisateur, appareil, service et emplacement;
- changement récent;
- tests et résultats;
- journaux/captures pertinents;
- hypothèses éliminées;
- action précise demandée à l'équipe suivante.

## Ne pas retarder une urgence

Pour un incident majeur ou sécurité, escalade d'abord selon le canal d'urgence, puis complète les données. N'attends pas d'avoir un ticket parfait pendant que l'impact augmente.

## Escalade fonctionnelle vs hiérarchique

- **fonctionnelle** : vers l'équipe possédant la technologie;
- **hiérarchique** : vers gestionnaire ou incident manager lorsque priorité, conflit, délai ou communication l'exige.

## Exemple de bonne escalade

```text
P2 — 14 utilisateurs du service Finance ne peuvent plus accéder à \\FS01\Finance depuis 08:42.
DNS et ping vers FS01 réussissent. Le port 445 expire depuis VLAN 20, mais fonctionne depuis VLAN 10.
Aucun changement local sur les postes. Incident réseau/ACL probable.
Demande : vérifier le flux VLAN20 → FS01 TCP 445 et les changements de pare-feu depuis 08:30.
```

## Mauvaise escalade

```text
Ça ne marche pas, probablement le serveur. Pouvez-vous regarder?
```

## Rester propriétaire du ticket

Même après escalade :

- informe l'utilisateur;
- ajoute les nouvelles informations;
- coordonne les tests;
- évite les doubles changements;
- confirme la résolution;
- ferme avec documentation complète.

## Exercice

Classe cinq cas : imprimante individuelle, cinq sites sans réseau, batterie gonflée, erreur Outlook web pour une personne, demande de Domain Admin. Indique « résoudre », « escalader après collecte » ou « escalader immédiatement ».
