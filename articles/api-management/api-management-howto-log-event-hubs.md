---
title: "aaaHow toolog eventos tooAzure concentradores de eventos de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="e6083-103">¿Cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="e6083-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="e6083-104">Centros de eventos de Azure es un servicio de entrada de datos altamente escalable que puede introducir millones de eventos por segundo para que le permitirán procesar y analizar Hola grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e6083-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="e6083-105">Los concentradores de eventos actúa como Hola "puerta principal" para una canalización de eventos, y una vez que se recopilan los datos en un centro de eventos, se pueden transformar y almacenado con cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento y procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="e6083-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="e6083-106">Los concentradores de eventos desacopla producción de hello de una secuencia de eventos de consumo de Hola de esos eventos, para que los consumidores de eventos pueden tener acceso a los eventos de hello en su propia programación.</span><span class="sxs-lookup"><span data-stu-id="e6083-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="e6083-107">Este artículo es una toohello complementaria [integrar la administración de API de Azure con los concentradores de eventos](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vídeo y se describe cómo los eventos de administración de API de toolog con los concentradores de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e6083-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="e6083-108">Crear un centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="e6083-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="e6083-109">un nuevo centro de eventos, inicio de sesión toohello toocreate [portal de Azure clásico](https://manage.windowsazure.com) y haga clic en **New**->**servicios de aplicaciones**->**Bus de servicio**  -> **Concentrador de eventos**->**creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="e6083-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="e6083-110">Escriba un nombre para el centro de eventos y la región. Seleccione una suscripción y elija un espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="e6083-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="e6083-111">Si anteriormente no ha creado un espacio de nombres puede crear uno, escriba un nombre en hello **Namespace** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e6083-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="e6083-112">Una vez configuradas todas las propiedades, haga clic en **crear un nuevo concentrador de eventos** toocreate Hola concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e6083-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Creación de un centro de eventos][create-event-hub]

<span data-ttu-id="e6083-114">A continuación, navegue toohello **configurar** pestaña para el nuevo centro de eventos y cree dos **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="e6083-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="e6083-115">Nombre hello primero **envío** y asígnele **enviar** permisos.</span><span class="sxs-lookup"><span data-stu-id="e6083-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Directiva de envío][sending-policy]

<span data-ttu-id="e6083-117">Nombre hello otra **recibir**, asígnele **escuchar** permisos y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e6083-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Directiva de recepción][receiving-policy]

<span data-ttu-id="e6083-119">Cada directiva de acceso compartido permite que las aplicaciones toosend y recibir eventos tooand de hello concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e6083-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="e6083-120">cadenas de conexión de hello tooaccess para estas directivas, vaya toohello **panel** ficha de hello centro de eventos y haga clic en **información de conexión**.</span><span class="sxs-lookup"><span data-stu-id="e6083-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Cadena de conexión][event-hub-dashboard]

<span data-ttu-id="e6083-122">Hola **envío** cadena de conexión se usa cuando el registro de eventos, hello y **recibir** se utiliza la cadena de conexión al descargar los eventos de hello concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e6083-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Cadena de conexión][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="e6083-124">Creación de un registrador de administración de API</span><span class="sxs-lookup"><span data-stu-id="e6083-124">Create an API Management logger</span></span>
<span data-ttu-id="e6083-125">Ahora que tiene un concentrador de eventos, Hola siguiente paso es tooconfigure una [registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) en la administración de API de servicio para que puedan iniciar eventos toohello concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e6083-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="e6083-126">Registradores de administración de API se configuran mediante hello [API de REST de administración](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="e6083-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="e6083-127">Antes de usar Hola API de REST para hello primera vez, revise hello [requisitos previos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) y asegúrese de que tiene [habilitado acceso toohello API de REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="e6083-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="e6083-128">toocreate un registrador, asegúrese de una solicitud HTTP PUT con hello después de la plantilla de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e6083-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="e6083-129">Reemplace `{your service}` con el nombre de saludo de la instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="e6083-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="e6083-130">Reemplace `{new logger name}` con el nombre elegido hello para el registrador nuevo.</span><span class="sxs-lookup"><span data-stu-id="e6083-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="e6083-131">Se hará referencia a este nombre cuando se configura hello [registro a eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) directiva</span><span class="sxs-lookup"><span data-stu-id="e6083-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="e6083-132">Agregar Hola después encabezados toohello solicitud.</span><span class="sxs-lookup"><span data-stu-id="e6083-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="e6083-133">Content-Type : application/json</span><span class="sxs-lookup"><span data-stu-id="e6083-133">Content-Type : application/json</span></span>
* <span data-ttu-id="e6083-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="e6083-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="e6083-135">Para obtener instrucciones acerca de cómo generar hello `SharedAccessSignature` vea [autenticación de API de REST de administración de API de Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="e6083-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="e6083-136">Especifique el cuerpo de la solicitud de hello mediante Hola después de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e6083-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="e6083-137">`type`debe establecerse demasiado`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="e6083-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="e6083-138">`description`Proporciona una descripción opcional del registrador de Hola y puede ser una cadena de longitud cero si lo desea.</span><span class="sxs-lookup"><span data-stu-id="e6083-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="e6083-139">`credentials`contiene Hola `name` y `connectionString` de su centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e6083-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="e6083-140">Cuando se realiza la solicitud hello, si registrador Hola se crea un código de estado `201 Created` se devuelve.</span><span class="sxs-lookup"><span data-stu-id="e6083-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="e6083-141">Para conocer otros posibles códigos de retorno y sus razones, vea [Creación de un registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="e6083-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="e6083-142">toosee cómo realizan otras operaciones, como la lista, update y delete, vea hello [registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentación de entidad.</span><span class="sxs-lookup"><span data-stu-id="e6083-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="e6083-143">Configuración de directivas log-to-eventhubs</span><span class="sxs-lookup"><span data-stu-id="e6083-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="e6083-144">Una vez que el registrador está configurado en administración de API, puede configurar los eventos de registro para eventhubs directivas toolog Hola deseado.</span><span class="sxs-lookup"><span data-stu-id="e6083-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="e6083-145">Hello registro a eventhubs directiva se puede usar en cualquier Hola sección de directiva de correo entrante o saliente directiva Hola.</span><span class="sxs-lookup"><span data-stu-id="e6083-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="e6083-146">las directivas tooconfigure, inicio de sesión toohello [portal de Azure](https://portal.azure.com), navegar por el servicio de administración de API de tooyour y haga clic en **portal para desarrolladores de** tooaccess Hola portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="e6083-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Portal del publicador][publisher-portal]

<span data-ttu-id="e6083-148">Haga clic en **directivas** en el menú de administración de API de Hola Hola izquierda, seleccione producto deseado hello y API y haga clic en **Agregar directiva**.</span><span class="sxs-lookup"><span data-stu-id="e6083-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="e6083-149">En este ejemplo estamos agregando una directiva toohello **API de eco** en hello **Unlimited** producto.</span><span class="sxs-lookup"><span data-stu-id="e6083-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Add policy][add-policy]

<span data-ttu-id="e6083-151">Coloque el cursor en hello `inbound` directiva de sección y haga clic en hello **registro tooEventHub** hello tooinsert de directiva `log-to-eventhub` plantilla de directiva de instrucción.</span><span class="sxs-lookup"><span data-stu-id="e6083-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="e6083-153">Reemplace `logger-id` con el nombre de Hola de registrador de administración de API de Hola que configuró en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e6083-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="e6083-154">Puede usar cualquier expresión que devuelve una cadena como valor de Hola de hello `log-to-eventhub` elemento.</span><span class="sxs-lookup"><span data-stu-id="e6083-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="e6083-155">En este ejemplo se registra una cadena que contiene Hola fecha y hora, nombre del servicio, Id. de solicitud, dirección ip de solicitud y nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="e6083-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="e6083-156">Haga clic en **guardar** toosave Hola actualiza la configuración de directiva.</span><span class="sxs-lookup"><span data-stu-id="e6083-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="e6083-157">Tan pronto como se guarda Hola directivas estén activas y los eventos son toohello registrado designado concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e6083-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6083-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6083-158">Next steps</span></span>
* <span data-ttu-id="e6083-159">Obtenga más información acerca de los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="e6083-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="e6083-160">Introducción a los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="e6083-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="e6083-161">Recepción de mensajes con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="e6083-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="e6083-162">Guía de programación de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="e6083-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="e6083-163">Obtener más información acerca de la integración de Administración de API y centros de eventos</span><span class="sxs-lookup"><span data-stu-id="e6083-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="e6083-164">Referencia de entidad del registrador</span><span class="sxs-lookup"><span data-stu-id="e6083-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="e6083-165">referencia de la directiva log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="e6083-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="e6083-166">Supervisión de API con Administración de API de Azure, Centros de eventos y Runscope</span><span class="sxs-lookup"><span data-stu-id="e6083-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="e6083-167">Ver un tutorial en vídeo</span><span class="sxs-lookup"><span data-stu-id="e6083-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
