## 1) *How many services are running under port 1000 ?*

Pour trouver combien de services sont en utilisation sur la machine, nous allons utiliser l'outil Nmap.

Il permet de scanner les ports de la machine avec divers options.

```bash
nmap -A -sT <ip address>
```

-A : Pour entrer dans le mode agressif, càd la détection d'OS, de version, script scanning et traceroute.

-sT: pour scanner en utilisant le TCP qui sera plus rapide que l'UDP.

On trouve donc qu'il y a 2 service d'utilisés sur les ports 21 et 80 en dessous de 1000.

## 2) *What is running on the higher port ?*

Comme on l'a vu sur l'étape précédente un service **SSH** tourne sur le port 2222.

## 3) What's the CVE you're using against the application ? 

Pour ce faire on va analyser plusieurs éléments, on peut commencer par le FTP ou le site HTTP.

J'ai commencé par le HTTP, cependant on ne trouve rien à l'adresse IP. J'ai donc utilisé l'outil **dirbuster** pour énumérer les différents dossiers qui pourraient être présent sur le site. Et là, on trouve un site sur l'url :

http://<ip address>/simple

On voit que le site utilise un CMS et que celui-ci à la version 2.2.8. Lorsqu'on tape cette version sur google ou qu'on fait une recherche avec **searchsploit**. On obtient une vulnérabilité listée sur exploit-db.

La CVE est donc : CVE-2019-9053

## 4) *To what kind of vulnerability is the application vulnerable ?*

On voit grâce au titre sur exploit-db que la vulnérabilité est liée à une **injection SQL.**

La réponse sera donc en anglais : SQLi pour SQL injection.

## 5) *What's the password ?*

On va télécharger le programme python de l'exploit disponible sur exploit-db. Celui-ci comporte des erreurs à cause de python3 qu'on peut simplement corriger en éditant le fichier. 

Ensuite on va lancer l'exploit avec la commande suivante :

```bash
python3 46635.py -u http://10.10.25.124/simple/ --crack -w /usr/share/wordlists/rockyou.txt
```

-u : Spécifie l'URL a attaqué

--crack : pour dire que l'on va essayé de cracker le site avec la wordlist spécfiée.

-w : Spécifie la wordlist a utilisée pour le crack, ici rockyou.

Une fois le programme terminé , vous aurez divers éléments :

- Le Salt
- Le Username
- L'email
- Le hash du mot de passe

Grâce à l'outil **Hashcat**, on va pouvoir retrouver le mot de passe de notre utilisateur. Avec la commande suivante :

```bash
hashcat -O -a 0 -m 20 0c01f4468bd75d7a84c7eb73846e8d96:1dac0d92e9fa6bb2 /usr/share/wordlists/rockyou.txt 
```

-O : Pour activer l'optimisation du kernel qui limite la longueur des mots de passes

-a 0 : Pour activer l'attaque par dictionnaire ou "Straight"

-m 10 : Pour spécifier e type de hash, ici md5

Ensuite on vient mettre le hash puis : puis le salt et la wordlist.

Le mot de passe qu'on trouvera sera : secret.

## 6) *Where can you login with the details obtained ?*

On peut facilement deviner que cet utilisateur et ce mot de passe, nous servira pour le ssh.

## 7) *What's the user flag ?*

Il suffit de se connecter en ssh sur le port 2222 avec les credentials précédemments trouvés.

## 8) *Is there any other user in the home directory ? What's its name ?*

Il suffit d'un peu naviguer dans les répertoire pour s'en apercevoir.

## 9) *What can you leverage to spawn a privileged shell ?*

Avec la commande :

```bash
sudo -l 
```

Elle nous permet de connaitre les commandes ne necéssitant pas d'accès administrateur, ici la commande vim.

## 10) *What's the root flag ?*

On peut obtenir un accès en cherchant sur google les commandes liés à vim pour devenir super utilisateurs. Une fois la commande établie, la commande "whoami" nous indique bien qu'on est root. Il nous suffit de naviguer jusqu'au dossier root et le tour est joué.

