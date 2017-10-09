## <a name="create-a-device-identity"></a><span data-ttu-id="d2b9e-101">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="d2b9e-101">Create a device identity</span></span>

<span data-ttu-id="d2b9e-102">En esta sección, utilice hello [portal de Azure] [ lnk-azure-portal] toocreate una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="d2b9e-103">Un dispositivo no puede conectar tooIoT concentrador a menos que tenga una entrada en el registro de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="d2b9e-104">Para obtener más información, vea la sección de "Registro de identidad" de Hola de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d2b9e-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d2b9e-105">Hola **dispositivo explorador** de hello portal le ayudará a generar un identificador de dispositivo único y una clave que el dispositivo pueda usar tooidentify sí mismo cuando se conecta tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="d2b9e-106">Los identificadores de dispositivos distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="d2b9e-107">Asegúrese de que ha iniciado sesión toohello [portal de Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d2b9e-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="d2b9e-108">Hola Jumpbar, haga clic en **todos los recursos** y se encuentra el recurso de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Navegar por el centro de Iot tooyour][img-find-iothub]

1. <span data-ttu-id="d2b9e-110">Cuando se abre el recurso de centro de IoT, haga clic en hello **dispositivo explorador** de herramientas y, a continuación, haga clic en **agregar** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="d2b9e-111">Proporcione el nombre de hello para el nuevo dispositivo, como **myDeviceId**y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Creación de la identidad del dispositivo en el portal][img-create-device]

   <span data-ttu-id="d2b9e-113">Se crea una nueva identidad de dispositivo para su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="d2b9e-114">Hola **dispositivo explorador**de lista de dispositivos, haga clic en el dispositivo de hello recién creado y tome nota de hello **cadena de conexión---clave principal**.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Cadena de conexión de dispositivo][img-connection-string]

> [!NOTE]
> <span data-ttu-id="d2b9e-116">Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d2b9e-117">Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d2b9e-118">Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="d2b9e-119">Consulte la [guía para desarrolladores de IoT Hub][lnk-devguide-identity] para más información.</span><span class="sxs-lookup"><span data-stu-id="d2b9e-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

