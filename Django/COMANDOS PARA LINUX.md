#### Versiones de Python en Linux

En general, Linux puede tener más de una versión de Python instalada, pero es necesario ejecutar la versión 3 o superior. En algunas distribuciones de Linux, al ejecutar `python --version`, se puede obtener la versión 3.x.x, pero en otros casos puede devolver un mensaje de error, en cuyo caso se debe usar `python3 --version` para obtener la versión específica instalada [1](https://docs.python.org/es/3/using/windows.html).

#### Crear un Entorno Virtual

Para crear un entorno virtual en Linux, se puede utilizar el comando `python3 -m venv [NOMBRE DEL ENTORNO]`,por ejemplo: `python3 -m venv .venv`.

#### Activar y Desactivar un Entorno Virtual

Para activar un entorno virtual en Linux, se debe acceder al directorio donde se creó el entorno virtual, ingresar a la carpeta del mismo y dentro a la carpeta "bin" y ejecutar el archivo "activate". El comando sería `source [NOMBRE DEL ENTORNO]/bin/activate` O `[NNOMBRE DEL ENTORNO]\script\active`, por ejemplo: `source miEntornoVirtual/bin/activate`. Para desactivar un entorno virtual, simplemente se debe tipear "deactivate" en la línea de comandos.

#### Listado de Librerías Instaladas en el Entorno Virtual

Para averiguar qué librerías están instaladas en el entorno virtual, se puede ejecutar cualquiera de estos dos comandos: `pip list` o `pip freeze` [1](https://docs.python.org/es/3/using/windows.html).

#### Generar un Registro de Paquetes del Proyecto

Para generar un archivo con el nombre "requirements.txt" que contenga un registro de los paquetes necesarios para el proyecto, se puede ejecutar el comando `pip freeze > requirements.txt`.

#### Instalar Paquetes Dependientes a través de un Archivo "requirements.txt"

Para instalar todas las librerías que utiliza el proyecto a través del archivo "requirements.txt", se debe tener activo el entorno virtual y luego ejecutar `pip install -r requirements.txt`.

#### Instalar Django en el Entorno Virtual

Para instalar la última versión de Django disponible, teniendo en cuenta la versión de Python instalada en el sistema, se puede utilizar el comando `pip install django`. Para instalar una versión específica de Django, se debe ejecutar `pip install django==3.2` [1](https://docs.python.org/es/3/using/windows.html).

#### Averiguar Versión de Django Instalada

Para averiguar la versión de Django instalada, se pueden utilizar varios comandos, como `django-admin --version`, `python3 -m django --version`, `pip freeze` o `pip list`.

#### Desinstalar una Librería del Entorno Virtual

Para desinstalar cualquier librería instalada en el entorno virtual, se puede ejecutar el comando `pip uninstall [NOMBRE DE LA LIBRERIA]`, por ejemplo: `pip uninstall Django`.

#### Crear un Proyecto de Django

Con el entorno virtual activado, se puede crear un proyecto de Django utilizando el comando `django-admin startproject [NOMBRE DEL PROYECTO] .`, el punto al final es para crear el proyecto en la raiz y no crear una sub-carpeta, por ejemplo: `django-admin startproject blogNoticias .`.

#### Iniciar el Proyecto Instalado

Para iniciar el proyecto instalado, con el entorno virtual activado y estando dentro de la carpeta del proyecto, se puede ejecutar el comando `python3 [NOMBRE DEL PROYECTO] runserver`, por ejemplo: `python3 blogNoticias runserver` [1](https://docs.python.org/es/3/using/windows.html).

#### Salir del Servidor Funcionando

Para salir del servidor de pruebas de Django, se debe dirigirse a la terminal o la consola de comandos donde se está ejecutando el servidor y ejecutar la secuencia de teclas: `CTRL + C` [1](https://docs.python.org/es/3/using/windows.html).

#### Ejecutar las Migraciones Después de Crear el Proyecto

Para crear la tabla de usuarios del sistema, se puede ejecutar el comando `python3 manage.py migrate`.

#### Crear una Aplicación en el Proyecto

Para crear una aplicación en el proyecto, se puede ejecutar cualquiera de los dos comandos: `python3 manage.py startapp [NOMBRE DE APP]` o `django-admin startapp [NOMBRE DE APP]`, por ejemplo: `python3 manage.py startapp core` [1](https://docs.python.org/es/3/using/windows.html).

#### Crear un Superusuario Administrador

Para crear un superusuario administrador, se puede ejecutar el comando `python3 manage.py createsuperuser`.

#### Ejecutar las Migraciones Después de Crear Modelos en una Aplicación

Luego de crear una aplicación, quizás definamos modelos en dicha aplicación. Para que éstas queden alojadas en la base de datos, tenemos que ejecutar estos dos comandos de manjera secuencial: `python3 manage.py makemigrations [NOMBRE DE LA APLICACION]
python3 manage.py migrate [NOMBRE DE LA APLICACION]`