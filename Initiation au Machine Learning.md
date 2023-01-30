# ++**Initiation au Machine Learning**++
## 1) ++Introduction++
Nous allons appréhender le métier de **Data Scientist** car c'est celui qui va le plus utilisé la technologie du machine learning.
D'autres métiers comme **Data Analyst** ou **Data Architect** peuvent aussi aider le Data Scientist pour certaines tâches.
## 2) ++Le cycle de travail du Data Scientist++
Il y a 6 différentes étapes dans le cycle de travail de ce métier :
1. **Récupération des données**
2. **Nettoyage des données**
3. **Exploration des données**
4. **Modélisation**
5. **Evaluation et interprétation**
6. **Mise en production**

### 2.1) La récupération des données
Dans cette étape, le but est de **récupérer le maximum d'information** qui serait susceptible de vous intéresser dans votre mission.
Cela peut se faire via plusieurs méthodes :
- Base de données existantes
- Données brutes
- Création de nouveaux canaux d'acquisition
- ...

### 2.2) Le nettoyage des données
Nettoyer les données signifie **qu'elles doivent être consistantes, sans valeures aberrantes ni manquantes.**
Elle doivent aussi être toutes sous le même format et accessible au même endroit. On peut créer aussi un regroupement de ces informations qui sera appelé **Data Lake.** 
C'est lors de cette étape qu'un Data Architect peut être appelé car celui-ci sera plus spécialisé dans ce domaine et donc vous octroyez un gain de temps.
**Retenez donc que l'important, c'est de bien prépaper le terrain pour les étapes suivantes. Vous y gagnerez du temps au final.**

### 2.3) L'exploration des données
Cette étape vous permets de **mieux comprendre les différents comportements et de bien saisir le phénomène sous-jacent.**
A la fin de cette étape vous devez être en mesure de :
- Proposer plusieurs hypothèses sur les causes sous-jacentes à la génération du dataset
- Proposer plusieurs pistes de modélisation statistique des données, qui vont permettre de résoudre la problématique de départ considérée
- Proposer si nécessaire de nouvelles sources de données qui aideraient à mieux comprendre le phénomène

C'est dans ces phases que les Data Scientist passe le plus clair de leur temps.

### 2.4) Modélisation des données
Dans cette étape nous allons créer un modèle statistique associé aux données qui nous intéressent. **C'est ça qu'on appelle le machine learning.**
L'objectif de ce modèle est de **considérer que chaque donnée observée est l'expression d'une variable aléatoire générée par une distribution de probabilité.** Celui-ci peut être de type **stochastique¹** ou **déterministe²**.
La modélisation consite à **trouver le bon modèle statistique qui collera au mieux avec les données traitées.**
 = synonyme d'aléatoire
² = chaque élément est déterminé par des évènements passés

### 2.5) Evaluer et interpréter les résultats
Cette étape consiste à **évaluer la qualité de notre modèle, c'est-à-dire sa capacité à représenter avec exactitude notre phénomène et à résoudre notre problèmatique.**
**Le Quartet d'Anscombe** permet de montrer visuellement que pour 4 jeux de données très différent on obient la même droite de régression.
![Quartet d'Anscombe](https://user.oc-static.com/upload/2016/09/17/14741418471714_640px-Anscombe.svg.png)

### 2.6) Déployer le modèle de production
Cette étape consiste à déployer votre modèle sur le web ou dans votre entreprise. Pour que des données inconnue puissent être entrée et que votre modèle en ressorte une approximation.

## 3) ++Type d'apprentissage du modèle++
### 3.1) Apprentissage supervisé
Les données récupérés lors de l'apprentissage supervisé sont **annotées**, c'est-à-dire qu'elles sont déjà associées à un label.
Vous voulez que votre algorithme soit capable de prédire dans quels labels seront les données dans le futur.
De facon plus mathématique, on va recevoir des données sous la forme de :
`(x1, y1),(x2, y2),...`
et on espère prédire la sortie sur de nouvelles observations :
`x* ---> y*`

### 3.2) Apprentissage non supervisé
L'algorithme va lui même essayé de catégoriser les données entre-elles car celles-ci ne sont pas annotées d'avance.
De facon plus mathématique, on va recevoir des données sous la forme de :
`x1, x2, x3, ...`
et on espère prédire la sortie sur de nouvelles observations :
`xₐ ---> yₐ`

## 4) ++Type de sortie++
### 4.1) Régression et classification
Si le type de valeurs de vos données en sortie sont **continues** (nombre) alors le type de sortie sera appelé **régression**.
Si le type de valeurs de vos données en sortie sont **discrète** (catégorie) alors le type de sortie sera appelé **classification**.
![Type de sortie](https://user.oc-static.com/upload/2016/09/18/14742103795655_ml.png)

## 5) ++Les besoins liés au machine learning++
Nous allons voir quelques exemples de solutions de machine learning. **Ce n'est en aucun cas une liste exhaustive.**

### 5.1) Prédire la rentabilité d'une campagne marketing
Les entreprises ont souvent besoin d'évaluer leur retour sur investissement (ROI).
Ce type de prédiction fera appel à des méthodes de **régression** puisqu'on veut obtenir une valeur numérique.

### 5.2) Affecter une catégorie à un produit
L'automatisation de cette tâche peut se faire avec des algorithmes de classification. En effet, la problématique est typiquement une **classification supervisée**.

### 5.3) Segmenter les visiteurs d'un site
Ce besoin peut se résoudre de diverses manière :
- Classification supervisée en annotant manuellement des segments
- Prédire à l'aide d'une régression la susceptibilité de conversion d'un client et effectuer une segmentation
- Effectuer une classification non supervisée afin de détecter les nouveaux groupes

### 5.4) Le clustering
Les algorithmes non supervisé détermineront les similitudes entre les données et les regrouperont en cluster.
![Clustering](https://user.oc-static.com/upload/2016/09/18/14742183540992_clustering.png)

### 5.5) Les évènements rares
Il est aussi possible de déterminer les évènements rares appelés **outlier** avec les méthodes de machine learning. On va tout simplement fixer un critère de distance qui permettra de déterminer si une entrée est trop éloignée de la modèlisation.
![Outlier](https://user.oc-static.com/upload/2016/09/18/14742169177589_outlier-2.png)

## 6) ++Les outils de Data Science++
### 6.1) R ou Python ?
**Le langage R** est utilisé historiquement par des statisticiens. Celui-ci sera donc plus poussé dans certaines fonctionnalités mathématiques.
**Le langage Python** est le langage de référence pour tous les ingénieurs pour mettre en place rapidement des algorithmes mathématiques.
Comme vous l'aurez compris, si vous souhaitez plus vous développez dans la branche statistique, privilégier R. Si vous êtes plus dans une branche informatique, prener Python.

### 6.2) Le nettoyage et l'exploration
L'écosystème **Scipy** est majoritairement utilisé avec les principales librairies suivantes :
- pandas (création de tableau à partir des données brutes)
- numpy (génération de matrices)
- matplotlib (générer des graphiques)
- iPython (feuilles de calculs)
- ...

### 6.3) Modélisation
Deux librairies sont les plus utilisées, il s'agit de **TensorFlow** et **Scikit-Learn**.
TensorFlow est plus complet et populaire mais Scikit-Learn est beaucoup plus simple d'accès.
Pour les débutants, il est donc conseillé de prendre Scikit-Learn.

### 6.4) Mise en production 
Le principale écosystème utilisé lors de cette étape est **Hadoop**. Notamment grâce au faite qu'il soit très complet.

### 6.5) API
Si vous manquez de temps lors de votre projet et que vous devez tester rapidement la viabilité de celui-ci. Vous pouvez passer par une API comme **Google Cloud IA, Microsoft Azure Machine Learning, Aws Machine Learning,...**

## 7) ++Construire un modèle statistique++
L'objectif du machine learnine est de **trouver un modèle qui effectue une approximation de la réalité**. Forcément puisqu'on fait une approximation, on aura une **perte d'information** qui est **un bruit non modélisé et qu'on estime indépendant**. 
La formule se résume grâce à l'équation suivante :
![Formule](https://user.oc-static.com/upload/2019/04/23/15560370661134_3c1-a.jpg)
Le modèle sous-jacent représente une contrainte de forme non dépendantes des données. Les notions de **complexité/contrainte/flexibilité** est primordial dans le travail de modélisation.
Voici un exemple si vous ne prenez pas en compte ces éléments et que vous choisi un mauvais modèle sous-jacent :
![Mauvais Modèle](https://user.oc-static.com/upload/2016/11/02/14781049277529_droite_nulle.png)
Les modèles sont le plus souvent représentés par un ensemble de paramètres qu'on mettra dans un **vecteur θ**. Une droite peut se représenté par l'équation suivante :
`y = θᵀx`

### 7.1) La fonction loss
En apprentissage supervisé, la notion principale est **la perte d'information** due à l'approximation. Elle détermine à quel point notre modélisation du phénomène perd de l'information par rapport à la réalité observée.
La plupart du temps, les algorithmes d'apprentissage **supervisé** utilisent cette fonction de perte. Cela se résume souvent à une méthode itérative qui converge vers un minimum. 
**Donc plus la perte d'information diminue, plus on se rapproche vers un modèle de meilleur qualité car plus réaliste.**

#### 7.1.1) Minimiser l'erreur du modèle
Une manière de représenter cette perte se fait par ce qu'on appelle **l'erreur** ou **le risque**. C'est-à-dire l'éloignement des données par rapport à la prédiction effectuée.
![Eloignement](https://user.oc-static.com/upload/2016/11/02/14781051794302_bien-mal.png)
La distance la plus utilisée pour mesurer cet éloignement est **l'erreur quadratique.**
Le plus souvent, on ne peut pas calculer directement l'erreur. Grâce aux données récoltées, on utilisera **une approximation** de celle-ci. On appelera cette erreur **le risque empirique**. Nous cherchons à converger vers le minimum de risque empirique sur notre modèle.

#### 7.1.2) Maximiser la vraisemblance du modèle
La vraisemblance d'un jeu d'observation par rapport à un modèle statistique est la fonction suivante :
`L(θ)=p(x₁...xₙ|θ)`
Cette valeur représente la probabilité d'avoir le jeu d'observation étant données les paramètres θ.
A l'inverse de la méthode précédente, il faut ici se rapprocher vers le maximum de la fonction. Ce qui en découle la fonction suivante :
`θ^ = argmax₀L(θ)`(*l'accent circonflexe doit d'être au dessus de théta*)
L'accent circonflexe est utilisé lorsqu'on parle d'un estimateur et pas de valeur réelle.

## 8) ++Programmer une régression linéaire++
### 8.1) Définir la problématique et ses données d'entrainements
Une fois que vous avez défini votre problématique et ses données d'entrainements, vous pouvez charger et afficher les données si vous souhaitez un meilleur visuel.
```python
import numpy as np`
import pandas as pd
import matplotlib.pyplot as plt
#On charge le dataset
house_data = pd.read_csv('house.csv')
#On affiche le nuage de points dont on dispose
plt.plot(house_data['surface'], house_data['loyer'], 'ro', markersize=4)
plt.show()
```

Voici un type de résultat que vous pourrez avoir :
![Loyer/surface](https://user.oc-static.com/upload/2019/04/23/15560371787169_3c1-b.jpg)
Dans notre modèle d'eentrainement, on voit clairement que Y dépent de X de manière linéaire. On peut donc émettre une hypothèse de modélisation qui est que le phénomène possède la forme d'une droite.
Cependant nous voyons qu'il y a certains évènements rares à partir d'un certain loyer. Nous allons donc enlevé ces outliers de notre modèle comme suit :
`house_data = house_data[house_data['loyer'] < 10000]`

### 8.2) Reformuler le problème dans l'espace de l'hypothèse
Dans notre exemple, il y a une relation linéaire entre l'entrée (observations) et la sortie (prédiction).
Notre contrainte de modèle sous-jacent doit être sous la forme suivante :
`y^ = xᵀθ`
avec `xᵀ=(x₁,x₂,x₃,...,xₙ), y^T=(y1^,y2^,y3^,...,yₙ^)`
où N est le nombre d'observations.
En générale une observation à plusieurs variables qui la caractérisent. Donc une observation est caractérisé par un vecteur :
`xᵢᵀ=(1,vⁱ₁,vⁱ₂,...,vⁱₐ)`
*La constante 1 est ajoutée après chaque observation pour représenter l'ordonnée à l'origine et avoir une écriture vectorielle plus compacte.*

### 8.3) Définir la fonction loss
La distance euclidienne (erreur quadratique) d'une observation yᵢ, vis-à-vis de notre modèle yᵢ^, est :
`||y^ᵢ−yᵢ||₂=||xTᵢθ−yᵢ||2`
Le risque empirique pour N observation est donc :
`E=∑ᴺᵢ=1||xTᵢθ−yᵢ||2  `

### 8.4) Apprentissage
```python
# On décompose le dataset et on le transforme en matrices
X = np.matrix([np.ones(house_data.shape[0]),house_data['surface'].values]).T
y = np.matrix(house_data['loyer']).T
# On effectue le calcul exact du paramètre theta
theta = np.linalg.inv(X.T.dot(X)).dot(X.T).dot(y)
print(theta)
Le résultat nous donne la valeur numérique de théta. Le modèle final qui colle bien aux données sera :
y = 2e résultat * x + 1er résultat
on peut représenter graphiquement la droite comme suit :
plt.xlabel('Surface')
plt.ylabel('Loyer')
plt.plot(house_data['surface'], house_data['loyer'], 'ro', markersize=4)
# On affiche la droite entre 0 et 250
plt.plot([0,250], [theta.item(0),theta.item(0) + 250 * theta.item(1)], linestyle='--', c='#000000')
plt.show()`
```
Ce qui nous donnera dans notre cas ceci :
![Régression linéaire](https://user.oc-static.com/upload/2016/11/03/14781762372969_loyers_fit.png)

### 8.5) Exploiter vos jeux de données
Si lors de votre étape de récoltes de données celles-ci sont beaucoup trop nombreuses, ça peut provoquer une perte énorme de temps. Pour contrer cet inconvénient, on peut utilisé la méthode de **l'échantillonage**.
L'inconvénient de cette méthode est qu'elle doit être représentative malgré l'échantillion prévelé.
Avec Python effectué un échantillion est assez simple :
`sample = np.random.randint(data_size, size=int(data_size*0.1))`
`sampled_data = data.iloc[sample]`

### 8.6) Training set et Testing set
Pour avoir un modèle de qualité, il faut éviter le piège de reprendre les mêmes données utilisées pour construire votre modèle ainsi que pour son test.
C'est pour ça qu'il faut dés le départ séparé votre jeu de données en deux groupes.
**Le training set** servira d'entrainement pour votre modèle et sera utilisé par l'algorithme d'apprentissage.
**Le testing set** permet de mesurer l'erreur du modèle final sur des données qu'il n'a jamais vues.
En général une portion de 80% de training set et 20% de testing sont recommandés.
Cela prend cette forme en dans notre programme :
`from sklearn.model_selection import train_test_split`
`xtrain, xtest, ytrain, ytest = train_test_split(X, y, train_size=0.8)`

## 9) ++Le modèle K-NN++
### 9.1) Fonctionnement
Le diminutif de K-NN est K Nearest Neighbors, c'est un algorithme qui peut aussi bien servir pour la classification que pour la régression. 
Prenons un enxemple :
![KNN](https://user.oc-static.com/upload/2016/10/10/14761049971968_k-nn-1.png)
Si nous prenons le 5-NN sur cette image, cela veut dire qu'on va prendre les 5 voisins les plus proches de chaque entrée. Ce qui va donc faire apparaitre deux "camps".
![5NN](https://user.oc-static.com/upload/2016/10/10/14761050284224_k-nn-2-2.png)
![5NN](https://user.oc-static.com/upload/2016/10/10/14761050939309_k-nn-3.png)
Pour mettre en place ce système dans un programme, il faut faire comme suit :
`from sklearn import neighbors`
`knn = neighbors.KNeighborsClassifier(n_neighbors=3)`
`knn.fit(xtrain, ytrain)`
`error = 1 - knn.score(xtest, ytest)`
`print('Erreur: %f' % error)`
Le résultat renvoie **le pourcentage de prédiction véridique.**

### 9.2) Trouver le bon K
Avec le code suivant, vous trouverez le K optimal :
`errors = []`
`for k in range(2,15):`
    `knn = neighbors.KNeighborsClassifier(k)`
    `errors.append(100*(1 - knn.fit(xtrain, ytrain).score(xtest, ytest)))`
`plt.plot(range(2,15), errors, 'o-')`
`plt.show()`
Vous obtenez un schéma comme ceci : 
![KNN](https://user.oc-static.com/upload/2018/12/13/15447033941192_figure-3.png)
Nous devons prendre l'élément le plus bas par rapport à l'axe des y. Ici ça sera donc 4.

## 10) ++Les limites du machine learning++
### 10.1) Le théorème No Free Lunch
Ce théorème met en lumière qu'aucun algorithme n'est, à ce jour, capable de résoudre tous les problèmes. Un modèle étant **une approximation de la réalité** car ils reposent sur un certain nombre d'hypothèses de départ. Celles-ci étant différentes pour chaque problème, on doit considérer différents modèles pour différents problèmes

## 10.2) Les problèmes insolubles
Cette notion désigne les problèmes qui **ne peuvent être résolus dans un temps raisonnable**, qui explosent en terme de complexité algorithmique.
Pour essayer d'évite ce problème, voici différents moyens :
- Réduire le nombre de variables en entrée
- Réduire la taille du dataset
- Réduire la complexité des hypothèses

## 11) ++Biais/Underfitting et Variance/Overfitting++
S'il y a une trop grosse dépendance au training set, suite à une mauvaise configuration, notre modèle sera de mauvais qualité. Cette dépendance est appelé **variance**. En voici un exemple :
![Variance](https://user.oc-static.com/upload/2016/10/14/14764380252279_1-nn-overfit.png)
Si, à l'inverse de la variance, on prend un problème avec une complexité trop simple. On aura aussi un modèle de mauvaise qualité. Ce problème est appelé **biais**, en voici un exemple :
![Biais](https://user.oc-static.com/upload/2016/10/14/14764384998991_underfit.png)
Il faut trouver une balance entre les deux pour avoir un bon modèle.
![Opti](https://user.oc-static.com/upload/2019/04/23/15560372893965_4c2.jpg)
