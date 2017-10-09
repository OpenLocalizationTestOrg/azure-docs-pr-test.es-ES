## <a name="create-a-device-identity"></a><span data-ttu-id="d5d4c-101">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="d5d4c-101">Create a device identity</span></span>
<span data-ttu-id="d5d4c-102">En esta sección, creará una aplicación de consola .NET que crea una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="d5d4c-103">Un dispositivo no puede conectar tooIoT concentrador a menos que tenga una entrada en el registro de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="d5d4c-104">Para obtener más información, vea la sección de "Registro de identidad" de Hola de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d5d4c-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d5d4c-105">Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="d5d4c-106">Los identificadores de dispositivos distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="d5d4c-107">En Visual Studio, agregue una nueva solución de Visual C# escritorio clásico de Windows proyecto tooa mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d5d4c-108">Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d5d4c-109">Proyecto de hello Name **CreateDeviceIdentity** y nombre hello solución **IoTHubGetStarted**.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10]
2. <span data-ttu-id="d5d4c-111">En el Explorador de soluciones, haga clic en hello **CreateDeviceIdentity** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="d5d4c-112">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d5d4c-113">Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][11]
4. <span data-ttu-id="d5d4c-115">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="d5d4c-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="d5d4c-116">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d5d4c-117">Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="d5d4c-118">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="d5d4c-118">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="d5d4c-119">Este método crea una identidad de dispositivo con el identificador **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="d5d4c-120">(Si este identificador de dispositivo ya existe en el registro de la identidad de hello, código de hello simplemente recupera información del dispositivo existente hello). aplicación Hello, a continuación, muestra la clave principal de Hola para esa identidad.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="d5d4c-121">Use esta clave en el centro de IoT de hello simulada dispositivos aplicación tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="d5d4c-122">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="d5d4c-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="d5d4c-123">Ejecutar esta aplicación y tome nota de la clave de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Clave de dispositivo generado por la aplicación hello][12]

> [!NOTE]
> <span data-ttu-id="d5d4c-125">Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d5d4c-126">Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d5d4c-127">Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="d5d4c-128">Consulte la [guía para desarrolladores de IoT Hub][lnk-devguide-identity] para más información.</span><span class="sxs-lookup"><span data-stu-id="d5d4c-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
