## 1) *Architecte des systèmes*

La vision du métier d'architecte des systèmes se base sur **la méthode et une vision** :

- La méthode permet d'analyser un système selon tous ses axes et surtout de poser les bonnes questions
- La vision est le fruit d'une réflexion en commun entre les experts des différents composants et l'architecte

**Le rôle de l'architecte est aussi de faire le pont entre un besoin fantasmé et la dure réalité des productions informatiques.**

Plus un architecte est expérimenté, plus il est à même d'appliquer la méthode de façon pertinente. De plus, il sera travaillé avec les experts efficacement. Pour booster son expérience métier, avoir un architecte senior est une très bonne méthode.

**Ce métier peut être fait toute sa vie car on peut progresser et évoluer en tant qu'architecte sur l'ensemble de sa carrière.**

Les qualités attendues sont d'être compétent dans **une diversité de domaines et être excellent communicant.**

## 2) *Caractéristiques d'une bonne architecture*

### 2.1) La sécurité

L'une des questions principale à se poser est : **Comment sécuriser mon application, mon infrastructure ?**

On va se baser sur le modèle DICT pour **Disponibilité, Intégrité, Confidentialité, Traçabilité.** On peut aussi y ajouter la PDMA pour **Perte de données maximum Admissible**.

### 2.2) L'élasticité

**C'est la capacité d'un système à répondre à des contraintes changeantes.**

On distingue deux types d'élasticité :

- Verticale -> Ajout de ressources supplémentaires
- Horizontale -> ajout de nouveaux éléments

### 2.3) Le couplage lâche

**Le couplage est la nature de l'adhérence qu'ont deux systèmes entre eux.** Une architecture moderne doit permettre **une adhérence faible avec ses interfaces externes et internes.**

### 2.4) La simplicité

**Un système simple sera par essence compréhensible donc opérable, extensible et stable dans la durée**

## 3) *Dessinez votre architecture*

**La documentation est essentielle à la communication et à la pérennité d'un système.** 

Pour décrire une architecture, un bon réflex est de vous appuyez sur ce qui a déjà été fait. On pourra par la suite définir **un référentiel commun** et l'utiliser.

Le mieux est de démarrer sur papier, vous ne serez pas gêné par la contrainte des outils. Une fois la phase papier finie et claire, on peut passer à la phase logicielle pour la rendre jolie et évolutive.

Pour savoir comment représenter l'architecture de votre système, vous pouvez la découper en **sous-ensembles cohérents et complémentaires.** Par défaut un SI, vu sous l'angle technique, dispose de 4 plans :

- Fonctionnel -> Que fait l'application et la nature des données (aspect métier)
- Applicatif -> Les flux, stocks, middlewares, framework (aspect logiciel)
- Infrastructure -> Décrire les choix techniques, serveurs, dimensionnement, interconnexion, ...
- Opérationnelle -> Gestion du système, mécanisme de sauvegarde, supervision, ...

## 4) *La couche Fonctionnelle*

Cette couche traite de **tout ce que fait l'application**, càd **les données manipulées et comment elle s'inscrit dans son écosystème applicatif.**

**Plus on évite l'analyse fonctionnelle, plus le système défini risque d'être inadapté au besoins réels des utilisateurs.** C'est donc la responsabilité de l'architecte de prendre du recul.

Il y a 4 axes principaux qui permettent de détailler l'aspect métier :

- Les utilisateurs
- Les données
- Les traitements
- Les interfaces

Afin d'identifier ces informations, vous allez devoir **identifier un représentant des métiers** ou interagir directement avec eux.

### 4.1) Les utilisateurs

Nous allons **identifier qui va utiliser le système** que l'on est en train de définir :

- Des employés de l’entreprise ?
- Des partenaires ?
- Des clients depuis internet ?
-  Où sont-ils situés ?

**La volumétrie** est importante également pour avoir une idée du nombre de personnels qui seront actifs en même temps :

- Combien vont-ils être au total ?
- En même temps ?
- Y a-t-il des populations « clés » devant être prise en compte en particulier ?
- Qui va faire de la consultation uniquement ?

### 4.2) Les données

Plusieurs questions à définir :

- D’où viennent-elles ? 
- Quelle est leur **sensibilité** (confidentialité) ? 
- Sur quels référentiels s’appuient-elles ? 
- Quel est leur **cycle de vie** : qui les produit, qui les transforme, qui les consomme ? 
- Quel est leur **format** ?
-  Quel est leur niveau de **qualité** ?

Ces informations vont vous permettre **d'affiner la composante sécurité de l'expression de besoin** autour du DICT.

### 4.3) Les traitements

Il va falloir lister les grands blocs fonctionnels par type d'usage : gestion d’inventaire, authentification des utilisateurs, production de rapports...

On va y associer des notions de performances : telle fonction doit répondre en moins de 3 secondes, tel rapport doit être produit chaque nuit, ...

Cependant, **personne n'est capable de fournir ces indications de manière explicite**. Il faudra revenir à cette étape une fois le système déployer.

### 4.4) Les interfaces

Les échanges entre les systèmes doivent être caractérisés par 2 éléments :

- La donnée portée
- Le sens de transfert

On parle ici des applications sources et cibles. Comprendre les flux vous permet de vous interroger sur le fonctionnement global du système. On pourra aussi identifier les problématiques structurelles et anticiper les problématiques techniques.

**Une bonne façon de bien identifier les interfaces et de vous demander  qui est le producteur de la donnée et qui sont ses consommateurs.**

## 5) *La couche Applicative*

Dans cette partie, nous allons faire apparaitre les différentes **contraintes de sécurité, de version, de volume, ...**

Lors des choix à effectuer, il faut prendre en compte la partie exploitation :

- Qui va être en charge du composant ?
- Est-ce que les équipes cibles sont en capacité d’assurer les plages de services requises (notamment en 24/7) ?
- Comment obtenir l’expertise en cas de besoin ?

On va essayer de comprendre comment les différents éléments capturés dans l'analyse fonctionnelle vont s'instancier :

- A quel(s) flux technique(s) correspond un flux métier ?
- Dans quelle base sera stockée la donnée ?
- Quel serveur d’application porte le traitement identifié ?

### 5.1) Identifier les flux

C'est la problématique la plus importante en architecture, grâce à l'émergence du Cloud.

Voici les aspects techniques :

- Le **protocole réseau—**UDP, TCP, SMB, le port utilisé…
- Le sens de **l’initialisation** du flux
- La **volumétrie** transmise, globale et unitaire
- La **fréquence** des envois
- Le **temps** qui vous est imposé entre la réception du flux et la restitution du résultat
- Les **zones réseau** traversées

**Le sens d'initialisation** permet de comprendre quels pare-feux ouvrir, et si l'architecture décrite respecte les contraintes de sécurité de l'entreprise.

### 5.2) Les zones de sécurité

Pour identifier les différentes zones de sécurité, nous avons 2 méthodes :

- S'appuyer sur une expertise externe
- Utiliser son expérience

Il ne faut pas se précipiter et agir avec méthodologie. **La méthode, c'est tout le temps.**

### 5.3) Les gisements de données

On va s'appuyer sur l'analyse faite au niveau fonctionnel et décrire l'aspect gisement :

- **Quelles sont les données** à garder—Faut-il en filtrer une partie ?
- Dans quel **format** ?—Fichier ? Base de données SQL ? NoSQL ?
- Pendant **combien de temps** ?—et quelle sera la politique de purge ?
- **Qui** devra y accéder et **comment** ?

### 5.4) Les middlewares

**L'ensemble des flux, données et des traitements est appelé Middleware.**

- Des logiciels permettant les **échanges** (MoM, EAI, Bus…), comme RabbitMQ, sftpd, WebMethods...
- Des **bases de données** (Oracle, SQL Server, MySQL, MariaDB, MongoDB, Cassandra, Azure SQL DB, DynamoDB, ...)
- Des **serveurs d’application** (MS IIS, Apache Tomcat, JBoss, …)
- Des **serveurs web** (Apache httpd, Nginx…)
- Des **services de sécurité réseau** type WAF, Firewall niveau 4, Load-balancer, proxy, reverse-proxy, VPN…
- Des **services d’authentification** ou de **SSO** (MS AD, Openstack Keystone)
- ...

**On va identifier et comprendre l'organisation de toutes les briques composant votre architecture. Cela va faciliter la vie des personnes qui vont déployer et opérer la solution au quotidien.**

## 6) *La couche infrastructure*

**Cette couche traite l'ensemble des mécanismes sous-jacent qui proposent des ressources et garantissent la performance, la disponibilité et la protection des données.**

Il faut distinguer 2 types d'infrastructure :

- Les infras mutualisées
- Les infras dédiées

La plus répandue étant l'infrastructure mutualisées.

### 6.1) Le calcul

On va décrire 3 éléments :

- Le dimensionnement -> Niveau de performance
- L'emplacement -> Localisation
- L'identifiant -> Lien avec la couche applicative

Le dimensionnement automatique est encore rare et ne couvre pas tous les usages.

### 6.2) Le réseau

Il faut analyser divers points :

- Comment mes composants sont-ils **interconnectés** ?
- Comment mes clients **communiquent-ils** avec les composants (que ce soit de façon physique ou virtuelle) ?
- Quel **débit** (1G, 10G ?), quelle latence ?
- Quel **type de lien** (RJ45, SFP, vAdapter ?) ?
- Quelle **redondance** (LACP, interfaces multiples…) ?

Selon **la complexité**, on analysera uniquement les interfaces directement utilisées, ou globalement l'ensemble des réseaux traversés.

### 6.3) Le stockage

Encore une fois, il faut se poser plusieurs questions :

- Comment **j’accède à mon stockage** (SAN ? NAS ? FC ? IP ? attachement direct ? Local ?)
- Quelle **forme** de stockage (bloc, fichier, objet) ?
- Quel **type de disque** utilisé (SSD vs HDD, Full Flash vs Hybride) ?
- Plus généralement les **performances** délivrées (latence, débit, nombre d’E/S...) ?

La localisation du stockage va également être un enjeu important afin de pouvoir évaluer les risques de sinistre dans une approche Plan de Reprise D'activité (PRA).

La **couche infrastructure** est aussi l’occasion  d’analyser et de détailler les différentes machines physiques ou  virtuelles dédiées à des usages spécifiques.

## 7) *La couche opérationnelle*

### 7.1) La supervision

La **supervision** permet de vous assurer que votre système est pleinement **opérationnel** et peut répondre à ses **contraintes** de services. Nous allons identifier les points de supervision sur lesquels on va déclencher des alertes en cas de déviation.

La finalité de la supervision est de résoudre le plus rapidement les incidents et les éviter. On va donc s'assurer de plusieurs points comme : 

- La perte de réseau
- Réponse d'un service web
- Présence utilisateurs
- ...

Il faut également décrire à quels systèmes de supervision, le système est raccordé.

### 7.2) La métrologie

La **métrologie** permet de suivre et d’analyser un système à travers la **collecte** et **l’exploitation** des **métriques.**

L'architecte doit mettre en places les caractéristiques des métriques. **Leur nature, la fréquence de collecte et la durée de rétention.**

### 7.3) La sauvegarde

C’est à l’architecte de s’assurer comment la sauvegarde sera réalisée et surtout si elle permet de **respecter la politique de sauvegarde** associée, et surtout de garantir les **délais de restauration**. Cette **politique de sauvegarde** décrit la fréquence et la rétention des sauvegardes réalisées.

**Seuls des tests de restauration réguliers peuvent réellement garantir que vos données sont bel et bien protégées**.

### 7.4) L'ordonnancement

**L’ordonnancement** est la gestion de l'exécution de **traitements successifs**, en intégrant des possibilités de **reprise** et **d’embranchement** selon les résultats de chacun des traitements.

Il est important de connaitre **la dépendance du système avec un mécanisme d'ordonnancement.** Celui-ci peut impacter la capacité à tenir les engagements. Il faut avoir **une vision transverse** : pouvoir prendre une décision technique à partir de la compréhension des enjeux métiers.

## 8) *Le document d'architecture technique (DAT)*

Avant de vous lancer dans la rédaction du document, il faut vous poser plusieurs questions :

- A qui le document est **destiné**—D’autres architectes ? Les chefs de projets ? Les administrateurs ? Le département sécurité ?
- Quel est le **message** à porter—Mettre en avant les contraintes d’exploitation ? Les  engagements de service vis à vis du métier ? Les flux et les  problématiques de filtrage ?

Les objectifs du DAT sont aux nombre de 5 :

- **Porter la vision** de l’architecture cible, c’est à dire décrire explicitement la synthèse de ce que chacune des parties prenantes a en tête, à travers des schémas reprenant les 4 couches.
- **Documenter les engagements** de service : DIMA, PDMA et les autres aspects présentés dans la première partie.
- **Présenter comment l’architecture cible y répond**, en détaillant les mécanismes de disponibilité, de performance, de résilience, de chiffrement, de sauvegarde…
- **Décrire le travail à réaliser** de façon macro et servir de référence pour le chef de projet.
- **Servir de support de communication** afin de présenter efficacement le projet au management, aux autres  architectes et aux équipes en charge de la réalisation.

## 9) *Plan type d'un DAT*

### 9.1) Le contexte, les besoins fonctionnels

Cette partie correspond à l'analyse fonctionnelle :

- Que fait le système décrit ?
- Quel a été l’historique du projet ?
- Quelles sont les attentes principales (nouveau marché pour le métier ? réduction des coûts ?...) ?
- Qui sont les principaux acteurs ?
- Quelles directions sponsorisent le projet ?
- Quelles sont les contraintes métiers qui auront un impact sur l’architecture ?

### 9.2) Les besoins non fonctionnels

On va lister les contraintes techniques, il faut être exhaustif et partager ces besoins pour faire toute la valeur de l'architecture proposée.

### 9.3) La représentation fonctionnelle

L'approche classique est de **suivre le parcours de l'utilisateur et son cheminement dans le système.**

Voici un exemple où l'on fait apparaître le sens de la donnée et non le sens du flux :

![g](https://user.oc-static.com/upload/2018/10/12/15393575713677_couche%20fonctionnelle.png)

Ensuite on va lister l'ensemble des environnements et en donnant quelques caractéristiques :

![f](https://user.oc-static.com/upload/2018/10/12/15393580856992_env.png)

### 9.4) La représentation applicative

Il faut faire apparaitre chacune des briques applicatives, flux techniques, port, protocole et le sens de l'initialisation. La localisation est aussi primordial :

![t](https://user.oc-static.com/upload/2018/10/12/15393576059008_couche%20applicative.png)

**La matrice de flux va permettre de faciliter le travail des équipes sécurité et des chefs de projet.**

![y](https://user.oc-static.com/upload/2018/10/11/15392737140394_flow%20matrix.png)

### 9.5) La représentation infrastructure

Elle permet de visualiser directement les ressources utilisées. Il faut faire apparaitre les configurations matérielles et les caractéristiques de disponibilité et de résilience :

![u](https://user.oc-static.com/upload/2018/10/12/15393576334969_couche%20techine.png)

### 9.6) La représentation opérationnelle

Mettre en avant les différents service d'exploitation :

![i](https://user.oc-static.com/upload/2018/10/12/15393576726172_couche%20operation.png)

De plus, les offres de services d'opérations sont pertinentes à préciser.

### 9.7) Les décisions d'architecture

Chacune des décision doit être expliquée afin de pouvoir être examinée avec son contexte à l'avenir. 

Une structure comme suit peut être bien :

- L’intitulé de la décision
- Son contexte (pourquoi il y a une décision à prendre)
- Les alternatives considérées
- La justification pour expliquer la décision et/ou le choix

![o](https://user.oc-static.com/upload/2018/10/12/15393578992789_decisions%20d%27arch.png)

### 9.8) Plan projet

Ce plan va permettre de lister chacune des **tâches** à réaliser et surtout quelle **équipe** en aura la charge.

![p](https://user.oc-static.com/upload/2018/10/12/15393584284089_raci%20projet.png)

### 9.10) Le calendrier de réalisation

Préciser quelles tâches sont réalisable en parallèle et lesquelles en séquence :

![m](https://user.oc-static.com/upload/2018/10/12/15393583109115_plan%20projet.png)

### 9.11) Les risques

Chaque risque doit être mesuré par son **impact** et sa **probabilité,** et agrémenté d’un **moyen de mitigation** s’il est déjà identifié.

### 9.12) Le *responsible*, *accountable*, *consulted* et *informed* (RACI)

Anticiper qui va exploiter les différents composants applicatifs et infrastructure retenus grâce à la méthode RACI.

### 9.13) Les coûts

Le rôle de l’architecte est de comprendre l’aspect technique des offres de services, des unités d’oeuvres proposées ou encore des différents devis.

## 10) *Organisez une revue par les pairs*

### 10.1) Le comité d'architecture technique (CAT)

Le comité d’architecture technique a pour but principal de **valider les systèmes ou applications en cours de conception.** Il faut présenter son dossier à un groupe composé de représentants de la DSI. Il faut être exhaustif, bonne communication.

### 10.2) La revue en groupe d'architecte

**La revue en groupe d’architectes** a l’avantage de moins exposer les jeunes architectes et de préparer les dossiers de façon **collégiale.** On va principalement chercher la somme des expériences communes pour  identifier les points faibles d’un dossier et les compléter au mieux.

### 10.3) La revue en binôme

Il vous faudra identifier un collègue qui sera votre binôme. Cela vous permettra de vous remettre en question.

## 11) *La mutation du métier*

L'implication de l'architecte est différente de nos jours :

- Un **accompagnement dans la durée**, en assumant les choix faits jusqu’à la production

- Une capacité à **guider les choix technologiques** ET à les **remettre en question** à tout moment

De plus, ils doivent prouver leur valeur dans des organisations aux cycles raccourcis. Il faut alors avoir **une vision de l'architecture en continu** en analysant le 4 couches. C'est à l'architecte d'assurer que toutes les couches sont bien comprises et partagées par tous.

Il faut aussi s'adapter aux changements technologiques car celles-ci changement très vite.

## 12) *Les innovations*

**Il faut évaluer les avantages et inconvénients de chaque solution.** 

**Utilisez la méthode proposée** en regardant :

- L’ensemble des axes **fonctionnel, applicatif, infrastructure et opérations** (sujet trop souvent mis de côté) ;
- Une **vue projet** (ex : calendrier, RACI) ;
- Une vue **coûts et organisation** (ex : disponibilité des ressources, compétences).

Toutefois, il faut se méfier des vendeurs "évangéliste" qui essaieront de vous poussez dans une direction.

Pour récolter les informations vous pouvez :

- Etre entourez d'experts
- S'informer
- Ne pas se précipiter
- ...

