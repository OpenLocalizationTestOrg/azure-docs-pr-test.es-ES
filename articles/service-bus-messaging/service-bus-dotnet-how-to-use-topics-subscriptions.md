---
title: aaaGet a trabajar con temas de Service Bus de Azure y las suscripciones | Documentos de Microsoft
description: "Escriba una aplicación de consola en C# que use los temas y las suscripciones de mensajería de Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Introducción a las colas de Service Bus

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>Lo que se logrará

Este tutorial trata Hola pasos:

1. Crear un espacio de nombres de Bus de servicio, mediante Hola portal de Azure.
2. Crear un tema de Bus de servicio, mediante Hola portal de Azure.
3. Crear un tema de toothat de la suscripción de Bus de servicio, mediante Hola portal de Azure.
4. Escribir una toosend de aplicación de consola en un tema de toohello de mensaje.
5. Escribir una tooreceive de aplicación de consola que el mensaje de suscripción de Hola.

## <a name="prerequisites"></a>Requisitos previos

1. [Visual Studio 2015 o posterior](http://www.visualstudio.com). ejemplos de Hello en este tutorial utiliza Visual Studio de 2017.
2. Una suscripción de Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Crear un espacio de nombres mediante Hola portal de Azure

Si ya ha creado un espacio de nombres de mensajería de Bus de servicio, consulte el toohello [crear un tema mediante el portal de Azure hello](#2-create-a-topic-using-the-azure-portal) sección.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Crear un tema mediante Hola portal de Azure

1. Inicie sesión en toohello [portal de Azure][azure-portal].
2. En el panel de navegación izquierdo de hello del portal de hello, haga clic en **Service Bus** (si no ve **Service Bus**, haga clic en **más servicios**).
3. Haga clic en el espacio de nombres de hello en el que le gustaría tema de hello toocreate. aparece la hoja de información general del espacio de nombres de Hello:
   
    ![de un tema][createtopic1]
4. Hola **espacio de nombres de Bus de servicio** hoja, haga clic en **temas**, a continuación, haga clic en **Agregar tema**.
   
    ![Seleccionar temas][createtopic2]
5. Escriba un nombre para el tema de Hola y desactive la opción hello **habilitar las particiones** opción. Deje Hola otras opciones con sus valores predeterminados.
   
    ![Seleccionar Nuevo][createtopic3]
6. En la parte inferior de Hola de hoja de hello, haga clic en **crear**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Crear un tema de toohello de suscripción

1. En panel de recursos del portal de hello, haga clic en el espacio de nombres de Hola que creó en el paso 1 y luego haga clic en el nombre del tema de Hola que creó en el paso 2.
2. Un principio Hola del panel de información general de hello, haga clic en hello además de iniciar sesión a continuación demasiado**suscripción** tooadd un tema de toothis de suscripción.

    ![Creación de una suscripción][createtopic4]

3. Escriba un nombre para la suscripción de Hola. Deje Hola otras opciones con sus valores predeterminados.

## <a name="4-send-messages-toohello-topic"></a>4. Enviar tema toohello de mensajes

tema de toohello de toosend mensajes, se escribe una aplicación de consola de C# con Visual Studio.

### <a name="create-a-console-application"></a>Creación de una aplicación de consola

Inicie Visual Studio y cree un nuevo proyecto **Console app (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Agregar paquete de NuGet de Bus de servicio de Hola

1. Haga clic en proyecto de hello recién creado y seleccione **administrar paquetes de NuGet**.
2. Haga clic en hello **examinar** ficha, busque **Microsoft Azure Service Bus**y, a continuación, seleccione hello **WindowsAzure.ServiceBus** elemento. Haga clic en **instalar** toocomplete Hola instalación, a continuación, cierre este cuadro de diálogo.
   
    ![Seleccionar un paquete NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Escriba algún código toosend un tema de toohello de mensaje

1. Agregue los siguiente hello `using` parte superior de toohello de instrucción del archivo Program.cs de Hola.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Agregar Hola después código toohello `Main` método. Conjunto hello `connectionString` cadena de conexión de la variable toohello que se obtuvo al crear el espacio de nombres de Hola y establecer `topicName` toohello nombre que usó al crear tema Hola.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Ejecutar programa hello y comprobar Hola portal de Azure: haga clic en nombre de hello del tema en el espacio de nombres de hello **Introducción** hoja. tema de Hello **Essentials** hoja se muestra. En suscripciones de hello cerca de la parte inferior de Hola de hoja de hello, tenga en cuenta que hello **número de mensajes** valor para cada suscripción ahora debe ser 1. Cada vez que se ejecute la aplicación del remitente Hola sin tener que recuperar mensajes de saludo (como se describe en la sección siguiente de hello), este valor se incrementa en 1. Tenga en cuenta también ese tamaño actual de Hola de Hola Hola de incrementos de tema **actual** valor en hello **Essentials** hoja cada vez aplicación hello agrega una mensaje toohello/suscripción al tema.
   
      ![Tamaño del mensaje][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Recibir mensajes de Hola suscripción

1. Hola tooreceive o mensajes que acabamos de enviar, cree una nueva aplicación de consola y agregue un paquete de NuGet de Bus de servicio de referencia toohello, aplicación remitente similar de toohello anterior.
2. Agregue los siguiente hello `using` parte superior de toohello de instrucción del archivo Program.cs de Hola.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Agregar Hola después código toohello `Main` método. Conjunto hello `connectionString` toohello variable conexión cadena que se obtuvo al crear el espacio de nombres de Hola y establecer `topicName` nombre toohello que usó al crear tema Hola.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. Ejecutar programa hello y visite el portal de Hola de nuevo. Tenga en cuenta que hello **número de mensajes** y **actual** valores ahora son 0.
   
    ![Longitud del tema][topic-message-receive]

¡Enhorabuena! Ya ha creado un tema y una suscripción, ha enviado un mensaje y ha recibido dicho mensaje.

## <a name="next-steps"></a>Pasos siguientes

Visite nuestro [repositorio de GitHub con ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que muestran algunas de las características de mensajería de Bus de servicio más avanzadas de Hola.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
