# Subnetting — aide-mémoire pratique

## Objectif

Comprendre si deux appareils sont dans le même réseau, calculer une plage d'adresses et reconnaître les masques les plus courants. Un technicien de soutien n'a pas besoin de faire du sous-réseautage avancé mentalement, mais doit savoir lire une configuration et repérer une incohérence.

## Les quatre valeurs à repérer

Pour une interface réseau, note toujours :

- l'adresse IP;
- le préfixe ou masque;
- la passerelle par défaut;
- le ou les serveurs DNS.

Exemple : `192.168.10.34/24`, passerelle `192.168.10.1`, DNS `192.168.10.10`.

## Notation CIDR courante

| CIDR | Masque | Adresses totales | Hôtes IPv4 utilisables* |
|---:|---|---:|---:|
| /8 | 255.0.0.0 | 16 777 216 | 16 777 214 |
| /16 | 255.255.0.0 | 65 536 | 65 534 |
| /20 | 255.255.240.0 | 4 096 | 4 094 |
| /21 | 255.255.248.0 | 2 048 | 2 046 |
| /22 | 255.255.252.0 | 1 024 | 1 022 |
| /23 | 255.255.254.0 | 512 | 510 |
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |

\*Dans un sous-réseau IPv4 classique, l'adresse réseau et l'adresse de diffusion ne sont pas attribuées aux hôtes.

## Méthode rapide

1. Trouve l'octet intéressant, c'est-à-dire celui du masque qui n'est ni 255 ni 0.
2. Calcule la taille de bloc : `256 - valeur du masque`.
3. Repère le multiple de cette taille immédiatement inférieur ou égal à l'octet de l'IP.
4. Ce multiple est le début du sous-réseau.
5. Le bloc suivant moins 1 est l'adresse de diffusion.
6. Les adresses entre les deux sont utilisables.

### Exemple 1 — /26

IP : `192.168.1.70`  
Masque : `255.255.255.192`

- taille de bloc : `256 - 192 = 64`;
- blocs : 0, 64, 128, 192;
- 70 appartient au bloc 64–127;
- réseau : `192.168.1.64`;
- diffusion : `192.168.1.127`;
- hôtes : `192.168.1.65` à `192.168.1.126`.

### Exemple 2 — /23

IP : `10.20.5.40`  
Masque : `255.255.254.0`

- octet intéressant : troisième;
- taille de bloc : `256 - 254 = 2`;
- 5 appartient au bloc 4–5;
- réseau : `10.20.4.0`;
- diffusion : `10.20.5.255`;
- hôtes : `10.20.4.1` à `10.20.5.254`.

## Même réseau ou non?

Deux appareils peuvent communiquer directement si leurs adresses, une fois comparées avec le même masque, donnent la même adresse réseau.

- `192.168.10.25/24` et `192.168.10.200/24` : même réseau.
- `192.168.10.25/24` et `192.168.11.20/24` : réseaux différents; un routeur est requis.
- `192.168.10.25/23` et `192.168.11.20/23` : ils peuvent être dans le même réseau, selon la limite du bloc /23.

## Plages privées IPv4

- `10.0.0.0/8`
- `172.16.0.0/12` à `172.31.255.255`
- `192.168.0.0/16`

Autres adresses utiles :

- `127.0.0.1` : boucle locale;
- `169.254.0.0/16` : APIPA, souvent signe d'échec DHCP;
- `0.0.0.0` : adresse non spécifiée ou route par défaut selon le contexte;
- `255.255.255.255` : diffusion limitée.

## Commandes de vérification

```powershell
ipconfig /all
Get-NetIPConfiguration
Get-NetIPAddress -AddressFamily IPv4
Get-NetRoute -DestinationPrefix "0.0.0.0/0"
```

Linux :

```bash
ip address
ip route
ip neigh
```

## Erreurs typiques

- passerelle hors du sous-réseau local;
- masque trop large ou trop étroit;
- adresse statique déjà utilisée;
- serveur configuré en DHCP alors qu'il devrait avoir une réservation ou une IP gérée;
- appareil en `169.254.x.x` à cause d'un DHCP inaccessible.

## Exercices

1. Donne le réseau, la diffusion et la plage d'hôtes de `192.168.50.142/27`.
2. Est-ce que `10.1.8.12/21` et `10.1.15.200/21` sont dans le même réseau?
3. Un poste a `192.168.20.40/24` et une passerelle `192.168.21.1`. Quel problème vois-tu?

## Validation

Tu maîtrises ce fichier si tu peux expliquer à voix haute pourquoi un masque détermine la portée locale et calculer un /24, /25, /26 et /27 sans outil.
