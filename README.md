#Simulation un réseau de bus

```
le rapport complet est dans le dossier data/
```

## L’Objectif du travail

l'objectif de ce travail est de créer une application dans le domaine des objets connectés qui consiste
à simuler un réseau de bus et de stations , en considérant que chaque bus possède un capteur qui
transmis sa position vers le cloud , chaque station de bus reçois la position des bus puis calcule le
temps d'arriver de chaque bus.
La deuxième partie de ce travail consiste à appliquer un des algorithmes d’apprentissage automatique
et de prédire le temps d’attente des bus.

## Structure du programme

pour bien décortiquer le problème, nous avons créés 2 classe Bus.py, Station.py , un fichier utils.py
pour les fonctions utilitaires et main.py pour la fonction principale.
Le fichier bus_predicition.py contient analyse les données collectées par les stations, le temps
d’attente calculé, puis il prédit le temps d’attente avec un algorithme d’apprentissage automatique.


```
#### Classe Bus :

La classe bus contient 6 attributs et 6 méthodes:
Id : un identifiant unique de type entier pour chaque bus.
Img : une image qui représente le bus sur l’interface graphique.
Stop : une variable de type booléenne, vraie dans le cas où le bus s’est arrêtée.
Température : désigne la température du bus de type réelle, généré d’une manière aléatoire.
X_pos : un entier qui représente la position du bus dans l’interface graphique par rapport à l’axe X.
Y_pos : un entier qui représente la position du bus dans l’interface graphique par rapport à l’axe Y.
setPosition() : une méthode qui sert à initialiser la position du bus.
getPosition() : une méthode qui sert à récupérer la position du bus.
sendPosition() : une méthode qui sert à envoyer la position du bus au cloud.
setTemperature() : une méthode qui sert à initialiser la température du bus.
getTemperature() : une méthode qui sert à récupérer la température du bus.
sendTemperature() : une méthode qui sert à envoyer la température du bus au cloud.


#### Classe station :

La classe bus contient 7 attributs et 5 méthodes:
Id : un identifiant unique de type entier pour chaque station.
Img : une image qui représente la station de bus sur l’interface graphique.
logger : un fichier de log qui set sauvegarder les données reçues et le temps d’attentes calculé.
Bus_horaires : vairiable de type liste
X_pos : un entier qui représente la position du bus dans l’interface graphique par rapport à l’axe X.
Y_pos : un entier qui représente la position du bus dans l’interface graphique par rapport à l’axe Y.
setPosition() : une méthode qui sert à initialiser la position du bus.
getPosition() : une méthode qui sert à récupérer la position du bus.
sendPosition() : une méthode qui sert à envoyer la position du bus au cloud.
setTemperature() : une méthode qui sert à initialiser la température du bus.
getTemperature() : une méthode qui sert à récupérer la température du bus.
sendTemperature() : une méthode qui sert à envoyer la température du bus au cloud.

#### Génération de vitesse aléatoire

Les bus avancent d’un seul pixel chaque t = time.sleep(uniform(T_MIN, T_MAX)).

#### Utilisation des Thread

Dans notre application, nous avons utilisé Les ``threads'' qui sont des unités d'exécution
autonomes qui peuvent effectuer des tâches, en parallèle avec d'autres threads, comme
pour l’affichage de chaque bus sur l’interface graphique, et l’envoie de données, et les

### calculs faits par chaque station.

thread_bus_1 = Thread(target=running_bus_1, args=(bus_1, False))
thread_bus_1.start()
thread_send_data = Thread(target=send_data, args=(bus_1, bus_2, bus_3))
thread_send_data.start()

## Apprentissage automatique

#### Prétraitement

Dans un premier temps nous avons collecté les donnes dans un fichier log activity.log qui contient un
journal d’activité de notre application sous forme de donnée séparé par des --
02/01/18- 20:16:36 -- 2018 -- 131 -- 80 -- {'2019': 1000.0, '2018': 1000.0, '2020': 1000.0}.
Puis nous avons supprimé les lignes dupliquées et générer un fichier train.txt, par la fonction
delete_duplicate().
la fonction text_to_csv() nous a permis de sélectionner toutes les données(lignes) qui
correspondent au bus 2018 et générer un fichier au format csv train.csv qui sera utilisé dans la
prédiction du temps d’attente du bus.
id_bus x_position, y_position wainting_time
2018 141 80 74.

#### Prédiction

Concernant la partie prédiction nous avons implémenté une fonction predict() qui applique la
régression bayésienne pour prédire le temps d'attente du bus 2018.
Le résultat est représenté sous format d’un graphe ci-dessous.


![comparaison des temps d’attente réel, prédis](https://github.com/fr33dz/IoT_bus/blob/master/images/Figure_2.png)



## Référence

[http://www.digitaldimension.solutions/blog/avis-d-experts/2015/02/mqtt-un-protocole-dedie-pour-liot/](http://www.digitaldimension.solutions/blog/avis-d-experts/2015/02/mqtt-un-protocole-dedie-pour-liot/)
[http://www.github.com/ibm-watson-iot/iot-python](http://www.github.com/ibm-watson-iot/iot-python)
https://console.bluemix.net/docs/services/IoT/applications/libraries/python.html#python
https://console.bluemix.net/docs/services/IoT/reference/mqtt/index.html#ref-mqtt
https://winpython.github.io
[http://scikit-learn.org/stable/](http://scikit-learn.org/stable/)
[http://scikit-learn.org/stable/modules/linear_model.html#bayesian-regression](http://scikit-learn.org/stable/modules/linear_model.html#bayesian-regression)

## Captures d'ecran

![screen 1 ](https://github.com/fr33dz/IoT_bus/blob/master/images/gui_1.png)
![screen 2 ](https://github.com/fr33dz/IoT_bus/blob/master/images/gui_2.png)
![screen 3 ](https://github.com/fr33dz/IoT_bus/blob/master/images/gui_3.png)