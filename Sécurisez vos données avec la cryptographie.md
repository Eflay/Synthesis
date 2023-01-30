## 1) *Découvrez la cryptographie*

**La cryptologie est la science du secret.** Elle se compose de 2 disciplines :

- La **cryptographie,** qui comprend l’ensemble des méthodes  de protection d'une information. Elle sert à garantir la confidentialité d'une information lors de communications ou de son stockage, en  utilisant le chiffrement. 
- La **cryptanalyse,** correspond aux méthodes utilisées pour analyser les messages chiffrés et "casser" la protection  cryptographique de ces messages, afin de retrouver l'information claire  sans connaître la clé de déchiffrement.

### 1.1) Le vocabulaire

- Le chiffrement :

Le **chiffrement** est la transformation d'une information  en clair en une information chiffrée, incompréhensible, mais que l'on  peut déchiffrer avec une clé pour obtenir l'information en clair originale.

- Le message en clair :

Un **message en clair** est une information non protégée et compréhensible par tout le monde.

- Un texte chiffré :

Un **texte chiffré** est une information incompréhensible pour qui ne possède pas la clé de déchiffrement, mais qu'on peut  déchiffrer, retransformer en texte clair, si on possède la clé.

- Un algorithme de chiffrement :

Un **algorithme de chiffrement** est une fonction qui prend en entrée le texte clair et la clé de chiffrement, transforme le texte par des opérations, et fournit en sortie un texte chiffré.

- Une clé de chiffrement :

La **clé de chiffrement** est l'information qui permet de transformer un texte clair en texte chiffré en utilisant un algorithme de chiffrement.

### 1.2) Méthodes d'attaques

L'attaque par force brute consiste à **essayer toute les valeurs de clé possibles** pour retrouver le texte clair.

On peut s'y protéger simplement grâce au chiffrement par substitution, par exemple. Avec ce chiffrement, il y aura 26! clés possibles. Ce qui contraint l'attaque par force brute a être beaucoup plus longue.

L'analyse fréquentielle consiste à **analyser la fréquence d'une lettre dans le message chiffré et à déduire le texte en clair.** Par exemple si la lettre V apparaît souvent, cela veut dire qu'elle remplace la lettre E. En effet le E dans la langue française est le plus fréquent.

### 1.3) Kerckhoffs

Monsieur Auguste Kerckhoffs va énoncé, à la fin du 19e siècle, les principes fondamentaux de la cryptographie moderne :

- La sécurité d'un algorithme de chiffrement doit uniquement être basée sur le fait que **l'attaquant ne connaît pas la clé**
- Les algorithmes de chiffrement doivent être **physiquement** ou **mathématiquement impossibles** **à résoudre pour l'attaquant**
- Le système doit être **adapté à son utilisation pratique** et la **clé** doit facilement être **modifiable**

Il faut aussi se dire que l'adversaire **connait toujours le système.**

### 1.4) Le chiffrement One-Time Pad

**La clé n'est jamais répétée dans l'opération de chiffrement,** ce qui empêche de casser le code avec les méthodes de cryptanalyse fréquentielle.

**Le principe de Claude Shannon dit que pour qu'une sécurité soit inconditionnelle, il faut qu'une clé aléatoire soit aussi longue que le message et utilisée une seule fois.**

## 2) *Générez des nombres aléatoires*

Vous utiliserez des nombres aléatoires pour divers raisons :

- Générer des clés secrètes
- Générer des nonces cryptographiques (IV, Salt, ...)
- Générer des nombres imprévisibles
- Simuler des jeux de hasard

Les algorithmes informatiques sont **déterministes**, càd qu'ils reproduisent les mêmes résultats si les paramètres sont inchangés. Pour ajouter la part d'aléatoire, on va utiliser **une source d'entropie externe.**

**L'entropie, c'est la mesure de la quantité de hasard d'une séquence de bits.**

En plus de l'entropie externe, une suite de nombres aléatoires doit avoir une distribution uniforme.

![y](https://user.oc-static.com/upload/2019/02/27/15512666362634_GNA%20%281%29.png)

Les fonctions de génération de nombres aléatoires sont **très lentes et coûteuses en ressources.**

Pour contrer ces inconvénients, on utilisera **des fonctions de génération de nombres pseudo-aléatoire**

Un **générateur de nombres pseudo-aléatoires (GNPA)**, c’est une fonction qui accepte une valeur en entrée, appelée **graine**, et qui fournit en sortie un nombre qui a l'apparence d'un nombre aléatoire, mais qui est en réalité le résultat d'un calcul algorithmique.

Les GNPA ont deux utilités :

- ils permettent de générer un nombre pseudo-aléatoire d'une taille plus grande que le nombre aléatoire utilisé comme graine.
- Si on appelle un GNPA avec la même graine, on obtiendra les mêmes résultats. Celui-ci est donc **déterministe**

![t](https://user.oc-static.com/upload/2019/02/27/15512668678217_p1c2a.png)

Les règles pour qu'un GNPA soit cryptographiquement sécurisé sont :

- Etre statistiquement aléatoire
- Etre imprédictible
- Etre résistant à une attaque sur les résultats précédents
- Avoir une période suffisamment longue (temps de rentrer dans un cycle)

## 3) *Le chiffrement symétrique*

Le **chiffrement symétrique** est un système de chiffrement qui utilise **la même clé secrète** pour le **chiffrement** et le **déchiffrement.**

### 3.1) Le chiffrement par flux

Il utilise une clé secrète de taille fixe, qui peut être plus petite que le message en clair. On utilisera un GNPA déterministe pour transformer la clé secrète en un nombre aléatoire, appelé **flux de clé**. Ensuite, on peut effectué l'opération bit à bit XOR entre le message en clair et le flux de clé pour obtenir le texte chiffré.

**Attention à ne jamais utiliser deux fois la même clé**.

Ce chiffrement est la solution la plus rapide, mais elle est aujourd'hui remplacée par le chiffrement par bloc.

### 3.2) Le chiffrement par bloc

Le chiffrement par bloc consiste à **découper un message en blocs de taille fixe**. Chaque bloc est chiffré avec la clé secrète et une fonction de chiffrement de bloc interne, ce qui donne un bloc chiffré de la même taille.

L'algorithme le plus utilisé est **AES** (Advanced Encryption Standard)

Il existe plusieurs modes de chiffrement par bloc :

- ECB (Electronic Code Book)
- CBC (Cipher Block Chaining)
- CTR (CounTeR)

#### 3.2.1) ECB

Vous réalisez le chiffrement de chaque bloc séparément et rassemblez tous les blocs en sortie pour former le texte chiffré.

![i](https://user.oc-static.com/upload/2019/02/27/15512717709847_p1c3a.png)

Le défaut principale est que **tous les blocs en clair identiques vont donner le même bloc chiffré.** Ce chiffrement est donc à éviter.

![h](https://user.oc-static.com/upload/2019/02/27/15512716971666_Capture%20d%E2%80%99e%CC%81cran%202019-02-27%20a%CC%80%2013.47.11-min.png)

#### 3.2.2) CBC

Ce mode consiste à effectuer l'opération XOR entre le bloc clair actuel  et le bloc chiffré précédent, avant de chiffrer le bloc actuel. Pour le  premier bloc, il n'y a pas de bloc précédent. On effectue l'opération  XOR avec une variable aléatoire appelée **vecteur d'initialisation** (IV), et on transmet l'IV en clair avec le texte chiffré. 

![i](https://user.oc-static.com/upload/2019/02/27/15512723064787_p1c3b.png)

L'IV ne doit jamais être réutilisé avec la même clé, pour contrer l'attaque de message en clair choisi.

#### 3.2.3) CTR

Ce mode imite le fonctionnement d'un chiffrement de flux, en utilisant un **compteur** qui s'incrémente à chaque bloc. Le compteur et la clé sont chiffrés  avec la fonction de chiffrement de bloc, ce qui donne un flux  pseudo-aléatoire découpé en blocs. Vous effectuez ensuite l'opération  XOR entre le bloc du flux pseudo-aléatoire et le bloc en clair, ce qui  donne le bloc chiffré.

![t](https://user.oc-static.com/upload/2019/02/27/15512724008503_p1c3c.png)

Il permet d'effectuer le chiffrement de manière parallèle, càd de chiffrer simultanément plusieurs blocs.

### 3.3) Taille de la clé

**La taille de la clé est cruciale pour la sécurité du chiffrement,** même si ce n'est pas le seul paramètre.

Pour résister à une attaque par force brute, le chiffrement doit **avoir un nombre de combinaisons de clé supérieur à ce qu'un attaquant peut calculer dans la pratique**. Actuellement, il est conseillé d'utiliser des **clés de 128 bits minimum.**

## 4) *Le hachage*

Une **fonction de hachage** est une fonction qui prend en entrée des données arbitraires, c'est-à-dire de différents types et tailles, et qui fournit en sortie une donnée de taille fixée. Cette fonction est **déterministe**, la sortie est appelée **haché ou empreinte**

Les fonctions de hachage cryptographique ont plusieurs utilités :

- Contrôler l'intégrité d'un message
- Stocker des mots de passe
- Générer des nombres pseudo-aléatoire
- Preuve de travail des blockchains

Elles ont aussi plusieurs sécurité à respecter :

- Etre irréversible
- Etre résistant aux collisions
- Etre pseudo-aléatoire

Une **collision** désigne deux données de valeurs différentes qui ont un haché de la même valeur.

Si l'ensemble des messages réalistes est beaucoup plus petit que  l'ensemble des hachés, et que les hachés ont une distribution aléatoire  par rapport aux messages, **le risque de collision est faible**.

![r](https://user.oc-static.com/upload/2019/02/27/15512776480571_Collision-hache.png)

## 5) *Contrôlez l'intégrité des messages*

L'intégrité des données désigne le fait que les données ne soient pas modifiées au cours d'une communication ou de leur stockage, que les données soient chiffrées ou non.

Un **code d'authentification de message** ou ***MAC\* (Message Authentication Code)** est une méthode de calcul d'une valeur de contrôle qui permet au  destinataire d'un message de vérifier l'intégrité d'une donnée reçue.

Ce système est composé de 2 fonctions :

- Une fonction MAC de création du code MAC
- Une fonction V de vérification du code MAC

Pour qu'un MAC soit sécurisé, il est nécessaire d'utiliser une clé  secrète qui est partagée entre l'expéditeur et le destinataire.

Cette méthode nuit à la performance du système à cause de l'augmentation des données a transporter.

**Le système CBC-MAC consiste donc à chiffrer entièrement le message en mode CBC, et à ne conserver que le dernier bloc chiffré.** Cependant c'est sécurisé uniquement si la taille du message est fixée à l'avance. Si la taille du message n'est pas fixée, un attaquant pourrait faire une attaque de type extension de message.

Une **attaque de type extension de message** désigne une  vulnérabilité où un attaquant, connaissant le message envoyé m et le code MAC associé, mais ne connaissant pas la clé secrète du code MAC, est capable d'allonger le message m en ajoutant des données en fin de message, et de calculer le nouveau code MAC valide.

Un **code HMAC (Hashed-MAC)** est un code MAC créé avec une fonction de hachage et une clé secrète.

## 6) *Le chiffrement asymétrique*

**Comment échanger la clé de manière confidentielle si l'on ne dispose pas de canal de communication sécurisé ?**

En 1976, les cryptologues Diffie et Hellman ont proposé une solution révolutionnaire à ce problème : le **protocole d'échange de clés Diffie-Hellman**. 

L'échange de clés Diffie-Hellman consiste à échanger une clé secrète  entre Alice et Bob sur un réseau non sécurisé de manière confidentielle. Il se déroule comme ceci :

![r](https://user.oc-static.com/upload/2019/08/13/15656923763204_diffie-hellman-v2.jpg)

Dans le chiffrement asymétrique, on utilise **la clé publique du destinataire** pour chiffrer et **la clé privée du destinataire** pour déchiffrer un message. 

**Comment faire donc pour assurer l’intégrité de l’émetteur du message ?**

En plus de chiffrer RSA permet de **signer un message**, c'est-à-dire d'apporter la preuve que l'expéditeur est bien la personne qu'il prétend être. Cela fonctionne avec le même principe que pour le MAC, une fonction de création et de vérification.

Seul l'auteur du message peut signer ses propres messages, c'est le **principe de non-répudiation d'un message signé**, en plus de l'authentification.

Cependant signer directement le message a plusieurs inconvénient :

- La longueur
- La lenteur
- La traçabilité

**Pour éviter ces problèmes, vous ne signez pas directement le message mais le haché du message avec une fonction de hachage cryptographique.**

## 7) *Créer des certificats numériques*

