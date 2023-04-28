# Gazebo en Docker para Windows

#### Prerrequisitos:


* Activar la virtualización desde BIOS
* Instalar [Docker Desktop](https://www.docker.com/products/docker-desktop/) para Windows, se requiere reiniciar después de su instalación.
* Actualizar el kernel de WSL poniendo en `cmd` el comando `wsl --update`. Es probable que sea necesario reiniciar después de actualizar el kernel.
  
  Hasta este punto, la virtualización y el kernel de WSL son requisitos necesarios para la inicialización de Docker Desktop, si están correctamente configurado, iniciará correctamente sin mostrar alertas.
  
* Instalar [Xming X Server](https://sourceforge.net/projects/xming/) para Windows **Al finalizar la instalación, seleccionar la opción "Public Access" para permitir el acceso a Xming desde otros equipos**

#### Implementación

Inicializar Docker Desktop y Xming, basta con abrir las aplicaciones desde el botón de inicio, podemos cerrarlas después, pues se mantienen en ejecución en segundo plano, pero para asegurarnos que están corriendo, debemos ver estos dos íconos en la barra de tareas ![image](https://user-images.githubusercontent.com/33168405/235026376-c030425b-aaec-46a9-b5b1-a980ab23b445.png)

Ahora podemos ejecutar en `cmd` el comando lo que descará la imagen que contiene ros melodic y gazebo pre configurados.
```shell
docker pull lissethamc/win_gazebo_repo:latest
```

Para ejecutar esa imagen y crear un contenedor se usa el siguiente comando, las banderas `-it` indican que queremos que se genere un entorno interactivo, es decir que se genere una consola para controlarlo y `--rm` que el contenedor termine cuando no haya nada ejecutándose, esto para evitar el consumo de recursos de la máquina host
```shell
docker run -it --rm lissethamc/win_gazebo_repo
```
Estando dentro del contenedor, podemos notarlo porque habrá cambiado el usuario en `cmd` de ser el path de windows a ser uno parecido a linux, podemos escribir `gazebo`, esto nos ejecutará Gazebo.

Para detener la ejecución podemos cerrar la ventana gráfica de Gazebo, luego en la consola escribir `ctrl + z` y para finaliazar el contenedor escribir `exit`. Ahora podemos cerrar en el menú de la barra de tareas el Docker Engine y Xming.
