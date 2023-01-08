
##### 1. Instalación del sistema Ubuntu Server 22.04 LTS

He escogido Ubuntu por estar familiarizado con el y con el gran soporte de comunidad que tiene, hay una gran guía de instalación en esta página: https://www.howtoforge.com/ubuntu-22-04-minimal-server/ 
yo he elegido la version por defecto no la minima.

##### 2. Actualizar el sistema
```
$ sudo apt uppdate -y && sudo apt uprade -y
```
##### 3. Instalar paquetes adicionales
 ```
 $ sudo apt install lm-sensors vim-nox
 ```
##### 4. Establecer nombre del servidor
```
$ sudo hostnamectl set-hostname NEW_HOSTNAME
```
##### 5. Establecer la zona horaria
```
$ timedatectl list-timezones
$ sudo timedatectl set-timezone Europe/Madrid
$ timedatectl
```
##### 6. Configurar el Firewall

Tutorial básico en [Digitial Ocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04)
```
# habilitar firewall
$ sudo systemctl enable ufw
$ sudo systemctl status ufw
$ sudo ufw enable

# politicas por defecto
$ sudo ufw default deny incoming
$ sudo ufw default allow outgoing

# acceso a ssh, http y https
$ sudo ufw allow from 192.168.1.7 to any port 22
$ sudo ufw allow http
$ sudo ufw allow https
``` 

##### 7. Instalar docker

Tutorial básico en [Digitial Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)
``` 
$ sudo apt install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    software-properties-common

# añadir clave GPG oficial de Docker 
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# añadir repositorio
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# actualizar e instalar
$ sudo apt update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# ejecutar el comando docker sin sudo
$ sudo usermod -aG docker ${USER}

# comprobar la instalación
$ docker run hello-world
$ docker ps
```
##### 8. Instalar docker-compose

Tutorial básico en [Digitial Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-22-04)
```
$ mkdir -p ~/.docker/cli-plugins/
$ curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
$ chmod +x ~/.docker/cli-plugins/docker-compose
$ docker compose version
```

