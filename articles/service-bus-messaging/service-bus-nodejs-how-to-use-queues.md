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
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>¿Cómo toouse Bus de servicio pone en cola con Node.js

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este artículo describe cómo toouse Bus de servicio pone en cola con Node.js. ejemplos de Hola se escriben en JavaScript y usar hello módulo Node.js Azure. Hello escenarios descritos se incluyen **crear colas**, **enviar y recibir mensajes**, y **eliminar colas**. Para obtener más información sobre las colas, vea hello [pasos siguientes](#next-steps) sección.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Creación de una aplicación Node.js
Cree una aplicación Node.js vacía. Para obtener instrucciones sobre cómo toocreate una aplicación Node.js, vea [crear e implementar un tooan de aplicación Node.js sitio Web de Azure][Create and deploy a Node.js application tooan Azure Website], o [servicio de nube de Node.js] [ Node.js Cloud Service] con Windows PowerShell.

## <a name="configure-your-application-toouse-service-bus"></a>Configurar el Bus de servicio de aplicación toouse
toouse Bus de servicio de Azure, descargar y usar hello paquete de Node.js Azure. Este paquete incluye un conjunto de bibliotecas que se comunican con los servicios de REST de Bus de servicio de Hola.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete
1. Hola de uso **Windows PowerShell para Node.js** comando ventana toonavigate toohello **c:\\nodo\\sbqueues\\WebRole1** carpeta que haya creado el aplicación de ejemplo.
2. Tipo de **npm instalar azure** en la ventana de comandos de hello, que debería resultado salida similares toohello siguiente:

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
3. También puede ejecutar manualmente hello **ls** tooverify de comando que un **node_modules** se creó la carpeta. Dentro de ese Hola de Buscar carpeta **azure** paquete, que contiene las bibliotecas de Hola que necesita tooaccess colas de Service Bus.

### <a name="import-hello-module"></a>Módulo de Hola de importación
Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Configuración de una conexión del Bus de servicio de Azure
módulo de Azure Hello lee variable de entorno de hello `AZURE_SERVICEBUS_CONNECTION_STRING` necesita la información del tooobtain tooconnect tooService Bus. Si no se establece esta variable de entorno, debe especificar la información de la cuenta de hello al llamar a `createServiceBusService`.

Para obtener un ejemplo de establecer las variables de entorno de hello en un archivo de configuración para un servicio de nube de Azure, consulte [Node.js de servicio de nube con almacenamiento][Node.js Cloud Service with Storage].

Para obtener un ejemplo de establecer las variables de entorno de hello en hello [portal de Azure] [ Azure portal] para un sitio Web de Azure, consulte [aplicación Web de Node.js con almacenamiento] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Creación de una cola
Hola **ServiceBusService** objeto permite toowork con colas de Service Bus. Hello código siguiente se crea un **ServiceBusService** objeto. Agregar cerca de parte superior de Hola de hello **server.js** archivo, después de hello tooimport de instrucción Hola módulo de Azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Mediante una llamada a `createQueueIfNotExists` en hello **ServiceBusService** objeto Hola especificado se devuelve cola (si existe), o se crea una nueva cola con el nombre especificado de Hola. Hola siguiente de código usa `createQueueIfNotExists` toocreate o conectar con el nombre de cola de toohello `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Hola `createServiceBusService` método es compatible también con opciones adicionales, que permiten la configuración de la cola de toooverride de forma predeterminada, como el tamaño de cola toolive o máximo de tiempo de mensaje. Hello en el ejemplo siguiente se establece Hola cola máximo tamaño too5 GB y un valor de hora toolive (TTL) de 1 minuto:

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

### <a name="filters"></a>Filtros
Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **ServiceBusService**. Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:

```javascript
function handle (requestOptions, next)
```

Después de realizar su procesamiento previo en Opciones de solicitud de hello, debe llamar al método hello `next`, pasando una devolución de llamada con hello siguiente firma:

```javascript
function (returnObject, finalCallback, next)
```

En esta devolución de llamada y después procesamiento hello `returnObject` (hello respuesta Hola solicitud toohello servidor), o bien debe invocar la devolución de llamada de hello `next` si existe toocontinue otros filtros de procesamiento, o simplemente invocar `finalCallback`, donde finaliza la invocación de servicios de Hola.

Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, `ExponentialRetryPolicyFilter` y `LinearRetryPolicyFilter`. Hello código siguiente se crea un `ServiceBusService` objeto que usa Hola `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>Cola de mensajes tooa de envío
la aplicación llama a una cola de Service Bus de mensajes tooa toosend, hello `sendQueueMessage` método en hello **ServiceBusService** objeto. Los mensajes de las colas son demasiado (recibidos y enviados desde) Bus de servicio **BrokeredMessage** objetos y tener un conjunto de propiedades estándar (como **etiqueta** y **TimeToLive**), diccionario de propiedades personalizadas de específicos de la aplicación de toohold usado y un cuerpo de datos de aplicación arbitraria que. Una aplicación puede establecer cuerpo Hola de mensaje de saludo pasando una cadena como mensaje de bienvenida. Las propiedades estándar requeridas se rellenan con valores predeterminados.

Hello en el ejemplo siguiente se muestra cómo toosend una cola de toohello de mensajes de prueba denominado `myqueue` con `sendQueueMessage`:

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

Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo. El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB. Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>mensajes de una cola
Se reciben mensajes de una cola utilizando hello `receiveQueueMessage` método en hello **ServiceBusService** objeto. De forma predeterminada, los mensajes se eliminan de cola de hello cuando se leen; Sin embargo, puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la cola de Hola por establecer el parámetro opcional de hello `isPeekLock` demasiado**true**.

Hola comportamiento predeterminado de lectura y eliminación de mensajes de bienvenida tal como parte del programa Hola a la operación de recepción es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

Si hello `isPeekLock` parámetro está establecido demasiado**true**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a `deleteMessage` método y proporcionar toobe de mensaje de Hola eliminado como un parámetro. Hola `deleteMessage` método marca el mensaje Hola como consumido y lo quita de la cola de Hola.

Hello en el ejemplo siguiente se muestra cómo tooreceive y procesar mensajes usando `receiveQueueMessage`. Hello en el ejemplo se recibe por primera vez y elimina un mensaje y, a continuación, recibe un mensaje con `isPeekLock` establecido demasiado**true**, a continuación, elimina Hola mensaje utilizando `deleteMessage`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en hello **ServiceBusService** objeto. Esto provocará toounlock de Bus de servicio en el mensaje en cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si se produce un error de aplicación de hello tooprocess Hola mensaje antes de Hola tiempo de espera de bloqueo expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará automáticamente mensajes de bienvenida y hacerla disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. A menudo esto se logra utilizando hello **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de las colas, vea Hola recursos siguientes.

* [Colas, temas y suscripciones][Queues, topics, and subscriptions]
* Repositorio de [Azure SDK para Node][Azure SDK for Node] en GitHub
* [Centro para desarrolladores de Node.js](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
