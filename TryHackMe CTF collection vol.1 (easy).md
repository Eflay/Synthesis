Voici le lien du CTF :
[CTF](https://tryhackme.com/room/ctfcollectionvol1)

## 1) *What does the base said ?*

Pouvez-vous déchiffrer le texte suivant ?
VEhNe2p1NTdfZDNjMGQzXzdoM19iNDUzfQ==

On reconnait souvent **l'algorithme de chiffrement base64** car la chaine de caractère est **un multiple de 4** et que **le padding peut se faire jusqu'à deux fois avec le symbole =** en fin de texte. Pour ce faire aller donc sur ce site [Base64Decode](https://www.base64decode.org/) et mettez le message. 
Ce qui retourne le texte suivant :
**THM{ju57_d3c0d3_7h3_b453}**

## 2) *Meta Meta*

Une fois que vous avez télécharger l'image. Grâce aux titre nous pouvons avoir une idée d'où chercher (meta data).
Rendez-vous sur une machine linux et exécuter la commande :

```bash
exiftool Findme.jpg
```

Exiftool est un logiciel permettant l'écriture, la lecture et la modification de meta data d'un fichier.
Une fois la commande exécutée, vous trouverez que l'Owner Name est le flag :
**THM{3x1f_0r_3x17}**

## 3) *Mon, are we going to be okay ?*

Une fois l'image téléchargé, on nous dit que quelque chose est caché dans l'image. C'est ce qu'on appelle **la stéganographie.** Un logiciel très répandu est **steghide.** Une fois que vous l'avez installé, vous pouvez faire la commande :

```bash
steghide extract -sf Extinction.jpg
```

On utilise l'option extract pour **extraire les données de l'image** s'il y en a et -sf pour spécifier **le stéganofile.**
Il n'y a pas besoin de spécifier de passphrase puisqu'il y en a pas.
Une fois ceci fait, ça vous renvoie qu'un fichier nommé **"Final_message.txt"** a été ajouté dans votre répertoire.
Lorsque vous faites un "cat" du fichier vous trouvez le drapeau suivant :
**THM{500n3r_0r_l473r_17_15_0ur_7urn}**

## 4) *Erm......Magick*

Comme vous le constatez, nous avons pas d'élément à télécharger ni d'indice dans le titre. Une bonne méthode est de commencer par analyser l'html du site pour voir s'il ne serait pas cacher là-dedans.
Pour ce faire, inspectez l'élément et au niveau du sous titre de la tâche, vous trouvez un élément caché qui contient le flag :
**THM{wh173_fl46}**
Une autre manière était simplement de surligner le sous titre et le flag apparaissait.

## 5) *QRrrrr*

Télécharger l'image qui contient un QRcode, scannez le et le tour est jouer :
**THM{qr_m4k3_l1f3_345y}**

## 6) *Reverse it or read it ?*

Encore une fois télécharger le fichier, le titre nous indique qu'il va falloir faire du reverse engineering.
Un outil très populaire est **Ghidra**, il permet de reverse le code pour le rendre lisible.
Une fois que vous l'avez installé avec Github, lancer le grâce à la commande :

```bash
ghidra
```

Après **créer un nouveau projet et glisser-déposer** votre fichier "hello.hello". 
Analysez-le pour permettre la lecture des fonctions du programme. Quand c'est fait, on va parcourir ce qui est le plus intéréssant càd les fonctions. On trouveras dans **la fonction skip** le flag suivant :
**THM{345y_f1nd_345y_60}**

## 7) *Another decoding stuff*

Vous avez le texte chiffré suivant :
3agrSy1CewF9v8ukcSkPSYm3oKUoByUpKG4L
Pour trouver de quel type d'algorithme de chiffrement il s'agit, on va aller sur :
[Cipher Identifier](https://www.dcode.fr/cipher-identifier)
Mettez le texte et ensuite il vous ai dit que le plus probable serait le base58.
Allez dans un décodeur de base58 en ligne et vous trouverez le flag suivant :
**THM{17_h45_l3553r_l3773r5}**

## 8) *Left or Right*

Cette fois-ci, on dit parle de chiffrement par caesar.
On va tout simplement prendre le texte chiffré et tester toutes les combinaisons de chiffrement par caesar grâce au site suivant :
[Caesar decode](https://www.dcode.fr/caesar-cipher)
Mettez votre texte et cochez toutes les possiblités.
Vous obtiendrez le flag qui était en décalage +19 :
**THM{hail_the_caesar}**

## 9) *Make a comment*

Pour ce flag, il suffit de faire les mêmes étapes que le flag de "Erm Magick"

## 10) *Can you fix it ?*

Une fois l'image téléchargée, on vous dit que l'image est corrumpue. Pour extraire l'image sous le format d'hexadécimal et ainsi essayer de réparer le fichier, nous allons utilisé l'outil "xxd".
Grâce à la commande :

```bash
xxd spoil.png > "NomFichier"
```

ici le ">" va permettre de renvoyer le résultat dans un fichier. On va ensuite ouvrir le fichier avec un éditeur de texte.
Préalablement, on peut regarder quel est la base hexadécimal pour un fichier png. Cela permettra de voir s'il y a une erreur dans le début de notre fichier.
Lorque vous comparez le début basique d'un fichier PNG et votre fichier, vous voyez une différence. Il faut donc supprimer cette différence et remettre l'hexadécimal adéquat.
Ensuite vous allez sur le site de :
[Cyberchef](https://gchq.github.io/CyberChef/)
Prenez votre message corrigé et collez-le dans les inputs. Puis dites que ca vient de l'hexadécimal (FROM hexa) et que vous voulez "render image", càd que le résultat doit être une image.
Et voilà le tour est joué :
**THM{y35_w3_c4n}**

## 11) *Read it*

On vous dit que le flag est sur un réseau social de TryHackMe. Dans votre barre de recherche, vous testez TryHackMe Social account et vous trouvez sur le 2e lien ce qui nous intéresse :
[TryHackMe](https://www.reddit.com/r/tryhackme/comments/jy8p3p/about_ctf_collection_vol1/)
Un commentaire nous dit de chercher "TryHackMe rooms Reddit", vous prenez le premier lien et voilà votre flag :
**THM{50c14l_4cc0un7_15_p4r7_0f_051n7}**

## 12) *Spin my head*

Comme d'habitude pour identifier l'algorithme de chiffrement, RDV sur :
[Cipher Identifier](https://www.dcode.fr/cipher-identifier)
Le message est probablement écrit en brainfuck, testons le decodeur brainfuck et le tour est joué :
**THM{0h_my_h34d}**

## 13) *An exclusive !*

Le titre vous donne un petit indice en parlant d'exclusive. Il fait référence à XOR "exclusive OR".
Il va falloir faire un calcule XOR entre le S1 et le S2, cela se fait facilement grâce au site suivant :
[XOR Calculator](http://xor.pw/#)
Vous obtenez le flag suivant :
**THM{3xclu51v3_0r}**

## 14) *Binary walk*

Le titre fait référence à l'outil binwalk, il permet de chercher des fichier cacher dans les images ainsi que des codes exécutables. Après avoir télécharger le fichier, on va faire la commande suivante :

```bash
binwalk -e hell.jpg
```

L'argument -e permet d'extraire automatiquement les types de fichiers connus.
Binwalk nous a crée un dossier à la suite de la commande. Si nous entrons dans celui-ci, nous trouvons un fichier texte que l'on ouvre pour trouver le flag :
**THM{y0u_w4lk_m3_0u7}**

## 15) *Darkness*

Un peu plus difficile à deviner ici on va jouer sur la couleur de l'image. Un outil peut nous aider, il s'agit de stegsolve :
[Stegsolve](https://github.com/zardus/ctf-tools/blob/master/stegsolve/install)
Après l'avoir installé, pour le lancer il faut faire :

```bash
java -jar stegsolve.jar
```

Ensuite mettez votre image et passez en revue les différentes manière. Vous finirez par trouver le flag :
**THM{7h3r3_15_h0p3_1n_7h3_d4rkn355}**

## 16) *A sounding QR*

De même que le flag Qrrrr, ici il nous renvoie vers un soundcloud. On entend dedans le flag suivant :
**THM{SOUNDINGQR}**

## 17) *Dig up the past*

Un site connu pour "retourner dans le passé" est celui-ci :
[Wayback Machine](https://archive.org/web/)
Sur le site vous allez à la date du 2 Janvier 2020 comme spécifier. Vous trouverez en scrollant le flag :
**THM{ch3ck_th3_h4ckb4ck}**

## 18) *Uncrackable*

Encore une fois, nous identifions l'algorithme de chiffrement, nous obtenons le chiffrement Vigenere.
Puis nous decodons celui-ci avec toutes les lettres de l'alphabet en anglais. 
Ce qui nous donne le flag suivant :
**TRYHACKME{YOU_FOUND_THE_KEY}**

## 19) *Small bases*

Celui-ci est un plus dur à trouver sans l'indice. Il faut d'abord rendre le message en hexadécimal puis le transformer en ASCII :
**THM{17_ju57_4n_0rd1n4ry_b4535}**

## 20) *Read the packet*

Le fichier téléchargé est **un pcapng** qui est un format de capture de paquet. Nous l'ouvrons dans wireshark. Une fois dedans, mettons le filtre http, nous aurons plus de chance de trouver quelque chose en rapport avec le flag.
En effet en examinant un passage, on obtient :
**THM{d0_n07_574lk_m3}**