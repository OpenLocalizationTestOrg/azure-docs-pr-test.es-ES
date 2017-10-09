## <a name="create-a-device-identity"></a>Creación de una identidad de dispositivo
En esta sección, creará una aplicación de consola .NET que crea una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT. Un dispositivo no puede conectar tooIoT concentrador a menos que tenga una entrada en el registro de la identidad de Hola. Para obtener más información, vea la sección de "Registro de identidad" de Hola de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity]. Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador. Los identificadores de dispositivos distinguen mayúsculas de minúsculas.

1. En Visual Studio, agregue una nueva solución de Visual C# escritorio clásico de Windows proyecto tooa mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto. Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior. Proyecto de hello Name **CreateDeviceIdentity** y nombre hello solución **IoTHubGetStarted**.
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10]
2. En el Explorador de soluciones, haga clic en hello **CreateDeviceIdentity** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.
3. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.
   
    ![Ventana del Administrador de paquetes NuGet][11]
4. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Agregar Hola después campos toohello **programa** clase. Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Agregar Hola siguiendo el método toohello **programa** clase:
   
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
   
    Este método crea una identidad de dispositivo con el identificador **myFirstDevice**. (Si este identificador de dispositivo ya existe en el registro de la identidad de hello, código de hello simplemente recupera información del dispositivo existente hello). aplicación Hello, a continuación, muestra la clave principal de Hola para esa identidad. Use esta clave en el centro de IoT de hello simulada dispositivos aplicación tooconnect tooyour.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. Por último, agregue Hola después líneas toohello **Main** método:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Ejecutar esta aplicación y tome nota de la clave de dispositivo de Hola.
   
    ![Clave de dispositivo generado por la aplicación hello][12]

> [!NOTE]
> Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro. Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual. Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación. Consulte la [guía para desarrolladores de IoT Hub][lnk-devguide-identity] para más información.
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
