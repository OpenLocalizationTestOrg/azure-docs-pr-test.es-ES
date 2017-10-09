## <a name="install-hello-prerequisites"></a>Instalar requisitos previos de Hola

1. Instale [Visual Studio 2015 o 2017](https://www.visualstudio.com). Puede usar hello libre Community Edition si se cumplen los requisitos de licencia de Hola. Ser seguro tooinclude Visual C++ y el Administrador de paquetes de NuGet.

1. Instalar [git](http://www.git-scm.com) y asegúrese de que puede ejecutar git.exe desde la línea de comandos de Hola.

1. Instalar [CMake](https://cmake.org/download/) y asegúrese de que puede ejecutar cmake.exe desde la línea de comandos de Hola. Se recomienda usar CMake versión 3.7.2 o posterior. Hola **.msi** installer es la opción más sencilla de hello en Windows. Agregar CMake toohello ruta de acceso para al menos Hola usuario actual cuando Hola instalador le preguntará.

1. Instale [Python 2.7](https://www.python.org/downloads/release/python-27). Asegúrese de agregar Python tooyour `PATH` variable de entorno en **el Panel de Control -> sistema -> Opciones avanzadas configuración del sistema -> Variables de entorno**.

1. En un símbolo del sistema, ejecute hello siguiendo el equipo local del tooyour de repositorio de comando tooclone hello Azure IoT borde GitHub:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>¿Cómo toobuild Hola ejemplo

Ahora puede compilar hello borde IoT en tiempo de ejecución y ejemplos en el equipo local:

1. Abra un **símbolo del sistema para desarrolladores de VS2015** o un **símbolo del sistema para desarrolladores de VS2017**.

1. Desplazarse por las carpetas raíz de toohello en su copia local de hello **iot borde** repositorio.

1. Ejecute el script de compilación como sigue:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Este script crea un archivo de solución de Visual Studio y compile Hola solución. Encontrará la solución de Visual Studio de hello en hello **generar** carpeta de la copia local de hello **iot borde** repositorio. Si desea toobuild y ejecutar pruebas unitarias de hello, agregar hello `--run-unittests` parámetro. Si desea toobuild y ejecutar pruebas de hello final tooend, agregar hello `--run-e2e-tests`.

> [!NOTE]
> Cada vez que ejecute hello **build.cmd** secuencia de comandos, elimina y, a continuación, vuelve a crear hello **compilar** carpeta raíz de Hola de su copia local de hello **iot borde** repositorio.
