# Dépannage Wi-Fi comparé au réseau filaire

## Différence fondamentale

Un câble Ethernet fournit un média dédié entre l'appareil et le commutateur. Le Wi-Fi partage le spectre radio avec d'autres appareils et subit davantage l'environnement physique, les interférences, la distance, l'itinérance et l'authentification sans fil.

## Diagnostic filaire

Vérifie dans cet ordre :

1. câble bien connecté et non endommagé;
2. voyants du port et de la carte réseau;
3. port de commutateur activé et placé dans le bon VLAN;
4. adaptateur activé et pilote sain;
5. vitesse négociée attendue;
6. adresse DHCP correcte;
7. passerelle, DNS et accès aux services.

PowerShell :

```powershell
Get-NetAdapter
Get-NetAdapter | Format-Table Name, Status, LinkSpeed, MacAddress
Get-NetIPConfiguration
```

## Diagnostic Wi-Fi

Vérifie :

- mode avion et radio Wi-Fi;
- bon SSID, pas un réseau invité ressemblant;
- mot de passe ou certificat;
- signal et qualité;
- bande 2,4 GHz, 5 GHz ou 6 GHz selon l'appareil;
- portail captif;
- pilote et profil Wi-Fi;
- DHCP et VLAN associés au SSID;
- itinérance entre points d'accès.

Commandes Windows :

```powershell
netsh wlan show interfaces
netsh wlan show drivers
netsh wlan show profiles
netsh wlan show wlanreport
```

Le rapport WLAN est généré en HTML et aide à voir les déconnexions et erreurs récentes.

## Symptômes et causes probables

| Symptôme | Causes à tester |
|---|---|
| Connecté, pas d'Internet | DHCP, DNS, portail captif, VLAN, passerelle |
| Déconnexions fréquentes | signal faible, interférences, pilote, économie d'énergie, point d'accès |
| Lent uniquement à un endroit | couverture, obstacles, canal saturé |
| Un seul appareil touché | profil, pilote, matériel, configuration locale |
| Tous les appareils touchés | point d'accès, contrôleur, liaison montante, DHCP |
| Fonctionne sur invité mais pas entreprise | 802.1X, certificat, compte, stratégie |

## 2,4 GHz vs 5 GHz vs 6 GHz

- 2,4 GHz : meilleure portée, moins de canaux, plus d'interférences.
- 5 GHz : davantage de capacité, portée plus courte, généralement meilleur choix près du point d'accès.
- 6 GHz : spectre plus récent et propre, mais nécessite matériel compatible et portée plus limitée.

Ne force pas une bande sans comprendre la conception du réseau. Le choix est souvent géré automatiquement.

## Test comparatif utile

1. Place le même appareil au même endroit.
2. Teste d'abord le câble, puis le Wi-Fi.
3. Compare adresse IP, DNS, latence, pertes et accès aux mêmes ressources.
4. Teste un second appareil.
5. Si plusieurs appareils Wi-Fi échouent mais le câble fonctionne, concentre-toi sur le WLAN.

## Mesurer sans surinterpréter

Un test de vitesse Internet mesure plusieurs éléments à la fois. Pour isoler :

- `ping` de la passerelle pour la qualité locale;
- test vers une ressource interne pour le LAN;
- test Internet pour le chemin externe;
- répétition à différents moments pour la saturation.

## Actions prudentes

- oublier puis recréer un profil Wi-Fi peut aider, mais note le SSID et la méthode d'authentification;
- ne supprime pas un certificat d'entreprise sans procédure;
- ne réinitialise pas toute la pile réseau avant d'avoir recueilli la configuration;
- n'installe pas un pilote trouvé sur un site non officiel.

## Exercices

- Un portable se déconnecte chaque fois qu'il change de salle. Quelles données recueilles-tu?
- Le Wi-Fi invité fonctionne, mais le réseau d'entreprise demande sans cesse les identifiants. Quelles couches sont déjà validées?
- Le câble négocie à 100 Mb/s au lieu de 1 Gb/s. Quelles causes physiques testes-tu?
