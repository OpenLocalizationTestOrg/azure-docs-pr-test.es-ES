---
title: "Recepción de eventos desde Azure Event Hubs mediante .NET Standard | Microsoft Docs"
description: "Introducción a la recepción de mensajes con EventProcessorHost en .NET Standard"
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="58159-103">Introducción a la recepción de mensajes con el Host del procesador de eventos en .NET Standard</span><span class="sxs-lookup"><span data-stu-id="58159-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="58159-104">Este ejemplo está disponible en [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="58159-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="58159-105">En este tutorial se muestra cómo escribir una aplicación de consola de .NET Core que recibe mensajes de un centro de eventos mediante **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="58159-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="58159-106">Puede ejecutar la solución de [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) tal como está, reemplazando las cadenas por los valores de la cuenta de almacenamiento y centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="58159-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="58159-107">También puede seguir los pasos de este tutorial para crear el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="58159-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58159-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="58159-108">Prerequisites</span></span>

* <span data-ttu-id="58159-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="58159-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="58159-110">En los ejemplos de este tutorial se usa Visual Studio 2017, pero también se admite Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="58159-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="58159-111">[Herramientas de .NET Core Visual Studio 2015 o 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="58159-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="58159-112">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58159-112">An Azure subscription.</span></span>
* <span data-ttu-id="58159-113">Un espacio de nombres de Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="58159-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="58159-114">Una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="58159-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="58159-115">Creación de un espacio de nombres de Event Hubs y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="58159-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="58159-116">El primer paso consiste en usar [Azure Portal](https://portal.azure.com) para crear un espacio de nombres de tipo Event Hubs y obtener las credenciales de administración que la aplicación necesita para comunicarse con el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="58159-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="58159-117">Para crear un espacio de nombres y un centro de eventos, siga el procedimiento de [este artículo](event-hubs-create.md) y después continúe con los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="58159-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="58159-118">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="58159-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="58159-119">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58159-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="58159-120">En el panel de navegación izquierdo del portal, haga clic en **Nuevo**, luego en **Almacenamiento** y, a continuación, en **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="58159-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="58159-121">Complete los campos de la hoja de la cuenta de almacenamiento y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="58159-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Crear cuenta de almacenamiento][1]

4. <span data-ttu-id="58159-123">Una vez que aparezca el mensaje **Implementaciones correctas**, haga clic en el nombre de la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="58159-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="58159-124">En la hoja **Essentials**, haga clic en **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="58159-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="58159-125">Cuando se abra la hoja **Blob service**, haga clic en **+ Container** (Contenedor +) en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="58159-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="58159-126">Asigne un nombre al contenedor y cierre la hoja **Blob Service**.</span><span class="sxs-lookup"><span data-stu-id="58159-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="58159-127">Haga clic en **Claves de acceso** en la hoja izquierda y copie el nombre del contenedor de almacenamiento, la cuenta de almacenamiento y el valor de **key1**.</span><span class="sxs-lookup"><span data-stu-id="58159-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="58159-128">Guarde estos valores en el Bloc de notas, o en cualquier otra ubicación temporal.</span><span class="sxs-lookup"><span data-stu-id="58159-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="58159-129">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="58159-129">Create a console application</span></span>

<span data-ttu-id="58159-130">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58159-130">Start Visual Studio.</span></span> <span data-ttu-id="58159-131">En el menú **Archivo**, haga clic en **Nuevo** y en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="58159-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="58159-132">Cree una aplicación de consola de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="58159-132">Create a .NET Core console application.</span></span>

![Nuevo proyecto][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="58159-134">Agregue el paquete NuGet de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="58159-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="58159-135">Agregue los paquetes NuGet de la biblioteca estándar .NET [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) y [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) a su proyecto siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="58159-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="58159-136">Haga clic con el botón derecho en el proyecto recién creado y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="58159-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="58159-137">Haga clic en la pestaña **Examinar** y, después, busque "Microsoft.Azure.EventHubs" y seleccione el paquete **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="58159-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="58159-138">Haga clic en **Instalar** para completar la instalación y, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="58159-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="58159-139">Repita los pasos 1 y 2 e instale el paquete **Microsoft.Azure.EventHubs.Processor**.</span><span class="sxs-lookup"><span data-stu-id="58159-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="58159-140">Implemente la interfaz de IEventProcessor.</span><span class="sxs-lookup"><span data-stu-id="58159-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="58159-141">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y después en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="58159-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="58159-142">Asigne el nombre **SimpleEventProcessor** a la nueva clase.</span><span class="sxs-lookup"><span data-stu-id="58159-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="58159-143">Abra el archivo SimpleEventProcessor.cs y agregue las siguientes instrucciones `using` en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="58159-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="58159-144">Implemente la interfaz `IEventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="58159-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="58159-145">Reemplace todo el contenido de la clase `SimpleEventProcessor` con el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="58159-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="58159-146">Escritura de un método de consola principal que usa la clase SimpleEventProcessor para recibir mensajes</span><span class="sxs-lookup"><span data-stu-id="58159-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="58159-147">Agregue las siguientes instrucciones `using` al principio del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="58159-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="58159-148">Agregue constantes a la clase `Program` para la cadena de conexión del centro de eventos, el nombre del centro de eventos, el nombre del contenedor de la cuenta de almacenamiento, y el nombre de la cuenta de almacenamiento y la clave de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="58159-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="58159-149">Agregue el código siguiente, reemplazando los marcadores de posición con sus valores correspondientes.</span><span class="sxs-lookup"><span data-stu-id="58159-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="58159-150">Agregue un nuevo método denominado `MainAsync` a la clase `Program`, de esta manera:</span><span class="sxs-lookup"><span data-stu-id="58159-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="58159-151">Agregue la siguiente línea de código al método `Main`:</span><span class="sxs-lookup"><span data-stu-id="58159-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="58159-152">Este es el aspecto que debería tener el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="58159-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="58159-153">Ejecute el programa y asegúrese de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="58159-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="58159-154">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="58159-154">Congratulations!</span></span> <span data-ttu-id="58159-155">Recibió mensajes de un centro de eventos mediante el host de procesador de eventos.</span><span class="sxs-lookup"><span data-stu-id="58159-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58159-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="58159-156">Next steps</span></span>
<span data-ttu-id="58159-157">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="58159-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="58159-158">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="58159-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="58159-159">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="58159-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="58159-160">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="58159-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
