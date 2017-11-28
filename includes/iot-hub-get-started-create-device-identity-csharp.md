## <a name="create-a-device-identity"></a><span data-ttu-id="0abd2-101">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="0abd2-101">Create a device identity</span></span>
<span data-ttu-id="0abd2-102">En esta sección, creará una aplicación de consola .NET que crea una identidad de dispositivo en el registro de identidades de su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0abd2-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="0abd2-103">No se puede conectar un dispositivo a IoT Hub a menos que tenga una entrada en el registro de identidades.</span><span class="sxs-lookup"><span data-stu-id="0abd2-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="0abd2-104">Para más información, consulte la sección sobre el registro de la identidad de la [guía para desarrolladores de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="0abd2-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="0abd2-105">Cuando ejecuta esta aplicación de consola, se genera una clave y un identificador de dispositivo únicos con el que el dispositivo puede identificarse cuando envía a IoT Hub mensajes de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="0abd2-105">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="0abd2-106">Los identificadores de dispositivos distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0abd2-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="0abd2-107">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a una nueva solución mediante la plantilla de proyecto **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="0abd2-107">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="0abd2-108">Asegúrese de que la versión de .NET Framework sea 4.5.1 o una posterior.</span><span class="sxs-lookup"><span data-stu-id="0abd2-108">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="0abd2-109">Llame **CreateDeviceIdentity** al proyecto e **IoTHubGetStarted** a la solución.</span><span class="sxs-lookup"><span data-stu-id="0abd2-109">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10]
2. <span data-ttu-id="0abd2-111">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **CreateDeviceIdentity** y, a continuación, seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0abd2-111">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="0abd2-112">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **microsoft.azure.devices**, seleccione **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="0abd2-112">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="0abd2-113">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-nuget-service-sdk] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="0abd2-113">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Ventana del Administrador de paquetes NuGet][11]
4. <span data-ttu-id="0abd2-115">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="0abd2-115">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="0abd2-116">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="0abd2-116">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="0abd2-117">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub para el centro que creó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="0abd2-117">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="0abd2-118">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="0abd2-118">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="0abd2-119">Este método crea una identidad de dispositivo con el identificador **myFirstDevice**.</span><span class="sxs-lookup"><span data-stu-id="0abd2-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="0abd2-120">(Si el identificador de dispositivo ya existe en el Registro de identidad, el código simplemente recupera la información existente del dispositivo). A continuación, la aplicación muestra la clave principal de esa identidad.</span><span class="sxs-lookup"><span data-stu-id="0abd2-120">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="0abd2-121">Esta clave se usará en la aplicación de dispositivo simulado para conectarse a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0abd2-121">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="0abd2-122">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="0abd2-122">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="0abd2-123">Ejecute la aplicación y anote la clave del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0abd2-123">Run this application, and make a note of the device key.</span></span>
   
    ![Clave de dispositivo generada por la aplicación][12]

> [!NOTE]
> <span data-ttu-id="0abd2-125">El registro de identidades de IoT Hub solo almacena identidades de dispositivos para permitir el acceso seguro al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0abd2-125">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="0abd2-126">Almacena las claves y los identificadores de dispositivo para usarlos como credenciales de seguridad, y un indicador de habilitado o deshabilitado que permite deshabilitar el acceso a un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="0abd2-126">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="0abd2-127">Si la aplicación necesita almacenar otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0abd2-127">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="0abd2-128">Consulte la [guía para desarrolladores de IoT Hub][lnk-devguide-identity] para más información.</span><span class="sxs-lookup"><span data-stu-id="0abd2-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
