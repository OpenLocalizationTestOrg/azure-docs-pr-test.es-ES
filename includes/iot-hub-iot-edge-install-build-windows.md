## <a name="install-the-prerequisites"></a><span data-ttu-id="23a24-101">Instalación de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="23a24-101">Install the prerequisites</span></span>

1. <span data-ttu-id="23a24-102">Instale [Visual Studio 2015 o 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="23a24-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="23a24-103">Puede usar la versión gratuita Community Edition si cumple los requisitos de concesión de licencias.</span><span class="sxs-lookup"><span data-stu-id="23a24-103">You can use the free Community Edition if you meet the licensing requirements.</span></span> <span data-ttu-id="23a24-104">No olvide incluir Visual C++ y el Administrador de paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="23a24-104">Be sure to include Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="23a24-105">Instale [git](http://www.git-scm.com) y asegúrese de que puede ejecutar git.exe desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="23a24-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from the command line.</span></span>

1. <span data-ttu-id="23a24-106">Instale [CMake](https://cmake.org/download/) y asegúrese de que puede ejecutar cmake.exe desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="23a24-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from the command line.</span></span> <span data-ttu-id="23a24-107">Se recomienda usar CMake versión 3.7.2 o posterior.</span><span class="sxs-lookup"><span data-stu-id="23a24-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="23a24-108">El instalador **.msi** es la opción más sencilla en Windows.</span><span class="sxs-lookup"><span data-stu-id="23a24-108">The **.msi** installer is the easiest option on Windows.</span></span> <span data-ttu-id="23a24-109">Agregue CMake a PATH al menos para el usuario actual cuando el instalador se lo solicite.</span><span class="sxs-lookup"><span data-stu-id="23a24-109">Add CMake to the PATH for at least the current user when the installer prompts you.</span></span>

1. <span data-ttu-id="23a24-110">Instale [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="23a24-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="23a24-111">Asegúrese de que agrega Python a su variable de entorno `PATH` en el **Panel de control -> Sistema -> Configuración avanzada del sistema -> Variables de entorno**.</span><span class="sxs-lookup"><span data-stu-id="23a24-111">Make sure you add Python to your `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="23a24-112">En un símbolo del sistema, ejecute el siguiente comando para clonar el repositorio de GitHub de Azure IoT Edge en la máquina local:</span><span class="sxs-lookup"><span data-stu-id="23a24-112">At a command prompt, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="23a24-113">Compilación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="23a24-113">How to build the sample</span></span>

<span data-ttu-id="23a24-114">Ya puede compilar el runtime de IoT Edge y los ejemplos en la máquina local:</span><span class="sxs-lookup"><span data-stu-id="23a24-114">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="23a24-115">Abra un **símbolo del sistema para desarrolladores de VS2015** o un **símbolo del sistema para desarrolladores de VS2017**.</span><span class="sxs-lookup"><span data-stu-id="23a24-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="23a24-116">Vaya a la carpeta raíz en la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="23a24-116">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="23a24-117">Ejecute el script de compilación como sigue:</span><span class="sxs-lookup"><span data-stu-id="23a24-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="23a24-118">Este script crea un archivo de solución de Visual Studio y compila la solución.</span><span class="sxs-lookup"><span data-stu-id="23a24-118">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="23a24-119">Puede encontrar la solución de Visual Studio en la carpeta **build** de su copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="23a24-119">You can find the Visual Studio solution in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="23a24-120">Si desea compilar y ejecutar las pruebas unitarias, agregue el parámetro `--run-unittests`.</span><span class="sxs-lookup"><span data-stu-id="23a24-120">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="23a24-121">Si desea compilar y ejecutar pruebas de extremo a extremo, agregue `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="23a24-121">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="23a24-122">Cada vez que ejecute el script **build.cmd**, elimine y luego vuelva a crear la carpeta **build** en la carpeta raíz de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="23a24-122">Every time you run the **build.cmd** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>