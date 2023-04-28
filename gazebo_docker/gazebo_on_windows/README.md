# Gazebo en Docker para Windows

#### Prerrequisitos:


* Activar la virtualización desde BIOS
* Instalar [Docker Desktop](https://www.docker.com/products/docker-desktop/) para Windows, se requiere reiniciar después de su instalación.
* Actualizar el kernel de WSL poniendo en cmd el comando `wsl --update`. Es probable que sea necesario reiniciar después de actualizar el kernel.
  
  Hasta este punto, la virtualización y el kernel de WSL son requisitos necesarios para la inicialización de Docker Desktop, si están correctamente configurado, iniciará correctamente sin mostrar alertas.
  
* Instalar [Xming X Server](https://sourceforge.net/projects/xming/) para Windows **Al finalizar la instalación, seleccionar la opción "Public Access" para permitir el acceso a Xming desde otros equipos**

#### Implementación

Inicializar Docker Desktop y Xming, basta con abrir las aplicaciones desde el botón de inicio, podemos cerrarlas después, pues se mantienen en ejecución en segundo plano, pero para asegurarnos que están corriendo, debemos ver estos dos íconos en la barra de tareas ![image](https://user-images.githubusercontent.com/33168405/235026376-c030425b-aaec-46a9-b5b1-a980ab23b445.png)

Ahora podemos correr en cmd el comando 
```shell
docker pull lissethamc/win_gazebo_repo:latest
```

