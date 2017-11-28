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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="1d46f-104">Conectar el centro de IoT de tooyour de dispositivo mediante .NET</span><span class="sxs-lookup"><span data-stu-id="1d46f-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="1d46f-105">Al final de Hola de este tutorial, tendrá tres aplicaciones de consola. NET:</span><span class="sxs-lookup"><span data-stu-id="1d46f-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="1d46f-106">**CreateDeviceIdentity**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1d46f-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="1d46f-107">**ReadDeviceToCloudMessages**, que muestra la telemetría de hello enviado por la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1d46f-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="1d46f-108">**SimulatedDevice**, que se conecta centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y envía un mensaje de telemetría cada segundo mediante hello MQTT protocolo.</span><span class="sxs-lookup"><span data-stu-id="1d46f-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="1d46f-109">Puede descargar o clonar la solución de Visual Studio de hello, que contiene tres aplicaciones de Hola desde Github.</span><span class="sxs-lookup"><span data-stu-id="1d46f-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="1d46f-110">Para obtener información sobre hello Azure IoT SDK que se puede usar toobuild toorun aplicaciones en dispositivos tanto el back-end de soluciones, consulte [SDK de Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="1d46f-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="1d46f-111">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="1d46f-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1d46f-112">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1d46f-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1d46f-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="1d46f-113">An active Azure account.</span></span> <span data-ttu-id="1d46f-114">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="1d46f-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="1d46f-115">Ahora ha creado su centro de IoT y tiene el nombre de host de Hola y cadena de conexión de centro de IoT que necesite que el resto de hello toocomplete de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d46f-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="1d46f-116">Recepción de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="1d46f-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="1d46f-117">En esta sección, creará una aplicación de consola de .NET que lee los mensajes de dispositivo a nube desde un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1d46f-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="1d46f-118">Un centro de IoT expone un [centros de eventos de Azure][lnk-event-hubs-overview]-extremo compatible tooenable tooread mensajes de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="1d46f-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="1d46f-119">tookeep cosas simples, en este tutorial se crea un lector básico que no es adecuado para una implementación de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1d46f-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="1d46f-120">toolearn cómo mensajes tooprocess dispositivo a la nube a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d46f-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="1d46f-121">Para obtener más información acerca de cómo tooprocess mensajes desde los centros de eventos, vea hello [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d46f-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="1d46f-122">(Este tutorial es aplicable toohello compatible con el centro de IoT Hub eventos extremos).</span><span class="sxs-lookup"><span data-stu-id="1d46f-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="1d46f-123">Hola extremo compatible de concentrador de eventos para leer mensajes de dispositivo para la nube siempre utiliza Hola protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="1d46f-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="1d46f-124">En Visual Studio, agregue una solución actual de la toohello de proyectos Visual C# escritorio clásico de Windows, mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="1d46f-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1d46f-125">Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="1d46f-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="1d46f-126">Proyecto de hello Name **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="1d46f-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10a]

2. <span data-ttu-id="1d46f-128">En el Explorador de soluciones, haga clic en hello **ReadDeviceToCloudMessages** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1d46f-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="1d46f-129">Hola **Administrador de paquetes de NuGet** ventana, busque **WindowsAzure.ServiceBus**, seleccione **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="1d46f-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="1d46f-130">Este procedimiento se descarga, se instala y se agrega una referencia demasiado[Azure Service Bus][lnk-servicebus-nuget], con todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="1d46f-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="1d46f-131">Este paquete permite extremo tooconnect toohello compatible de concentrador de eventos de la aplicación de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1d46f-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="1d46f-132">Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="1d46f-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="1d46f-133">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="1d46f-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="1d46f-134">Sustituya el valor de marcador de posición de hello con la cadena de conexión de centro de IoT para los concentradores de Hola que creó en la sección "Crear un centro de IoT" Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="1d46f-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="1d46f-135">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="1d46f-135">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="1d46f-136">Este método usa un **EventHubReceiver** particiones de recepción de mensajes de instancia tooreceive desde todos los Hola IoT hub dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="1d46f-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="1d46f-137">Tenga en cuenta cómo pasar un `DateTime.Now` parámetro cuando creas hello **EventHubReceiver** objeto, por lo que solo recibe mensajes enviados después de iniciarse.</span><span class="sxs-lookup"><span data-stu-id="1d46f-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="1d46f-138">Este filtro es útil en un entorno de prueba para que pueda ver el conjunto actual de Hola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="1d46f-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="1d46f-139">En un entorno de producción, el código debe asegurarse de que procesa todos los mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="1d46f-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="1d46f-140">Para obtener más información, vea el tutorial de hello [cómo tooprocess mensajes del dispositivo a la nube de centro de IoT][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="1d46f-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="1d46f-141">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="1d46f-141">Finally, add hello following lines toohello **Main** method:</span></span>

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

## <a name="create-a-device-app"></a><span data-ttu-id="1d46f-142">Creación de una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="1d46f-142">Create a device app</span></span>

<span data-ttu-id="1d46f-143">En esta sección, creará una aplicación de consola .NET que simula un dispositivo que envía el centro de IoT tooan de mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="1d46f-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="1d46f-144">En Visual Studio, agregue una solución actual de la toohello de proyectos Visual C# escritorio clásico de Windows, mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="1d46f-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1d46f-145">Asegúrese de que la versión de .NET Framework de hello es 4.5.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="1d46f-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="1d46f-146">Proyecto de hello Name **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="1d46f-146">Name hello project **SimulatedDevice**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10b]

2. <span data-ttu-id="1d46f-148">En el Explorador de soluciones, haga clic en hello **SimulatedDevice** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1d46f-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="1d46f-149">Hola **Administrador de paquetes de NuGet** ventana, seleccione **examinar**, busque **Microsoft.Azure.Devices.Client**, seleccione **instalar** Hola tooinstall **Microsoft.Azure.Devices.Client** empaquetar y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="1d46f-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="1d46f-150">Este procedimiento se descarga, se instala y se agrega una referencia toohello [paquete de NuGet de SDK de dispositivos de IoT de Azure] [ lnk-device-nuget] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="1d46f-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="1d46f-151">Agregue los siguiente hello `using` declaración en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="1d46f-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="1d46f-152">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="1d46f-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="1d46f-153">SUBSTITUTE `{iot hub hostname}` con nombre de host de hello IoT hub recuperó en la sección "Crear un centro de IoT" de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d46f-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="1d46f-154">SUBSTITUTE `{device key}` con clave de dispositivo de hello recuperó en la sección "Crear una identidad de dispositivo" de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d46f-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="1d46f-155">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="1d46f-155">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="1d46f-156">Este método envía un nuevo mensaje de dispositivo a nube cada segundo.</span><span class="sxs-lookup"><span data-stu-id="1d46f-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="1d46f-157">mensaje de bienvenida contiene un objeto JSON serializado, con el Id. de dispositivo de Hola y genera números toosimulate un sensor de temperatura y un sensor de humedad de forma aleatoria.</span><span class="sxs-lookup"><span data-stu-id="1d46f-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="1d46f-158">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="1d46f-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="1d46f-159">De forma predeterminada, Hola **crear** método en una aplicación de .NET Framework crea un **DeviceClient** instancia que utiliza hello AMQP protocolo toocommunicate con centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1d46f-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="1d46f-160">Hola toouse protocolo MQTT o HTTP, usar la invalidación de Hola de hello **Create** método que le permite el protocolo de hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="1d46f-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="1d46f-161">Los clientes UWP y PCL utilizan Protocolo de hello HTTP de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1d46f-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="1d46f-162">Si utiliza el protocolo de hello HTTP, también debe agregar hello **Microsoft.AspNet.WebApi.Client** Hola de NuGet paquete tooyour proyecto tooinclude **System.Net.Http.Formatting** espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="1d46f-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="1d46f-163">Este tutorial le guiará Hola pasos toocreate un centro de IoT del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1d46f-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="1d46f-164">También puede usar hello [servicio conectado de centro de IoT de Azure] [ lnk-connected-service] Visual Studio extensión tooadd Hola código necesario tooyour del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1d46f-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="1d46f-165">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="1d46f-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1d46f-166">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="1d46f-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="1d46f-167">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="1d46f-167">Run hello apps</span></span>

<span data-ttu-id="1d46f-168">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1d46f-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="1d46f-169">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="1d46f-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="1d46f-170">Seleccione **proyectos de inicio múltiples**y, a continuación, seleccione **iniciar** como acción de Hola para ambos hello **ReadDeviceToCloudMessages** y **SimulatedDevice** proyectos.</span><span class="sxs-lookup"><span data-stu-id="1d46f-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Propiedades del proyecto de inicio][41]

2. <span data-ttu-id="1d46f-172">Presione **F5** toostart ambas aplicaciones que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="1d46f-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="1d46f-173">Hola de salida de la consola de hello **SimulatedDevice** mensajes de saludo de aplicación se muestra en la aplicación de dispositivo envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1d46f-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="1d46f-174">Hola de salida de la consola de hello **ReadDeviceToCloudMessages** aplicación muestra mensajes de Hola que recibe de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1d46f-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Salida de la consola de aplicaciones][42]

3. <span data-ttu-id="1d46f-176">Hola **uso** el icono Servicios hello [portal de Azure] [ lnk-portal] muestra Hola número de mensajes enviados toohello centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="1d46f-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Icono Uso de Azure Portal][43]

## <a name="next-steps"></a><span data-ttu-id="1d46f-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d46f-178">Next steps</span></span>

<span data-ttu-id="1d46f-179">En este tutorial, configura un centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="1d46f-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="1d46f-180">Usar este dispositivo identidad tooenable Hola dispositivo aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1d46f-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="1d46f-181">También crea una aplicación que muestra los mensajes de saludo recibidos por centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="1d46f-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="1d46f-182">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="1d46f-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="1d46f-183">[Conexión del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="1d46f-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="1d46f-184">[Introducción a la administración de dispositivos][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="1d46f-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="1d46f-185">[Introducción a IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="1d46f-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="1d46f-186">toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1d46f-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
