# bikeNantes

## Projet regroupant les différentes API développées pour la ville de Nantes

### Technologies utilisées
- Node.js
- Base de données Cassandra
- Memcached
- Angular2

### Contributeurs
 - Laura Souchu
 - Thomas Berthé
 - Tanguy Le Roux
 
 ### Notice d'installation
 
 #### Récupérer et mettre à jour les sources
 
 - Récupérer le projet via Github
 ```
git clone git@github.com:Dasten-Duranin/bikeNantes.git
```

- Mettre à jour les sous projets présents dans le projet 
 ```
 cd bikeNantes
git submodule update --init --force --remote
```

- Pour les dossiers weatherNantes, pollutionNantes, volVelo et alertNantes, lancer la commande de mise à jour des modules à l'aide de npm
 ```
npm install
```

- Pour le dossier Appli, il faut d'abord installer Angular
 ```
npm install -g @angular/cli
npm install
```

###### L'application est maintenant prête à être utilisée, il ne reste plus qu'à installer et configurer Memcached et Cassandra.

#### Installation de NodeJs
NodeJs permet de gérer la partie serveur de l'application. Voici le lien pour installer : <a href="https://nodejs.org/en/">installer nodeJs</a>

#### Installation de Memcached
Memcached est utilisé par l'API weatherNantes qui vient stocker les informations en cache. Pour l'installer, ouvrir un terminal puis suivez les instructions.

- Linux
```
sudo apt-get update
sudo apt-get install memcached
```

- MacOS
```
brew install memcached
```

- Windows<br>
Suivre le tutoriel : <a href="https://commaster.net/content/installing-memcached-windows" target="_blank">Lien vers le tutoriel</a><br><br>

Une fois Memcached installé, dans le terminal lancer la commande :
```
memcached
```

###### Memcached est prêt à être utilisé.

#### Installation de Cassandra
Cassandra est une base de données de type NoSQL. Elle est utlisée par l'API weatherNantes et volVelo. Pour l'installer, suivez le tutoriel qui correspond à votre OS.

- Linux<br>
Suivre le tutoriel : <a href="https://cassandra.apache.org/download/" target="_blank">Lien vers le tutoriel</a>

- MacOS<br>
Suivre le tutoriel : <a href="https://gist.github.com/hkhamm/a9a2b45dd749e5d3b3ae" target="_blank">Lien vers le tutoriel</a>

- Windows<br>
Suivre le tutoriel : <a href="https://www.tutorialspoint.com/cassandra/cassandra_installation.htm" target="_blank">Lien vers le tutoriel</a><br><br>

Une fois Cassandra correctement installé, ouvrir un terminal et lancer la commande :
```
cqlsh
```
Vous êtes maintenant connectez à la base de données Cassandra.<br>
Voici les deux scripts à exécuter afin de créer les deux bases de données utilisées :

- Script pour l'API weatherNantes :
```
CREATE KEYSPACE weathernantes WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};
USE volvelo;
CREATE TABLE weather2(weather_id uuid primary key, condition varchar, date date, icon varchar, temp float, temp_max float, temp_min float);
```

- Script pour l'API volVelo :
```
CREATE KEYSPACE volvelo WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};
USE volvelo;
CREATE TABLE vol(vol_id uuid primary key, location varchar, date date, owner varchar, new boolean);
```

###### Voilà ! L'application est prête à être lancée ! Il ne reste plus qu'à démarrer les APIs et l'application Angular.

Depuis la racine du dossier bikeNantes, voici les commandes à exécuter pour démmarer l'ensemble de l'application (vous devrez avoir un terminal ouvert pour chaque API) :
```
node alertNantes/app/server.js
node pollutionNantes/app/server.js
node volVelo/app/server.js
node weatherNantes/app/server.js
```
Puis démmarez l'application Angular :
```
ng serve --open
```
 L'application est lancée sur <a>http://localhost:4200</a><br><br>
Enjoy !
