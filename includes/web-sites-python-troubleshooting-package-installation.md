Algunos paquetes no pueden instalarse con pip cuando se ejecutan en Azure.  Puede ser simplemente que ese paquete hello no está disponible en hello índice del paquete Python.  Es posible que un compilador es necesario (un compilador no está disponible en hello máquina hello web aplicación en ejecución en el servicio de aplicación de Azure).

En esta sección, se examinará toodeal maneras con este problema.

### <a name="request-wheels"></a>Solicitar ruedas
Si la instalación del paquete Hola requiere que un compilador, debe intentar ponerse en contacto con toorequest Hola de propietario del paquete que estar disponibles para su paquete de hello ruedas.

Con la disponibilidad reciente Hola de [compilador de Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], ahora resulta más fácil toobuild que los paquetes con código nativo para Python 2.7.

### <a name="build-wheels-requires-windows"></a>Compilar ruedas (necesita Windows)
Nota: Cuando se usa esta opción, asegúrese de seguro de paquete de hello toocompile utilizando un entorno de Python que coincida con hello plataforma / / versión de arquitectura que se usa en la aplicación web de hello en el servicio de aplicación de Azure (Windows/32-bit/2.7 o 3.4).

Si no se instala el paquete de hello porque requiere un compilador, puede instalar el compilador de hello en el equipo local y generar una rueda para paquete de hello, que, a continuación, se incluirá en el repositorio.

Los usuarios de Mac y Linux: Si no dispone de máquina de Windows tooa de acceso, consulte [crear una máquina Virtual de Windows ejecutando] [ Create a Virtual Machine Running Windows] para saber cómo toocreate una máquina virtual en Azure.  Puede utilizar ruedas de hello toobuild, agregarlos toohello repositorio y descartar Hola VM si lo desea. 

Python 2.7, puede instalar [compilador de Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

3.4 de Python, puede instalar [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

ruedas toobuild, necesitará paquete rueda de hello:

    env\scripts\pip install wheel

Deberá usar `pip wheel` toocompile una dependencia:

    env\scripts\pip wheel azure==0.8.4

Esto crea un archivo .whl en la carpeta de \wheelhouse Hola.  Agregar carpeta de \wheelhouse de Hola y del repositorio de tooyour de archivos de rueda.

Editar el saludo de tooadd requirements.txt `--find-links` opción a la parte superior de Hola. Esto indica a pip toolook una coincidencia exacta en la carpeta local de hello antes del índice del paquete de python de curso toohello.

    --find-links wheelhouse
    azure==0.8.4

Si desea tooinclude todas las dependencias hello \wheelhouse carpeta y no use Hola paquete de python de índice en absoluto, puede forzar el índice del paquete de pip tooignore Hola agregando `--no-index` toohello superior de su requirements.txt.

    --no-index

### <a name="customize-installation"></a>Personalizar la instalación
Puede personalizar tooinstall de script de implementación de hello un paquete en el entorno virtual de hello mediante un instalador alternativo, como la forma más fácil\_instalar.  Consulte deploy.cmd para obtener un ejemplo comentado.  Asegúrese de que estos paquetes no aparezcan en requirements.txt, tooprevent pip de instalarlos.

Agregue esta secuencia de comandos de implementación de toohello:

    env\scripts\easy_install somepackage

También es posible que pueda toouse fácil\_instalar tooinstall desde un instalador exe (algunos son zip compatible, es muy fácil\_instalación es compatible con ellos).  Agregar repositorio de tooyour de instalador de hello e invocar la forma más fácil\_instalar pasando ejecutable hello toohello de ruta de acceso.

Agregue esta secuencia de comandos de implementación de toohello:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Incluir el entorno virtual de hello en el repositorio de hello (requiere Windows)
Nota: Cuando se usa esta opción, asegúrese de toouse seguro de un entorno virtual que coincida con hello plataforma / / versión de arquitectura que se usa en la aplicación web de hello en el servicio de aplicación de Azure (Windows/32-bit/2.7 o 3.4).

Si incluye el entorno virtual de hello en el repositorio de hello, puede impedir que el script de implementación de hello dedican a la administración del entorno virtual en Azure mediante la creación de un archivo vacío:

    .skipPythonDeployment

Se recomienda eliminar entorno virtual existente de hello en la aplicación hello, archivos que hayan quedado tooprevent desde al entorno virtual de Hola se administra automáticamente.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
