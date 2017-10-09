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
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>Empezar a enviar mensajes tooAzure centros de eventos de .NET estándar

> [!NOTE]
> Este ejemplo está disponible en [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

Este tutorial muestra cómo toowrite una aplicación de consola .NET Core que envía un conjunto de mensajes tooan concentrador de eventos. Puede ejecutar hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solución como-se, reemplazando hello `EhConnectionString` y `EhEntityPath` cadenas con sus valores de concentrador de eventos. O bien puede seguir Hola los pasos de este tutorial toocreate sus propios.

## <a name="prerequisites"></a>Requisitos previos

* [Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com). ejemplos de Hello en este tutorial, use Visual Studio de 2017, pero Visual Studio 2015 también es compatible.
* [Herramientas de .NET Core Visual Studio 2015 o 2017](http://www.microsoft.com/net/core).
* Una suscripción de Azure.
* Un espacio de nombres del centro de eventos.

Centro de eventos de toosend mensajes tooan, usaremos toowrite de Visual Studio una aplicación de consola de C#.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creación de un espacio de nombres de Event Hubs y un centro de eventos

Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres para el tipo de concentrador de eventos de hello y obtener las credenciales de administración que la aplicación necesita toocommunicate con el concentrador de eventos de Hola de Hola. toocreate un espacio de nombres y un concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md)y, a continuación, continúe con hello pasos.

## <a name="create-a-console-application"></a>Creación de una aplicación de consola

Inicie Visual Studio. De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**. Cree una aplicación de consola de .NET Core.

![Nuevo proyecto][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Agregar paquete de NuGet de concentradores de eventos de Hola

Agregar hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) proyecto del tooyour de paquete de NuGet de .NET estándar biblioteca siguiendo estos pasos: 

1. Haga clic en proyecto de hello recién creado y seleccione **administrar paquetes de NuGet**.
2. Haga clic en hello **examinar** ficha, realice una búsqueda de "Microsoft.Azure.EventHubs" y seleccione hello **Microsoft.Azure.EventHubs** paquete. Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Escribir algunas concentrador de eventos de código toosend mensajes toohello

1. Agregue los siguiente hello `using` parte superior de toohello de las instrucciones del archivo Program.cs de Hola.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Agregar constantes toohello `Program` clase para hello centros de eventos conexión entidad y la cadena de ruta de acceso (nombre de concentrador de eventos individuales). Reemplace los marcadores de posición de hello corchetes con los valores adecuados de Hola que se obtuvieron al crear el concentrador de eventos de Hola.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Agregar un nuevo método denominado `MainAsync` toohello `Program` de la clase, como se indica a continuación:

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

4. Agregar un nuevo método denominado `SendMessagesToEventHub` toohello `Program` de la clase, como se indica a continuación:

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

5. Agregar Hola después código toohello `Main` método Hola `Program` clase.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Este es el aspecto que debería tener Program.cs.

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

6. Ejecutar programa hello y asegúrese de que no hay ningún error.

¡Enhorabuena! Ahora ha enviado el concentrador de eventos de tooan de mensajes.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Recepción de eventos de Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
