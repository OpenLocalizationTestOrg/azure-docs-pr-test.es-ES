---
title: aaaGet a trabajar con colas de Bus de servicio de Azure | Documentos de Microsoft
description: "Escriba una aplicación de consola en C# que use las colas de mensajería de Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Introducción a las colas de Service Bus
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>Lo que se logrará
Este tutorial trata Hola pasos:

1. Crear un espacio de nombres de Bus de servicio, mediante Hola portal de Azure.
2. Crear una cola de Bus de servicio, utilizando Hola portal de Azure.
3. Escribir un mensaje de un toosend de aplicación de consola.
4. Escribir un hello tooreceive de aplicación de consola mensajes enviados en el paso anterior de Hola.

## <a name="prerequisites"></a>Requisitos previos
1. [Visual Studio 2015 o posterior](http://www.visualstudio.com). ejemplos de Hello en este tutorial utiliza Visual Studio de 2017.
2. Una suscripción de Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Crear un espacio de nombres mediante Hola portal de Azure
Si ya ha creado un espacio de nombres de mensajería de Bus de servicio, consulte el toohello [crear una cola mediante el portal de Azure de hello](#2-create-a-queue-using-the-azure-portal) sección.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Crear una cola con hello portal de Azure
Si ya ha creado una cola de Bus de servicio, consulte el toohello [toohello cola de mensajes de envío](#3-send-messages-to-the-queue) sección.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. Cola de mensajes toohello de envío
cola de toohello de toosend mensajes, se escribe una aplicación de consola de C# con Visual Studio.

### <a name="create-a-console-application"></a>Creación de una aplicación de consola

Inicie Visual Studio y cree un nuevo proyecto **Console app (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Agregar paquete de NuGet de Bus de servicio de Hola
1. Haga clic en proyecto de hello recién creado y seleccione **administrar paquetes de NuGet**.
2. Haga clic en hello **examinar** ficha, busque **Microsoft Azure Service Bus**y, a continuación, seleccione hello **WindowsAzure.ServiceBus** elemento. Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.
   
    ![Seleccionar un paquete NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Escribir algunas toosend de código en una cola de mensajes toohello
1. Agregue los siguiente hello `using` parte superior de toohello de instrucción del archivo Program.cs de Hola.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Agregar Hola después código toohello `Main` método. Conjunto hello `connectionString` cadena de conexión de la variable toohello que se obtuvo al crear el espacio de nombres de Hola y establecer `queueName` nombre de la cola de toohello que utilizó al crear la cola de Hola.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Así debería ser el archivo Program.cs.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Ejecutar programa hello y comprobar Hola portal de Azure: haga clic en nombre de saludo de la cola en el espacio de nombres de hello **Introducción** hoja. cola de Hello **Essentials** hoja se muestra. Tenga en cuenta que hello **Active mensaje Count** valor ahora debe ser 1. Cada vez que ejecute la aplicación del remitente Hola sin tener que recuperar mensajes de Hola, este valor aumenta en 1. También tenga en cuenta que el tamaño actual de Hola de cola de hello incrementa cada aplicación hello de tiempo agrega una cola de toohello de mensajes.
   
      ![Tamaño del mensaje][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Recibir mensajes de Hola cola

1. mensajes de saludo tooreceive acabamos de enviar, cree una nueva aplicación de consola y agregar un paquete de NuGet de Bus de servicio de referencia toohello, aplicación remitente similar de toohello anterior.
2. Agregue los siguiente hello `using` parte superior de toohello de instrucción del archivo Program.cs de Hola.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Agregar Hola después código toohello `Main` método. Conjunto hello `connectionString` toohello variable cadena de conexión que se obtuvo al crear el espacio de nombres de Hola y establezca `queueName` nombre de la cola de toohello que utilizó al crear la cola de Hola.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Este es el aspecto que debería tener el archivo Program.cs:
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Ejecutar programa hello y visite el portal de Hola de nuevo. Tenga en cuenta que hello **Active mensaje Count** y **actual** valores ahora son 0.
   
    ![Longitud de la cola][queue-message-receive]

¡Enhorabuena! Ha creado una cola, ha enviado un mensaje y ha recibido un mensaje.

## <a name="next-steps"></a>Pasos siguientes

Visite nuestro [repositorio de GitHub con ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que muestran algunas de las características de mensajería de Bus de servicio más avanzadas de Hola.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
