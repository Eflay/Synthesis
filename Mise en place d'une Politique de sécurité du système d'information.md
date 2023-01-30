## 1) *Les objectifs d'une PSSI et ses enjeux*
Une Politique de Sécurité des Systèmes d’Information (PSSI) reflète la vision stratégique de la direction de l’organisme (PME, PMI, industrie, administration...) en matière de sécurité des systèmes d'information (SSI) et de gestion de risques SSI. 
Cette définition regroupe plusieurs éléments importants :
- Une dimension stratégique
- Un outil de communication
- Un socle commun de mesure

Plus simplement, une PSSI est un document exposant **la vision stratégique des dirigeants de l'entreprise en termes de SSI.**

### 1.1) Plan d'une PSSI
Il y a différentes façon de rédiger une PSSI. Voici un exemple type :
![PSSI](https://user.oc-static.com/upload/2019/05/09/15574277423222_p1c2-compressor.png)

## 2) *Les normes ISO2700x*
La rédaction d'une PSSI s'appuie sur des normes, notamment la famille **ISO 2700x.**
Ces normes regroupent un ensemble de standards et de bonne pratiques pour leurs travaux de sécurisation. L'application de ces normes garantit un cadre éprouvé et reconnu.
On utilisera les normes suivantes lors de notre mise en place :
- 27001 (socle pour la mise en place d'un Système de management de la sécurité de l'information)
- 27002 (méthodologie pour fixer les exigences et règles de sécurité)
- 27003 (Mise en place d'un SMSI)
- 27005 (Analyse de risque)

## 3) *Planification du projet*
La méthodologie se décompose en 4 étapes principales :
1. Donner un cadre à la démarche
2. Faire l'inventaire des moyens du SI
3. Analyser les risques
4. Choisir les mesures de sécurité

### 3.1) Donner un cadre à la démarche (phase 1)
La première étape est donc de proposer une note de cadrage. Pour rédiger cette phase, vous devez vous poser ces questions :
- Quelle est la mission de l’entreprise à laquelle la PSSI est appliquée ?
- Quelles informations sont présentes et ont de la valeur pour la mission de l’entreprise ? 
- Quelles sont les utilisations du SI par rapport à cette mission ?
- Quels éléments (de manière macroscopique) présentent particulièrement des risques ?

![Cadre](https://user.oc-static.com/upload/2019/05/09/15574279984963_Capture%20d%E2%80%99e%CC%81cran%202019-05-09%20a%CC%80%2020.53.01.png)

### 3.2) Formulez les enjeux et le champ d'application de la PSSI (phase 1)
Parrallèlement à l'étape précédente, vous allez devoir fixer un objectif à votre PSSI grâce aux éléments suivants :
- Faire référence spécifiquement à leur contexte de travail en termes de SSI
- Expliciter les enjeux de sécurité pour l'activité
- Présenter les actions à mettre en oeuvre pour amoindrir les risques

Ensuite vous allez définir **votre périmètre d'application** grâce aux questions suivantes : 
- Quelles sont les activités de l’entreprise ?
- Comment celles-ci sont-elles organisées et coordonnées entre elles ?
- Quel est le degré de criticité pour chacune de ces activités, c’est-à-dire quelles activités pourraient mettre en danger la mission de l’entreprise, si leurs informations étaient compromises, indisponibles, volées, ou encore rendues publiques ?

Par après vous déterminerez **les enjeux de sécurité** de votre entreprise.
L'objectif final est de **fixer les exigences de sécurité** pour améliorer le niveau sécurité du SI. Celles-ci sont liées aux **DICT** (Disponibilité, Intégrité, Confidentialité, Traçabilité).

### 3.3) Fixer le cadre légal et réglementaire (phase 1)
Pour définir ce cadre, voici les questions à vous poser :
- Quels sont les textes de haut niveau qui imposent des contraintes à l’entreprise ?
- Existe-t-il un règlement intérieur ?
- L’entreprise traite-t-elle des données personnelles ?
- A-t-elle des contrats particuliers avec des prestataires ?
- Quelles sont les normes (ISO 9001 pour la qualité, ISO 14001 pour la responsabilité environnementale) ?
- Quelles sont les références à donner aux différentes équipes pour intégrer la sécurité dans les projets de recherche ?

Vous auvez très certainement un cadre législatif commun dans votre pays, comme le RGPD, le Code pénal, le Code civil, ...

### 3.4) Faire le bilan des biens à protéger (phase 2)
Pour réaliser ce bilan, voici quelques questions à vous poser :
- Quels sont les éléments physiques et applicatifs du SI (locaux, serveurs, bases de données...) devant être protégés ?
- Quelle partie de l’organisation (membres, personnels ayant des fonctions sensibles)  possède une fonction critique qui doit être monitorée ?
- Quels sont les locaux qui méritent une attention particulière ?
- Quelles sont les catégories homogènes de biens (matériels, immatériels, organisationnels) à intégrer dans la démarche d’analyse ?
- À qui sera confiée la mise en œuvre des règles de sécurité?

### 3.5) Les principaux risques et la stratégie de mitigation (phase 3)
Pour mener une analyse et identifier les risques, vous pouvez utiliser plusieurs méthodes d'analyse des risques SSI. 
La formalisation de cette analyse se présente comme suit :
![risque](https://user.oc-static.com/upload/2019/05/09/15574281348476_p2c3.png)
![exemple](https://user.oc-static.com/upload/2019/05/07/15572339619422_Capture%20d%E2%80%99e%CC%81cran%202019-05-07%20a%CC%80%2014.54.42.png)
Par après, vous allez devoir définir une stratégie de traitement. 
Grâce à la méthode **EBIOS**, celle-ci vous propose différent niveaux de traitements :
- Réduction
- Partage
- Refus
- Maintien

Ce qui nous donne ceci : 
![traitement](https://user.oc-static.com/upload/2019/05/07/15572341261676_Capture%20d%E2%80%99e%CC%81cran%202019-05-07%20a%CC%80%2015.01.28.png)

### 3.6) Choisir les exigences et les mesures de sécurités (phase 4)
Une exigence de sécurité est **numérotée** et est exprimée sous la forme d’une phrase commençant par un **verbe, non technique et orientée** sur une fonction à remplir ou un service à délivrer. Par exemple, *“Sensibiliser le personnel du laboratoire aux enjeux sécurité”.*
Pour déterminer les exigences, voici encore une fois quelques questions :
- Quels sont les besoins de l’entreprise en termes de sécurité des locaux, de ses données et du traitement de ces données ?
- Quelles sont les procédures ou les méthodes que l’entreprise doit mettre en oeuvre pour éviter qu’un risque se concrétise ou pour en réduire les impacts ?
- Sur quels acteurs doit-on appliquer les exigences ?
- Comment diminuer les risques identifiés dans le tableau ?
- Comment répondre aux principales obligations légales en termes de sécurité des SI de la structure ?

Pour déterminer les règles à appliquer dans chaque exigence, il faut s'appuyer sur les bonnes pratiques :
- Norme ISO27002
- Document de référence de l'ANSSI
- Guide de l'hygiène informatique
- ...

Pour réaliser cette étude, vous allez vous poser les questions suivantes :
- Cette règle générique s’applique-t-elle à mon contexte ?
- Quelles sont les circonstances particulières qui en nuancent ou en complètent la vision ?
- À quel composant du SI s’applique cette règle ?
- Comment le responsable du composant va-t-il appliquer la règle correspondante ?
- Peut-on externaliser cette règle ?

### 3.7) Finir la rédaction de la PSSI
N'oubliez pas **les coordonnées des personnels et la matrice exigence risque.**
