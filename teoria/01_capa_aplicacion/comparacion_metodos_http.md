# Comparación de métodos entre HTTP 1.0, HTTP 1.1 y HTTP 2

|HTTP 1.0| HTTP 1.1 | HTTP 2 |
|---|---|---|
|GET|GET|GET|
|POST|POST|POST|
|PUT|PUT|PUT|
|DELETE|DELETE|DELETE|
|HEAD|HEAD|HEAD|
|LINK|LINK|LINK|
|UNLINK|UNLINK|UNLINK|
| - |OPTIONS|OPTIONS|
| - | CONNECT | CONNECT |
| - | TRACE | TRACE |

## Explicación Métodos
### GET
Se utiliza para solicitar un recurso del servidor. Los parámetros se envían en la URL y no deben tener efectos secundarios en el servidor. 

- ej: 
```
GET /index.html HTTP/1.1
Host: www.ejemplo.com
```

### POST
Se utiliza para enviar datos al servidor, generalmente para crear o actualizar un recurso. Los parámetros se envían en el cuerpo de la solicitud y pueden tener efectos secundarios en el servidor.

- ej:
```
POST /form HTTP/1.1
Host: www.ejemplo.com
Content-Type: application/x-www-form-urlencoded

name=John&age=30
```

### PUT
Se utiliza para actualizar un recurso existente en el servidor. Los parámetros se envían en el cuerpo de la solicitud y pueden tener efectos secundarios en el servidor.

- ej:
```
PUT /user/123 HTTP/1.1
Host: www.ejemplo.com
Content-Type: application/json

{
  "name": "John",
  "age": 30
}
```

### DELETE
Se utiliza para eliminar un recurso del servidor. Los parámetros se envían en la URL y pueden tener efectos secundarios en el servidor.

- ej:
```
DELETE /user/123 HTTP/1.1
Host: www.ejemplo.com 
```

### HEAD
Se utiliza para solicitar los encabezados de un recurso sin obtener el cuerpo de la respuesta. Es útil para verificar la existencia de un recurso o para obtener metadatos sin descargar el contenido completo.

- ej:
```
HEAD /index.html HTTP/1.1
Host: www.ejemplo.com
```

### LINK
Se utiliza para establecer una relación entre el recurso solicitado y otro recurso. Los parámetros se envían en la URL y pueden tener efectos secundarios en el servidor.

- ej:
```
LINK /resource/123 HTTP/1.1
Host: www.ejemplo.com
```

### UNLINK
Se utiliza para eliminar una relación entre el recurso solicitado y otro recurso. Los parámetros se envían en la URL y pueden tener efectos secundarios en el servidor.

- ej:
```
UNLINK /resource/123 HTTP/1.1
Host: www.ejemplo.com
```

### OPTIONS
Se utiliza para solicitar información sobre las opciones de comunicación disponibles para un recurso. Los parámetros se envían en la URL y no deben tener efectos secundarios en el servidor.

- ej:
```
OPTIONS /resource/123 HTTP/1.1
Host: www.ejemplo.com
```

### CONNECT
Se utiliza para establecer un túnel de comunicación con el servidor, generalmente para conexiones seguras (HTTPS). Los parámetros se envían en la URL y pueden tener efectos secundarios en el servidor.

- ej:
```
CONNECT www.ejemplo.com:443 HTTP/1.1
Host: www.ejemplo.com
``` 

### TRACE
Se utiliza para realizar un seguimiento de la ruta que sigue una solicitud a través de los servidores intermedios. Los parámetros se envían en la URL y no deben tener efectos secundarios en el servidor.
- ej:
```
TRACE /resource/123 HTTP/1.1
Host: www.ejemplo.com
```

