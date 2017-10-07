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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>¿Cómo toouse Service Bus temas y suscripciones con PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este artículo muestra cómo toouse Service Bus temas y suscripciones. ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP](../php-download-sdk.md). Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar tema de mensajes tooa**, **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>Creación de una aplicación PHP
Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de Blob de Azure Hola es clases de tooreference de hello [Azure SDK para PHP](../php-download-sdk.md) desde dentro del código. Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación o el Bloc de notas.

> [!NOTE]
> La instalación de PHP también debe tener hello [OpenSSL extensión](http://php.net/openssl) instalado y habilitado.
> 
> 

Este artículo describe cómo toouse service características que se pueden llamar dentro de una aplicación PHP localmente o en código que se ejecuta dentro de un rol web de Azure, el rol de trabajo o el sitio Web.

## <a name="get-hello-azure-client-libraries"></a>Obtener Hola bibliotecas de cliente de Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar el Bus de servicio de aplicación toouse
Hola toouse API del Bus de servicio:

1. Archivo de referencia hello cargador automático con hello [require_once] [ require-once] instrucción.
2. Hacer referencia a todas las clases que utilice.

Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático **ServiceBusService** clase.

> [!NOTE]
> En este ejemplo (y otros ejemplos de este artículo) supone que ha instalado Hola PHP bibliotecas de cliente de Azure a través del compositor. Si instala las bibliotecas de hello manualmente o como un paquete de PERA, debe hacer referencia a hello **WindowsAzure.php** archivo cargador automático.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Hola en los ejemplos siguientes, Hola `require_once` siempre se mostrará la instrucción, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.

## <a name="set-up-a-service-bus-connection"></a>Configuración de una conexión del Bus de servicio
tooinstantiate un cliente de Bus de servicio, primero debe tener una cadena de conexión válido en este formato:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Donde `Endpoint` normalmente tiene un formato hello `https://[yourNamespace].servicebus.windows.net`.

toocreate cualquier cliente de servicio de Azure debe usar hello `ServicesBuilder` clase. Puede:

* Pasar Hola conexión directamente cadena tooit.
* Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:
  * De manera predeterminada, admite un origen externo: variables de entorno.
  * Puede agregar nuevos orígenes de extendiendo hello `ConnectionStringSource` clase.

Para obtener ejemplos de hello descritos a continuación, la cadena de conexión de Hola se pasa directamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>de un tema
Puede realizar operaciones de administración para temas de Bus de servicio a través de hello `ServiceBusRestProxy` clase. A `ServiceBusRestProxy` se haya construido a través de hello `ServicesBuilder::createServiceBusService` método de fábrica con una cadena de conexión apropiada que encapsula Hola permisos token toomanage lo.

Hola siguiente ejemplo se muestra cómo tooinstantiate una `ServiceBusRestProxy` y llame a `ServiceBusRestProxy->createTopic` toocreate un tema llamado `mytopic` dentro de un `MySBNamespace` espacio de nombres:

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
> Puede usar hello `listTopics` método en `ServiceBusRestProxy` objetos toocheck si ya existe un tema con un nombre especificado dentro de un espacio de nombres de servicio.
> 
> 

## <a name="create-a-subscription"></a>una suscripción
Suscripciones al tema también se crean con hello `ServiceBusRestProxy->createSubscription` método. Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes que se pasan cola virtual de la suscripción de toohello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Crea una suscripción con el filtro de hello predeterminado (MatchAll)
Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción. Cuando Hola **MatchAll** se utiliza el filtro, tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción de Hola. Hello en el ejemplo siguiente se crea una suscripción denominada 'mysubscription' y usos Hola predeterminado **MatchAll** filtro.

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

### <a name="create-subscriptions-with-filters"></a>Creación de suscripciones con filtros
También puede configurar filtros que le permiten toospecify que envían los mensajes tooa tema debe aparecer dentro de una suscripción de tema específico. el tipo más flexible de filtro compatible con las suscripciones Hello es hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), que implementa un subconjunto de SQL92. Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema. Para más información sobre SqlFilters, consulte la [propiedad SqlFilter.SqlExpression][sqlfilter].

> [!NOTE]
> Cada regla en una suscripción procesa los mensajes entrantes de forma independiente, agregar su suscripción de toohello de mensajes de resultados. Además, cada nueva suscripción tiene un valor predeterminado **regla** objeto con un filtro que agrega todos los mensajes de Hola tema toohello una suscripción. tooreceive sólo los mensajes que coincidan con el filtro, debe quitar la regla predeterminada de Hola. Puede quitar regla predeterminada de hello mediante hello `ServiceBusRestProxy->deleteRule` método.
> 
> 

Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `MessageNumber` propiedad mayor que 3. Vea [tema de enviar mensajes tooa](#send-messages-to-a-topic) para obtener información acerca de cómo agregar propiedades personalizadas toomessages.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Tenga en cuenta que este código requiere el uso de Hola de un espacio de nombres adicional: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un `SqlFilter` que selecciona sólo los mensajes que tienen un `MessageNumber` propiedad menor o igual too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

Ahora, cuando se envía un mensaje toohello `mytopic` tema, siempre que se entregue tooreceivers suscrito toohello `mysubscription` suscripción y tooreceivers selectivamente entregado suscrito toohello `HighMessages` y `LowMessages` (de suscripciones según el contenido del mensaje de Hola).

## <a name="send-messages-tooa-topic"></a>Enviar tema tooa de mensajes
toosend un tema de Bus de servicio de tooa de mensaje, llama a la aplicación hello `ServiceBusRestProxy->sendTopicMessage` método. Hola el siguiente código muestra cómo toosend un mensaje toohello `mytopic` tema creado anteriormente en el `MySBNamespace` el espacio de nombres de servicio.

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

Mensajes envían a temas de Bus tooService son instancias de hello [BrokeredMessage] [ BrokeredMessage] clase. [BrokeredMessage] [ BrokeredMessage] objetos tienen un conjunto de métodos y propiedades estándar, así como propiedades que pueden ser propiedades específicas de la aplicación personalizadas de toohold usado. Hello en el ejemplo siguiente se muestra cómo los mensajes de prueba toosend 5 toohello `mytopic` tema creado anteriormente. Hola `setProperty` método es tooadd usa una propiedad personalizada (`MessageNumber`) tooeach mensaje. Tenga en cuenta que hello `MessageNumber` valor de propiedad varía en cada mensaje (puede usar este toodetermine valor qué suscripciones de recepción, tal y como se muestra en hello [crear una suscripción](#create-a-subscription) sección):

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

Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema. El límite superior para el tamaño del tema es de 5 GB. Para más información sobre las cuotas, consulte [Cuotas de Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Recepción de mensajes de una suscripción
mensajes de tooreceive de manera mejor de saludo de una suscripción es toouse un `ServiceBusRestProxy->receiveSubscriptionMessage` método. Los mensajes se pueden recibir de dos modos diferentes: [*ReceiveAndDelete* y *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** es Hola predeterminado.

Cuando se usa Hola [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , el modo de recepción es una operación de captura único; es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje en una suscripción, marca Hola mensaje como consumido y lo devuelve toohello aplicación. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modo es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

En el valor predeterminado de hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modo, recibir un mensaje se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a proceso de recepción, pasando el mensaje de bienvenida recibido demasiado`ServiceBusRestProxy->deleteMessage`. Al Bus de servicio ve hello `deleteMessage` llamada, se marca el mensaje Hola como consumido y quitarlo de la cola de Hola.

Hola siguiente ejemplo se muestra cómo tooreceive y procesar un mensaje mediante [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (modo Hola de forma predeterminada). 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Actuación ante errores de la aplicación y mensajes que no se pueden leer
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en mensajes de bienvenida recibido (en lugar de hello `deleteMessage` método). Esto provocará el mensaje de saludo toounlock de Bus de servicio de cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará el mensaje de bienvenida de automáticamente y hacerla disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se emite la solicitud, entonces el mensaje de Hola será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar *al menos una vez* procesamiento; es decir, cada mensaje se procesa al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar la entrega de mensajes duplicados de una lógica adicional tooapplications toohandle. A menudo esto se logra utilizando hello `getMessageId` método del mensaje de Hola, que permanece constante en los intentos de entrega.

## <a name="delete-topics-and-subscriptions"></a>Eliminación de temas y suscripciones
toodelete un tema o una suscripción, use hello `ServiceBusRestProxy->deleteTopic` o hello `ServiceBusRestProxy->deleteSubscripton` métodos, respectivamente. Tenga en cuenta que al eliminar un tema, también se elimina todas las suscripciones que están registradas en el tema de Hola.

Hello en el ejemplo siguiente se muestra cómo toodelete un tema denominado `mytopic` y sus suscripciones registrados.

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

Mediante el uso de hello `deleteSubscription` método, puede eliminar una suscripción de forma independiente:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas, temas y suscripciones] [ Queues, topics, and subscriptions] para obtener más información.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
