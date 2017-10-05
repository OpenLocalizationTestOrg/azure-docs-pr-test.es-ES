---
title: Uso de colas de Service Bus con PHP | Microsoft Docs
description: "Obtenga información acerca de cómo usar las colas del Bus de servicio en Azure. Ejemplos de código escritos en PHP."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="b7624-104">Uso de colas de Service Bus con PHP</span><span class="sxs-lookup"><span data-stu-id="b7624-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="b7624-105">En esta guía se muestra cómo usar las colas del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b7624-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="b7624-106">Los ejemplos están escritos en PHP y utilizan el [SDK de Azure para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="b7624-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="b7624-107">Entre los escenarios proporcionados se incluyen los siguientes: **creación de colas**, **envío y recepción de mensajes** y **eliminación de colas**.</span><span class="sxs-lookup"><span data-stu-id="b7624-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="b7624-108">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="b7624-108">Create a PHP application</span></span>
<span data-ttu-id="b7624-109">El único requisito a la hora de crear una aplicación PHP para obtener acceso al servicio BLOB de Azure es que el código haga referencia a clases de [Azure SDK para PHP](../php-download-sdk.md) dentro del código.</span><span class="sxs-lookup"><span data-stu-id="b7624-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="b7624-110">Puede utilizar cualquier herramienta de desarrollo para crear la aplicación, o bien el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="b7624-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="b7624-111">La instalación de PHP debe tener también la [extensión OpenSSL](http://php.net/openssl) instalada y habilitada.</span><span class="sxs-lookup"><span data-stu-id="b7624-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="b7624-112">En esta guía, utilizará funciones del servicio a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7624-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="b7624-113">Obtención de las bibliotecas de clientes de Azure</span><span class="sxs-lookup"><span data-stu-id="b7624-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="b7624-114">Configuración de la aplicación para usar el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b7624-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="b7624-115">Para usar las API de la cola del Bus de servicio de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b7624-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="b7624-116">Haga referencia al archivo autocargador mediante la instrucción [require_once][require_once].</span><span class="sxs-lookup"><span data-stu-id="b7624-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="b7624-117">Hacer referencia a todas las clases que utilice.</span><span class="sxs-lookup"><span data-stu-id="b7624-117">Reference any classes you might use.</span></span>

<span data-ttu-id="b7624-118">En el siguiente ejemplo se muestra cómo incluir el archivo autocargador y hacer referencia a la clase `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="b7624-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="b7624-119">En este ejemplo (así como en otros ejemplos de este artículo), se asume que ha instalado las bibliotecas de clientes PHP para Azure mediante el compositor.</span><span class="sxs-lookup"><span data-stu-id="b7624-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="b7624-120">Si las instaló las bibliotecas manualmente o como un paquete PEAR, debe hacer referencia al archivo autocargador **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="b7624-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="b7624-121">En los ejemplos que aparecen a continuación, la instrucción `require_once` aparecerá siempre, pero solo se hará referencia a las clases necesarias para la ejecución del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b7624-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="b7624-122">Configuración de una conexión del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b7624-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="b7624-123">Para crear una instancia de un cliente del Bus de servicio, primero debe disponer de una cadena de conexión válida con el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="b7624-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="b7624-124">Donde `Endpoint` tiene generalmente el formato `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="b7624-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="b7624-125">Para crear cualquier cliente de servicio de Azure, debe usar la clase `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="b7624-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="b7624-126">Puede:</span><span class="sxs-lookup"><span data-stu-id="b7624-126">You can:</span></span>

* <span data-ttu-id="b7624-127">pasarle directamente la cadena de conexión, o bien</span><span class="sxs-lookup"><span data-stu-id="b7624-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="b7624-128">usar **CloudConfigurationManager (CCM)** para buscar la cadena de conexión en varios orígenes externos:</span><span class="sxs-lookup"><span data-stu-id="b7624-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="b7624-129">De manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="b7624-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="b7624-130">Puede agregar nuevos orígenes extendiendo la clase `ConnectionStringSource`.</span><span class="sxs-lookup"><span data-stu-id="b7624-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="b7624-131">En los ejemplos descritos aquí, la cadena de conexión se pasa directamente.</span><span class="sxs-lookup"><span data-stu-id="b7624-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="b7624-132">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="b7624-132">Create a queue</span></span>
<span data-ttu-id="b7624-133">Puede realizar operaciones de administración para colas de Service Bus mediante la clase `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="b7624-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="b7624-134">Un objeto `ServiceBusRestProxy` se construye mediante el método de generador `ServicesBuilder::createServiceBusService` con una cadena de conexión adecuada que encapsula los permisos de token para administrarlo.</span><span class="sxs-lookup"><span data-stu-id="b7624-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="b7624-135">En el ejemplo siguiente se muestra cómo crear una instancia de un objeto `ServiceBusRestProxy` y llamar a `ServiceBusRestProxy->createQueue` para crear una cola denominada `myqueue` dentro de un espacio de nombres de servicios `MySBNamespace`:</span><span class="sxs-lookup"><span data-stu-id="b7624-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="b7624-136">Puede usar el método `listQueues` en los objetos `ServiceBusRestProxy` para comprobar si ya existe una cola con un nombre especificado en un espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b7624-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="b7624-137">mensajes a una cola</span><span class="sxs-lookup"><span data-stu-id="b7624-137">Send messages to a queue</span></span>
<span data-ttu-id="b7624-138">Para enviar un mensaje a una cola de Service Bus, su aplicación llama al método `ServiceBusRestProxy->sendQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="b7624-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="b7624-139">El código siguiente muestra cómo enviar un mensaje a la cola `myqueue` que hemos creado anteriormente en el espacio de nombres de servicio `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="b7624-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="b7624-140">Los mensajes enviados a las colas de Service Bus y recibidos en ellas son instancias de la clase [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="b7624-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="b7624-141">Los objetos [BrokeredMessage][BrokeredMessage] tienen un conjunto de métodos y propiedades estándar que se usan para retener las propiedades personalizadas específicas de la aplicación y un conjunto de datos arbitrarios de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7624-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="b7624-142">El tamaño máximo de mensaje que admiten las colas de Service Bus es de 256 KB en el [nivel Estándar](service-bus-premium-messaging.md) y de 1 MB en el [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="b7624-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="b7624-143">El encabezado, que incluye propiedades de la aplicación estándar y personalizadas, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="b7624-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="b7624-144">No hay límite para el número de mensajes que contiene una cola, pero hay un tope para el tamaño total de los mensajes contenidos en una cola.</span><span class="sxs-lookup"><span data-stu-id="b7624-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="b7624-145">Este límite superior para el tamaño de la cola es de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="b7624-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="b7624-146">mensajes de una cola</span><span class="sxs-lookup"><span data-stu-id="b7624-146">Receive messages from a queue</span></span>

<span data-ttu-id="b7624-147">La mejor forma de recibir mensajes desde una cola es usar un método `ServiceBusRestProxy->receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="b7624-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="b7624-148">Los mensajes se pueden recibir de dos modos diferentes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) y [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="b7624-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="b7624-149">**PeekLock** es el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="b7624-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="b7624-150">Al usar el modo [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete), la operación de recepción consta de una sola fase; es decir, cuando el bus de servicio recibe una solicitud de lectura para un mensaje de la cola, marca el mensaje como consumido y lo devuelve a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7624-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="b7624-151">El modo [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) es el modelo más sencillo y funciona mejor para los escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de error.</span><span class="sxs-lookup"><span data-stu-id="b7624-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="b7624-152">Para entenderlo mejor, pongamos una situación en la que un consumidor emite la solicitud de recepción que se bloquea antes de procesarla.</span><span class="sxs-lookup"><span data-stu-id="b7624-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="b7624-153">Como el Bus de servicio habrá marcado el mensaje como consumido, cuando la aplicación se reinicie y empiece a consumir mensajes de nuevo, habrá perdido el mensaje que se consumió antes del bloqueo.</span><span class="sxs-lookup"><span data-stu-id="b7624-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="b7624-154">En el modo [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock), la recepción de un mensaje se convierte en una operación de dos etapas, lo que hace posible admitir aplicaciones que no pueden tolerar la pérdida de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b7624-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="b7624-155">Cuando el bus de servicio recibe una solicitud, busca el siguiente mensaje que se va a consumir, lo bloquea para impedir que otros consumidores lo reciban y, a continuación, lo devuelve a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7624-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="b7624-156">Una vez que la aplicación termina de procesar el mensaje (o lo almacena de forma confiable para su futuro procesamiento), completa la segunda fase del proceso de recepción mediante la realización de una llamada a `ServiceBusRestProxy->deleteMessage` en el mensaje recibido.</span><span class="sxs-lookup"><span data-stu-id="b7624-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="b7624-157">Cuando Service Bus ve la llamada `deleteMessage`, marca el mensaje como consumido y lo elimina de la cola.</span><span class="sxs-lookup"><span data-stu-id="b7624-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="b7624-158">En el ejemplo que aparece a continuación, se indica cómo se puede recibir y procesar un mensaje usando el modo [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (el modo predeterminado).</span><span class="sxs-lookup"><span data-stu-id="b7624-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="b7624-159">Actuación ante errores de la aplicación y mensajes que no se pueden leer</span><span class="sxs-lookup"><span data-stu-id="b7624-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="b7624-160">El Bus de servicio proporciona una funcionalidad que le ayuda a superar sin problemas los errores de la aplicación o las dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="b7624-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="b7624-161">Si por cualquier motivo una aplicación de recepción no puede procesar el mensaje, puede llamar al método `unlockMessage` en el mensaje recibido (en lugar de al método `deleteMessage`).</span><span class="sxs-lookup"><span data-stu-id="b7624-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="b7624-162">Esto hará que el Bus de servicio desbloquee el mensaje de la cola y esté disponible para que pueda volver a recibirse, ya sea por la misma aplicación que lo consume o por otra.</span><span class="sxs-lookup"><span data-stu-id="b7624-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="b7624-163">También hay un tiempo de espera asociado con un mensaje bloqueado en la cola y, si la aplicación no puede procesar el mensaje antes de que finalice el tiempo de espera del bloqueo (por ejemplo, si la aplicación sufre un error), entonces el Bus de servicio desbloquea el mensaje automáticamente y hace que esté disponible para que pueda volver a recibirse.</span><span class="sxs-lookup"><span data-stu-id="b7624-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="b7624-164">En caso de que la aplicación se bloquee después de procesar el mensaje, pero antes de realizar la solicitud `deleteMessage`, el mensaje se volverá a entregar a la aplicación cuando esta se reinicie.</span><span class="sxs-lookup"><span data-stu-id="b7624-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="b7624-165">Esta posibilidad habitualmente se denomina *Al menos un procesamiento*, es decir, cada mensaje se procesará al menos una vez; aunque en determinadas situaciones podría volver a entregarse el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="b7624-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="b7624-166">Si el escenario no puede tolerar el procesamiento duplicado,entonces se recomienda la incorporación de lógica adicional a la aplicación para administrar la entrega de mensajes duplicados.</span><span class="sxs-lookup"><span data-stu-id="b7624-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="b7624-167">A menudo, esto se consigue con la propiedad `getMessageId` del mensaje, que permanece constante en todos los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="b7624-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7624-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7624-168">Next steps</span></span>
<span data-ttu-id="b7624-169">Ahora que ya conoce los aspectos básicos de las colas de Service Bus, consulte [Colas, temas y suscripciones][Queues, topics, and subscriptions], donde encontrará más información.</span><span class="sxs-lookup"><span data-stu-id="b7624-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="b7624-170">Para más información, visite también el [Centro para desarrolladores de PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="b7624-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


