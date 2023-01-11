* Dynamic DNS Updater

https://github.com/qdm12/ddns-updater

Este servicio docker sirve para actualizar la IP a la que apunta nuestro dominio, para ello en el gestor de nuestro dominio establecemos una clave de aacceso que se guardará en el fichero config.json y según el periodo que establezcamos se conectará al servcio de dominio y le dira la IP pública desde la que se está ejecutando.

Crear un directorio donde estará el fichero de configuración y se guardaran los datos:
```
$ mkdir dataDocker/ddns-updater
$ touch dataDocker/ddns-updater/config.json
# Owned by user ID of Docker container (1000)
$ chown -R 1000 dataDocker/ddns-updater
$ chmod 700 dataDocker/ddns-updater
$ chmod 400 dataDocker/ddns-updater/config.json
```
Crear el fichero de configuración:
```
$ vi dataDocker/ddns-updater/config.json
{
    "settings": [
        {
            "provider": "name-provider",
            "domain": "example.com", 
            "host": "@, subdomain1, subdomain2",
            "password": "MY_SECRECT_PASSWORD"
        }
    ]
}
```
El servicio dispone de un interface web donde se puede ver las actualizaciones de IP que arranca por defecto en el puerto 8000 y que se puede ver accediendo con un navegador a http://localhost:8000



