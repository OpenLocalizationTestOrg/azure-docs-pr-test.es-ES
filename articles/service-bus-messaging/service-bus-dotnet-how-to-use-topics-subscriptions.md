---
title: "Introducción a los temas y las suscripciones de Azure Service Bus | Microsoft Docs"
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
ms.openlocfilehash: 9401ada519f600b0d2817f06a396e16607a24129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="607b2-103">Introducción a las colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="607b2-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="607b2-104">Lo que se logrará</span><span class="sxs-lookup"><span data-stu-id="607b2-104">What will be accomplished</span></span>

<span data-ttu-id="607b2-105">En este tutorial se describen los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="607b2-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="607b2-106">Creación de un espacio de nombres de Service Bus mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="607b2-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="607b2-107">Creación de un tema de Service Bus mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="607b2-107">Create a Service Bus topic, using the Azure portal.</span></span>
3. <span data-ttu-id="607b2-108">Creación de una suscripción de Service Bus a dicho tema mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="607b2-108">Create a Service Bus subscription to that topic, using the Azure portal.</span></span>
4. <span data-ttu-id="607b2-109">Escritura de una aplicación de consola para enviar un mensaje al tema.</span><span class="sxs-lookup"><span data-stu-id="607b2-109">Write a console application to send a message to the topic.</span></span>
5. <span data-ttu-id="607b2-110">Escritura de una aplicación de consola para recibir dicho mensaje de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="607b2-110">Write a console application to receive that message from the subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="607b2-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="607b2-111">Prerequisites</span></span>

1. <span data-ttu-id="607b2-112">[Visual Studio 2015 o posterior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="607b2-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="607b2-113">En los ejemplos de este tutorial se usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="607b2-113">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="607b2-114">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="607b2-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="607b2-115">1. Creación de un espacio de nombres mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="607b2-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="607b2-116">Si ya ha creado un espacio de nombres de mensajería de Service Bus, vaya a la sección [Creación de un tema mediante Azure Portal](#2-create-a-topic-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="607b2-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a topic using the Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-the-azure-portal"></a><span data-ttu-id="607b2-117">2. Creación de un tema mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="607b2-117">2. Create a topic using the Azure portal</span></span>

1. <span data-ttu-id="607b2-118">Inicie sesión en [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="607b2-118">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="607b2-119">En el panel de navegación izquierdo del portal, haga clic en **Service Bus** (si no ve **Service Bus**, haga clic en **Más servicios**).</span><span class="sxs-lookup"><span data-stu-id="607b2-119">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="607b2-120">Haga clic en el espacio de nombres en el que desea crear el tema.</span><span class="sxs-lookup"><span data-stu-id="607b2-120">Click the namespace in which you would like to create the topic.</span></span> <span data-ttu-id="607b2-121">Aparece la hoja de información general del espacio de nombres:</span><span class="sxs-lookup"><span data-stu-id="607b2-121">The namespace overview blade appears:</span></span>
   
    ![Creación de un tema][createtopic1]
4. <span data-ttu-id="607b2-123">En la hoja **Espacio de nombres de Service Bus**, haga clic en **Temas** y, después, en **Agregar tema**.</span><span class="sxs-lookup"><span data-stu-id="607b2-123">In the **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Seleccionar temas][createtopic2]
5. <span data-ttu-id="607b2-125">Escriba el nombre del tema y desactive la opción **Habilitar particiones**.</span><span class="sxs-lookup"><span data-stu-id="607b2-125">Enter a name for the topic, and uncheck the **Enable partitioning** option.</span></span> <span data-ttu-id="607b2-126">Deje las restantes opciones con sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="607b2-126">Leave the other options with their default values.</span></span>
   
    ![Seleccionar Nuevo][createtopic3]
6. <span data-ttu-id="607b2-128">Haga clic en **Crear**en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="607b2-128">At the bottom of the blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-to-the-topic"></a><span data-ttu-id="607b2-129">3. Creación de una suscripción al tema</span><span class="sxs-lookup"><span data-stu-id="607b2-129">3. Create a subscription to the topic</span></span>

1. <span data-ttu-id="607b2-130">En el panel recursos del portal, haga clic en el espacio de nombres que creó en el paso 1 y, después, en el nombre del tema que creó en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="607b2-130">In the portal resources pane, click the namespace you created in step 1, then click name of the topic you created in step 2.</span></span>
2. <span data-ttu-id="607b2-131">A la parte superior del panel de información general, haga clic en el signo más junto a **Suscripción** para agregar una suscripción a este tema.</span><span class="sxs-lookup"><span data-stu-id="607b2-131">A the top of the overview pane, click the plus sign next to **Subscription** to add a subscription to this topic.</span></span>

    ![Creación de una suscripción][createtopic4]

3. <span data-ttu-id="607b2-133">Escriba el nombre de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="607b2-133">Enter a name for the subscription.</span></span> <span data-ttu-id="607b2-134">Deje las restantes opciones con sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="607b2-134">Leave the other options with their default values.</span></span>

## <a name="4-send-messages-to-the-topic"></a><span data-ttu-id="607b2-135">4. Envío de mensajes al tema</span><span class="sxs-lookup"><span data-stu-id="607b2-135">4. Send messages to the topic</span></span>

<span data-ttu-id="607b2-136">Para enviar mensajes al tema, se escribe una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="607b2-136">To send messages to the topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="607b2-137">Creación de una aplicación de consola</span><span class="sxs-lookup"><span data-stu-id="607b2-137">Create a console application</span></span>

<span data-ttu-id="607b2-138">Inicie Visual Studio y cree un nuevo proyecto **Console app (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="607b2-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="607b2-139">Agregar el paquete NuGet de Service Bus</span><span class="sxs-lookup"><span data-stu-id="607b2-139">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="607b2-140">Haga clic con el botón derecho en el proyecto recién creado y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="607b2-140">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="607b2-141">Haga clic en la pestaña **Examinar**, busque **Microsoft Azure Service Bus** y seleccione el elemento **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="607b2-141">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="607b2-142">Haga clic en **Instalar** para completar la instalación y, a continuación, cierre este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="607b2-142">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Seleccionar un paquete NuGet][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-topic"></a><span data-ttu-id="607b2-144">Escritura de código para enviar un mensaje al tema</span><span class="sxs-lookup"><span data-stu-id="607b2-144">Write some code to send a message to the topic</span></span>

1. <span data-ttu-id="607b2-145">Agregue la siguiente instrucción `using` al principio del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="607b2-145">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="607b2-146">Agregue el siguiente código al método `Main`.</span><span class="sxs-lookup"><span data-stu-id="607b2-146">Add the following code to the `Main` method.</span></span> <span data-ttu-id="607b2-147">Establezca la variable `connectionString` en la cadena de conexión que obtuvo al crear el espacio de nombres y establezca `topicName` en el nombre que usó cuando creó el tema.</span><span class="sxs-lookup"><span data-stu-id="607b2-147">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="607b2-148">Así debería ser el archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="607b2-148">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="607b2-149">Ejecute el programa y compruebe Azure Portal: haga clic en el nombre del tema en la hoja **Introducción** del espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="607b2-149">Run the program, and check the Azure portal: click the name of your topic in the namespace **Overview** blade.</span></span> <span data-ttu-id="607b2-150">Se muestra la hoja **Essentials** del tema.</span><span class="sxs-lookup"><span data-stu-id="607b2-150">The topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="607b2-151">En las suscripciones que se enumeran cerca de la parte inferior de la hoja, observe que el valor **Número de mensajes** de cada suscripción ahora debe ser 1.</span><span class="sxs-lookup"><span data-stu-id="607b2-151">In the subscription(s) listed near the bottom of the blade, notice that the **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="607b2-152">Cada vez que se ejecuta la aplicación de remitente sin recuperar los mensajes (como se describe en la siguiente sección), este valor aumenta en 1.</span><span class="sxs-lookup"><span data-stu-id="607b2-152">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 1.</span></span> <span data-ttu-id="607b2-153">Tenga en cuenta también que el tamaño actual del tema aumenta el valor de **Actual** en la hoja **Essentials** cada vez que la aplicación agrega un mensaje al tema o a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="607b2-153">Also note that the current size of the topic increments the **Current** value on the **Essentials** blade each time the app adds a message to the topic/subscription.</span></span>
   
      ![Tamaño del mensaje][topic-message]

## <a name="5-receive-messages-from-the-subscription"></a><span data-ttu-id="607b2-155">5. Recepción de mensajes de la suscripción</span><span class="sxs-lookup"><span data-stu-id="607b2-155">5. Receive messages from the subscription</span></span>

1. <span data-ttu-id="607b2-156">Para recibir el mensaje, o los mensajes, que acaba de enviar, cree una nueva aplicación de consola y agregue una referencia al paquete NuGet de Service Bus, de forma similar a la aplicación de remitente anterior.</span><span class="sxs-lookup"><span data-stu-id="607b2-156">To receive the message or messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="607b2-157">Agregue la siguiente instrucción `using` al principio del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="607b2-157">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="607b2-158">Agregue el siguiente código al método `Main`.</span><span class="sxs-lookup"><span data-stu-id="607b2-158">Add the following code to the `Main` method.</span></span> <span data-ttu-id="607b2-159">Establezca la variable `connectionString` en la cadena de conexión que obtuvo al crear el espacio de nombres y establezca `topicName` en el nombre que usó cuando creó el tema.</span><span class="sxs-lookup"><span data-stu-id="607b2-159">Set the `connectionString` variable to the connection string you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="607b2-160">Este es el aspecto que debería tener el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="607b2-160">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="607b2-161">Ejecute el programa y vuelva a comprobar el portal.</span><span class="sxs-lookup"><span data-stu-id="607b2-161">Run the program, and check the portal again.</span></span> <span data-ttu-id="607b2-162">Tenga en cuenta que los valores de **Recuento de mensajes** y **Actual** deben ser ahora 0.</span><span class="sxs-lookup"><span data-stu-id="607b2-162">Notice that the **Message Count** and **Current** values are now 0.</span></span>
   
    ![Longitud del tema][topic-message-receive]

<span data-ttu-id="607b2-164">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="607b2-164">Congratulations!</span></span> <span data-ttu-id="607b2-165">Ya ha creado un tema y una suscripción, ha enviado un mensaje y ha recibido dicho mensaje.</span><span class="sxs-lookup"><span data-stu-id="607b2-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="607b2-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="607b2-166">Next steps</span></span>

<span data-ttu-id="607b2-167">Consulte nuestro [repositorio de GitHub con ejemplos](https://github.com/Azure/azure-service-bus/tree/master/samples), donde se muestran algunas de las características más avanzadas de la mensajería de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="607b2-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

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
