---
title: "Introducción a las colas de Azure Service Bus | Microsoft Docs"
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
ms.openlocfilehash: 99a377db6341d90d263b98e14227db61dd9beabd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="e8d8f-103">Introducción a las colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="e8d8f-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="e8d8f-104">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="e8d8f-104">What will be accomplished</span></span>
<span data-ttu-id="e8d8f-105">En este tutorial se describen los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e8d8f-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="e8d8f-106">Creación de un espacio de nombres de Service Bus mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e8d8f-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="e8d8f-107">Creación de una cola de Service Bus mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-107">Create a Service Bus queue, using the Azure portal.</span></span>
3. <span data-ttu-id="e8d8f-108">Escritura de una aplicación de consola para enviar un mensaje</span><span class="sxs-lookup"><span data-stu-id="e8d8f-108">Write a console application to send a message.</span></span>
4. <span data-ttu-id="e8d8f-109">Escritura de una aplicación de consola para recibir los mensajes enviados en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-109">Write a console application to receive the messages sent in the previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8d8f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e8d8f-110">Prerequisites</span></span>
1. <span data-ttu-id="e8d8f-111">[Visual Studio 2015 o posterior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e8d8f-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="e8d8f-112">En los ejemplos de este tutorial se usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-112">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="e8d8f-113">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="e8d8f-114">1. Creación de un espacio de nombres mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e8d8f-114">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="e8d8f-115">Si ya ha creado un espacio de nombres de mensajería de Service Bus, vaya a la sección [Creación de una cola mediante Azure Portal](#2-create-a-queue-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="e8d8f-115">If you've already created a Service Bus Messaging namespace, jump to the [Create a queue using the Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-the-azure-portal"></a><span data-ttu-id="e8d8f-116">2. Creación de una cola mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e8d8f-116">2. Create a queue using the Azure portal</span></span>
<span data-ttu-id="e8d8f-117">Si ya ha creado una cola de Service Bus, vaya a la sección [Envío de mensajes a la cola](#3-send-messages-to-the-queue).</span><span class="sxs-lookup"><span data-stu-id="e8d8f-117">If you have already created a Service Bus queue, jump to the [Send messages to the queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-to-the-queue"></a><span data-ttu-id="e8d8f-118">3. Envío de mensajes a la cola</span><span class="sxs-lookup"><span data-stu-id="e8d8f-118">3. Send messages to the queue</span></span>
<span data-ttu-id="e8d8f-119">Para enviar mensajes a la cola, se escribe una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-119">To send messages to the queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="e8d8f-120">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="e8d8f-120">Create a console application</span></span>

<span data-ttu-id="e8d8f-121">Inicie Visual Studio y cree un nuevo proyecto **Console app (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="e8d8f-122">Agregar el paquete NuGet de Service Bus</span><span class="sxs-lookup"><span data-stu-id="e8d8f-122">Add the Service Bus NuGet package</span></span>
1. <span data-ttu-id="e8d8f-123">Haga clic con el botón derecho en el proyecto recién creado y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-123">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="e8d8f-124">Haga clic en la pestaña **Examinar**, busque **Microsoft Azure Service Bus** y seleccione el elemento **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-124">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="e8d8f-125">Haga clic en **Instalar** para completar la instalación y, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-125">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Seleccionar un paquete NuGet][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-queue"></a><span data-ttu-id="e8d8f-127">Escritura de código para enviar un mensaje a la cola</span><span class="sxs-lookup"><span data-stu-id="e8d8f-127">Write some code to send a message to the queue</span></span>
1. <span data-ttu-id="e8d8f-128">Agregue la siguiente instrucción `using` al principio del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-128">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="e8d8f-129">Agregue el siguiente código al método `Main`.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-129">Add the following code to the `Main` method.</span></span> <span data-ttu-id="e8d8f-130">Establezca la variable `connectionString` en la cadena de conexión que obtuvo al crear el espacio de nombres y establezca `queueName` en el nombre de cola que usó cuando creó la cola.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-130">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `queueName` to the queue name that you used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="e8d8f-131">Así debería ser el archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-131">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="e8d8f-132">Ejecute el programa y compruebe Azure Portal: haga clic en el nombre de la cola en la hoja **Introducción** del espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-132">Run the program, and check the Azure portal: click the name of your queue in the namespace **Overview** blade.</span></span> <span data-ttu-id="e8d8f-133">Se muestra la hoja **Essentials** de la cola.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-133">The queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="e8d8f-134">Tenga en cuenta que el valor de **Recuento de mensajes activos** debe ser ahora 1.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-134">Notice that the **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="e8d8f-135">Cada vez que se ejecuta la aplicación de remitente sin recuperar los mensajes, este valor aumenta en 1.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-135">Each time you run the sender application without retrieving the messages, this value increases by 1.</span></span> <span data-ttu-id="e8d8f-136">Tenga también en cuenta que el tamaño actual de la cola aumenta cada vez que la aplicación agrega un mensaje a la misma.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-136">Also note that the current size of the queue increments each time the app adds a message to the queue.</span></span>
   
      ![Tamaño del mensaje][queue-message]

## <a name="4-receive-messages-from-the-queue"></a><span data-ttu-id="e8d8f-138">4. Recepción de mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="e8d8f-138">4. Receive messages from the queue</span></span>

1. <span data-ttu-id="e8d8f-139">Para recibir los mensajes que acaba de enviar, cree una nueva aplicación de consola y agregue una referencia al paquete NuGet de Service Bus, similar a la aplicación de remitente anterior.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-139">To receive the messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="e8d8f-140">Agregue la siguiente instrucción `using` al principio del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-140">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="e8d8f-141">Agregue el siguiente código al método `Main`.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-141">Add the following code to the `Main` method.</span></span> <span data-ttu-id="e8d8f-142">Establezca la variable `connectionString` en la cadena de conexión que se obtuvo al crear el espacio de nombres y establezca `queueName` en el nombre de cola que usó cuando creó la cola.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-142">Set the `connectionString` variable to the connection string that was obtained when creating the namespace, and set `queueName` to the queue name that you used when creating the queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="e8d8f-143">Este es el aspecto que debería tener el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="e8d8f-143">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="e8d8f-144">Ejecute el programa y vuelva a comprobar el portal.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-144">Run the program, and check the portal again.</span></span> <span data-ttu-id="e8d8f-145">Tenga en cuenta que los valores de **Recuento de mensajes activos** y **Actual** deben ser ahora 0.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-145">Notice that the **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Longitud de la cola][queue-message-receive]

<span data-ttu-id="e8d8f-147">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="e8d8f-147">Congratulations!</span></span> <span data-ttu-id="e8d8f-148">Ha creado una cola, ha enviado un mensaje y ha recibido un mensaje.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8d8f-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e8d8f-149">Next steps</span></span>

<span data-ttu-id="e8d8f-150">Consulte nuestro [repositorio de GitHub con ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples), donde se muestran algunas de las características más avanzadas de la mensajería de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e8d8f-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
