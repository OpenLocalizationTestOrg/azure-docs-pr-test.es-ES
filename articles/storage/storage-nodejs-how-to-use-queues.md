---
title: almacenamiento de la cola de Node.js del aaaHow toouse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate del servicio de cola de Azure de toouse hello y colas de delete y insert, obtener y eliminar mensajes. Ejemplos escritos en Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>¿Cómo toouse almacenamiento de cola de Node.js
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio cola de Microsoft Azure. ejemplos de Hola se escriben con hello API Node.js. Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Creación de una aplicación Node.js
Cree una aplicación Node.js vacía. Consulte las instrucciones de creación de una aplicación Node.js [crear una aplicación web de Node.js en el servicio de aplicación de Azure], [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure] mediante Windows PowerShell o [ Compilar e implementar un tooAzure de aplicación web de Node.js mediante Web Matrix].

## <a name="configure-your-application-tooaccess-storage"></a>Configurar la aplicación tooAccess almacenamiento
toouse almacenamiento de Azure, necesitará Hola SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), desplazarse por las carpetas de toohello en la que creó la aplicación de ejemplo.
2. Tipo de **npm instalar almacenamiento de azure** en la ventana de comandos de Hola. Salida de comando de hello es similar toohello siguiente ejemplo.
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta. Dentro de esa carpeta, encontrará hello **almacenamiento de azure** paquete, que contiene las bibliotecas de Hola que necesita para tener acceso al almacenamiento.

### <a name="import-hello-package"></a>Importar paquete de Hola
Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello el **server.js** archivo de aplicación hello donde piensa toouse almacenamiento:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Configuración de una conexión de almacenamiento de Azure
módulo de Hello azure leerá variables de entorno de hello AZURE\_almacenamiento\_cuenta y AZURE\_almacenamiento\_acceso\_clave o AZURE\_almacenamiento\_conexión \_Cadena para la información necesaria tooconnect tooyour cuenta de almacenamiento de Azure. Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a **createQueueService**.

Para obtener un ejemplo de establecer las variables de entorno de hello en hello [Portal de Azure](https://portal.azure.com) para un sitio Web de Azure, consulte [aplicación web de Node.js con Hola servicio tabla de Azure].

## <a name="how-to-create-a-queue"></a>Creación de una cola
Hello código siguiente se crea un **QueueService** objeto, lo que permite toowork con colas.

```
var queueSvc = azure.createQueueService();
```

Hola de uso **createQueueIfNotExists** método, que devuelve la cola especificada Hola si ya existe o crea una nueva cola con el nombre especificado de hello si aún no existe.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Si se crea la cola de hello, `result.created` es true. Si existe la cola de hello, `result.created` es false.

### <a name="filters"></a>Filtros
Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **QueueService**. Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:

```
function handle (requestOptions, next)
```

Una vez hecho el preprocesamiento sobre las opciones de solicitud de hello, método hello necesita toocall "siguiente" pasando una devolución de llamada con hello siguiente firma:

```
function (returnObject, finalCallback, next)
```

En esta devolución de llamada y, después de procesar hello returnObject (respuesta Hola Hola solicitud enviada toohello al servidor), la devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o simplemente invocar finalCallback tooend en caso contrario la Hola invocación de servicio.

Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**. Hola siguiente crea un **QueueService** objeto que usa hello **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Inserción de un mensaje en una cola
un mensaje en una cola, use hello tooinsert **createMessage** método para crear un nuevo mensaje y agregar toohello cola.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Cómo: Ver en el siguiente mensaje de Hola
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peekMessages** método. De forma predeterminada, **peekMessages** inspecciona un único mensaje.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Hola `result` contiene mensajes de bienvenida.

> [!NOTE]
> Usar **peekMessages** cuando hay mensajes en cola de hello no devolverá un error, sin embargo, no se devolverá ningún mensaje.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Cómo: Hola siguiente mensaje de eliminación de cola
El procesamiento de un mensaje es un proceso que consta de dos etapas:

1. Eliminar mensajes de bienvenida de la cola.
2. Eliminar mensajes de bienvenida.

toodequeue un mensaje, utilice **getMessages**. Esto hace que los mensajes de Hola invisible en la cola de hello, por lo que no hay otros clientes que pueden procesar. Una vez que la aplicación ha procesado un mensaje, llame a **deleteMessage** toodelete desde cola de Hola. Hola de ejemplo siguiente obtiene un mensaje y, a continuación, elimina:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> De forma predeterminada, sólo se oculta un mensaje durante 30 segundos, tras lo cual es clientes tooother visible. Puede especificar un valor diferente usando `options.visibilityTimeout` con **getMessages**.
> 
> [!NOTE]
> Usar **getMessages** cuando hay mensajes en cola de hello no devolverá un error, sin embargo, no se devolverá ningún mensaje.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Cómo: Cambiar el contenido de Hola de un mensaje en cola
Se puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de hello mediante **updateMessage**. Hola siguiente ejemplo actualiza el texto hello de un mensaje:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Opciones adicionales para extraer mensajes de la cola
Hay dos formas de personalizar la recuperación de mensajes de una cola:

* `options.numOfMessages`-Recupere un lote de mensajes (arriba too32.)
* `options.visibilityTimeout` - Establecer un tiempo de espera de invisibilidad más largo o más corto.

Hello en el ejemplo siguiente se usa hello **getMessages** tooget 15 mensajes de método en una llamada. A continuación, procesa cada mensaje con un bucle for. También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para todos los mensajes devueltos por este método.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>Cómo: Obtener la longitud de la cola de Hola
Hola **getQueueMetadata** devuelve los metadatos de la cola de hello, incluyendo el número aproximado de Hola de mensajes en espera en cola Hola.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Enumeración de las colas
una lista de las colas, utilice tooretrieve **listQueuesSegmented**. tooretrieve una lista filtrada por un prefijo concreto, use **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Si no se puede devolver todas las colas, `result.continuationToken` puede utilizarse como Hola el primer parámetro de **listQueuesSegmented** u Hola segundo parámetro de **listQueuesSegmentedWithPrefix** tooretrieve más resultados.

## <a name="how-to-delete-a-queue"></a>Eliminación de una cola
toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **deleteQueue** método hello en objetos de cola.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

tooclear todos los mensajes de una cola sin eliminarla, use **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Trabajo con firmas de acceso compartido
Las firmas de acceso compartido (SAS) son un tooqueues de acceso granular de tooprovide de forma segura sin tener que proporcionar el nombre de la cuenta de almacenamiento o claves. SAS son a menudo las colas de tooyour del acceso de tooprovide uso limitado, como permitir que los mensajes de toosubmit de una aplicación móvil.

Una aplicación de confianza, como un servicio basado en la nube genera una SAS con hello **generatesharedaccesssignature tal** de hello **QueueService**y proporciona tooan aplicación de confianza o de confianza parcial. Por ejemplo, una aplicación móvil. Hola SAS se genera mediante una directiva, que describe el inicio de Hola y fechas de finalización durante qué Hola SAS es válido, así como Hola titular SAS toohello concedidos nivel de acceso.

Hola de ejemplo siguiente genera una nueva directiva de acceso compartido que le permitirá la cola toohello SAS titular tooadd mensajes hello y expira 100 minutos tarde Hola se crea.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Tenga en cuenta que información de host de hello debe proporcionarse también, tal y como se requiere cuando titular SAS de hello intentos de cola de hello tooaccess.

Hola aplicación cliente, a continuación, utiliza Hola SAS con **QueueServiceWithSAS** tooperform operaciones en cola Hola. Hola siguiente ejemplo conecta la cola de toohello y crea un mensaje.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Puesto que hello SAS se generó con el acceso de complemento, si se realiza un intento tooread, actualizar o eliminar los mensajes, se devolvería un error.

### <a name="access-control-lists"></a>Listas de control de acceso
También puede usar una directiva de acceso de Hola de tooset de lista de Control de acceso (ACL) para una SAS. Esto es útil si desea tooallow cola de varios clientes tooaccess hello, pero proporcionar las directivas de acceso diferente para cada cliente.

Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva. Hola siguiente ejemplo define dos directivas; uno para "user1" y otro para el usuario '2':

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hola siguiendo el ejemplo se obtiene Hola ACL actual para **myqueue**, a continuación, agrega nuevas directivas de hello mediante **setQueueAcl**. Este enfoque permite lo siguiente:

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Una vez se ha establecido la ACL de hello, puede crear una SAS basada en Id. de Hola para una directiva. Hola de ejemplo siguiente crea una nueva SAS para el usuario '2':

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.

* Visite hello [Blog del equipo de almacenamiento de Azure][Azure Storage Team Blog].
* Visite hello [SDK de almacenamiento de Azure para el nodo] [ Azure Storage SDK for Node] repositorio en GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[crear una aplicación web de Node.js en el servicio de aplicación de Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[aplicación web de Node.js con Hola servicio tabla de Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Compilar e implementar un tooAzure de aplicación web de Node.js mediante Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
