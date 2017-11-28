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
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="94869-104">¿Cómo toouse almacenamiento de cola de Node.js</span><span class="sxs-lookup"><span data-stu-id="94869-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="94869-105">Información general</span><span class="sxs-lookup"><span data-stu-id="94869-105">Overview</span></span>
<span data-ttu-id="94869-106">Esta guía le mostrará cómo tooperform escenarios comunes con Hola servicio cola de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="94869-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="94869-107">ejemplos de Hola se escriben con hello API Node.js.</span><span class="sxs-lookup"><span data-stu-id="94869-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="94869-108">Hello escenarios descritos se incluyen **insertar**, **leerlo**, **obtener**, y **eliminar** cola los mensajes, así como  **crear y eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="94869-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="94869-109">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="94869-109">Create a Node.js Application</span></span>
<span data-ttu-id="94869-110">Cree una aplicación Node.js vacía.</span><span class="sxs-lookup"><span data-stu-id="94869-110">Create a blank Node.js application.</span></span> <span data-ttu-id="94869-111">Consulte las instrucciones de creación de una aplicación Node.js [crear una aplicación web de Node.js en el servicio de aplicación de Azure](../../app-service-web/app-service-web-get-started-nodejs.md), [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) mediante Windows PowerShell o [ Compilar e implementar un tooAzure de aplicación web de Node.js mediante Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="94869-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="94869-112">Configurar la aplicación tooAccess almacenamiento</span><span class="sxs-lookup"><span data-stu-id="94869-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="94869-113">toouse almacenamiento de Azure, necesitará Hola SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="94869-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="94869-114">Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete</span><span class="sxs-lookup"><span data-stu-id="94869-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="94869-115">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), desplazarse por las carpetas de toohello en la que creó la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="94869-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="94869-116">Tipo de **npm instalar almacenamiento de azure** en la ventana de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="94869-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="94869-117">Salida de comando de hello es similar toohello siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="94869-117">Output from hello command is similar toohello following example.</span></span>
 
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

3. <span data-ttu-id="94869-118">También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta.</span><span class="sxs-lookup"><span data-stu-id="94869-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="94869-119">Dentro de esa carpeta, encontrará hello **almacenamiento de azure** paquete, que contiene las bibliotecas de Hola que necesita para tener acceso al almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="94869-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="94869-120">Importar paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="94869-120">Import hello package</span></span>
<span data-ttu-id="94869-121">Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello el **server.js** archivo de aplicación hello donde piensa toouse almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="94869-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="94869-122">Configuración de una conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="94869-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="94869-123">módulo de Hello azure leerá variables de entorno de hello AZURE\_almacenamiento\_cuenta y AZURE\_almacenamiento\_acceso\_clave o AZURE\_almacenamiento\_conexión \_Cadena para la información necesaria tooconnect tooyour cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="94869-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="94869-124">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="94869-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="94869-125">Para obtener un ejemplo de establecer las variables de entorno de hello en hello [Portal de Azure](https://portal.azure.com) para un sitio Web de Azure, vea [Node.js web app con] Hola servicio tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="94869-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="94869-126">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="94869-126">How To: Create a Queue</span></span>
<span data-ttu-id="94869-127">Hello código siguiente se crea un **QueueService** objeto, lo que permite toowork con colas.</span><span class="sxs-lookup"><span data-stu-id="94869-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="94869-128">Hola de uso **createQueueIfNotExists** método, que devuelve la cola especificada Hola si ya existe o crea una nueva cola con el nombre especificado de hello si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="94869-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="94869-129">Si se crea la cola de hello, `result.created` es true.</span><span class="sxs-lookup"><span data-stu-id="94869-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="94869-130">Si existe la cola de hello, `result.created` es false.</span><span class="sxs-lookup"><span data-stu-id="94869-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="94869-131">Filtros</span><span class="sxs-lookup"><span data-stu-id="94869-131">Filters</span></span>
<span data-ttu-id="94869-132">Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="94869-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="94869-133">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:</span><span class="sxs-lookup"><span data-stu-id="94869-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="94869-134">Una vez hecho el preprocesamiento sobre las opciones de solicitud de hello, método hello necesita toocall "siguiente" pasando una devolución de llamada con hello siguiente firma:</span><span class="sxs-lookup"><span data-stu-id="94869-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="94869-135">En esta devolución de llamada y, después de procesar hello returnObject (respuesta Hola Hola solicitud enviada toohello al servidor), la devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o simplemente invocar finalCallback tooend en caso contrario la Hola invocación de servicio.</span><span class="sxs-lookup"><span data-stu-id="94869-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="94869-136">Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="94869-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="94869-137">Hola siguiente crea un **QueueService** objeto que usa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="94869-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="94869-138">Inserción de un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="94869-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="94869-139">un mensaje en una cola, use hello tooinsert **createMessage** método para crear un nuevo mensaje y agregar toohello cola.</span><span class="sxs-lookup"><span data-stu-id="94869-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="94869-140">Cómo: Ver en el siguiente mensaje de Hola</span><span class="sxs-lookup"><span data-stu-id="94869-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="94869-141">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **peekMessages** método.</span><span class="sxs-lookup"><span data-stu-id="94869-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="94869-142">De forma predeterminada, **peekMessages** inspecciona un único mensaje.</span><span class="sxs-lookup"><span data-stu-id="94869-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="94869-143">Hola `result` contiene mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="94869-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="94869-144">Usar **peekMessages** cuando hay mensajes en cola de hello no devolverá un error, sin embargo, no se devolverá ningún mensaje.</span><span class="sxs-lookup"><span data-stu-id="94869-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="94869-145">Cómo: Hola siguiente mensaje de eliminación de cola</span><span class="sxs-lookup"><span data-stu-id="94869-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="94869-146">El procesamiento de un mensaje es un proceso que consta de dos etapas:</span><span class="sxs-lookup"><span data-stu-id="94869-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="94869-147">Eliminar mensajes de bienvenida de la cola.</span><span class="sxs-lookup"><span data-stu-id="94869-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="94869-148">Eliminar mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="94869-148">Delete hello message.</span></span>

<span data-ttu-id="94869-149">toodequeue un mensaje, utilice **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="94869-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="94869-150">Esto hace que los mensajes de Hola invisible en la cola de hello, por lo que no hay otros clientes que pueden procesar.</span><span class="sxs-lookup"><span data-stu-id="94869-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="94869-151">Una vez que la aplicación ha procesado un mensaje, llame a **deleteMessage** toodelete desde cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="94869-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="94869-152">Hola de ejemplo siguiente obtiene un mensaje y, a continuación, elimina:</span><span class="sxs-lookup"><span data-stu-id="94869-152">hello following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="94869-153">De forma predeterminada, sólo se oculta un mensaje durante 30 segundos, tras lo cual es clientes tooother visible.</span><span class="sxs-lookup"><span data-stu-id="94869-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="94869-154">Puede especificar un valor diferente usando `options.visibilityTimeout` con **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="94869-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="94869-155">Usar **getMessages** cuando hay mensajes en cola de hello no devolverá un error, sin embargo, no se devolverá ningún mensaje.</span><span class="sxs-lookup"><span data-stu-id="94869-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="94869-156">Cómo: Cambiar el contenido de Hola de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="94869-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="94869-157">Se puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de hello mediante **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="94869-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="94869-158">Hola siguiente ejemplo actualiza el texto hello de un mensaje:</span><span class="sxs-lookup"><span data-stu-id="94869-158">hello following example updates hello text of a message:</span></span>

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

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="94869-159">Opciones adicionales para extraer mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="94869-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="94869-160">Hay dos formas de personalizar la recuperación de mensajes de una cola:</span><span class="sxs-lookup"><span data-stu-id="94869-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="94869-161">`options.numOfMessages`-Recupere un lote de mensajes (arriba too32.)</span><span class="sxs-lookup"><span data-stu-id="94869-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="94869-162">`options.visibilityTimeout` - Establecer un tiempo de espera de invisibilidad más largo o más corto.</span><span class="sxs-lookup"><span data-stu-id="94869-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="94869-163">Hello en el ejemplo siguiente se usa hello **getMessages** tooget 15 mensajes de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="94869-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="94869-164">A continuación, procesa cada mensaje con un bucle for.</span><span class="sxs-lookup"><span data-stu-id="94869-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="94869-165">También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para todos los mensajes devueltos por este método.</span><span class="sxs-lookup"><span data-stu-id="94869-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="94869-166">Cómo: Obtener la longitud de la cola de Hola</span><span class="sxs-lookup"><span data-stu-id="94869-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="94869-167">Hola **getQueueMetadata** devuelve los metadatos de la cola de hello, incluyendo el número aproximado de Hola de mensajes en espera en cola Hola.</span><span class="sxs-lookup"><span data-stu-id="94869-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="94869-168">Enumeración de las colas</span><span class="sxs-lookup"><span data-stu-id="94869-168">How To: List Queues</span></span>
<span data-ttu-id="94869-169">una lista de las colas, utilice tooretrieve **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="94869-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="94869-170">tooretrieve una lista filtrada por un prefijo concreto, use **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="94869-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="94869-171">Si no se puede devolver todas las colas, `result.continuationToken` puede utilizarse como Hola el primer parámetro de **listQueuesSegmented** u Hola segundo parámetro de **listQueuesSegmentedWithPrefix** tooretrieve más resultados.</span><span class="sxs-lookup"><span data-stu-id="94869-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="94869-172">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="94869-172">How To: Delete a Queue</span></span>
<span data-ttu-id="94869-173">toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **deleteQueue** método hello en objetos de cola.</span><span class="sxs-lookup"><span data-stu-id="94869-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="94869-174">tooclear todos los mensajes de una cola sin eliminarla, use **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="94869-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="94869-175">Trabajo con firmas de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="94869-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="94869-176">Las firmas de acceso compartido (SAS) son un tooqueues de acceso granular de tooprovide de forma segura sin tener que proporcionar el nombre de la cuenta de almacenamiento o claves.</span><span class="sxs-lookup"><span data-stu-id="94869-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="94869-177">SAS son a menudo las colas de tooyour del acceso de tooprovide uso limitado, como permitir que los mensajes de toosubmit de una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="94869-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="94869-178">Una aplicación de confianza, como un servicio basado en la nube genera una SAS con hello **generatesharedaccesssignature tal** de hello **QueueService**y proporciona tooan aplicación de confianza o de confianza parcial.</span><span class="sxs-lookup"><span data-stu-id="94869-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="94869-179">Por ejemplo, una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="94869-179">For example, a mobile app.</span></span> <span data-ttu-id="94869-180">Hola SAS se genera mediante una directiva, que describe el inicio de Hola y fechas de finalización durante qué Hola SAS es válido, así como Hola titular SAS toohello concedidos nivel de acceso.</span><span class="sxs-lookup"><span data-stu-id="94869-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="94869-181">Hola de ejemplo siguiente genera una nueva directiva de acceso compartido que le permitirá la cola toohello SAS titular tooadd mensajes hello y expira 100 minutos tarde Hola se crea.</span><span class="sxs-lookup"><span data-stu-id="94869-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="94869-182">Tenga en cuenta que información de host de hello debe proporcionarse también, tal y como se requiere cuando titular SAS de hello intentos de cola de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="94869-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="94869-183">Hola aplicación cliente, a continuación, utiliza Hola SAS con **QueueServiceWithSAS** tooperform operaciones en cola Hola.</span><span class="sxs-lookup"><span data-stu-id="94869-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="94869-184">Hola siguiente ejemplo conecta la cola de toohello y crea un mensaje.</span><span class="sxs-lookup"><span data-stu-id="94869-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="94869-185">Puesto que hello SAS se generó con el acceso de complemento, si se realiza un intento tooread, actualizar o eliminar los mensajes, se devolvería un error.</span><span class="sxs-lookup"><span data-stu-id="94869-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="94869-186">Listas de control de acceso</span><span class="sxs-lookup"><span data-stu-id="94869-186">Access control lists</span></span>
<span data-ttu-id="94869-187">También puede usar una directiva de acceso de Hola de tooset de lista de Control de acceso (ACL) para una SAS.</span><span class="sxs-lookup"><span data-stu-id="94869-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="94869-188">Esto es útil si desea tooallow cola de varios clientes tooaccess hello, pero proporcionar las directivas de acceso diferente para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="94869-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="94869-189">Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva.</span><span class="sxs-lookup"><span data-stu-id="94869-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="94869-190">Hola siguiente ejemplo define dos directivas; uno para "user1" y otro para el usuario '2':</span><span class="sxs-lookup"><span data-stu-id="94869-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="94869-191">Hola siguiendo el ejemplo se obtiene Hola ACL actual para **myqueue**, a continuación, agrega nuevas directivas de hello mediante **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="94869-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="94869-192">Este enfoque permite lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="94869-192">This approach allows:</span></span>

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

<span data-ttu-id="94869-193">Una vez se ha establecido la ACL de hello, puede crear una SAS basada en Id. de Hola para una directiva.</span><span class="sxs-lookup"><span data-stu-id="94869-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="94869-194">Hola de ejemplo siguiente crea una nueva SAS para el usuario '2':</span><span class="sxs-lookup"><span data-stu-id="94869-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="94869-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94869-195">Next Steps</span></span>
<span data-ttu-id="94869-196">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="94869-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="94869-197">Visite Hola [Team Blog de almacenamiento Azure] [Blog del equipo de almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="94869-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="94869-198">Visite hello [SDK de almacenamiento de Azure para el nodo] [ Azure Storage SDK for Node] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="94869-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="94869-199">
[Creación de una aplicación web de Node.js en Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="94869-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="94869-200">[Aplicación web de Node.js con hello servicio tabla de Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="94869-200">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="94869-201">[Compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="94869-201">[Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="94869-202">[Blog del equipo de almacenamiento de azure]: http://blogs.msdn.com/b/windowsazurestorage/ [compilar e implementar un tooAzure de aplicación web de Node.js mediante Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="94869-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
