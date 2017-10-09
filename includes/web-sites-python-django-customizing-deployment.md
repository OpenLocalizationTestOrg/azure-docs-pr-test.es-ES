Azure determinará que la aplicación use Python **si se cumplen estas condiciones**:

* archivo Requirements.txt en la carpeta raíz de Hola
* cualquier archivo .py en la carpeta raíz de Hola o runtime.txt que especifica python

Una vez que el caso de hello, usará un script de implementación específica de Python, que lleva a cabo Hola estándar sincronización de archivos, así como operaciones adicionales de Python, como:

* la administración automática del entorno virtual,
* la instalación de paquetes que aparecen en requirements.txt con pip,
* Creación de hello web.config adecuado en función de hello seleccionado versión de Python.
* la recopilación de archivos estáticos para aplicaciones Django.

Puede controlar algunos aspectos de pasos de implementación predeterminado de hello sin necesidad de script de Hola toocustomize.

Si desea tooskip todos los pasos de implementación específica de Python, puede crear este archivo vacío:

    \.skipPythonDeployment

Si desea tooskip colección de archivos estáticos de la aplicación Django:

    \.skipDjango 

Para tener más control sobre la implementación, puede invalidar el script de implementación predeterminado de hello mediante la creación de hello siguientes archivos:

    \.deployment
    \deploy.cmd

Puede usar hello [interfaz de línea de comandos de Azure] [ Azure command-line interface] toocreate archivos de Hola.  Use este comando desde la carpeta del proyecto:

    azure site deploymentscript --python

Cuando estos archivos no existen, Azure crea un script de implementación temporal y lo ejecuta.  Es idéntico toohello que cree con hello comando anterior.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
