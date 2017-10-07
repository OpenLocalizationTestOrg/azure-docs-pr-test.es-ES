---
title: "Centro de IoT de Azure aaaUse dirigir métodos (.NET/.NET) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dirigir métodos. Usar dispositivos de IoT de Azure de hello SDK para .NET tooimplement una aplicación de dispositivo simulado que incluye un método directo y el servicio IoT de Azure SDK para .NET tooimplement una aplicación de servicio que invoca el método directo Hola Hola."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Uso de métodos directos (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

En este tutorial, estamos continuo toodevelop aplicaciones de consola de .NET dos:

* **CallMethodOnDevice**, una aplicación back-end, que llama a un método de aplicación de dispositivo simulado de hello y muestra la respuesta de Hola.
* **SimulateDeviceMethods**, una aplicación de consola que simula un dispositivo que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y responde método toohello llamado a nube Hola.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.
> 
> 

toocomplete este tutorial, necesita:

* Visual Studio 2015 o Visual Studio 2017.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si desea identidad del dispositivo toocreate hello mediante programación en su lugar, lea las secciones correspondientes de Hola Hola [conectar el centro de IoT de tooyour dispositivo simulado mediante .NET] [ lnk-device-identity-csharp] artículo.


## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado
En esta sección, creará una aplicación de consola .NET que responde el método tooa llamado a soluciones de hello volver final.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Proyecto de hello Name **SimulateDeviceMethods**.
   
    ![Nueva aplicación para dispositivo de Windows clásico de Visual C#][img-createdeviceapp]
    
1. En el Explorador de soluciones, haga clic en hello **SimulateDeviceMethods** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
1. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar** y busque **microsoft.azure.devices.client**. Seleccione **instalar** tooinstall hello **Microsoft.Azure.Devices.Client** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [dispositivos de IoT de Azure SDK] [ lnk-nuget-client-sdk] NuGet paquete y sus dependencias.
   
    ![Ventana del Administrador de paquetes NuGet: aplicación cliente][img-clientnuget]
1. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Agregar Hola después campos toohello **programa** clase. Reemplace el valor de marcador de posición de hello con cadena de conexión de dispositivo de Hola que anotó en la sección anterior de Hola.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Agregue Hola siguiendo métodos directas de tooimplement hello en dispositivo hello:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Por último, agregue Hola después código toohello **Main** método tooopen Hola conexión tooyour IoT hub- and initialize Hola método agente de escucha:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. Hola Visual Studio Solution Explorer, haga clic en la solución y, a continuación, haga clic en **Establecer proyectos de inicio...** . Seleccione **proyecto de inicio único**y, a continuación, seleccione hello **SimulateDeviceMethods** proyecto en el menú desplegable de Hola.        

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, los reintentos de conexión), tal como se sugiere en el artículo MSDN de hello [control de errores transitorios][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Llamada a un método directo en un dispositivo
En esta sección, creará una aplicación de consola .NET que llama a un método de aplicación de dispositivo simulado de hello y, a continuación, muestra la respuesta de Hola.

1. En Visual Studio, agregue una solución actual de toohello de proyectos de Visual C# escritorio clásico de Windows mediante el uso de hello **aplicación de consola** plantilla de proyecto. Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior. Proyecto de hello Name **CallMethodOnDevice**.
   
    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][img-createserviceapp]
2. En el Explorador de soluciones, haga clic en hello **CallMethodOnDevice** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet...** .
3. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **microsoft.azure.devices**, seleccione **instalar** tooinstall Hola **Microsoft.Azure.Devices** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [IoT de Azure SDK del servicio] [ lnk-nuget-service-sdk] NuGet paquete y sus dependencias.
   
    ![Ventana del Administrador de paquetes NuGet][img-servicenuget]

4. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Agregar Hola después campos toohello **programa** clase. Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección anterior de Hola Hola.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Agregar Hola siguiendo el método toohello **programa** clase:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Este método invoca un método directo con el nombre `writeLine` en hello `myDeviceId` dispositivo. A continuación, escribe respuesta Hola proporcionada por dispositivo de hello en la consola de Hola. Tenga en cuenta cómo es posible toospecify un valor de tiempo de espera para hello dispositivo toorespond.
7. Por último, agregue Hola después líneas toohello **Main** método:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Hola Visual Studio Solution Explorer, haga clic en la solución y, a continuación, haga clic en **Establecer proyectos de inicio...** . Seleccione **proyecto de inicio único**y, a continuación, seleccione hello **CallMethodOnDevice** proyecto en el menú desplegable de Hola.

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola
Ya estás listo toorun aplicaciones de Hola.

1. Ejecutar la aplicación de dispositivo de hello .NET **SimulateDeviceMethods**. Debería empezar a escuchar llamadas de método desde IoT Hub: 

    ![Ejecución de la aplicación de dispositivo][img-deviceapprun]
1. Ahora está conectado a ese dispositivo hello y espera para las invocaciones de método, ejecute hello .NET **CallMethodOnDevice** el método de aplicación tooinvoke hello en la aplicación de dispositivo simulado de hello. Debería ver la respuesta del dispositivo Hola escrito en la consola de Hola.
   
    ![Ejecución de la aplicación de servicio][img-serviceapprun]
1. dispositivo de Hello, a continuación, reacciona toohello método imprimiendo este mensaje:
   
    ![Método directo que se invoca en el dispositivo de Hola][img-directmethodinvoked]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola. También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola. 

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

* [Introducción al Centro de IoT]
* [Programación de trabajos en varios dispositivos][lnk-devguide-jobs]

toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Introducción al Centro de IoT]: iot-hub-node-node-getstarted.md
