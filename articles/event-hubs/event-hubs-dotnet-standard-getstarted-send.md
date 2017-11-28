---
title: "Envío de eventos a Azure Event Hubs mediante .NET Standard | Microsoft Docs"
description: "Introducción al envío de eventos a Event Hubs en .NET Standard"
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
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="4e80f-103">Introducción al envío de mensajes a Azure Event Hubs en .NET Standard</span><span class="sxs-lookup"><span data-stu-id="4e80f-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="4e80f-104">Este ejemplo está disponible en [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="4e80f-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="4e80f-105">En este tutorial se muestra cómo escribir una aplicación de consola de .NET Core que envía un conjunto de mensajes a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e80f-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="4e80f-106">Puede ejecutar la solución de [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) tal cual está, reemplazando las cadenas`EhConnectionString` y `EhEntityPath` por los valores del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e80f-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="4e80f-107">También puede seguir los pasos de este tutorial para crear el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="4e80f-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e80f-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4e80f-108">Prerequisites</span></span>

* <span data-ttu-id="4e80f-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="4e80f-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="4e80f-110">En los ejemplos de este tutorial se usa Visual Studio 2017, pero también se admite Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4e80f-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="4e80f-111">[Herramientas de .NET Core Visual Studio 2015 o 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="4e80f-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="4e80f-112">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e80f-112">An Azure subscription.</span></span>
* <span data-ttu-id="4e80f-113">Un espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e80f-113">An event hub namespace.</span></span>

<span data-ttu-id="4e80f-114">Para enviar mensajes a un centro de eventos, escribiremos una aplicación de consola en C# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e80f-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="4e80f-115">Creación de un espacio de nombres de Event Hubs y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="4e80f-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="4e80f-116">El primer paso consiste en usar [Azure Portal](https://portal.azure.com) para crear un espacio de nombres de tipo de centro de eventos y obtener las credenciales de administración que la aplicación necesita para comunicarse con el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e80f-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="4e80f-117">Para crear un espacio de nombres y un centro de eventos, siga el procedimiento de [este artículo](event-hubs-create.md) y después continúe con los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="4e80f-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="4e80f-118">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="4e80f-118">Create a console application</span></span>

<span data-ttu-id="4e80f-119">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e80f-119">Start Visual Studio.</span></span> <span data-ttu-id="4e80f-120">En el menú **Archivo**, haga clic en **Nuevo** y en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="4e80f-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="4e80f-121">Cree una aplicación de consola de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4e80f-121">Create a .NET Core console application.</span></span>

![Nuevo proyecto][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="4e80f-123">Agregue el paquete NuGet de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4e80f-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="4e80f-124">Agregue el paquete NuGet de la biblioteca estándar .NET [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) a su proyecto siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4e80f-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="4e80f-125">Haga clic con el botón derecho en el proyecto recién creado y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4e80f-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="4e80f-126">Haga clic en la pestaña **Examinar** y, después, busque "Microsoft.Azure.EventHubs" y seleccione el paquete **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="4e80f-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="4e80f-127">Haga clic en **Instalar** para completar la instalación y, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e80f-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="4e80f-128">Escritura de código para enviar mensajes al centro de eventos</span><span class="sxs-lookup"><span data-stu-id="4e80f-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="4e80f-129">Agregue las siguientes instrucciones `using` al principio del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="4e80f-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="4e80f-130">Agregue constantes a la clase `Program` para la cadena de conexión de Event Hubs y la ruta de la entidad (nombre de centro de eventos individual).</span><span class="sxs-lookup"><span data-stu-id="4e80f-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="4e80f-131">Reemplace los marcadores de posición entre llaves por los valores adecuados obtenidos al crear el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e80f-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="4e80f-132">Agregue un nuevo método denominado `MainAsync` a la clase `Program`, de esta manera:</span><span class="sxs-lookup"><span data-stu-id="4e80f-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="4e80f-133">Agregue un nuevo método denominado `SendMessagesToEventHub` a la clase `Program`, de esta manera:</span><span class="sxs-lookup"><span data-stu-id="4e80f-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="4e80f-134">Agregue el siguiente código al método `Main` de la clase `Program`.</span><span class="sxs-lookup"><span data-stu-id="4e80f-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="4e80f-135">Este es el aspecto que debería tener Program.cs.</span><span class="sxs-lookup"><span data-stu-id="4e80f-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="4e80f-136">Ejecute el programa y asegúrese de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="4e80f-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="4e80f-137">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="4e80f-137">Congratulations!</span></span> <span data-ttu-id="4e80f-138">Ha enviado mensajes a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4e80f-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e80f-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e80f-139">Next steps</span></span>
<span data-ttu-id="4e80f-140">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4e80f-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="4e80f-141">Recepción de eventos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4e80f-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="4e80f-142">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4e80f-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="4e80f-143">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="4e80f-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="4e80f-144">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4e80f-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
