**Deprecated**

Slim request time middleware
=====

Middleware para Slim 3 que agrega cabecera (Slim-Request-Total-Time) con el tiempo total del request.

[![Build Status](https://travis-ci.org/mostofreddy/slim-request-time-middleware.svg?branch=master)](https://travis-ci.org/mostofreddy/slim-request-time-middleware)

Versión
-------

0.1.0

License
-------

The MIT License (MIT). Ver el archivo [LICENSE](LICENSE.md) para más información

Documentación
-------------

El middleware agrega la cabecera `Slim-Request-Total-Time` en la respuesta del request con el __tiempo total en segundos__ que tarda el request en procesarse

```
$ curl -v "http://localhost:5005"
* Rebuilt URL to: http://localhost:5005/
*   Trying 127.0.0.1...
* Connected to localhost (127.0.0.1) port 5005 (#0)
> GET / HTTP/1.1
> Host: localhost:5005
> User-Agent: curl/7.47.0
> Accept: */*
> 
< HTTP/1.1 404 Not Found
< Host: localhost:5005
< Connection: close
< X-Powered-By: PHP/7.0.12
< Content-type: application/json
< Slim-Request-Total-Time: 0.3244
< Content-Length: 200

```

Ejemplo de uso
-------------

### Configurar middleware para todas las rutas

```
require_once "../vendor/autoload.php";

use Slim\App;
use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Message\ResponseInterface;

$config = [];
$config['settings'] = [
    "displayErrorDetails" => true, // or false
    "determineRouteBeforeAppMiddleware" => true
];

$api = new App($config);

$api->add('\Resty\Slim\TotalTimeRequestMiddleware');

//...

$api->run();

```

### Configurar middleware para alguna ruta (o grupo) en particular

```
require_once "../vendor/autoload.php";

use Slim\App;
use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Message\ResponseInterface;

$config = [];
$config['settings'] = [
    "displayErrorDetails" => true, // or false
    "determineRouteBeforeAppMiddleware" => true
];

$api = new App($config);

$api->get('/', function (ServerRequestInterface $request, ResponseInterface $response) {
    $body = $response->getBody();
    $body->write('Hello');
    return $response;
})->add('\Resty\Slim\TotalTimeRequestMiddleware')

$api->run();
```
