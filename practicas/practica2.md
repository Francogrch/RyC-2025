# Práctica 2: Capa de Aplicación - HTTP

## 1. ¿Cuál es la función de la capa de aplicación?

La capa de aplicación es donde **residen las aplicaciones de red y sus protocolos de nivel de aplicación**. Su función principal es **proporcionar servicios de comunicación directamente a los procesos de aplicación** que se ejecutan en diferentes _hosts_. Desde la perspectiva del desarrollador, el desarrollo de una aplicación de red implica **escribir programas que se ejecuten en distintos sistemas terminales y que se comuniquen entre sí a través de la red**.

Esta capa define cómo los procesos de una aplicación, ejecutándose en diferentes sistemas terminales, se pasan los mensajes entre sí. Específicamente, un protocolo de la capa de aplicación define:

- Los tipos de mensajes intercambiados (por ejemplo, mensajes de solicitud y respuesta).
- La sintaxis de estos mensajes (campos y delimitación).
- La semántica de los campos (significado de la información).
- Las reglas para cuándo y cómo un proceso envía y responde a los mensajes.

Las aplicaciones de red, como la Web, el correo electrónico o DNS, utilizan los servicios de esta capa para interactuar.

## 2. Si dos procesos deben comunicarse:

### a. ¿Cómo podrían hacerlo si están en diferentes máquinas?

Los procesos de dos sistemas terminales diferentes se comunican entre sí **intercambiando mensajes a través de la red de computadoras**. Un proceso emisor crea y envía mensajes a la red, y un proceso receptor recibe estos mensajes y posiblemente responde. Esta comunicación se realiza a través de una **interfaz _software_ denominada _socket_**. El proceso emisor envía el mensaje a través de su propio _socket_, esperando que una infraestructura de transporte al otro lado del _socket_ lleve el mensaje hasta el _socket_ del proceso de destino. Para identificar al proceso receptor, se especifican **la dirección IP del _host_ de destino y un número de puerto de destino** que identifica el _socket_ específico en ese _host_.

### b. Y si están en la misma máquina, ¿qué alternativas existen?

Cuando los procesos se ejecutan en el mismo sistema terminal, pueden comunicarse entre sí mediante **sistemas de comunicación inter-procesos, aplicando reglas gobernadas por el sistema operativo del sistema terminal**.

## 3. Explique brevemente cómo es el modelo Cliente/Servidor. Dé un ejemplo de un sistema Cliente/Servidor en la “vida cotidiana” y un ejemplo de un sistema informático que siga el modelo Cliente/Servidor. ¿Conoce algún otro modelo de comunicación?

En una **arquitectura cliente-servidor**, existe un _host_ siempre activo, denominado **servidor**, que da servicio a las solicitudes de muchos otros _hosts_, que son los **clientes**. Los clientes no se comunican directamente entre sí, sino solo con el servidor. Una característica clave es que el servidor tiene una **dirección fija y conocida (dirección IP)** y está siempre activo, lo que permite a los clientes contactarlo enviándole paquetes a su dirección IP.

- **Ejemplo en la “vida cotidiana”**: Una analogía adecuada podría ser una **biblioteca**. Los usuarios (clientes) van a la biblioteca (servidor) para solicitar y obtener libros (información o servicios). La biblioteca está siempre disponible, tiene una dirección fija y contiene los recursos. Los usuarios no interactúan directamente entre sí para obtener libros, sino a través de la biblioteca.

- **Ejemplo de sistema informático**: La **Web** es un ejemplo clásico, donde un servidor web siempre activo sirve las solicitudes de los navegadores que se ejecutan en los _hosts_ clientes. Otros ejemplos incluyen **FTP, Telnet y el correo electrónico**, así como motores de búsqueda, sitios de comercio electrónico y redes sociales, que a menudo utilizan grandes **centros de datos** para actuar como servidores virtuales de gran capacidad.

- **Otro modelo de comunicación**: El modelo **P2P (Peer-to-Peer)** es otro paradigma arquitectónico predominante. En este modelo, los _hosts_ conectados de forma intermitente, denominados _pares_ o _peers_, se comunican directamente entre sí, dependiendo mínimamente o en absoluto de una infraestructura de servidores siempre activos. Un ejemplo de aplicación P2P es la **compartición de archivos (como BitTorrent)**. Algunas aplicaciones pueden tener **arquitecturas híbridas** que combinan elementos cliente-servidor y P2P.

## 4. Describa la funcionalidad de la entidad genérica “Agente de usuario” o “User agent”.

El término "**Agente de usuario**" o "**User-agent**" se utiliza en dos contextos principales:

1.  **En HTTP (Web)**: La línea de cabecera `User-agent:` en un mensaje de solicitud HTTP **especifica el tipo de navegador que está haciendo la solicitud al servidor**. Esto es útil porque el servidor puede enviar versiones diferentes del mismo objeto a distintos tipos de agentes de usuario (navegadores), aunque todas las versiones tengan la misma URL. Por ejemplo, `User-agent: Mozilla/5.0` identifica un navegador Firefox.

2.  **En Correo Electrónico**: Los "**agentes de usuario**" permiten a los usuarios **leer, responder, reenviar, guardar y componer mensajes**. Ejemplos incluyen Microsoft Outlook y Apple Mail. Cuando un usuario termina de componer un mensaje, su agente de usuario lo envía a su servidor de correo, y cuando un destinatario quiere leer un mensaje, su agente de usuario lo recupera de su buzón en el servidor de correo.

En resumen, un agente de usuario es el **programa _cliente_ que interactúa directamente con el usuario final**, permitiéndole acceder y manipular los servicios de red.

## 5. ¿Qué son y en qué se diferencian HTML y HTTP?

- **HTML (HyperText Markup Language)**: Es un **estándar para los formatos de documentos**. Se utiliza para **crear objetos o documentos web**, que consisten en archivos como texto, imágenes JPEG, applets Java o clips de vídeo, direccionables mediante una URL. Las páginas web suelen estar compuestas por un archivo base HTML y varios objetos referenciados por URLs dentro de ese archivo.
- **HTTP (HyperText Transfer Protocol)**: Es el **protocolo de la capa de aplicación de la Web**. Define **cómo los clientes web solicitan páginas web a los servidores y cómo estos servidores web transfieren esas páginas a los clientes**. También especifica la **estructura y la secuencia de los mensajes** que se pasan entre el navegador web y el servidor web. HTTP utiliza TCP como su protocolo de transporte subyacente.

**Diferencias:**

- **Naturaleza**: HTML es un **formato de lenguaje de marcado** utilizado para estructurar y presentar contenido en la Web. HTTP es un **protocolo de comunicación** que define las reglas para la transferencia de esos documentos y objetos web entre clientes y servidores.
- **Función**: HTML se encarga de **lo que se muestra** y cómo se organiza el contenido en una página. HTTP se encarga de **cómo se obtiene y se envía ese contenido** a través de la red.
- **Relación**: HTML es un _componente_ de la aplicación Web, mientras que HTTP es el _protocolo de la capa de aplicación_ que permite la existencia de la Web, transfiriendo los documentos HTML y otros objetos.

## 6. HTTP tiene definido un formato de mensaje para los requerimientos y las respuestas. (Ayuda: apartado “Formato de mensaje HTTP”, Kurose).

### a. ¿Qué información de la capa de aplicación nos indica si un mensaje es de requerimiento o de respuesta para HTTP? ¿Cómo está compuesta dicha información? ¿Para qué sirven las cabeceras?

- **Identificación de requerimiento o respuesta**: La **primera línea** del mensaje HTTP es la que indica si es un requerimiento o una respuesta.
  - Para un **mensaje de solicitud (requerimiento)**, esta es la **línea de solicitud**, que consta de tres campos: el **método** (por ejemplo, GET, POST, HEAD, PUT, DELETE), la **URL** del objeto solicitado y la **versión HTTP**.
  - Para un **mensaje de respuesta**, esta es la **línea de estado**, que contiene la **versión del protocolo, un código de estado y un mensaje explicativo del estado** (por ejemplo, "200 OK", "404 Not Found").

- **Función de las cabeceras**: Las líneas de cabecera que siguen a la línea de solicitud o de estado proporcionan **información adicional** sobre el mensaje o el objeto. Sirven para:
  - **Identificación del _host_**: Como `Host:` en solicitudes, que especifica el _host_ donde reside el objeto.
  - **Control de conexión**: Como `Connection: close` o `Connection: keep-alive`.
  - **Información del _cliente_**: Como `User-agent:` para el tipo de navegador, o `Accept-language:` para idiomas preferidos.
  - **Información del _servidor_**: Como `Server:` (tipo de servidor web), `Date:` (fecha de creación de la respuesta), `Last-Modified:` (última modificación del objeto).
  - **Descripción del contenido**: Como `Content-Length:` (tamaño del objeto) y `Content-Type:` (tipo de medio del objeto).
  - **Mecanismos de autenticación y caché**: Las cabeceras son fundamentales para funciones como las _cookies_ y las solicitudes **GET condicionales** con `If-Modified-Since:` para la gestión de cachés.

### b. ¿Cuál es su formato? (Ayuda: https://developer.mozilla.org/es/docs/Web/HTTP/Headers)

El formato general de los mensajes HTTP es el siguiente:

- **Mensaje de solicitud HTTP**:

  ```
  <Línea de solicitud>
  <Líneas de cabecera>
  <Línea en blanco>
  <Cuerpo de entidad (opcional)>
  ```

  La **línea de solicitud** incluye el método, el URL y la versión HTTP (ej: `GET /index.html HTTP/1.1`). El **cuerpo de entidad** suele estar vacío para el método `GET`, pero contiene datos de formulario para el método `POST`.

- **Mensaje de respuesta HTTP**:
  ```
  <Línea de estado>
  <Líneas de cabecera>
  <Línea en blanco>
  <Cuerpo de entidad (con el objeto solicitado)>
  ```
  La **línea de estado** incluye la versión HTTP, un código de estado y una frase explicativa (ej: `HTTP/1.1 200 OK`). El **cuerpo de entidad** contiene el objeto solicitado, como un archivo HTML o una imagen.

### c. Suponga que desea enviar un requerimiento con la versión de HTTP 1.1 desde curl/7.74.0 a un sitio de ejemplo como www.misitio.com para obtener el recurso /index.html. En base a lo indicado, ¿qué información debería enviarse mediante encabezados? Indique cómo quedaría el requerimiento.

Según el formato de mensaje de solicitud HTTP y considerando la información provista, el requerimiento debería incluir:

- **Línea de Solicitud**: Método `GET`, URL `/index.html`, versión `HTTP/1.1`.
- **Cabeceras**:
  - `Host:` para especificar el _host_ `www.misitio.com`.
  - `User-Agent:` para identificar el cliente como `curl/7.74.0`.
  - `Connection: close` para indicar que el cliente desea que el servidor cierre la conexión después de enviar el objeto, aunque HTTP/1.1 utilice conexiones persistentes por defecto, el cliente puede especificar lo contrario.

El requerimiento quedaría así:

```bash
GET /index.html HTTP/1.1
Host: www.misitio.com
User-Agent: curl/7.74.0
Connection: close
(línea en blanco adicional para indicar el final de las cabeceras)
```

## 7. Utilizando la VM, abra una terminal e investigue sobre el comando curl. Analice para qué sirven los siguientes parámetros (-I, -H, -X, -s).

Curl es una herramienta de línea de comandos utilizada para transferir datos desde o hacia un servidor, utilizando varios protocolos, incluido HTTP. A continuación se describen los parámetros mencionados:

- `-I` o `--head`: Este parámetro se utiliza para realizar una solicitud HTTP HEAD. En lugar de descargar el contenido del recurso, solo recupera las cabeceras de la respuesta. Es útil para obtener información sobre el recurso, como su tipo, tamaño y fecha de última modificación, sin descargar el cuerpo del mensaje.

```bash
curl -I www.redes.unlp.edu.ar
HTTP/1.1 200 OK
Date: Wed, 03 Sep 2025 17:18:01 GMT
Server: Apache/2.4.56 (Unix)
Last-Modified: Sun, 19 Mar 2023 19:04:46 GMT
ETag: "1322-5f7457bd64f80"
Accept-Ranges: bytes
Content-Length: 4898
Content-Type: text/html

```

- `-H` o `--header <header>`: Este parámetro permite agregar cabeceras personalizadas a la solicitud HTTP. Puedes especificar cualquier cabecera que desees enviar al servidor, como `User-Agent`, `Accept`, `Authorization`, entre otras. Por ejemplo, `-H "User-Agent: MyCustomAgent"` agrega una cabecera personalizada a la solicitud.

```bash
curl -H "User-Agent: MyCustomAgent" www.redes.unlp.edu.ar
<!DOCTYPE html>
<html>...</heml>
```

- `-X` o `--request <command>`: Este parámetro se utiliza para especificar el método HTTP que deseas utilizar en la solicitud. Por defecto, curl utiliza el método GET, pero con `-X` puedes cambiarlo a otros métodos como POST, PUT, DELETE, etc. Por ejemplo, `-X POST` indica que la solicitud debe ser un POST en lugar de un GET.

```bash
curl -X POST -d "param1=value1&param2=value2" www.redes.unlp.edu.ar
<!DOCTYPE html>
<html>...</html>
```

## 8. Ejecute el comando curl sin ningún parámetro adicional y acceda a www.redes.unlp.edu.ar. Luego responda:

### a. ¿Cuántos requerimientos realizó y qué recibió? Pruebe redirigiendo la salida (>) del comando curl a un archivo con extensión html y abrirlo con un navegador.

Realizó un único requerimiento HTTP GET y recibió el código fuente (el archivo HTML) de la página. A diferencia de un navegador web, que realiza múltiples peticiones para obtener imágenes, hojas de estilo (CSS) y scripts (JavaScript), curl solo descarga el archivo principal que le indicaste.

### b. ¿Cómo funcionan los atributos href de los tags link e img en html?

### c. Para visualizar la página completa con imágenes como en un navegador, ¿alcanza con realizar un único requerimiento?

### d. ¿Cuántos requerimientos serían necesarios para obtener una página que tiene dos CSS, dos Javascript y tres imágenes? Diferencie cómo funcionaría un navegador respecto al comando curl ejecutado previamente.

## 9. Ejecute a continuación los siguientes comandos:

    curl -v -s www.redes.unlp.edu.ar > /dev/null
    curl -I -v -s www.redes.unlp.edu.ar

### a. ¿Qué diferencias nota entre cada uno?

### b. ¿Qué ocurre si en el primer comando se quita la redirección a /dev/null? ¿Por qué no es necesaria en el segundo comando?

### c. ¿Cuántas cabeceras viajaron en el requerimiento? ¿Y en la respuesta?

## 10. ¿Qué indica la cabecera Date?

## 11. En HTTP/1.0, ¿cómo sabe el cliente que ya recibió todo el objeto solicitado de manera completa? ¿Y en HTTP/1.1?

## 12. Investigue los distintos tipos de códigos de retorno de un servidor web y su significado. Considere que los mismos se clasifican en categorías (2XX, 3XX, 4XX, 5XX).

## 13. Utilizando curl, realice un requerimiento con el método HEAD al sitio www.redes.unlp.edu.ar e indique:

### a. ¿Qué información brinda la primera línea de la respuesta?

### b. ¿Cuántos encabezados muestra la respuesta?

### c. ¿Qué servidor web está sirviendo la página?

### d. ¿El acceso a la página solicitada fue exitoso o no?

### e. ¿Cuándo fue la última vez que se modificó la página?

### f. Solicite la página nuevamente con curl usando GET, pero esta vez indique que quiere obtenerla sólo si la misma fue modificada en una fecha posterior a la que efectivamente fue modificada. ¿Cómo lo hace? ¿Qué resultado obtuvo? ¿Puede explicar para qué sirve?

## 14. Utilizando curl, acceda al sitio www.redes.unlp.edu.ar/restringido/index.php y siga las instrucciones y las pistas que vaya recibiendo hasta obtener la respuesta final. Será de utilidad para resolver este ejercicio poder analizar tanto el contenido de cada página como los encabezados.

## 15. Utilizando la VM, realice las siguientes pruebas:

### a. Ejecute el comando ’curl www.redes.unlp.edu.ar/extras/prueba-http-1-0.txt’ y copie la salida completa (incluyendo los dos saltos de línea del final).

### b. Desde la consola ejecute el comando telnet www.redes.unlp.edu.ar 80 y luego pegue el contenido que tiene almacenado en el portapapeles. ¿Qué ocurre luego de hacerlo?

### c. Repita el proceso anterior, pero copiando la salida del recurso /extras/prueba-http-1-1.txt. Verifique que debería poder pegar varias veces el mismo contenido sin tener que ejecutar el comando telnet nuevamente.

## 16. En base a lo obtenido en el ejercicio anterior, responda:

### a. ¿Qué está haciendo al ejecutar el comando telnet?

### b. ¿Qué método HTTP utilizó? ¿Qué recurso solicitó?

### c. ¿Qué diferencias notó entre los dos casos? ¿Puede explicar por qué?

### d. ¿Cuál de los dos casos le parece más eficiente? Piense en el ejercicio donde analizó la cantidad de requerimientos necesarios para obtener una página con estilos, javascripts e imágenes. El caso elegido, ¿puede traer asociado algún problema?

## 17. En el siguiente ejercicio veremos la diferencia entre los métodos POST y GET. Para ello, será necesario utilizar la VM y la herramienta Wireshark. Antes de iniciar considere:

- Capture los paquetes utilizando la interfaz con IP 172.28.0.1. (Menú “Capture ->Options”. Luego seleccione la interfaz correspondiente y presione Start).
- Para que el analizador de red sólo nos muestre los mensajes del protocolo http introduciremos la cadena ‘http’ (sin las comillas) en la ventana de especificación de filtros de visualización (display-filter). Si no hiciéramos esto veríamos todo el tráfico que es capaz de capturar nuestra placa de red. De los paquetes que son capturados, aquel que esté seleccionado será mostrado en forma detallada en la sección que está justo debajo. Como sólo estamos interesados en http ocultaremos toda la información que no es relevante para esta práctica (Información de trama, Ethernet, IP y TCP). Desplegar la información correspondiente al protocolo HTTP bajo la leyenda “Hypertext Transfer Protocol”.
- Para borrar la cache del navegador, deberá ir al menú “Herramientas->Borrar historial reciente”. Alternativamente puede utilizar Ctrl+F5 en el navegador para forzar la petición HTTP evitando el uso de caché del navegador.
- En caso de querer ver de forma simplificada el contenido de una comunicación http, utilice el botón derecho sobre un paquete HTTP perteneciente al flujo capturado y seleccione la opción Follow TCP Stream.

### a. Abra un navegador e ingrese a la URL: www.redes.unlp.edu.ar e ingrese al link en la sección “Capa de Aplicación” llamado “Métodos HTTP”. En la página mostrada se visualizan dos nuevos links llamados: Método GET y Método POST. Ambos muestran un formulario como el siguiente:

### b. Analice el código HTML

### c. Utilizando el analizador de paquetes Wireshark capture los paquetes enviados y recibidos al presionar el botón Enviar.

### d. ¿Qué diferencias detectó en los mensajes enviados por el cliente?

### e. ¿Observó alguna diferencia en el browser si se utiliza un mensaje u otro?

## 18. Investigue cuál es el principal uso que se le da a las cabeceras Set-Cookie y Cookie en HTTP y qué relación tienen con el funcionamiento del protocolo HTTP.

## 19. ¿Cuál es la diferencia entre un protocolo binario y uno basado en texto? ¿De qué tipo de protocolo se trata HTTP/1.0, HTTP/1.1 y HTTP/2? 20. Responder las siguientes preguntas:

### a. ¿Qué función cumple la cabecera Host en HTTP 1.1? ¿Existía en HTTP 1.0? ¿Qué sucede en HTTP/2? (Ayuda: https://undertow.io/blog/2015/04/27/An-in-depth-overview-of-HTTP2.html para HTTP/2)

### b. En HTTP/1.1, ¿es correcto el siguiente requerimiento?

    GET /index.php HTTP/1.1
    User-Agent: curl/7.54.0

### c. ¿Cómo quedaría en HTTP/2 el siguiente pedido realizado en HTTP/1.1 si se está usando https?

    GET /index.php HTTP/1.1
    Host: www.info.unlp.edu.ar

## Ejercicio de Parcial

    curl -X ?? www.redes.unlp.edu.ar/??

    HEAD /metodos/ HTTP/??
    Host: www.redes.unlp.edu.ar
    User-Agent: curl/7.54.0
    < HTTP/?? 200 OK
    < Server: nginx/1.4.6 (Ubuntu)
    < Date: Wed, 31 Jan 2018 22:22:22 GMT
    < Last-Modified: Sat, 20 Jan 2018 13:02:41 GMT
    < Content-Type: text/html; charset=UTF-8
    < Connection: close

### a. ¿Qué versión de HTTP podría estar utilizando el servidor?

### b. ¿Qué método está utilizando? Dicho método, ¿retorna el recurso completo solicitado?

### c. ¿Cuál es el recurso solicitado?

### d. ¿El método funcionó correctamente?

### e. Si la solicitud hubiera llevado un encabezado que diga:

    If-Modified-Since: Sat, 20 Jan 2018 13:02:41 GMT

¿Cuál habría sido la respuesta del servidor web? ¿Qué habría hecho el navegador en este caso?
