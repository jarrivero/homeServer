# homeServer

Este repositorio describe el proceso de instalación y configuración de servicios auto-alojados (selfhosted) que son  servidos con contedores docker que correrá sobre un linux (Debian, Raspbian, Ubuntu, etc) con dos discos, uno para el sistema y los datos de configuración y el otro como almacenamiento.

Se usa Traefik como balanceador de carga y ademas se encargará de obtener el certificado Let’s Encrypt para nuestro dominio

1. Actualizar el sistema
```
$ sudo apt uppdate -y && sudo apt uprade -y
```
2. Instalar docker
``` 
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# añadir clave GPG oficial de Docker 
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# añadir repositorio
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# actualizar e instalar
$ sudo apt updte
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# ejecutar el comando docker sin sudo
$ sudo usermod -aG docker ${USER}

# comprobar la instalación
$ docker run hello-world
$ docker ps
```
3. Instalar docker-compose

