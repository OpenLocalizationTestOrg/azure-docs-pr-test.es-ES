---
title: "Introducción a Azure IoT Hub (.NET) | Microsoft Docs"
description: "Obtenga información sobre cómo enviar mensajes del dispositivo a la nube a una instancia de Azure IoT Hub mediante los SDK de IoT para .NET. Cree aplicaciones de servicio y de dispositivo simuladas para registrar el dispositivo, enviar mensajes y leerlos en IoT Hub."
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
ms.openlocfilehash: 69296eb9ac2a74a97b632d27733a6a06500b4abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-net"></a><span data-ttu-id="92063-104">Conexión del dispositivo en IoT Hub con .NET</span><span class="sxs-lookup"><span data-stu-id="92063-104">Connect your device to your IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="92063-105">Al final de este tutorial tendrá tres aplicaciones de consola de .NET:</span><span class="sxs-lookup"><span data-stu-id="92063-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="92063-106">**CreateDeviceIdentity**, que crea una identidad de dispositivo y una clave de seguridad asociada para conectar la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92063-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="92063-107">**ReadDeviceToCloudMessages**, que muestra los datos de telemetría enviados por la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92063-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="92063-108">**SimulatedDevice**, que se conecta con su IoT Hub con la identidad de dispositivo creada anteriormente, y envía un mensaje de telemetría cada segundo mediante el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="92063-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

<span data-ttu-id="92063-109">Puede descargar o clonar la solución de Visual Studio, que contiene las tres aplicaciones de Github.</span><span class="sxs-lookup"><span data-stu-id="92063-109">You can download or clone the Visual Studio solution, which contains the three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="92063-110">Para más información acerca de los diversos SDK que puede usar para crear ambas aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución, consulte [Azure IoT SDKs][lnk-hub-sdks] (SDK de IoT de Azure).</span><span class="sxs-lookup"><span data-stu-id="92063-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="92063-111">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="92063-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="92063-112">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="92063-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="92063-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="92063-113">An active Azure account.</span></span> <span data-ttu-id="92063-114">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="92063-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="92063-115">Ya se creó IoT Hub y ya tiene el nombre de host y la cadena de conexión de IoT Hub que necesita para completar el resto del tutorial.</span><span class="sxs-lookup"><span data-stu-id="92063-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="92063-116">Recepción de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="92063-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="92063-117">En esta sección, creará una aplicación de consola de .NET que lee los mensajes de dispositivo a nube desde un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92063-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="92063-118">El centro de IoT expone un punto de conexión compatible con [Azure Event Hubs][lnk-event-hubs-overview] para permitirle leer los mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="92063-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="92063-119">Para simplificar las cosas, este tutorial crea un lector básico que no es apto para una implementación de alta capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="92063-119">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="92063-120">El tutorial sobre [procesamiento de mensajes del dispositivo a la nube][lnk-process-d2c-tutorial] muestra cómo procesar mensajes del dispositivo a la nube a escala.</span><span class="sxs-lookup"><span data-stu-id="92063-120">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="92063-121">Para más información sobre cómo procesar los mensajes de los Centros de eventos, consulte el tutorial [Introducción a Event Hubs][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="92063-121">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="92063-122">(Este tutorial es aplicable a los puntos de conexión compatibles con los centros de eventos de IoT Hub).</span><span class="sxs-lookup"><span data-stu-id="92063-122">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="92063-123">El punto de conexión compatible con Event Hubs para leer mensajes de dispositivo a la nube siempre usa el protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="92063-123">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="92063-124">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="92063-124">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="92063-125">Asegúrese de que la versión de .NET Framework sea 4.5.1 o una posterior.</span><span class="sxs-lookup"><span data-stu-id="92063-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="92063-126">Asigne al proyecto el nombre **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="92063-126">Name the project **ReadDeviceToCloudMessages**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10a]

2. <span data-ttu-id="92063-128">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ReadDeviceToCloudMessages** y luego haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92063-128">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="92063-129">En la ventana **Administrador de paquetes NuGet**, busque **WindowsAzure.ServiceBus**, seleccione **Instalar** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="92063-129">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="92063-130">Este procedimiento permite descargar, instalar y agregar una referencia a [Azure Service Bus][lnk-servicebus-nuget], con todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="92063-130">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="92063-131">Este paquete permite que la aplicación para se conecte al punto de conexión compatible con centros de eventos en su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="92063-131">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="92063-132">Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="92063-132">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="92063-133">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="92063-133">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="92063-134">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub que creó en la sección "Creación de un IoT Hub".</span><span class="sxs-lookup"><span data-stu-id="92063-134">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="92063-135">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="92063-135">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="92063-136">Este método usa una instancia de **EventHubReceiver** para recibir mensajes de todas las particiones de recepción de dispositivo a nube del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="92063-136">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="92063-137">Observe cómo pasar un parámetro `DateTime.Now` al crear el objeto **EventHubReceiver** para que solo reciba los mensajes enviados después de iniciarse.</span><span class="sxs-lookup"><span data-stu-id="92063-137">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="92063-138">Este filtro es útil en un entorno de prueba, porque puede ver el conjunto actual de mensajes.</span><span class="sxs-lookup"><span data-stu-id="92063-138">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="92063-139">En un entorno de producción, el código debe asegurarse de que este procesa todos los mensajes.</span><span class="sxs-lookup"><span data-stu-id="92063-139">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="92063-140">Para más información, consulte el tutorial [Procesamiento de mensajes de dispositivo a la nube de IoT Hub][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="92063-140">For more information, see the tutorial [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="92063-141">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="92063-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
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

## <a name="create-a-device-app"></a><span data-ttu-id="92063-142">Creación de una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="92063-142">Create a device app</span></span>

<span data-ttu-id="92063-143">En esta sección, creará una aplicación de consola de .NET que simula un dispositivo que envía mensajes de dispositivo a nube a un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92063-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="92063-144">En Visual Studio, agregue un proyecto de escritorio clásico de Windows de Visual C# a la solución actual mediante la plantilla de proyecto **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="92063-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="92063-145">Asegúrese de que la versión de .NET Framework sea 4.5.1 o una posterior.</span><span class="sxs-lookup"><span data-stu-id="92063-145">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="92063-146">Asigne al proyecto el nombre **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="92063-146">Name the project **SimulatedDevice**.</span></span>

    ![Nuevo proyecto de escritorio clásico de Windows de Visual C#][10b]

2. <span data-ttu-id="92063-148">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **SimulatedDevice** y, a continuación, seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="92063-148">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="92063-149">En la ventana **Administrador de paquetes NuGet**, seleccione **Examinar**, busque **Microsoft.Azure.Devices.Client**, haga clic en **Instalar** para instalar el paquete **Microsoft.Azure.Devices** y acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="92063-149">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="92063-150">Este procedimiento permite descargar, instalar y agregar una referencia al [paquete NuGet del SDK de dispositivo de IoT de Azure][lnk-device-nuget] y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="92063-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="92063-151">Agregue la siguiente instrucción `using` en la parte superior del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="92063-151">Add the following `using` statement at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="92063-152">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="92063-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="92063-153">Sustituya `{iot hub hostname}` por el nombre de host del centro de IoT que obtuvo en la sección "Creación de un centro de IoT".</span><span class="sxs-lookup"><span data-stu-id="92063-153">Substitute `{iot hub hostname}` with the IoT hub host name you retrieved in the "Create an IoT hub" section.</span></span> <span data-ttu-id="92063-154">Sustituya `{device key}` por la clave de dispositivo que obtuvo en la sección "Creación de una identidad de dispositivo".</span><span class="sxs-lookup"><span data-stu-id="92063-154">Substitute `{device key}` with the device key you retrieved in the "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="92063-155">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="92063-155">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="92063-156">Este método envía un nuevo mensaje de dispositivo a nube cada segundo.</span><span class="sxs-lookup"><span data-stu-id="92063-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="92063-157">El mensaje contiene un objeto JSON serializado con el identificador de dispositivo y un número generado aleatoriamente para simular un sensor de temperatura y otro de humedad.</span><span class="sxs-lookup"><span data-stu-id="92063-157">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="92063-158">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="92063-158">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="92063-159">De forma predeterminada, el método **Create** en una aplicación de .NET Framework crea una instancia de **DeviceClient** que usa el protocolo AMQP para comunicarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92063-159">By default, the **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="92063-160">Para usar el protocolo MQTT o HTTP, use la invalidación del método **Create** que permite especificar el protocolo.</span><span class="sxs-lookup"><span data-stu-id="92063-160">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="92063-161">Los clientes de UWP y PCL utilizan el protocolo HTTP de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="92063-161">UWP and PCL clients use the HTTP protocol by default.</span></span> <span data-ttu-id="92063-162">Si usa el protocolo HTTPS, debe agregar también el paquete NuGet **Microsoft.AspNet.WebApi.Client** al proyecto para incluir el espacio de nombres **System.Net.Http.Formatting**.</span><span class="sxs-lookup"><span data-stu-id="92063-162">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="92063-163">Este tutorial le guiará por los pasos para crear una aplicación de dispositivo de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92063-163">This tutorial takes you through the steps to create an IoT Hub device app.</span></span> <span data-ttu-id="92063-164">También puede utilizar la extensión de Visual Studio [Connected Service for Azure IoT Hub][lnk-connected-service] (Servicio conectado para Azure IoT Hub) para agregar el código necesario a la aplicación del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92063-164">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="92063-165">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="92063-165">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="92063-166">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Tratamiento de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="92063-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="92063-167">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="92063-167">Run the apps</span></span>

<span data-ttu-id="92063-168">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="92063-168">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="92063-169">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="92063-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="92063-170">Seleccione **Proyectos de inicio múltiples** y seleccione **Iniciar** como acción para los proyectos **ReadDeviceToCloudMessages** y **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="92063-170">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Propiedades del proyecto de inicio][41]

2. <span data-ttu-id="92063-172">Presione **F5** para iniciar la ejecución de ambas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="92063-172">Press **F5** to start both apps running.</span></span> <span data-ttu-id="92063-173">La salida de la consola de la aplicación **SimulatedDevice** muestra los mensajes que envía la aplicación de dispositivo a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="92063-173">The console output from the **SimulatedDevice** app shows the messages your device app sends to your IoT hub.</span></span> <span data-ttu-id="92063-174">La salida de la consola de la aplicación **ReadDeviceToCloudMessages** muestra los mensajes que recibe el Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="92063-174">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>

    ![Salida de la consola de aplicaciones][42]

3. <span data-ttu-id="92063-176">El icono **Uso** de [Azure Portal][lnk-portal] muestra el número de mensajes enviados al centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="92063-176">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Icono Uso de Azure Portal][43]

## <a name="next-steps"></a><span data-ttu-id="92063-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92063-178">Next steps</span></span>

<span data-ttu-id="92063-179">En este tutorial, configuró un centro de IoT en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="92063-179">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="92063-180">Usó esta identidad de dispositivo para habilitar la aplicación del dispositivo para enviar a IoT Hub los mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="92063-180">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="92063-181">También creó otra aplicación que muestra los mensajes recibidos por el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="92063-181">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="92063-182">Para continuar la introducción a IoT Hub y explorar otros escenarios de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="92063-182">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="92063-183">[Conexión del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="92063-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="92063-184">[Introducción a la administración de dispositivos][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="92063-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="92063-185">[Introducción a IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="92063-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="92063-186">Para aprender a ampliar su solución IoT y cómo procesar mensajes de dispositivo a la nube a escala, consulte [Tutorial: procesamiento de mensajes de dispositivo a la nube][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="92063-186">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
