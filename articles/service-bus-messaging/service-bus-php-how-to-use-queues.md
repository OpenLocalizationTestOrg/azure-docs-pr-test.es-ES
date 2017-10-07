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
# <a name="how-toouse-service-bus-queues-with-php"></a>¿Cómo toouse Bus de servicio pone en cola con PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Esta guía le mostrará cómo toouse colas de Service Bus. ejemplos de Hello escritos en PHP y usar hello [Azure SDK para PHP](../php-download-sdk.md). Hello escenarios descritos se incluyen **crear colas**, **enviar y recibir mensajes**, y **eliminar colas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Creación de una aplicación PHP
Hola solo requisito para crear una aplicación PHP que tiene acceso a servicio de Blob de Azure de hello es hello las referencias de las clases de hello [Azure SDK para PHP](../php-download-sdk.md) desde dentro del código. Puede usar cualquier toocreate de herramientas de desarrollo de la aplicación o el Bloc de notas.

> [!NOTE]
> La instalación de PHP también debe tener hello [OpenSSL extensión](http://php.net/openssl) instalado y habilitado.
> 
> 

En esta guía, utilizará funciones del servicio a las que se puede llamar desde una aplicación PHP localmente o bien mediante código a través de un rol web, rol de trabajo o sitio web de Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtener Hola bibliotecas de cliente de Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar el Bus de servicio de aplicación toouse
cola de Service Bus de hello toouse API, Hola siguientes:

1. Archivo de referencia hello cargador automático con hello [require_once] [ require_once] instrucción.
2. Hacer referencia a todas las clases que utilice.

Hello en el ejemplo siguiente se muestra cómo tooinclude Hola Hola de referencia y el archivo de cargador automático `ServicesBuilder` clase.

> [!NOTE]
> En este ejemplo (y otros ejemplos de este artículo) supone que ha instalado Hola PHP bibliotecas de cliente de Azure a través del compositor. Si instala las bibliotecas de hello manualmente o como un paquete de PERA, debe hacer referencia a hello **WindowsAzure.php** archivo cargador automático.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

En los siguientes ejemplos de hello, Hola `require_once` siempre se mostrará la instrucción, pero se hace referencia a clases de hello solo es necesarias para tooexecute de ejemplo de Hola.

## <a name="set-up-a-service-bus-connection"></a>Configuración de una conexión del Bus de servicio
tooinstantiate un cliente de Bus de servicio, primero debe tener una cadena de conexión válida en este formato:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Donde `Endpoint` normalmente tiene un formato hello `[yourNamespace].servicebus.windows.net`.

toocreate cualquier cliente de servicio de Azure debe usar hello `ServicesBuilder` clase. Puede:

* Pasar Hola conexión directamente cadena tooit.
* Hola de uso **CloudConfigurationManager (CCM)** toocheck externos de varios orígenes para la cadena de conexión de hello:
  * De manera predeterminada, admite un origen externo: variables de entorno.
  * Puede agregar nuevos orígenes de extendiendo hello `ConnectionStringSource` (clase)

Para obtener ejemplos de hello descritos a continuación, la cadena de conexión de Hola se pasa directamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Creación de una cola
Puede realizar operaciones de administración para las colas de Bus de servicio a través de hello `ServiceBusRestProxy` clase. A `ServiceBusRestProxy` se haya construido a través de hello `ServicesBuilder::createServiceBusService` método de fábrica con una cadena de conexión apropiada que encapsula Hola permisos token toomanage lo.

Hola siguiente ejemplo se muestra cómo tooinstantiate una `ServiceBusRestProxy` y llame a `ServiceBusRestProxy->createQueue` toocreate una cola denominada `myqueue` dentro de un `MySBNamespace` el espacio de nombres de servicio:

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
> Puede usar hello `listQueues` método en `ServiceBusRestProxy` objetos toocheck si ya existe una cola con un nombre especificado dentro de un espacio de nombres.
> 
> 

## <a name="send-messages-tooa-queue"></a>Cola de mensajes tooa de envío
la aplicación llama a una cola de Service Bus de mensajes tooa toosend, hello `ServiceBusRestProxy->sendQueueMessage` método. Hola el siguiente código muestra cómo toosend un mensaje toohello `myqueue` cola creada anteriormente en el `MySBNamespace` espacio de nombres de servicio.

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

Mensajes de colas de Service Bus demasiado (recibidas y enviadas desde) son instancias de hello [BrokeredMessage] [ BrokeredMessage] clase. [BrokeredMessage] [ BrokeredMessage] objetos tienen un conjunto de métodos estándar y propiedades que son propiedades de toohold usado personalizadas específicas de la aplicación y un cuerpo de datos de aplicación arbitrarios.

Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo. Este límite superior para el tamaño de la cola es de 5 GB.

## <a name="receive-messages-from-a-queue"></a>mensajes de una cola

mensajes de tooreceive de manera mejor de saludo de una cola es toouse un `ServiceBusRestProxy->receiveQueueMessage` método. Los mensajes se pueden recibir de dos modos diferentes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) y [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** es Hola predeterminado.

Cuando se usa [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) , el modo de recepción es una operación de captura único; es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje en una cola, marca Hola mensaje como consumido y lo devuelve toohello aplicación. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modo es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

En el valor predeterminado de hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modo, recibir un mensaje se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, encuentra Hola siguiente mensaje toobe consumido, la bloquea tooprevent otros consumidores de recibir y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a proceso de recepción, pasando el mensaje de bienvenida recibido demasiado`ServiceBusRestProxy->deleteMessage`. Al Bus de servicio ve hello `deleteMessage` llamada, se marca el mensaje Hola como consumido y quitarlo de la cola de Hola.

Hola siguiente ejemplo se muestra cómo tooreceive y procesar un mensaje mediante [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (modo Hola de forma predeterminada).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle

Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en mensajes de bienvenida recibido (en lugar de hello `deleteMessage` método). Esto provocará el mensaje de saludo toounlock de Bus de servicio de cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará el mensaje de bienvenida de automáticamente y hacerla disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se emite la solicitud, entonces el mensaje de Hola será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar *al menos una vez* procesamiento; es decir, cada mensaje se procesa al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, a continuación, se recomienda agregar la entrega de mensajes duplicados de una lógica adicional tooapplications toohandle. A menudo esto se logra utilizando hello `getMessageId` método del mensaje de Hola, que permanece constante en los intentos de entrega.

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas, temas y suscripciones] [ Queues, topics, and subscriptions] para obtener más información.

Para obtener más información, visite también hello [Centro para desarrolladores de PHP](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


