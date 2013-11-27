Plataphorma
===========

Meteor pet project created to teach my students the following Meteor functionality: 

* Collection's publish/subscribe 
* Deps.autorun 
* Meteor.methods/call 
* Integration of non-Meteor code in compatibility folder (HTML5 games Alien Invasion and Froot Wars)
* Usage of allow to control client access to collections

![ScreenShot](/screenshot.png)


Plataphorma offers the possibility to run 2 different HTML5 games: Alien Invasion and Froot Wars. 

On the right side of the screen the best players of each game are shown, updated in real time each time a signed in player finishes a game. If no game is selected, the best players overall are shown.

On the left side of the screen a chatroom for the current game is available. Only signed in users can post messages. If no game is selected a general chatroom is shown.

The original code of the two HTML5 games integrated in this project is available here:
* Alien Invasion: https://github.com/cykod/AlienInvasion
* Froot Wars: http://www.wrox.com/WileyCDA/WroxTitle/Professional-HTML5-Mobile-Game-Development.productCd-1118301323,descCd-DOWNLOAD.html

Bootstrap style (file bootstrap.min.css) provided by http://bootswatch.com


Running the project
-------------------

A live version of this code is running here: http://plataphorma.meteor.com

To run the project locally, clone the repo and run ```meteor``` inside it. You can see in .meteor/packages that this Meteor project uses these packages:
* ```meteor remove autopublish```
* ```meteor remove insecure```
* ```meteor add bootstrap```
* ```meteor add accounts-ui```
* ```meteor add accounts-password```



Respuesta a Preguntas
---------------------

1) Click en boton de juego.
En la linea 81 del index.html se define una plantilla que contiene botones con ids iguales a los nombres de los juegos. A dicha plantilla se le asocia un evento de click, de forma que cada boton tiene asociado una funcion que se ejecutará cuando hagas click en dicho boton. En esa funcion,se busca en la coleccion Games, definida en el model.js, la id del boton que se ha hecho click, que coincide con la del juego en si, y se asigna el contenido a la variable game, y despues se establece la variable Session con la etiqueta "Current_ game" con valor el campo id de la variable game. Al contener Session datos reactivos, pasamos a Deps.autorun en la linea 20 del client.js, una funcion que dependa de Session para que se autoejecute al modificarse dichos datos. Como se han modificado al hacer click en el boton del juego, se ejecuta la funcion que hace que se obtenga el nombre del juego contenido en la etiqueta "Current_ game" como valor, y se asigne a la variable current_game. 

2) Se escribe mensaje chat sin estar autenticado.
En la linea 84 del client.js se asocia un evento de entrada a una plantilla id input definida en la linea 56 del index.html. Al pulsar intro, el evento comprobara que existe Meteor.userId(), objeto que contendrá los datos del usuario autenticado. Al no encontrarlo por no estar autenticado, hace que muestre un mensaje con el contenido del div con id igual a login-error, que te informa de que te autentiques para escribir.

3) Se escribe mensaje chat estando autenticado.
Ahora si se econtrara el objeto que contiene tus datos, y sacará de él nombre de usuario y el mensaje que has escrito que se encuentra en la variable con id igual message. Ademas lo insertará en la coleccion Messages, previamente definida en models.js con los campos, nombre de usuario, mensaje, fecha, y juego al que pertenecia el chat. Despues la variable message se inicializa otra vez a ''.

4)
