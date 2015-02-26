### HTML
HTML es un lenguaje de etiquetas. Un navegador sabe interpretar y renderizar HTML.
Con HTML podemos definir párrafos, tablas, cabeceras, imagenes, links, etc.
El navegador, por normal general, recibe HTML desde un servidor web. 

### Típica interacción web
1. El usuario hace click en un link a mywebsite.com/index.html.
2. Esto hace que el navegador envie una petición HTTP GET a mywebsite.com/index.html.
3. En algún sitio en internet, mywebsite.com se traduce a una dirección IP.
Mediante esa dirección IP podemos acceder al servidor de mywebsite.com.
4. La petición llega al servidor de mywebsite.com.
5. El servidor se da cuenta que la petición está pidiendo el fichero index.html.
6. El servidor responde a la petición enviando el contenido del fichero index.html
el cual contiene HTML.
7. El navegador recibe la respuesta del servidor.
8. El navegador interpreta el HTML y lo muestra por pantalla. 

### URI (concepto parecido a URL)
Una URI identifica un recurso en un servidor en particular.
Varios ejemplos:

* mywebsite.com/compras/1234 identifica a la compra 1234 que se ha llevado
a cabo en mywebsite.com. 
* mywebsite.com/compras identifica a la lista de compras que se han llevado 
a cabo en mywebsite.com.
* mywebsite.com/compras?ciudad_cliente=barcelona identifica a la lista de compras 
cuyos clientes son de Barcelona.

### HTTP
Es un protocolo que sirve para que un navegador y un servidor web se comuniquen.

En realidad, también se usa para que dos servidores web se comuniquen entre ellos.

En un ejemplo de comunicación HTTP, siempre hay un cliente y un servidor. 
El servidor siempre es un servidor web. El cliente puede ser cualquier cosa: 
un navegador web, un servidor web, una aplicación de móvil, un programa de escritorio, etc.

El cliente empieza la comunicación siempre. El cliente envía una HTTP Request o
una petición HTTP. El servidor la recibe, la procesa y genera una respuesta, también
llamada HTTP Response. Esa respuesta le llega al cliente y el cliente hace lo que quiera
con ella. 

Lista de ejemplos de comunicación HTTP:
* Cuando desde la web de Twitter envío un tweet, mi navegador está enviando una petición
HTTP al servidor de Twitter. 
* Desde mi móvil abro una conversación de Whatsapp, la aplicación whatsapp le envía una
petición al servidor de Whatsapp para obtener la lista de mensajes de esa conversación.  

### HTTP Request
Un cliente HTTP envía HTTP Requests. Una Request contiene:
* HTTP method 
  * GET: sirve para obtener información de un servidor. El cliente no envía nada de información
en una GET request. Por ejemplo, GET /compras/1234, serviría para pedirle al servidor que
me devuelva la información de la compra 1234. Una GET request no tiene body.  
  * POST: sirve para que el cliente le envíe información al servidor. Una POST request tiene
un body, el cual contiene la información que el cliente envía al servidor.  Por ejemplo, 
POST /compras serviría para crear una nueva compra. El body podría ser: 
```
{
  producto: "iphone",
  precio: 300,
  moneda: "euro",
  cliente: {
    nombre: "Laura",
    ciudad: "Barcelona",
    direccion: "Diagonal"
  }
}
```
  * PUT: actualizar un recurso que ya existe con un nuevo body. 
  * DELETE: sirve para borrar un recurso. Raramente utilizado.
* URI (/compras/1234)
* host (mywebsite.com)
* cabeceras HTTP: 
  * Accept: especifica el formato de respuesta que el cliente espera (html, xml, plain, json)
  * Content-type: usada únicamente por POST y PUT requests. Indica el formato de la información
que el cliente le envía al servidor dentro de esta petición (json, html). 

### HTTP Response 



### API
Significa Abstract Public Interface. Es una interfaz pública definida por un componente. Ese
componente puede ser un servidor web, una clase java, un módulo PHP, etc. Un componente
define una interfaz pública (API) para que sus clientes se comuniquen con dicho componente. 
Por ejemplo:
* La API del servidor web de Twitter, https://dev.twitter.com/rest/public, define como un cliente
se tiene que comunicar con el servidor de Twitter. Esa API define los endpoints (POST /media/upload, 
GET /statuses/user_timeline) y define conceptualmente para que sirve cada endpoint. 
* Una clase java llamada PurchaseManager.java también define una API la cual tiene que ser
utilizada por otras clases java que quieran hablar con PurchaseManager. Por ejemplo, PurchaseManager
puede definir funciones públicas como nuevaCompra, getCompra, updateCompra, getCompras. 
La API de una clase java es la lista de funciones públicas de esa clase. 

Un servidor web es responsable de definir y publicar su API. Un cliente es responsable de conocer y entender
la API del servidor con el cual quiere hablar. 










