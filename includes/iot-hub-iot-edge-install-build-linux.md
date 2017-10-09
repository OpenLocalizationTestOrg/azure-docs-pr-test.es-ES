## <a name="install-hello-prerequisites"></a>Instalar requisitos previos de Hola

pasos de Hello en este tutorial supone que está ejecutando Ubuntu Linux.

Abra un shell y ejecute Hola después de paquetes de requisitos previos de Hola de tooinstall de comandos:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

En el shell de hello, ejecute hello siguiendo el equipo local del tooyour de repositorio de comando tooclone hello Azure IoT borde GitHub:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>¿Cómo toobuild Hola ejemplo

Ahora puede compilar hello borde IoT en tiempo de ejecución y ejemplos en el equipo local:

1. Abra un shell.

1. Desplazarse por las carpetas raíz de toohello en su copia local de hello **iot borde** repositorio.

1. Ejecute el script de compilación como sigue:

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Esta secuencia de comandos utiliza el **cmake** toocreate utilidad una carpeta llamada **generar** en carpeta de raíz de hello de la copia local de la **iot borde** repositorio y generar un archivo MAKE. script de Hola, a continuación, compile la solución de hello, omitiendo las pruebas unitarias y pruebas de tooend final. Si desea toobuild y ejecutar pruebas unitarias de hello, agregar hello `--run-unittests` parámetro. Si desea toobuild y ejecutar pruebas de hello final tooend, agregar hello `--run-e2e-tests`.

> [!NOTE]
> Cada vez que ejecute hello **build.sh** secuencia de comandos, elimina y, a continuación, vuelve a crear hello **compilar** carpeta raíz de Hola de su copia local de hello **iot borde** repositorio.
