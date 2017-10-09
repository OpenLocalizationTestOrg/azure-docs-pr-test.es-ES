---
title: temas de aaaHow toouse Service Bus de Azure con Java | Documentos de Microsoft
description: Uso de temas y suscripciones de Service Bus en Azure
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="db909-103">¿Cómo toouse Service Bus temas y suscripciones con Java</span><span class="sxs-lookup"><span data-stu-id="db909-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="db909-104">Esta guía se describe cómo toouse Service Bus temas y suscripciones.</span><span class="sxs-lookup"><span data-stu-id="db909-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="db909-105">ejemplos de Hello están escritos en Java y usar hello [Azure SDK para Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="db909-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="db909-106">Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar tema de mensajes tooa**, **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="db909-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="db909-107">Qué son los temas y las suscripciones del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="db909-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="db909-108">Las suscripciones y los temas del Bus de servicio son compatibles con el modelo de comunicación de mensajería de *publicación/suscripción* .</span><span class="sxs-lookup"><span data-stu-id="db909-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="db909-109">Cuando se usan temas y suscripciones, los componentes de una aplicación distribuida no se comunican directamente entre sí, sino que intercambian mensajes a través de un tema, que actúa como un intermediario.</span><span class="sxs-lookup"><span data-stu-id="db909-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="db909-111">A diferencia de las colas del Bus de servicio, en las que un solo destinatario procesa cada mensaje, los temas y las suscripciones proporcionan una forma de comunicación de uno a varios mediante un patrón de publicación/suscripción.</span><span class="sxs-lookup"><span data-stu-id="db909-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="db909-112">Es posible registrar varios temas de tooa de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="db909-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="db909-113">Cuando se envía un mensaje tooa tema, luego se convierte en disponible tooeach suscripción toohandle o proceso por separado.</span><span class="sxs-lookup"><span data-stu-id="db909-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="db909-114">Un tema de tooa de suscripción es similar a una cola virtual que recibe copias de mensajes de Hola que se enviaron toohello tema.</span><span class="sxs-lookup"><span data-stu-id="db909-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="db909-115">Si lo desea, puede registrar las reglas de filtro para un tema en una base por suscripción, lo que le permite toofilter/restringir qué tema tooa de mensajes son recibidos por qué suscripciones al tema.</span><span class="sxs-lookup"><span data-stu-id="db909-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="db909-116">Las suscripciones y los temas de Bus de servicio le permiten tooscale tooprocess un gran número de mensajes a través de un gran número de usuarios y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="db909-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="db909-117">Creación de un espacio de nombres de servicio</span><span class="sxs-lookup"><span data-stu-id="db909-117">Create a service namespace</span></span>
<span data-ttu-id="db909-118">toobegin con temas de Bus de servicio y las suscripciones de Azure, primero debe crear un espacio de nombres, que proporciona un contenedor de ámbito para tener acceso a recursos de Bus de servicio dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db909-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="db909-119">toocreate un espacio de nombres:</span><span class="sxs-lookup"><span data-stu-id="db909-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="db909-120">Configurar el Bus de servicio de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="db909-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="db909-121">Asegúrese de que ha instalado hello [Azure SDK para Java] [ Azure SDK for Java] antes de compilar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="db909-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="db909-122">Si está usando Eclipse, puede instalar hello [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse] que incluye hello Azure SDK para Java.</span><span class="sxs-lookup"><span data-stu-id="db909-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="db909-123">A continuación, puede agregar hello **bibliotecas de Microsoft Azure para Java** tooyour proyecto:</span><span class="sxs-lookup"><span data-stu-id="db909-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="db909-124">Agregue los siguiente hello `import` superior de toohello instrucciones Hola del archivo de Java:</span><span class="sxs-lookup"><span data-stu-id="db909-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="db909-125">Agregar Hola bibliotecas de Azure para Java tooyour ruta de acceso de compilación e incluirla en el ensamblado de implementación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="db909-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="db909-126">de un tema</span><span class="sxs-lookup"><span data-stu-id="db909-126">Create a topic</span></span>
<span data-ttu-id="db909-127">Las operaciones de administración para los temas de Service Bus pueden realizarse mediante la clase **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="db909-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="db909-128">A **ServiceBusContract** objeto se construyó con una configuración apropiada que encapsula el token SAS con permisos toomanage y hello **ServiceBusContract** clase es punto único de Hola comunicación con Azure.</span><span class="sxs-lookup"><span data-stu-id="db909-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="db909-129">Hola **ServiceBusService** clase proporciona métodos toocreate, enumerar y eliminar los temas.</span><span class="sxs-lookup"><span data-stu-id="db909-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="db909-130">Hola siguiente ejemplo se muestra cómo un **ServiceBusService** objeto puede ser usado toocreate un tema denominado `TestTopic`, con un espacio de nombres denominado `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="db909-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="db909-131">Hay métodos en **TopicInfo** que habilitar propiedades de tema de hello establecerse (por ejemplo: tooset Hola predeterminado time-to-live (TTL) valor toobe aplica toomessages envía toohello tema).</span><span class="sxs-lookup"><span data-stu-id="db909-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="db909-132">Hello en el ejemplo siguiente se muestra cómo toocreate un tema denominado `TestTopic` con un tamaño máximo de 5 GB:</span><span class="sxs-lookup"><span data-stu-id="db909-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="db909-133">Tenga en cuenta que puede usar hello **listTopics** método **ServiceBusContract** objetos toocheck si ya existe un tema con un nombre especificado dentro de un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="db909-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="db909-134">Creación de suscripciones</span><span class="sxs-lookup"><span data-stu-id="db909-134">Create subscriptions</span></span>
<span data-ttu-id="db909-135">También se crean suscripciones tootopics con hello **ServiceBusService** clase.</span><span class="sxs-lookup"><span data-stu-id="db909-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="db909-136">Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes que se pasan cola virtual de la suscripción de toohello.</span><span class="sxs-lookup"><span data-stu-id="db909-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="db909-137">Crea una suscripción con el filtro de hello predeterminado (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="db909-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="db909-138">Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="db909-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="db909-139">Cuando Hola **MatchAll** filtro se usa, el tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="db909-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="db909-140">Hello en el ejemplo siguiente se crea una suscripción denominada "AllMessages" y usa Hola predeterminado **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="db909-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="db909-141">Creación de suscripciones con filtros</span><span class="sxs-lookup"><span data-stu-id="db909-141">Create subscriptions with filters</span></span>
<span data-ttu-id="db909-142">También puede crear filtros que le permiten tooscope que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción de tema específico.</span><span class="sxs-lookup"><span data-stu-id="db909-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="db909-143">Hola tipo más flexible de filtro compatible con las suscripciones es el [SqlFilter][SqlFilter], que implementa un subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="db909-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="db909-144">Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema.</span><span class="sxs-lookup"><span data-stu-id="db909-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="db909-145">Para obtener más información acerca de las expresiones de Hola que pueden usarse con un filtro SQL, revise hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintaxis.</span><span class="sxs-lookup"><span data-stu-id="db909-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="db909-146">Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un [SqlFilter] [ SqlFilter] objeto que selecciona sólo los mensajes que tienen un personalizado **MessageNumber** propiedad es mayor que 3:</span><span class="sxs-lookup"><span data-stu-id="db909-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="db909-147">De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un [SqlFilter] [ SqlFilter] objeto que selecciona sólo los mensajes que tienen un **MessageNumber** propiedad menor o igual too3:</span><span class="sxs-lookup"><span data-stu-id="db909-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="db909-148">Cuando se envía un mensaje ahora demasiado`TestTopic`, siempre se entregarán tooreceivers suscrito toohello `AllMessages` suscripción y tooreceivers selectivamente entregado suscrito toohello `HighMessages` y `LowMessages` (de suscripciones Dependiendo del contenido del mensaje).</span><span class="sxs-lookup"><span data-stu-id="db909-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="db909-149">Enviar tema tooa de mensajes</span><span class="sxs-lookup"><span data-stu-id="db909-149">Send messages tooa topic</span></span>
<span data-ttu-id="db909-150">toosend un tema de Bus de servicio de tooa de mensaje, la aplicación obtiene un **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="db909-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="db909-151">Hello código siguiente se muestra cómo un mensaje para hello toosend `TestTopic` tema creado previamente en hello `HowToSample` espacio de nombres:</span><span class="sxs-lookup"><span data-stu-id="db909-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="db909-152">Instancias de los mensajes enviados tooService Bus temas son la [BrokeredMessage] [ BrokeredMessage] clase.</span><span class="sxs-lookup"><span data-stu-id="db909-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="db909-153">[BrokeredMessage][BrokeredMessage]* objetos tienen un conjunto de métodos estándar (como **setLabel** y **TimeToLive**), un diccionario que es usado toohold personalizado propiedades específicas de la aplicación y un cuerpo de datos de aplicación arbitrarios.</span><span class="sxs-lookup"><span data-stu-id="db909-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="db909-154">Una aplicación puede establecer el cuerpo de saludo del mensaje pasando cualquier objeto serializable en el constructor de saludo de la [BrokeredMessage][BrokeredMessage], hello adecuado y **DataContractSerializer**  , a continuación, será objeto de Hola de tooserialize usado.</span><span class="sxs-lookup"><span data-stu-id="db909-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="db909-155">También se puede proporcionar un elemento **java.io.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="db909-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="db909-156">Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes toothe `TestTopic` **MessageSender** se obtenido en el fragmento de código de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="db909-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="db909-157">Tenga en cuenta cómo Hola **MessageNumber** valor de propiedad de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determinará qué suscripciones reciban):</span><span class="sxs-lookup"><span data-stu-id="db909-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="db909-158">Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="db909-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="db909-159">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="db909-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="db909-160">No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite de tamaño total de Hola de mensajes de saludo mantenidos por un tema.</span><span class="sxs-lookup"><span data-stu-id="db909-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="db909-161">El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).</span><span class="sxs-lookup"><span data-stu-id="db909-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="db909-162">¿Cómo tooreceive mensajes desde una suscripción</span><span class="sxs-lookup"><span data-stu-id="db909-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="db909-163">mensajes de tooreceive de una suscripción, use un **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="db909-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="db909-164">Los mensajes recibidos pueden funcionar en dos modos distintos: **ReceiveAndDelete** y **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="db909-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="db909-165">Cuando se usa hello **ReceiveAndDelete** modo, de recepción es una operación de captura único: es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje, marca Hola mensaje como consumido y lo devuelve toothe aplicación.</span><span class="sxs-lookup"><span data-stu-id="db909-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="db909-166">**ReceiveAndDelete** modo es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="db909-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="db909-167">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="db909-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="db909-168">Dado que Service Bus habrá marca el mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="db909-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="db909-169">En **PeekLock** , el modo de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="db909-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="db909-170">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="db909-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="db909-171">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a **eliminar** en mensajes de bienvenida recibido.</span><span class="sxs-lookup"><span data-stu-id="db909-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="db909-172">Al Bus de servicio ve hello **eliminar** llamada, se marcar Hola mensaje como consumido y lo quitará de tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="db909-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="db909-173">Hello ejemplo siguiente muestra cómo se pueden recibir mensajes y el uso de procesado **PeekLock** modo (no en el modo de saludo predeterminado).</span><span class="sxs-lookup"><span data-stu-id="db909-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="db909-174">Hello ejemplo siguiente realiza un bucle y procesa los mensajes de Hola "HighMessages" suscripción y, a continuación, se cierra cuando no hay más mensajes (o bien, se puede establecer toowait si hay mensajes nuevos).</span><span class="sxs-lookup"><span data-stu-id="db909-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="db909-175">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="db909-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="db909-176">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="db909-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="db909-177">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello **unlockMessage** método en mensajes de bienvenida recibido (en lugar de hello **deleteMessage** método).</span><span class="sxs-lookup"><span data-stu-id="db909-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="db909-178">Esto provocará el mensaje de saludo toounlock de Bus de servicio dentro de tema de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="db909-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="db909-179">También hay un tiempo de espera asociado con un mensaje bloqueado en el tema, y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes del tiempo de espera de bloqueo expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará automáticamente mensajes de bienvenida y hacerla disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="db909-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="db909-180">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello **deleteMessage** se emite la solicitud, entonces el mensaje de Hola será aplicación toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="db909-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="db909-181">Esto se suele denominar **al menos una vez procesamiento**; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="db909-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="db909-182">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje.</span><span class="sxs-lookup"><span data-stu-id="db909-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="db909-183">A menudo esto se logra utilizando hello **getMessageId** método del mensaje de Hola, que permanece constante entre intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="db909-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="db909-184">Eliminación de temas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="db909-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="db909-185">Hola temas toodelete de modo principal y las suscripciones es toouse una **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="db909-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="db909-186">Eliminar un tema, también se eliminarán las suscripciones que están registradas en el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="db909-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="db909-187">También se pueden eliminar las suscripciones de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="db909-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="db909-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db909-188">Next Steps</span></span>
<span data-ttu-id="db909-189">Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas de Service Bus, temas y suscripciones] [ Service Bus queues, topics, and subscriptions] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="db909-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
