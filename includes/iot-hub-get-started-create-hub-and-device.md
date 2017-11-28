## <a name="create-an-iot-hub"></a><span data-ttu-id="43b8a-101">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="43b8a-101">Create an IoT hub</span></span>

1. <span data-ttu-id="43b8a-102">En [Azure Portal](https://portal.azure.com/), haga clic en **Nuevo** > **Internet de las cosas** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-102">In the [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Creación de un centro de IoT mediante Azure Portal](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="43b8a-104">En el panel **Centro de IoT**, escriba la información necesaria para su centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="43b8a-104">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

     <span data-ttu-id="43b8a-105">**Nombre**: escriba el nombre de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="43b8a-105">**Name**: Enter the name of your IoT hub.</span></span> <span data-ttu-id="43b8a-106">Si el nombre que escribe es válido, aparece una marca de verificación verde.</span><span class="sxs-lookup"><span data-stu-id="43b8a-106">If the name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="43b8a-107">**Nivel de precios y de escala**: seleccione el nivel **F1 - Gratis**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-107">**Pricing and scale tier**: Select the **F1 - Free** tier.</span></span> <span data-ttu-id="43b8a-108">Esta opción es suficiente para esta demostración.</span><span class="sxs-lookup"><span data-stu-id="43b8a-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="43b8a-109">Para más información, consulte la página de [precios de IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="43b8a-109">For more information, see the [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="43b8a-110">**Grupo de recursos**: cree un grupo de recursos para hospedar el centro de IoT o use uno existente.</span><span class="sxs-lookup"><span data-stu-id="43b8a-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="43b8a-111">Para más información, consulte [Administración de los recursos de Azure a través del Portal](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43b8a-111">For more information, see [Use resource groups to manage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="43b8a-112">**Ubicación**: seleccione la ubicación más cercana a usted donde se crea el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="43b8a-112">**Location**: Select the closest location to you where the IoT hub is created.</span></span>

     <span data-ttu-id="43b8a-113">**Anclar al panel**: seleccione esta opción para facilitar el acceso al centro de IoT desde el panel.</span><span class="sxs-lookup"><span data-stu-id="43b8a-113">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Escribir la información necesaria para crear su centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="43b8a-115">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-115">Click **Create**.</span></span> <span data-ttu-id="43b8a-116">El centro de IoT puede tardar varios minutos en crearse.</span><span class="sxs-lookup"><span data-stu-id="43b8a-116">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="43b8a-117">Puede ver el progreso en el panel **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-117">You can see progress in the **Notifications** pane.</span></span>

   ![Ver las notificaciones de progreso para el centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="43b8a-119">Después de crear el centro de IoT, haga clic en él en el panel.</span><span class="sxs-lookup"><span data-stu-id="43b8a-119">After your IoT hub is created, click it on the dashboard.</span></span> <span data-ttu-id="43b8a-120">Anote el **Nombre de host** y haga clic en **Directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-120">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>

   ![Obtener el nombre de host de su centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="43b8a-122">En el panel **Directivas de acceso compartido**, haga clic en la directiva **iothubowner** y, luego, copie y anote la **cadena de conexión** de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="43b8a-122">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub.</span></span> <span data-ttu-id="43b8a-123">Para más información, consulte [Control del acceso a IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="43b8a-123">For more information, see [Control access to IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="43b8a-124">En este tutorial de configuración, no necesita esta cadena de conexión iothubowner.</span><span class="sxs-lookup"><span data-stu-id="43b8a-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="43b8a-125">Sin embargo, puede necesitarla en algunos de los tutoriales en diferentes escenarios de IoT después de realizar esta configuración.</span><span class="sxs-lookup"><span data-stu-id="43b8a-125">However, you may need it for some of the tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Obtener la cadena de conexión del centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a><span data-ttu-id="43b8a-127">Registro de su dispositivo en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="43b8a-127">Register a device in the IoT hub for your device</span></span>

1. <span data-ttu-id="43b8a-128">En [Azure Portal](https://portal.azure.com/), abra su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="43b8a-128">In the [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="43b8a-129">Haga clic en **Explorador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="43b8a-130">En el panel Explorador del dispositivo, haga clic en **Agregar** para agregar un dispositivo a su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="43b8a-130">In the Device Explorer pane, click **Add** to add a device to your IoT hub.</span></span> <span data-ttu-id="43b8a-131">A continuación, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="43b8a-131">Then do the following:</span></span>

   <span data-ttu-id="43b8a-132">**Id. de dispositivo**: escriba el identificador del nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="43b8a-132">**Device ID**: Enter the ID of the new device.</span></span> <span data-ttu-id="43b8a-133">Los identificadores de dispositivos distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="43b8a-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="43b8a-134">**Tipo de autenticación**: seleccione **Clave simétrica**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="43b8a-135">**Generar claves automáticamente**: active esta casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="43b8a-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="43b8a-136">**Connect device to IoT Hub** (Conectar dispositivos a IoT Hub): haga clic en **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-136">**Connect device to IoT Hub**: Click **Enable**.</span></span>

   ![Agregar un dispositivo en Device Explorer de su centro de IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="43b8a-138">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-138">Click **Save**.</span></span>
5. <span data-ttu-id="43b8a-139">Después de crear el dispositivo, ábralo en el panel **Explorador de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="43b8a-139">After the device is created, open the device in the **Device Explorer** pane.</span></span>
6. <span data-ttu-id="43b8a-140">Anote la clave principal de la cadena de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="43b8a-140">Make a note of the primary key of the connection string.</span></span>

   ![Obtener la cadena de conexión del dispositivo](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
