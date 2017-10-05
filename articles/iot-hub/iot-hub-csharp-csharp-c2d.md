---
title: Mensajes de nube a dispositivo con IoT Hub de Azure (.NET) | Microsoft Docs
description: "Cómo enviar mensajes de nube a un dispositivo de una instancia de IoT Hub de Azure mediante los SDK de IoT de Azure para .NET. Modifique una aplicación de dispositivo para recibir mensajes de nube a dispositivo y cambie una aplicación de back-end para enviar los mensajes de nube a dispositivo."
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
ms.openlocfilehash: 3f5f83671054c30afde3d7f18ff0edcdb8f78a01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a><span data-ttu-id="629ae-104">Envío de mensajes desde la nube al dispositivo con IoT Hub (.NET)</span><span class="sxs-lookup"><span data-stu-id="629ae-104">Send messages from the cloud to your device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="629ae-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="629ae-105">Introduction</span></span>
<span data-ttu-id="629ae-106">IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="629ae-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="629ae-107">El tutorial [Introducción a Iot Hub] muestra cómo crear un centro de IoT, aprovisionar la identidad de un dispositivo en él y programar una aplicación de dispositivo que envía mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="629ae-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="629ae-108">Este tutorial se basa en la [Introducción a Iot Hub].</span><span class="sxs-lookup"><span data-stu-id="629ae-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="629ae-109">En él se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="629ae-109">It shows you how to:</span></span>

* <span data-ttu-id="629ae-110">Desde el back-end de la nube de la aplicación, envíe mensajes de nube a dispositivo en un único dispositivo a través de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="629ae-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="629ae-111">Reciba mensajes de nube a dispositivo en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="629ae-112">Desde el back-end de la nube de la aplicación, solicite confirmación de entrega (*comentarios*) para los mensajes enviados a un dispositivo desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="629ae-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="629ae-113">Encontrará más información sobre los mensajes de nube a dispositivo en la [Guía para desarrolladores de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="629ae-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="629ae-114">Al final de este tutorial, ejecutará dos aplicaciones de consola de .NET:</span><span class="sxs-lookup"><span data-stu-id="629ae-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="629ae-115">**SimulatedDevice**, versión modificada de la aplicación creada en [Introducción a Iot Hub], que se conecta al Centro de IoT y recibe mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="629ae-116">**SendCloudToDevice**, que envía un mensaje de nube a dispositivo a la aplicación de dispositivo mediante IoT Hub y, luego, recibe su confirmación de entrega.</span><span class="sxs-lookup"><span data-stu-id="629ae-116">**SendCloudToDevice**, which sends a cloud-to-device message to the device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="629ae-117">IoT Hub ofrece compatibilidad con SDK para muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante [SDK de dispositivos IoT de Azure].</span><span class="sxs-lookup"><span data-stu-id="629ae-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="629ae-118">Para obtener instrucciones paso a paso sobre cómo conectar el dispositivo al código de este tutorial y, en general a Azure IoT Hub consulte la [Guía del desarrollador de IoTHub de Azure].</span><span class="sxs-lookup"><span data-stu-id="629ae-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="629ae-119">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="629ae-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="629ae-120">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="629ae-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="629ae-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="629ae-121">An active Azure account.</span></span> <span data-ttu-id="629ae-122">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="629ae-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-device-app"></a><span data-ttu-id="629ae-123">Recepción de mensajes en la aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="629ae-123">Receive messages in the device app</span></span>
<span data-ttu-id="629ae-124">En esta sección, modificará la aplicación de dispositivo que creó en el tutorial [Introducción a Iot Hub] para recibir mensajes de nube a dispositivo desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="629ae-124">In this section, you'll modify the device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="629ae-125">En Visual Studio, en el proyecto **SimulatedDevice**, agregue el método siguiente a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="629ae-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
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
   
    <span data-ttu-id="629ae-126">El método `ReceiveAsync` devuelve de forma asincrónica el mensaje recibido en el momento en que lo recibe el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="629ae-127">Se devuelve *null* tras un período de espera que se puede especificar (en este caso, se usa el valor predeterminado de un minuto).</span><span class="sxs-lookup"><span data-stu-id="629ae-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="629ae-128">Cuando la aplicación recibe un valor *null*, debe continuar esperando nuevos mensajes.</span><span class="sxs-lookup"><span data-stu-id="629ae-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="629ae-129">Este requisito es el motivo de la línea `if (receivedMessage == null) continue`.</span><span class="sxs-lookup"><span data-stu-id="629ae-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="629ae-130">La llamada a `CompleteAsync()` notifica al Centro de IoT que el mensaje se ha procesado correctamente.</span><span class="sxs-lookup"><span data-stu-id="629ae-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="629ae-131">Los mensajes pueden quitarse con seguridad de la cola del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="629ae-132">Si ha sucedido algo que ha impedido que la aplicación del dispositivo termine de procesar el mensaje, el Centro de IoT lo entrega de nuevo.</span><span class="sxs-lookup"><span data-stu-id="629ae-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="629ae-133">Es importante que la lógica de procesamiento de mensajes de la aplicación de dispositivo sea *idempotente*, de modo que, si se recibe el mismo mensaje varias veces, se genera el mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="629ae-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="629ae-134">Una aplicación también puede abandonar temporalmente un mensaje, lo que da lugar a que el Centro de IoT retenga el mensaje en la cola para su consumo futuro.</span><span class="sxs-lookup"><span data-stu-id="629ae-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="629ae-135">O bien, la aplicación puede rechazar un mensaje, de forma que este se quita permanentemente de la cola.</span><span class="sxs-lookup"><span data-stu-id="629ae-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="629ae-136">Para obtener más información sobre el ciclo de vida de los mensajes de nube a dispositivo, consulte la [Guía del desarrollador de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="629ae-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="629ae-137">Cuando se usa HTTP en lugar de MQTT o AMQP como transporte, el método `ReceiveAsync` se devuelve inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="629ae-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="629ae-138">El patrón admitido para los mensajes de nube a dispositivo con HTTP es dispositivos conectados de forma intermitente que buscan mensajes con poca frecuencia (menos de 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="629ae-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="629ae-139">Emitir más recepciones HTTP tendrá como resultado la limitación de solicitudes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="629ae-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="629ae-140">Para obtener más información sobre las diferencias entre la compatibilidad con MQTT, AMQP y HTTP, y la limitación de IoT Hub, consulte la [Guía del desarrollador de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="629ae-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="629ae-141">Agregue el siguiente método en el método **Main**, inmediatamente delante de la línea `Console.ReadLine()`:</span><span class="sxs-lookup"><span data-stu-id="629ae-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="629ae-142">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="629ae-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="629ae-143">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling](Control de errores transitorios).</span><span class="sxs-lookup"><span data-stu-id="629ae-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="629ae-144">Envío de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="629ae-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="629ae-145">En esta sección, escribirá una aplicación de consola de .NET que envía mensajes de nube a dispositivo a la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-145">In this section, you write a .NET console app that sends cloud-to-device messages to the device app.</span></span>

1. <span data-ttu-id="629ae-146">En la solución actual de Visual Studio, cree un proyecto de aplicación de escritorio de Visual C# con la plantilla de proyecto **Aplicación de consola**.</span><span class="sxs-lookup"><span data-stu-id="629ae-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="629ae-147">Denomine el proyecto **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="629ae-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![Nuevo proyecto en Visual Studio][20]
2. <span data-ttu-id="629ae-149">En el Explorador de soluciones, haga clic con el botón derecho en la solución y luego haga clic en **Administrar paquetes de NuGet para la solución...**.</span><span class="sxs-lookup"><span data-stu-id="629ae-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="629ae-150">Esta acción abre la ventana **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="629ae-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="629ae-151">Busque **Microsoft.Azure.Devices**, haga clic en **Instalar** y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="629ae-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="629ae-152">De esta forma, se descarga, instala y agrega una referencia al [paquete NuGet del SDK de Servicios IoT de Azure].</span><span class="sxs-lookup"><span data-stu-id="629ae-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="629ae-153">Agregue la siguiente instrucción `using` en la parte superior del archivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="629ae-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="629ae-154">Agregue los campos siguientes a la clase **Program** .</span><span class="sxs-lookup"><span data-stu-id="629ae-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="629ae-155">Sustituya el valor de marcador de posición por la cadena de conexión de IoT Hub de [Introducción a Iot Hub]:</span><span class="sxs-lookup"><span data-stu-id="629ae-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="629ae-156">Agregue el método siguiente a la clase **Program** :</span><span class="sxs-lookup"><span data-stu-id="629ae-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="629ae-157">Este método envía un nuevo mensaje de la nube al dispositivo con el identificador `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="629ae-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="629ae-158">Cambie este parámetro solo si lo modificó con respecto del utilizado en [Introducción a Iot Hub].</span><span class="sxs-lookup"><span data-stu-id="629ae-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="629ae-159">Por último, agregue las líneas siguientes al método **Main** :</span><span class="sxs-lookup"><span data-stu-id="629ae-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="629ae-160">Desde Visual Studio, haga clic con el botón derecho en la solución y seleccione **Establecer proyectos de inicio**. Seleccione **Proyectos de inicio múltiples** y elija la acción **Iniciar** para **ReadDeviceToCloudMessages**, **SimulatedDevice** y **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="629ae-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="629ae-161">Presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="629ae-161">Press **F5**.</span></span> <span data-ttu-id="629ae-162">Deberían iniciarse las tres aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="629ae-162">All three applications should start.</span></span> <span data-ttu-id="629ae-163">Seleccione la ventana **SendCloudToDevice** y presione **Intro**.</span><span class="sxs-lookup"><span data-stu-id="629ae-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="629ae-164">Debería ver el mensaje que recibe la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-164">You should see the message being received by the device app.</span></span>
   
   ![Aplicación que recibe el mensaje][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="629ae-166">Recepción de comentarios de entrega</span><span class="sxs-lookup"><span data-stu-id="629ae-166">Receive delivery feedback</span></span>
<span data-ttu-id="629ae-167">Es posible solicitar confirmaciones de entrega (o expiración) del Centro de IoT para cada mensaje de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="629ae-168">Esta opción permite que el back-end de solución notifique fácilmente la lógica de reintento o compensación.</span><span class="sxs-lookup"><span data-stu-id="629ae-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="629ae-169">Para obtener más información sobre los comentarios de nube a dispositivo, consulte la [Guía del desarrollador de IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="629ae-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="629ae-170">En esta sección, modificará la aplicación **SendCloudToDevice** para solicitar comentarios y recibirlos de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="629ae-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="629ae-171">En Visual Studio, en el proyecto **SendCloudToDevice**, agregue el método siguiente a la clase **Program**.</span><span class="sxs-lookup"><span data-stu-id="629ae-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
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
   
    <span data-ttu-id="629ae-172">Tenga en cuenta que este patrón de recepción es el mismo que se usa para recibir mensajes de nube a dispositivo desde la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="629ae-173">Agregue el siguiente método en **Main** inmediatamente después de la línea `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)`:</span><span class="sxs-lookup"><span data-stu-id="629ae-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="629ae-174">Para solicitar comentarios de la entrega del mensaje de la nube a un dispositivo, debe especificar una propiedad en el método **SendCloudToDeviceMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="629ae-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="629ae-175">Agregue la línea siguiente, inmediatamente después de la línea `var commandMessage = new Message(...);` :</span><span class="sxs-lookup"><span data-stu-id="629ae-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="629ae-176">Ejecute las aplicaciones presionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="629ae-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="629ae-177">Debería ver que se inician las tres aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="629ae-177">You should see all three applications start.</span></span> <span data-ttu-id="629ae-178">Seleccione la ventana **SendCloudToDevice** y presione **Intro**.</span><span class="sxs-lookup"><span data-stu-id="629ae-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="629ae-179">Verá los mensajes que recibe la aplicación de dispositivo y, al cabo de unos segundos, el mensaje de comentarios que recibe la aplicación **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="629ae-179">You should see the message being received by the device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Aplicación que recibe el mensaje][22]

> [!NOTE]
> <span data-ttu-id="629ae-181">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="629ae-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="629ae-182">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling](Control de errores transitorios).</span><span class="sxs-lookup"><span data-stu-id="629ae-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="629ae-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="629ae-183">Next steps</span></span>
<span data-ttu-id="629ae-184">En este tutorial, aprendió a enviar y recibir mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="629ae-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="629ae-185">Para ver ejemplos de soluciones completas de un extremo a otro que usen el Centro de IoT, consulte [Documentación del Conjunto de aplicaciones de IoT].</span><span class="sxs-lookup"><span data-stu-id="629ae-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="629ae-186">Para obtener más información sobre cómo desarrollar soluciones con IoT Hub, consulte la [Guía del desarrollador de IoTHub de Azure].</span><span class="sxs-lookup"><span data-stu-id="629ae-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[paquete NuGet del SDK de Servicios IoT de Azure]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guía del desarrollador de IoTHub de Azure]: iot-hub-devguide.md
[Introducción a Iot Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Documentación del Conjunto de aplicaciones de IoT]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDK de dispositivos IoT de Azure]: iot-hub-devguide-sdks.md