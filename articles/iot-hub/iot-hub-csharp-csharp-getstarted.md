---
title: "aaaGet inició con Azure IoT Hub (. NET) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosend dispositivo a la nube mensajes tooAzure centro de IoT mediante IoT SDK para. NET. Crear dispositivo simulado y tooregister de aplicaciones de servicio, el dispositivo, enviar mensajes y leer los mensajes de centro de IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Conectar el centro de IoT de tooyour de dispositivo mediante .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Al final de Hola de este tutorial, tendrá tres aplicaciones de consola. NET:

* **CreateDeviceIdentity**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo.
* **ReadDeviceToCloudMessages**, que muestra la telemetría de hello enviado por la aplicación de dispositivo.
* **SimulatedDevice**, que se conecta centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y envía un mensaje de telemetría cada segundo mediante hello MQTT protocolo.

Puede descargar o clonar la solución de Visual Studio de hello, que contiene tres aplicaciones de Hola desde Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Para obtener información sobre hello Azure IoT SDK que se puede usar toobuild toorun aplicaciones en dispositivos tanto el back-end de soluciones, consulte [SDK de Azure IoT][lnk-hub-sdks].

toocomplete este tutorial, necesita Hola siguientes:

* Visual Studio 2015 o Visual Studio 2017.
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Ahora ha creado su centro de IoT y tiene el nombre de host de Hola y cadena de conexión de centro de IoT que necesite que el resto de hello toocomplete de este tutorial.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Recepción de mensajes de dispositivo a nube
En esta sección, creará una aplicación de consola de .NET que lee los mensajes de dispositivo a nube desde un IoT Hub. Un centro de IoT expone un [centros de eventos de Azure][lnk-event-hubs-overview]-extremo compatible tooenable tooread mensajes de dispositivo a la nube. tookeep cosas simples, en este tutorial se crea un lector básico que no es adecuado para una implementación de alto rendimiento. toolearn cómo mensajes tooprocess dispositivo a la nube a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial. Para obtener más información acerca de cómo tooprocess mensajes desde los centros de eventos, vea hello [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial. (Este tutorial es aplicable toohello compatible con el centro de IoT Hub eventos extremos).

> [!NOTE]
> Hola extremo compatible de concentrador de eventos para leer mensajes de dispositivo para la nube siempre utiliza Hola protocolo AMQP.

1. En Visual Studio, agregue una solución actual de la toohello de proyectos Visual C# escritorio clásico de Windows, mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto. Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior. Proyecto de hello Name **ReadDeviceToCloudMessages**.

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10a]

2. En el Explorador de soluciones, haga clic en hello **ReadDeviceToCloudMessages** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.

3. Hola **Administrador de paquetes de NuGet** ventana, busque **WindowsAzure.ServiceBus**, seleccione **instalar**y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia demasiado[Azure Service Bus][lnk-servicebus-nuget], con todas sus dependencias. Este paquete permite extremo tooconnect toohello compatible de concentrador de eventos de la aplicación de hello en el centro de IoT.

4. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Agregar Hola después campos toohello **programa** clase. Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección "Crear un centro de IoT" Hola Hola.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Agregar Hola siguiendo el método toohello **programa** clase:

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    Este método usa un **EventHubReceiver** particiones de recepción de mensajes de instancia tooreceive desde todos los Hola IoT hub dispositivo a la nube. Tenga en cuenta cómo pasar un `DateTime.Now` parámetro cuando creas hello **EventHubReceiver** objeto, por lo que solo recibe mensajes enviados después de iniciarse. Este filtro es útil en un entorno de prueba para que pueda ver el conjunto actual de Hola de mensajes. En un entorno de producción, el código debe asegurarse de que procesa todos los mensajes de saludo. Para obtener más información, vea el tutorial de hello [cómo tooprocess mensajes del dispositivo a la nube de centro de IoT][lnk-process-d2c-tutorial].

7. Por último, agregue Hola después líneas toohello **Main** método:

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a>Creación de una aplicación de dispositivo

En esta sección, creará una aplicación de consola .NET que simula un dispositivo que envía el centro de IoT tooan de mensajes del dispositivo a la nube.

1. En Visual Studio, agregue una solución actual de la toohello de proyectos Visual C# escritorio clásico de Windows, mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto. Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior. Proyecto de hello Name **SimulatedDevice**.

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10b]

2. En el Explorador de soluciones, haga clic en hello **SimulatedDevice** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.

3. Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **Microsoft.Azure.Devices.Client**, seleccione **instalar** Hola tooinstall **Microsoft.Azure.Devices.Client** empaquetar y acepte los términos de Hola de uso. Este procedimiento se descarga, se instala y se agrega una referencia toohello [paquete de NuGet de SDK de dispositivos de IoT de Azure] [ lnk-device-nuget] y sus dependencias.

4. Agregue los siguiente hello `using` declaración en la parte superior de Hola de hello **Program.cs** archivo:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Agregar Hola después campos toohello **programa** clase. SUBSTITUTE `{iot hub hostname}` con nombre de host de hello IoT hub recuperó en la sección "Crear un centro de IoT" de Hola. SUBSTITUTE `{device key}` con clave de dispositivo de hello recuperó en la sección "Crear una identidad de dispositivo" de Hola.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Agregar Hola siguiendo el método toohello **programa** clase:

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    Este método envía un nuevo mensaje de dispositivo a nube cada segundo. mensaje de bienvenida contiene un objeto JSON serializado, con el Id. de dispositivo de Hola y genera números toosimulate un sensor de temperatura y un sensor de humedad de forma aleatoria.

7. Por último, agregue Hola después líneas toohello **Main** método:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    De forma predeterminada, Hola **crear** método en una aplicación de .NET Framework crea un **DeviceClient** instancia que utiliza hello AMQP protocolo toocommunicate con centro de IoT. Hola toouse protocolo MQTT o HTTP, usar la invalidación de Hola de hello **Create** método que le permite el protocolo de hello toospecify. Los clientes UWP y PCL utilizan Protocolo de hello HTTP de forma predeterminada. Si utiliza el protocolo de hello HTTP, también debe agregar hello **Microsoft.AspNet.WebApi.Client** Hola de NuGet paquete tooyour proyecto tooinclude **System.Net.Http.Formatting** espacio de nombres.

Este tutorial le guiará Hola pasos toocreate un centro de IoT del dispositivo. También puede usar hello [servicio conectado de centro de IoT de Azure] [ lnk-connected-service] Visual Studio extensión tooadd Hola código necesario tooyour del dispositivo.

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun Hola aplicaciones.

1. En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**. Seleccione **proyectos de inicio múltiples**y, a continuación, seleccione **iniciar** como acción de Hola para ambos hello **ReadDeviceToCloudMessages** y **SimulatedDevice** proyectos.

    ![Propiedades del proyecto de inicio][41]

2. Presione **F5** toostart ambas aplicaciones que se ejecutan. Hola de salida de la consola de hello **SimulatedDevice** mensajes de saludo de aplicación se muestra en la aplicación de dispositivo envía tooyour centro de IoT. Hola de salida de la consola de hello **ReadDeviceToCloudMessages** aplicación muestra mensajes de Hola que recibe de su centro de IoT.

    ![Salida de la consola de aplicaciones][42]

3. Hola **uso** el icono Servicios hello [portal de Azure] [ lnk-portal] muestra Hola número de mensajes enviados toohello centro de IoT:

    ![Icono Uso de Azure Portal][43]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, configura un centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Usar este dispositivo identidad tooenable Hola dispositivo aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT. También crea una aplicación que muestra los mensajes de saludo recibidos por centro de IoT Hola.

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

* [Conexión del dispositivo][lnk-connect-device]
* [Introducción a la administración de dispositivos][lnk-device-management]
* [Introducción a IoT Edge][lnk-iot-edge]

toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
