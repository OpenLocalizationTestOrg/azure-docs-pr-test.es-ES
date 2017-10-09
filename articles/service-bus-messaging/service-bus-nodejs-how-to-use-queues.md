---
title: aaaHow toouse Bus de servicio pone en cola en Node.js | Documentos de Microsoft
description: "Obtenga información acerca de cómo pone en cola toouse Service Bus en Azure desde una aplicación Node.js."
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
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="bcfee-103">¿Cómo toouse Bus de servicio pone en cola con Node.js</span><span class="sxs-lookup"><span data-stu-id="bcfee-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="bcfee-104">Este artículo describe cómo toouse Bus de servicio pone en cola con Node.js.</span><span class="sxs-lookup"><span data-stu-id="bcfee-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="bcfee-105">ejemplos de Hola se escriben en JavaScript y usar hello módulo Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="bcfee-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="bcfee-106">Hello escenarios descritos se incluyen **crear colas**, **enviar y recibir mensajes**, y **eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="bcfee-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="bcfee-107">Para obtener más información sobre las colas, vea hello [pasos siguientes](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="bcfee-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="bcfee-108">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="bcfee-108">Create a Node.js application</span></span>
<span data-ttu-id="bcfee-109">Cree una aplicación Node.js vacía.</span><span class="sxs-lookup"><span data-stu-id="bcfee-109">Create a blank Node.js application.</span></span> <span data-ttu-id="bcfee-110">Para obtener instrucciones sobre cómo toocreate una aplicación Node.js, vea [crear e implementar un tooan de aplicación Node.js sitio Web de Azure][Create and deploy a Node.js application tooan Azure Website], o [servicio de nube de Node.js] [ Node.js Cloud Service] con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcfee-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="bcfee-111">Configurar el Bus de servicio de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="bcfee-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="bcfee-112">toouse Bus de servicio de Azure, descargar y usar hello paquete de Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="bcfee-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="bcfee-113">Este paquete incluye un conjunto de bibliotecas que se comunican con los servicios de REST de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcfee-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="bcfee-114">Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete</span><span class="sxs-lookup"><span data-stu-id="bcfee-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="bcfee-115">Hola de uso **Windows PowerShell para Node.js** comando ventana toonavigate toohello **c:\\nodo\\sbqueues\\WebRole1** carpeta que haya creado el aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="bcfee-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="bcfee-116">Tipo de **npm instalar azure** en la ventana de comandos de hello, que debería resultado salida similares toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="bcfee-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="bcfee-117">También puede ejecutar manualmente hello **ls** tooverify de comando que un **node_modules** se creó la carpeta.</span><span class="sxs-lookup"><span data-stu-id="bcfee-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="bcfee-118">Dentro de ese Hola de Buscar carpeta **azure** paquete, que contiene las bibliotecas de Hola que necesita tooaccess colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bcfee-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="bcfee-119">Módulo de Hola de importación</span><span class="sxs-lookup"><span data-stu-id="bcfee-119">Import hello module</span></span>
<span data-ttu-id="bcfee-120">Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="bcfee-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="bcfee-121">Configuración de una conexión del Bus de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="bcfee-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="bcfee-122">módulo de Azure Hello lee variable de entorno de hello `AZURE_SERVICEBUS_CONNECTION_STRING` necesita la información del tooobtain tooconnect tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="bcfee-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="bcfee-123">Si no se establece esta variable de entorno, debe especificar la información de la cuenta de hello al llamar a `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="bcfee-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="bcfee-124">Para obtener un ejemplo de establecer las variables de entorno de hello en un archivo de configuración para un servicio de nube de Azure, consulte [Node.js de servicio de nube con almacenamiento][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="bcfee-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="bcfee-125">Para obtener un ejemplo de establecer las variables de entorno de hello en hello [portal de Azure] [ Azure portal] para un sitio Web de Azure, consulte [aplicación Web de Node.js con almacenamiento] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="bcfee-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="bcfee-126">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="bcfee-126">Create a queue</span></span>
<span data-ttu-id="bcfee-127">Hola **ServiceBusService** objeto permite toowork con colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bcfee-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="bcfee-128">Hello código siguiente se crea un **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="bcfee-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="bcfee-129">Agregar cerca de parte superior de Hola de hello **server.js** archivo, después de hello tooimport de instrucción Hola módulo de Azure:</span><span class="sxs-lookup"><span data-stu-id="bcfee-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="bcfee-130">Mediante una llamada a `createQueueIfNotExists` en hello **ServiceBusService** objeto Hola especificado se devuelve cola (si existe), o se crea una nueva cola con el nombre especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcfee-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="bcfee-131">Hola siguiente de código usa `createQueueIfNotExists` toocreate o conectar con el nombre de cola de toohello `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="bcfee-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="bcfee-132">Hola `createServiceBusService` método es compatible también con opciones adicionales, que permiten la configuración de la cola de toooverride de forma predeterminada, como el tamaño de cola toolive o máximo de tiempo de mensaje.</span><span class="sxs-lookup"><span data-stu-id="bcfee-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="bcfee-133">Hello en el ejemplo siguiente se establece Hola cola máximo tamaño too5 GB y un valor de hora toolive (TTL) de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="bcfee-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="bcfee-134">Filtros</span><span class="sxs-lookup"><span data-stu-id="bcfee-134">Filters</span></span>
<span data-ttu-id="bcfee-135">Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="bcfee-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="bcfee-136">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:</span><span class="sxs-lookup"><span data-stu-id="bcfee-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="bcfee-137">Después de realizar su procesamiento previo en Opciones de solicitud de hello, debe llamar al método hello `next`, pasando una devolución de llamada con hello siguiente firma:</span><span class="sxs-lookup"><span data-stu-id="bcfee-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="bcfee-138">En esta devolución de llamada y después procesamiento hello `returnObject` (hello respuesta Hola solicitud toohello servidor), o bien debe invocar la devolución de llamada de hello `next` si existe toocontinue otros filtros de procesamiento, o simplemente invocar `finalCallback`, donde finaliza la invocación de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcfee-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="bcfee-139">Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, `ExponentialRetryPolicyFilter` y `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="bcfee-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="bcfee-140">Hello código siguiente se crea un `ServiceBusService` objeto que usa Hola `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="bcfee-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="bcfee-141">Cola de mensajes tooa de envío</span><span class="sxs-lookup"><span data-stu-id="bcfee-141">Send messages tooa queue</span></span>
<span data-ttu-id="bcfee-142">la aplicación llama a una cola de Service Bus de mensajes tooa toosend, hello `sendQueueMessage` método en hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="bcfee-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="bcfee-143">Los mensajes de las colas son demasiado (recibidos y enviados desde) Bus de servicio **BrokeredMessage** objetos y tener un conjunto de propiedades estándar (como **etiqueta** y **TimeToLive**), diccionario de propiedades personalizadas de específicos de la aplicación de toohold usado y un cuerpo de datos de aplicación arbitraria que.</span><span class="sxs-lookup"><span data-stu-id="bcfee-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="bcfee-144">Una aplicación puede establecer cuerpo Hola de mensaje de saludo pasando una cadena como mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="bcfee-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="bcfee-145">Las propiedades estándar requeridas se rellenan con valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="bcfee-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="bcfee-146">Hello en el ejemplo siguiente se muestra cómo toosend una cola de toohello de mensajes de prueba denominado `myqueue` con `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="bcfee-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="bcfee-147">Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="bcfee-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="bcfee-148">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="bcfee-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="bcfee-149">No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="bcfee-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="bcfee-150">El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="bcfee-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="bcfee-151">Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="bcfee-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="bcfee-152">mensajes de una cola</span><span class="sxs-lookup"><span data-stu-id="bcfee-152">Receive messages from a queue</span></span>
<span data-ttu-id="bcfee-153">Se reciben mensajes de una cola utilizando hello `receiveQueueMessage` método en hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="bcfee-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="bcfee-154">De forma predeterminada, los mensajes se eliminan de cola de hello cuando se leen; Sin embargo, puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la cola de Hola por establecer el parámetro opcional de hello `isPeekLock` demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="bcfee-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="bcfee-155">Hola comportamiento predeterminado de lectura y eliminación de mensajes de bienvenida tal como parte del programa Hola a la operación de recepción es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="bcfee-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="bcfee-156">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="bcfee-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="bcfee-157">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="bcfee-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="bcfee-158">Si hello `isPeekLock` parámetro está establecido demasiado**true**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="bcfee-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="bcfee-159">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="bcfee-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="bcfee-160">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a `deleteMessage` método y proporcionar toobe de mensaje de Hola eliminado como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="bcfee-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="bcfee-161">Hola `deleteMessage` método marca el mensaje Hola como consumido y lo quita de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcfee-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="bcfee-162">Hello en el ejemplo siguiente se muestra cómo tooreceive y procesar mensajes usando `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="bcfee-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="bcfee-163">Hello en el ejemplo se recibe por primera vez y elimina un mensaje y, a continuación, recibe un mensaje con `isPeekLock` establecido demasiado**true**, a continuación, elimina Hola mensaje utilizando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="bcfee-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="bcfee-164">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="bcfee-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="bcfee-165">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="bcfee-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="bcfee-166">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="bcfee-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="bcfee-167">Esto provocará toounlock de Bus de servicio en el mensaje en cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="bcfee-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="bcfee-168">También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si se produce un error de aplicación de hello tooprocess Hola mensaje antes de Hola tiempo de espera de bloqueo expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará automáticamente mensajes de bienvenida y hacerla disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="bcfee-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="bcfee-169">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="bcfee-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="bcfee-170">Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="bcfee-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="bcfee-171">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje.</span><span class="sxs-lookup"><span data-stu-id="bcfee-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="bcfee-172">A menudo esto se logra utilizando hello **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="bcfee-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcfee-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bcfee-173">Next steps</span></span>
<span data-ttu-id="bcfee-174">toolearn más información acerca de las colas, vea Hola recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="bcfee-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="bcfee-175">[Colas, temas y suscripciones][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="bcfee-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="bcfee-176">Repositorio de [Azure SDK para Node][Azure SDK for Node] en GitHub</span><span class="sxs-lookup"><span data-stu-id="bcfee-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="bcfee-177">Centro para desarrolladores de Node.js</span><span class="sxs-lookup"><span data-stu-id="bcfee-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
