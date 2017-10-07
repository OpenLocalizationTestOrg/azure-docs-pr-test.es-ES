---
title: "información general de cuadrícula de eventos de aaaAzure"
description: Describe Azure Event Grid y sus conceptos.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="a4be1-103">Una cuadrícula de eventos de tooAzure de introducción</span><span class="sxs-lookup"><span data-stu-id="a4be1-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="a4be1-104">Cuadrícula de eventos de Azure permite tooeasily crear aplicaciones con las arquitecturas basadas en eventos.</span><span class="sxs-lookup"><span data-stu-id="a4be1-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="a4be1-105">Seleccione Hola recursos de Azure que desee toosubscribe a y proporcionar un controlador de eventos de Hola o WebHook extremo toosend Hola evento.</span><span class="sxs-lookup"><span data-stu-id="a4be1-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="a4be1-106">Event Grid tiene compatibilidad integrada para eventos procedentes de los servicios de Azure, como los blobs de almacenamiento y los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4be1-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="a4be1-107">Event Grid también tiene soporte personalizado para aplicaciones y eventos de otros fabricantes, con temas personalizados y webhooks personalizados.</span><span class="sxs-lookup"><span data-stu-id="a4be1-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="a4be1-108">Puede usar filtros tooroute eventos específicos toodifferent puntos de conexión, los puntos de conexión de multidifusión toomultiple y asegúrese de que los eventos se entregan de forma confiable.</span><span class="sxs-lookup"><span data-stu-id="a4be1-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="a4be1-109">Event Grid también tiene compatibilidad integrada para eventos personalizados y de terceros.</span><span class="sxs-lookup"><span data-stu-id="a4be1-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="a4be1-110">Para la versión de vista previa de hello, admite la cuadrícula de eventos **westus2** y **westcentralus** ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="a4be1-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="a4be1-111">Se agregarán otras regiones.</span><span class="sxs-lookup"><span data-stu-id="a4be1-111">Other regions will be added.</span></span>

<span data-ttu-id="a4be1-112">Este artículo ofrece información general sobre Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="a4be1-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="a4be1-113">Si desea que tooget a trabajar con la cuadrícula de eventos, vea [ruta y crear eventos personalizados con la cuadrícula de eventos de Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="a4be1-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Modelo funcional de Event Grid](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="a4be1-115">Actualmente, Blob Storage no está disponible públicamente como publicador.</span><span class="sxs-lookup"><span data-stu-id="a4be1-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="a4be1-116">Conceptos</span><span class="sxs-lookup"><span data-stu-id="a4be1-116">Concepts</span></span>

<span data-ttu-id="a4be1-117">Hay cinco conceptos en Azure Event Grid que le permiten empezar a trabajar:</span><span class="sxs-lookup"><span data-stu-id="a4be1-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="a4be1-118">**Eventos**: ¿qué ha ocurrido?</span><span class="sxs-lookup"><span data-stu-id="a4be1-118">**Events** - What happened.</span></span>
* <span data-ttu-id="a4be1-119">**Orígenes de eventos/publicadores** : si se ha producido el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4be1-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="a4be1-120">**Temas** -Hola donde publicadores envían eventos de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="a4be1-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="a4be1-121">**Suscripciones a eventos** -eventos de tooroute de mecanismo de punto de conexión o integradas hello, a veces toomultiple controladores.</span><span class="sxs-lookup"><span data-stu-id="a4be1-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="a4be1-122">También se utilizan suscripciones de eventos de entrada de filtro de toointelligently de controladores.</span><span class="sxs-lookup"><span data-stu-id="a4be1-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="a4be1-123">**Controladores de eventos** : Hola aplicación o servicio reaccionando eventos toohello.</span><span class="sxs-lookup"><span data-stu-id="a4be1-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="a4be1-124">Para más información acerca de estos conceptos, consulte [Conceptos en Azure Event Grid](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a4be1-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="a4be1-125">Capacidades</span><span class="sxs-lookup"><span data-stu-id="a4be1-125">Capabilities</span></span>

<span data-ttu-id="a4be1-126">Estas son algunas de las principales características de Hola de cuadrícula de eventos de Azure:</span><span class="sxs-lookup"><span data-stu-id="a4be1-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="a4be1-127">**Simplicidad** -punto y haga clic en eventos de tooaim del controlador de eventos de tooany de recursos de Azure o el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="a4be1-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="a4be1-128">**Filtrado avanzado** -filtro de evento tooensure de ruta de acceso de publicación de evento o tipo de controladores de eventos sólo reciban los eventos relevantes.</span><span class="sxs-lookup"><span data-stu-id="a4be1-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="a4be1-129">**Distribución ramificada** -suscribirse toohello de varios puntos de conexión mismo toosend de eventos copia de hello eventos tooas muchos lugares según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a4be1-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="a4be1-130">**Confiabilidad** -utilizar reintento de 24 horas con tooensure de retroceso exponencial se entregan eventos.</span><span class="sxs-lookup"><span data-stu-id="a4be1-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="a4be1-131">**Pago por evento** : paga solo para la cantidad de hello utilizar cuadrícula de eventos.</span><span class="sxs-lookup"><span data-stu-id="a4be1-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="a4be1-132">**Alto rendimiento**: cree cargas de trabajo de gran volumen en Event Grid con soporte para millones de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="a4be1-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="a4be1-133">**Eventos integrados**: desarrolle y ejecute rápidamente con eventos integrados definidos por el recurso.</span><span class="sxs-lookup"><span data-stu-id="a4be1-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="a4be1-134">**Eventos personalizados**: use la ruta, el filtrado y la entrega confiable de eventos personalizados de Event Grid en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a4be1-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="a4be1-135">Integración incorporada del publicador y el controlador</span><span class="sxs-lookup"><span data-stu-id="a4be1-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="a4be1-136">Azure ofrece compatibilidad de eventos integrada con numerosos servicios, incluidos tanto publicadores como controladores.</span><span class="sxs-lookup"><span data-stu-id="a4be1-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="a4be1-137">Publicadores</span><span class="sxs-lookup"><span data-stu-id="a4be1-137">Publishers</span></span>

<span data-ttu-id="a4be1-138">Actualmente, hello servicios de Azure siguientes tienen publicador integrada compatibilidad con la cuadrícula de eventos:</span><span class="sxs-lookup"><span data-stu-id="a4be1-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="a4be1-139">Grupos de recursos (operaciones de administración)</span><span class="sxs-lookup"><span data-stu-id="a4be1-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="a4be1-140">Suscripciones de Azure (operaciones de administración)</span><span class="sxs-lookup"><span data-stu-id="a4be1-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="a4be1-141">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="a4be1-141">Event Hubs</span></span>
* <span data-ttu-id="a4be1-142">Temas personalizados</span><span class="sxs-lookup"><span data-stu-id="a4be1-142">Custom Topics</span></span>

<span data-ttu-id="a4be1-143">Otros servicios de Azure se agregarán este año.</span><span class="sxs-lookup"><span data-stu-id="a4be1-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="a4be1-144">Controladores</span><span class="sxs-lookup"><span data-stu-id="a4be1-144">Handlers</span></span>

<span data-ttu-id="a4be1-145">Actualmente, hello servicios de Azure siguientes tienen controlador integrados compatibilidad con la cuadrícula de eventos:</span><span class="sxs-lookup"><span data-stu-id="a4be1-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="a4be1-146">Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a4be1-146">Azure Functions</span></span>
* <span data-ttu-id="a4be1-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a4be1-147">Logic Apps</span></span>
* <span data-ttu-id="a4be1-148">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="a4be1-148">Azure Automation</span></span>
* <span data-ttu-id="a4be1-149">WebHooks</span><span class="sxs-lookup"><span data-stu-id="a4be1-149">WebHooks</span></span>

<span data-ttu-id="a4be1-150">Otros servicios de Azure se agregarán este año.</span><span class="sxs-lookup"><span data-stu-id="a4be1-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="a4be1-151">¿Qué puedo hacer con Event Grid?</span><span class="sxs-lookup"><span data-stu-id="a4be1-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="a4be1-152">Azure Event Grid proporciona varias funcionalidades que mejoran considerablemente el trabajo sin servidor, la automatización de operaciones y la integración:</span><span class="sxs-lookup"><span data-stu-id="a4be1-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="a4be1-153">Arquitecturas de aplicación sin servidor</span><span class="sxs-lookup"><span data-stu-id="a4be1-153">Serverless application architectures</span></span>

![Aplicación sin servidor](./media/overview/serverless_web_app.png)

<span data-ttu-id="a4be1-155">Event Grid conecta orígenes de datos y controladores de eventos.</span><span class="sxs-lookup"><span data-stu-id="a4be1-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="a4be1-156">Por ejemplo, usar un análisis de imágenes de toorun de función sin servidor cada vez que una nueva foto agrega contenedor de almacenamiento de blobs de tooa desencadenador tooinstantly de cuadrícula de eventos.</span><span class="sxs-lookup"><span data-stu-id="a4be1-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="a4be1-157">Automatización de operaciones</span><span class="sxs-lookup"><span data-stu-id="a4be1-157">Ops Automation</span></span>

![Automatización de operaciones](./media/overview/Ops_automation.png)

<span data-ttu-id="a4be1-159">Cuadrícula de eventos permite la automatización de toospeed y simplificar el cumplimiento de directivas.</span><span class="sxs-lookup"><span data-stu-id="a4be1-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="a4be1-160">Por ejemplo, Event Grid puede enviar una notificación a Azure Automation cuando se crea una máquina virtual o cuando se pone en marcha una instancia de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4be1-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="a4be1-161">Estos eventos se pueden utilizar tooautomatically Compruebe que las configuraciones de servicio son compatibles, poner metadatos en herramientas de operations, máquinas virtuales de etiqueta o elementos de trabajo de archivo.</span><span class="sxs-lookup"><span data-stu-id="a4be1-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="a4be1-162">Integración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a4be1-162">Application integration</span></span>

![Integración de aplicaciones](./media/overview/app_integration.png)

<span data-ttu-id="a4be1-164">Event Grid conecta su aplicación con otros servicios.</span><span class="sxs-lookup"><span data-stu-id="a4be1-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="a4be1-165">Por ejemplo, puede crear un tema personalizado toosend tooEvent de datos de eventos de la aplicación cuadrícula y aprovechar las ventajas de su entrega confiable, avanzada de enrutamiento y la integración directa con Azure.</span><span class="sxs-lookup"><span data-stu-id="a4be1-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="a4be1-166">Como alternativa, puede usar la cuadrícula de eventos con datos en cualquier parte, de las aplicaciones lógicas tooprocess sin escribir código.</span><span class="sxs-lookup"><span data-stu-id="a4be1-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="a4be1-167">¿En qué se diferencia Event Grid de otros servicios de integración de Azure?</span><span class="sxs-lookup"><span data-stu-id="a4be1-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="a4be1-168">Event Grid es un panel posterior de eventos que habilita la programación orientada a eventos y reactiva.</span><span class="sxs-lookup"><span data-stu-id="a4be1-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="a4be1-169">Está totalmente integrado con los servicios de Azure y puede integrarse con servicios de terceros.</span><span class="sxs-lookup"><span data-stu-id="a4be1-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="a4be1-170">mensajes de bienvenida del evento contiene información de Hola que necesita tooreact toochanges en aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="a4be1-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="a4be1-171">Cuadrícula de eventos no es una canalización de datos y no entrega objeto real Hola que se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="a4be1-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="a4be1-172">Service Bus se adapta perfectamente a aplicaciones empresariales tradicionales que requieren transacciones, ordenación, detección de duplicados y coherencia inmediata.</span><span class="sxs-lookup"><span data-stu-id="a4be1-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="a4be1-173">Event Grid está diseñado para la velocidad, la escala, la amplitud y el bajo costo en un modelo reactivo.</span><span class="sxs-lookup"><span data-stu-id="a4be1-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="a4be1-174">Resulta idóneo tooserverless arquitectura.</span><span class="sxs-lookup"><span data-stu-id="a4be1-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="a4be1-175">Event Grid complementa otros servicios de Azure como Logic Apps y Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="a4be1-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="a4be1-176">Desencadenadores de la cuadrícula de eventos Hola toobegin de aplicación lógica de su flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a4be1-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="a4be1-177">Los concentradores de eventos funciona con cuadrícula de eventos, permitiéndole tooreact tooevents de captura de los centros de eventos y canalizaciones de entrada y de transformación de datos de compilación.</span><span class="sxs-lookup"><span data-stu-id="a4be1-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="a4be1-178">¿Cuánto cuesta Event Grid?</span><span class="sxs-lookup"><span data-stu-id="a4be1-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="a4be1-179">Azure Event Grid usa un modelo de precios de pago por evento, por lo que solo se paga por lo que usa.</span><span class="sxs-lookup"><span data-stu-id="a4be1-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="a4be1-180">Cuadrícula de eventos cuesta 0,60 $ por cada millón de operaciones (0,30 USD durante la vista previa) y Hola primero 100.000 operación al mes son gratuitas.</span><span class="sxs-lookup"><span data-stu-id="a4be1-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="a4be1-181">Estas operaciones se definen como eventos de entrada, coincidencia avanzada, intentos de entrega y llamadas de administración.</span><span class="sxs-lookup"><span data-stu-id="a4be1-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="a4be1-182">Pueden encontrar más detalles en hello [página de precios](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="a4be1-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4be1-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4be1-183">Next steps</span></span>

* <span data-ttu-id="a4be1-184">[Crear y suscribirse a eventos toocustom](custom-event-quickstart.md) comenzar de inmediato y empezar a enviar su propio punto de conexión de tooany de eventos personalizados mediante Inicio rápido de hello cuadrícula de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4be1-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="a4be1-185">[Con las aplicaciones lógicas como un controlador de eventos](monitor-virtual-machine-changes-event-grid-logic-app.md) un tutorial sobre la creación de una aplicación con las aplicaciones lógicas tooreact tooevents inserta con cuadrícula de eventos.</span><span class="sxs-lookup"><span data-stu-id="a4be1-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="a4be1-186">Referencia de la API de REST de Event Grid</span><span class="sxs-lookup"><span data-stu-id="a4be1-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="a4be1-187">Proporciona información más técnica sobre Hola cuadrícula de eventos de Azure y una referencia para administrar suscripciones a eventos, enrutamiento y filtrado.</span><span class="sxs-lookup"><span data-stu-id="a4be1-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
