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

1. Click en boton de juego
cuando se clicka en un juego se subscribe a los mensajes y a las puntuaciones de ese juego en particular lineas 20-30 de client.js
para que se muestre el juego cada juego tiene
el chat se carga desde la template chat lineas 38-47 de index.html los mensajes se cargan desde la template messages lineas 67-78 de index.html para mostrar los mensajes del chat hay dos funciones dependiendo de si estamos o no en un juego, sino estamos en ningun juego sacamos los 10 ultimos mensajes y si no sacamos los 10 ultimos mensajes que se han escrito en el juego lineas 145-154 de client.js para filtrar por juego y para mostrar los mensajes nos hemos subscrito a las actualizaciones de ese juego (o none si no estamos en un juego) y desde el servidor se buscan los mensajes lineas 26-32 de server.js
análogo sería para las puntuaciones aunque evidentemente las lineas de código en el index.html serían 91-109 en el client.js lineas 133-1444 serían server.js líneas 10-23
se muestra tambien el juego lineas 112-130 de client.js donde se esconden las demás partes y solo se muestra 

2. Se escribe mensaje chat sin estar autenticado
cuando se escribe un mensaje y de da al enter entonces en client.js lineas 84-105 donde tenemos el código que maneja los mensajes del chat se ejecuta. vemos que si damos al enter (13 en ASCII) entonces si no estamos autenticados entonces entramos en la linea 100 y mostramos un mensaje de error porque no esta autenticado
3. estando autenticado
cuando se escribe un mensaje y de da al enter entonces en client.js lineas 84-105 donde tenemos el código que maneja los mensajes del chat se ejecuta. vemos que si damos al enter (13 en ASCII) entonces si estamos autenticados saltamos a la siguiente línea porque el user._id no es nulo entonces comprobamos si el mensaje es distinto de ' ' para que no sea un string vacío entonces se guarda en la base de datos de messages el user-id (para despues poder identificar al usuario a traves de su id), el mensaje (a traves de message.val que nos da el contenido del imput que hemos puesto), el game-id (para depues poder identificar al juego buscandolo por su id) y la fecha (para después poder elegir los ultimos a traves de la fecha de envio del mensaje) y depues volvemos poner vacío el input (messsage.val(' '))
4. se termina partida con puntuacion sin estar autenticado
linea 46-57 de server.js cuando un juego termina si el usuario esta autenticado entonces entra en el if porque userid no es null y entonces se inserta en matches que donde se guardan las puntuaciones el id del usuario para despues poder identificarlo, la hora a la que se ha finalizado el juego por si hay varios jugadores que han obtenido la misma puntuacion mostrarla en orden de tiempo, la puntuacion obtenida para despues mostrarla y el id del juego para despues saber a que juego pertenece
5. sin estar autenticado
seria igual que el cuatro lo que pasa que no entra en el if y entonces no se guarda la puntuacion
6. que sale en la consola cuando te autenticas sign in:
"current user: null" 
"current user: ubR2Lo3deoRpaJBjX" 
7. cuando sales sign out:
"current user: ubR2Lo3deoRpaJBjX" 
"current user: null" 
sirve tanto para la pregunta 6 y 7
las lineas son en client.js desde la 56 a la 61 
var currentUser = null;
Deps.autorun(function(){
    console.log("current user: " + currentUser);
    currentUser = Meteor.userId();
    console.log("current user: " + currentUser);
});





