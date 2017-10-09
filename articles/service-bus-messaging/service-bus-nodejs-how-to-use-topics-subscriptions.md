---
title: aaaHow toouse Service Bus de Azure temas y suscripciones con Node.js | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Service Bus temas y suscripciones de Azure desde una aplicación Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>¿Cómo tooUse Service Bus temas y suscripciones con Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Esta guía se describe cómo toouse Service Bus temas y suscripciones desde aplicaciones Node.js. Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar mensajes** tooa tema **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**. Para obtener más información acerca de temas y suscripciones, vea hello [pasos siguientes](#next-steps) sección.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Creación de una aplicación Node.js
Cree una aplicación Node.js vacía. Para obtener instrucciones sobre cómo crear una aplicación Node.js, vea [crear e implementar un tooan de aplicación Node.js sitio Web de Azure], [servicio de nube de Node.js] [ Node.js Cloud Service] con Windows PowerShell o sitio Web con WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Configurar el Bus de servicio de aplicación toouse
toouse Bus de servicio, descargue Hola paquete de Node.js Azure. Este paquete incluye un conjunto de bibliotecas que se comunican con los servicios de REST de Bus de servicio de Hola.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), desplazarse por las carpetas de toohello en la que creó la aplicación de ejemplo.
2. Tipo de **npm instalar azure** en la ventana de comandos de hello, que debe dar como resultado de hello después de salida:

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
3. También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta. Dentro de esa carpeta, busque la **azure** paquete, que contiene las bibliotecas de Hola que necesita tooaccess temas de Bus de servicio.

### <a name="import-hello-module"></a>Módulo de Hola de importación
Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Configuración de una conexión del Bus de servicio
módulo de Azure Hello lee las variables de entorno de hello `AZURE_SERVICEBUS_NAMESPACE` y `AZURE_SERVICEBUS_ACCESS_KEY` para obtener información necesaria tooconnect tooService Bus. Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a `createServiceBusService`.

Para obtener un ejemplo de establecer variables de entorno de Hola para un servicio de nube de Azure, consulte [Node.js de servicio de nube con almacenamiento][Node.js Cloud Service with Storage].

Para obtener un ejemplo de Hola las variables de entorno para un sitio Web de Azure, consulte [aplicación Web de Node.js con almacenamiento][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>de un tema
Hola **ServiceBusService** objeto permite toowork con temas. El siguiente código crea un objeto **ServiceBusService**. Agregar en la parte superior de hello **server.js** archivo, después de módulo de hello instrucción tooimport hello azure:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Mediante una llamada a `createTopicIfNotExists` en hello **ServiceBusService** objeto Hola especificado (si existe), se devolverá tema o se creará un nuevo tema con nombre especificado de Hola. Hola siguiente de código usa `createTopicIfNotExists` toocreate o conectar con el nombre de tema de toohello `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Hola `createServiceBusService` método es compatible también con opciones adicionales, que permiten la configuración de tema predeterminada toooverride como tiempo de mensaje para activarse o tamaño máximo del tema. Hello en el ejemplo siguiente se establece hello too5GB de tamaño máximo del tema con un tiempo toolive de 1 minuto:

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>Filtros
Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **ServiceBusService**. Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:

```javascript
function handle (requestOptions, next)
```

Tras el preprocesamiento sobre las opciones de solicitud de hello, Hola llamadas al método `next`, pasando una devolución de llamada con hello siguiente firma:

```javascript
function (returnObject, finalCallback, next)
```

En esta devolución de llamada y después Hola de procesamiento `returnObject` (hello respuesta Hola solicitud toohello servidor), devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o invocar `finalCallback` en caso contrario, hello tooend invocación de servicio.

Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**. Hola siguiente crea un **ServiceBusService** objeto que usa hello **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Creación de suscripciones
Suscripciones al tema también se crean con hello **ServiceBusService** objeto. Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes entregados cola virtual de la suscripción de toohello.

> [!NOTE]
> Las suscripciones son persistentes y continuará tooexist hasta que ambos se o hello tema están asociadas, se eliminan. Si la aplicación contiene lógica toocreate una suscripción, debe comprobar primero si Hola ya existe la suscripción mediante el uso de la `getSubscription` método.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Crea una suscripción con el filtro de hello predeterminado (MatchAll)
Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción. Cuando Hola **MatchAll** filtro se usa, el tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción. Hello en el ejemplo siguiente se crea una suscripción denominada 'AllMessages' y usos Hola predeterminado **MatchAll** filtro.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Creación de suscripciones con filtros
También puede crear filtros que le permiten tooscope que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción de tema específico.

Hola tipo más flexible de filtro compatible con las suscripciones es el **SqlFilter**, que implementa un subconjunto de SQL92. Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema. Para obtener más información acerca de las expresiones de Hola que pueden usarse con un filtro SQL, revise hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintaxis.

Filtros se pueden agregar suscripción tooa mediante el uso de hello `createRule` método de hello **ServiceBusService** objeto. Este método permite agregar nueva suscripción existente tooan de filtros.

> [!NOTE]
> Porque el filtro de hello predeterminado se aplica automáticamente tooall nuevas suscripciones, primero debe quitar el filtro predeterminado de Hola o **MatchAll** invalidará cualquier otro filtro que se puede especificar. Puede quitar regla predeterminada de hello mediante hello `deleteRule` método de la **ServiceBusService** objeto.
>
>

Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `messagenumber` propiedad mayor que 3:

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un `messagenumber` propiedad menor o igual too3:

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Cuando se envía un mensaje ahora demasiado`MyTopic`, siempre se entregará a los receptores suscritos toohello `AllMessages` suscripción al tema y tooreceivers selectivamente entregado suscrito toohello `HighMessages` y `LowMessages` suscripciones al tema (según el contenido del mensaje de Hola.)

## <a name="how-toosend-messages-tooa-topic"></a>¿Cómo toosend mensajes tooa tema
toosend un tema de Bus de servicio de tooa de mensaje, la aplicación debe utilizar el `sendTopicMessage` método de hello **ServiceBusService** objeto.
Mensajes envían son temas de Bus tooService **BrokeredMessage** objetos.
**BrokeredMessage** objetos tienen un conjunto de propiedades estándar (como `Label` y `TimeToLive`), un diccionario de propiedades de toohold usado personalizadas específicas de la aplicación y un cuerpo de datos de cadena. Una aplicación puede establecer cuerpo Hola de mensaje de bienvenida, pasando el valor de cadena a saludos `sendTopicMessage` y cualquier necesaria propiedades estándar se rellenará con valores predeterminados.

Hello en el ejemplo siguiente se muestra cómo toosend cinco mensajes de prueba a `MyTopic`. Tenga en cuenta que hello `messagenumber` valor de propiedad de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determinará qué suscripciones reciban):

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema. El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).

## <a name="receive-messages-from-a-subscription"></a>Recepción de mensajes de una suscripción
Los mensajes se reciben de una suscripción con el `receiveSubscriptionMessage` método en hello **ServiceBusService** objeto. De forma predeterminada, los mensajes se eliminan de la suscripción de hello cuando se leen; Sin embargo, puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la suscripción de Hola por establecer el parámetro opcional de hello `isPeekLock` demasiado**true**.

comportamiento predeterminado de Hola de leer y eliminar mensajes de bienvenida como parte de la operación de recepción es el modelo más sencillo de Hola y funciona mejor en escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en el que el ejemplo hello problemas de consumidor recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

Si hello `isPeekLock` parámetro está establecido demasiado**true**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.
Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del proceso de recepción mediante una llamada a **deleteMessage** método y proporcionar la toobe de mensaje eliminar como un parámetro. Hola **deleteMessage** método marcar Hola mensaje como consumido y quitarlo de la suscripción de Hola.

Hello en el ejemplo siguiente se muestra cómo se pueden recibir mensajes y el uso de procesado `receiveSubscriptionMessage`. Hello en el ejemplo se recibe por primera vez y elimina un mensaje de Hola 'LowMessages' suscripción y, a continuación, recibe un mensaje de Hola 'HighMessages' suscripción con `isPeekLock` establecer tootrue. A continuación, elimina el mensaje hello mediante `deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en el **ServiceBusService** objeto. Esto provocará toounlock de Bus de servicio en el mensaje de suscripción de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado con un mensaje bloqueado dentro de la suscripción, y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloquea el mensaje de bienvenida automáticamente y la convierte en disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. A menudo esto se logra mediante la **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.

## <a name="delete-topics-and-subscriptions"></a>Eliminación de temas y suscripciones
Temas y suscripciones son persistentes y debe ser explícitamente eliminados a través de hello [portal de Azure] [ Azure portal] o mediante programación.
Hello en el ejemplo siguiente se muestra cómo se denomina tema de hello toodelete `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Eliminar un tema, también se eliminarán las suscripciones que están registradas en el tema de Hola. También se pueden eliminar las suscripciones de forma independiente. En el ejemplo siguiente se muestra cómo toodelete una suscripción denominada `HighMessages` de hello `MyTopic` tema:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de temas de Bus de servicio, siga estos toolearn de vínculos más.

* Vea [Colas, temas y suscripciones][Queues, topics, and subscriptions].
* Referencia de API para [SqlFilter][SqlFilter].
* Visite hello [Azure SDK para el nodo] [ Azure SDK for Node] repositorio en GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[crear e implementar un tooan de aplicación Node.js sitio Web de Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
