# Méthode universelle de dépannage

## Les six étapes

### 1. Identifier le problème

- Qui est touché : une personne, un service, un site ou toute l'entreprise?
- Depuis quand?
- Qu'est-ce qui a changé juste avant?
- Quel est le message exact?
- Le problème est-il reproductible?
- Quelle est la situation normale attendue?

### 2. Établir des hypothèses

Commence par les causes simples et probables. Sépare les catégories : physique, réseau, identité, permissions, système, application, service externe et sécurité.

### 3. Tester une hypothèse à la fois

Utilise un test qui confirme ou élimine clairement l'hypothèse. Note le résultat. Évite de modifier cinq paramètres en même temps.

### 4. Planifier et appliquer la correction

Évalue l'impact, demande l'autorisation nécessaire, sauvegarde la configuration et prépare un retour arrière. Applique le changement le moins risqué qui corrige la cause.

### 5. Vérifier complètement

- Le symptôme initial a-t-il disparu?
- L'utilisateur confirme-t-il que son flux de travail fonctionne?
- Les fonctions connexes fonctionnent-elles encore?
- Le problème risque-t-il de revenir?

### 6. Documenter

Inscris les symptômes, le contexte, les tests, la cause, la solution, la validation, les changements effectués et toute action de suivi.

## Technique d'isolation

Compare toujours :

- utilisateur touché vs autre utilisateur;
- poste touché vs autre poste;
- réseau filaire vs Wi-Fi;
- nom DNS vs adresse IP;
- application vs version web;
- profil utilisateur vs nouveau profil;
- problème local vs service externe.

## Règles professionnelles

- Ne suppose pas que l'utilisateur a tort; vérifie les faits.
- Ne demande jamais le mot de passe de l'utilisateur.
- Ne désactive pas une protection de sécurité sans autorisation et justification.
- N'efface pas les journaux après un incident.
- Évite les redémarrages aveugles avant d'avoir recueilli les informations utiles.
- Escalade rapidement quand l'impact, le risque ou les permissions dépassent ton rôle.
