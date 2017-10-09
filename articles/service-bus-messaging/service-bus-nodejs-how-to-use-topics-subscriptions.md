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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="ea6af-103">¿Cómo tooUse Service Bus temas y suscripciones con Node.js</span><span class="sxs-lookup"><span data-stu-id="ea6af-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="ea6af-104">Esta guía se describe cómo toouse Service Bus temas y suscripciones desde aplicaciones Node.js.</span><span class="sxs-lookup"><span data-stu-id="ea6af-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="ea6af-105">Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar mensajes** tooa tema **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="ea6af-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="ea6af-106">Para obtener más información acerca de temas y suscripciones, vea hello [pasos siguientes](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="ea6af-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="ea6af-107">Creación de una aplicación Node.js</span><span class="sxs-lookup"><span data-stu-id="ea6af-107">Create a Node.js application</span></span>
<span data-ttu-id="ea6af-108">Cree una aplicación Node.js vacía.</span><span class="sxs-lookup"><span data-stu-id="ea6af-108">Create a blank Node.js application.</span></span> <span data-ttu-id="ea6af-109">Para obtener instrucciones sobre cómo crear una aplicación Node.js, vea [crear e implementar un tooan de aplicación Node.js sitio Web de Azure], [servicio de nube de Node.js] [ Node.js Cloud Service] con Windows PowerShell o sitio Web con WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="ea6af-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="ea6af-110">Configurar el Bus de servicio de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="ea6af-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="ea6af-111">toouse Bus de servicio, descargue Hola paquete de Node.js Azure.</span><span class="sxs-lookup"><span data-stu-id="ea6af-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="ea6af-112">Este paquete incluye un conjunto de bibliotecas que se comunican con los servicios de REST de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea6af-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="ea6af-113">Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete</span><span class="sxs-lookup"><span data-stu-id="ea6af-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="ea6af-114">Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), desplazarse por las carpetas de toohello en la que creó la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ea6af-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="ea6af-115">Tipo de **npm instalar azure** en la ventana de comandos de hello, que debe dar como resultado de hello después de salida:</span><span class="sxs-lookup"><span data-stu-id="ea6af-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="ea6af-116">También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta.</span><span class="sxs-lookup"><span data-stu-id="ea6af-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="ea6af-117">Dentro de esa carpeta, busque la **azure** paquete, que contiene las bibliotecas de Hola que necesita tooaccess temas de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="ea6af-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="ea6af-118">Módulo de Hola de importación</span><span class="sxs-lookup"><span data-stu-id="ea6af-118">Import hello module</span></span>
<span data-ttu-id="ea6af-119">Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="ea6af-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="ea6af-120">Configuración de una conexión del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="ea6af-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="ea6af-121">módulo de Azure Hello lee las variables de entorno de hello `AZURE_SERVICEBUS_NAMESPACE` y `AZURE_SERVICEBUS_ACCESS_KEY` para obtener información necesaria tooconnect tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="ea6af-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="ea6af-122">Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="ea6af-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="ea6af-123">Para obtener un ejemplo de establecer variables de entorno de Hola para un servicio de nube de Azure, consulte [Node.js de servicio de nube con almacenamiento][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="ea6af-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="ea6af-124">Para obtener un ejemplo de Hola las variables de entorno para un sitio Web de Azure, consulte [aplicación Web de Node.js con almacenamiento][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="ea6af-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="ea6af-125">de un tema</span><span class="sxs-lookup"><span data-stu-id="ea6af-125">Create a topic</span></span>
<span data-ttu-id="ea6af-126">Hola **ServiceBusService** objeto permite toowork con temas.</span><span class="sxs-lookup"><span data-stu-id="ea6af-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="ea6af-127">El siguiente código crea un objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ea6af-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="ea6af-128">Agregar en la parte superior de hello **server.js** archivo, después de módulo de hello instrucción tooimport hello azure:</span><span class="sxs-lookup"><span data-stu-id="ea6af-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="ea6af-129">Mediante una llamada a `createTopicIfNotExists` en hello **ServiceBusService** objeto Hola especificado (si existe), se devolverá tema o se creará un nuevo tema con nombre especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea6af-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="ea6af-130">Hola siguiente de código usa `createTopicIfNotExists` toocreate o conectar con el nombre de tema de toohello `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="ea6af-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="ea6af-131">Hola `createServiceBusService` método es compatible también con opciones adicionales, que permiten la configuración de tema predeterminada toooverride como tiempo de mensaje para activarse o tamaño máximo del tema.</span><span class="sxs-lookup"><span data-stu-id="ea6af-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="ea6af-132">Hello en el ejemplo siguiente se establece hello too5GB de tamaño máximo del tema con un tiempo toolive de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="ea6af-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="ea6af-133">Filtros</span><span class="sxs-lookup"><span data-stu-id="ea6af-133">Filters</span></span>
<span data-ttu-id="ea6af-134">Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ea6af-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="ea6af-135">Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:</span><span class="sxs-lookup"><span data-stu-id="ea6af-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="ea6af-136">Tras el preprocesamiento sobre las opciones de solicitud de hello, Hola llamadas al método `next`, pasando una devolución de llamada con hello siguiente firma:</span><span class="sxs-lookup"><span data-stu-id="ea6af-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="ea6af-137">En esta devolución de llamada y después Hola de procesamiento `returnObject` (hello respuesta Hola solicitud toohello servidor), devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o invocar `finalCallback` en caso contrario, hello tooend invocación de servicio.</span><span class="sxs-lookup"><span data-stu-id="ea6af-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="ea6af-138">Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="ea6af-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="ea6af-139">Hola siguiente crea un **ServiceBusService** objeto que usa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="ea6af-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="ea6af-140">Creación de suscripciones</span><span class="sxs-lookup"><span data-stu-id="ea6af-140">Create subscriptions</span></span>
<span data-ttu-id="ea6af-141">Suscripciones al tema también se crean con hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ea6af-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="ea6af-142">Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes entregados cola virtual de la suscripción de toohello.</span><span class="sxs-lookup"><span data-stu-id="ea6af-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="ea6af-143">Las suscripciones son persistentes y continuará tooexist hasta que ambos se o hello tema están asociadas, se eliminan.</span><span class="sxs-lookup"><span data-stu-id="ea6af-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="ea6af-144">Si la aplicación contiene lógica toocreate una suscripción, debe comprobar primero si Hola ya existe la suscripción mediante el uso de la `getSubscription` método.</span><span class="sxs-lookup"><span data-stu-id="ea6af-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="ea6af-145">Crea una suscripción con el filtro de hello predeterminado (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="ea6af-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="ea6af-146">Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="ea6af-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="ea6af-147">Cuando Hola **MatchAll** filtro se usa, el tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ea6af-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="ea6af-148">Hello en el ejemplo siguiente se crea una suscripción denominada 'AllMessages' y usos Hola predeterminado **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="ea6af-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="ea6af-149">Creación de suscripciones con filtros</span><span class="sxs-lookup"><span data-stu-id="ea6af-149">Create subscriptions with filters</span></span>
<span data-ttu-id="ea6af-150">También puede crear filtros que le permiten tooscope que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción de tema específico.</span><span class="sxs-lookup"><span data-stu-id="ea6af-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="ea6af-151">Hola tipo más flexible de filtro compatible con las suscripciones es el **SqlFilter**, que implementa un subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="ea6af-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="ea6af-152">Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema.</span><span class="sxs-lookup"><span data-stu-id="ea6af-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="ea6af-153">Para obtener más información acerca de las expresiones de Hola que pueden usarse con un filtro SQL, revise hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintaxis.</span><span class="sxs-lookup"><span data-stu-id="ea6af-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="ea6af-154">Filtros se pueden agregar suscripción tooa mediante el uso de hello `createRule` método de hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ea6af-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="ea6af-155">Este método permite agregar nueva suscripción existente tooan de filtros.</span><span class="sxs-lookup"><span data-stu-id="ea6af-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ea6af-156">Porque el filtro de hello predeterminado se aplica automáticamente tooall nuevas suscripciones, primero debe quitar el filtro predeterminado de Hola o **MatchAll** invalidará cualquier otro filtro que se puede especificar.</span><span class="sxs-lookup"><span data-stu-id="ea6af-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="ea6af-157">Puede quitar regla predeterminada de hello mediante hello `deleteRule` método de la **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ea6af-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="ea6af-158">Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `messagenumber` propiedad mayor que 3:</span><span class="sxs-lookup"><span data-stu-id="ea6af-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="ea6af-159">De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un `messagenumber` propiedad menor o igual too3:</span><span class="sxs-lookup"><span data-stu-id="ea6af-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="ea6af-160">Cuando se envía un mensaje ahora demasiado`MyTopic`, siempre se entregará a los receptores suscritos toohello `AllMessages` suscripción al tema y tooreceivers selectivamente entregado suscrito toohello `HighMessages` y `LowMessages` suscripciones al tema (según el contenido del mensaje de Hola.)</span><span class="sxs-lookup"><span data-stu-id="ea6af-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="ea6af-161">¿Cómo toosend mensajes tooa tema</span><span class="sxs-lookup"><span data-stu-id="ea6af-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="ea6af-162">toosend un tema de Bus de servicio de tooa de mensaje, la aplicación debe utilizar el `sendTopicMessage` método de hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ea6af-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="ea6af-163">Mensajes envían son temas de Bus tooService **BrokeredMessage** objetos.</span><span class="sxs-lookup"><span data-stu-id="ea6af-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="ea6af-164">**BrokeredMessage** objetos tienen un conjunto de propiedades estándar (como `Label` y `TimeToLive`), un diccionario de propiedades de toohold usado personalizadas específicas de la aplicación y un cuerpo de datos de cadena.</span><span class="sxs-lookup"><span data-stu-id="ea6af-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="ea6af-165">Una aplicación puede establecer cuerpo Hola de mensaje de bienvenida, pasando el valor de cadena a saludos `sendTopicMessage` y cualquier necesaria propiedades estándar se rellenará con valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="ea6af-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="ea6af-166">Hello en el ejemplo siguiente se muestra cómo toosend cinco mensajes de prueba a `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="ea6af-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="ea6af-167">Tenga en cuenta que hello `messagenumber` valor de propiedad de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determinará qué suscripciones reciban):</span><span class="sxs-lookup"><span data-stu-id="ea6af-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="ea6af-168">Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ea6af-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ea6af-169">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ea6af-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ea6af-170">No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema.</span><span class="sxs-lookup"><span data-stu-id="ea6af-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="ea6af-171">El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).</span><span class="sxs-lookup"><span data-stu-id="ea6af-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="ea6af-172">Recepción de mensajes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="ea6af-172">Receive messages from a subscription</span></span>
<span data-ttu-id="ea6af-173">Los mensajes se reciben de una suscripción con el `receiveSubscriptionMessage` método en hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ea6af-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="ea6af-174">De forma predeterminada, los mensajes se eliminan de la suscripción de hello cuando se leen; Sin embargo, puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la suscripción de Hola por establecer el parámetro opcional de hello `isPeekLock` demasiado**true**.</span><span class="sxs-lookup"><span data-stu-id="ea6af-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="ea6af-175">comportamiento predeterminado de Hola de leer y eliminar mensajes de bienvenida como parte de la operación de recepción es el modelo más sencillo de Hola y funciona mejor en escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="ea6af-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="ea6af-176">toounderstand esto, considere un escenario en el que el ejemplo hello problemas de consumidor recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="ea6af-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="ea6af-177">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="ea6af-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="ea6af-178">Si hello `isPeekLock` parámetro está establecido demasiado**true**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="ea6af-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ea6af-179">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="ea6af-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="ea6af-180">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del proceso de recepción mediante una llamada a **deleteMessage** método y proporcionar la toobe de mensaje eliminar como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="ea6af-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="ea6af-181">Hola **deleteMessage** método marcar Hola mensaje como consumido y quitarlo de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea6af-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="ea6af-182">Hello en el ejemplo siguiente se muestra cómo se pueden recibir mensajes y el uso de procesado `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="ea6af-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="ea6af-183">Hello en el ejemplo se recibe por primera vez y elimina un mensaje de Hola 'LowMessages' suscripción y, a continuación, recibe un mensaje de Hola 'HighMessages' suscripción con `isPeekLock` establecer tootrue.</span><span class="sxs-lookup"><span data-stu-id="ea6af-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="ea6af-184">A continuación, elimina el mensaje hello mediante `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="ea6af-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ea6af-185">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="ea6af-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="ea6af-186">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="ea6af-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ea6af-187">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlockMessage` método en el **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="ea6af-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="ea6af-188">Esto provocará toounlock de Bus de servicio en el mensaje de suscripción de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="ea6af-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ea6af-189">También hay un tiempo de espera asociado con un mensaje bloqueado dentro de la suscripción, y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloquea el mensaje de bienvenida automáticamente y la convierte en disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ea6af-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="ea6af-190">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `deleteMessage` se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="ea6af-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="ea6af-191">Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="ea6af-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="ea6af-192">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje.</span><span class="sxs-lookup"><span data-stu-id="ea6af-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="ea6af-193">A menudo esto se logra mediante la **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="ea6af-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="ea6af-194">Eliminación de temas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="ea6af-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="ea6af-195">Temas y suscripciones son persistentes y debe ser explícitamente eliminados a través de hello [portal de Azure] [ Azure portal] o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="ea6af-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="ea6af-196">Hello en el ejemplo siguiente se muestra cómo se denomina tema de hello toodelete `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="ea6af-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="ea6af-197">Eliminar un tema, también se eliminarán las suscripciones que están registradas en el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea6af-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="ea6af-198">También se pueden eliminar las suscripciones de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="ea6af-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="ea6af-199">En el ejemplo siguiente se muestra cómo toodelete una suscripción denominada `HighMessages` de hello `MyTopic` tema:</span><span class="sxs-lookup"><span data-stu-id="ea6af-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="ea6af-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea6af-200">Next Steps</span></span>
<span data-ttu-id="ea6af-201">Ahora que conoce los fundamentos de Hola de temas de Bus de servicio, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="ea6af-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="ea6af-202">Vea [Colas, temas y suscripciones][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="ea6af-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="ea6af-203">Referencia de API para [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="ea6af-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="ea6af-204">Visite hello [Azure SDK para el nodo] [ Azure SDK for Node] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ea6af-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[crear e implementar un tooan de aplicación Node.js sitio Web de Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
