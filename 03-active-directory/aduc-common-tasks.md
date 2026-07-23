# Active Directory Users and Computers — tâches courantes

## Concepts essentiels

- **Domaine** : frontière d'administration et d'identité AD DS.
- **Contrôleur de domaine** : serveur qui héberge l'annuaire, authentifie et réplique.
- **OU** : conteneur administratif utilisé pour délégation et application de GPO.
- **Utilisateur, ordinateur, groupe** : objets principaux.
- **Groupe de sécurité** : donne accès à une ressource; évite d'attribuer des droits directement à chaque personne.

## Avant toute tâche

- valide l'identité du demandeur;
- confirme l'autorisation et le ticket;
- respecte la convention de nommage;
- applique le moindre privilège;
- note les groupes et paramètres avant modification;
- ne demande jamais le mot de passe existant.

## Créer un utilisateur

Dans ADUC :

1. sélectionne la bonne OU;
2. crée l'utilisateur avec le nom de connexion conforme;
3. définis un mot de passe temporaire transmis de façon approuvée;
4. oblige le changement à la première connexion si la procédure l'exige;
5. ajoute uniquement les groupes nécessaires;
6. complète les attributs utiles;
7. vérifie la synchronisation si l'identité est hybride;
8. documente.

PowerShell, en laboratoire ou selon procédure :

```powershell
$params = @{
    Name                  = 'Julie Dupont'
    GivenName             = 'Julie'
    Surname               = 'Dupont'
    SamAccountName        = 'jdupont'
    UserPrincipalName     = 'jdupont@contoso.local'
    Path                  = 'OU=Users,OU=Montreal,DC=contoso,DC=local'
    Enabled               = $true
    ChangePasswordAtLogon = $true
    AccountPassword       = Read-Host -AsSecureString 'Temporary password'
}
New-ADUser @params
```

## Réinitialiser un mot de passe

1. vérifie l'identité selon la politique;
2. distingue mot de passe oublié, compte verrouillé et problème MFA;
3. réinitialise le mot de passe;
4. déverrouille si nécessaire;
5. explique la prochaine connexion et les appareils qui pourraient conserver l'ancien mot de passe;
6. surveille un nouveau verrouillage.

```powershell
Set-ADAccountPassword -Identity jdupont -Reset -NewPassword (Read-Host -AsSecureString)
Unlock-ADAccount -Identity jdupont
```

## Ajouter à un groupe

Confirme le propriétaire du groupe, la justification et la durée si l'accès est temporaire.

```powershell
Add-ADGroupMember -Identity 'GG-Finance-Read' -Members jdupont
Get-ADPrincipalGroupMembership jdupont | Sort-Object Name
```

N'utilise pas Domain Admins ou un groupe privilégié pour résoudre un accès ordinaire.

## Désactiver un départ

Selon le processus d'offboarding :

- désactive le compte rapidement à l'heure prévue;
- révoque les sessions cloud via l'équipe ou l'outil approprié;
- retire les accès ou déplace le compte dans l'OU de départ;
- conserve ou transfère les données selon politique;
- ne supprime pas immédiatement l'objet sans politique de rétention;
- traite aussi les comptes secondaires, VPN, applications et appareils.

## Ordinateur et domaine

Tâches courantes : joindre un poste au domaine, déplacer l'objet dans la bonne OU, réinitialiser un compte ordinateur si la relation d'approbation est brisée, puis confirmer DNS et heure.

## Recherche utile

```powershell
Get-ADUser -Filter "Surname -like 'Dup*'" -Properties Department,Enabled
Search-ADAccount -LockedOut
Search-ADAccount -AccountDisabled -UsersOnly
Get-ADComputer -Filter * -SearchBase 'OU=Workstations,DC=contoso,DC=local'
```

## Erreurs courantes

- créer l'utilisateur dans le conteneur par défaut au lieu de la bonne OU;
- copier un ancien compte sans vérifier tous les groupes;
- donner trop de droits pour accélérer;
- supprimer un compte au lieu de le désactiver;
- oublier les effets de la synchronisation cloud;
- annoncer une réussite sans tester la connexion ou l'accès.

## Exercices de laboratoire

Crée deux OU, trois groupes basés sur des rôles, quatre utilisateurs et un partage. Utilise un modèle AGDLP : Accounts → Global groups → Domain Local groups → Permissions.
