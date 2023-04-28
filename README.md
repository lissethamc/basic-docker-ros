# Implementación de HelloWorld Docker con ROS

#### 218292645 | Lisseth Abigail Martínez Castillo  :octocat:

### ¿Qué es Docker?
Es una plataforma que permite el despliegue de de aplicaciones en un entorno aislado, en forma de _contenedores_. Los contenedores son instancias que maneja Docker para donde se ejecuta una versión ligera de un sistema operativo. Algunas de las ventajas de usar Docker son:
* __Portabilidad__: Los contenedores de Docker son portátiles, es decir, se pueden ejecutar en cualquier plataforma que tenga Docker instalado, es posible desarrollar una aplicación en una máquina de manera local, pero ejecutarla en cualquier otro entorno, sin preocuparse por la compatibilidad de las plataformas.
* __Consistencia__: Es posible crear entornos de desarrollo y producción idénticos, por lo que las aplicaciones se comportarán de la misma forma en las etapas del ciclo de vida de la aplicación.
* __Aislamiento__: Los contenedores de Docker están aislados entre sí y del sistema operativo host, esto evita conflictos de software y que se afecten entre ellos.
* __Escalabilidad__: Permite agregar o eliminar contenedores según sea necesario para escalar aplicaciones fácilmente.

### ¿Qué es ROS?
Es una plataforma de código abierto que contiene un conjunto de herramientas para facilitar el desarrollo de software y control para robots. Proporciona herramientas para la programación y manejo de robots, así como facilita la estructura para la comuicación entre procesos y control de hardware.

Es también a menudo llamado "metasistema operativo" porque se construye sobre un sisetma operativo subyacente (como Linux), pero proporciona además una capa de abstracción de hardware, herramientas y servicios que permiten comunicación entre los componentes de un robot o sistema robótico (en vez de un sistema operativo tradicional que lo hace a nivel de sistema de computación general). Igualmente proporciona servicios como la gestión y comunicación entre procesos, administración de recursos, entre otras funciones de sistema operativo.
Entre las herramientas que proporciona ROS son las de visualización, simulación, planificación y control de movimiento, percepción y procesamiento de imágenes entre muchas otros.

De las herramientas que proporciona ROS para el manejo de recursos en los sistemas robóticos, es posible considerar sensores, actuadores, planificación de movimiento, entre otros; por lo que en vez de desarrollar software personalizado para cada de estos componentes, es posible usar los servicios de ROS para integrarlos y construir sistemas más complejos. Es decir, nos proporciona una capa de abstracción que permite centrarnos en el desarrollo específico del robot o sistema en vez de preocuparnos por los detalles de bajo nivel o sistema operativo subyacente.

### Implementación

Docker puede ser utilizado con diferentes distribuciones de ROS, algunas de las versiones compatibles con Docker son:
* ROS Kinetic Kame
* ROS Melodic Morenia
* ROS Noetic Ninjemys
* ROS2 Dasing Diademata
* ROS2 ELoquent Elusor
* ROS2 Fosy Fitzroy

Entre otros

Es necesario primero asegurarnos que la imagen de Docker es compatible con la distribución de Linux que estamos usando, aunque las imágenes de Docker para ROS suelen ser para una distribucion de Linux en especifica como Ubuntu.

No todas las distribuciones de ROS son compatibles con Docker pero la mayoría lo son, se recomienda usar una versión de ROS que tenga soporte activo y se actualice regularmente. Si se usa una versión de ROS menos común es probable que no haya una versión de Docker disponible o se deba de construir una imagen personalizada.

Es posible utilizar Docker con prácticamente cualquier distribución de Linux y las imágenes de Docker para ROS suelen estar construidas para Ubuntu. Si se usa una distrubición de Linux diferente, es posible que sea necesario ajustar la configuración de Docker y ROS para asegurarnos del correcto funcionamiento.

**Nota**: No es necesario tener instalado ROS de antemano en el sistema host para poder correrlo en un entorno Docker, ese es el objetivo de instalar Docker

#### Instalación de Docker en Linux

Primero debemos comprobar si tenemos instalado Docker, para ello ejecutamos el siguiente comando en una terminal

```shell
docker --version
```
De tener Docker instalado, debemos ver una salida que indica la versión de docker instalado, sino el comando dará un mensaje de error que indica que el comando "docker" no se encuentra en el sistema.

Para instalar Docker en caso de ser necesario

1. Actualizar los paquetes del sistema:
```shell
sudo apt-get update
```

2. Instalar los paquetes necesarios utilizar paquetes via HTTPS:
```shell
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

3. Descargar e importar la clave GPG oficial de Docker:
```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
4. Agregar el repositorio de Docker a las fuentes de paquetes de APT:
```shell
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
5. Actualizar de nuevo los paquetes del sistema para que sea posible reconocer los paquetes de Docker recién agregados
```shell
sudo apt-get update
```

6. Instalar Docker
```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Podemos confirmar su instalación ejecutando el comando
```shell
docker run hello-world
```
Esto nos descarga una imagen de prueba y la ejecuta en un contenedor de Docker, mostrando su correcto funcionamiento.

#### Instalación de Docker en Windows

* Activar la virtualización desde BIOS

* Instalar [Docker Desktop](https://www.docker.com/products/docker-desktop/) para Windows, se requiere reiniciar después de su instalación.

* Actualizar el kernel de WSL poniendo en `cmd` el comando `wsl --update`. Es probable que sea necesario reiniciar después de actualizar el kernel.
  
  Hasta este punto, la virtualización y el kernel de WSL son requisitos necesarios para la inicialización de **Docker Desktop**, si están correctamente configurado, iniciará correctamente sin mostrar alertas.

###### Descargar y correr una imagen de ROS en Docker

**Nota**: Estos comandos pueden ser implementados tanto en **Windows** desde `cmd` como desde **Linux** habiendo hecho los pasos anteriores para el SO correspondiente. Para Linux es probable que necesite permisos de super usuario, para Windows no es necesario, simplemente basta con omitir `sudo` para los comandos.

Para poder trabajar con ROS, necesitamos una imagen de Docker, es decir un sistema operativo que tenga pre instalado ROS. Podemos descargar una imagen desde Docker Hub, Por ejemplo, podemos descargar la última imagen de ROS Melodic, corremos el siguiente comando en una terminal (es probable que estos comandos necesiten permisos de superusuario):

```shell
sudo docker pull ros:melodic
```
Si el comando es correcto, veremos una descarga. La versión puede variar por la necesaria.

En caso de querer corroborar la descarga o el resto de imágenes descargadas es posible enlistarlas con

```shell
sudo docker images
```
![Screenshot from 2023-04-21 16-41-01](https://user-images.githubusercontent.com/33168405/233739088-f2b9e72b-862e-4993-9dd6-413a6121c19d.png)


Una vez descargada la imagen, para crear y ejecutar un contenedor interactivo, debemos usar el siguiente comando: 

```shell
sudo docker run -it --name my_melodic_container ros:melodic
```
El nombre **"my_melodic_container"** es un _placeholder_ que puede ser elegido a voluntad del usuario, puede ser omitido y Docker le asignará un nombre aleatorio que deberá consultar después para poder acceder a él. En caso de ser omitido, también deberá omitir la bandera "--name" y el comando funcionará igualmente. El parámetro "-it" indica que queremos una sesión interactiva, es decir, que se muestre una consola para que podamos trabajar en ella. 

Podemos notar que el nombre del usuario y del equipo en la consola cambian al correr el comando pues ahora nos encontramos dentro del contenedor de Docker 
![image](https://user-images.githubusercontent.com/33168405/233739333-08c5a115-71f0-4e85-ba6f-01bb0d1f030d.png)

Dentro del contenedor ahora podemos ejecutar el comando
```shell
roscore
```
Esto debe funcionar pues la imagen que descargamos y ejecutamos ya tenía instalado ROS, pero también nos mantendrá la consola ocupada, por lo que para el resto de comandos debemos ejecutarlos en otra terminal, **sin cerrar la terminal actual**. 
![image](https://user-images.githubusercontent.com/33168405/233742393-ff24e742-4f41-44e4-b7e2-f3a880bbf048.png)

Podemos corroborar las imágenes que tenemos descargadas con el comando
```shell
sudo docker ps -a
```
Este comando además nos enlista los nombres con los que fueron creados los contenedores, necesario para le siguiente paso.
![image](https://user-images.githubusercontent.com/33168405/233739800-12017ea2-11e1-47b6-a46c-3edfe7b6cc93.png)


Para abir el mismo contenedor en una nueva terminal ejecutamos el siguiente comando:
```shell
sudo docker exec -it my_melodic_container bash
```
Siendo **`my_melodic_container`** el contenedor que hayamos nombrado nostros al inicio, o el que haya nombrado Docker y que hayamos consultado através del paso anterior.

Ahora es necesario incializar el ambiente de ROS en la terminal actual, para ello ejecutamos el siguiente comando:
```shell
source /opt/ros/<distro>/setup.bash
```
reemplazando *`<distro>` con el nombre de la distribución de ROS que estamos usando*

Dentro de la segunda terminal hay que asegurarnos que estén los paquetes necesarios para el talker y chatter, por lo que ejecutaremos los siguientes comandos

```shell
$ sudo apt-get update
$ sudo apt-get install -y ros-<ROS_VERSION>-roscpp-tutorials
$ source /opt/ros/<ROS_VERSION>/setup.bash
```

Una vez hecho esto en la segunda terminal podemos crear el nodo talker que publicará mensajes en el tópico *`/chatter`* con el siguiente comando:

```shell
$ rosrun roscpp_tutorials talker
```
![image](https://user-images.githubusercontent.com/33168405/233743560-edfd58bb-d9dc-4fdd-a2ec-f36926f31ba5.png)

Para ver los mensajes que publica el nodo _talker_ podemos abrir una tercera terminal y acceder al mismo contenedor de la misma manera que a la segunda, y en esta tercer teminal ejecutar el comando:
```shell
$ rostopic echo /chatter
```
![image](https://user-images.githubusercontent.com/33168405/233743574-397faeef-169e-4b74-91ed-a2f49ea9705c.png)

Para salir del contenedor basta con ejecutar 
```shell
$ exit
```

**Nota**: de forma default, los contenedores se "apagan" sino están ejecutando nada y la terminal se cierra, se ejecuta "exit", la computadora se apaga o se temina el proceso y no es posible acceder a ese mismo contenedor de forma normal pues dice que el nombre yá en uso al querer correrlo o dice que no esá corriendo al querer ejecutarlo. Es posible agregar una bandera en la creación del contenedor para indicar que es necesario que se continue su ejecución en segundo plano, pero depende de si este es el comportamiento esperado, aún estoy documentándome en esta parte. De momento, si el contenedor se "apaga", es posible volver a ejecutarlo reiniciándolo: obteniendo su ID a través de:
```shell
docker ps -a
docker restart <CONTAINER ID>
``` 
https://stackoverflow.com/questions/29599632/container-is-not-running
