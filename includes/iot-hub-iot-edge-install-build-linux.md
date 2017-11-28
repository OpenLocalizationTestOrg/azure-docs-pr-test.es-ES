## <a name="install-the-prerequisites"></a><span data-ttu-id="9520d-101">Instalación de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9520d-101">Install the prerequisites</span></span>

<span data-ttu-id="9520d-102">En los pasos de este tutorial se supone que está ejecutando Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="9520d-102">The steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="9520d-103">Abra un shell y ejecute los comandos siguientes para instalar los paquetes de requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="9520d-103">Open a shell and run the following commands to install the prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="9520d-104">En el shell, ejecute el siguiente comando para clonar el repositorio de GitHub de Azure IoT Edge en la máquina local:</span><span class="sxs-lookup"><span data-stu-id="9520d-104">In the shell, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="9520d-105">Compilación del ejemplo</span><span class="sxs-lookup"><span data-stu-id="9520d-105">How to build the sample</span></span>

<span data-ttu-id="9520d-106">Ya puede compilar el runtime de IoT Edge y los ejemplos en la máquina local:</span><span class="sxs-lookup"><span data-stu-id="9520d-106">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="9520d-107">Abra un shell.</span><span class="sxs-lookup"><span data-stu-id="9520d-107">Open a shell.</span></span>

1. <span data-ttu-id="9520d-108">Vaya a la carpeta raíz en la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="9520d-108">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="9520d-109">Ejecute el script de compilación como sigue:</span><span class="sxs-lookup"><span data-stu-id="9520d-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="9520d-110">Este script emplea la utilidad **cmake** para crear una carpeta llamada **build** en la carpeta raíz de la copia local del repositorio **iot-edge** y generar un archivo Make.</span><span class="sxs-lookup"><span data-stu-id="9520d-110">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="9520d-111">A continuación, el script compila la solución, omitiendo las pruebas unitarias y las pruebas completas.</span><span class="sxs-lookup"><span data-stu-id="9520d-111">The script then builds the solution, skipping unit tests and end to end tests.</span></span> <span data-ttu-id="9520d-112">Si desea compilar y ejecutar las pruebas unitarias, agregue el parámetro `--run-unittests`.</span><span class="sxs-lookup"><span data-stu-id="9520d-112">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="9520d-113">Si desea compilar y ejecutar pruebas de extremo a extremo, agregue `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="9520d-113">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="9520d-114">Cada vez que ejecute el script **build.sh**, elimina y luego vuelve a crear la carpeta **build** en la carpeta raíz de la copia local del repositorio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="9520d-114">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>