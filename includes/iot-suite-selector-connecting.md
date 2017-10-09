> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c6ec-101">C en Windows</span><span class="sxs-lookup"><span data-stu-id="3c6ec-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="3c6ec-102">C en Linux</span><span class="sxs-lookup"><span data-stu-id="3c6ec-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="3c6ec-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c6ec-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="3c6ec-104">Información general de escenario</span><span class="sxs-lookup"><span data-stu-id="3c6ec-104">Scenario overview</span></span>
<span data-ttu-id="3c6ec-105">En este escenario, se crea un dispositivo que envía Hola después de supervisión remota de telemetría toohello [preconfigurado solución][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="3c6ec-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="3c6ec-106">Temperatura exterior</span><span class="sxs-lookup"><span data-stu-id="3c6ec-106">External temperature</span></span>
* <span data-ttu-id="3c6ec-107">Temperatura interior</span><span class="sxs-lookup"><span data-stu-id="3c6ec-107">Internal temperature</span></span>
* <span data-ttu-id="3c6ec-108">Humedad</span><span class="sxs-lookup"><span data-stu-id="3c6ec-108">Humidity</span></span>

<span data-ttu-id="3c6ec-109">Para simplificar, valores de ejemplo genera el código de hello en dispositivo hello, pero recomendamos ejemplo Hola tooextend: conectar dispositivo tooyour de sensores real y enviar telemetría real.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="3c6ec-110">dispositivo de Hello también es toomethods toorespond puede invocar desde el panel de la solución de Hola y desea valores de propiedad establecidos en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="3c6ec-111">toocomplete este tutorial, necesita una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="3c6ec-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3c6ec-113">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="3c6ec-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3c6ec-114">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="3c6ec-114">Before you start</span></span>
<span data-ttu-id="3c6ec-115">Antes de escribir ningún código para el dispositivo, debe aprovisionar la solución preconfigurada de supervisión remota y aprovisionar un nuevo dispositivo personalizado en esa solución.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="3c6ec-116">Aprovisionar su solución preconfigurada de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="3c6ec-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="3c6ec-117">dispositivo de Hola que creará en este tutorial envía la instancia de datos de tooan de hello [supervisión remota] [ lnk-remote-monitoring] preconfigurado solución.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="3c6ec-118">Si aún no aprovisionada Hola supervisión solución preconfigurada en su cuenta de Azure remota, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3c6ec-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="3c6ec-119">En hello <https://www.azureiotsuite.com/> página, haga clic en  **+**  toocreate una solución.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="3c6ec-120">Haga clic en **seleccione** en hello **supervisión remota** panel toocreate la solución.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="3c6ec-121">En hello **crear remoto solución de supervisión** página, escriba un **nombre de la solución** de su elección, seleccione hello **región** desee toodeploy a y seleccione hello Azure suscripción toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="3c6ec-122">Haga clic en **Crear solución**.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="3c6ec-123">Espere hasta que se complete el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="3c6ec-124">las soluciones de Hello preconfigurado usan los servicios de Azure facturables.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="3c6ec-125">Asegúrese de tooremove Hola solución preconfigurada de la suscripción cuando haya terminado con él tooavoid los cargos innecesarios.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="3c6ec-126">Puede quitar completamente una solución preconfigurada de su suscripción visitando hello <https://www.azureiotsuite.com/> página.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="3c6ec-127">Cuando finalice el proceso para hello remoto de solución de supervisión de aprovisionamiento de hello, haga clic en **iniciar** tooopen panel de solución de hello en el explorador.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Panel de soluciones][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="3c6ec-129">Aprovisionar el dispositivo en hello remoto de solución de supervisión</span><span class="sxs-lookup"><span data-stu-id="3c6ec-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="3c6ec-130">Si ya ha aprovisionado un dispositivo en la solución, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="3c6ec-131">Necesita credenciales de dispositivo de hello tooknow cuando se crea la aplicación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="3c6ec-132">Para una solución de toohello preconfigurado tooconnect de dispositivo, debe identificarse tooIoT concentrador con credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="3c6ec-133">Puede recuperar las credenciales del dispositivo Hola de panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="3c6ec-134">Incluye las credenciales del dispositivo hello en la aplicación de cliente más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="3c6ec-135">tooadd una solución de supervisión remota de tooyour de dispositivo, Hola completa siguiendo los pasos en el panel de la solución de hello:</span><span class="sxs-lookup"><span data-stu-id="3c6ec-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="3c6ec-136">En hello esquina izquierda inferior del panel de hello, haga clic en **agregar un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Agregar un dispositivo][1]
2. <span data-ttu-id="3c6ec-138">Hola **dispositivo personalizado** del panel, haga clic en **agregar nueva**.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Agregar un dispositivo personalizado][2]
3. <span data-ttu-id="3c6ec-140">Elija **Permitirme definir mi propio id. de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="3c6ec-141">Escriba un Id. de dispositivo como **mydevice**, haga clic en **Check ID** tooverify ese nombre no está en uso y, a continuación, haga clic en **crear** dispositivo de tooprovision Hola.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Agregar id. de dispositivo][3]
4. <span data-ttu-id="3c6ec-143">Hacer que un dispositivo de hello tenga en cuenta las credenciales (Id. de dispositivo, el nombre de host de IoT Hub y clave de dispositivo).</span><span class="sxs-lookup"><span data-stu-id="3c6ec-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="3c6ec-144">La aplicación cliente necesita estos toohello de tooconnect valores remoto de solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="3c6ec-145">A continuación, haga clic en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-145">Then click **Done**.</span></span>
   
    ![Ver las credenciales del dispositivo][4]
5. <span data-ttu-id="3c6ec-147">Seleccione el dispositivo en la lista de dispositivos de hello en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="3c6ec-148">A continuación, en hello **detalles del dispositivo** del panel, haga clic en **Habilitar dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="3c6ec-149">Hola estado del dispositivo es ahora **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="3c6ec-150">solución de supervisión remoto Hello ahora puede reciba datos de telemetría del dispositivo e invocar métodos de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c6ec-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/