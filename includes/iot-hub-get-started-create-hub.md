## <a name="create-an-iot-hub"></a><span data-ttu-id="552e9-101">Crear un centro de IoT</span><span class="sxs-lookup"><span data-stu-id="552e9-101">Create an IoT hub</span></span>
<span data-ttu-id="552e9-102">Crear un centro de IoT para su tooconnect de aplicación de dispositivo simulado para.</span><span class="sxs-lookup"><span data-stu-id="552e9-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="552e9-103">Hello pasos siguientes muestran cómo toocomplete esta tarea al usar Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="552e9-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="552e9-104">Inicie sesión en toohello [portal de Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="552e9-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="552e9-105">Hola Jumpbar, haga clic en **New** > **Internet de las cosas** > **centro de IoT**.</span><span class="sxs-lookup"><span data-stu-id="552e9-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Barra de accesos del Portal de Azure][1]
1. <span data-ttu-id="552e9-107">Hola **centro de IoT** hoja, elija Configuración de hello para el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="552e9-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Hoja del Centro de IoT][2]
   
   1. <span data-ttu-id="552e9-109">Hola **nombre** cuadro, escriba un nombre para el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="552e9-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="552e9-110">Si hello **nombre** es válida y está disponible, aparece una marca de verificación verde en hello **nombre** cuadro.</span><span class="sxs-lookup"><span data-stu-id="552e9-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="552e9-111">Seleccione un [plan de tarifa y escalado][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="552e9-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="552e9-112">Este tutorial no requiere ningún nivel determinado.</span><span class="sxs-lookup"><span data-stu-id="552e9-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="552e9-113">Para este tutorial, use el nivel gratuito de F1 de Hola.</span><span class="sxs-lookup"><span data-stu-id="552e9-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="552e9-114">En **Grupo de recursos**, cree un grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="552e9-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="552e9-115">Para obtener más información, consulte [utilizando recurso agrupa los recursos de Azure de toomanage][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="552e9-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="552e9-116">En **ubicación**, seleccione Hola toohost de ubicación de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="552e9-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="552e9-117">Para este tutorial, elija la ubicación más cercana.</span><span class="sxs-lookup"><span data-stu-id="552e9-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="552e9-118">Cuando haya elegido las opciones de configuración del Centro de IoT, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="552e9-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="552e9-119">Puede tardar unos minutos para Azure toocreate su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="552e9-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="552e9-120">estado de hello toocheck, puede supervisar el progreso de hello en el panel de inicio de Hola o en el panel de las notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="552e9-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Estado del nuevo Centro de IoT][3]
1. <span data-ttu-id="552e9-122">Cuando se ha creado correctamente el centro de IoT hello, haga clic en nuevo icono de hello para el centro de IoT en hoja de hello tooopen portal Azure de hello para el nuevo centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="552e9-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="552e9-123">Tome nota de hello **Hostname**y, a continuación, haga clic en **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="552e9-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Nueva hoja del Centro de IoT][4]
1. <span data-ttu-id="552e9-125">Hola **directivas de acceso compartido** hoja, haga clic en hello **iothubowner** directiva y, a continuación, copie y tome nota de la cadena de conexión de centro de IoT Hola Hola **iothubowner** hoja.</span><span class="sxs-lookup"><span data-stu-id="552e9-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="552e9-126">Para obtener más información, consulte [el control de acceso] [ lnk-access-control] Hola "Guía del desarrollador de centro de IoT".</span><span class="sxs-lookup"><span data-stu-id="552e9-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![Hoja de directivas de acceso compartido][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
