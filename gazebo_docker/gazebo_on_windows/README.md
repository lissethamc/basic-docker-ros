# Gazebo en Docker para Windows

#### Prerrequisitos:


* Activar la virtualización desde BIOS
* Instalar [Docker Desktop](https://www.docker.com/products/docker-desktop/) para Windows, se requiere reiniciar después de su instalación.
* Actualizar el kernel de WSL poniendo en cmd el comando `wsl --update`. Es probable que sea necesario reiniciar despuès de actualizar el kernel.
  
  Hasta este punto, la virtualización y el kernel de WSL son requisitos necesarios para la inicialización de WSL, si están correctamente configurados Docker Desktop iniciará correctamente sin mostrar alertas.
  
* Instalar [Xming X Server](https://sourceforge.net/projects/xming/) para Windows **Al finalizar la instalación, seleccionar la opción "Public Access" para permitir el acceso a Xming desde otros equipos**
