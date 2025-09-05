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

  GET /index.html HTTP/1.1
  Host: www.misitio.com
  User-Agent: curl/7.74.0
  Connection: close

  (cuerpo de entidad, vacio para el metodo GET)
  ```

  La **línea de solicitud** incluye el método, el URL y la versión HTTP (ej: `GET /index.html HTTP/1.1`). El **cuerpo de entidad** suele estar vacío para el método `GET`, pero contiene datos de formulario para el método `POST`.

- **Mensaje de respuesta HTTP**:

  ```
  <Línea de estado>
  <Líneas de cabecera>
  <Línea en blanco>
  <Cuerpo de entidad (con el objeto solicitado)>

  HTTP/1.1 200 OK
  Date: Wed, 03 Sep 2025 17:18:01 GMT
  Server: Apache/2.4.56 (Unix)
  Last-Modified: Sun, 19 Mar 2023 19:04:46 GMT
  ETag: "1322-5f7457bd64f80"
  Accept-Ranges: bytes
  Content-Length: 4898
  Content-Type: text/html

  <html>...</html>
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

**Tal como indicas**, el comando `curl` sin parámetros adicionales realiza **un único requerimiento HTTP GET** al servidor `www.redes.unlp.edu.ar` y **recibe como respuesta el código fuente del archivo HTML principal** de la página solicitada.

Cuando rediriges la salida de `curl` a un archivo `.html` y lo abres con un navegador, el navegador solo muestra el texto y la estructura del HTML, pero no descarga ni muestra las imágenes, hojas de estilo (CSS) o scripts (JavaScript) referenciados. Esto se debe a que `curl` actúa como un **cliente HTTP básico** que solo busca el objeto especificado en la URL, mientras que un navegador web es un cliente HTTP completo que, al analizar el archivo HTML recibido, identifica y solicita de forma independiente todos los objetos referenciados.

### b. ¿Cómo funcionan los atributos href de los tags link e img en html?

En HTML, los atributos `href` (en el caso de las etiquetas `<link>`, por ejemplo, para hojas de estilo) y `src` (en el caso de las etiquetas `<img>` para imágenes) funcionan como **referencias a las URL de otros objetos** que forman parte de la página web.

Cuando un navegador web recibe un archivo HTML base, lo **analiza para encontrar estas referencias** a otros objetos (como imágenes JPEG, applets Java, hojas de estilo o clips de vídeo). Cada una de estas URL indica la ubicación del objeto, compuesta por el nombre de host del servidor que lo aloja y la ruta al objeto dentro de ese servidor.

El navegador utiliza esta información para **enviar mensajes de solicitud HTTP adicionales al servidor** para cada uno de los objetos referenciados, a fin de poder presentarlos en la página. Este proceso demuestra que una página web no es un único archivo, sino una colección de objetos distintos.

### c. Para visualizar la página completa con imágenes como en un navegador, ¿alcanza con realizar un único requerimiento?

**No, no es suficiente con realizar un único requerimiento HTTP GET** para visualizar una página web completa con sus imágenes, hojas de estilo y scripts, tal como lo haría un navegador.

### d. ¿Cuántos requerimientos serían necesarios para obtener una página que tiene dos CSS, dos Javascript y tres imágenes? Diferencie cómo funcionaría un navegador respecto al comando curl ejecutado previamente.

Para una página web que contiene dos archivos CSS, dos archivos JavaScript y tres imágenes, el número de requerimientos HTTP sería el siguiente:

- **Para el comando `curl` (ejecutado previamente):**
  - Se realizaría **1 requerimiento HTTP GET**.
  - `curl` solo descarga el archivo HTML principal de la URL especificada, **sin procesar las referencias a otros objetos** incrustados. Por lo tanto, no realizaría peticiones adicionales para los archivos CSS, JavaScript o las imágenes.

- **Para un navegador web:**
  - Se realizarían un total de **8 requerimientos HTTP GET**:
    - 1 requerimiento para el archivo HTML principal.
    - 2 requerimientos para los dos archivos CSS referenciados.
    - 2 requerimientos para los dos archivos JavaScript referenciados.
    - 3 requerimientos para las tres imágenes referenciadas.

La diferencia clave radica en que el **navegador web actúa como un cliente HTTP completo** que **analiza el archivo HTML recibido** y, al encontrar las URL de los objetos referenciados, **inicia de forma autónoma nuevas solicitudes HTTP** para obtener cada uno de ellos. Por el contrario, el comando `curl` se comporta como un **cliente HTTP simplificado** que solo recupera el recurso directamente indicado por la URL en la línea de comandos y no realiza un análisis posterior del contenido para descargar recursos vinculados.

## 9. Ejecute a continuación los siguientes comandos:

    curl -v -s www.redes.unlp.edu.ar > /dev/null
    curl -I -v -s www.redes.unlp.edu.ar

### a. ¿Qué diferencias nota entre cada uno?

El primer comando `curl -v -s www.redes.unlp.edu.ar > /dev/null` realiza una solicitud HTTP GET al servidor `www.redes.unlp.edu.ar` y redirige la salida estándar a `/dev/null`, lo que significa que no verás el contenido del cuerpo de la respuesta. Sin embargo, debido a la opción `-v` (verbose), verás en la salida estándar los detalles de la conexión, incluyendo las cabeceras de solicitud y respuesta, así como información sobre la conexión TCP.
El segundo comando `curl -I -v -s www.redes.unlp.edu.ar` realiza una solicitud HTTP HEAD al mismo servidor. La opción `-I` indica que solo se envian las cabeceras de la respuesta, sin el cuerpo del mensaje. Al igual que en el primer comando, la opción `-v` proporciona detalles de la conexión y las cabeceras.

### b. ¿Qué ocurre si en el primer comando se quita la redirección a /dev/null? ¿Por qué no es necesaria en el segundo comando?

Si le quitas la redireccion vas a obtener el contenido completo, incluyendo el body del mensaje. En el segundo comando no es necesario ya que al utilizar el metodo HEAD no se obtiene el body del mensaje.

### c. ¿Cuántas cabeceras viajaron en el requerimiento? ¿Y en la respuesta?

En el primer comando, el numero de cabeceras son 3 en el requerimiento y 8 en la respuesta, mientras que en el segundo comando fueron 3 en el requerimiento y 8 en la respuesta.

## 10. ¿Qué indica la cabecera Date?

La cabecera `Date` en una respuesta HTTP indica la **fecha y hora en que el mensaje fue generado por el servidor**. Esta información es útil para que el cliente pueda conocer cuándo se creó la respuesta, lo que puede ser relevante para la gestión de cachés y para sincronizar la información entre el cliente y el servidor. La fecha y hora están en formato GMT (Greenwich Mean Time) y siguen el estándar definido por RFC 7231.

## 11. En HTTP/1.0, ¿cómo sabe el cliente que ya recibió todo el objeto solicitado de manera completa? ¿Y en HTTP/1.1?

Para determinar cuándo un cliente ha recibido completamente el objeto solicitado en HTTP, existen diferencias clave entre HTTP/1.0 y HTTP/1.1, principalmente relacionadas con el manejo de las conexiones TCP y las cabeceras de los mensajes.

- **En HTTP/1.0 (conexiones no persistentes):**
  En HTTP/1.0, las conexiones suelen ser **no persistentes**. Esto significa que se establece una conexión TCP separada para cada solicitud y respuesta de un objeto.
  El cliente sabe que ha recibido el objeto completo porque el **servidor cierra la conexión TCP** una vez que ha terminado de enviar el objeto solicitado. La conexión no se mantiene (no persiste) para otros objetos. Cada conexión TCP transporta exactamente un mensaje de solicitud y un mensaje de respuesta.

- **En HTTP/1.1 (conexiones persistentes):**
  HTTP/1.1 utiliza **conexiones persistentes por defecto**. Con las conexiones persistentes, el servidor deja la conexión TCP abierta después de enviar una respuesta, permitiendo que subsiguientes solicitudes y respuestas entre el mismo cliente y servidor se envíen a través de la misma conexión. Esto implica que el cierre de la conexión TCP ya no puede ser el mecanismo para señalar el fin de un objeto individual.
  En su lugar, el cliente de HTTP/1.1 determina que ha recibido el objeto completo mediante la **cabecera `Content-Length`** incluida en el mensaje de respuesta HTTP. Esta cabecera especifica el número de bytes del objeto que está siendo enviado. El cliente lee exactamente esa cantidad de bytes y, al hacerlo, sabe que ha recibido el objeto en su totalidad.
  Es importante notar que, aunque HTTP/1.1 usa conexiones persistentes por defecto, un cliente puede solicitar explícitamente una conexión no persistente incluyendo la cabecera `Connection: close` en su mensaje de solicitud. En ese caso, el comportamiento sería similar al de HTTP/1.0, donde el cierre de la conexión TCP indicaría el final del objeto.

## 12. Investigue los distintos tipos de códigos de retorno de un servidor web y su significado. Considere que los mismos se clasifican en categorías (2XX, 3XX, 4XX, 5XX).

Los códigos de estado se clasifican en categorías según su primer dígito:

- **Códigos 2XX: Respuestas satisfactorias**
  - Estos códigos indican que la acción solicitada por el cliente ha sido **recibida, comprendida y aceptada con éxito**.
  - **Ejemplo:** `200 OK`
    - Este código, como se ve en un mensaje de respuesta HTTP típico, significa que "todo es correcto; es decir, que el servidor ha encontrado y está enviando el objeto solicitado".

- **Códigos 3XX: Redirecciones**
  - Estos códigos informan al cliente que la solicitud requiere de una **acción adicional** para completarse, generalmente una redirección a otra ubicación.
  - **Ejemplo:** `301 Moved Permanently`
    - Significa que "el objeto solicitado ha sido movido de forma permanente; el nuevo URL se especifica en la línea de cabecera `Location:` del mensaje de respuesta. El software cliente recuperará automáticamente el nuevo URL".

- **Códigos 4XX: Errores del cliente**
  - Estos códigos indican que ha habido un error por parte del **cliente** al realizar la solicitud.
  - **Ejemplo:** `400 Bad Request`
    - Es "un código de error genérico que indica que la solicitud no ha sido comprendida por el servidor".
  - **Ejemplo:** `404 Not Found`
    - Indica que "el documento solicitado no existe en este servidor".

- **Códigos 5XX: Errores del servidor**
  - Estos códigos señalan que el **servidor falló** al cumplir una solicitud aparentemente válida.
  - **Ejemplo:** `505 HTTP Version Not Supported`
    - Indica que "la versión de protocolo HTTP solicitada no es soportada por el servidor".

[Mas codigos de respuestas](https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status)

## 13. Utilizando curl, realice un requerimiento con el método HEAD al sitio www.redes.unlp.edu.ar e indique:

```bash
curl -I www.redes.unlp.edu.ar
HTTP/1.1 200 OK
Date: Thu, 04 Sep 2025 12:00:51 GMT
Server: Apache/2.4.53 (Unix)
Last-Modified: Wed, 13 Apr 2022 22:55:32 GMT
ETag: "1322-5dc9113140100"
Accept-Ranges: bytes
Content-Length: 4898
Content-Type: text/html
```

### a. ¿Qué información brinda la primera línea de la respuesta?

_HTTP/1.1 200 OK_ - La respuesta fue exitosa y que la version de HTTP es 1.1

### b. ¿Cuántos encabezados muestra la respuesta?

Muestra 8 encabezados.

### c. ¿Qué servidor web está sirviendo la página?

Un servidor Apache/2.4.53 (Unix).

### d. ¿El acceso a la página solicitada fue exitoso o no?

Sí, fue exitoso. El código de estado es 200 OK.

### e. ¿Cuándo fue la última vez que se modificó la página?

La última vez que se modificó la página fue el Wed, 13 Apr 2022 22:55:32 GMT.

### f. Solicite la página nuevamente con curl usando GET, pero esta vez indique que quiere obtenerla sólo si la misma fue modificada en una fecha posterior a la que efectivamente fue modificada. ¿Cómo lo hace? ¿Qué resultado obtuvo? ¿Puede explicar para qué sirve?

```bash
curl -H "If-Modified-Since: Wed, 13 Apr 2022 23:55:32 GMT" -I www.redes.unlp.edu.ar
HTTP/1.1 304 Not Modified
Date: Thu, 04 Sep 2025 12:18:35 GMT
Server: Apache/2.4.53 (Unix)
Last-Modified: Wed, 13 Apr 2022 22:55:32 GMT
ETag: "1322-5dc9113140100"
Accept-Ranges: bytes
```

Para hacerlo agregue una cabecera `If-Modified-Since` con una fecha posterior a la última modificación conocida. El resultado fue un código de estado `304 Not Modified`, lo que indica que el recurso no ha sido modificado desde la fecha especificada. Esto es útil para **optimizar el uso del ancho de banda y mejorar la eficiencia**, ya que evita la transferencia innecesaria de datos si el recurso no ha cambiado.

## 14. Utilizando curl, acceda al sitio www.redes.unlp.edu.ar/restringido/index.php y siga las instrucciones y las pistas que vaya recibiendo hasta obtener la respuesta final. Será de utilidad para resolver este ejercicio poder analizar tanto el contenido de cada página como los encabezados.

```bash

curl www.redes.unlp.edu.ar/restringido/index.php
#<h1>Acceso restringido</h1>
#<p>Para acceder al contenido es necesario autenticarse. Para obtener los datos de acceso seguir las instrucciones detalladas en www.redes.unlp.edu.ar/obtener-usuario.php</p>

curl www.redes.unlp.edu.ar/obtener-usuario.php
#<p>Para obtener el usuario y la contraseña haga un requerimiento a esta página seteando el encabezado 'Usuario-Redes' con el valor 'obtener'</p>

curl -H "Usuario-Redes:obtener" www.redes.unlp.edu.ar/obtener-usuario.php
# <p>Bien hecho! Los datos para ingresar son:
#
#     Usuario: redes
#
#     Contraseña: RYC
#
#     Ahora vuelva a acceder a la página inicial con los datos anteriores.
#
#     PISTA: Investigue el uso del encabezado Authorization para el método Basic. El comando base64 puede ser de ayuda!</p>

echo -n redes:RYC | base64
#cmVkZXM6UllD

curl -H "Authorization: Basic cmVkZXM6UllD" www.redes.unlp.edu.ar/restringido/index.php
# <h1>Excelente!</h1>
#
# <p>Para terminar el ejercicio deberás agregar en la entrega los datos que se muestran en la siguiente página.</p>
# <p>ACLARACIÓN: la URL de la siguiente página está contenida en esta misma respuesta.</p>

curl -H "Authorization: Basic cmVkZXM6UllD" -I www.redes.unlp.edu.ar/restringido/index.php
# HTTP/1.1 302 Found
# Date: Thu, 04 Sep 2025 21:57:05 GMT
# Server: Apache/2.4.56 (Unix)
# X-Powered-By: PHP/7.4.33
# Location: http://www.redes.unlp.edu.ar/restringido/the-end.php
# Content-Type: text/html; charset=UTF-8

curl -H "Authorization: Basic cmVkZXM6UllD" www.redes.unlp.edu.ar/restringido/the-end.php

# ¡Felicitaciones, llegaste al final del ejercicio!
#
# Fecha: 2025-09-04 21:58:13
# Verificación: 3e8e9905d1c4d5018d445c2a31168709eb313ea4f13c5067a477a2435121e187re
```

## 15. Utilizando la VM, realice las siguientes pruebas:

### a. Ejecute el comando ’curl www.redes.unlp.edu.ar/extras/prueba-http-1-0.txt’ y copie la salida completa (incluyendo los dos saltos de línea del final).

```bash
curl www.redes.unlp.edu.ar/extras/prueba-http-1-0.txt
GET /http/HTTP-1.1/ HTTP/1.0
User-Agent: curl/7.38.0
Host: www.redes.unlp.edu.ar
Accept: */*




```

### b. Desde la consola ejecute el comando telnet www.redes.unlp.edu.ar 80 y luego pegue el contenido que tiene almacenado en el portapapeles. ¿Qué ocurre luego de hacerlo?

```bash
telnet www.redes.unlp.edu.ar 80
Trying 172.28.0.50...
Connected to www.redes.unlp.edu.ar.
Escape character is '^]'.
GET /http/HTTP-1.1/ HTTP/1.0
User-Agent: curl/7.38.0
Host: www.redes.unlp.edu.ar
Accept: */*




HTTP/1.1 200 OK
Date: Thu, 04 Sep 2025 22:03:09 GMT
Server: Apache/2.4.56 (Unix)
Last-Modified: Sun, 19 Mar 2023 19:04:46 GMT
ETag: "760-5f7457bd64f80"
Accept-Ranges: bytes
Content-Length: 1888
Connection: close
Content-Type: text/html

<!DOCTYPE html>
<html lang="en">...</html>
Connection closed by foreign host.
```

### c. Repita el proceso anterior, pero copiando la salida del recurso /extras/prueba-http-1-1.txt. Verifique que debería poder pegar varias veces el mismo contenido sin tener que ejecutar el comando telnet nuevamente.

```bash
curl www.redes.unlp.edu.ar/extras/prueba-http-1-1.txt
GET /http/HTTP-1.1/ HTTP/1.1
User-Agent: curl/7.38.0
Host: www.redes.unlp.edu.ar
Accept: */*

telnet www.redes.unlp.edu.ar 80
Trying 172.28.0.50...
Connected to www.redes.unlp.edu.ar.
Escape character is '^]'.
GET /http/HTTP-1.1/ HTTP/1.1
User-Agent: curl/7.38.0
Host: www.redes.unlp.edu.ar
Accept: */*



HTTP/1.1 200 OK
Date: Thu, 04 Sep 2025 22:33:23 GMT
Server: Apache/2.4.56 (Unix)
Last-Modified: Sun, 19 Mar 2023 19:04:46 GMT
ETag: "760-5f7457bd64f80"
Accept-Ranges: bytes
Content-Length: 1888
Content-Type: text/html

<!DOCTYPE html>
<html lang="en">...</html>

# La conexión permanece abierta, permitiendo enviar más solicitudes sin reconectar.


```

## 16. En base a lo obtenido en el ejercicio anterior, responda:

### a. ¿Qué está haciendo al ejecutar el comando telnet?

Telnet es un protocolo de red que permite a los usuarios conectarse y comunicarse con una computadora remota a través de una interfaz de línea de comandos. Funciona en un modelo de cliente-servidor, donde el cliente Telnet inicia una conexión TCP con el servidor Telnet en un puerto específico (generalmente el puerto 23). Una vez establecida la conexión, el cliente puede enviar comandos al servidor, que los ejecuta como si el usuario estuviera sentado frente a la máquina.

### b. ¿Qué método HTTP utilizó? ¿Qué recurso solicitó?

En ambos casos, se utilizó el método HTTP `GET`. El recurso solicitado fue `/http/HTTP-1.1/`.

### c. ¿Qué diferencias notó entre los dos casos? ¿Puede explicar por qué?

La diferencia principal entre los dos casos radica en la versión del protocolo HTTP utilizado en la línea de solicitud:

- En el primer caso, se utilizó HTTP/1.0.
- En el segundo caso, se utilizó HTTP/1.1, haciendo que la conexión permanezca abierta para múltiples solicitudes.

### d. ¿Cuál de los dos casos le parece más eficiente? Piense en el ejercicio donde analizó la cantidad de requerimientos necesarios para obtener una página con estilos, javascripts e imágenes. El caso elegido, ¿puede traer asociado algún problema?

El caso de HTTP/1.1 es más eficiente debido a su capacidad para mantener conexiones persistentes, lo que reduce la sobrecarga de establecer nuevas conexiones TCP para cada solicitud. Sin embargo, las conexiones persistentes pueden llevar a problemas como el agotamiento de recursos del servidor si demasiadas conexiones permanecen abiertas durante mucho tiempo, lo que podría afectar el rendimiento del servidor y la capacidad de respuesta para otros clientes.

## 17. En el siguiente ejercicio veremos la diferencia entre los métodos POST y GET. Para ello, será necesario utilizar la VM y la herramienta Wireshark. Antes de iniciar considere:

- Capture los paquetes utilizando la interfaz con IP 172.28.0.1. (Menú “Capture ->Options”. Luego seleccione la interfaz correspondiente y presione Start).
- Para que el analizador de red sólo nos muestre los mensajes del protocolo http introduciremos la cadena ‘http’ (sin las comillas) en la ventana de especificación de filtros de visualización (display-filter). Si no hiciéramos esto veríamos todo el tráfico que es capaz de capturar nuestra placa de red. De los paquetes que son capturados, aquel que esté seleccionado será mostrado en forma detallada en la sección que está justo debajo. Como sólo estamos interesados en http ocultaremos toda la información que no es relevante para esta práctica (Información de trama, Ethernet, IP y TCP). Desplegar la información correspondiente al protocolo HTTP bajo la leyenda “Hypertext Transfer Protocol”.
- Para borrar la cache del navegador, deberá ir al menú “Herramientas->Borrar historial reciente”. Alternativamente puede utilizar Ctrl+F5 en el navegador para forzar la petición HTTP evitando el uso de caché del navegador.
- En caso de querer ver de forma simplificada el contenido de una comunicación http, utilice el botón derecho sobre un paquete HTTP perteneciente al flujo capturado y seleccione la opción Follow TCP Stream.

### a. Abra un navegador e ingrese a la URL: www.redes.unlp.edu.ar e ingrese al link en la sección “Capa de Aplicación” llamado “Métodos HTTP”. En la página mostrada se visualizan dos nuevos links llamados: Método GET y Método POST. Ambos muestran un formulario como el siguiente:

### b. Analice el código HTML

```html
<form method="GET" action="metodos-lectura-valores.php">...</form>

<form method="POST" action="metodos-lectura-valores.php">...</form>
```

### c. Utilizando el analizador de paquetes Wireshark capture los paquetes enviados y recibidos al presionar el botón Enviar.

```HTTP
GET /http/metodos-lectura-valores.php?form*nombre=Franco&form_apellido=ASD&form_mail=asdf%40gmail.com&form_sexo=sexo_fem&form_pass= HTTP/1.1
Host: www.redes.unlp.edu.ar
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/\_;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
Referer: http://www.redes.unlp.edu.ar/http/metodo-get.html
Upgrade-Insecure-Requests: 1

POST /http/metodos-lectura-valores.php HTTP/1.1
Host: www.redes.unlp.edu.ar
User-Agent: Mozilla/5.0 (X11; Linux x86*64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/\_;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 118
Origin: http://www.redes.unlp.edu.ar
Connection: keep-alive
Referer: http://www.redes.unlp.edu.ar/http/metodo-post.html
Upgrade-Insecure-Requests: 1

form_nombre=Franco&form_apellido=ASD&form_mail=asd%40mail.com&form_sexo=sexo_masc&form_pass=1234&form_confirma_mail=on

```

### d. ¿Qué diferencias detectó en los mensajes enviados por el cliente?

Las diferencias principales entre los mensajes enviados por el cliente utilizando los métodos GET y POST son las siguientes:

- **Ubicación de los datos**:
  - En el método **GET**, los datos del formulario se envían como parte de la URL en la línea de solicitud, después del signo de interrogación (`?`). Esto hace que los datos sean visibles en la barra de direcciones del navegador y en los registros del servidor.
  - En el método **POST**, los datos del formulario se envían en el cuerpo del mensaje HTTP, lo que significa que no son visibles en la URL y no aparecen en los registros del servidor de la misma manera.
- **Cabeceras adicionales**:
  - En el método **POST**, se incluye la cabecera `Content-Type: application/x-www-form-urlencoded`, que indica el tipo de datos que se están enviando en el cuerpo del mensaje. Además, se incluye la cabecera `Content-Length`, que especifica la longitud del cuerpo del mensaje.
  - En el método **GET**, estas cabeceras no son necesarias ya que los datos se envían en la URL.
- **Longitud de los datos**:
  - El método **GET** tiene limitaciones en la cantidad de datos que se pueden enviar debido a las restricciones de longitud de la URL impuestas por los navegadores y servidores.
  - El método **POST** no tiene estas limitaciones y puede manejar grandes cantidades de datos, ya que los datos se envían en el cuerpo del mensaje.
- **Seguridad**:
  - Los datos enviados mediante el método **GET** son menos seguros, ya que son visibles en la URL y pueden ser almacenados en el historial del navegador o en los registros del servidor.
  - Los datos enviados mediante el método **POST** son más seguros en este sentido, ya que no son visibles en la URL.

### e. ¿Observó alguna diferencia en el browser si se utiliza un mensaje u otro?

No, en términos de visualización en el navegador, ambos métodos (GET y POST) pueden resultar en la misma página web siendo mostrada al usuario. La diferencia radica principalmente en cómo se envían los datos al servidor y no en cómo se presenta la información al usuario final. Sin embargo, el método POST es generalmente preferido para enviar datos sensibles o grandes cantidades de información debido a las razones de seguridad y limitaciones mencionadas anteriormente.

## 18. Investigue cuál es el principal uso que se le da a las cabeceras Set-Cookie y Cookie en HTTP y qué relación tienen con el funcionamiento del protocolo HTTP.

El **principal uso** de las cabeceras `Set-Cookie` y `Cookie` en HTTP es permitir que los sitios web **identifiquen a los usuarios y realicen un seguimiento de su actividad**, superando así la naturaleza **"sin memoria de estado" (stateless)** del protocolo HTTP.

El protocolo HTTP, por sí mismo, no mantiene ninguna información sobre el estado de un cliente entre solicitudes. Esto simplifica el diseño del servidor, permitiéndole manejar miles de conexiones TCP simultáneas de manera eficiente. Sin embargo, para muchas funciones deseables de los sitios web, como restringir el acceso, servir contenido personalizado o gestionar carritos de compra, es necesario poder identificar a los usuarios. Las **cookies** son la tecnología que permite esta funcionalidad.

La tecnología de las cookies se basa en cuatro componentes clave:

1.  Una línea de cabecera `Set-cookie:` en el mensaje de respuesta HTTP del servidor.
2.  Una línea de cabecera `Cookie:` en el mensaje de solicitud HTTP del cliente.
3.  Un archivo de cookies almacenado en el sistema terminal del usuario y gestionado por el navegador.
4.  Una base de datos _back-end_ en el sitio web.

A continuación, se detalla la relación y el funcionamiento de estas cabeceras:

- **Cabecera `Set-Cookie` (respuesta del servidor):**
  - Cuando un usuario visita un sitio web por primera vez (por ejemplo, Amazon.com), el servidor web genera un **número de identificación exclusivo** para ese usuario.
  - El servidor crea una entrada en su base de datos _back-end_ indexada por este número de identificación.
  - La respuesta HTTP del servidor al navegador del usuario incluye una línea de cabecera `Set-cookie:`, que contiene este número de identificación (por ejemplo, `Set-cookie: 1678`).
  - Al recibir este mensaje, el navegador del usuario añade una línea a su archivo de cookies, que incluye el nombre de host del servidor y el número de identificación.

- **Cabecera `Cookie` (solicitud del cliente):**
  - En las visitas posteriores o durante la navegación continua por el mismo sitio, cada vez que el usuario solicita una página web, su navegador consulta su archivo de cookies.
  - El navegador extrae el número de identificación asociado a ese sitio y lo añade a la solicitud HTTP mediante una línea de cabecera `Cookie:` (por ejemplo, `Cookie: 1678`).
  - De esta manera, el servidor puede seguir la actividad del usuario en el sitio web. Aunque el sitio no conozca el nombre real del usuario, sabe qué páginas ha visitado el usuario identificado con ese número, en qué orden y cuántas veces.

**Relación con el funcionamiento del protocolo HTTP:**

Las cabeceras `Set-Cookie` y `Cookie` permiten al protocolo HTTP, que es inherentemente **sin memoria de estado**, simular una **capa de sesión**. Esto significa que, a pesar de que cada solicitud HTTP es independiente, las cookies permiten al servidor "recordar" las interacciones previas de un usuario. Esto es fundamental para funcionalidades como:

- **Carritos de compra:** Amazon puede mantener una lista de compras planificadas por el usuario para que pueda pagarlas todas juntas al final de la sesión.
- **Inicio de sesión:** En aplicaciones de correo electrónico basadas en la web (como Hotmail), el navegador envía información de la cookie al servidor, lo que permite al servidor identificar al usuario a lo largo de su sesión.
- **Contenido personalizado:** Los sitios web pueden adaptar el contenido mostrado al usuario basándose en su historial de navegación o preferencias almacenadas en las cookies.

Es importante mencionar que las cookies son un tema controvertido debido a las **preocupaciones por la privacidad del usuario**, ya que permiten a los sitios web recopilar mucha información sobre las actividades de navegación y, potencialmente, venderla a terceros.

## 19. ¿Cuál es la diferencia entre un protocolo binario y uno basado en texto? ¿De qué tipo de protocolo se trata HTTP/1.0, HTTP/1.1 y HTTP/2?

La principal diferencia entre un protocolo **binario** y uno **basado en texto** es el formato en que se envían los datos.

- Un protocolo **basado en texto** utiliza caracteres legibles para los humanos (como ASCII). Esto facilita la lectura, la depuración manual y la implementación con herramientas sencillas. Sin embargo, su análisis es más lento para las máquinas y su uso de caracteres puede generar una sobrecarga innecesaria.
- Un protocolo **binario** utiliza secuencias de bytes (ceros y unos). No es legible para los humanos, pero es mucho más eficiente en términos de transferencia de datos y velocidad de análisis para las computadoras, ya que no se requiere una conversión de formato.

Clasificación de Protocolos HTTP:

- **HTTP/1.0 y HTTP/1.1** son protocolos **basados en texto**. Las solicitudes y respuestas, incluyendo las cabeceras, se envían como texto plano, lo que permite que sean fácilmente leídas y entendidas por personas.
- **HTTP/2** es un protocolo **binario**. Fue diseñado para resolver las ineficiencias de HTTP/1.x y, para ello, encapsula las solicitudes y respuestas en un formato binario. Esto permite un análisis más rápido y la multiplexación de múltiples transmisiones de datos sobre una única conexión.

## 20. Responder las siguientes preguntas:

### a. ¿Qué función cumple la cabecera Host en HTTP 1.1? ¿Existía en HTTP 1.0? ¿Qué sucede en HTTP/2? (Ayuda: https://undertow.io/blog/2015/04/27/An-in-depth-overview-of-HTTP2.html para HTTP/2)

La cabecera `Host` es **obligatoria** en HTTP/1.1 y cumple una función vital: **especificar el dominio al que se dirige la solicitud**. Su propósito principal es permitir el **alojamiento virtual (virtual hosting)**. Esto significa que un solo servidor web con una única dirección IP puede hospedar múltiples sitios web (dominios). El servidor utiliza el valor de la cabecera `Host` para determinar a qué sitio web el cliente quiere acceder y servir el contenido correcto. 🌐

En HTTP 1.0 la cabecera `Host` **no era obligatoria** en HTTP/1.0. En esa versión del protocolo, se asumía que cada sitio web tenía su propia dirección IP dedicada, por lo que el servidor ya sabía a qué sitio se dirigía la solicitud. Aunque algunos clientes y servidores podían incluirla, no era un requisito para el correcto funcionamiento.

En HTTP/2, la funcionalidad de la cabecera `Host` **se mantiene**, pero su implementación cambia. La información del nombre de host se envía en una nueva pseudo-cabecera llamada **`:authority`**. Esta pseudo-cabecera cumple exactamente el mismo propósito que la cabecera `Host` de HTTP/1.1: identificar el host al que se dirige la solicitud. Sin embargo, en HTTP/2 se integra en el eficiente formato binario del protocolo, eliminando la necesidad de una cabecera de texto separada.

### b. En HTTP/1.1, ¿es correcto el siguiente requerimiento?

    GET /index.php HTTP/1.1
    User-Agent: curl/7.54.0

No, es incorrecta ya que falta la cabecera `Host`, que es obligatoria en HTTP/1.1.

### c. ¿Cómo quedaría en HTTP/2 el siguiente pedido realizado en HTTP/1.1 si se está usando https?

    GET /index.php HTTP/1.1
    Host: www.info.unlp.edu.ar

En HTTP/2, el pedido se representaría utilizando pseudo-cabeceras. Si se está usando HTTPS, la solicitud quedaría de la siguiente manera:

    :method: GET
    :scheme: https
    :authority: www.info.unlp.edu.ar
    :path: /index.php

## Ejercicio de Parcial

    curl -X "host www.redes.unlp.edu.ar"

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

Esta utilizando la version de HTTP/1.0 ya que la conexion se cierra luego de la respuesta.

La consulta y respuesta quedaria asi:

    curl -X HEAD www.redes.unlp.edu.ar/metodos/
    HEAD /metodos/ HTTP/1.0
    Host: www.redes.unlp.edu.ar
    User-Agent: curl/7.54.0
    < HTTP/1.0 200 OK
    < Server: nginx/1.4.6 (Ubuntu)
    < Date: Wed, 31 Jan 2018 22:22:22 GMT
    < Last-Modified: Sat, 20 Jan 2018 13:02:41 GMT
    < Content-Type: text/html; charset=UTF-8
    < Connection: close

### b. ¿Qué método está utilizando? Dicho método, ¿retorna el recurso completo solicitado?

Esta utilizando el metodo HEAD, el cual no retorna el recurso completo, solo las cabeceras.

### c. ¿Cuál es el recurso solicitado?

El recurso soluicitado es /metodos/

### d. ¿El método funcionó correctamente?

Sí, funcionó correctamente. El código de estado es 200 OK, lo que indica que la solicitud fue exitosa.

### e. Si la solicitud hubiera llevado un encabezado que diga:

    If-Modified-Since: Sat, 20 Jan 2018 13:02:41 GMT

¿Cuál habría sido la respuesta del servidor web? ¿Qué habría hecho el navegador en este caso?
La respuesta del servidor web habría sido:

    HTTP/1.0 304 Not Modified
    Date: Wed, 31 Jan 2018 22:22:22 GMT
    Server: nginx/1.4.6 (Ubuntu)
    Connection: close

El navegador no habria descargado el recurso nuevamente, ya que el servidor indica que el recurso no ha sido modificado desde la fecha especificada en el encabezado `If-Modified-Since`. En su lugar, el navegador utilizaría la versión en caché del recurso, optimizando así el uso del ancho de banda y mejorando la eficiencia.
