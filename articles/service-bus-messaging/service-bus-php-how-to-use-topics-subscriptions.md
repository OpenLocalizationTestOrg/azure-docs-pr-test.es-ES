---
title: temas de Bus de servicio de aaaHow toouse con PHP | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse temas de Bus de servicio con PHP en Azure."
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="8375a-103">¿Cómo toouse Service Bus temas y suscripciones con PHP</span><span class="sxs-lookup"><span data-stu-id="8375a-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="8375a-104">Este artículo muestra cómo toouse Service Bus temas y suscripciones.</span><span class="sxs-lookup"><span data-stu-id="8375a-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="8375a-105">ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="8375a-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="8375a-106">Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar tema de mensajes tooa**, **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="8375a-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="8375a-107">Creación de una aplicación PHP</span><span class="sxs-lookup"><span data-stu-id="8375a-107">Create a PHP application</span></span>
<span data-ttu-id="8375a-108">Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de Blob de Azure Hola es clases de tooreference de hello [Azure SDK para PHP](../php-download-sdk.md) desde dentro del código.</span><span class="sxs-lookup"><span data-stu-id="8375a-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="8375a-109">Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación o el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="8375a-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="8375a-110">La instalación de PHP también debe tener hello [OpenSSL extensión](http://php.net/openssl) instalado y habilitado.</span><span class="sxs-lookup"><span data-stu-id="8375a-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="8375a-111">Este artículo describe cómo toouse service características que se pueden llamar dentro de una aplicación PHP localmente o en código que se ejecuta dentro de un rol web de Azure, el rol de trabajo o el sitio Web.</span><span class="sxs-lookup"><span data-stu-id="8375a-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="8375a-112">Obtener Hola bibliotecas de cliente de Azure</span><span class="sxs-lookup"><span data-stu-id="8375a-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="8375a-113">Configurar el Bus de servicio de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="8375a-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="8375a-114">Hola toouse API del Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="8375a-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="8375a-115">Archivo de referencia hello cargador automático con hello [require_once] [ require-once] instrucción.</span><span class="sxs-lookup"><span data-stu-id="8375a-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="8375a-116">Hacer referencia a todas las clases que utilice.</span><span class="sxs-lookup"><span data-stu-id="8375a-116">Reference any classes you might use.</span></span>

<span data-ttu-id="8375a-117">Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServiceBusService** clase.</span><span class="sxs-lookup"><span data-stu-id="8375a-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="8375a-118">En este ejemplo (y otros ejemplos de este artículo) supone que ha instalado Hola PHP bibliotecas de cliente de Azure a través del compositor.</span><span class="sxs-lookup"><span data-stu-id="8375a-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="8375a-119">Si instala las bibliotecas de hello manualmente o como un paquete de PERA, debe hacer referencia a hello **WindowsAzure.php** archivo cargador automático.</span><span class="sxs-lookup"><span data-stu-id="8375a-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="8375a-120">Hola en los ejemplos siguientes, Hola `require_once` siempre se mostrará la instrucción, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8375a-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="8375a-121">Configuración de una conexión del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="8375a-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="8375a-122">tooinstantiate un cliente de Bus de servicio, primero debe tener una cadena de conexión válido en este formato:</span><span class="sxs-lookup"><span data-stu-id="8375a-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="8375a-123">Donde `Endpoint` normalmente tiene un formato hello `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="8375a-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="8375a-124">toocreate cualquier cliente de servicio de Azure debe usar hello `ServicesBuilder` clase.</span><span class="sxs-lookup"><span data-stu-id="8375a-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="8375a-125">Puede:</span><span class="sxs-lookup"><span data-stu-id="8375a-125">You can:</span></span>

* <span data-ttu-id="8375a-126">Pasar Hola conexión directamente cadena tooit.</span><span class="sxs-lookup"><span data-stu-id="8375a-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="8375a-127">Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="8375a-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="8375a-128">De manera predeterminada, admite un origen externo: variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="8375a-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="8375a-129">Puede agregar nuevos orígenes de extendiendo hello `ConnectionStringSource` clase.</span><span class="sxs-lookup"><span data-stu-id="8375a-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="8375a-130">Para obtener ejemplos de hello descritos a continuación, la cadena de conexión de Hola se pasa directamente.</span><span class="sxs-lookup"><span data-stu-id="8375a-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="8375a-131">de un tema</span><span class="sxs-lookup"><span data-stu-id="8375a-131">Create a topic</span></span>
<span data-ttu-id="8375a-132">Puede realizar operaciones de administración para temas de Bus de servicio a través de hello `ServiceBusRestProxy` clase.</span><span class="sxs-lookup"><span data-stu-id="8375a-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="8375a-133">A `ServiceBusRestProxy` se haya construido a través de hello `ServicesBuilder::createServiceBusService` método de fábrica con una cadena de conexión apropiada que encapsula Hola permisos token toomanage lo.</span><span class="sxs-lookup"><span data-stu-id="8375a-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="8375a-134">Hola siguiente ejemplo se muestra cómo tooinstantiate una `ServiceBusRestProxy` y llame a `ServiceBusRestProxy->createTopic` toocreate un tema llamado `mytopic` dentro de un `MySBNamespace` espacio de nombres:</span><span class="sxs-lookup"><span data-stu-id="8375a-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
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
> <span data-ttu-id="8375a-135">Puede usar hello `listTopics` método en `ServiceBusRestProxy` objetos toocheck si ya existe un tema con un nombre especificado dentro de un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="8375a-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="8375a-136">una suscripción</span><span class="sxs-lookup"><span data-stu-id="8375a-136">Create a subscription</span></span>
<span data-ttu-id="8375a-137">Suscripciones al tema también se crean con hello `ServiceBusRestProxy->createSubscription` método.</span><span class="sxs-lookup"><span data-stu-id="8375a-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="8375a-138">Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes que se pasan cola virtual de la suscripción de toohello.</span><span class="sxs-lookup"><span data-stu-id="8375a-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="8375a-139">Crea una suscripción con el filtro de hello predeterminado (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="8375a-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="8375a-140">Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="8375a-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="8375a-141">Cuando Hola **MatchAll** se utiliza el filtro, tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="8375a-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="8375a-142">Hello en el ejemplo siguiente se crea una suscripción denominada 'mysubscription' y usos Hola predeterminado **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="8375a-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="8375a-143">Creación de suscripciones con filtros</span><span class="sxs-lookup"><span data-stu-id="8375a-143">Create subscriptions with filters</span></span>
<span data-ttu-id="8375a-144">También puede configurar filtros que le permiten toospecify que envían los mensajes tooa tema debe aparecer dentro de una suscripción de tema específico.</span><span class="sxs-lookup"><span data-stu-id="8375a-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="8375a-145">el tipo más flexible de filtro compatible con las suscripciones Hello es hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), que implementa un subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="8375a-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="8375a-146">Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema.</span><span class="sxs-lookup"><span data-stu-id="8375a-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="8375a-147">Para más información sobre SqlFilters, consulte la [propiedad SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="8375a-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="8375a-148">Cada regla en una suscripción procesa los mensajes entrantes de forma independiente, agregar su suscripción de toohello de mensajes de resultados.</span><span class="sxs-lookup"><span data-stu-id="8375a-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="8375a-149">Además, cada nueva suscripción tiene un valor predeterminado **regla** objeto con un filtro que agrega todos los mensajes de Hola tema toohello una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8375a-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="8375a-150">tooreceive sólo los mensajes que coincidan con el filtro, debe quitar la regla predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8375a-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="8375a-151">Puede quitar regla predeterminada de hello mediante hello `ServiceBusRestProxy->deleteRule` método.</span><span class="sxs-lookup"><span data-stu-id="8375a-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="8375a-152">Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `MessageNumber` propiedad mayor que 3.</span><span class="sxs-lookup"><span data-stu-id="8375a-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="8375a-153">Vea [tema de enviar mensajes tooa](#send-messages-to-a-topic) para obtener información acerca de cómo agregar propiedades personalizadas toomessages.</span><span class="sxs-lookup"><span data-stu-id="8375a-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="8375a-154">Tenga en cuenta que este código requiere el uso de Hola de un espacio de nombres adicional: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="8375a-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="8375a-155">De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un `SqlFilter` que selecciona sólo los mensajes que tienen un `MessageNumber` propiedad menor o igual too3.</span><span class="sxs-lookup"><span data-stu-id="8375a-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="8375a-156">Ahora, cuando se envía un mensaje toohello `mytopic` tema, siempre que se entregue tooreceivers suscrito toohello `mysubscription` suscripción y tooreceivers selectivamente entregado suscrito toohello `HighMessages` y `LowMessages` (de suscripciones según el contenido del mensaje de Hola).</span><span class="sxs-lookup"><span data-stu-id="8375a-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="8375a-157">Enviar tema tooa de mensajes</span><span class="sxs-lookup"><span data-stu-id="8375a-157">Send messages tooa topic</span></span>
<span data-ttu-id="8375a-158">toosend un tema de Bus de servicio de tooa de mensaje, llama a la aplicación hello `ServiceBusRestProxy->sendTopicMessage` método.</span><span class="sxs-lookup"><span data-stu-id="8375a-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="8375a-159">Hola el siguiente código muestra cómo toosend un mensaje toohello `mytopic` tema creado anteriormente en el `MySBNamespace` el espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="8375a-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
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

<span data-ttu-id="8375a-160">Mensajes envían a temas de Bus tooService son instancias de hello [BrokeredMessage] [ BrokeredMessage] clase.</span><span class="sxs-lookup"><span data-stu-id="8375a-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="8375a-161">[BrokeredMessage] [ BrokeredMessage] objetos tienen un conjunto de métodos y propiedades estándar, así como propiedades que pueden ser propiedades específicas de la aplicación personalizadas de toohold usado.</span><span class="sxs-lookup"><span data-stu-id="8375a-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="8375a-162">Hello en el ejemplo siguiente se muestra cómo los mensajes de prueba toosend 5 toohello `mytopic` tema creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8375a-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="8375a-163">Hola `setProperty` método es tooadd usa una propiedad personalizada (`MessageNumber`) tooeach mensaje.</span><span class="sxs-lookup"><span data-stu-id="8375a-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="8375a-164">Tenga en cuenta que hello `MessageNumber` valor de propiedad varía en cada mensaje (puede usar este toodetermine valor qué suscripciones de recepción, tal y como se muestra en hello [crear una suscripción](#create-a-subscription) sección):</span><span class="sxs-lookup"><span data-stu-id="8375a-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="8375a-165">Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="8375a-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="8375a-166">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="8375a-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="8375a-167">No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema.</span><span class="sxs-lookup"><span data-stu-id="8375a-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="8375a-168">El límite superior para el tamaño del tema es de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="8375a-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="8375a-169">Para más información sobre las cuotas, consulte [Cuotas de Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="8375a-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="8375a-170">Recepción de mensajes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="8375a-170">Receive messages from a subscription</span></span>
<span data-ttu-id="8375a-171">mensajes de tooreceive de manera mejor de saludo de una suscripción es toouse un `ServiceBusRestProxy->receiveSubscriptionMessage` método.</span><span class="sxs-lookup"><span data-stu-id="8375a-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="8375a-172">Los mensajes se pueden recibir de dos modos diferentes: [*ReceiveAndDelete* y *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="8375a-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="8375a-173">**PeekLock** es Hola predeterminado.</span><span class="sxs-lookup"><span data-stu-id="8375a-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="8375a-174">Cuando se usa Hola [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , el modo de recepción es una operación de captura único; es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje en una suscripción, marca Hola mensaje como consumido y lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="8375a-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="8375a-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modo es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="8375a-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="8375a-176">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="8375a-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="8375a-177">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="8375a-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="8375a-178">En el valor predeterminado de hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, recibir un mensaje se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="8375a-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="8375a-179">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="8375a-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="8375a-180">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a proceso de recepción, pasando el mensaje de bienvenida recibido demasiado`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="8375a-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="8375a-181">Al Bus de servicio ve hello `deleteMessage` llamada, se marca el mensaje Hola como consumido y quitarlo de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="8375a-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="8375a-182">Hola siguiente ejemplo se muestra cómo tooreceive y procesar un mensaje mediante [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (modo Hola de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="8375a-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="8375a-183">Actuación ante errores de la aplicación y mensajes que no se pueden leer</span><span class="sxs-lookup"><span data-stu-id="8375a-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="8375a-184">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="8375a-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="8375a-185">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en mensajes de bienvenida recibido (en lugar de hello `deleteMessage` método).</span><span class="sxs-lookup"><span data-stu-id="8375a-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="8375a-186">Esto provocará el mensaje de saludo toounlock de Bus de servicio de cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="8375a-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="8375a-187">También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará el mensaje de bienvenida de automáticamente y hacerla disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="8375a-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="8375a-188">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se emite la solicitud, entonces el mensaje de Hola será aplicación toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="8375a-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="8375a-189">Esto se suele denominar *al menos una vez* procesamiento; es decir, cada mensaje se procesa al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="8375a-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="8375a-190">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar la entrega de mensajes duplicados de una lógica adicional tooapplications toohandle.</span><span class="sxs-lookup"><span data-stu-id="8375a-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="8375a-191">A menudo esto se logra utilizando hello `getMessageId` método del mensaje de Hola, que permanece constante en los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="8375a-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="8375a-192">Eliminación de temas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="8375a-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="8375a-193">toodelete un tema o una suscripción, use hello `ServiceBusRestProxy->deleteTopic` o hello `ServiceBusRestProxy->deleteSubscripton` métodos, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8375a-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="8375a-194">Tenga en cuenta que al eliminar un tema, también se elimina todas las suscripciones que están registradas en el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="8375a-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="8375a-195">Hello en el ejemplo siguiente se muestra cómo toodelete un tema denominado `mytopic` y sus suscripciones registrados.</span><span class="sxs-lookup"><span data-stu-id="8375a-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
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

<span data-ttu-id="8375a-196">Mediante el uso de hello `deleteSubscription` método, puede eliminar una suscripción de forma independiente:</span><span class="sxs-lookup"><span data-stu-id="8375a-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="8375a-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8375a-197">Next steps</span></span>
<span data-ttu-id="8375a-198">Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas, temas y suscripciones] [ Queues, topics, and subscriptions] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8375a-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
