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
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Empezar a recibir mensajes con hello Host procesador de eventos de .NET estándar

> [!NOTE]
> Este ejemplo está disponible en [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

Este tutorial muestra cómo el aplicación que recibe mensajes de un concentrador de eventos mediante el uso de la consola de toowrite un núcleo de .NET **EventProcessorHost**. Puede ejecutar hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solución como-se, reemplazar cadenas de hello con sus valores de cuenta de concentrador y el almacenamiento de eventos. O bien puede seguir Hola los pasos de este tutorial toocreate sus propios.

## <a name="prerequisites"></a>Requisitos previos

* [Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com). ejemplos de Hello en este tutorial, use Visual Studio de 2017, pero Visual Studio 2015 también es compatible.
* [Herramientas de .NET Core Visual Studio 2015 o 2017](http://www.microsoft.com/net/core).
* Una suscripción de Azure.
* Un espacio de nombres de Azure Event Hubs.
* Una cuenta de almacenamiento de Azure.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creación de un espacio de nombres de Event Hubs y un centro de eventos  

Hola primer paso es hello toouse [portal de Azure](https://portal.azure.com) toocreate un espacio de nombres para los concentradores de eventos de hello escriba y obtener las credenciales de administración que la aplicación necesita toocommunicate con el concentrador de eventos de Hola de Hola. toocreate un espacio de nombres y el concentrador de eventos, siga el procedimiento de hello en [este artículo](event-hubs-create.md)y, a continuación, continúe con hello pasos.  

## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de Azure Storage  

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).  
2. En el panel de navegación izquierdo de hello del portal de hello, haga clic en **New**, haga clic en **almacenamiento**y, a continuación, haga clic en **cuenta de almacenamiento**.  
3. Complete los campos de hello en la hoja de cuenta de almacenamiento de hello y, a continuación, haga clic en **crear**.

    ![Crear cuenta de almacenamiento][1]

4. Después de ver hello **se ha realizado correctamente en implementaciones** de mensajes, haga clic en nombre de Hola de hello nueva cuenta de almacenamiento. Hola **Essentials** hoja, haga clic en **Blobs**. Cuando Hola **servicio Blob** hoja se abre, haga clic en **+ contenedor** en la parte superior de Hola. Asigne un nombre de contenedor de hello y, a continuación, cierre hello **servicio Blob** hoja.  
5. Haga clic en **las claves de acceso** en hello izquierdo hoja y copia Hola el nombre del contenedor de almacenamiento de hello, la cuenta de almacenamiento de Hola y el valor de Hola de **key1**. Guardar estos valores tooNotepad o alguna otra ubicación temporal.  

## <a name="create-a-console-application"></a>Creación de una aplicación de consola

Inicie Visual Studio. De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**. Cree una aplicación de consola de .NET Core.

![Nuevo proyecto][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Agregar paquete de NuGet de concentradores de eventos de Hola

Agregar hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) y [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) proyecto del tooyour de paquetes de NuGet de .NET estándar biblioteca siguiendo estos pasos: 

1. Haga clic en proyecto de hello recién creado y seleccione **administrar paquetes de NuGet**.
2. Haga clic en hello **examinar** ficha, realice una búsqueda de "Microsoft.Azure.EventHubs" y seleccione hello **Microsoft.Azure.EventHubs** paquete. Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.
3. Repita los pasos 1 y 2 e instalar hello **Microsoft.Azure.EventHubs.Processor** paquete.

## <a name="implement-hello-ieventprocessor-interface"></a>Implementar una interfaz IEventProcessor Hola

1. En el Explorador de soluciones, proyectos de Hola de menú contextual, haga clic en **agregar**y, a continuación, haga clic en **clase**. Hola nueva clase el nombre **SimpleEventProcessor**.

2. Abra el archivo de SimpleEventProcessor.cs hello y agregue Hola siguiente `using` parte superior de toohello de las instrucciones del archivo hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Hola implemente `IEventProcessor` interfaz. Reemplace todo contenido de Hola de hello `SimpleEventProcessor` clase con el siguiente código de hello:

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Escribir un método de la consola principal que utiliza los mensajes de Hola SimpleEventProcessor clase tooreceive

1. Agregue los siguiente hello `using` parte superior de toohello de las instrucciones del archivo Program.cs de Hola.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Agregar constantes toohello `Program` clase para la cadena de conexión de concentrador de eventos de Hola, nombre del concentrador de eventos, el nombre de contenedor de cuenta de almacenamiento, nombre de la cuenta de almacenamiento y clave de la cuenta de almacenamiento. Agregar Hola siguiente código, reemplazando los marcadores de posición de hello con sus valores correspondientes.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Agregar un nuevo método denominado `MainAsync` toohello `Program` de la clase, como se indica a continuación:

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

3. Agregar Hola después de la línea de código toohello `Main` método:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Este es el aspecto que debería tener el archivo Program.cs:

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

4. Ejecutar programa hello y asegúrese de que no hay ningún error.

¡Enhorabuena! Ahora ha recibido mensajes de un concentrador de eventos mediante el uso de hello Host procesador de eventos.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
