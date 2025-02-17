# PROXY - INVERSO
## Servidor w1
En el servidor w1 editamos el archivo <a href="/proxy-inverso/w1/default"> default </a> de la ruta /etc/nginx/sites-available/default.
Luego reiniciamos Nginx para aplicar los cambios mediante el comando "sudo systemctl restart nginx".
Creamos una página de prueba <a href="/proxy-inverso/w1/index.html"> index.html </a>
Probamos la apliación con curl, primero lo instalamos (sudo apt install -y curl) y luego lo conectamos (curl http://localhost:8080)
<img src="/proxy-inverso/w1/img/curl.png" alt="curl">

## Nginx proxy inverso 
En el servidor proxy editamos el <a href="/proxy-inverso/proxy/hosts"> archivo hosts </a>, de la ruta  /etc/hosts. También modificamos el <a href="/proxy-inverso/proxy/default"> fichero default </a> . Luego mediante la ip podremos acceder a la aplicación
<img src="/proxy-inverso/proxy/navegador.png" alt="salida por navegador">

# Comprobaciones
Luego de acceder a la página por la ip podemos comprobar los logs.
Access.log de Proxy
<img src="/proxy-inverso/proxy/access-log.png" alt="access.log">
Access.log de web
<img src="/proxy-inverso/w1/img/access-log.png" alt="access-log de web">

# Cabeceras
La cabecera host indica la procedencia 
<img src="/proxy-inverso/w1/img/cabecera-hosts.png" alt="cabecera host">

Si accedemos mediante www.192.168.57.10.nip.io, veremos que la cabecera Host cambia. 
<img src="/proxy-inverso/w1/img/host-no-ip.png" alt="cabecera con nip.io">

## Añadiendo cabeceras
Luego de editar correctamente el bloque location/ del fichero default y reiniciar Nginx podemos añadir la cabecera "X-friends"
<img src="/proxy-inverso/proxy/cabecera-x-friend.png" alt="cabecera x-friend">

## Cabeceras en el servidor web
Volvemos a hacer los pasos anteriores en los que editamos el fichero default y comprobamos que se añade la cabecera.
<img src="/proxy-inverso/w1/img/2da-cabecera-host.png">


# Ampliación
Creamos dos directorios uno para <a href="/proxy-inverso/docker-proxy/proxy/"> proxy </a> y otro para <a href="/proxy-inverso/docker-proxy/web/"> web </a>.
Cada uno con su respectivo Dockerfile: <a href="/proxy-inverso/docker-proxy/proxy/Dockerfile" > Dockerfile de proxy </a> y <a href="/proxy-inverso/docker-proxy/web/Dockerfile" > Dockerfile de web </a> 
El fichero <a href="/proxy-inverso/docker-proxy/docker-compose.yml"> docker-compose.yml </a>
Luego creamos los contenedores.
<img src="/proxy-inverso/docker-proxy/docker-up.png">
Y comprobamos que se ejecuta correctamente la página 
<img src="/proxy-inverso/docker-proxy/ejecucion.png">
