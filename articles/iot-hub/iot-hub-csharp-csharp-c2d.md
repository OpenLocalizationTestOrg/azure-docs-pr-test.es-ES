---
title: mensajes de aaaCloud al dispositivo con Azure IoT Hub (. NET) | Documentos de Microsoft
description: "¿Cómo toosend en la nube al dispositivo mensajes tooa del dispositivo de un centro de IoT de Azure mediante hello Azure IoT SDK para. NET. Modificar una aplicación de dispositivo tooreceive los mensajes de nube al dispositivo y modificar un mensajes de aplicaciones back-end toosend hello en la nube al dispositivo."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="11a3d-104">Enviar mensajes desde el dispositivo de tooyour hello en la nube con IoT Hub (. NET)</span><span class="sxs-lookup"><span data-stu-id="11a3d-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="11a3d-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="11a3d-105">Introduction</span></span>
<span data-ttu-id="11a3d-106">IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="11a3d-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="11a3d-107">Hola [empezar a trabajar con el centro de IoT] tutorial muestra cómo aprovisionar una identidad de dispositivo en ella toocreate un centro de IoT y codificar una aplicación para dispositivos que envía mensajes de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="11a3d-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="11a3d-108">Este tutorial se basa en la [introducción al Centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="11a3d-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="11a3d-109">En él se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="11a3d-109">It shows you how to:</span></span>

* <span data-ttu-id="11a3d-110">Desde el back-end de soluciones, enviar mensajes en la nube al dispositivo tooa dispositivo a través del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="11a3d-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="11a3d-111">Reciba mensajes de nube a dispositivo en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11a3d-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="11a3d-112">En el back-end de soluciones, solicitar confirmación de entrega (*comentarios*) para mensajes envían tooa dispositivo desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="11a3d-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="11a3d-113">Puede encontrar más información sobre los mensajes en la nube al dispositivo en hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="11a3d-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="11a3d-114">Al final de Hola de este tutorial, ejecute dos aplicaciones de consola. NET:</span><span class="sxs-lookup"><span data-stu-id="11a3d-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="11a3d-115">**SimulatedDevice**, una versión modificada de la aplicación hello creado en [empezar a trabajar con el centro de IoT], que se conecta el centro de IoT tooyour y recibe los mensajes de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11a3d-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="11a3d-116">**SendCloudToDevice**, que envía un mensaje en la nube a dispositivo toohello del dispositivo a través del centro de IoT y, a continuación, recibe la confirmación de entrega.</span><span class="sxs-lookup"><span data-stu-id="11a3d-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="11a3d-117">IoT Hub ofrece compatibilidad con SDK para muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante [SDK de dispositivos IoT de Azure].</span><span class="sxs-lookup"><span data-stu-id="11a3d-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="11a3d-118">Para obtener instrucciones paso a paso sobre cómo tooconnect del su dispositivo toothis tutorial código y generalmente tooAzure centro de IoT, vea hello [Guía del desarrollador de centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="11a3d-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="11a3d-119">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="11a3d-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="11a3d-120">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="11a3d-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="11a3d-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="11a3d-121">An active Azure account.</span></span> <span data-ttu-id="11a3d-122">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="11a3d-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="11a3d-123">Recibir mensajes en la aplicación de dispositivo de hello</span><span class="sxs-lookup"><span data-stu-id="11a3d-123">Receive messages in hello device app</span></span>
<span data-ttu-id="11a3d-124">En esta sección, modificará la aplicación de dispositivo de Hola que creó en [empezar a trabajar con el centro de IoT] mensajes de nube al dispositivo tooreceive Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="11a3d-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="11a3d-125">En Visual Studio, en hello **SimulatedDevice** proyecto de equipo y agregar Hola siguiendo el método toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="11a3d-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="11a3d-126">Hola `ReceiveAsync` método asincrónicamente devuelve mensajes de bienvenida recibido en el tiempo de Hola que se recibe por dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3d-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="11a3d-127">Devuelve *null* tras un período de tiempo de espera puede especificar (en este caso, se utiliza el predeterminado de Hola de un minuto).</span><span class="sxs-lookup"><span data-stu-id="11a3d-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="11a3d-128">Cuando recibe la aplicación hello un *null*, debería continuar toowait si hay mensajes nuevos.</span><span class="sxs-lookup"><span data-stu-id="11a3d-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="11a3d-129">Este requisito es motivo Hola Hola `if (receivedMessage == null) continue` línea.</span><span class="sxs-lookup"><span data-stu-id="11a3d-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="11a3d-130">Hola llamada demasiado`CompleteAsync()` notifica al centro de IoT ese mensaje Hola se ha procesado correctamente.</span><span class="sxs-lookup"><span data-stu-id="11a3d-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="11a3d-131">mensaje de saludo puede quitarse con seguridad de cola de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3d-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="11a3d-132">Si hubo un problema de esa aplicación de dispositivo ha impedido Hola de completar el procesamiento de Hola de mensaje de bienvenida, centro de IoT lo entrega de nuevo.</span><span class="sxs-lookup"><span data-stu-id="11a3d-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="11a3d-133">A continuación, es importante esa lógica en la aplicación de dispositivo de hello de procesamiento de mensajes es *idempotente*, de modo que recibir Hola mismo mensaje varias veces genera Hola el mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="11a3d-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="11a3d-134">Una aplicación también temporalmente puede abandonar un mensaje, lo que resulta en el centro de IoT conserva el mensaje de saludo en cola de Hola para su futura utilización.</span><span class="sxs-lookup"><span data-stu-id="11a3d-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="11a3d-135">O bien, aplicación hello puede rechazar un mensaje, que quita de forma permanente los mensajes de bienvenida de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3d-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="11a3d-136">Para obtener más información acerca del ciclo de vida del mensaje en la nube al dispositivo de hello, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="11a3d-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="11a3d-137">Cuando se utiliza HTTP en lugar de MQTT o AMQP como transporte, Hola `ReceiveAsync` método vuelve inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="11a3d-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="11a3d-138">patrón de Hello admitida para los mensajes en la nube al dispositivo con HTTP es dispositivos conectados de forma intermitente que comprobación para mensajes con poca frecuencia (menor que cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="11a3d-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="11a3d-139">Emitir más HTTP recibe resultados en las solicitudes de centro de IoT limitación Hola.</span><span class="sxs-lookup"><span data-stu-id="11a3d-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="11a3d-140">Para obtener más información acerca de las diferencias de hello entre soporte MQTT, AMQP y HTTP y la limitación de centro de IoT, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="11a3d-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="11a3d-141">Agregar Hola siguiente método Hola **Main** método, justo antes de hello `Console.ReadLine()` línea:</span><span class="sxs-lookup"><span data-stu-id="11a3d-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="11a3d-142">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="11a3d-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="11a3d-143">En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].</span><span class="sxs-lookup"><span data-stu-id="11a3d-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="11a3d-144">Envío de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="11a3d-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="11a3d-145">En esta sección, se escribe una aplicación de consola .NET que envía mensajes en la nube al dispositivo toohello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11a3d-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="11a3d-146">En la solución de Visual Studio actual hello, crear un proyecto de aplicación de escritorio de Visual C# mediante hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="11a3d-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="11a3d-147">Proyecto de hello Name **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="11a3d-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Nuevo proyecto en Visual Studio][20]
2. <span data-ttu-id="11a3d-149">En el Explorador de soluciones, haga clic en soluciones de hello y, a continuación, haga clic en **administrar paquetes de NuGet para la solución... **.</span><span class="sxs-lookup"><span data-stu-id="11a3d-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="11a3d-150">Esta acción abre hello **administrar paquetes de NuGet** ventana.</span><span class="sxs-lookup"><span data-stu-id="11a3d-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="11a3d-151">Busque **Microsoft.Azure.Devices**, haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="11a3d-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="11a3d-152">Esta descarga, se instala y se agrega una referencia toohello [paquete de NuGet del SDK de servicios de Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="11a3d-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="11a3d-153">Agregue los siguiente hello `using` declaración en la parte superior de Hola de hello **Program.cs** archivo:</span><span class="sxs-lookup"><span data-stu-id="11a3d-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="11a3d-154">Agregar Hola después campos toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="11a3d-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="11a3d-155">Sustituir el valor de marcador de posición de hello con la cadena de conexión de base de datos central de hello IoT desde [empezar a trabajar con el centro de IoT]:</span><span class="sxs-lookup"><span data-stu-id="11a3d-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="11a3d-156">Agregar Hola siguiendo el método toohello **programa** clase:</span><span class="sxs-lookup"><span data-stu-id="11a3d-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="11a3d-157">Este método envía un nuevo dispositivo de toohello de mensaje en la nube al dispositivo con el Id. de hello, `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="11a3d-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="11a3d-158">Cambiar este parámetro únicamente si se ha modificado desde Hola utilizada en [empezar a trabajar con el centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="11a3d-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="11a3d-159">Por último, agregue Hola después líneas toohello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="11a3d-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="11a3d-160">Desde Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**. Seleccione **proyectos de inicio múltiples**, a continuación, seleccione hello **iniciar** acción para **ReadDeviceToCloudMessages**, **SimulatedDevice**, y **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="11a3d-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="11a3d-161">Presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="11a3d-161">Press **F5**.</span></span> <span data-ttu-id="11a3d-162">Deberían iniciarse las tres aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="11a3d-162">All three applications should start.</span></span> <span data-ttu-id="11a3d-163">Seleccione hello **SendCloudToDevice** windows y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="11a3d-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="11a3d-164">Debería ver con la aplicación de dispositivo de hello recibe el mensaje de saludo.</span><span class="sxs-lookup"><span data-stu-id="11a3d-164">You should see hello message being received by hello device app.</span></span>
   
   ![Aplicación que recibe el mensaje][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="11a3d-166">Recepción de comentarios de entrega</span><span class="sxs-lookup"><span data-stu-id="11a3d-166">Receive delivery feedback</span></span>
<span data-ttu-id="11a3d-167">Es confirmaciones de entrega (o expiración) de posibles toorequest centro de IoT para cada mensaje en la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11a3d-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="11a3d-168">Esta tooeasily de back-end de soluciones de opción habilita Hola informar a la lógica de reintento o compensación.</span><span class="sxs-lookup"><span data-stu-id="11a3d-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="11a3d-169">Para obtener más información sobre los comentarios de la nube al dispositivo, consulte hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="11a3d-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="11a3d-170">En esta sección, se modifica hello **SendCloudToDevice** comentarios de toorequest la aplicación y recibir desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="11a3d-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="11a3d-171">En Visual Studio, en hello **SendCloudToDevice** proyecto de equipo y agregar Hola siguiendo el método toohello **programa** clase.</span><span class="sxs-lookup"><span data-stu-id="11a3d-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="11a3d-172">Tenga en cuenta este patrón de recepción es Hola mismos mensajes de nube al dispositivo tooreceive usa uno de aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="11a3d-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="11a3d-173">Agregar Hola siguiente método Hola **Main** método, justo después de hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` línea:</span><span class="sxs-lookup"><span data-stu-id="11a3d-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="11a3d-174">comentarios de toorequest para la entrega de saludo del mensaje en la nube al dispositivo, tiene toospecify una propiedad en hello **SendCloudToDeviceMessageAsync** método.</span><span class="sxs-lookup"><span data-stu-id="11a3d-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="11a3d-175">Agregar Hola después de línea, justo después de hello `var commandMessage = new Message(...);` línea:</span><span class="sxs-lookup"><span data-stu-id="11a3d-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="11a3d-176">Ejecutar aplicaciones de hello presionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="11a3d-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="11a3d-177">Debería ver que se inician las tres aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="11a3d-177">You should see all three applications start.</span></span> <span data-ttu-id="11a3d-178">Seleccione hello **SendCloudToDevice** windows y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="11a3d-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="11a3d-179">Debería ver Hola de mensajes que se reciben por aplicación de dispositivo de hello y después de unos segundos, recibe el mensaje de Hola su **SendCloudToDevice** aplicación.</span><span class="sxs-lookup"><span data-stu-id="11a3d-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Aplicación que recibe el mensaje][22]

> [!NOTE]
> <span data-ttu-id="11a3d-181">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="11a3d-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="11a3d-182">En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].</span><span class="sxs-lookup"><span data-stu-id="11a3d-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="11a3d-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11a3d-183">Next steps</span></span>
<span data-ttu-id="11a3d-184">En este tutorial, se habrá aprendido cómo toosend y recibir mensajes en la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11a3d-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="11a3d-185">ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="11a3d-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="11a3d-186">toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="11a3d-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[paquete NuGet del SDK de Servicios IoT de Azure]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guía para desarrolladores de IoT Hub]: iot-hub-devguide.md
[Introducción al Centro de IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Documentación del Conjunto de aplicaciones de IoT]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDK de dispositivos IoT de Azure]: iot-hub-devguide-sdks.md