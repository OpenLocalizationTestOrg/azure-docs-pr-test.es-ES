---
title: Registro de eventos en Azure Event Hubs en API Management de Azure
description: "Aprenda a registrar eventos en los centros de eventos de Azure en la administración de API de Azure."
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
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="907da-103">Cómo registrar eventos en los centros de eventos de Azure en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="907da-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="907da-104">Centros de eventos de Azure es un servicio de introducción de datos altamente escalable que permite la introducción de millones de eventos por segundo para que pueda procesar y analizar grandes cantidades de datos generados por los dispositivos y aplicaciones conectados.</span><span class="sxs-lookup"><span data-stu-id="907da-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="907da-105">Centros de eventos actúa como la "puerta principal" de una canalización de eventos y, una vez que los datos se recopilan en un centro de eventos, se pueden transformar y almacenar con cualquier proveedor de análisis en tiempo real o adaptadores de procesamiento por lotes/almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="907da-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="907da-106">Centros de eventos desacopla la producción de un flujo de eventos desde el consumo de los eventos, para que los consumidores de eventos pueden tener acceso a los eventos según su propia programación.</span><span class="sxs-lookup"><span data-stu-id="907da-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="907da-107">Este artículo es un complemento del vídeo [Integración de Administración de API de Azure con centros de eventos](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) y describe cómo registrar eventos de Administración de API mediante centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="907da-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="907da-108">Crear un centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="907da-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="907da-109">Para crear un nuevo centro de eventos, inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com) y haga clic en **Nuevo**->**App Services**->**Service Bus**->**Centro de eventos**->**Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="907da-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="907da-110">Escriba un nombre para el centro de eventos y la región. Seleccione una suscripción y elija un espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="907da-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="907da-111">Si no ha creado previamente un espacio de nombres, puede crear uno escribiendo un nombre en el cuadro de texto **Espacio de nombres**.</span><span class="sxs-lookup"><span data-stu-id="907da-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="907da-112">Una vez configuradas todas las propiedades, haga clic en **Crear un centro de eventos** para crear el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="907da-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Creación de un centro de eventos][create-event-hub]

<span data-ttu-id="907da-114">Luego navegue a la pestaña **Configurar** para el nuevo centro de eventos y cree dos **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="907da-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="907da-115">La primera de ellas se debe llamar **Envío**. Asígnele permisos de **envío**.</span><span class="sxs-lookup"><span data-stu-id="907da-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Directiva de envío][sending-policy]

<span data-ttu-id="907da-117">La segunda de ellas se debe llamar **Recepción**. Asígnele permisos de **escucha** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="907da-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Directiva de recepción][receiving-policy]

<span data-ttu-id="907da-119">Cada directiva de acceso compartido permite a las aplicaciones enviar y recibir eventos desde y hacia el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="907da-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="907da-120">Para obtener acceso a las cadenas de conexión de estas directivas, navegue a la pestaña **Panel** del centro de eventos y haga clic en **Información de conexión**.</span><span class="sxs-lookup"><span data-stu-id="907da-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Cadena de conexión][event-hub-dashboard]

<span data-ttu-id="907da-122">La cadena de conexión **Envío** se usa para registrar eventos, mientras que la cadena de conexión **Recepción** se usa para descargar eventos desde el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="907da-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Cadena de conexión][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="907da-124">Creación de un registrador de administración de API</span><span class="sxs-lookup"><span data-stu-id="907da-124">Create an API Management logger</span></span>
<span data-ttu-id="907da-125">Ahora que tiene un centro de eventos, el siguiente paso es configurar un [registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) en el servicio Administración de API para que se puedan registrar eventos en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="907da-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="907da-126">Los registradores de Administración de API se configuran mediante la [API de REST de Administración de API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="907da-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="907da-127">Antes de usar la API de REST por primera vez, revise los [requisitos previos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) y asegúrese de tener [habilitado el acceso a la API de REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="907da-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="907da-128">Para crear un registrador, efectúe una solicitud HTTP PUT con la siguiente plantilla de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="907da-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="907da-129">Sustituya `{your service}` por el nombre de la instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="907da-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="907da-130">Sustituya `{new logger name}` por el nombre deseado del nuevo registrador.</span><span class="sxs-lookup"><span data-stu-id="907da-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="907da-131">A este nombre se hará referencia al configurar la directiva [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) .</span><span class="sxs-lookup"><span data-stu-id="907da-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="907da-132">Agregue los siguientes encabezados a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="907da-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="907da-133">Content-Type : application/json</span><span class="sxs-lookup"><span data-stu-id="907da-133">Content-Type : application/json</span></span>
* <span data-ttu-id="907da-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="907da-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="907da-135">Para instrucciones sobre cómo generar `SharedAccessSignature` , vea [Autenticación de la API de REST de administración de API de Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="907da-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="907da-136">Especifique el cuerpo de la solicitud utilizando la siguiente plantilla.</span><span class="sxs-lookup"><span data-stu-id="907da-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="907da-137">`type` se debe establecer en `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="907da-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="907da-138">`description` ofrece una descripción opcional del registrador y puede ser una cadena de longitud cero si lo desea.</span><span class="sxs-lookup"><span data-stu-id="907da-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="907da-139">`credentials` contiene el `name` y `connectionString` del centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="907da-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="907da-140">Al realizar la solicitud, si se crea el registrador, se devuelve un código de estado de `201 Created` .</span><span class="sxs-lookup"><span data-stu-id="907da-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="907da-141">Para conocer otros posibles códigos de retorno y sus razones, vea [Creación de un registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="907da-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="907da-142">Para conocer la forma de realizar otras operaciones como crear listas, actualizar y eliminar, vea la documentación de la entidad del [registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) .</span><span class="sxs-lookup"><span data-stu-id="907da-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="907da-143">Configuración de directivas log-to-eventhubs</span><span class="sxs-lookup"><span data-stu-id="907da-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="907da-144">Una vez que el registrador está configurado en la administración de API, puede configurar las directivas de log-to-eventhubs para registrar los eventos oportunos.</span><span class="sxs-lookup"><span data-stu-id="907da-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="907da-145">La directiva log-to-eventhubs puede utilizarse en la sección de las directivas de entrada o de salida.</span><span class="sxs-lookup"><span data-stu-id="907da-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="907da-146">Para configurar las directivas, inicie sesión en [Azure Portal](https://portal.azure.com), acceda al servicio API Management y haga clic en el **portal para editores** para acceder al portal para editores.</span><span class="sxs-lookup"><span data-stu-id="907da-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Portal del publicador][publisher-portal]

<span data-ttu-id="907da-148">Haga clic en **Directivas** en el menú de API Management situado a la izquierda. Seleccione el producto que quiera y la API. Por último, haga clic en **Agregar directiva**.</span><span class="sxs-lookup"><span data-stu-id="907da-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="907da-149">En este ejemplo, vamos a agregar una directiva para la **API Echo** en el producto **Sin límites**.</span><span class="sxs-lookup"><span data-stu-id="907da-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Add policy][add-policy]

<span data-ttu-id="907da-151">Sitúe el cursor en la sección de la directiva de `inbound` y haga clic en la directiva **Registro en el centro de eventos`log-to-eventhub` para insertar la plantilla de declaración de directivas** .</span><span class="sxs-lookup"><span data-stu-id="907da-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="907da-153">Sustituya `logger-id` por el nombre del registrador de administración de API que configuró en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="907da-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="907da-154">Puede usar cualquier expresión que devuelva una cadena como valor para el elemento `log-to-eventhub`.</span><span class="sxs-lookup"><span data-stu-id="907da-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="907da-155">En este ejemplo, se registra una cadena que contiene la fecha y la hora, el nombre de servicio, el Id. de la solicitud, la dirección IP de la solicitud y el nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="907da-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="907da-156">Haga clic en **Guardar** para guardar la configuración de la directiva actualizada.</span><span class="sxs-lookup"><span data-stu-id="907da-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="907da-157">En el momento de guardarla, la directiva se activa y los eventos se registran en el centro de eventos designado.</span><span class="sxs-lookup"><span data-stu-id="907da-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="907da-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="907da-158">Next steps</span></span>
* <span data-ttu-id="907da-159">Obtenga más información acerca de los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="907da-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="907da-160">Introducción a los centros de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="907da-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="907da-161">Recepción de mensajes con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="907da-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="907da-162">Guía de programación de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="907da-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="907da-163">Obtener más información acerca de la integración de Administración de API y centros de eventos</span><span class="sxs-lookup"><span data-stu-id="907da-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="907da-164">Referencia de entidad del registrador</span><span class="sxs-lookup"><span data-stu-id="907da-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="907da-165">referencia de la directiva log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="907da-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="907da-166">Supervisión de API con Administración de API de Azure, Centros de eventos y Runscope</span><span class="sxs-lookup"><span data-stu-id="907da-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="907da-167">Ver un tutorial en vídeo</span><span class="sxs-lookup"><span data-stu-id="907da-167">Watch a video walkthrough</span></span>
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
