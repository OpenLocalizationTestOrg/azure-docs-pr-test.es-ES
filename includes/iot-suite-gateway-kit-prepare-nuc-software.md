## <a name="build-iot-edge"></a><span data-ttu-id="20bbb-101">Compilación de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="20bbb-101">Build IoT Edge</span></span>

<span data-ttu-id="20bbb-102">Este tutorial usa módulos personalizados de IoT Edge para comunicarse con la solución preconfigurada de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="20bbb-102">This tutorial uses custom IoT Edge modules to communicate with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="20bbb-103">Por tanto, es necesario compilar los módulos de IoT Edge desde el código fuente personalizado.</span><span class="sxs-lookup"><span data-stu-id="20bbb-103">Therefore, you need to build the IoT Edge modules from custom source code.</span></span> <span data-ttu-id="20bbb-104">Las secciones siguientes describen cómo instalar IoT Edge y compilar el módulo personalizado de IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="20bbb-104">The following sections describe how to install IoT Edge and build the custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="20bbb-105">Instalación de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="20bbb-105">Install IoT Edge</span></span>

<span data-ttu-id="20bbb-106">Los pasos siguientes describen cómo instalar el software precompilado de IoT Edge en un Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="20bbb-106">The following steps describe how to install the pre-compiled IoT Edge software on the Intel NUC:</span></span>

1. <span data-ttu-id="20bbb-107">Configure los repositorios necesarios de Smart Package mediante la ejecución de los comandos siguientes en el Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="20bbb-107">Configure the required smart package repositories by running the following commands on the Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="20bbb-108">Escriba `y` cuando el comando le pregunte **Include this channel?** (¿Incluir este canal?).</span><span class="sxs-lookup"><span data-stu-id="20bbb-108">Enter `y` when the command prompts you to **Include this channel?**.</span></span>

1. <span data-ttu-id="20bbb-109">Actualice Smart Package Manager ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="20bbb-109">Update the smart package manager by running the following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="20bbb-110">Instale el paquete de Azure IoT Edge ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="20bbb-110">Install the Azure IoT Edge package by running the following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="20bbb-111">Compruebe la instalación ejecutando el ejemplo "Hola mundo".</span><span class="sxs-lookup"><span data-stu-id="20bbb-111">Verify the installation by running the "Hello world" sample.</span></span> <span data-ttu-id="20bbb-112">Este ejemplo escribe el mensaje Hola mundo en el archivo log.txt cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="20bbb-112">This sample writes a hello world message to the log.txT file every five seconds.</span></span> <span data-ttu-id="20bbb-113">Los comandos siguientes ejecutan el ejemplo "Hola mundo":</span><span class="sxs-lookup"><span data-stu-id="20bbb-113">The following commands run the "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="20bbb-114">Ignore cualquier mensaje de **argumento no válido** que se produzca al detener el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="20bbb-114">Ignore any **invalid argument** messages when you stop the sample.</span></span>

    <span data-ttu-id="20bbb-115">Use el comando siguiente para ver el contenido del archivo de registro:</span><span class="sxs-lookup"><span data-stu-id="20bbb-115">Use the following command to view the contents of the log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="20bbb-116">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="20bbb-116">Troubleshooting</span></span>

<span data-ttu-id="20bbb-117">Reinicie el dispositivo Intel NUC si ve el siguiente error: "no package provides util-linux-dev" (ningún paquete proporciona util-linux-dev).</span><span class="sxs-lookup"><span data-stu-id="20bbb-117">If you receive the error "No package provides util-linux-dev", try rebooting the Intel NUC.</span></span>
