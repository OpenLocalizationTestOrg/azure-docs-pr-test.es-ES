## <a name="build-iot-edge"></a>Compilación de IoT Edge

Este tutorial usa toocommunicate de módulos personalizado de borde IoT con hello solución preconfigurada de supervisión remoto. Por lo tanto, debe módulos de toobuild hello borde IoT desde el código de origen personalizado. Hola las secciones siguientes describe cómo tooinstall IoT borde y compilación Hola módulo IoT borde personalizado.

### <a name="install-iot-edge"></a>Instalación de IoT Edge

Hello siguientes pasos describen cómo tooinstall Hola había compilado previamente software IoT borde en hello NUC de Intel:

1. Configurar repositorios de paquete inteligente Hola necesario mediante la ejecución Hola siguiente comandos de hello NUC de Intel:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Escriba `y` cuando Hola comando le pide que demasiado**incluir este canal?**.

1. Actualizar el Administrador de paquetes inteligentes Hola ejecutando Hola siguiente comando:

    ```bash
    smart update
    ```

1. Instalar paquete de hello borde de IoT de Azure ejecutando el siguiente comando de hello:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Comprobar la instalación de hello ejecución ejemplo de Hola a "¡Hello world". En este ejemplo se escribe un archivo hello world mensaje toohello log.txT cada cinco segundos. Hello siguientes comandos ejecutan muestra de Hola a "¡Hello world":

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Omitir cualquier cambio **argumento no válido** mensajes cuando se detiene la muestra de Hola.

    Usar hello después el contenido de comando tooview Hola Hola del archivo de registro:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Solución de problemas

Si recibe el error Hola "ningún paquete proporciona util-linux-dev", pruebe a reiniciar hello NUC de Intel.
