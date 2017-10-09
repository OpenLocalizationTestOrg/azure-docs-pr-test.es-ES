## <a name="build-iot-edge"></a><span data-ttu-id="055ea-101">Compilación de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="055ea-101">Build IoT Edge</span></span>

<span data-ttu-id="055ea-102">Este tutorial usa toocommunicate de módulos personalizado de borde IoT con hello solución preconfigurada de supervisión remoto.</span><span class="sxs-lookup"><span data-stu-id="055ea-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="055ea-103">Por lo tanto, debe módulos de toobuild hello borde IoT desde el código de origen personalizado.</span><span class="sxs-lookup"><span data-stu-id="055ea-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="055ea-104">Hola las secciones siguientes describe cómo tooinstall IoT borde y compilación Hola módulo IoT borde personalizado.</span><span class="sxs-lookup"><span data-stu-id="055ea-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="055ea-105">Instalación de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="055ea-105">Install IoT Edge</span></span>

<span data-ttu-id="055ea-106">Hello siguientes pasos describen cómo tooinstall Hola había compilado previamente software IoT borde en hello NUC de Intel:</span><span class="sxs-lookup"><span data-stu-id="055ea-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="055ea-107">Configurar repositorios de paquete inteligente Hola necesario mediante la ejecución Hola siguiente comandos de hello NUC de Intel:</span><span class="sxs-lookup"><span data-stu-id="055ea-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="055ea-108">Escriba `y` cuando Hola comando le pide que demasiado**incluir este canal?**.</span><span class="sxs-lookup"><span data-stu-id="055ea-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="055ea-109">Actualizar el Administrador de paquetes inteligentes Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="055ea-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="055ea-110">Instalar paquete de hello borde de IoT de Azure ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="055ea-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="055ea-111">Comprobar la instalación de hello ejecución ejemplo de Hola a "¡Hello world".</span><span class="sxs-lookup"><span data-stu-id="055ea-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="055ea-112">En este ejemplo se escribe un archivo hello world mensaje toohello log.txT cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="055ea-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="055ea-113">Hello siguientes comandos ejecutan muestra de Hola a "¡Hello world":</span><span class="sxs-lookup"><span data-stu-id="055ea-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="055ea-114">Omitir cualquier cambio **argumento no válido** mensajes cuando se detiene la muestra de Hola.</span><span class="sxs-lookup"><span data-stu-id="055ea-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="055ea-115">Usar hello después el contenido de comando tooview Hola Hola del archivo de registro:</span><span class="sxs-lookup"><span data-stu-id="055ea-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="055ea-116">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="055ea-116">Troubleshooting</span></span>

<span data-ttu-id="055ea-117">Si recibe el error Hola "ningún paquete proporciona util-linux-dev", pruebe a reiniciar hello NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="055ea-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
