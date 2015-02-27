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
Una HTTP response es lo que responde el servidor cuando recibe y procesa una HTTP request.
El servidor, mediante la HTTP response, indica el resultado de la request:
* Si ha habido un error al procesarla.
* Si se ha procesado bien.
* También puede incluir un body, es decir, una respuesta hacia el cliente.

Una response contiene:
* Status_code: 100...599 que indica el resultado de la petición.
Los más importantes son:
  * 200: significa que la petición ha sido procesada correctamente.
  * 201: significa que la petición ha sido procesada correctamente y una entidad ha sido creada.
Por ejemplo, una compra.
  * 400: es un error, bad request. Significa que el body de la request es incorrecto porque faltan
campos que son obligatorios o hay campos con nombres no reconocidos por el servidor o el formato
del valor de un campo es incorrecto. Por ejemplo, debería ser un int y es un string. 
  * 404: not found. La URL a la cual he enviado la request no existe. Por ejemplo /compras/messi
 no existe.
  * 405: method not allowed. El method especificado en HTTP request no está permitido para la URL
especificada. 
  * 500: Internal server error. El servidor ha sufrido una excepción al procesar la petición. 
  * 503: Service unavailable. El servidor web está down. 
* Cabeceras: Como por ejemplo Set-Cookie, Content-Type, etc.
* Body: Contiene la respuesta. Por ejemplo, si haces una request GET /compras, el body de la 
response contiene esa lista de compras.

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

### Cookies
Una cookie es un valor(sessionid=12345) el cual el servidor, envía al cliente en la cabecera 
Set-Cookie de una HTTP Response. El navegador se guarda esta cookie al recibirla. El navegador está
obligado a enviar esa cookie en las siguientes HTTP requests que le envía a este servidor. 
El navegador envía la cookie en una cabecera de la HTTP request.

### Web Server
Un servidor web es un ordenador el cual está escuchando peticiones HTTP en un puerto determinado,
usualmente el 80. 

### Server-side technologies
Cuando un programador quiere programar un web server, tiene que escoger una server side technology.
¿Que tecnología/framework/lenguaje quiero usar para programar mi web server? Puedo usar java servlets, 
PHP, ruby on rails, nodeJS, Python, django. Cada tecnología tiene sus ventajas y sus desventajas. 
Programar un web server consiste en definir los endpoints de mi web server. Por ejemplo:
* Una petición a POST /compras requiere los campos obligatorios producto, precio, etc. en formato json.
  * Si algún campo obligatorio no es parte de la petición, devolveré un error 400. 
  * Si el body de la request no está en json, y json es el único formato que yo acepto, devolveré
un error 406. 
  * Si el body de la request es válido, crearé una nueva compra, la guardaré en mi base de datos y 
devolveré en la response el identificador de la compra que acabo de crear.

### Browser-Side technologies

#### HTML
HTML es un lenguaje de etiquetas. Un navegador sabe interpretar y renderizar HTML.
Con HTML podemos definir párrafos, tablas, cabeceras, imagenes, links, etc.

Un servidor web puede retornar HTML dentro de una HTTP response. El navegador renderizará este HTML.

#### CSS
Otro tipo de ficheros que un servidor web retorna al navegador. Es un lenguaje que sirve para
especificar el formato y aspecto visual de los elementos que forman un documento HTML.

#### JavaScript
Es otro tipo de ficheros que un servidor web retorna. JavaScript es una lenguaje de programación 
que los navegadores saben interpretar y ejecutar. Es código que se ejecuta en el navegador y 
no en el servidor web. Sirve para:
* Validación de formularios en la parte del navegador.
* Enviar peticiones HTTP a un servidor web para actualizar una parte de la página web.
* En general, sirve para ofrecer una user experience más moderna y dinámica.

#### AJAX
Asynchronous JavaScript And XML. Es una técnica que permite a un código JavaScript que se está
ejecutando en el navegador enviar peticiones HTTP a un servidor web.

Un navegador envía peticiones HTTP en dos principales casos:
* El más común es cuando el usuario escribe en la caja de texto del navegador una URL a la cual
quiere acceder. Al pulsar Enter el navegador envía una petición GET a esa URL. El servidor web,
normalmente, responde con un HTML el cual, dentro de su `head` tag hace referencia a ficheros CSS
y JavaScript.
```
<html>
  <head>
    <link rel="stylesheet" type="text/css" href="mystyle.css">
    <script src="script.js" type="text/javascript"></script>
  </head>
  <body>

  </body>
</html>
```
Estos son los pasos:
1. Usuario escribe mywebsite.com en la caja de texto del navegador y pulsa enter.
2. El navegador envia una peticion GET mywebsite.com
3. El servidor web recibe esta peticion.
4. El servidor envia una HTTP response que contiene el fichero index.html (un fichero como el del
ejemplo de arriba).
5. El navegador lee el index.html y se da cuenta de que hace referencia a dos ficheros: mystyle.css y
script.js.
6. Automaticamente, el navegador envia una HTTP request GET mywebsite.com/mystyle.css.
7. El servidor contesta con una HTTP response que contiene el fichero mystyle.css
8. El navegador interpreta mystyle.css y se lo guarda para saber como mostrar cada uno de los elementos
HTML.
9. Ahora el navegador envia otra HTTP request GET mywebsite.com/script.js para obtener el fichero JS
referenciado en index.html.
10. El servidor contesta con una HTTP response que contiene el fichero script.js
11. El navegador recibe esa response y se guarda el fichero script.js.

Estas tres HTTP requests que el navegador ha hecho estaban pidiendo contenido estatico. Es decir,
piden ficheros de texto (html, css, js) que el servidor web tiene guardados en disco. El servidor web
no tiene nada mas que coger esos ficheros y devolverlos. Se le llama servir contenido estatico.

* El otro tipo de peticiones HTTP más común son las peticiones dinámicas hechas por un JS script.
Por ejemplo:
  * cuando desde la página de Twitter, escribes un nuevo tweet en la caja de texto y haces
click en el botón de Enviar tweet, hay un código JS que captura ese click y entonces envía una HTTP
request POST al servidor de twitter para publicar este nuevo tweet.
Este segundo tipo de peticiones son peticiones AJAX.

#### HTML5































