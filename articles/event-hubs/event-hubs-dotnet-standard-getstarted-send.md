---
title: "aaaSend eventos tooAzure centros de eventos mediante el estándar de .NET | Documentos de Microsoft"
description: "Empezar a enviar tooEvent centros de eventos en el estándar de .NET"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="01a16-103">Empezar a enviar mensajes tooAzure centros de eventos de .NET estándar</span><span class="sxs-lookup"><span data-stu-id="01a16-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="01a16-104">Este ejemplo está disponible en [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="01a16-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="01a16-105">Este tutorial muestra cómo toowrite una aplicación de consola .NET Core que envía un conjunto de mensajes tooan concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="01a16-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="01a16-106">Puede ejecutar hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solución como-se, reemplazando hello `EhConnectionString` y `EhEntityPath` cadenas con sus valores de concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="01a16-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="01a16-107">O bien puede seguir Hola los pasos de este tutorial toocreate sus propios.</span><span class="sxs-lookup"><span data-stu-id="01a16-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01a16-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="01a16-108">Prerequisites</span></span>

* <span data-ttu-id="01a16-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="01a16-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="01a16-110">ejemplos de Hello en este tutorial, use Visual Studio de 2017, pero Visual Studio 2015 también es compatible.</span><span class="sxs-lookup"><span data-stu-id="01a16-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="01a16-111">[Herramientas de .NET Core Visual Studio 2015 o 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="01a16-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="01a16-112">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="01a16-112">An Azure subscription.</span></span>
* <span data-ttu-id="01a16-113">Un espacio de nombres del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="01a16-113">An event hub namespace.</span></span>

<span data-ttu-id="01a16-114">Centro de eventos de toosend mensajes tooan, usaremos toowrite de Visual Studio una aplicación de consola de C#.</span><span class="sxs-lookup"><span data-stu-id="01a16-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="01a16-115">Creación de un espacio de nombres de Event Hubs y un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="01a16-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="01a16-116">Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres para el tipo de concentrador de eventos de hello y obtener las credenciales de administración que la aplicación necesita toocommunicate con el concentrador de eventos de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a16-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="01a16-117">toocreate un espacio de nombres y un concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md)y, a continuación, continúe con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="01a16-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="01a16-118">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="01a16-118">Create a console application</span></span>

<span data-ttu-id="01a16-119">Inicie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01a16-119">Start Visual Studio.</span></span> <span data-ttu-id="01a16-120">De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="01a16-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="01a16-121">Cree una aplicación de consola de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="01a16-121">Create a .NET Core console application.</span></span>

![Nuevo proyecto][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="01a16-123">Agregar paquete de NuGet de concentradores de eventos de Hola</span><span class="sxs-lookup"><span data-stu-id="01a16-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="01a16-124">Agregar hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) proyecto del tooyour de paquete de NuGet de .NET estándar biblioteca siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="01a16-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="01a16-125">Haga clic en proyecto de hello recién creado y seleccione **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="01a16-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="01a16-126">Haga clic en hello **examinar** ficha, realice una búsqueda de "Microsoft.Azure.EventHubs" y seleccione hello **Microsoft.Azure.EventHubs** paquete.</span><span class="sxs-lookup"><span data-stu-id="01a16-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="01a16-127">Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01a16-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="01a16-128">Escribir algunas concentrador de eventos de código toosend mensajes toohello</span><span class="sxs-lookup"><span data-stu-id="01a16-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="01a16-129">Agregue los siguiente hello `using` parte superior de toohello de las instrucciones del archivo Program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a16-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="01a16-130">Agregar constantes toohello `Program` clase para hello centros de eventos conexión entidad y la cadena de ruta de acceso (nombre de concentrador de eventos individuales).</span><span class="sxs-lookup"><span data-stu-id="01a16-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="01a16-131">Reemplace los marcadores de posición de hello corchetes con los valores adecuados de Hola que se obtuvieron al crear el concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="01a16-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="01a16-132">Agregar un nuevo método denominado `MainAsync` toohello `Program` de la clase, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="01a16-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="01a16-133">Agregar un nuevo método denominado `SendMessagesToEventHub` toohello `Program` de la clase, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="01a16-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
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

5. <span data-ttu-id="01a16-134">Agregar Hola después código toohello `Main` método Hola `Program` clase.</span><span class="sxs-lookup"><span data-stu-id="01a16-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="01a16-135">Este es el aspecto que debería tener Program.cs.</span><span class="sxs-lookup"><span data-stu-id="01a16-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
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

6. <span data-ttu-id="01a16-136">Ejecutar programa hello y asegúrese de que no hay ningún error.</span><span class="sxs-lookup"><span data-stu-id="01a16-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="01a16-137">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="01a16-137">Congratulations!</span></span> <span data-ttu-id="01a16-138">Ahora ha enviado el concentrador de eventos de tooan de mensajes.</span><span class="sxs-lookup"><span data-stu-id="01a16-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01a16-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01a16-139">Next steps</span></span>
<span data-ttu-id="01a16-140">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="01a16-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="01a16-141">Recepción de eventos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="01a16-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="01a16-142">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="01a16-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="01a16-143">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="01a16-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="01a16-144">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="01a16-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
