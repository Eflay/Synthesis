## 1 ) Introduction

Les domaines et leurs cotations :

- **Networking Fundamentals** -- 24%
- **Network Implementations** -- 19%
- **Network Operations** -- 16%
- **Network Security** -- 19%
- **Network Troubleshooting** -- 22%

Il y a jusqu'à 90 questions pour 90 minutes à l'examen. De plus, il y a des QCM avec une seule réponse ou plusieurs a donné et aussi des simulations a réaliser.

Les questions de simulations seront les premières à être demandées à l'examen suivi des QCM.

Il faut au minimum **80%** (720/900) pour obtenir la certification lors de l'examen. Pour passer l'examen, il faut acheter un voucher sur le store de [CompTIA](https://store.comptia.org) ou l'acheter sur [Dion-Training](https://cart.diontraining.com/comptia-network-voucher-eur/) pour avoir 10% de réduction. 

Pour s’entraîner, on peut aussi télécharger le study guide.

## 2) Network Basics (OBJ 1.2 et 2.1)

#### *2.1) Network Basics (OBJ 1.2)*

Le but du réseau est de connecter des machines entres elles. Les réseaux sont devenus de plus en plus convergents au fil du temps.

Il n'est pas possible d'avoir une disponibilité de 100%, mais on peut s'y rapprocher. Une nomenclature a été décidée sur le "Uptime Guarantee" qui peut aller de 99% à 99.999%(The five nine of availability).

Pour le 99.999%, cela veut dire que le serveur peut être indisponible pendant maximum 5 minutes par an. Il est fondamental de garder le réseau disponible et en ligne en tout temps.

On peut faire plein de chose avec le réseau de nos jours comme : le partage de fichier, accéder au site web, réseaux sociaux, streaming video, email, ...

Le challenge est de pouvoir supporter tous ces nouveaux éléments. On verra différentes sections dans ce chapitre :

- Network Components
- Network Resources
- Network Geography
- Network Typologies
- Internet of Things (IoT)

#### *2.2) Network Components (OBJ 2.1)*

Dans cette section, nous parlerons de plusieurs éléments :

- Client
- Server
- Wireless Access Point
- Hub
- Switch
- Router
- Wan Link
- Media

##### 2.2.1) Client

**It's a device used by an end-user to access network.** Cela peut être une tablette, téléphine, serveur, ordinateur, ...

Cela peut être **n'importe quelles machines qui se connectent au réseau.**

##### 2.2.2) Server

**It's a device that provides resources to the rest of the network.** Il existe différents serveurs pour différentes fonctionnalités. Ils peuvent être hardware ou software.

##### 2.2.3) Hub

**Older technology that connects network devices together.** On ne les utilise plus maintenant. 

On pouvait monter plusieurs Hub entre eux pour avoir plus de ports disponible. Cependant, **ça augmentait le nombre d'erreurs réseaux.** L'information entrée dans un port est **rediffuser dans tous les autres ports.** Les Switchs sont la seconde génération de Hub, ils ont le "bridge" en plus.

##### 2.2.4) Wireless Access Point (WAP)

**It's a device that allows wireless devices to connect into a wired network.** Un WAP est comme un wireless Hub.

##### 2.2.5) Switch

**It's a device that connects network devices together.** Il agit comme un hub, mais il garde en mémoire les ports utilisés. Ce qui permet de ne pas rediffuser l'information partout mais seulement au port necéssaire.

Les switchs servent juste à rediriger les informations d'un port à l'autre. Ils sont aussi appelés "Smart Hub". Ils ont plus de sécurité et plus d'éfficacité sur l'utilisation de la bande passante.

##### 2.2.6) Router

**It's a device that connects two different networks together and forwards traffic to and from network.** Ils redirigeront les réseaux en fonction des adresses IP.

##### 2.2.7) Media

**Connects two devices or a device to a switch port.** Comme les cables ethernet, la fibre, ...

Chaque type de media a ses propres avantages et inconvénients.

##### 2.2.8) Wide Area Network (WAN) Link

**Phisically connects two geograhically dispersed networks.** Il permet de visiter les sites internet, ...

Il sert de connexion entre notre réseau interne et externe.

#### *2.3) Network Resources (OBJ 1.2)*

Il y a deux principaux modèles : 

- Client/Server Model
- Peer-to-Peer Model

##### 2.3.1) Client/Server Model

**Uses a dedicated server to provide access to files, scanners, printers and other resources.** L'administration et les sauvegardes sont plus faciles a réaliser.

Il n'y a qu'un seul serveur où les ressources sont stockées, ce qui permet la sauvegarde rapide, de même pour l'administration. **Cela permet la "Centralized Administration", "Easier Management", "Better scalability".**

Les incovénients de ce modèle sont : un coût élévé (serveur, infra, ...), des OS spécialisés, des ressources dédiées.

C'est le modèle le plus utilisé.

##### 2.3.2) Peer-to-Peer Model

**Peers share resources directly with others.** L''administration et les sauvegardes sont plus compliquées car les fichiers sont disperser sur différentes machines à différents endroits. Il n'y a pas de différentiation.

Les avantages de ce modèles sont : peu couteux, pas de ressources dédiées, pas d'OS spécialisés.

Vu qu'il n'y a pas de serveur, si notre machine est éteinte, on ne peut accéder au réseau P2P.

Les inconvénient sont : le management décentralisé, pas efficace pour un grand réseau, mauvaise adaptation.

#### *2.4) Network Geography*

On va commencer par l'ordre croissant :

- **PAN** : Personnal Area Network (Bluetooth, usb, ...), **smallest type of wired or wireless network and covers the least amount of area** (3m or less)
- **LAN** : Local Area Network, **connects components within a limited distance** (100m max), si l'on utilise ethernet -> IEEE **802.3**, si l'on utilise le wifi -> IEEE **802.11**
- **CAN** : Campus Area Network, **connects LANs that are building-centric across a university, ...**, (few miles range)
- **MAN** : Metropolitan Area Network, **connects scattered locations across a city or metro area** (25 miles)
- **WAN** : Wide Area Network, **connects geographically disparate internal networks and consists of leased lines or VPNs** (Worlwide area)

#### *2.5) Wired Network Topology*

Il y a deux façon de se représenter la topologie : 

- **Physical **: How devices are connected by media
- **Logical** : How the actual network traffic flows

Les différentes topologies :

- **Bus Topology** : Uses a single cable where each device taps into by using either a vampire tap or a T-connector (risque de colision car un seul cable)
- **Ring Topology** : Uses a cable running in a circular loop where each device connects to the ring but data travels in a singular direction. Pour contrer les colisions, on utilise un **Token Ring**. Il permet de donner de l'ordre aux demandes. Le problème qui persiste est la redondance si un cable se casse. Pour ce faire on utilisera le **FDDI** (Fiber Distributed Data Interface) qui permet d'avoir un second Ring. **Les RIng Topology modern sont généralement des FDDI RIng**. A L'EXAMEN quand RING -> FDDI RING
- **Star Topology** : Most popular physical LAN topology where devices connect to a single point, **si le point centrale casse c'est le réseau entier qui crash.**
- **Hub-and-Spoke Topology** : Similar to star but with WAN links instead of LAN connections and it is used for connecting multiple sites. Grâce a ces multiples hub, si l'un deux casse l'autre peut prendre le relais même si une partie du réseau sera down.
- **Full-Mesh Topology** : Optimal routing is always available as every node connects to every other node. Pour une redondance complète, mais quand il y a beaucoup de machines ca devient vite ingérable.
- **Partial-Mesh Topology** : Hybrid of the full-mesh and the hub-and-spoke topologies. Permet un réseau optimal entre plusieurs sites mais pas tous. Il faut connaitre les points importants.

#### *2.6) Wireless Network Topology*

Il y a différents modes à comprendre :

- **Infrastructure Mode** : Uses a wireless access point as a centralized point and supports wireless security controls. (Wifi maison)
- **Ad Hoc Mode** : Decentralized wireless network which creates P2P connections and does not require a router or access point.
- **Wireless Mesh Topology** : Interconnection of different types of nodes, devices or radios, cela permet d'avoir une connexion redondante et fiable. (Catastrophe naturelle, besoin de connexion)

#### *2.7) Internet of Things (IoT)*

**Tous les éléments qui sont connectés** comme : thermostat, montre, frigo, TV, ... font partie de l'IoT.

La 1ère technologie utilisée est la **802.11** -> **Wireless networks that can operate in infrastructure or ad hoc mode**

La 2e technologie est le **Bluetooth** -> **Low-Energy use variant of Bluetooth which allows for a mesh network**

La 3e technologie est la **Radio-Frequency identification (RFID)** -> **Uses electromagnetic fields to read data stored in embedded tags** (Clé hotel, traquer les colis, ...)

La 4e technologie est le **Near-field Communication (NFC)** -> **Enables two devices to communicate within a 4cm range** (Apple Pay, Google Pay, ...)

La 5e technologie est le **Infrared (IR)** -> **Operates with line of sight** (télécommande télé)

La 6e technologie est la **Z-Wave** -> **Provides short-range, low latency data transfer with slower rates and less power consumption than WI-fi** (Home Automation, lumière, ...)

La 7e technologie est le **ANT+** -> **Collection and transfer of sensory data** (pression pneu, tv, lumière)

## 3) OSI Model (OBJ 1.1 et 5.3)

L'acronyme OSI signifie Open Systems Interconnection Model. Il a été developpé en 1977 par **"Internal Organization for Standardization (ISO)"**. 

Il peut aussi être appelé OSI stack. Le modèle OSI est **TRES important pour l'examen**. Le logiciel Wireshark est un bon outil pour analyser ce qu'il se passe sur le réseau et fait partie de l'examen (5.3). Ce modèle sert aussi de référence **pour classifier les fonctionnalités du réseau en différentes couches.** De plus, il peut être utilisé dans beaucoup de technologies différentes

Le modèle n'est pas parfait de nos jours, par exemple, un fonctionnalité pour se faire sur plusieurs couches. Le réseau moderne se base sur le modèle **TCP/IP** 

Les 7 couches du modèles OSI sont :

1. **Physical Layer** (Bits)
2. **Data Link Layer **(Frames)
3. **Network Layer **(Packets)
4. **Transport Layer** (Segments)
5. **Session Layer** (Data)
6. **Presentation Layer** (Data)
7. **Application Layer** (Data)

#### *3.1) Physical Layer*

**Where transmission of bits across the network occurs and includes physical and electrical network characteristics.** Quand on utilise les cables ethernet, CAT5, fréquence radio, ... Les données envoyées sont toujours sous forme de **bits binaire**.

- **Tansition Modulation** : If it changes during the clock cycle, then a 1 is represented (otherwise, a 0 is represented)

Les cables ethernet (CAT5, CAT6) ont des embout appelés **RJ45**. Ce cable est fait selon 2 standard :

- TIA/EIA-568A
- TIA/EIA-568B

Cela va déterminer si l'on utilise des cables croisés ou direct. Un croisé, on aura un A et l'autre B. Pour un direct, on aura deux B.

Ces cables sont connectés suivant la topologie vue dans le chapitre précédent (2.5).

La communication peut être synchronisé de deux manières :

- **Asynchronous** : Uses start and stop bits to indicate when transmissions occur from the sender to the receiver.
- **Synchronous** : Uses a reference clock to coordinate the transmissions by both sender and receiver

Il y a deux façons d'utiliser la bande passante :

- **Broadband** : Divides bandwith into seperates channels
- **Baseband** : Uses all available frequencies on a medium (cable) to transmit data -> uses a reference clock

Pour optimiser son réseau, on pourra faire différents mécanisme :

- **Time-Division Multiplexing (TDM)** : Each session takes a turn, using time slots, to share the mediium between all users -> Chacun son tour avec un temps limité
- **Statistical Time-Division Multiplexing (StatTDM)** : Dynamically allocates the time slots on an as-needed basis -> Selon la demande avec un temps limité
- **Frequency-Division Multiplexing (FDM)** : Divides the medium into channels based on frequencies and each session is transmitted over a different channel

Ce qu'il faut retenir c'est que : **Multiplexing is getting more out of a limited network. Permet à plusieurs personnes d'utiliser une connexion BaseBand en même temps.**

Les exemples de matériel de la couche 1 sont : les cables (ethernet, fibre, coaxial), Bluetooth, Wifi, NFC, hubs, access point, ...

La couche 1 répète seulement ce qu'on leur donne.

#### *3.2) Data Link Layer*

**Packages data into frames and transmits those frames on the network.** 

Une MAC adresse signifie :

- **Media Access Control (MAC)** : Physical addressing system of a device which operates on a logical topology

Elle est établie : **Uses a 48-bit address assigned to a network interface card (NIC).**

Un exemple : 00:37:6C:E2:EB:62 -> chaque lettre/nombre = 4 bits

**Les 24 premiers bits** représentent servent à identifier le vendeur qui a fabriqué la NIC -> 00:37:6C

**Les bits suivants** représente une valeur unique de la machine -> E2:EB:62

Les machines de couche 2 se représentent le réseau de manière **logique**.

Pour controler l'information, on utilisera :

- **Logical Link Control (LLC)** : Provides connection services and allows acknowledgement of receipt of messages. -> **Outil basique de controle de flux** -> va permettre de ne pas surcharger le receveur en limitant le nombre d'information envoyées. Il permet aussi d'apporter une **"basic error control functions"** -> se fait en utilisant les checksum.

Il y a 3 différentes méthodes pour synchroniser les données dans la couche 2 :

- **Isochronous** : Network devices use a common reference clock source and create time slots for transmission.
- **Synchronous** : Network devices agree on clocking method to indicate beginning and end of frames and can use control characters -> l'inconvénient est d'avoir beaucoup de temps mort vu qu'on se règle au cycle.
- **Asynchronous** : Network devices reference their own internal clocks and use start and stop bits

#### *3.3) Network Layer*

**Forwars traffic (routing) with logical address.** 

Dans ce chapitre, on verra différents éléments :

- **Logical adressing**
- **Switching**
- **Route discovery and selection**
- **Connection services**
- **Bandwith usage**
- **Multiplexing strategy**

##### 3.3.1) Logical adressing

Il n'y a pas que les protocols IPv4 et IPv6. 

Un exemple d'adresse IPv4 : 10.10.10.10 -> 4 nombres séparés par des points -> **"dotted-octet notation"**

Comment la donnée est redirgée ou routé :

- **Packet switching** : Data is divided into packets and then forwarded
- **Circuit switching** : Decicated communication link is established between two devices -> même chemin
- **Message switching** : Data is divided into messages which may be stored and then forwarded -> stockage + packet switching

Le plus utilisé est le Packet switching car on a d'autre technologie pour vérifier si le message a été délivré.

##### 3.3.2) Route discovery and selection

**Manually configured as a static route or dynamically through a rounting protocol.** -> choisir le chemin du packet.

Le protocol de routage nous aide a décider comment les données vont être envoyées dans le réseau -> choisir le chemin le plus optimisé

##### 3.3.3) Connection Services

**Augment Layer 2 connection services to improve reliability.**

Permet d'avoir plus de controle sur le flux -> **Flow Control**

Le **Packet reordering** permet de diviser la donnée en packet et envoyé ces paquets dans différentes directions pour arriver à la destionation. 

Parfois, les paquets arrivent dans le mauvais ordre et le **Packet reordering** les remets dans le bon ordre. Caque paquet est numéroté et séquencé grâce au routing.

##### 3.3.4) Internet Control Message Protocol (ICMP)

**Sends error messages and operational information to an IP destination.**

Les commandes les plus utilisées par ce protocol sont ; ping et traceroute.

##### 3.3.5) Element à retenir

Les routeurs et les switchs Layer 3 (3 et 2), IPv4, IPv6, ICMP.

#### *3.4) Transport Layer*

Les données sont appelées **"Segments" pour le TCP et "Datagram" pour l'UDP.**

Il y a deux protocols de transport :

- TCP : Transmission Control Protocol, **conection-oriented protocol that is a reliable way to transport segments across the network.** -> Permet le cotrole du bon transport -> si segment échoue il est renvoyé. **Three-way Handshake TCP** 
- UDP : User Datagram Protocol, **connectionless protocol that is an unreliable way to transport segments across the network.** -> N'attend pas la connexion -> si datagram échoue, l'envoyeur n'est pas avertit. -> Bien pour le video streaming.

![TCP vs UDP](/home/eflay/Images/TCP_UDP.png)

Et d'autres fonctionnalités comme :

- Windowing : **Allows the clients to adjust the amount of data in each segment.** -> Sends less data with increased retransmissions ou Sends more data with decreased retransmissions. -> Exemple : le téléchargement

- Buffering : **Occurs when devices allocate memory to store segments if bandwith isn't readily available.** -> Garde les segments en données pour les envoyés quand c'est disponible -> Exemple : vidéo youtube qui se pré-charge -> Buffer Overflow si le buffer est trop rempli -> les données vont être abandonnées.

Les éléments de couche 4 sont : TCP, UDP, WAN Accelerator, load balancer, firewall

#### *3.5) Session Layer*

**Keep conversation separate to prevent intermingling of the data**. 

Ce que l'on va faire dans ce chapitre :

- Set up session : **Checking of user credentials and assigning numbers to sessions to help identify them.** -> Négociation de la session pour le service + qui commence
- Maintain session -> va découler divers éléments :
  - Transfer data
  - Reestablish connection
  - Acknowledge receipt
- Tear down session : **Ending of a session after the transfer is done or when the other party disconnects.** -> Arreter la session par une réussite ou une déconnexion

Exemple d'éléments de couche 5 : **H.323 et NetBIOS** 

- H.323/H.264 : **Used to set up, maintain and tear down voice and video connections.** -> Over Real-Time Protocol (RTP) -> Facetime, Skype, Youtube, ...
- NetBIOS : **Used to share files over a network.** 

#### *3.6) Presentation Layer*

**Formats the data to be exchanged and secures that data with proper encryption.**

Les mots à retenir dans cette couche sont :

- Data formatting : **Data is formatted by the computer to have compatibility between different devices.** -> ASCII, GIF, JPG, PNG
  - ASCII : **Ensures data is readable by receiving system**, provides proper data structures
- Encryption : **Used to scramble the data in transit to keep it secure from prying eyes and provide data confidentiality** -> Transport Layer Security (TLS)

Exemple d'éléments à la couche 6 : **Scripting Language (HTML, XML, PHP, JS, ...), Standart Text (ASCII, Unicode, EBCDIC), Pictures (Gif, JPG, PNG), Movie Files (MP4, ...), Encryption Algorithms (SSL/TLS)**

#### *3.7) Application Layer*

**Provides application-level services where users communicate with the computer.** -> File Transfer, Network Transfer

Les fonctionnalités sont : 

- Application services : **Unites communicating components from more than one network application.** -> File tranfer, file sharing, email (POP3, IMAP, ...), remote access, ...
- Service advertisement : **Sending out of announcements to other devices on the network to state the services they offer**. -> printer, file server, AD management

Exemple d'éléments de couche 7 : **POP3, IMAP, SMTP, HTTP, HTTPS, DNS, FTP, FTPS, SFTP, Telnet, SSH, SNMP, ...**

#### *3.8) Encapsulation and Decapsulation*

Encapsulation : **Process of putting headers (and trailers) around some data.**

Decapsulation : **Action of removing the encapsulation that was applied.**

Si on part de la couche 7 à la couche 1 -> **Encapsulation**

Si on part de la couche 1 à la couche 7 -> **Decapsulation**

On va utiliser un protocol pour ce faire :

- Protocol Data Unit (PDU) : **A single unit of information transmitted in a computer network.** -> bits, frames, packets, segments, data

![Encapsulation](/home/eflay/Images/encaop.png)

A partir du Layer 4, voici le header TCP :

![TCP Header](/home/eflay/Images/TCP Header.jpg)

Un autre élément important sont les Control Flag :

- SYN (Synchronization) : **Used to synchronise connection during the three-way handshake.**
- ACK (Acknowledgement) : **Used during the three-way handshake, but also use to acknowledge the successful receipt of packets**
- FIN (Finished) : **Used to tear down the virtual connections created using the three-way handshake and the SYN flag.**
- RST (Reset) : **Used when a client or server receives a packet that it was not expecting during the connection.**
- PSH (Push) : **Used to ensure data is given priority and is processed at the sending or receiving ends.**
- URG (Urgent) : **Similar to PSH and identifies incoming data as urgent.**

Le Header UDP :

![UDP Header](/home/eflay/Images/UDP-packet-1024x375.jpg)

Length : Combient de bits le packet fera.

Checksum : Permet des vérifications.

Ensuite, on va encore encapsuler au layer 3 avec le header IP :

![IP Header](/home/eflay/Images/IPv4_Packet-en.svg.png)

Ensuite, on va encore encapsuler au layer 2 avec le header Ethernet :

![Ethernet Header](/home/eflay/Images/Eth Header.jpg)

Parlons de la MAC address :

**A physical address that is used to identify a network card on the local area network** -> Permet de connaitre la destination.

Le champ EtherType :

**Used to indicate which protocol is encapsulated in the payload of the frame**. -> Détermine si l'on a utilisé le IPv4 ou IPv6.

Le payload peut être de maximum 46 bits sans VLAN et 42 bits avec. le MTU (MAximum transmission Unit) par défaut de ethernet est de 1500 bytes

En résumer : 

- **Layer 4 -> Ajout du port source et du port destination**
- **Layer 3 -> Ajout de l'IP source et de l'IP destination**
- **Layer 2 -> Ajout de la MAC source et la MAC destination**

## 4) TCP/IP Model (OBJ 1.1, 1.5 et 5.3)

**Aussi appelé le TCP/IP Stack ou le DoD Model.**

C'est une alternative au modèle OSI. Il n'y a que 4 couche. **La plupart des réseaux modernes sont basés sur ce modèle.**

Voici à quoi ressemble le Modèle TCP/IP par rapport au OSI :

![TCP Model](/home/eflay/Images/modele-osi-vs-tcp.png)

#### *4.1) Network Interface Layer (1)*

Tout ce qui concerne les caractéristiques physiques et électriques.

**Describes how to transmits bits across a network and determines how the network medium is going to be used.**

Comme medium -> les cables coaxial, fibre, ...

Exemple : Ethernet, Token Ring, FDDI, RS-232, ...

#### *4.2) Internet Layer (2)*

**Where data is taken and packaged into IP datagrams.**

Cela va contenir l'IP source et destination et rédirige les datagrams entre les différents hôtes sur le réseau.

Ils seront redirigé grâce au routing. Cette connexion va s'établir de façon externe.

Des exemples d'éléments à cette couche : **IP, ICMP, ARP, Reverse ARP**

#### *4.3) Transport Layer (3)*

**Defines the level of service and the status of the connection being used bu TCP, UDP or RTP.**

#### *4.4) Apllication Layer (4)*

**Dictated how programs are going to interface with the transport layer by conduction session management.**

Exemple d'éléments à cette couche : **HTTP, Telnet, SSH, SNMP, DNS, SMTP, FTP, ...**

#### *4.5) Data Transfer Over Networks*

Un port est -> **A logical opening on a system representing a service or application that"s listening and waiting for traffic.**

Les ports peuvent aller de 0 à 65 535, séparés en deux groupes :

- Well-know Ports : **0 à 1023**
- Ephemeral Ports : **1024 à 65 535** -> short-lived transport port

Comment les données sont transférées :

![Data Transfer](/home/eflay/Images/data transfer.png)

On envoie l'information par le biai des packets IPv4 -> **Consists of a source addres, destination address, IP flags and protocols**

Différence de Header TCP/UDP (rappel) :

![TCP/UDP](/home/eflay/Images/header.png)

#### *4.6) Ports and Protocols (OBJ 1.5) IMPORTANT*

- **File Transfer Protocol (FTP) -> 20,21 -> Provides insecure file transfers (clear text)**
- **Secure Shell (SSH) -> 22 -> Provides secure remote control of another machine using a text-based environment (chiffré) ** 
- **Secure File Transfer Protocol (SFTP) -> 22 -> Provides secure file transfers**
- **Telnet -> 23 -> Provides insecure remote control of another machine using a text-based (clear text)**
- **Simple Mail Transfer Protocol -> 25 -> Provides the ability to send emails over the network** -> RFC 821 en 1982 et RFC 5321 en 2008
- **Domain Name Service (DNS) -> 53 -> Converts domain names to IP addresses et inversément**
- **Dynamic Host Control Protocol (DHCP) -> 67, 68 -> Automatically provides network parameters to your clients, such as ther assigned IP address, subnet mask, ...**
- **Trivial Transfer Protocol (TFTP) -> 69 -> Used as a lightweight file transfer method for sending configuration files or network booting of an operating system**
- **Hypertext Transfer Protocol (HTTP) -> 80 -> Used for insecure web browsing**
- **Post Office Protocol v3 (POP3) -> 110 -> Used for receiving incoming emails**
- **Network Time Protocol (NTP) -> 123 -> Used to keep accurate time for clients on a network**
- **NetBIOS -> 139 -> Used for file or printer sharing in a windows network**
- **Internet mail Application Protocol (IMAP) -> 143 -> A newer method of rretreiving incoming emails which improves upon the older POP3**
- **Simple Network Management Protocol (SNMP) -> 161, 162 -> Used to collect data about network devices and monitor their status**
- **Lightweight Directory Access Protocol (LDAP) -> 389 -> Used to provide directory service to your network**
- **HTTP Secure (HTTPS) -> 443 -> Used for secure web browsing, SSL/TLS**
- **Server Message Block (SMB) -> 445 -> Used for windows file and printer sharing services**
- **System Logging Protocol (Syslog) -> 514 -> Used to send logging data back to a centralized server**
- **Simple Mail Transfer Protocol Transport Layer Security (SMTP TLS) -> 587 -> Secure and encrypted way to send emails**
- **LDAP Secure (LDAPS) -> 636 -> Provides secure directory services**
- **Internet Message Access Protocol over SSL (IMAP over SSL) -> 993 -> Secure and encrypted way to receive emails**
- **Post Office Protocol Version 3 over SSL (POP3 over SSL) -> 995 -> Secure and encrypted way to receive emails**
- **Structured Query Language Server Protocol (SQL) -> 1433 -> Used for communication from a client to the databse engine**
- **SQLnet Protocol -> 1521 -> Used for communcation from a client to an Oracle Database**
- **MySQL -> 3306 -> Used for communcation from a client to a MySQL Database engine** 
- **Remote Desktop Protocol (RDP) -> 3389 -> Provides graphical remote control of another client or server**
- **Session Initiation Protocol (SIP) -> 5060, 5061 -> Used to initiate VoIP and video calls**

![ports](/home/eflay/Images/ports.png)

#### *4.7) IP Protocol Types (Rappel)*

On va parler de différents protocols comme :

- TCP
- UDP
- ICMP
- GRE
- IPsec

Et le concept de : **Connectionless vs Connection-oriented**

##### 4.7.1) TCP

C'est un protocol de la couche Transport (4) du modèle OSI. **Used on top of the Internet Protocol for the reliable packet transmission**. Rappel des parties précédentes. Il est connection-oriented

##### 4.7.2) UDP

L'opposé de TCP. Utilisé pour le streaming audio et vidéo.

##### 4.7.3) ICMP

A network level protocol that is used to communicate information about network connectivity issues back to the sender.

##### 4.7.4) Generic Routing Encapsulation Protocol (GRE)

**A tunneling protocol that was developed by Cisco to encapsulate a wide variety of network layer protocols inside a virtual point-to-point or point-to-multipoint link over an Internet Protocol network.**

Il n'a pas de chiffrement. Important de savoir sur MTU, maximum 1500 bytes.

##### 4.7.5) Internet Protocol Security protocol (IPsec)

**Set of secure communication protocols at the network or packet processing layer that is used to protect data flows between peers.**

On pourra permettre différentes fonctionnalités :

- Data confidentiality
- Data Integrity
- Origin Authentication
- Anti-replay

Il en découle deux sous protocols :

- Authentication Header (AH) : **A protocol within IPSec that provides integrity and authentication**
- Encapsulating security payload (ESP) : **Provides encryption and integrity for the data packets sent over IPsec**

## 5) Media and cabling distribution (OBJ 1.3 et 5.2)

**Material used to transmit data over the network.**

Il y a trois types de media différents :

- Copper
- Fiber Optic
- WIreless -> Dans une autre section

#### *5.1) Copper Media*

Il y a trois types de copper media différents :

- Coaxial
- Twisted pair
- Serial

##### 5.1.1) Coaxial

**Inner -> insulated conductor or center wire passes data.** -> Center core

**Outer -> Braided metal shiel used to help shield and protect the data transmission.**

- Cela permet de résister aux ondes électromagnétique

<img src="/home/eflay/Images/Copper.png" alt="Copper" style="zoom:150%;" />

Les types de cables coaxials :

- RG-6 : **Commonly used by local cable companies to connect individual homes**
- RG-59 : **Typically used to carry composite video between two nearby devices, such as from a cable box to the television**

Comment ils se connectent aux éléments :

- F-connector : **Typically used for cable TV and cable modem connections**
- BNC (Bayonet Neill Concelman connector ou British Naval connector) : **Was used for 10BASE2 Ethernet networks**

Le cable coaxial moderne :

- Twinaxial Cable : **Similar to coaxial cable but uses two inner conductors to carry the data instead of just one** -> courte portée mais rapide +- 10gb/s, moins d'énergie.

##### 5.1.2) Serial

**Usually have a series of straight copper wires inside a single cable or plastic jacket**

Ils auront un connecteur de type **DB-9 ou DB-25 (RS-232)**. -> 9 pins ou 25 pins D-subminiature

Ils sont utilisés pour les connexion séries asynchrones et se connecte à un modem externe.

##### 5.1.3) Twisted Pair

Les cables le plus populaire au sein de LAN.

Dans ce cable, il y a 8 fils de cuivre pour le cable. -> Chacun est torsadé en pair.

**Plus les pairs torsadées sont nombreuse moins il y a de fréquence électromagnétique.**

Il y a différents types de cables allant de CAT5 à CAT8 -> moins vite au plus vite.

Il y a 2 types de twisted pair :

- UTP (Unshielded Twisted Pair) : **moins chère, tout plastic -> le plus populaire pour les LANs.**
- STP (Shield Twisted Pair) : **plus chère, enrobé de métal -> minimiser les interférence EMI**

Ils peuvent aller tous les deux à une centaine de mètres.

Il y a 2 types de connectors :

- RJ-45 : **Coonecteur 8 pins -> le plus utilisé -> la plupart utilisent 4 pins (CAT5)**
- RJ-11 : **Connecteur 6 pins -> téléphonie -> le plus souvent 2 pins utilisées -> une pin réservé au ring et l'autre pour le signal.**

Que veut dire RJ :

- Registered Jack : **Used to carry voice or data which specifies the standards a device needs to meet to connect to tje phone or data network**

##### 5.1.4) Bandwidth

**Theorical measure of how much data could be transferred from a source to its destination.**

##### 5.1.5) Throughput

**Actual measure of how much data transferred from a source to its destination**

<img src="/home/eflay/Images/BD.png" alt="Bandwidth" style="zoom: 150%;" />

**Faire attention a la différence entre maximum distance du cable et la distance par rapport à IDF.**

Keep cable runs under 70 meters from the IDF to the office

##### 5.1.6) Straight-Through Cable (Patch Cable) -> Cable direct

**Contains the exact same pinout on both ends of the cable.**

Les cables T-568B sont préférés pour cablé un building si aucune autre méthode n'est appliquée.

Ils sont utilisés pour connecter un DTE à un DCE :

- DTE : Data Terminal Equipment -> **“Endpoint” devices that connect to a piece of data communications equipment or DCE (e.g. laptops, desktops, servers, and routers)**
- DCE : Data Communication Equipment -> **Includes things like switches, modems, hubs, and bridges**

![Cable Direct](/home/eflay/Images/Cable Direct.png)

##### 5.1.7) Crossover Cable -> Cable Croisé

**Swaps the send and receive pins on the other end of the cable when the connector and its pinout are created**

Les pairs verts et oranges s'échangent -> un bout T-568A, l'autre T-568B

![Cable Croisé](/home/eflay/Images/Cable Croisé.png)

##### 5.1.8) Medium Dependent Interface Crossover (MDIX)

Les switchs modernes ont cette technologie qui permet : 

**An automated way to electronically simulate a crossover cable connector even if using a straight-through patch cable**

##### 5.1.9) Plenum and Non-Plenum cable

Plenum Cable :

**A special coating put on a UTP or an STP cable that provides a fire-retardant chemical layer to the outer insulating jacket**

Permet une résistance au feu et au fumée nocive. Obliger selon les lois en vigueur du pays dans les murs, plafond, ...

Non-Plenum Cable :

Aussi connu sous le nom PVC, utilisation normal UTP/STP.

#### *5.2) FIber Media*

**Uses light from an LED or laser to transmit information through a glass fiber**

Ces cables sont immunisés aux interférence électromagnétique. Utilisation de la lumière à la place de l'électricité.

Les avantages :

- Portée grandement augmentée -> plusieurs centaines de mètres voire km
- Bande passante plus importante -> Tb/s

**La plupart des entreprises continuent d'utiliser les cables en cuivre car les routeurs et les switchs ne sont pas adaptés à une telle vitesse.**

Les inconvénients :

- Très chère
- Plus difficile a travailler

Il y a deux modes de fibre :

- Single Mode (SMF) : **Used for longer distances and has smaller core size which allows for only a single mode of travel for the light signal** -> 8.3-10µ in diameter -> + chère
- Multimode (MMF) : **Used for shorter distances and has larger core size which allows for multiple modes of travel for the light signal** -> 50-100µ in diameter -> 2hm ou moins -> - chère

Les différents connecteurs sont :

<img src="/home/eflay/Images/Fiber Connectors.png" alt="FIber C" style="zoom:150%;" />

Les APC ont des embouts verts et les UPC des embouts bleus. **Moins de signal dans l'UPC que dans l'APC**

Une autre technologie importante est :

- Wavelength Division Multiplexing (WDM) : **Combines multiple signals into one signal and sends over a single fiber optic strand using different wavelengths of the laser light source**

![WDM](/home/eflay/Images/WDM.png)

Le plus souvent en mode SMF.

il y a deux types de WDM :

<img src="/home/eflay/Images/WDM types.png" alt="WDM types" style="zoom:150%;" />

#### *5.3) Transceivers*

**Device that sends (transmits) and receives data**

Les critères a comparé entre un cable de cuivre et la fibre sont **la bande passante, la distance, la résistance à l'EMI et la sécurité.**

Avantages de la fibre :

- Bande passante supérieure -> 69Tb/s +
- Plus de distance -> 40km+
- Immuniser aux EMI grâce à la lumière
- Meilleur sécurité

Avantages du cable de cuivre :

- Moins chère
- Facile a installer
- Outils pas chère

Les cables de cuivres <100m et 10 Gb/s

##### 5.3.1) Media Converter/Transceiver

**Converts medio from one format to another.** Elément de couche 1.

Exemple : ethernet to fiber optic et inversément

##### 5.3.2) Type de Transceivers

Il y a plusieurs types :

- Bidirectional (half-duplex) : **Where devices must take turns to communicate** -> Talkie
- Duplex : **Full duplex occurs when devices can both communicate at the same time** -> phone

Les types utilisé dans les switchs et les routeurs :

- GBIC : **Standard, hot-pluggable gigabit Ethernet transceiver (copper or fiber)**
- Small Form-factor Pluggable (SFP) : **Compact, hot-pluggable optical module transceiver** -> Mini-GBIC
- SFP+
- Quad Small Form-factor Pluggable (QSFP)

<img src="/home/eflay/Images/Transceivers.png" alt="Transceivers" style="zoom:150%;" />

#### *5.4) Cable Distribution*

**An organized system to connect the network’s backbone in the main distribution frame to the intermediate distribution frames and finally to the end user’s wall jacks**

Penchons nous sur le Cable Distribution System :

**Use an organized system that is hierarchical**

- Demarcation Point : **Where the internet service provider's connection ends and ypur network begin**

Après la démarcation, on va connecter le réseau à notre routeur puis à notre **"backbone switch"**, qui servira pour se connecter à l'ensemble de notre réseau. Un **"edge switch"** est connecter pour nos utilisateur et est un enfant du **backbone switch**.

Le backbone switch sera connecté au MDF (Main distribution Frame) -> **MDF = main starting point for all interior cabling**. Les IDF (intermediate Distribution Frame) seront connecté au MDF.

Pour connecter le MDF aux IDF, on utilisera le **"Cable Tray"** -> **A unit or assembly of units that form a rigid structural system to securely support the cables and raceways.**

Le mieux est de minimiser les cables traversant verticalement.

Voici un exemple d'installation :

<img src="/home/eflay/Images/Installation.png" alt="Installation" style="zoom:150%;" />

Les composants :

- Entrance facilities
- MDF
- Cross-connect facilities
- IDF
- Backbone wiring
- Telecommunications closet
- Horizontal wiring
- Patch Panels
- Work area

##### 5.4.1) Punch Down Blocks

Il y a quatres types : 

- 66 Block : **Used in older analog telephone systems and older CAT3 networks and supports a 25-pair cable that would run to the MDF or IDF.** -> Mauvais choix pour la vitesse
- 110 Block : **Supports high speed data networks for CAT5 and above and includes the use of insulation displacement contract connectors**
- Krone Block : **Proprietary European alternative to 110 Block** -> specific tool
- BIX Block : **Another proprietary punch down block that comes in various sizes** -> specific tool

##### 5.4.2) Patch Panel (Copper)

**Keeps a data center or server room organized by making it easy to move, add or change a cable distribution infrastruture**

Has punch downs (like a 110 block) on the back side that is used to connect wiring to wall jacks in building. Front has RJ-45 jacks

##### 5.4.3) Patch Panel (Fiber)

**Connect fiber jacks throughout building to a single patch panel in network closet**

Front uses patch cables to connect different wall jacks and switch ports.

## 6) Ethernet Fundamentals

#### *6.1) Ethernet Fundamentals*

Dans le passé, il y avait beaucoup de technologie réseau différentes qui était en compétition pour une part de marché :

- Ethernet
- Token Bus
- Token Ring
- Fiber Distributed Data Interface (FDD)
- Others

Ethernet est tellement populaire, qu'on doit être obligé de le comprendre. Les anciens réseaux étaient appelés **10BASE2 et 10BASE5.**

Après, on utilise le **10BASE-T** qui permet une vitesse jusqu'à 10Mbps mais couvre seulement 100m.

Comment les machines vont accéder au réseau ?

- Deterministic : **Very organized and orderly and requires an electronic token to transmit** -> Token Bus, Token Ring
- Contention-based : **Very chaotic and can transmit whenever possible** -> Ethernet

Pour prévenir des colissions :

- Carrier Sense Multiple Access with Collision Detection (CSMA/CD) : **Prevents collisions by using carrier-sensing to defer transmissions until no other stations are transmitting**
  - Carrier Sense : **Listen to the wire, verify if is not busy**
  - Multiple Access : **All devices have access at any time**
  - Collision Detect : If two devices transmit at the same time, a collision occurs -> **Back off, wait a random time and try again**

Exemple :

![CSMACD](/home/eflay/Images/CSMACD.png)

Collision Domains -> **Each are of the network that wshares a single segment**

Devices need to operate in **half-duplex** mode when connected to a hub.

Collision Domains with Switches -> **Increases scalability of a network by creating multiple collision domains**.

Chaque port sur un switch est considéré comme son propre Collision Domain. Les switchs peuvent être en **Full-duplex**.

![Ethernet Rev](/home/eflay/Images/Ethernet review.png)

La bande passante -> **the measure of how many bits the network can transmit in 1-second (bps)**

Pour la fibre :

![Fibre BW](/home/eflay/Images/Fibre BW.png)

#### *6.2) Network Infrastructure Devices*

Les machines réseaux primordiales sont :

- Router (évolution du Bridge)
- Switch (évolution du Hub)

##### 6.2.1) Hub

**Also known as a multiport repeater, it is a Layer 1 device that connects multiple network devices and workstations.**

Il y a 3 différents type de Hub :

- Passive : **Repeats signal with no amplification**
- Active : **Repeats signal with amplification**
- Smart : **Active hub with enhanced features like SNMP**
  ![Hubs](/home/eflay/Images/HUbs.png)

##### 6.2.2) Collision Domains

**Multiple network segments connected together by hubs.**
Les hubs interconnectent les machines se qui crée un seul et unique collision Domain, ce qui est très mauvais pour le réseau.

##### 6.2.3) Bridge

**Analyzes source MAC addresses and makes intelligent forwarding decisions based on the destination MAC in the frames.**
Il permet de séparer les hubs et ainsi crée deux zones de collision Domains et une zone de broadcast Domain.
![Bridge](/home/eflay/Images/Bridge.png)

##### 6.2.4) Switch

**Also known as a multiport bridge, it is a Layer 2 device that connects multiple network segments together.**
Les switchs apprennent les adresses MAC et prennent des décisions de rédirection basées sur elles. Il va analyser les MAC adresses sources et les stockés dans une table.
Chaque port représente une collision Domain. Les ports appartiennent à la même zone de broadcast.
![Switch](/home/eflay/Images/Switch.png)

##### 6.2.5) Router

**Layer 3 device that connects multiple networks and makes forwarding decisions based on logical network information (IPv4 ou IPv6).**
il permet de diviser la zone de broadcast entre les switchs.
![Router](/home/eflay/Images/Router.png)

##### 6.2.6) Layer 3 Switch

**Makes Layer 3 routing decisions and then interconnects entire networks, not just network segments.**
![L3S](/home/eflay/Images/Layer 3 Switch.png)

##### 6.2.7) Résumer

![Résumer](/home/eflay/Images/Résumer.png)

#### *6.3) Ethernet Switch Features*

**Features to enhance network performance, redundancy, security, management,
flexibility, and scalability.**

Les fonctionnalités des switchs :

- Virtual LAN
- Trunking
- Spanning tree protocol
- Link aggregation
- Power over Ethernet
- Port monitoring
- User Authentication

##### 6.3.1) Link aggregation (IEEE 802.3ad)

**Combines multiple physical connections into a single logical connection to minimize or prevent congestion.**
Congestion can occur when ports all operates at the same speed. 
On va combiner les ports du switch pour augmenter la bande passante et donc réduire la congestion.

##### 6.3.2) Power over Ethernet (PoE 802.3af, PoE+ 802.3at)

**Supplies electrical power over ethernet and requires CAT5 or higher copper cable.**
Le PoE -> 15.4 W
Le PoE+ -> 25.5 W

il y a deux types de machines :

- Power Sourcing Equipment (PSE) -> donne l'énergie
- Powered Device (PD) -> recois l'énergie

##### 6.3.3) Port monitoring or mirroring

**Makes a copy of all traffic destined for a port and sends it to another port.**

Permet d'analyser le réseau en connectant un sniffer à un hub ou sur un switch avec le port monitoring0

##### 6.3.4) User Authentication (802.1x)

**Requires users to authenticate themselves before gaining access to the network.**
Une fois authentifié, une clé est générée et partagée entre le pc et le switch (authenticator). Celui-ci vérifie les credentials du pc et crée une clé.

##### 6.3.5) Management Access and Authentication

Il y a deux options pour configurer les switchs :

- SSH -> remotly
- Console Port -> locally
- Out-of-band (OOB) Management : **Keeps all network configuration devices on a separate network**

##### 6.3.6) First-Hop Redundacy

**Uses Hot Standby Router Protocol (HSRP) to create virtual IP and MAC addresses to provide active and standby routers.**
C'est un protocol propriétaire de CISCO (HSRP). Le routeur virtuelle permet d'envoyer le traffic vers lui puis vers le routeur actif.

Il y a d'autres protocol de redondances :

- Gateway Load Balancing Protocol (GLBP)
- Virtul Router Redundancy Protocol (VRRP)
- Common Address Redundancy Protoco (CARP)

##### 6.3.7) MAC Filtering

**Permits or denies traffic based on a device's MAC address.**

##### 6.3.8) Traffic Filtering

**Permits or denies traffic based on IP addresses or application ports.**

##### 6.3.9) Quality of Service (QoS)

**Forwars traffic based on priority markings.**

#### *6.4) Spanning Tree Protocol (802.1d)*

**Permits redundant links between switches and events looping of network traffic.**

Shortest Path Bridging (SPB) -> Used instead of STP for larger network environments.

Sans STP, la table de MAC address peut être corrompue. On va appelé ce phénomène **Broadcast Storm** -> **Multiple copies of frames being forwarded back and forth which then consumes the network.**

Le STP marche en utilisant deux technologies :

- Root bridge : **Switch with the lowest bridge ID (BID)**
- Non-root bridge : **All other switches in a STP topology**

Le BID est fait de la valeur de priorité et de la MAC address.

Il y a plusieurs éléments à connaitre :

- Root port : **Every non-root bridge has a single root port which is the closest to the root bridge in terms of cost.**
- Designated port : **Every network segment has a designated port which is the closest to the root bridge in terms of cost.**
- Non-designated port : **Ports that block traffic to create loop-free topology.**

Le cout est déterminé en fonction de la vitesse des câbles -> + petit = mieux
![cout](/home/eflay/Images/Cost.png)

Tous les ports sur le root bridge sont des Designated ports.

Ensuite, les ports peuvent avoir plusieurs états -> **Non-designated ports do not forward traffic during normal operation, but do receive bridge protocol data units (BPDUs)**
Si un lien est cassé, le non-designated port le détecte et avise s'il doit passé en forward ou pas.
Pour passer à l'état de fowarding, il y a 4 étapes :

- Blocking : **BPDUs are received but not forwarded.**
- Listening : **Populates the MAC address table but does not forward frames.**
- Learning : **Processes BDPUs and this is where switch determines its role in the spanning tree.**
- Forwarding : **Forwards for operations.**

Les non-designated port et les roots port sont blockant.

#### *6.5) Virtual Local Area Network (VLAN)*

Les ports switch sont sur un seul broadcast domain.

**Allows different logical networks to sare the same physical hardware and provides added security and efficiency.**

La VLAN permet de séparer certains ports pour être dans une différente zone de broadcast.
Avant les VLANs s'était les routeurs qui faisaient se travail.
Logiquement, il a y deux cables mais en réalité les VLAN se font que sur un seul cable.

Pour ce faire on va utilisé le protocole :

- VLAN Trunking (802.1q) : **Multiple VLAN transmitted over the same physical cable.**

Comment reconnait-on les VLANs ?

En utilisant un tag electronique qui est de longueur 4-byte (4-byte identifier).
**Il y a le Tag Protocol Identifier (TPI) et le Tag Control Identifier (TCI).**

Quand on n'a pas de vlan -> Native vlan -> VLAN 0

#### *6.6) Specialized Network Devices*

##### 6.6.1) Virtual Private Network (VPN)

**Creates a secure VPN or virtual tunnel over untrusted network like the internet.**

##### 6.6.2) VPN Concentrator

**Terminates VPN tunnels and allows for multiple VPN connections in one location.**

##### 6.6.3) VPN Headend

**A specific type of VPN concentrator used to terminate IPsec VPN tunnels within a router or other device.**

##### 6.6.4) Firewall

**A network security appliance placed at the boundary of a network.**
Ils peuvent être software ou hardware, stateless ou stateful.
Permet au traffic qui vient du réseau à sortir et block le traffic externe.

##### 6.6.5) Next-Generation Firewall (NGFW)

**Conducts deep packet inspection at Layer 7 and can look through traffic to detect and prevent attacks.**
Connecter au cloud pour connaitre les nouvelles menaces.

##### 6.6.6) Intrusion Detection or Prevention System (IDS/IPS)

**Recognizes and responds to attacks through signatures and anomalies.**
IDS = recognizes attacks through signatures and anomalies
IPS = recognizes and responds

Ils peuvent être Host-based ou Network-based.

##### 6.6.7) Proxy Server

**A specialized device that makes requests to an external network on behalf of a client.**

##### 6.6.8) Content Engine/Caching Engine

**Dedicated appliance that performs the caching functions of a proxy server.**

##### 6.6.9) Content Switch/Load Balancer

**Distributes incoming requests across various servers in a server farm.**

#### *6.7) Other devices*

##### 6.7.1) VoIP Phone

**A hardware device that connects to your IP network to make a connection to a call manager within your network.**

##### 6.7.2) Unified Communications (or Call) Manager

**Used to perform the call processing for hardware and software-based IP phones.**

##### 6.7.3) Industrial COntrol System (ICS)

**Describes the different types of control systems and associated instrumentation.**

##### 6.7.4) Supervisory Control and Data Acquisition (SCADA)

**Acquires and transmits data from different systems to a centrl panel for monitoring and control.**

##### 6.7.5) Virtual Network Devices

**Major shift in the way data centers are designed, fielded, and operated.**

## 7) IP Addressing

Internet Protocol (IP) Address : **An assigned numerical label that is used to identify Internet communicating devices on a computer network.**

IP est utilisé à la couche 3 pour la connexion de réseau entre eux et 2 pour les réseaux LAN.

#### *7.1) IPv4 Addressing*

Les adresses sont notées sous le format : 0.0.0.0 (Dotted-Decimal Notation)

Chaque partie est un octet, qui équivaut à 8 bits -> max 32 bits. Les nombres sont écrit en binaires en réalité.

En plus de l'adresse IP, il y a **le masque sous-réseau qui est aussi composé de 32 bits**. Il sert à établir la portion du réseau et de l'hôte dans l'espace d'adresses.
Exemple : 255.255.255 | .0 -> réseau | hôte

Pour les classes d'adresses :

- **1-127 -> A -> Hote possible 16.7 millions**
- **128-191 -> B -> Hote possible 65.536**
- **192-223 -> C -> Hote possible 256**
- **224-239 -> D -> Spécialement réservé au multicasting**
- **240-255 -> E -> Spécialement réservé à des fins de recherches.**

Multicast Address : **A logical identifier for a group of hosts in a computer.**

Si une adresse match avec son masque sous-réseau, on appele ça un "Classful Mask" -> **The default subnet mask for a given class of IP addresses.**

Pour diviser les réseau en plus petit, on va utiliser le "Subnetting" : **Allows for the use of a classless subnet mask to create smaller networks with fewer hosts in each network.**

Mais on peut aussi utilisé le Classless Inter-Domain Routing (CIDR) : **Allows for the borrowing some of those host bits and reassigning them to the network portion.**

La notation CIDR -> 192.168.1.4**/24**

Il y a deux types d'adressage IPv4 :

- Public (Routable) : **Can be accessed over the internet and is assigned to the network by an internet Service provicer. PAYANT**
- Private (Non-routable) : **Can be used by anyone any time, but only within their own LAN.**

Internet Corporation for Assigned Names and Numbers (ICANN) : **Globally manages and leases publicly routable IP addresses.**

Il y a cinq entreprises en dossous de l'ICANN : **ARIN (North America), LACNIC (Latin America), AFNIC (Africa), APNIC (ASia Pacific), RIPE (Europe).**

Pour permettre la transition de l'IP privée à publique pour accéder à internet, on va utiliser :

- Network Address Translation (NAT) : **Allows for routing of private IPs through a public IP.**

L'RFC 1918 : **Used to document how organizations could conduct address allocation for private Internets (Intranets).**

![Private IP](/home/eflay/Images/CIDR.png)

Ensuite il y a les IP spécialisée :

- Loopback (127.0.0.1) : **Creates a loopback to the host and is often used in troubleshooting and testing network protocols on a system.** 
- Automatic Private IP Addresses (APIPA) (169.254.0.0): **Dynamically assigned by OS when DHCP server is unavailable and address not assigned manually.**

L'adresse DHCP s'effectue selon les étapes DORA -> Discover, Offer, Request, Acknowledge.

Dernièrement :

- Virtual IP Address (VIP or VIPA) : **An IP address that does not correlate to an actual physical network interface.**
- Subinterface : **A virtual interface that is created by dividing up one physical interface into multiple logical interfaces.**

Le VIP est utilisé pour : NAT, Fault-tolerance, Virtualization.

#### *7.2) IPv4 Data Flows*

Il y a trois types de flux de données :

- Unicast : **Data travels from a single source device to a single destination device.**
- Multicast : **Data travels from a single source device to multiple (but specific)
  destination devices.**
- Broadcast : **Data travels from a single source device to all devices on a destination
  network.**

#### *7.3) Assigning IP Addresses*

Il y a deux méthodes que l'on peut utiliser :

- Static : **Manually tiping in the IP address for the host, its subnet mask, default gateway, and DNS server.**
- Dynamic : **Quicker, Easier, Less confusing, Simplistic for large network.**

Les composants qui sont remplis :

- IP address
- Subnet Mask
- Gateway
- Server addresses (DNS, WINS)

Il y a 4 méthodes d'assignements dynicamique :

- BOOTP : **Dynamically assigns IP addresses and allows a workstation to load a copy if their boot image over the network. -> static database of IP and MAC.**
- DHCP : **Assigns an IP based on an assignable scope or pool of addresses and provides the ability to configure numerous other options within it.**
- Automatic Private IP Address (APIPA) : **Used when device does not have astatic IP address and cannot reach a DHCP server.**
- Zero Config : **A newer technology based on APIPA which provides a lot of the same features and some new ones. -> Resolving computer names to IP addresses without the need for DNS server on local network. -> Discovery Protocols.**

#### *7.4) Computer Mathematics*

Les humains compte en base-10 : 0,1,2,3,4,5,...

Les ordinateurs ne comprennents pas cette notation -> traduit en binaire -> 0,1,10,11,...

0000 0001 = 1
0000 0010 = 2
0000 0011 = 3
...

#### *7.5) Subnetting*

**Taking a large network and splitting it up into smaller networks.**

10.0.0.0/8 -> Trop grande capacité Host

10.0.1.0/24 -> 256 hotes -> mieux adapter
10.0.2.0/24 -> 256 hotes -> mieux adpater

On va prendre des bits dans la portion hote et les mettre dans la portion network.

Cela permet plus de :

- **Securité**
- **Efficacité**
- **Controle de la bande passante**

Les masques sous réseau de base /8, /16, /24 sont **Classful**.
Les masques sous réseau /26, /27, ... sont **Classless**.

Quelques formules :

- 2² -> **x = number of borrowed bits** -> Subnets
- 2²-2 -> **h = number of host bits** -> Assignable IP addresses

Les sous réseaux ont au minimum besoin de deux adresses -> Network ID (1ere) -> BroadcastID (last).

Variable-Length Subnet Masking (VLSM) : **Allows subnets of various sizes to be used and requires a routing protocol that supports it.** -> Subnetting of subnets -> permet d'avoir des capacités différentes.

Pour mettre en place le VLSM, il faut un protocole de routage comme :

- RIP
- OSPF
- IS-IS
- EIGRP
- BGP

**NE PAS OUBLIER LE -2 ou LE +2.**

#### *7.6) IPv6 Addressing*

Au risque de ne plus avoir assez d'adresses IPv4 -> **Address Exhaustion**
Les adresses IPv6 les remplacent.

En effet, il peut y avoir 2 expoasant 128, soit 340 undecillion addresses.

L'IPv5 était une version expérimentale, certains de ces cooncepts sont repris dans la version IPv6.

Les avantages de l'iPv6 :

- Larger address space
- No braodcasts
- No fragmentation : Performs MTU discovery for each session
- Can coexist with IPv4 -> Dual stack : **Running both the IPv4 and IPv6 protocols by your network devices simultaneously.**
- Simplified header : 5 fields instead of 12

Le tunneling : **Allows an existing IPv4 router to carry IPv6 traffic.** -> Encapsulates IPv6 packets within IPv4 Headers to carry this IPV6 data over IPv4 routers and other infrastrucure.

On écritl l'adresse IPv6 en hexadécimal -> 1 hex = 4 bits -> pas plus que 32 hexadécimal.

Pour faire simple : 

2018:0000:0000:0000:0000:0000:4815:54ae -> 2018:0:0:0:0:0:4815:54ae -> 2018::4815:54ae

ATTENTION -> **MAC ADDRESS 12 digits et 2 par 2.**

Types d'adressage IPv6 :

- Unicast : Used to identify a single interface
  - Globally-routed : **Similar to IPv4's unicast class A,B,C addresses and egins with 2000-3999**
  - Link-local address : **Used like a private IP in IPv4 that can only be used on the local area network and begins with FE80** -> Statless Address Autoconfiguration (SLAAC) : **Eliminates the need to obtain addresses or other configuration information from a central server.**
- Multicast : **Used to identify a group of interfaces so that a packet can be sent to a multicast address and then be delivered to all of the interfaces in the group -> Begins with FF*
- Anycast : **Used to identify a set of interfaces so that a packet can be sent to
  any member of a set**

Il n'a plus necéssairement besoin de DHCP mais le DHCPv6 protocol existe et peut être utilisé.
**L'IPv6 utillise le protocol "Neighbor Discovery Protocol (NDP)" pour apprendre les addresses à la couche 2.**

NDP est utilisé pour :

- Router solicitation : **Hosts send message to locate routers on link**
- Router advertisement : **Router advertise their presence periodically and in response to solicitation**
- Neighbor solicitation : **Used by nodes to determine link layer addresses**
- Neighbor advertisement : **Used by nodes to respond to solicitation messages**
- Redirect : **Routers informing host of better first-hop routers**

Le processus Extended Unique Identifier (EUI64) : **Allows a host to assign itself a unique 64-bit IPv6 inteface identifier called a EUI-64.**  

Pour avoir une EUI adresse, il faut séparer la MAC addresse en 2 et rajoute FF FE entre : 00 21 2f FF FE B5 6E 10.

## 8) Routing

#### *8.1) Routing Fundamentals*
