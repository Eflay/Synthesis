## 1) *Les différents types de scans*

Il y a 3 types de bases dans les scans Nmap :

- TCP Connect Scans
- SYN "Half-open" Scans
- UDP Scans

Ensuite il y en a des moins populaire :

- TCP Null Scans
- TCP Fin Scans
- TCP Xmas Scans

La plupart à l'exception de "UDP Scans" ont des objectifs similaires. Toutefois, leurs résultats de scans diffèrent selon le type utilisé. On va aussi parler du **ICMP Scanning**.

## 2) *TCP Connect Scans*

Pour comprendre ce scan, il vous faut une bonne connaissance avec la communication TCP.

Pour les connection TCP, il y a 3 étapes distinctes :

1. SYN

2. SYN/ACK

3. ACK

On va tout d'abord envoyer une requête SYN au serveur, qui va ensuite nous répondre avec un flag SYN/ACK et finalement, on renverra un paquet ACK.

![TCP CS](https://muirlandoracle.co.uk/wp-content/uploads/2020/03/image-2.png)

Le but avec nmap étant de faire ce principe pour **chaque port de la machine ciblée.** Nmap saura si un port est ouvert/fermé en fonction de la réponse du serveur. Grâce à l'RFC 793 qui spécifie que :

> Si une connection n'existe pas (port fermé) alors un paquet reset (RST) est envoyé en réponse à tout paquet entrant sauf le paquet (RST).

Grâce à ceci, nmap peut déterminer si un port est ouvert ou non avec ce type de scan.

![rst](https://i.imgur.com/vUQL9SK.png)

Si au contraire, nmap rençoit une réponse SYN/ACK, alors le port est ouvert.

Cependant il y a une 3e possiblité, si le port se trouve derrière un firewall. En effet, beaucoup de pare-feu ne répondent tout simplement pas aux paquets entrants. Nmap ne reçoit donc rien de la part du serveur et le port sera marqué comme étant filtré (filtered).

## 3) *SYN Scans*

**L'objectif de ce scan est de le rendre moins visible** que le TCP Connect Scan. La différence est qu'au lieu de renvoyer un paquet ACK, après avoir reçu le SYN/ACK de la part du serveur, **il renvoie un paquet RST.**

![syn](https://i.imgur.com/cPzF0kU.png)

Il y a plusieurs avantages :

- Possiblité de contourner les **anciens** Intrusion Detection System (IDS)
- Les SYN Scans ne sont pas journalisés car la connexion n'est pas établie grâce au RST
- Plus rapide qu'un TCP Connect Scan

Il y a aussi quelques inconvénients :

- L'utilisation requiert les droits d'administrations car il doit avoir la possibilité de créer des "raw packets"
- Les services instables sont parfois interrompus à cause de ce scan

C'est le scan utilisé **par défaut** de Nmap quand il y a les droits d'administrations.

## 4) *UDP Scans*

Les connexions UDP sont **"stateless"**, c'est-à-dire qu'ils se contentent juste d'envoyer des paquets en espérant qu'ils arrivent à destination. 

Ce qui rend l'UDP pratique pour les connexions qui se base sur la vitesse plutôt que la qualité. Mais ça rend aussi **plus dur et beaucoup plus lent le scan.** La plupart du temps, il ne devrait pas y avoir de réponse, le port sera donc marqué comme ouvert/filtré. Si un port UDP est fermé, il renverra un paquet ICMP contenant le message "port unreachable", ce qui permet à Nmap de connaitre les ports fermés et de les marqués.

Une bonne pratique est d'utilisé ce scan avec un argument supplémentaire, celui de "--top-port <number>" qui permet de **déterminer les X ports les plus communs a scannés.**

## 5) *NULL, FIN et Xmas Scans*

Ils sont tous les 3 liés et sont plus furtif que le SYN Scan. La réponse si le port est ouvert est **identique** que l'UDP Scan.

### 5.1) Null Scans

Comme son nom l'indique, c'est quand le paquet TCP n'a pas de flag d'établi. Le port ciblé répondra par un RST s'il est fermé.

![null](https://i.imgur.com/ABCxAwf.png)

### 5.2) Fin Scans

Preque le même que le Null Scan sauf qu'un flag FIN est établi. Encore une fois, nmap reçoit un RST si le port est fermé.

![fin](https://i.imgur.com/gIzKbEk.png)

### 5.3) Xmas Scans

On va envoyé un paquet malformé et on espère aussi un paquet RST en retour si le port est fermé.

![xmas](https://i.imgur.com/gKVkGug.png)

## 6) *ICMP Network Scanning*

**Notre objectif est de cartographier l'infrastructure réseau de nore cible**, une façon de le faire est d'utilisé ce scan.

Nmap va envoyé un paquet ICMP à chaque adresses IP possible du réseau, s'il reçoit une réponse Nmap marque l'adresse IP comme étant "en vie". Nous verrons les commandes plus tard.

## 7) *NSE Script Overview*

Le "Nmap Scripting Engine" (NSE) est un programme de Nmap en langage LUA. Il peut être utilisé pour diverses manières de scanner des vulnérabilités à automatiser l'exploitation de celle-ci.

Il y a plusieurs catégories :

- Safe
- Intrusive
- Vuln
- Exploit
- Auth
- Brute
- Discovery
- ...

## 8) *Travailler avec le NSE*

Pour exécuter un script, nous avons diverses manières :

```bash
--script=<script-name>
```

Quelques scripts requierent des arguments, ils peuvent être mis grâce à la commande :

```bash
--script-args
```

La nomanclature des arguments est toujours le nom puis l'argument, le tout séparé par un point.

## 9) *Rechercher des scripts*

Les scripts de Nmap sont tous repris dans le dossier **"/usr/share/nmap/scripts"**

Il y a deux façon de chercher un scripts, soit par le fichier script.db, soit par la commande :

```bash
ls -l /usr/share/nmap/scripts/*<Nom>*
```

## 10) *Les commandes Nmap*

Voici une liste non exhaustive des commandes Nmap :

```bash
nmap -sS (SYN SCAN)
nmap -sU (UDP SCAN)
nmap -O (Detect OS)
nmap -sV (Detect Version Service)
nmap -v ou -vv (Verbosity et Verbosity lvl2)
nmap -oA (Save Nmap results en 3 formats)
nmap -oN (Save en format normal)
nmap -oG (Save en format Grepable)
nmap -A (Agressive mode)
nmap -T<0-5> (Timing mode)
nmap -p 80 (Port 80)
nmap -p 1000-1500 (Port 1000 à 1500)
nmap -p- (Tous les ports)
nmap --script (Script)
nmap --script=vuln (Scripts catégorie vuln)
```

