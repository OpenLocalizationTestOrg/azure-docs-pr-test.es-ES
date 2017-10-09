## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="67ce7-101">Configurar dispositivo simulado de hello Node.js</span><span class="sxs-lookup"><span data-stu-id="67ce7-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="67ce7-102">En el panel de supervisión remota de hello, haga clic en **+ agregar un dispositivo** y, a continuación, agregue un *dispositivo personalizado*.</span><span class="sxs-lookup"><span data-stu-id="67ce7-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="67ce7-103">Tome nota del centro de IoT Hola hostname, Id. de dispositivo y una clave de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="67ce7-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="67ce7-104">Se necesita más adelante en este tutorial cuando se prepara una aplicación de cliente de dispositivo de hello remote_monitoring.js.</span><span class="sxs-lookup"><span data-stu-id="67ce7-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="67ce7-105">Asegúrese de que tiene instalada la versión 0.12.x o posterior de Node.js en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="67ce7-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="67ce7-106">Ejecutar `node --version` en un símbolo del sistema o en una versión de hello toocheck de shell.</span><span class="sxs-lookup"><span data-stu-id="67ce7-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="67ce7-107">Para obtener información sobre el uso de un tooinstall de administrador de paquetes Node.js en Linux, consulte [instalar Node.js a través del Administrador de paquetes][node-linux].</span><span class="sxs-lookup"><span data-stu-id="67ce7-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="67ce7-108">Cuando haya instalado Node.js, clonar la versión más reciente de Hola de hello [azure iot sdk nodos] [ lnk-github-repo] equipo de desarrollo de tooyour de repositorio.</span><span class="sxs-lookup"><span data-stu-id="67ce7-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="67ce7-109">Utilice siempre hello **maestro** rama para la versión más reciente de Hola de bibliotecas de Hola y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="67ce7-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="67ce7-110">Desde la copia local de hello [azure iot sdk nodos] [ lnk-github-repo] repositorio, Hola copia siguiendo dos archivos de hello nodo/dispositivo/samples tooan vacía la carpeta en el equipo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="67ce7-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="67ce7-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="67ce7-111">packages.json</span></span>
   * <span data-ttu-id="67ce7-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="67ce7-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="67ce7-113">Abra el archivo de remote_monitoring.js hello y busque Hola después de la definición de variable:</span><span class="sxs-lookup"><span data-stu-id="67ce7-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="67ce7-114">Reemplace **[IoT Hub device connection string]** con la cadena de conexión al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="67ce7-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="67ce7-115">Usar valores de hello de clave de dispositivo que se anotó en el paso 1, Id. de dispositivo y nombre de host del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="67ce7-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="67ce7-116">Una cadena de conexión de dispositivo tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="67ce7-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="67ce7-117">Si es el nombre de host del centro de IoT **contoso** y el identificador de dispositivo es **mydevice**, la cadena de conexión es similar a Hola siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="67ce7-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Guarde el archivo hello. <span data-ttu-id="67ce7-119">Ejecute hello siga los comandos en un shell o el símbolo del sistema en carpeta de Hola que contiene estos paquetes de archivos tooinstall Hola necesarios y, a continuación, ejecute la aplicación de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="67ce7-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="67ce7-120">Observación de la telemetría dinámica en acción</span><span class="sxs-lookup"><span data-stu-id="67ce7-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="67ce7-121">panel de Hello muestra telemetría de temperatura y humedad Hola desde dispositivos simulada de hello existente:</span><span class="sxs-lookup"><span data-stu-id="67ce7-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![panel de saludo predeterminado][image1]

<span data-ttu-id="67ce7-123">Si selecciona el dispositivo simulado Node.js de hello, que se ejecutaron en la sección anterior de hello, verá temperatura y humedad, telemetría de temperatura externo:</span><span class="sxs-lookup"><span data-stu-id="67ce7-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Agregar temperatura externo toohello panel][image2]

<span data-ttu-id="67ce7-125">solución de supervisión remoto Hello automáticamente detecta el tipo de telemetría de temperatura externos adicionales de Hola y lo agrega toohello gráfico en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="67ce7-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png