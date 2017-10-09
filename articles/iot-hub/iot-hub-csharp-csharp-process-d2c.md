---
title: mensajes de dispositivo a la nube de Azure IoT Hub aaaProcess mediante las rutas (. NET) | Documentos de Microsoft
description: "¿Cómo tooprocess mensajes de dispositivo a la nube del centro de IoT mediante las reglas de enrutamiento y los extremos personalizados toodispatch mensajes tooother servicios de back-end."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="4c32e-103">Procesamiento de mensajes de dispositivo a nube de IoT Hub mediante rutas (.NET)</span><span class="sxs-lookup"><span data-stu-id="4c32e-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="4c32e-104">Este tutorial se basa en hello [empezar a trabajar con el centro de IoT] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4c32e-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="4c32e-105">tutorial de Hello:</span><span class="sxs-lookup"><span data-stu-id="4c32e-105">hello tutorial:</span></span>

* <span data-ttu-id="4c32e-106">Muestra cómo toouse enrutamiento mensajes del dispositivo a la nube de toodispatch las reglas de una manera fácil y de configuración.</span><span class="sxs-lookup"><span data-stu-id="4c32e-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="4c32e-107">Muestra cómo tooisolate mensajes interactivo que requieren acción inmediata de solución de hello back-end para su posterior procesamiento.</span><span class="sxs-lookup"><span data-stu-id="4c32e-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="4c32e-108">Por ejemplo, un dispositivo puede enviar un mensaje de alarma que desencadena la inserción de una incidencia en un sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="4c32e-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="4c32e-109">Por el contrario, los mensajes de punto de datos, como los datos de telemetría de temperatura, se envían a un motor de análisis.</span><span class="sxs-lookup"><span data-stu-id="4c32e-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="4c32e-110">Al final de Hola de este tutorial, ejecutar tres aplicaciones de consola. NET:</span><span class="sxs-lookup"><span data-stu-id="4c32e-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="4c32e-111">**SimulatedDevice**, una versión modificada de la aplicación hello creado en hello [empezar a trabajar con el centro de IoT] tutorial envía mensajes de dispositivo a la nube de punto de datos cada segundo e interactivo dispositivo a la nube mensajes cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="4c32e-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="4c32e-112">**ReadDeviceToCloudMessages** que muestra Hola no críticos telemetría enviado por la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4c32e-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="4c32e-113">**ReadCriticalQueue** anular pone en cola mensajes críticos de saludo enviados por la aplicación de dispositivo de una cola de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="4c32e-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="4c32e-114">Esta cola es Centro de IoT toohello adjunto.</span><span class="sxs-lookup"><span data-stu-id="4c32e-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="4c32e-115">El Centro de IoT ofrece compatibilidad con el SDK para muchas plataformas de dispositivos y lenguajes, entre los que se incluyen C, Java y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4c32e-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="4c32e-116">toolearn cómo tooreplace Hola dispositivo simulado en este tutorial con un dispositivo físico, vea hello [Centro para desarrolladores de Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="4c32e-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="4c32e-117">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="4c32e-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4c32e-118">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4c32e-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="4c32e-119">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="4c32e-119">An active Azure account.</span></span> <br/><span data-ttu-id="4c32e-120">En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4c32e-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="4c32e-121">También se dan por sentados ciertos conocimientos sobre [Azure Storage] y [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="4c32e-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="4c32e-122">Envío de mensajes interactivos</span><span class="sxs-lookup"><span data-stu-id="4c32e-122">Send interactive messages</span></span>

<span data-ttu-id="4c32e-123">Modificar la aplicación de dispositivo de Hola que creó en hello [empezar a trabajar con el centro de IoT] toooccasionally tutorial enviar mensajes interactivos.</span><span class="sxs-lookup"><span data-stu-id="4c32e-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="4c32e-124">En Visual Studio, en hello **SimulatedDevice** proyecto de equipo y reemplace hello `SendDeviceToCloudMessagesAsync` método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="4c32e-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="4c32e-125">Este método agrega al azar propiedad hello `"level": "critical"` toomessages enviados por dispositivo de hello, que simula un mensaje que requiere una acción inmediata por hello solución back-end.</span><span class="sxs-lookup"><span data-stu-id="4c32e-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="4c32e-126">aplicación de dispositivo de Hello pasa esta información en las propiedades de mensaje de Hola, en lugar de en el cuerpo del mensaje Hola, para que ese centro de IoT pueda enrutar el destino del mensaje adecuado de toohello de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="4c32e-127">Puede utilizar mensajes de tooroute de propiedades de mensaje para varios escenarios incluidos frío-path, además de procesamiento toohello ruta de acceso activa en el ejemplo se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="4c32e-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="4c32e-128">Para simplificar Hola simplicidad, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="4c32e-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4c32e-129">En el código de producción, debe implementar una directiva de reintentos como retroceso exponencial, tal como se sugiere en el artículo MSDN de hello [control de errores transitorios].</span><span class="sxs-lookup"><span data-stu-id="4c32e-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="4c32e-130">Cola de mensajes tooa de ruta en el centro de IoT</span><span class="sxs-lookup"><span data-stu-id="4c32e-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="4c32e-131">En esta sección:</span><span class="sxs-lookup"><span data-stu-id="4c32e-131">In this section, you:</span></span>

* <span data-ttu-id="4c32e-132">Creará una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4c32e-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="4c32e-133">Conéctelo tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="4c32e-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="4c32e-134">Configurar la cola de toohello IoT hub toosend mensajes basada en presencia de Hola de una propiedad de mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="4c32e-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="4c32e-135">Para obtener más información acerca de cómo tooprocess mensajes desde las colas de Bus de servicio, consulte [empezar a trabajar con colas][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="4c32e-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="4c32e-136">Cree una cola de Service Bus como se describe en [Introducción a las colas][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="4c32e-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="4c32e-137">Hola cola debe ser Hola misma suscripción y región que el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="4c32e-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="4c32e-138">Tome nota del nombre de espacio de nombres y la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4c32e-139">Las colas y los temas de Service Bus usados como puntos de conexión de IoT Hub no deben tener habilitadas las opciones **Sesiones** o **Detección de duplicados**.</span><span class="sxs-lookup"><span data-stu-id="4c32e-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="4c32e-140">Si cualquiera de estas opciones están habilitada, el punto de conexión de hello aparece como **inaccesible** Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c32e-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="4c32e-141">En Hola portal de Azure, abra el centro de IoT y haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="4c32e-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Puntos de conexión en IoT Hub][30]

3. <span data-ttu-id="4c32e-143">Hola **extremos** hoja, haga clic en **agregar** en Hola tooadd superior su centro de IoT tooyour de cola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="4c32e-144">El punto de conexión de nombre hello **CriticalQueue** y usar Hola listas desplegables tooselect **cola de Service Bus**, Hola espacio de nombres de Bus de servicio en el que reside la cola y Hola nombre de la cola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="4c32e-145">Cuando haya terminado, haga clic en **guardar** final Hola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Adición de un punto de conexión][31]
    
4. <span data-ttu-id="4c32e-147">Ahora haga clic en **Routes** (Rutas) en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4c32e-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="4c32e-148">Haga clic en **agregar** en parte superior de Hola de hello hoja toocreate agrega una regla de enrutamiento que enruta los mensajes de cola que toohello se acaba.</span><span class="sxs-lookup"><span data-stu-id="4c32e-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="4c32e-149">Seleccione **DeviceTelemetry** como origen de Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="4c32e-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="4c32e-150">Escriba `level="critical"` como condición de hello y elija la cola de Hola que acaba de agregar como un extremo personalizado como Hola extremo de la regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="4c32e-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="4c32e-151">Cuando haya terminado, haga clic en **guardar** final Hola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Adición de una ruta][32]
    
    <span data-ttu-id="4c32e-153">Asegúrese de que la ruta de reserva de Hola se establece demasiado**ON**.</span><span class="sxs-lookup"><span data-stu-id="4c32e-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="4c32e-154">Este valor es la configuración predeterminada de Hola para un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="4c32e-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Ruta de reserva][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="4c32e-156">Leer desde el punto de conexión de hello cola</span><span class="sxs-lookup"><span data-stu-id="4c32e-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="4c32e-157">En esta sección, se leen mensajes de Hola de extremo de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="4c32e-158">En Visual Studio, agregue una solución actual de la toohello de proyectos Visual C# escritorio clásico de Windows, mediante el uso de hello **aplicación de consola (.NET Framework)** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="4c32e-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="4c32e-159">Proyecto de hello Name **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="4c32e-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="4c32e-160">En el Explorador de soluciones, haga clic en hello **ReadCriticalQueue** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4c32e-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="4c32e-161">Esta operación muestra hello **Administrador de paquetes de NuGet** ventana.</span><span class="sxs-lookup"><span data-stu-id="4c32e-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="4c32e-162">Busque **WindowsAzure.ServiceBus**, haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="4c32e-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="4c32e-163">Esta operación se descarga, se instala y agrega una referencia toohello Bus de servicio de Azure, con todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="4c32e-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="4c32e-164">Agregue los siguiente hello **mediante** las instrucciones en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="4c32e-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="4c32e-165">Por último, agregue Hola después líneas toohello **Main** método.</span><span class="sxs-lookup"><span data-stu-id="4c32e-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="4c32e-166">Sustituya la cadena de conexión de hello con **escuchar** permisos para hello cola:</span><span class="sxs-lookup"><span data-stu-id="4c32e-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="4c32e-167">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="4c32e-167">Run hello applications</span></span>
<span data-ttu-id="4c32e-168">Ahora está listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="4c32e-169">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**.</span><span class="sxs-lookup"><span data-stu-id="4c32e-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="4c32e-170">Seleccione **proyectos de inicio múltiples**, a continuación, seleccione **iniciar** como acción de Hola para hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, y **ReadCriticalQueue** proyectos.</span><span class="sxs-lookup"><span data-stu-id="4c32e-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="4c32e-171">Presione **F5** toostart Hola tres aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="4c32e-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="4c32e-172">Hola **ReadDeviceToCloudMessages** aplicación tiene solo no críticos mensajes enviados desde hello **SimulatedDevice** hello y aplicación **ReadCriticalQueue** aplicación sólo tiene mensajes críticos.</span><span class="sxs-lookup"><span data-stu-id="4c32e-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Tres aplicaciones de consola][50]

## <a name="next-steps"></a><span data-ttu-id="4c32e-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c32e-174">Next steps</span></span>
<span data-ttu-id="4c32e-175">En este tutorial, ha aprendido cómo tooreliably enviar mensajes del dispositivo a la nube mediante la funcionalidad de enrutamiento de mensajes de Hola de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="4c32e-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="4c32e-176">Hola [cómo mensajes toosend en la nube al dispositivo con el centro de IoT] [ lnk-c2d] muestra cómo toosend mensajes tooyour dispositivos desde el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="4c32e-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="4c32e-177">ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="4c32e-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="4c32e-178">toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="4c32e-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="4c32e-179">toolearn más información acerca de enrutamiento de mensajes en el centro de IoT, consulte [enviar y recibir mensajes con el centro de IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="4c32e-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[Guía del desarrollador de centro de IoT]: iot-hub-devguide.md
[empezar a trabajar con el centro de IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Centro para desarrolladores de Azure IoT]: https://azure.microsoft.com/develop/iot
[control de errores transitorios]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
