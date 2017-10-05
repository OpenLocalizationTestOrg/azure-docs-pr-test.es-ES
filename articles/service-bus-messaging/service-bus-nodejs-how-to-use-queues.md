---
title: Uso de colas de Service Bus en Node.js | Microsoft Docs
description: "Obtenga información sobre cómo usar las colas del Bus de servicio en Azure desde una aplicación Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="2bee8-103">Uso de colas de Service Bus con Node.js</span><span class="sxs-lookup"><span data-stu-id="2bee8-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="2bee8-104">En este artículo se describe cómo usar las colas de Service Bus con Node.js.</span><span class="sxs-lookup"><span data-stu-id="2bee8-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="2bee8-105">Los ejemplos están escritos en JavaScript y usan el módulo Node.js de Azure.</span><span class="sxs-lookup"><span data-stu-id="2bee8-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="2bee8-106">Entre los escenarios proporcionados se incluyen los siguientes: **creación de colas**, **envío y recepción de mensajes** y **eliminación de colas**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="2bee8-107">Para obtener más información sobre las colas, consulte la sección [Pasos siguientes](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="2bee8-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="2bee8-108">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="2bee8-108">Create a Node.js application</span></span>
<span data-ttu-id="2bee8-109">Cree una aplicación Node.js vacía.</span><span class="sxs-lookup"><span data-stu-id="2bee8-109">Create a blank Node.js application.</span></span> <span data-ttu-id="2bee8-110">Para obtener instrucciones acerca de cómo crear una aplicación Node.js, consulte [Creación e implementación de una aplicación Node.js en un sitio web de Azure][Create and deploy a Node.js application to an Azure Website] o [Servicio en la nube Node.js][Node.js Cloud Service] (con Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="2bee8-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="2bee8-111">Configuración de la aplicación para usar el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="2bee8-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="2bee8-112">Para utilizar el Bus de servicio de Azure, descargue y use el paquete Azure para Node.js.</span><span class="sxs-lookup"><span data-stu-id="2bee8-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="2bee8-113">Este paquete incluye un conjunto de bibliotecas que se comunican con los servicios REST del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="2bee8-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="2bee8-114">Uso del Administrador de paquetes para Node (NPM) para obtener el paquete</span><span class="sxs-lookup"><span data-stu-id="2bee8-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="2bee8-115">Use la ventana de comandos de **Windows PowerShell for Node.js** para navegar a la carpeta **c:\\node\\sbqueues\\WebRole1** en la que ha creado la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2bee8-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="2bee8-116">Escriba **npm install azure** en la ventana de comandos, cuyo resultado debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2bee8-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. <span data-ttu-id="2bee8-117">Puede ejecutar manualmente el comando **ls** para comprobar si se ha creado una carpeta **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="2bee8-118">Dentro de esa carpeta, busque el paquete **azure**, que contiene las bibliotecas necesarias para obtener acceso a las colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2bee8-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="2bee8-119">Importación del módulo</span><span class="sxs-lookup"><span data-stu-id="2bee8-119">Import the module</span></span>
<span data-ttu-id="2bee8-120">Utilizando el Bloc de notas u otro editor de texto, agregue el código siguiente en la parte superior del archivo **server.js** de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="2bee8-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="2bee8-121">Configuración de una conexión del Bus de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="2bee8-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="2bee8-122">El módulo de Azure lee las variables de entorno `AZURE_SERVICEBUS_CONNECTION_STRING` para obtener la información necesaria para conectarse a Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2bee8-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="2bee8-123">Si no se configura esta variable de entorno, debe especificar la información de la cuenta al llamar a `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="2bee8-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="2bee8-124">Para ver un ejemplo de cómo configurar las variables de entorno en un archivo de configuración para un servicio en la nube de Azure, consulte [Servicio de nube de Node.js con Storage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="2bee8-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="2bee8-125">Para ver un ejemplo de configuración de las variables de entorno en [Azure Portal][Azure portal] para un sitio web de Azure, consulte [Aplicación web Node.js con Storage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="2bee8-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="2bee8-126">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="2bee8-126">Create a queue</span></span>
<span data-ttu-id="2bee8-127">El objeto **ServiceBusService** le permite trabajar con colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2bee8-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="2bee8-128">El siguiente código crea un objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="2bee8-129">Agréguelo cerca de la parte superior del archivo **server.js** , tras la instrucción para importar el módulo azure:</span><span class="sxs-lookup"><span data-stu-id="2bee8-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="2bee8-130">Al llamar a `createQueueIfNotExists` en el objeto **ServiceBusService**, se obtiene la cola especificada (si existe) o se crea una nueva con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="2bee8-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="2bee8-131">El código siguiente usa `createQueueIfNotExists` para crear una cola llamada `myqueue` o conectarse a ella:</span><span class="sxs-lookup"><span data-stu-id="2bee8-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="2bee8-132">El método `createServiceBusService` también admite opciones adicionales, que le permiten invalidar la configuración predeterminada de las colas, como el período de vida de los mensajes o el tamaño máximo de las colas.</span><span class="sxs-lookup"><span data-stu-id="2bee8-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="2bee8-133">En el siguiente ejemplo se establece el tamaño máximo de las colas en 5 GB y el valor del período de vida (TTL) en 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="2bee8-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="2bee8-134">Filtros</span><span class="sxs-lookup"><span data-stu-id="2bee8-134">Filters</span></span>
<span data-ttu-id="2bee8-135">Las operaciones de filtrado opcionales pueden aplicarse a las tareas realizadas utilizando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="2bee8-136">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con la firma:</span><span class="sxs-lookup"><span data-stu-id="2bee8-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="2bee8-137">Después de realizar el preprocesamiento en las opciones de solicitud, el método tiene que llamar a `next`, pasando una devolución de llamada con la firma siguiente:</span><span class="sxs-lookup"><span data-stu-id="2bee8-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="2bee8-138">En esta devolución de llamada y después de procesar `returnObject` (la respuesta de la solicitud al servidor), la devolución de llamada tiene que invocar a `next`, si existe, para continuar procesando otros filtros, o bien simplemente invocar a `finalCallback`, que finaliza la invocación del servicio.</span><span class="sxs-lookup"><span data-stu-id="2bee8-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="2bee8-139">Con el SDK de Azure, se incluyen dos filtros que implementan la lógica de reintento para Node.js, `ExponentialRetryPolicyFilter` y `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="2bee8-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="2bee8-140">El siguiente código crea un objeto `ServiceBusService` que usa `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="2bee8-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="2bee8-141">mensajes a una cola</span><span class="sxs-lookup"><span data-stu-id="2bee8-141">Send messages to a queue</span></span>
<span data-ttu-id="2bee8-142">Para enviar un mensaje a una cola de Service Bus, la aplicación debe llamar al método `sendQueueMessage` del objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="2bee8-143">Los mensajes enviados a las colas de Service Bus (y recibidos de ellas) son objetos **BrokeredMessage** y cuentan con un conjunto de propiedades estándar (como **Label** y **TimeToLive**), un diccionario que se usa para mantener las propiedades personalizadas específicas de la aplicación y un conjunto de datos arbitrarios de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2bee8-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="2bee8-144">Una aplicación puede establecer el cuerpo del mensaje pasando una cadena como el mensaje.</span><span class="sxs-lookup"><span data-stu-id="2bee8-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="2bee8-145">Las propiedades estándar requeridas se rellenan con valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="2bee8-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="2bee8-146">En el ejemplo siguiente se muestra cómo enviar un mensaje de prueba a la cola `myqueue` mediante `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="2bee8-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="2bee8-147">El tamaño máximo de mensaje que admiten las colas de Service Bus es de 256 KB en el [nivel Estándar](service-bus-premium-messaging.md) y de 1 MB en el [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="2bee8-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="2bee8-148">El encabezado, que incluye propiedades de la aplicación estándar y personalizadas, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="2bee8-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="2bee8-149">No hay límite para el número de mensajes que contiene una cola, pero hay un tope para el tamaño total de los mensajes contenidos en una cola.</span><span class="sxs-lookup"><span data-stu-id="2bee8-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="2bee8-150">El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="2bee8-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="2bee8-151">Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="2bee8-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="2bee8-152">mensajes de una cola</span><span class="sxs-lookup"><span data-stu-id="2bee8-152">Receive messages from a queue</span></span>
<span data-ttu-id="2bee8-153">Los mensajes se reciben de una cola utilizando el método `receiveQueueMessage` del objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="2bee8-154">De manera predeterminada, los mensajes se eliminan de la cola una vez que se leen; sin embargo, puede leer (echar un vistazo) y bloquear los mensajes sin eliminarlos de la cola estableciendo el parámetro opcional `isPeekLock` en **true**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="2bee8-155">El funcionamiento predeterminado por el que los mensajes se eliminan tras leerlos como parte del proceso de recepción es el modelo más sencillo y el que mejor funciona en aquellas situaciones en las que una aplicación puede tolerar que no se procese un mensaje en caso de error.</span><span class="sxs-lookup"><span data-stu-id="2bee8-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="2bee8-156">Para entenderlo mejor, pongamos una situación en la que un consumidor emite la solicitud de recepción que se bloquea antes de procesarla.</span><span class="sxs-lookup"><span data-stu-id="2bee8-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="2bee8-157">Como el Bus de servicio habrá marcado el mensaje como consumido, cuando la aplicación se reinicie y empiece a consumir mensajes de nuevo, habrá perdido el mensaje que se consumió antes del bloqueo.</span><span class="sxs-lookup"><span data-stu-id="2bee8-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="2bee8-158">Si el parámetro `isPeekLock` está establecido en **true**, el proceso de recepción se convierte en una operación en dos fases que permite admitir aplicaciones que no toleran la pérdida de mensajes.</span><span class="sxs-lookup"><span data-stu-id="2bee8-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="2bee8-159">Cuando el Bus de servicio recibe una solicitud, busca el siguiente mensaje que se va a consumir, lo bloquea para impedir que otros consumidores lo reciban y, a continuación, lo devuelve a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2bee8-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="2bee8-160">Una vez que la aplicación termina de procesar el mensaje (o lo almacena de forma fiable para su futuro procesamiento), completa la segunda fase del proceso de recepción llamando al método `deleteMessage` y facilitando el mensaje que se va a eliminar a modo de parámetro.</span><span class="sxs-lookup"><span data-stu-id="2bee8-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="2bee8-161">El método `deleteMessage` marca el mensaje como consumido y lo elimina de la cola.</span><span class="sxs-lookup"><span data-stu-id="2bee8-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="2bee8-162">En el ejemplo siguiente se muestra cómo recibir y procesar mensajes mediante `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="2bee8-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="2bee8-163">En primer lugar, el ejemplo recibe y elimina un mensaje, después recibe un mensaje con `isPeekLock` establecido en **true** y luego lo elimina mediante `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="2bee8-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="2bee8-164">Actuación ante errores de la aplicación y mensajes que no se pueden leer</span><span class="sxs-lookup"><span data-stu-id="2bee8-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="2bee8-165">El Bus de servicio proporciona una funcionalidad que le ayuda a superar sin problemas los errores de la aplicación o las dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="2bee8-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="2bee8-166">Si por cualquier motivo una aplicación de recepción es incapaz de procesar el mensaje, entonces puede llamar al método `unlockMessage` del objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="2bee8-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="2bee8-167">Esto hará que el Bus de servicio desbloquee el mensaje de la cola y esté disponible para que pueda volver a recibirse, ya sea por la misma aplicación que lo consume o por otra.</span><span class="sxs-lookup"><span data-stu-id="2bee8-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="2bee8-168">También hay un tiempo de espera asociado con un mensaje bloqueado en la cola y, si la aplicación no puede procesar el mensaje antes de que finalice el tiempo de espera del bloqueo (por ejemplo, si la aplicación sufre un error), entonces el bus de servicio desbloquea el mensaje automáticamente y hace que esté disponible para que pueda volver a recibirse.</span><span class="sxs-lookup"><span data-stu-id="2bee8-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="2bee8-169">En caso de que la aplicación sufra un error después de procesar el mensaje y antes de llamar al método `deleteMessage`, entonces el mensaje se volverá a entregar a la aplicación cuando esta se reinicie.</span><span class="sxs-lookup"><span data-stu-id="2bee8-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="2bee8-170">Habitualmente se denomina *Al menos un procesamiento*, es decir, cada mensaje se procesará al menos una vez; aunque en determinadas situaciones podría volver a entregarse el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="2bee8-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="2bee8-171">Si el escenario no puede tolerar el procesamiento duplicado, entonces los desarrolladores de la aplicación deberían agregar lógica adicional a su aplicación para solucionar la entrega de mensajes duplicados.</span><span class="sxs-lookup"><span data-stu-id="2bee8-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="2bee8-172">A menudo, esto se consigue usando la propiedad **MessageId** del mensaje, que permanecerá constante en todos los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="2bee8-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bee8-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2bee8-173">Next steps</span></span>
<span data-ttu-id="2bee8-174">Para más información sobre las colas, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="2bee8-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="2bee8-175">[Colas, temas y suscripciones][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="2bee8-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="2bee8-176">Repositorio de [Azure SDK para Node][Azure SDK for Node] en GitHub</span><span class="sxs-lookup"><span data-stu-id="2bee8-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="2bee8-177">Centro para desarrolladores de Node.js</span><span class="sxs-lookup"><span data-stu-id="2bee8-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
