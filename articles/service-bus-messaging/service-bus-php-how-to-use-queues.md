---
title: aaaHow toouse Bus de servicio pone en cola con PHP | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Bus de servicio pone en cola en Azure. Ejemplos de código escritos en PHP."
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
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="0dd1a-104">¿Cómo toouse Bus de servicio pone en cola con PHP</span><span class="sxs-lookup"><span data-stu-id="0dd1a-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="0dd1a-105">Esta guía le mostrará cómo toouse colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="0dd1a-106">ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0dd1a-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="0dd1a-107">Hello escenarios descritos se incluyen **crear colas**, **enviar y recibir mensajes**, y **eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="0dd1a-108">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="0dd1a-108">Create a PHP application</span></span>
<span data-ttu-id="0dd1a-109">Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de Blob de Azure de hello es hello las referencias de las clases de hello [Azure SDK para PHP](../php-download-sdk.md) desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="0dd1a-110">Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación o el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="0dd1a-111">La instalación de PHP también debe tener hello [OpenSSL extensión](http://php.net/openssl) instalado y habilitado.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="0dd1a-112">En esta guía, utilizará funciones del servicio a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="0dd1a-113">Obtener Hola bibliotecas de cliente de Azure</span><span class="sxs-lookup"><span data-stu-id="0dd1a-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="0dd1a-114">Configurar el Bus de servicio de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="0dd1a-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="0dd1a-115">cola de Service Bus de hello toouse API, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="0dd1a-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="0dd1a-116">Archivo de referencia hello cargador automático con hello [require_once] [ require_once] instrucción.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="0dd1a-117">Hacer referencia a todas las clases que utilice.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-117">Reference any classes you might use.</span></span>

<span data-ttu-id="0dd1a-118">Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático `ServicesBuilder` clase.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="0dd1a-119">En este ejemplo (y otros ejemplos de este artículo) supone que ha instalado Hola PHP bibliotecas de cliente de Azure a través del compositor.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="0dd1a-120">Si instala las bibliotecas de hello manualmente o como un paquete de PERA, debe hacer referencia a hello **WindowsAzure.php** archivo cargador automático.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="0dd1a-121">En los siguientes ejemplos de hello, Hola `require_once` siempre se mostrará la instrucción, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="0dd1a-122">Configuración de una conexión del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="0dd1a-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="0dd1a-123">tooinstantiate un cliente de Bus de servicio, primero debe tener una cadena de conexión válida en este formato:</span><span class="sxs-lookup"><span data-stu-id="0dd1a-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="0dd1a-124">Donde `Endpoint` normalmente tiene un formato hello `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="0dd1a-125">toocreate cualquier cliente de servicio de Azure debe usar hello `ServicesBuilder` clase.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="0dd1a-126">Puede:</span><span class="sxs-lookup"><span data-stu-id="0dd1a-126">You can:</span></span>

* <span data-ttu-id="0dd1a-127">Pasar Hola conexión directamente cadena tooit.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="0dd1a-128">Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="0dd1a-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="0dd1a-129">De manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="0dd1a-130">Puede agregar nuevos orígenes de extendiendo hello `ConnectionStringSource` (clase)</span><span class="sxs-lookup"><span data-stu-id="0dd1a-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="0dd1a-131">Para obtener ejemplos de hello descritos a continuación, la cadena de conexión de Hola se pasa directamente.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="0dd1a-132">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="0dd1a-132">Create a queue</span></span>
<span data-ttu-id="0dd1a-133">Puede realizar operaciones de administración para las colas de Bus de servicio a través de hello `ServiceBusRestProxy` clase.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="0dd1a-134">A `ServiceBusRestProxy` se haya construido a través de hello `ServicesBuilder::createServiceBusService` método de fábrica con una cadena de conexión apropiada que encapsula Hola permisos token toomanage lo.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="0dd1a-135">Hola siguiente ejemplo se muestra cómo tooinstantiate una `ServiceBusRestProxy` y llame a `ServiceBusRestProxy->createQueue` toocreate una cola denominada `myqueue` dentro de un `MySBNamespace` el espacio de nombres de servicio:</span><span class="sxs-lookup"><span data-stu-id="0dd1a-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="0dd1a-136">Puede usar hello `listQueues` método en `ServiceBusRestProxy` objetos toocheck si ya existe una cola con un nombre especificado dentro de un espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="0dd1a-137">Cola de mensajes tooa de envío</span><span class="sxs-lookup"><span data-stu-id="0dd1a-137">Send messages tooa queue</span></span>
<span data-ttu-id="0dd1a-138">la aplicación llama a una cola de Service Bus de mensajes tooa toosend, hello `ServiceBusRestProxy->sendQueueMessage` método.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="0dd1a-139">Hola el siguiente código muestra cómo toosend un mensaje toohello `myqueue` cola creada anteriormente en el `MySBNamespace` espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="0dd1a-140">Mensajes de colas de Service Bus demasiado (recibidas y enviadas desde) son instancias de hello [BrokeredMessage] [ BrokeredMessage] clase.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="0dd1a-141">[BrokeredMessage] [ BrokeredMessage] objetos tienen un conjunto de métodos estándar y propiedades que son propiedades de toohold usado personalizadas específicas de la aplicación y un cuerpo de datos de aplicación arbitrarios.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="0dd1a-142">Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="0dd1a-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="0dd1a-143">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="0dd1a-144">No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="0dd1a-145">Este límite superior para el tamaño de la cola es de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="0dd1a-146">mensajes de una cola</span><span class="sxs-lookup"><span data-stu-id="0dd1a-146">Receive messages from a queue</span></span>

<span data-ttu-id="0dd1a-147">mensajes de tooreceive de manera mejor de saludo de una cola es toouse un `ServiceBusRestProxy->receiveQueueMessage` método.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="0dd1a-148">Los mensajes se pueden recibir de dos modos diferentes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) y [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="0dd1a-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="0dd1a-149">**PeekLock** es Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="0dd1a-150">Cuando se usa [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) , el modo de recepción es una operación de captura único; es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje en una cola, marca Hola mensaje como consumido y lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="0dd1a-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="0dd1a-152">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="0dd1a-153">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="0dd1a-154">En el valor predeterminado de hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo, recibir un mensaje se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="0dd1a-155">Al Bus de servicio recibe una solicitud, encuentra Hola siguiente mensaje toobe consumido, la bloquea tooprevent otros consumidores de recibir y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="0dd1a-156">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a proceso de recepción, pasando el mensaje de bienvenida recibido demasiado`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="0dd1a-157">Al Bus de servicio ve hello `deleteMessage` llamada, se marca el mensaje Hola como consumido y quitarlo de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="0dd1a-158">Hola siguiente ejemplo se muestra cómo tooreceive y procesar un mensaje mediante [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (modo Hola de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="0dd1a-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="0dd1a-159">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="0dd1a-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="0dd1a-160">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="0dd1a-161">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en mensajes de bienvenida recibido (en lugar de hello `deleteMessage` método).</span><span class="sxs-lookup"><span data-stu-id="0dd1a-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="0dd1a-162">Esto provocará el mensaje de saludo toounlock de Bus de servicio de cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="0dd1a-163">También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará el mensaje de bienvenida de automáticamente y hacerla disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="0dd1a-164">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se emite la solicitud, entonces el mensaje de Hola será aplicación toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="0dd1a-165">Esto se suele denominar *al menos una vez* procesamiento; es decir, cada mensaje se procesa al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="0dd1a-166">Si el escenario de hello no puede tolerar el procesamiento duplicado, a continuación, se recomienda agregar la entrega de mensajes duplicados de una lógica adicional tooapplications toohandle.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="0dd1a-167">A menudo esto se logra utilizando hello `getMessageId` método del mensaje de Hola, que permanece constante en los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dd1a-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0dd1a-168">Next steps</span></span>
<span data-ttu-id="0dd1a-169">Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas, temas y suscripciones] [ Queues, topics, and subscriptions] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0dd1a-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="0dd1a-170">Para obtener más información, visite también hello [Centro para desarrolladores de PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="0dd1a-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


