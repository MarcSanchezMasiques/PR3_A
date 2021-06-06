# Pr3A: Procedimiento
Comenzaremos haciendo un include de dos librerías, siendo la primera``` #include <WiFi.h&gt; ```
haremos uso de esta para que nuestra placa pueda conectarse a internet. La segunda librería ```#include <WebServer.h&gt; ``` Esta será para hacer un servidor web. Seguimos poniendo en una variable char el nombre(SSID) y contraseña de nuestro WIFI
```
const char* ssid = "Casa-Repetidor";
const char* password = "22052001m";
```
Dentro del void setup() primero imprimimos por pantalla:
Try Connecting to:
Casa-Repetidor
Lo hacemos utilizando el siguiente código:
```
Serial.println("Try Connecting to ");
Serial.println(ssid);
```
Despues conectamos el mòdem WiFi a la placa con:
WiFi.begin(ssid, password);
Una vez hecho esto debemos comprobar si el WiFi está conectado a la red WiFi, lo hacemos con el
código:
```
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.print(".");
}
```
El bucle comprueba la conexion y si es correcta imprime un punto por pantalla.
Seguimos el proceso imprimiendo por pantalla "WIFI connected successfully" y la ip del ESP32.
```
Serial.println("");
Serial.println("WiFi connected successfully");
Serial.print("Got IP: ");
Serial.println(WiFi.localIP());
```
Y para finalizar el void setup() empezamos el servidor HTTP con:
```
server.begin();
Serial.println("HTTP server started");
delay(100);
```
En este loop debemos utilizar la funcion hadleclient() para recibir peticiones de clientes para devolver las funciones del ruteo.

```
void loop() {
server.handleClient();
}
```
Por ultimo, creamos un string HTML para mostrar el texto que entrara dentro del servidor web creado en nuestro caso se mostrara: Hello World, im using ESP32.
```
String HTML = "<!DOCTYPE html&gt;\
<html&gt;\
<body&gt;\
<h1&gt;My Primera Pagina con ESP32 - Station Mode &#128522;</h1&gt;\
body&gt;\
html&gt;";
```
Creamos la función void handle_root() . Dentro de hand_root llamamos a la funcion .send, la cual recibe 3 parametros:

- Código de respuesta (300, 404, 121, 301...)
- Un tipo de contenido HTTP (text/plain, text/html, text/json, image/png...)
- Contenido del cuerpo de la respuesta(string HTML en este programa)
```
void handle_root() {
server.send(200, "text/html", HTML);
}
```

### Resultados de la simulación
En esta simulación podemos ver como la placa se conecta correcta al wifi Casa_Repetidor, de esta manera, podremos entrar através de la IP en el buscador y ver el mensaje impreso, siendo este Hello World, im using ESP32 como titulo.

### Ultimo apartado
Por ultimo imprimimos el readme.md através de la IP y de la conexión web, de esta manera, podremos ver todo el README.md en esta pagina.
