### Exemplo de rota

#### .htaccess
``` php
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php [NC,L]
```
#### Rota
``` php
<?php

require __DIR__ . '/vendor/autoload.php';

use Fredrumond\Bakkhos\Router;

$method = $_SERVER['REQUEST_METHOD'];
$path = $_SERVER['PATH_INFO'] ?? '/';

$router = new Router($method, $path);

$router->get('/', function () {
    return 'Olá mundo';
});

$router->get('/ola-{nome}', function () {
    return 'Olá mundo 2';
});

$result = $router->handler();


if (!$result) {
    http_response_code(404);
    echo 'Página não encontrada!';
    die();
}


echo $result();
```