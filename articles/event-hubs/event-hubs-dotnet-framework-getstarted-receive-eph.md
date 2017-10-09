---
title: Hola a aaaReceive eventos desde los centros de eventos de Azure mediante .NET Framework | Documentos de Microsoft
description: Siga este tutorial tooreceive eventos desde los centros de eventos de Azure con hello .NET Framework.
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="7b9b3-103">Recibir eventos desde los centros de eventos de Azure con hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="7b9b3-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="7b9b3-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="7b9b3-104">Introduction</span></span>

<span data-ttu-id="7b9b3-105">Event Hubs es un servicio que procesa grandes cantidades de datos de eventos (telemetría) desde aplicaciones y dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="7b9b3-106">Después de recopilar datos en los centros de eventos, puede almacenar datos de hello mediante un clúster de almacenamiento o transformar mediante un proveedor de análisis en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="7b9b3-107">Esta capacidad de procesamiento y la colección de eventos a gran escala es un componente clave de arquitecturas de aplicación moderna incluidos Hola Internet de las cosas (IoT).</span><span class="sxs-lookup"><span data-stu-id="7b9b3-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="7b9b3-108">Este tutorial muestra cómo toowrite de .NET Framework consola aplicación que recibe los mensajes de un concentrador de eventos con hello  **[Host procesador de eventos][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="7b9b3-109">eventos de toosend mediante Hola .NET Framework, vea hello [enviar eventos tooAzure centros de eventos mediante .NET Framework hello](event-hubs-dotnet-framework-getstarted-send.md) el artículo, o haga clic en el idioma envío adecuado de hello en la tabla de contenido izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="7b9b3-110">Hola [Host procesador de eventos] [ EventProcessorHost] es una clase .NET que simplifica la reciba los eventos de los centros de eventos mediante la administración de los puntos de control persistentes y paralelo recibe de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="7b9b3-111">Con hello [Host procesador de eventos][Event Processor Host], puede dividir los eventos de varios receptores, incluso cuando se hospeda en distintos nodos.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="7b9b3-112">Este ejemplo se muestra cómo hello toouse [Host procesador de eventos] [ EventProcessorHost] para un único receptor.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="7b9b3-113">Hola [escalar horizontalmente el procesamiento de eventos] [ Scale out Event Processing with Event Hubs] ejemplo muestra cómo hello toouse [Host procesador de eventos] [ EventProcessorHost] con varios receptores.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b9b3-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b9b3-114">Prerequisites</span></span>

<span data-ttu-id="7b9b3-115">toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="7b9b3-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="7b9b3-116">[Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="7b9b3-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="7b9b3-117">capturas de pantalla de Hello en este tutorial utilizan Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="7b9b3-118">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-118">An active Azure account.</span></span> <span data-ttu-id="7b9b3-119">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="7b9b3-120">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7b9b3-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="7b9b3-121">Creación de un espacio de nombres de Event Hubs y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="7b9b3-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="7b9b3-122">Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres del tipo centros de eventos y obtener Hola credenciales de administración de la aplicación necesita toocommunicate con el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="7b9b3-123">toocreate un espacio de nombres y el concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md), a continuación, continúe con hello sigue los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="7b9b3-124">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7b9b3-124">Create an Azure Storage account</span></span>

<span data-ttu-id="7b9b3-125">Hola toouse [Host procesador de eventos][EventProcessorHost], debe tener un [cuenta de almacenamiento de Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="7b9b3-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="7b9b3-126">Inicie sesión en toohello [portal de Azure][Azure portal]y haga clic en **New** en hello parte superior izquierda de la pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="7b9b3-127">Haga clic en **Storage** y luego en **Cuenta de Storage**.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="7b9b3-128">Hola **crear cuenta de almacenamiento** hoja, escriba un nombre para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="7b9b3-129">Elija una suscripción de Azure, el grupo de recursos y la ubicación en el recurso que hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="7b9b3-130">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="7b9b3-131">Hola lista de cuentas de almacenamiento, haga clic en hello recién creado la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="7b9b3-132">En la hoja de la cuenta de almacenamiento de hello, haga clic en **las claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="7b9b3-133">Copiar valor de Hola de **key1** toouse más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="7b9b3-134">Creación de una aplicación de consola de destinatario</span><span class="sxs-lookup"><span data-stu-id="7b9b3-134">Create a receiver console application</span></span>

1. <span data-ttu-id="7b9b3-135">En Visual Studio, cree un nuevo proyecto de aplicación de escritorio de Visual C# con hello **aplicación de consola** plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="7b9b3-136">Proyecto de hello Name **receptor**.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="7b9b3-137">En el Explorador de soluciones, haga clic en hello **receptor** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet para la solución**.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="7b9b3-138">Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="7b9b3-139">Haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="7b9b3-140">Visual Studio descarga, instala y agrega una referencia toohello [centro de eventos de Bus de servicio de Azure - paquete de EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), con todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="7b9b3-141">Menú contextual hello **receptor** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="7b9b3-142">Hola nueva clase el nombre **SimpleEventProcessor**y, a continuación, haga clic en **agregar** clase de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="7b9b3-143">Agregue Hola siguiendo las instrucciones al principio de hello del archivo de SimpleEventProcessor.cs de hello:</span><span class="sxs-lookup"><span data-stu-id="7b9b3-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="7b9b3-144">A continuación, sustituya Hola siguiente código en el cuerpo de Hola de clase hello:</span><span class="sxs-lookup"><span data-stu-id="7b9b3-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  <span data-ttu-id="7b9b3-145">Esta clase se denomina por hello **EventProcessorHost** eventos de tooprocess recibidos desde el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="7b9b3-146">Hola `SimpleEventProcessor` clase utiliza un método de punto de comprobación de cronómetro tooperiodically llamada hello en hello **EventProcessorHost** contexto.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="7b9b3-147">Este proceso garantiza que, si se reinicia el receptor de hello, pierde no más de cinco minutos de trabajo de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="7b9b3-148">Hola **programa** de clases, agregue los siguientes hello `using` declaración en la parte superior de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="7b9b3-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="7b9b3-149">A continuación, reemplace hello `Main` método Hola `Program` clase con el siguiente código de hello, sustituyendo el nombre del centro de eventos de Hola y conexiones de nivel de espacio de nombres de Hola de cadena que se guardó anteriormente y Hola cuenta de almacenamiento y la clave que ha copiado en hello secciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="7b9b3-150">Ejecutar programa hello y asegúrese de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="7b9b3-151">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="7b9b3-151">Congratulations!</span></span> <span data-ttu-id="7b9b3-152">Ahora ha recibido mensajes de un concentrador de eventos mediante Hola Host procesador de eventos.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="7b9b3-153">Este tutorial usa una sola instancia de [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="7b9b3-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="7b9b3-154">tooincrease rendimiento, se recomienda ejecutar varias instancias de [EventProcessorHost][EventProcessorHost], tal y como se muestra en hello [escala espera de procesamiento de eventos] [escala espera de procesamiento de eventos] ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="7b9b3-155">En esos casos, hello diversas instancias automáticamente coordinan entre sí eventos de tooload saldo Hola recibido.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="7b9b3-156">Si desea que el proceso de varios receptores tooeach *todos los* Hola eventos, debe usar hello **ConsumerGroup** concepto.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="7b9b3-157">Cuando se reciben eventos de equipos diferentes, podría ser útil toospecify nombres para [EventProcessorHost] [ EventProcessorHost] instancias basadas en máquinas de hello (o roles) en que se implementan.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="7b9b3-158">Para obtener más información acerca de estos temas, vea hello [información general de los centros de eventos] [ Event Hubs overview] hello y [Guía de programación de los centros de eventos] [ Event Hubs Programming Guide] temas.</span><span class="sxs-lookup"><span data-stu-id="7b9b3-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7b9b3-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b9b3-159">Next steps</span></span>

<span data-ttu-id="7b9b3-160">Ahora que ha creado una aplicación que crea un centro de eventos y envía y recibe datos, puede aprender más visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="7b9b3-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="7b9b3-161">[Event​Processor​Host Class][Event Processor Host] (Clase EventProcessor​Host)</span><span class="sxs-lookup"><span data-stu-id="7b9b3-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="7b9b3-162">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="7b9b3-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="7b9b3-163">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7b9b3-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
