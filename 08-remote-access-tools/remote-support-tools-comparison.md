# Outils de soutien à distance — comparaison

## Critères importants

- consentement utilisateur;
- accès assisté ou non assisté;
- chiffrement;
- MFA et rôles;
- journalisation et enregistrement;
- transfert de fichiers;
- élévation de privilèges;
- compatibilité OS;
- déploiement central;
- résidence des données;
- coût et licence;
- expérience sur réseau lent;
- capacité à bloquer le clavier ou l'écran;
- conformité de l'entreprise.

## Catégories

### Assistance rapide Windows

Simple pour aider un utilisateur Windows présent. Le code et le consentement réduisent l'accès permanent. Limites possibles selon compte, réseau, élévation et politique.

### TeamViewer / AnyDesk et similaires

Multi-plateforme et fonctionnalités riches. Ils doivent être approuvés et configurés centralement. Les versions grand public ou installations improvisées peuvent créer un risque d'accès persistant.

### Outils RMM

Gestion de parc, scripts, inventaire, alertes et accès non assisté. Très puissants : compromission d'un compte RMM peut affecter tout le parc. MFA, moindre privilège, approbation et audit sont essentiels.

### Intune / outils MDM

Pas toujours un outil de prise de contrôle direct. Ils gèrent configuration, applications, conformité et actions à distance.

### RDP/VNC

Accès technique direct, mais moins orienté vers le consentement et la communication avec l'utilisateur. Doivent être intégrés à une architecture sécurisée.

## Avant une session

1. vérifie le ticket et l'identité;
2. explique ce que tu vas faire;
3. demande le consentement;
4. demande à l'utilisateur de fermer les données sensibles;
5. utilise l'outil approuvé;
6. ne demande pas son mot de passe;
7. annonce toute élévation ou redémarrage;
8. termine la session et confirme la déconnexion.

## Pendant la session

- laisse l'utilisateur voir les actions;
- explique brièvement;
- ne parcoure pas des dossiers non nécessaires;
- ne copie pas de fichiers sans permission;
- masque les secrets;
- collecte seulement les informations utiles;
- évite de laisser un agent temporaire actif.

## Accès non assisté

Doit être : autorisé, inventorié, journalisé, limité, protégé par MFA et revu. Supprime l'accès quand il n'est plus nécessaire.

## Arnaques de faux support

Les attaquants demandent souvent d'installer un outil distant. Un technicien doit rappeler aux utilisateurs de vérifier l'identité du support via les canaux officiels et de ne jamais donner un code inattendu.

## Matrice de choix

| Besoin | Choix typique |
|---|---|
| Aider une personne présente | Outil assisté avec consentement |
| Administrer un serveur Linux | SSH via VPN/bastion |
| Gérer mille postes | RMM/MDM central approuvé |
| Accès à un poste Windows interne | RDP via architecture sécurisée |
| Formation visuelle multi-plateforme | Outil de partage d'écran approuvé |

## Exercice

Rédige un script de 30 secondes pour demander le consentement, expliquer la session et rappeler à l'utilisateur qu'il garde le contrôle.
