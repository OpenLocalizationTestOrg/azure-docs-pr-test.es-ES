## <a name="create-an-iot-hub"></a><span data-ttu-id="458e0-101">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="458e0-101">Create an IoT hub</span></span>

1. <span data-ttu-id="458e0-102">Hola [portal de Azure](https://portal.azure.com/), haga clic en **New** > **Internet de las cosas** > **centro de IoT**.</span><span class="sxs-lookup"><span data-stu-id="458e0-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Crear un centro de IoT en hello portal de Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="458e0-104">Hola **centro de IoT** panel, escriba la siguiente información para su centro de IoT de Hola:</span><span class="sxs-lookup"><span data-stu-id="458e0-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="458e0-105">**Nombre**: escriba Hola nombre de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="458e0-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="458e0-106">Si el nombre de Hola que escribió es válida, aparece una marca de verificación verde.</span><span class="sxs-lookup"><span data-stu-id="458e0-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="458e0-107">**Nivel de precios y de escala**: Hola seleccione **F1 - libre** capa.</span><span class="sxs-lookup"><span data-stu-id="458e0-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="458e0-108">Esta opción es suficiente para esta demostración.</span><span class="sxs-lookup"><span data-stu-id="458e0-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="458e0-109">Para obtener más información, vea hello [nivel de precios y escala](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="458e0-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="458e0-110">**Grupo de recursos**: crear un centro de IoT de recursos grupo toohost Hola o utilizar uno existente.</span><span class="sxs-lookup"><span data-stu-id="458e0-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="458e0-111">Para obtener más información, consulte [grupos de recursos de uso toomanage los recursos de Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="458e0-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="458e0-112">**Ubicación**: seleccione Hola más cercano tooyou ubicación donde se crea el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="458e0-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="458e0-113">**PIN toodashboard**: seleccione esta opción para el centro de IoT tooyour de fácil acceso desde el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e0-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Escriba información toocreate su centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="458e0-115">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="458e0-115">Click **Create**.</span></span> <span data-ttu-id="458e0-116">El centro de IoT podría tardar toocreate unos minutos.</span><span class="sxs-lookup"><span data-stu-id="458e0-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="458e0-117">Puede ver el progreso en hello **notificaciones** panel.</span><span class="sxs-lookup"><span data-stu-id="458e0-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Ver las notificaciones de progreso para el centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="458e0-119">Después de crea el centro de IoT, haga clic en él en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e0-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="458e0-120">Tome nota de hello **Hostname**y, a continuación, haga clic en **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="458e0-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Obtener nombre de host de Hola de su centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="458e0-122">Hola **directivas de acceso compartido** panel, haga clic en hello **iothubowner** directiva y, a continuación, copia y ha anotado de hello **cadena de conexión** de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="458e0-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="458e0-123">Para obtener más información, consulte [tooIoT de acceso de Control concentrador](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="458e0-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="458e0-124">En este tutorial de configuración, no necesita esta cadena de conexión iothubowner.</span><span class="sxs-lookup"><span data-stu-id="458e0-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="458e0-125">Sin embargo, puede necesitarlo para algunos de los tutoriales de hello en diferentes escenarios de IoT después de completar esta instalación.</span><span class="sxs-lookup"><span data-stu-id="458e0-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Obtener la cadena de conexión del centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="458e0-127">Registrar un dispositivo en el centro de IoT de hello para el dispositivo</span><span class="sxs-lookup"><span data-stu-id="458e0-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="458e0-128">Hola [portal de Azure](https://portal.azure.com/), abra el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="458e0-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="458e0-129">Haga clic en **Explorador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="458e0-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="458e0-130">En el panel del explorador de dispositivo de hello, haga clic en **agregar** tooadd un centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="458e0-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="458e0-131">A continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="458e0-131">Then do hello following:</span></span>

   <span data-ttu-id="458e0-132">**Id. de dispositivo**: escriba el identificador de Hola de nuevo dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e0-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="458e0-133">Los identificadores de dispositivos distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="458e0-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="458e0-134">**Tipo de autenticación**: seleccione **Clave simétrica**.</span><span class="sxs-lookup"><span data-stu-id="458e0-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="458e0-135">**Generar claves automáticamente**: active esta casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="458e0-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="458e0-136">**Conectar dispositivo tooIoT concentrador**: haga clic en **habilitar**.</span><span class="sxs-lookup"><span data-stu-id="458e0-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Agregar un dispositivo en el Explorador de dispositivos de su centro de IoT Hola](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="458e0-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="458e0-138">Click **Save**.</span></span>
5. <span data-ttu-id="458e0-139">Una vez creado el dispositivo de hello, abrir el dispositivo de Hola Hola **dispositivo explorador** panel.</span><span class="sxs-lookup"><span data-stu-id="458e0-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="458e0-140">Tome nota de la clave principal de Hola de cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="458e0-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Obtener la cadena de conexión de dispositivo de Hola](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
