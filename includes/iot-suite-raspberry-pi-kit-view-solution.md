## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="cccc1-101">Panel de vista Hola solución</span><span class="sxs-lookup"><span data-stu-id="cccc1-101">View hello solution dashboard</span></span>

<span data-ttu-id="cccc1-102">panel de la solución de Hello permite toomanage solución de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="cccc1-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="cccc1-103">Por ejemplo, puede ver la telemetría, agregar dispositivos e invocar métodos.</span><span class="sxs-lookup"><span data-stu-id="cccc1-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="cccc1-104">Cuando el aprovisionamiento de hello está completado e indica el icono de Hola para su solución preconfigurada **listo**, elija **iniciar** tooopen su portal de solución de supervisión remoto en una nueva pestaña.</span><span class="sxs-lookup"><span data-stu-id="cccc1-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Iniciar solución de hello preconfigurado][img-launch-solution]

1. <span data-ttu-id="cccc1-106">De forma predeterminada, el portal de solución de hello muestra hello *panel*.</span><span class="sxs-lookup"><span data-stu-id="cccc1-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="cccc1-107">Puede navegar por las áreas de tooother del portal de solución de hello con menú de hello en el lado izquierdo de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="cccc1-107">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Panel de la solución preconfigurada de supervisión remota][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="cccc1-109">Agregar un dispositivo</span><span class="sxs-lookup"><span data-stu-id="cccc1-109">Add a device</span></span>

<span data-ttu-id="cccc1-110">Para una solución de toohello preconfigurado tooconnect de dispositivo, debe identificarse tooIoT concentrador con credenciales válidas.</span><span class="sxs-lookup"><span data-stu-id="cccc1-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="cccc1-111">Puede recuperar las credenciales del dispositivo Hola de panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="cccc1-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="cccc1-112">Incluye las credenciales del dispositivo hello en la aplicación de cliente más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cccc1-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="cccc1-113">Si aún no lo ha hecho, agregue una solución de supervisión remota de tooyour de dispositivo personalizado.</span><span class="sxs-lookup"><span data-stu-id="cccc1-113">If you haven't already done so, add a custom device tooyour remote monitoring solution.</span></span> <span data-ttu-id="cccc1-114">Hola completa siguiendo los pasos en el panel de la solución de hello:</span><span class="sxs-lookup"><span data-stu-id="cccc1-114">Complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="cccc1-115">En hello esquina izquierda inferior del panel de hello, haga clic en **agregar un dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="cccc1-115">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Agregar un dispositivo][1]

1. <span data-ttu-id="cccc1-117">Hola **dispositivo personalizado** del panel, haga clic en **agregar nueva**.</span><span class="sxs-lookup"><span data-stu-id="cccc1-117">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Agregar un dispositivo personalizado][2]

1. <span data-ttu-id="cccc1-119">Elija **Permitirme definir mi propio id. de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="cccc1-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="cccc1-120">Escriba un Id. de dispositivo como **rasppi**, haga clic en **Check ID** tooverify no has utilizado ya nombre hello en la solución y, a continuación, haga clic en **crear** dispositivo de tooprovision Hola.</span><span class="sxs-lookup"><span data-stu-id="cccc1-120">Enter a Device ID such as **rasppi**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Agregar id. de dispositivo][3]

1. <span data-ttu-id="cccc1-122">Hacer que un dispositivo de hello Nota credenciales (**Id. de dispositivo**, **IoT Hub Hostname**, y **clave de dispositivo**).</span><span class="sxs-lookup"><span data-stu-id="cccc1-122">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="cccc1-123">La aplicación de cliente en hello frambuesa Pi necesita estos toohello de tooconnect valores remoto de solución de supervisión.</span><span class="sxs-lookup"><span data-stu-id="cccc1-123">Your client application on hello Raspberry Pi needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="cccc1-124">A continuación, haga clic en **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="cccc1-124">Then click **Done**.</span></span>

    ![Ver las credenciales del dispositivo][4]

1. <span data-ttu-id="cccc1-126">Seleccione el dispositivo en la lista de dispositivos de hello en el panel de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="cccc1-126">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="cccc1-127">A continuación, en hello **detalles del dispositivo** del panel, haga clic en **Habilitar dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="cccc1-127">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="cccc1-128">Hola estado del dispositivo es ahora **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="cccc1-128">hello status of your device is now **Running**.</span></span> <span data-ttu-id="cccc1-129">solución de supervisión remoto Hello ahora puede reciba datos de telemetría del dispositivo e invocar métodos de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cccc1-129">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png