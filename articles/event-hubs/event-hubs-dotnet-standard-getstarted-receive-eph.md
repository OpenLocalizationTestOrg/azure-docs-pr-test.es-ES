---
title: "aaaReceive eventos desde los centros de eventos de Azure mediante .NET estándar | Documentos de Microsoft"
description: "Empezar a recibir mensajes con hello EventProcessorHost en .NET estándar"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="81a3a-103">Empezar a recibir mensajes con hello Host procesador de eventos de .NET estándar</span><span class="sxs-lookup"><span data-stu-id="81a3a-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="81a3a-104">Este ejemplo está disponible en [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="81a3a-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="81a3a-105">Este tutorial muestra cómo el aplicación que recibe mensajes de un concentrador de eventos mediante el uso de la consola de toowrite un núcleo de .NET **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="81a3a-106">Puede ejecutar hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solución como-se, reemplazar cadenas de hello con sus valores de cuenta de concentrador y el almacenamiento de eventos.</span><span class="sxs-lookup"><span data-stu-id="81a3a-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="81a3a-107">O bien puede seguir Hola los pasos de este tutorial toocreate sus propios.</span><span class="sxs-lookup"><span data-stu-id="81a3a-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81a3a-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="81a3a-108">Prerequisites</span></span>

* <span data-ttu-id="81a3a-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="81a3a-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="81a3a-110">ejemplos de Hello en este tutorial, use Visual Studio de 2017, pero Visual Studio 2015 también es compatible.</span><span class="sxs-lookup"><span data-stu-id="81a3a-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="81a3a-111">[Herramientas de .NET Core Visual Studio 2015 o 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="81a3a-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="81a3a-112">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="81a3a-112">An Azure subscription.</span></span>
* <span data-ttu-id="81a3a-113">Un espacio de nombres de Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="81a3a-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="81a3a-114">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="81a3a-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="81a3a-115">Creación de un espacio de nombres de Event Hubs y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="81a3a-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="81a3a-116">Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres para los concentradores de eventos de hello escriba y obtener las credenciales de administración que la aplicación necesita toocommunicate con el concentrador de eventos de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="81a3a-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="81a3a-117">toocreate un espacio de nombres y el concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md)y, a continuación, continúe con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="81a3a-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="81a3a-118">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="81a3a-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="81a3a-119">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81a3a-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="81a3a-120">En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, haga clic en **almacenamiento**y, a continuación, haga clic en **cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="81a3a-121">Complete los campos de hello en la hoja de cuenta de almacenamiento de hello y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Crear cuenta de almacenamiento][1]

4. <span data-ttu-id="81a3a-123">Después de ver hello **se ha realizado correctamente en implementaciones** de mensajes, haga clic en nombre de Hola de hello nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="81a3a-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="81a3a-124">Hola **Essentials** hoja, haga clic en **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="81a3a-125">Cuando Hola **servicio Blob** hoja se abre, haga clic en **+ contenedor** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="81a3a-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="81a3a-126">Asigne un nombre de contenedor de hello y, a continuación, cierre hello **servicio Blob** hoja.</span><span class="sxs-lookup"><span data-stu-id="81a3a-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="81a3a-127">Haga clic en **las claves de acceso** en hello izquierdo hoja y copia Hola el nombre del contenedor de almacenamiento de hello, la cuenta de almacenamiento de Hola y el valor de Hola de **key1**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="81a3a-128">Guardar estos valores tooNotepad o alguna otra ubicación temporal.</span><span class="sxs-lookup"><span data-stu-id="81a3a-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="81a3a-129">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="81a3a-129">Create a console application</span></span>

<span data-ttu-id="81a3a-130">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81a3a-130">Start Visual Studio.</span></span> <span data-ttu-id="81a3a-131">De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="81a3a-132">Cree una aplicación de consola de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="81a3a-132">Create a .NET Core console application.</span></span>

![Nuevo proyecto][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="81a3a-134">Agregar paquete de NuGet de concentradores de eventos de Hola</span><span class="sxs-lookup"><span data-stu-id="81a3a-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="81a3a-135">Agregar hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) y [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) proyecto del tooyour de paquetes de NuGet de .NET estándar biblioteca siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="81a3a-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="81a3a-136">Haga clic en proyecto de hello recién creado y seleccione **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="81a3a-137">Haga clic en hello **examinar** ficha, realice una búsqueda de "Microsoft.Azure.EventHubs" y seleccione hello **Microsoft.Azure.EventHubs** paquete.</span><span class="sxs-lookup"><span data-stu-id="81a3a-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="81a3a-138">Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81a3a-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="81a3a-139">Repita los pasos 1 y 2 e instalar hello **Microsoft.Azure.EventHubs.Processor** paquete.</span><span class="sxs-lookup"><span data-stu-id="81a3a-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="81a3a-140">Implementar una interfaz IEventProcessor Hola</span><span class="sxs-lookup"><span data-stu-id="81a3a-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="81a3a-141">En el Explorador de soluciones, proyectos de Hola de menú contextual, haga clic en **agregar**y, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="81a3a-142">Hola nueva clase el nombre **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="81a3a-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="81a3a-143">Abra el archivo de SimpleEventProcessor.cs hello y agregue Hola siguiente `using` parte superior de toohello de las instrucciones del archivo hello.</span><span class="sxs-lookup"><span data-stu-id="81a3a-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="81a3a-144">Hola implemente `IEventProcessor` interfaz.</span><span class="sxs-lookup"><span data-stu-id="81a3a-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="81a3a-145">Reemplace todo contenido de Hola de hello `SimpleEventProcessor` clase con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="81a3a-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="81a3a-146">Escribir un método de la consola principal que utiliza los mensajes de Hola SimpleEventProcessor clase tooreceive</span><span class="sxs-lookup"><span data-stu-id="81a3a-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="81a3a-147">Agregue los siguiente hello `using` parte superior de toohello de las instrucciones del archivo Program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="81a3a-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="81a3a-148">Agregar constantes toohello `Program` clase para la cadena de conexión de concentrador de eventos de Hola, nombre del concentrador de eventos, el nombre de contenedor de cuenta de almacenamiento, nombre de la cuenta de almacenamiento y clave de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="81a3a-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="81a3a-149">Agregar Hola siguiente código, reemplazando los marcadores de posición de hello con sus valores correspondientes.</span><span class="sxs-lookup"><span data-stu-id="81a3a-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="81a3a-150">Agregar un nuevo método denominado `MainAsync` toohello `Program` de la clase, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="81a3a-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="81a3a-151">Agregar Hola después de la línea de código toohello `Main` método:</span><span class="sxs-lookup"><span data-stu-id="81a3a-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="81a3a-152">Este es el aspecto que debería tener el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="81a3a-152">Here is what your Program.cs file should look like:</span></span>

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="81a3a-153">Ejecutar programa hello y asegúrese de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="81a3a-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="81a3a-154">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="81a3a-154">Congratulations!</span></span> <span data-ttu-id="81a3a-155">Ahora ha recibido mensajes de un concentrador de eventos mediante el uso de hello Host procesador de eventos.</span><span class="sxs-lookup"><span data-stu-id="81a3a-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81a3a-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81a3a-156">Next steps</span></span>
<span data-ttu-id="81a3a-157">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="81a3a-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="81a3a-158">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="81a3a-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="81a3a-159">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="81a3a-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="81a3a-160">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="81a3a-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
