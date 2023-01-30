## 1) *Préparer votre système à la mise en réseau*
Voici plusieurs étapes au bon déroulement de votre préparation :
- Vérifier les mises à jour du système
- Lui donner un nom approprié
- Configurer votre interface réseau
- Désactiver NETBIOS ainsi que les services par défaut non utiles.
![NETBIOS](https://user.oc-static.com/upload/2018/11/29/1543510797576_image11.png)
- Paramètrer votre pare-feu (notification)
![Pare-feu](https://user.oc-static.com/upload/2018/11/29/15435109624567_image8.png)

Une fois ceci terminé, votre machine sera plus sécurisée et prête à être mise en réseau.

## 2) *Rôles et fonctionnalités*
Tout d'abord quelle est leur différence.
Voici un schéma pour que vous compreniez au mieux :
![Role](https://user.oc-static.com/upload/2019/01/10/15471323228309_p1c3.png)
Voici une liste non exhaustive, pour vous donnez une idée des rôles sous un serveur Windows :
- Accès à distance
- Hyper-V
- DHCP
- DNS
- Serveur Web
- AD DS
- AD RMS
- Stratégier et accès réseau
- ...

Grâce à la zone de démarrage rapide de Windows Server, on peut aller directement sur :
- Ajouter des rôles et des fonctionnalités
- Ajouter d'autres serveurs à gérer
- Regrouper vos serveurs
- Gérer des services Cloud

Les rôles que vous installerez seront disponible directement sur votre tableau de bord.
![Tableau](https://user.oc-static.com/upload/2018/11/29/1543512660479_image11.png)
Pour ajouter des rôles, vous pouvez aussi aller en haut a droite et cliquez sur gérer.

## 3) *La surveillance du serveur*
Microsoft a mis en place **un système similaire à "journalctl" sous Linux.** En effet, tous les évènements sont enregistrés dans différents journaux. De plus, l'affichage est centralisé.
![Event](https://user.oc-static.com/upload/2018/11/29/15435129390496_image3.png)
Vous pouvez choisir quel degré de gravité vous voulez voir.
Avec **le Best Practice Analyzer** vous pouvez vérifier si vous êtes en conformité avec les bonnes pratiques de Microsoft.
![BPA](https://user.oc-static.com/upload/2018/11/29/1543513067547_image9.png)
La performance de votre serveur est aussi primordial, vous pouvez diagnostiquer un problème de ressources sur le serveur avec l'onglet "performance".

## 4) *Installer et configurer le rôle DHCP (Dynamic Host Configuration Protocol)*
Commençons par ajouter le rôle grâce à l'onglet dédié. Cochez juste la case Serveur DHCP et faites suivant.

Après l'installation une alerte va s'afficher en haut à droite, vous pouvez terminer la configuration. Une fois la configuration terminée, vous pouvez vous rendre sur le DHCP et cliquez sur gestionnaire DHCP.

Vous devez arriver sur cette image si tout se passe bien :
![DHCP](https://user.oc-static.com/upload/2018/11/29/1543514323117_image17.png)
Plusieurs paramètre s'offre à vous :
- Options de serveur
- Stratégies (Condition)
- Filtres (Exclusion ou Autorisation)

En sélectionnant IPv4 et clic droit vous pourrez ajouté une étendue d'adresses à distribuer. 
**L'étendue est une plage d'adresses IP assignées aux ordianteurs demandant une adresse IP dynamique.**

A travers l'assistant, vous pourrez remplir les différents champ comme l'adresse de début et de fin de votre pool ainsi que son masque.
![Pool](https://user.oc-static.com/upload/2018/11/29/15435146786577_image8.png)
Il vous propose aussi d'entrer des exlusions ou de retarder les réponses du serveur.

**Voilà la configuration DHCP est terminée**. Pour aller plus en profondeur, vous pouvez clique droit sur le nom de votre étendue et allez dans Propriétés.

**L’onglet DNS** permet de gérer la mise à jour des enregistrements DNS à chaque fourniture de configuration.
**L’onglet Avancé** permet de choisir si seul le protocole DHCP sera utilisé, ou si le protocole BOOTP sera utilisé (ou les deux)

Une dernière étape est importante pour que votre DHCP fonctionne correctement, c'est d'autoriser les flux au niveau de votre pare-feu. Pour ce faire RDV, dans l'onglet **"Pare-feu Windows avec fonctions avancées de sécurité"** et crée une nouvelle règle entrante sur les port 67, 68 en UDP.

Vous pouvez diagnostiquer votre DHCP à **l'aide de l'observateur d'évènements.** De plus, avec l'ajout d'un nouveau serveur, vous pouvez assurer **une redondance** avec un 2e serveur DHCP.
![redondance](https://user.oc-static.com/upload/2018/11/29/154351481552_image9.png)

## 5) *Installer et configurer le rôle DNS (Domain Name Service)*
**Le DNS permet d'associer un nom qualifié à une adresse IP.**
Voici un schéma de fonctionnement du DNS :
![DNS](https://user.oc-static.com/upload/2018/11/29/15435156145791_image19.png)
On va d'abord commencer par chercher un serveur qui connait le .org ensuite le wikipedia.org et enfin le fr.wikipedia.org et renvoyer l'adresse IP. L'dresse est ensuite mis en cache pour ne plus devoir faire cette manipulation et ainsi gagner du temps. Pour afficher les informations concernant le cache, vous pouvez taper la commande suivante :
```ps
get-dnsservercache
```

Pour installer ce rôle, il vous suffit de faire la même manipulation que pour le DHCP.
![installer](https://user.oc-static.com/upload/2018/11/29/15435165937677_image15.png)
Ensuite comme le DHCP, vous vous rendez dans le gestionnaire DNS.
![gest](https://user.oc-static.com/upload/2018/11/29/15435166715065_image17.png)

### 5.1) Zone Directe
Maintenant mettons en place la première zone directe.
**Une zone directe permet d’associer un nom à une adresse IP**. Cliquez droit sur le nom de votre serveur et crée un serveur DNS. Pretez bien attention à **"la msie à niveau dynamique"** qu'elle soit bien sur **"ne pas autoriser"** sinon un utilisateur pourrait modifier vos enregistrements.
![att](https://user.oc-static.com/upload/2018/11/29/15435172788329_image24.png)

Ensuite vous pouvez configurer vos redirecteurs, il s'agit des serveurs DNS qui interrogeront les serveurs racines.
![rac](https://user.oc-static.com/upload/2018/11/29/1543517298033_image8.png)

Nous allons crée les enregistrement A qui feront le lien entre l'adresse IP et le nom de domaine. Pour ce faire clic droit dans la fenêtre de votre zone directe.
![A](https://user.oc-static.com/upload/2018/11/29/15435173503862_image10.png)

### 5.2) Zone inversée
**C’est une association d’une adresse IP à un nom, l'inverse d'une zone directe.**
Le principe de configuration reste le même sauf que vous devrez spécifier l'adresse IP à la place du nom.
![reverse](https://user.oc-static.com/upload/2018/11/29/15435209950688_image3.png)
Une fois la configuration faites, vous pouvez ajouter un nouveau pointeur PTR, avec le même procédé que l'enregistrement A. Vous devez être capable maintenant grâce à un ping de l'adresse IP de renvoyer le nom de domaine.

## 6) *Installer et configurer un serveur de fichier*
Pour qu'un fichier soit accesible depuis votre réseau, un protocole doit être utilisé. **Le protocol SMB** (Server Message Block) se caractérise par **un client natif intégré à Microsoft** et à un serveur.

Il se base sur **NTFS (New Technology File System) pour la gestion des droits d'accès et les partages sont accessible via un chemin universel.**

Pas besoin d'installer ce rôle car il est disponible de base. Pour le test, nous allons ajouté deux disques durs de 10GB. Lorsque ceci est fait RDV dans votre onglet "Services de fichiers et de stockage". Vous y voyez vos deux disques ajoutés.

Voici les différentes étapes :
1. Initialiser vos disques en faisant un clique droit.
2. Créer un pool de stockage avec les deux disques
![pool](https://user.oc-static.com/upload/2018/11/29/15435216995175_image5.png)
3. Créer votre disque virtuel après la création de votre pool de stockage et spécifier le mode mirror pour la redondance
![dv](https://user.oc-static.com/upload/2018/11/29/15435217121906_image3.png)
4. Suivez l'assitant qui créera un nouveau disque et le formatera pour vous.
5. Allez voir dans vos dossier s'il s'est crée
![test](https://user.oc-static.com/upload/2018/11/29/15435217760474_image7.png)

### 6.1) Créer votre partage
RDV dans la partie Volumes, puis dans l'encart "Ressources partagées" et cliquez sur :
![1](https://user.oc-static.com/upload/2018/11/29/15435218822747_image13.png)
"Démarrer l'assistant ajout ..." puis poursuivez l'installation.

Ensuite créer un nouveau partage grâce à l'onglet tâche.
![2](https://user.oc-static.com/upload/2018/11/29/1543521910625_image20.png)
Vous aurez le choix entre 5 propositions :
- **SMB simple** : le plus simple, vous fournissez un partage sur votre réseau via SMB
- **SMB avancé** : permet d’aller plus loin que le précédent en gérant des quotas et des droits avancés
- **SMB Applications** : utilisé pour Hyper-V et les bases de données ou autres serveurs
- **NFS simple** : identique à SMB simple mais via NFS (avec donc une meilleure compatibilité avec Linux)
- **NFS avancé** : idem SMB avancé

Ici nous allons resté sur SMB simple. Poursuivez la configuration en spécifiant votre disque précédemment crée. Vous aurez la possibilité de chiffrer l'accès aux données et une configuration des droits d'utilisateurs.
![3](https://user.oc-static.com/upload/2018/11/29/15435220820328_image18.png)
Et voila votre partage est crée.

## 7) *Installer un serveur d'accès au réseau*
Comme d'habitude, vous installez ce rôle avec l'assistant d'ajout pour **le rôle "Services de stratégie et d'accès réseau".** Grâce à NPS (Network policy Server), le contrôle d'accès au réseau est assuré. 

Il agit comme **un serveur RADIUS (Remote Authentication Dial-in User Service)** qui est un protocole permettant de **vérifier l'identité d'un client, ses droits et de lui fournir un service.**

Par après, vous faites un clique droit sur votre nom de serveur et "Serveur NPS", vous obtiendrez ceci :
![4](https://user.oc-static.com/upload/2018/11/29/15435223510969_image14.png)
L'onglet stratégie permet de spécifier quels types de supplicants (utilisateur) peuvent faire des demandes légitimes.
## 8) *Montez un cluster à basculement*
**C'est une fonctionnalité qui permet la mise en oeuvre de différents rôles sur plusieurs serveurs.** Elle permet de **garantir la disponibilité d'un rôle** durant une maintenance.

Quelques nouvelles fonctionnalités depuis Windows Server 2016 :
- Les mises à jour sont automatisées
- Possiblité d'avoir un témoin de cluster dans le cloud
- Le multicanal SMB

Voici quelques pré-requis :
- Avoir minimum 2 serveurs prêt
- La même version de Windows Server sur tous vos noeuds
- Vérifier la compatibilité matérielle
- Accès au stockage
- Joint au même AD
- Compte Admin sur chaque serveur


### 8.1) Installez la fonctionnalité
On commence par ajouter le rôle **de stockage iSCSI**, pour devenir le schéma suivant :
![cluster](https://user.oc-static.com/upload/2018/12/04/15439387591158_image7.png)
Ensuite, il ne vous reste plus qu'à créer un nouveau volume iSCSI sur **un serveur dédié à cette tâche.**
![creer](https://user.oc-static.com/upload/2018/12/04/1543938827616_image11.png)
Avec l'assistant, il faudra spécifier l'emplacement du volume partagé,  définir les serveur qui auront accès au partage (initiateur).

Une fois ceci fait, ajoutez **la fonctionnalité** Clustering avec basculement. Quand il est installé, RDV dans l'outil Gestionnaire du CLuster à basculement.
![gest](https://user.oc-static.com/upload/2018/12/04/15439389410768_image15.png)

Toutes les actions se feront à partir de cette console. On va **"Validez la configuration"** pour vérifier si vos hotes valident les conditions de Microsoft.
![val](https://user.oc-static.com/upload/2018/12/04/15439389730355_image3.png)
Attention, il est nécessaire de réactiver certaines fonctionnalités réseaux comme :
- Client pour les réseaux Microsoft
- Ipv6
- Découverte LLDP
- Découverte Topologie

Vous disposez maintenant de deux noeuds valides. Il ne vous reste plus qu'à **créer un cluster** grâce à la zone "Actions" du gestionnaire. Suivez le guide d'installation et terminez la configuration.
![f](https://user.oc-static.com/upload/2018/12/04/15439390344062_image1.png)
![g](https://user.oc-static.com/upload/2018/12/04/15439390550885_image2.png)

On va pouvoir ajouter des rôles Windows dans notre cluster et ainsi avoir une haute disponibilité.
![j](https://user.oc-static.com/upload/2018/12/04/15439390796488_image12.png)

Il ne vous reste plus qu'à installer le rôle choisi sur vos deux autres serveurs et de les spécifier en tant qu'initiateur iSCSI grâce à l'outil adéquat dans le menu démarrer. Vous allez voir dans l'onglet gestion de l'ordinateur, la gestion des disques pour ainsi les activer,les initialiser et créer un volume simple.

## 9) *Implémentez un service de déploiement*
**Ce rôle permet de démarrer un poste client par le réseau, et de lui envoyer un OS personnalisé.**
Une fois ajouté, vous pouvez configurer le rôle.
![t](https://user.oc-static.com/upload/2018/11/30/15435688810229_image1.png)
Cependant, il y a certains pré-requis :
![tk](https://user.oc-static.com/upload/2018/11/30/15435688937838_image4.png)
Suivez l'assistant, en sélectionnant ce qui vous convient.

Le rôle est configurer, il ne reste plus qu'à intégrer des images d'installation et de démarrage.
![y](https://user.oc-static.com/upload/2018/11/30/15435689570209_image6.png)
![g](https://user.oc-static.com/upload/2018/11/30/15435689682739_image2.png)

Il y a 2 autres types d'image :
- Image de capture (capturer le sysème pour le répliquer)
- Image de découverte (client n'utilisant pas pleienement pXe)

**Pour configurer un client, il faut démarrer le poste en mode WDS, càd en sélectionnant l'interface réseau dans votre gestionnaire BIOS.**

## 10) *Partagez un bureau avec vos utilisateurs*

### 10.1) Activer le service

Rendez-vous sur les paramètre de bureau à distance avec la barre de recherche et activer le service. Pour vous connecter, utiliser le raccourcis Bureau à distance et connectez-vous avec un compte valide.

### 10.2) Personnalisez le bureau à distance

Il convient de personnaliser le bureau d'un utilisateur en réduisant la présence de certains raccourcis, notamment dans le menu démarrer, qui se trouve dans l'emplacement suivant :

```powershell
C:\Users\<nom-d-utilisateur>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs
```

Ou par défaut :

```powershell
C:\Users\Default\AppData\Roaming\Microsoft\Windows\Start Menu\Programs
```

De plus l'Active Directory et les Group Policy Object (GPO) vous seront d'une grande aide.

### 10.3) Gérez une ferme de serveurs bureaux à distance

Grâce à ce type d'infrastructure, vous pourrez :

- Avoir une gestion avancée des sessions
- Avoir la possiblité de déployer un bureau
- L'ajout des serveurs sera simplifié

Il existe 3 options :

- Plusieurs serveurs (chacun ayant un rôle spécifique dans le système VDI)
- Unique serveur (regroupant tous les rôles VDI)
- Services Multipoint (qui permettent de créer des stations pour des utilisateurs et de leur donner accès avec des concentrateurs USB)

### 10.4) Les services Multipoint

**C'est la façon la plus simple pour configurer un serveur qui sera utilisé par plusieurs claviers, écran et souris.**

Chaque utilisateur doit disposer de son clavier, souris, écran et de sa propre session. Ce qui permet de considérablement réduire les frais.

Cependant il y a certains désavantages :

- Nombre limité de sessions possible
- Une administration a gérer

Cette solution convient parfaitement pour les environnements scolaires par exemple.

### 10.5) Mettre en place un serveur unique regroupant tous les VDI

Il y a 2 scénarios pour l'option de déploiement :

- Utiliser des ordinateurs virtuels
- Utiliser des sessions sur le serveur actuel

Pour ajouter ce service, il ne faut pas faire une installation d'un rôle mais d'un service de Bureau à distance dans le 2e onglet. 

Une fois configurer, vous devez redémarré votre ordinateur. Voici les rôles qui seront installés avec cet outil :

- Service Broker pour les connexions Bureau à distance (diriger les utilisateurs)
- Accès Web des services Bureau à distance (interface web)
- Hôte de session Bureau à distance (serveur hébergeur)

## 11) *Distribuer des mises à jour avec Windows Server Update Services (WSUS)*

**C'est l'équivalent du service Windows Update à destination des Administrateurs.**

Il permet de télécharger les mises à jour de votre parc une seule fois via le serveur WSUS. C'est la solution idéale pour éviter des problèmes avec les utilisateurs.

Pour installer le rôle, faites comme d'habitude et ensuite cliquez droit sur votre serveur et allez dans Service WSUS.

![wsus](https://user.oc-static.com/upload/2018/11/30/15435677270812_image9.png)

Pour ajouter un client deux option s'offre à vous :

- Utiliser des GPO (avec AD)
- Utiliser la base de registre (sans AD)

Pour ajouter un client avec des GPO, il faut aller dans **"Outils>Utilisateur et Ordinateur>Ordinateur>Stratégies>Modèle d'administration>Composant Windows>Windows Update"** et configurez le comme vous le souhaitez.

Vous pouvez aussi approuvés ou désapprouvés les mises à jour s'il ne vous convienne pas.

## 12) *Administrez votre serveur avec Powershell*

Pour ce faire nous allons utilisé **l'ISE Powershell**

**Integrated Script Environment (ISE) est un environnement dédié qui permet de simplifier l'écriture de scripts.**

Les premières commandes utiles sont celles de l'ajout de rôles ou de fonctionnalité.

![test](https://user.oc-static.com/upload/2018/11/30/15435650474112_image1.png)

Vous remarquez qu'on importe le module server manager car celui-ci regroupe de nombreuses commandes liées à l'administration. Ensuite nous ajoutons la fonctionnalité Telnet.

Une commande pratique est :

```powershell
Get-WindowsFeature
```

Elle permet de lister les fonctionnalités du serveur.

Une des forces de Powershell est sa communauté. Vous trouverez de nombreux scripts tout prêts ce qui vous permettra d'économiser du temps et ainsi améliorer d'autre point de votre infrastructure comme la sécurité. Pour vous permettre de rechercher des modules en ligne vous devez installer le module **NuGet.** 

Vous pouvez faire la commande suivante pour rechercher un type de module particulier, ici avec l'AD :

```powershell
find-module -name *AD*
```

**Les Desired State Configuration (DSC) est l'ensemble des scripts permettant de configurer un serveur.** De plus cette fonctionnalité DSC permet de compiler les scripts en fichier Managed Object Format (MOF) afin qu'ils puissent être utilisés en mode PUSH ou PULL sur un serveur.

**Le mode PUSH**, la configuration désirée sera poussée sur le serveur. L'objectif de cette fonctionnalité est de s'assurer que votre serveur est correctement configurer.

**Le mode PULL**, c'est votre serveur qui ira chercher la bonne configuration à appliquer.

## 13) *Virtualisez vos serveurs avec Hyper-V*

### 13.1) Distinguez les différentes version d'Hyper-V

Si vous possédez une licence Windows Server Standard, vous aurez accès qu'à deux VM, si vous prenez l'édition Datacenter, vous aurez alors un nombre de VM illimité.

### 13.2) Prendre en main Hyper-V

Lors de l'installation de ce rôle sur votre Windows Server, vous pouvez rencontré le problème suivant :

![err](https://user.oc-static.com/upload/2018/11/30/15435659443582_image3.png)

Trois option s'offrent à vous :

- Changer d'hyperviseur, Vitualbox ne permet pas la virtualisation au sein d'une machine virtuelle tandis que VMware oui.
- Basculer sur un OS 32bits, virtualbox le permet en 32bits
- basculer sur une machine physique Windows Server

Une fois installé, vous allez vers le panneau de configuration :

![v](https://user.oc-static.com/upload/2018/11/30/15435661728_image5.png)

Votre ordinateur est maintenant devenu **une zone d'hébergement** avec une gestion réseau complète, une gestion du stockage et des ressources CPU, RAM.

Hyper-V dispose de fonctions permettant de virtualiser la carte réseau. Il va donc créer un switch virtuel connecté à votre carte réseau physique. Il va fournir un certain nombre de ports réseau disponible pour les VM.

![t](https://user.oc-static.com/upload/2018/11/30/15435660252476_image2.png)

Vous pouvez aussi configurer votre switch en cliquant sur  “**Gestionnaire de commutateur virtuel…**” dans le menu Actions.

![y](https://user.oc-static.com/upload/2018/11/30/15435660490198_image4.png)

Il existe 3 modes de fonctionnement réseau :

- Réseau externe,  qui permet de donner accès à une interface réseau physique
- Réseau interne, qui crée un switch sans connexion avec le réseau physique juste votre serveur hôte et lui
- Réseau privé, les VM n'auront accès ni à l'hôte ni au réseau externe

### 13.3) Créez votre première machine virtuelle Hyper-V

Grâce au menu action, ajoutez une machine virtuelle. Les étapes a suivre sont :

1. Nom
2. Espace de stockage
3. Génération
4. RAM
5. Connexion réseau
6. Configuration disque virtuel
7. OS
8. Affection processeur

Quelques précautions sont à prendre avec l'espace de stockage :

- Spécifiez un espace suffisamment conséquent et rapide
- Les disques durs du commerce ne sont pas fait pour ce type d'utilisation
- Les SSD sont bien mais leur durée de vie serait fortement réduite

Une fois configurer vous pouvez la démarrer et vous y connecter.

## 14) *Le service IIS pour héberger vos applications Web*

Une fois le rôle Serveur Web (IIS) installé, voici votre panneau de configuration.

![iis](https://user.oc-static.com/upload/2018/11/30/15435673710417_image3.png)

Vous pouvez à présent créer des fichiers PHP, REACT, ... et les mettre dans la racine de votre serveur web càd **"C:\inetpub\wwwroot"**

Cependant le PHP n'est pas interprêté de base par le rôle, 2 méthodes s'offrent à vous :

- Méthode automatique avec Web Plaform Installer
- Méthode manuelle

Les étapes pour la méthode manuelle sont :

1. Récupérer le binaire PHP
2. configurer php.ini
3. Associer php à un module CGI

Pour la méthode automatique, grâce au menu Actions. Vous pouvez sélectionné "Obtenir de nouveaux composants Web Platform". Une fois l'extension Web Platform Installer installé, faites une recherche de php dans l'outil et ajoutez PHP.

![php](https://user.oc-static.com/upload/2018/11/30/15435674131029_image1.png)

