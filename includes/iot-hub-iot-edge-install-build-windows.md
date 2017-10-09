## <a name="install-hello-prerequisites"></a><span data-ttu-id="16fc9-101">Instalar requisitos previos de Hola</span><span class="sxs-lookup"><span data-stu-id="16fc9-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="16fc9-102">Instale [Visual Studio 2015 o 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="16fc9-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="16fc9-103">Puede usar hello libre Community Edition si se cumplen los requisitos de licencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="16fc9-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="16fc9-104">Ser seguro tooinclude Visual C++ y el Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="16fc9-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="16fc9-105">Instalar [git](http://www.git-scm.com) y asegúrese de que puede ejecutar git.exe desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="16fc9-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="16fc9-106">Instalar [CMake](https://cmake.org/download/) y asegúrese de que puede ejecutar cmake.exe desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="16fc9-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="16fc9-107">Se recomienda usar CMake versión 3.7.2 o posterior.</span><span class="sxs-lookup"><span data-stu-id="16fc9-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="16fc9-108">Hola **.msi** installer es la opción más sencilla de hello en Windows.</span><span class="sxs-lookup"><span data-stu-id="16fc9-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="16fc9-109">Agregar CMake toohello ruta de acceso para al menos Hola usuario actual cuando Hola instalador le preguntará.</span><span class="sxs-lookup"><span data-stu-id="16fc9-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="16fc9-110">Instale [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="16fc9-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="16fc9-111">Asegúrese de agregar Python tooyour `PATH` variable de entorno en **el Panel de Control -> sistema -> Opciones avanzadas configuración del sistema -> Variables de entorno**.</span><span class="sxs-lookup"><span data-stu-id="16fc9-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="16fc9-112">En un símbolo del sistema, ejecute hello siguiendo el equipo local del tooyour de repositorio de comando tooclone hello Azure IoT borde GitHub:</span><span class="sxs-lookup"><span data-stu-id="16fc9-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="16fc9-113">¿Cómo toobuild Hola ejemplo</span><span class="sxs-lookup"><span data-stu-id="16fc9-113">How toobuild hello sample</span></span>

<span data-ttu-id="16fc9-114">Ahora puede compilar hello borde IoT en tiempo de ejecución y ejemplos en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="16fc9-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="16fc9-115">Abra un **símbolo del sistema para desarrolladores de VS2015** o un **símbolo del sistema para desarrolladores de VS2017**.</span><span class="sxs-lookup"><span data-stu-id="16fc9-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="16fc9-116">Desplazarse por las carpetas raíz de toohello en su copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="16fc9-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="16fc9-117">Ejecute el script de compilación como sigue:</span><span class="sxs-lookup"><span data-stu-id="16fc9-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="16fc9-118">Este script crea un archivo de solución de Visual Studio y compile Hola solución.</span><span class="sxs-lookup"><span data-stu-id="16fc9-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="16fc9-119">Encontrará la solución de Visual Studio de hello en hello **generar** carpeta de la copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="16fc9-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="16fc9-120">Si desea toobuild y ejecutar pruebas unitarias de hello, agregar hello `--run-unittests` parámetro.</span><span class="sxs-lookup"><span data-stu-id="16fc9-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="16fc9-121">Si desea toobuild y ejecutar pruebas de hello final tooend, agregar hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="16fc9-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="16fc9-122">Cada vez que ejecute hello **build.cmd** secuencia de comandos, elimina y, a continuación, vuelve a crear hello **compilar** carpeta raíz de Hola de su copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="16fc9-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
