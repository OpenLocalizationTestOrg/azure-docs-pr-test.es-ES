## <a name="install-hello-prerequisites"></a><span data-ttu-id="11af6-101">Instalar requisitos previos de Hola</span><span class="sxs-lookup"><span data-stu-id="11af6-101">Install hello prerequisites</span></span>

<span data-ttu-id="11af6-102">pasos de Hello en este tutorial supone que está ejecutando Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="11af6-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="11af6-103">Abra un shell y ejecute Hola después de paquetes de requisitos previos de Hola de tooinstall de comandos:</span><span class="sxs-lookup"><span data-stu-id="11af6-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="11af6-104">En el shell de hello, ejecute hello siguiendo el equipo local del tooyour de repositorio de comando tooclone hello Azure IoT borde GitHub:</span><span class="sxs-lookup"><span data-stu-id="11af6-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="11af6-105">¿Cómo toobuild Hola ejemplo</span><span class="sxs-lookup"><span data-stu-id="11af6-105">How toobuild hello sample</span></span>

<span data-ttu-id="11af6-106">Ahora puede compilar hello borde IoT en tiempo de ejecución y ejemplos en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="11af6-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="11af6-107">Abra un shell.</span><span class="sxs-lookup"><span data-stu-id="11af6-107">Open a shell.</span></span>

1. <span data-ttu-id="11af6-108">Desplazarse por las carpetas raíz de toohello en su copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="11af6-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="11af6-109">Ejecute el script de compilación como sigue:</span><span class="sxs-lookup"><span data-stu-id="11af6-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="11af6-110">Esta secuencia de comandos utiliza el **cmake** toocreate utilidad una carpeta llamada **generar** en carpeta de raíz de hello de la copia local de la **iot borde** repositorio y generar un archivo MAKE.</span><span class="sxs-lookup"><span data-stu-id="11af6-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="11af6-111">script de Hola, a continuación, compile la solución de hello, omitiendo las pruebas unitarias y pruebas de tooend final.</span><span class="sxs-lookup"><span data-stu-id="11af6-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="11af6-112">Si desea toobuild y ejecutar pruebas unitarias de hello, agregar hello `--run-unittests` parámetro.</span><span class="sxs-lookup"><span data-stu-id="11af6-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="11af6-113">Si desea toobuild y ejecutar pruebas de hello final tooend, agregar hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="11af6-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="11af6-114">Cada vez que ejecute hello **build.sh** secuencia de comandos, elimina y, a continuación, vuelve a crear hello **compilar** carpeta raíz de Hola de su copia local de hello **iot borde** repositorio.</span><span class="sxs-lookup"><span data-stu-id="11af6-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
