## 1) *Une machine virtuelle*
Tout d'abord, pour une machine virtuelle voici plusieurs contraintes :
- Prend du temps à démarrer
- Réserve les ressources du système hôte

Mais aussi quelques avantages liés aux inconvénients :
- Totalement isolé du système hôte
- Les ressources lui sont totalement dédiée
- Installation de différents OS possible

## 2) *Un conteneur*
C'est **un processus** ou **un ensemble de processus** isolés du reste du système, tout en étant légers.
Celui-ci permet de faire de la virtualisation légère car il ne virtualise pas les ressources comparé à la machine virtuelle.
Pour vous donnez une idée voici un schéma :
![schéma](https://user.oc-static.com/upload/2019/05/13/15577645779374_vm-vs-conteneur.png)
Les avantages du conteneur sont nombreux :
- Réserver que les ressources nécessaires
- Démarrer rapidement
- Plus d'autonomie pour les développeurs
- Réduire les coûts
- Réduire la densité de l'infrastructure

## 3) *Docker*
Le logiciel open-source a été crée par la société Docker Inc, anciennement DotCloud.
Dans la vision de Docker, un conteneur ne doit faire tourner **qu'un seul processus.**
![Logo](https://user.oc-static.com/upload/2019/05/10/15574814980481_Docker-660x269.png)

### 3.1) Pourquoi l'utiliser ?
Tout d'abord, il permet d'avoir **un environnement unifié et fonctionnel** chez l'ensemble des utilisateurs.
Ensuite, il peut aussi servir pour **créer des environnements locaux**.

#### 3.1.1) Stateless/Stateful et immutabilité
Un élément est **stateful** si l'application doit gérer un état comme par exemple celle d'une base de données.
A l'inverse, il est **stateless** s'il ne stocke pas d'état.
Un conteneur ne doit ni être modifié ni stocker des valeurs qui doivent être pérennes.

### 3.2) Installation de Docker
Tout d'abord commencer par mettre à jour votre système et les appliquez.
```bash
sudo apt-get update 
sudo apt-get upgrade
```
Ensuite télécharger le fichier .deb des version de docker-ce-cli, docker-ce, containerd.io. Pour se faire aller sur le site de docker suivant (ubuntu):
[Download Docker Deb](https://download.docker.com/linux/ubuntu/dists/hirsute/pool/stable/amd64/)
Lorsque vous aurez téléchargé les fichers, installer les :
```bash
sudo dpkg -i "VotreCheminDeb"
```
Pour vérifier votre installation, exécuter la commande suivante :
```bash
sudo docker run hello-world
```
Elle permettra de lancer un script vous téléchargeant automatiquement un fichier et vous l'affiche.
Enfin pour vous octroyez les accès nécessaire :
```bash
sudo usermod -aG docker VotreUtilisateur
```
La commande ajoutera aux droits votre utilisateur. (-a = append, -G = Groups)

### 3.3) Lancer un conteneur en local
Comme vous l'avez vu dans la commande précédente, il vous suffit de faire **un docker run.**
Tout d'abord, docker va recherché en local si le conteneur existe déjà. Ensuite, s'il ne le trouve pas, il va vous le télécharger automatiquement en allant sur docker hub. 
Les arguments que vous passez après le run sont appelés **des images.**
Si l'on souhaite que le conteneur reste allumé, il faudra rajouter l'option **-d**, qui signifie **detach.**
L'option permettra de ne pas rester attaché au conteneur et donc de pouvoir en lancer plusieurs.
Grâce à la commande suivante vous pourrez démarrer un conteneur sur un certain port : 
```bash
docker run -d -p 8080:80 "VotreConteneur"
```
L'option -p permet de **spécifier le port** où vous voulez travaillez. Dans ce cas, vous devez vous rendre à http://127.0.0.1:8080

#### 3.3.1) Arrêtez votre conteneur
Il suffit simplement de faire la commande suivante :
```bash
docker stop "IDduConteneur"
```
Pour connaitre l'ID de votre conteneur, faire la commande :
```bash
docker ps
```
Celle-ci listera tous vos conteneur allumé + leurs IDs associés.
Enfin pour supprimer le conteneur : 
```bash
docker rm "IDduConteneur"
```

#### 3.3.2) Récupérer des images sur Docker Hub
Cela se fait avec la commande :
```bash
docker pull "Conteneur"
```

#### 3.3.3) Pour nettoyer votre système Docker
Grâce à la commande suivante :
```bash
docker system prune
```
Les données de **l'ensemble des conteneur arrêtés, des réseaux crées arrêtés, des images non utilisées et des caches utilisés pour la création d'image Docker.**

### 3.4) Créer son premier Docker File
La première chose à faire est de **créer un fichier "Dockerfile"** puis de définir dans celui-ci l'image que vous allez utilisé grâce à l'instruction **FROM.**
Vous trouverez ci-dessous un fichier exemple :
``` bash
FROM "Distribution"

RUN apt-get update -yq \
&& apt-get install curl gnupg -yq \
&& curl -sL https://deb.nodesource.com/setup_10.x | bash \
&& apt-get install nodejs -yq \
&& apt-get clean -y

ADD . /app/
WORKDIR /app
RUN npm install

EXPOSE 2368
VOLUME /app/logs

CMD npm run start
```
L'instruction **RUN** permet d'exécuter une commande dans notre conteneur. Attention a limité l'utilisation de cette commande, afin de réduire la taille de notre image. Car chaque commende RUN crée un layer, qui rajoute de la taille.
L'instruction **ADD** afin de copier ou télécharger des fichiers dans l'image.
L'instruction **WORKDIR** permet de modifier le répertoire courant, c'est l'équivalent de la commande cd.
L'instruction **ExPOSE** ermet d'indiquer le port sur lequel l'application écoute.
L'instrction **VOLUME** permet d'indiquer quel répertoire vous voulez partager avec votre host.
L'instruction **CMD** permet à notre conteneur de savoir quelle commande lancer au démarrage.
Puis créer votre image avec la commande suivante :
```bash
docker build -t ocr-docker-build .
```
L'argument -t permet de donner un nom à notre image et le point est notre réertoire où se trouve le Dockerfile.
Ensuite lancer votre conteneur :
```bash
docker run -d -p 2368:2368 ocr-docker-build
```

### 3.5) Envoyez des images sur Docker Hub
Après avoir créer un compte, vous devez faire la commande :
```bash
docker login
```
Cela permettra de lier votre compte à votre machine.
Ensuite, il faut créer un lien entren notre image et l'image que nous voulons envoyer :
```bash
docker tag ocr-docker-build:latest "VotrePseudoDockerHub"/ocr-docker-build:latest
```
Lorsque ceci est fait, vous pouvez envoyer votre image :
```bash
docker push "VotrePseudoDockerHub"/ocr-docker-build:latest
```

### 3.6) Docker Compose
Docker Compose permet d'orchestrer vos conteneurs et ainsi de simplifier vos déploiements sur de multiple environnements, le tout dans **un fichier YAML**.
![Compose](https://user.oc-static.com/upload/2019/05/08/15573466889395_1_QVFjsW8gyIXeCUJucmK4XA.png)
Pour l'installer il vous suffit de faire ceci :
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose && sudo chmod +x /usr/bin/docker-compose
```
Voici quelques commandes du CLI de Docker Compose :
- docker-compose up (lancer la création de l'ensemble des conteneurs appelé **stack**)
- docker-compose down (détruire l'ensemble des ressources crées)
- docker-compose config (valider la syntaxe du fichier de config)

Les autres commandes sont les mêmes que pour Docker à l'exception d'utiliser docker-compose à la place de docker.

#### 3.6.1) Création de fichier Docker Compose
Pour commencer, il faut créer un fichier "docker-compose.yml". Le début de celui-ci sera toujours la version que vous allez utilisé.
Voici le fichier complet que je vais détailler :
```bash
version: '3'
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress

volumes:
  db_data: {}
```
L'ensemble des conteneurs qui doivent être créés son sous l'argument **services**. Chaque conteneur commence par un nom qui lui ai propre.
Ensuite nous décrivons notre conteneur, on va définir son image avec l'argument **image**. L'argument **volumes** permet de stocker l'ensemble du contenu du dossier en question.
De plus, lorsque le processus rencontre une erreur on lui spécifie qu'il redémarre toujours avec l'argument **restart**. Pour définir des variables d'environnements, il suffit d'ajouter l'argument **environment**.
Enfin l'argument **depends_on** permet de faire une dépendance entre deux conteneurs.

#### 3.6.2) Lancer votre stack
Grâce à la commande :
```bash
docker-compose up -d
```
Il ne reste plus qu'a vérifier si votre site wordpress fonctionne à l'adresse http://127.0.0.1:8000