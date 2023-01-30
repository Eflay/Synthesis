## 1) Commande Azure (Powershell)

Pour installer le module :

```powershell
Install-Module MSOnline 
```

---

Pour se connecter :

```powershell
Connect-MsolService 
```

---

Pour activer, le MFA une fois connecter :

```powershell
$st = New-Object -TypeName 
Microsoft.Online.Administration.StrongAuthenticationRequirement 
$st.RelyingParty = "*" 
$st.State = "Enabled" 
$sta = @($st) 

# Change the following UserPrincipalName to the user you wish to change state 
Set-MsolUser -UserPrincipalName  
CameronW@M365x674380.OnMicrosoft.com -StrongAuthenticationRequirements $sta 
```

---

Pour désactiver le MFA :

```powershell
Set-MsolUser -UserPrincipalName CameronW@M365x674380.OnMicrosoft.com 
-StrongAuthenticationRequirements @() 
```

---

Pour activer plusieurs utilisateur à la fois :

```powershell
$users = "DeliaD@M365x674380.OnMicrosoft.com",
"DiegoS@M365x674380.OnMicrosoft.com" 

foreach ($user in $users) 
{ 
   $st = New-Object -TypeName 
Microsoft.Online.Administration.StrongAuthenticationRequirement 
   $st.RelyingParty = "*" 
   $st.State = "Enabled" 
   $sta = @($st) 
   Set-MsolUser -UserPrincipalName $user 
-StrongAuthenticationRequirements $sta 
} 
```

---

Pour crée un accès conditionel :

```powershell
$conditions = New-Object -TypeName 
Microsoft.Open.MSGraph.Model.ConditionalAccessConditionSet 
$conditions.Applications = New-Object -TypeName 
Microsoft.Open.MSGraph.Model.ConditionalAccessApplicationCondition 
$conditions.Applications.IncludeApplications = "All" 
$conditions.Users = New-Object -TypeName 
Microsoft.Open.MSGraph.Model.ConditionalAccessUserCondition 
$conditions.Users.IncludeUsers = "All" 
$conditions.Users.ExcludeGroups = "e884a21d-792a-4d6b-ba37-117121f7474a" 
$conditions.ClientAppTypes = @('ExchangeActiveSync', 'Other') 
$controls = New-Object -TypeName 
Microsoft.Open.MSGraph.Model.ConditionalAccessGrantControls 
$controls._Operator = "OR" 
$controls.BuiltInControls = "Block" 

New-AzureADMSConditionalAccessPolicy -DisplayName 
"PowerShell_Block_LegacyAuthentication-ENI" -State "enabled" 
-Conditions $conditions -GrantControls $controls 
```

Celle-ci va exclure un utilisateur grâce à son ID de la condition. Elle sera nommée "PowerShell_Block_LegacyAuthentication-ENI".
---

Pour lister toutes les stratégies d'accès conditionels ou les modifier:

```powershell
Get-AzureADMSConditionalAccessPolicy 
Set-AzureADMSConditionalAccessPolicy 
```

## 2) Bonne Pratiques

Quelques bonnes pratiques sont ici proposées, basées sur l’expérience terrain de l’auteur.

Avant de commencer, il est important d’exclure de toutes les stratégies d’accès conditionnel les comptes brise-glaces.

1. - Convention de nommage

Édicter une convention de nommage afin de rendre les stratégies plus lisibles :

Par exemple : [ ID ] _[ Application ]_[ Scope ]_ [ Action ]

Voici quelques exemples :

CA04012021-00_LegacyAuthentication_ALL_Block

CA04012021-01_AzureMFA_Admins_Allow

CA04012021-02_AzureMFA_ALL_Allow

CA04012021-03_AzureMFA_B2b_Allow

2. - Organisation

Toujours séparer les stratégies de cette façon :

- Stratégie pour les administrateurs et comptes à privilège
- Stratégie d’accès uniquement pour les utilisateurs (utilisateurs standards)

Celles-ci doivent être indépendantes du type de plateforme ou système utilisé (poste de travail ou téléphone mobile).

Il n’est pas recommandé de mélanger ces deux populations dans les stratégies d’accès conditionnel. Ainsi, quand l’une d’entre elles concerne tous les utilisateurs (All Users), il est très important d’exclure les administrateurs et les comptes brise-glaces.

3. - Design avant implémentation

Il est important de construire votre matrice de stratégie qui reprend toutes les stratégies avant la mise en production. Ceci permet d’avoir une vision globale et surtout d’éviter les erreurs.

4. - Séparation des parties

Comme expliqué précédemment, il est important de définir des stratégies d’accès conditionnel en fonction de trois parties importantes et bien distinctes :

- Authentification : tout ce qui est lié au MFA et à l’authentification

- Les appareils : concerne les plateformes utilisées pour se connecter : les mobiles ainsi que les systèmes comme Windows 10

- Sécurité : toutes les règles liées à la sécurité de l’environnement Microsoft 365 et Azure
5. - Plan de test

Avant de commencer à appliquer les stratégies en production sur des utilisateurs, il est nécessaire de disposer des éléments suivants :

Pour jouer ce plan, nous proposons l’utilisation de What If afin de rendre le jeu de test complet et probant.

6. - Utiliser le mode Report Only

Utiliser le mode Report Only afin d’éviter les impacts, du reste cela vous permettra de bien comprendre les stratégies d’accès conditionnel dans votre environnement avant de les appliquer en production pour tous les utilisateurs.

7. - Legacy Authentication

Il faut bloquer les authentifications héritées comme nous l’avons fait précédemment, mais avant cela, il est nécessaire de regarder dans les logs Azure AD si vos utilisateurs utilisent des applications avec ce mode d’authentification pour éviter de les pénaliser. Il est aussi conseillé de faire une communication avant de déployer cette stratégie.

8. - Exemple de déploiement d’une nouvelle stratégie d’accès conditionnel

Voici l’exemple d’un déploiement de stratégie dans un environnement de production complexe que l’auteur a pour habitude de mettre en œuvre chez ses clients :

- Décrire le besoin et en parler en équipe (IT, sécurité et métier).

- Une fois le besoin défini et la règle à créer identifiée, écrire la stratégie d’accès conditionnel dans la matrice de design.

- La valider en équipe.

- Effectuer la prévalidation dans le Lab.

- Réaliser le test de la stratégie avec What If (attention, certains cas ne fonctionnent pas très bien) mais cela ne remplace pas un test en réel avec un vrai compte utilisateur.

- Une fois testé et le jeu de test validé en Lab, commencer le jeu de test sur l’infrastructure de production (incluant d’abord la simulation avec What If, ensuite un test avec un compte utilisateur réel de test, ou des groupes identifiés, etc.).

- Tester avec des utilisateurs "types" sur le scope défini (téléphone mobile, ou postes de travail, etc.).

- Valider avec ces utilisateurs "types" le comportement attendu.

- Remplir le fichier de jeux de test (le documenter et le valider en interne avec la population concernée).

- Communiquer avec les utilisateurs si besoin est (par exemple effectuer la publication des conditions d’utilisation à la prochaine connexion au portail Microsoft 365, ou MFA).

- Effectuer le passage en production en incluant un groupe d’utilisateurs pilotes dans la stratégie d’accès conditionnel.

- Valider les retours des utilisateurs pilotes.

- Activer la stratégie en mode Report Only afin de vérifier l’impact de la stratégie sur les utilisateurs.

-Réaliser le meeting de validation du pilote et de passage en production.

- Effectuer le passage en production avec tous les autres utilisateurs du groupe concerné.

## 3) Mettre en place Microsoft Defender for Identity

TOut d'abord, il faut mettre en place les capteurs et aussi crée la base de données.

Pour se faire rendez-vous sur le site : [Azure ATP](https://portal.atp.azure.com/)

Ensuite cliquer sur créer apresè -> Dans configuration -> Service Annuaire -> Enregistrer un utilisateur qui sera capable d'avoir au moins les droits en lectures sur tous les domaines Active Directory.

Ensuite il faut télécharger le programme d'installation du capteur, dans Configuration -> Capteur. Copier coller aussi la clé d'accès.

Pour finir mettez le fichier télécharger dans votre controleur de domaine et lancé le .exe et mettez votre clé d'accès.

## 4) Mettre en place Microsoft Defender for Office 365

Aller dans le [security center](https://security.microsoft.com/homepage) de microsoft -> Stratégie et règle -> Stratégies de menaces.
Ensuite cliquer sur "Rénitialiser les stratégies de sécurités" et actver le type de protection que vous voulez.

## 5) Simulations Phishing

Aller dans le [security center](https://security.microsoft.com/homepage) de microsoft -> Formation sur la simulation d'attaque -> simulation.
Ensuite configurer votre simualtion avec vos options. Lorsque que la simutlation est lancée, les utilisateurs recevront l'email et vous verrez en temps réel si ils ont été duper ou pas.
Vous pourrez leur proposer des formations s'ils l'ont été.

## 6) Microsoft Defender for Endpoint

Aller dans le [security center](https://security.microsoft.com/homepage) de microsoft -> Points de terminaison -> Gestion de la configuration -> accéder au paramètres -> intégration.
Télécharger le script et lancer-le sur la machine. Elle sera alors intégréer dans l'inventaire des appareils.

## 7) Protection des Informations

Pour aller dans le centre d'administration des protection des données, il faut aller sur ce [Compliance Microsoft](https://compliance.microsoft.com).

#### 7.1) <u>Création d'une étiquette de confidentialité</u>

Ensuite on va mettre en place des étiquettes. Pour ce faire, aller dans la section **"Protection des informations"** et crée une nouvelle étiquette. Vous pouvez choisir si l'étiquette sera appliquée sur les fichiers & e-mails, groupes et sites ou Azure Purview.

On peut choisir de chiffrer le document ou le mail et de le marquer. Si l'option marquer est activer cela ajoutera des en-têtes et des pieds de pages pour sécuriser le documents et le rendre unique.

Après, il faut configurer les paramètres de chiffrement, l'attribution des autorisations permet aux utilisateurs ou groupes sélectionnés de pourvoir lire le document chiffré avec cette étiquette ainsi que d'appliquer celle-ci.

Vien la configuration des droits du document, on peut choisir qu'il soit en mode read only, en écriture, ...

Ceci nous a permis de créer notre première étiquette basique, qui permet le chiffrement et des documents & e-mails.

#### 7.2) <u>Publication de l'étiquette de confidentialité</u>

Cliquer sur votre étiquette -> Publier l'étiquette

Viens un nouvel écran, sélectionnez les utilisateurs ou groupes où l'étiquette va être publiée, choisissez les paramètres et nommez votre stratégie.

Patientez 1h et vous pourrez sélectionnez l'étiquette dans l'environnement Cloud.

#### 7.3) <u>Installation de l'agent de Protection des Informations</u>

Pour les machines On-premises, il faut installer l'agent de Protection des Informations via l'url suivante [AIPUL](https://www.microsoft.com/en-us/download/details.aspx?id=53018). L'agent permet d'ajouter, le module Powershell, la visionneuse ainsi que la classification de dossier ou de fichier.

Ensuite installez-le sur la machines, il faut ensuite se connecter à votre environnements Cloud pendant l'installtion.

#### 7.4) <u>Monitoring</u>

L'activité de l'application des étiquettes peut être consultée dans "Explorateur d'activité".

#### 7.5) <u>Paramètres avancés</u>

Pour permettre de blocker les messages vers l'extérieur et trust uniquement notre domaine, il faudre faire comme suit :

```powershell
Install-Module -Name ExchangeOnlineManagement
Import-Module ExchangeOnlineManagement
Connect-IPPSSession -UserPrincipalName <Nom>
```

Ceci permettra de se connecter à votre domaine.

Ensuite pour afficher la configuration de la stratégie de publication :

```powershell
(Get-LabelPolicy -Identity <Nom>).settings
```

Récupérer le GUID d'une étiquette :

```powershell
Get-Label -Identity "<nom>" | Format-List
```

Pour bloquer la collaboration sur l'étiquette :

```powershell
Set-LabelPolicy -Identity <nom> -AdvancedSettings
${OutlookBlockUntrustedCollaborationsLabe="<GUID>"}
```

Pour autoriser le domaine interne :

```powershell
Set-LabelPolicy -Identity <nom> -AdvancedSettings
${OutlookBlockTrustedDomains="<Domain>"}
```

#### 7.6) <u>Etiquettes Automatiques</u>

*Pour l'étiquette orienté client.* (mot dans un document , ...)

Depuis le portail dédié, il vaut créer dans "Classification des données" un types d'infos confidentielles. Ensuite suivez les étapes et crée un nouveau modèle, en ajoutant un élément principal.

Une fois ceci fait, vous pouvez créer l'information sensible.

Maintenant pour l'appliquer, il faut modifier votre étiquette et aller dans la section étiquettage automatique et l'activer. Ajoutez la condition que vous venez de créer dans l'onglet "Classifications des données". et voilà le tour est joué.

*Pour l'étiquette orienté service.* (étiquetter tous les fichiers, ...)

Rdv dans protections des informations -> Créer une stratégie d'étiquetage automatique. Choisissez Custom -> Custom et remplissez les différentes étapes.

Ajoutez une nouvelle règle, et mettez-y votre type d'infos confidentielles. Par après, il faut choisir l'étiquette qui sera appliquée à la stratégie.

#### 7.7) <u>Etiquettes de confidentialité dans Teams, Sharepoint et Groupes M365</u>

Cela se fait que par ligne de commande.

Pour commencer, il faut activer le paramètre concerné :

```powershell
Install-Module AzureADPreview
Import-Module AzureADPreview
Connect-AzureAD
```

Pour récupérer la configuration actuelle de vos groupes de l'organisation :

```powershell
$Setting = Get-AzureADDirectorySetting -Id 
(Get-AzureADDirectorySetting | where -Property DisplayName
-Value "Group.Unified" -EQ).id
```

Pour activer l'étiquette :

```powershell
$Setting["EnableMIPLabels"]="True"
```

Pour appliquez et enregistrez les paramètres :

```powershell
Set-AzureADDirectorySetting -Id $Setting.id -DirectorySetting $Setting
```

Maintenant, il faut synchroniser ces paramètres avec Azure dans le cloud :

```powershell
Install-Module ExchangeOnlineManagement
Import-Module ExchangeOnlineManagement
Connect-IPPSSession -UserPrincipalName <nom>
Execute-AzureAdLabelSync
```

Il faudra attendre 24h et vous pourrez créer des étiquettes pour Groupes et SItes.

#### 7.8) <u>Super User</u>

Les Super User permettent de déchiffrer tous les fichiers.

```powershell
Connect-AipService
Enable-AipServiceSuperUserFeature
Add-AipServiceSuperUser -EmailAddress "<mail>"
```

#### 7.9) <u>Protection contre la perte de données</u>

Pour empêcher un message sensible d'être envoyé sur Teams (exemple).

il faut tout d'abord se rendre dans l'onglet "Protection contre la perte des données" et crée une nouvelle stratégie. L'emplacement sera pour Teams. 

Créer une règle personnalisé et ajoutez une condition qui inclut votre élément confidentiel. Remplissez les différents choix selon votre convenance et créer la stratégie.

Les DLP peuvent aussi s'effectuer sur les machines actives dans le domaines. Il ne faut pas oublier d'intégrer les appareils grâce au script fourni dans la platforme Azure.