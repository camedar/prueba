# prueba

Ambiente de Desarrollo

El ambiente se ha configurado usando la plataforma Docker. Esta herramienta permite el despliegue de aplicaciones y servicios proporcionando un ambiente aislado para esto. Docker funciona sobre el sistema operativo del computador en el cual es instalado y proporciona una estructura que ofrece la posibilidad de crear entornos separados (Con su propio sistema operativo y configuración). En un mismo equipo o servidor pueden funcionar muchos Contenedores de Docker, cada uno con su propia configuración interna y funcionando de manera independiente.
 
El servidor en el cual se configuro el ambiente de desarrollo esta instalado en la nube, utilizando el proveedor Azure. En este servidor se publicó la aplicación Jupyter Notebook y puede ser accedida con la siguiente url:
http://20.25.13.68:8888/?token=ds4a-project

Ambiente Local (Opcional)

También se puede generar un ambiente local con Jupyter Notebook a partir de los mismos archivos de configuración de Docker usados en el servidor, para esto el primer paso es instalar Docker en el equipo donde se quiera tener el entorno local.
Docker se puede descargar de uno de los siguientes links dependiendo del sistema operativo usar:
https://docs.docker.com/desktop/windows/install/
https://docs.docker.com/desktop/mac/install/
La instalación es sencilla, en caso de cualquier inconveniente se puede encontrar información en el siguiente enlace:
https://www.c-sharpcorner.com/article/how-to-install-docker-desktop-and-troubleshoot-issues-in-windows-machine/

Una vez se ha terminado de instalar Docker se debe ver una ventana como la siguiente, una vez terminada el computador debe ser reiniciado.  

Después de instalado Docker debe se iniciar el servicio. Para iniciar la configuración del ambiente local se debe crear una carpeta, para efectos de simplicidad se puede crear en el disco C: con el nombre ‘contenedor_ds4a’. en esta carpeta copiamos los archivos Dockerfile y requirements.txt.
También dentro de esta carpeta creamos otra carpeta llamada ‘jupyter_shared_files’
Para crear y ejecutar el contenedor se deben correr los siguientes comandos, para esto se puede abrir una terminal (En el caso de Windows cmd, se puede buscar en el campo de búsqueda de la barra de tareas). Una vez en la terminal se debe ingresar a la carpeta ‘contenedor_ds4a’:
 

Una vez dentro de la carpeta ejecutar el siguiente comando:
docker build . -t ds4a-jupyter-image
La duración de la ejecución de este comando puede tardar varios minutos dependiendo de las características del computador. Una vez terminado el proceso se puede ver algo como lo siguiente:
 
A continuación, ingresamos el siguiente comando en la misma terminal:
docker create --name ds4a-jupyter-container -p 8888:8888 -v /c/contenedor_ds4a/jupyter_shared_files:/home/jupyter ds4a-jupyter-image
Este comando debería correr rápidamente y su resultado en pantalla es simplemente el identificador del nuevo contenedor creado, el cual es una cadena de caracteres. Finalmente ejecutar el comando para iniciar el contendor referenciándolo por el nombre que le dimos en el comando anterior:
	docker start ds4a-jupyter-container
La salida de este comando es el nombre del contenedor que se inicio (ds4a-jupyter-container), en este punto ya se puede acceder a la aplicación que fue publicada en el contenedor que reposa en Docker. Para acceder a Jupyter se puede usar la siguiente url desde cualquier navegador Web (Este navegador corre en el servidor local conocido como localhost):
http://127.0.0.1:8888/?token=ds4a-project

Todos los archivos y carpetas copiados en la carpeta creada anteriormente jupyter_shared_files son visibles de este la aplicación Jupyter, así mismo todas las modificaciones hechas desde Jupyter son guardadas en esta misma carpeta.
 

 

![image](https://user-images.githubusercontent.com/3820713/172734589-77041133-7a3e-4907-85ae-75a76369fe26.png)
