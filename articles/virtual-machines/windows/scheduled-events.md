---
title: "aaaScheduled eventos para máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Eventos programados utilizando el servicio de metadatos de Azure de Hola para en las máquinas virtuales de Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="2116d-103">Servicio Azure Metadata: eventos programados (versión preliminar) para VM Windows</span><span class="sxs-lookup"><span data-stu-id="2116d-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="2116d-104">Las vistas previas se realizan tooyou disponible en condición Hola acepta toohello términos de uso.</span><span class="sxs-lookup"><span data-stu-id="2116d-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="2116d-105">Para obtener más información, consulte [Términos de uso complementarios de las Versiones Preliminares de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="2116d-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="2116d-106">Eventos programados es uno de los subservicios de hello en hello Azure metadatos de servicio.</span><span class="sxs-lookup"><span data-stu-id="2116d-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="2116d-107">Se encarga de mostrar información relacionada con eventos próximos (por ejemplo, un reinicio) para que la aplicación pueda prepararse para ellos y limitar las interrupciones.</span><span class="sxs-lookup"><span data-stu-id="2116d-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="2116d-108">Está disponible para todos los tipos de máquina virtual de Azure, incluso para IaaS y PaaS.</span><span class="sxs-lookup"><span data-stu-id="2116d-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="2116d-109">Eventos programados ofrece a las tareas de máquina Virtual tiempo tooperform preventivas efecto de hello toominimize de un evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="2116d-110">Scheduled Events está disponible para máquinas virtuales Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="2116d-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="2116d-111">Para más información acerca de Scheduled Events en Linux, consulte [Scheduled Events para máquinas virtuales Linux](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="2116d-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="2116d-112">¿Por qué Scheduled Events?</span><span class="sxs-lookup"><span data-stu-id="2116d-112">Why Scheduled Events?</span></span>

<span data-ttu-id="2116d-113">Con los eventos programados, puede tomar medidas impacto de hello toolimit de mantenimiento de la plataforma intiated o las acciones iniciadas por el usuario en su servicio.</span><span class="sxs-lookup"><span data-stu-id="2116d-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="2116d-114">Las cargas de trabajo de varias instancias, que utilizan el estado de replicación técnicas toomaintain, pueden ser vulnerable toooutages sucediendo en varias instancias.</span><span class="sxs-lookup"><span data-stu-id="2116d-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="2116d-115">Esas interrupciones pueden dar lugar a tareas costosas (por ejemplo, volver a elaborar los índices) o, incluso, a una pérdida de las réplicas.</span><span class="sxs-lookup"><span data-stu-id="2116d-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="2116d-116">En muchos casos, hello general disponibilidad del servicio se puede mejorar mediante la realización de una secuencia de cierre como transacciones en curso se completan (o canceladas), reasignar tareas tooother máquinas virtuales en clúster de hello (conmutación por error manual), o quitar Hola Máquina virtual de un grupo de equilibradores de carga de red.</span><span class="sxs-lookup"><span data-stu-id="2116d-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="2116d-117">Hay casos donde notificando a un administrador sobre un evento próximo o registrar un evento de este tipo ayudará a mejorar la capacidad de servicio de Hola de las aplicaciones hospedadas en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="2116d-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="2116d-118">Casos de uso de Azure Metadata Service superficies programado los eventos en los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="2116d-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="2116d-119">Mantenimiento iniciado por la plataforma (por ejemplo, la implementación del SO del host)</span><span class="sxs-lookup"><span data-stu-id="2116d-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="2116d-120">Llamadas iniciadas por el usuario (por ejemplo, si el usuario reinicia una VM o la vuelve a implementar)</span><span class="sxs-lookup"><span data-stu-id="2116d-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="2116d-121">conceptos básicos de Hola</span><span class="sxs-lookup"><span data-stu-id="2116d-121">hello basics</span></span>  

<span data-ttu-id="2116d-122">Servicio de metadatos de Azure expone información acerca de cómo ejecutar máquinas virtuales con un extremo de REST accesible desde dentro de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2116d-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="2116d-123">información de Hello está disponible a través de una dirección IP no enrutables para que no se expone fuera Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2116d-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="2116d-124">Scope</span><span class="sxs-lookup"><span data-stu-id="2116d-124">Scope</span></span>
<span data-ttu-id="2116d-125">Eventos programados son tooall apareció máquinas virtuales en un servicio de nube o tooall máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="2116d-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="2116d-126">Como resultado, debe comprobar hello `Resources` campo Hola evento tooidentify que las máquinas virtuales van toobe afectado.</span><span class="sxs-lookup"><span data-stu-id="2116d-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="2116d-127">Detección de punto de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="2116d-127">Discovering hello endpoint</span></span>
<span data-ttu-id="2116d-128">En el caso de hello donde se crea una máquina Virtual en una red Virtual (VNet), está disponible en una dirección IP no enrutables estática, servicio de metadatos de hello `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="2116d-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="2116d-129">Si Hola Máquina Virtual no se crea dentro de una red Virtual, de los casos Hola predeterminados para los servicios de nube y máquinas virtuales de clásicas, lógica adicional es necesario toodiscover Hola extremo toouse.</span><span class="sxs-lookup"><span data-stu-id="2116d-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="2116d-130">Consulte cómo demasiado toothis ejemplo toolearn[detectar el extremo de host de hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="2116d-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="2116d-131">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="2116d-131">Versioning</span></span> 
<span data-ttu-id="2116d-132">Hola servicio de metadatos de instancia tiene una versión.</span><span class="sxs-lookup"><span data-stu-id="2116d-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="2116d-133">Versiones son obligatorias y la versión actual de hello es `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="2116d-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2116d-134">Versiones anteriores de vista previa de los eventos programados formando Hola api-version {más reciente}.</span><span class="sxs-lookup"><span data-stu-id="2116d-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="2116d-135">Este formato ya no se admite y dejará de utilizarse en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="2116d-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="2116d-136">Uso de encabezados</span><span class="sxs-lookup"><span data-stu-id="2116d-136">Using headers</span></span>
<span data-ttu-id="2116d-137">Al consultar Hola Metadata Service, debe proporcionar encabezado de hello `Metadata: true` solicitud de hello tooensure no se ha redirigido involuntariamente.</span><span class="sxs-lookup"><span data-stu-id="2116d-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="2116d-138">Habilitación de eventos programados</span><span class="sxs-lookup"><span data-stu-id="2116d-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="2116d-139">Hello primera vez que se realiza una solicitud para los eventos programados, Azure implícitamente habilita Hola característica en la máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="2116d-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="2116d-140">Como resultado, debe esperar una respuesta diferida en la primera llamada de seguridad tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="2116d-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="2116d-141">Mantenimiento iniciado por el usuario</span><span class="sxs-lookup"><span data-stu-id="2116d-141">User initiated maintenance</span></span>
<span data-ttu-id="2116d-142">Mantenimiento de máquinas virtuales a través de hello portal de Azure, API, CLI, iniciada por el usuario o PowerShell da como resultado un evento programado.</span><span class="sxs-lookup"><span data-stu-id="2116d-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="2116d-143">Esto le permite lógica de preparación de mantenimiento de tootest hello en la aplicación y permite la tooprepare de aplicación para el mantenimiento iniciada por el usuario.</span><span class="sxs-lookup"><span data-stu-id="2116d-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="2116d-144">Si se reinicia una máquina virtual, se programa un evento con el tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="2116d-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="2116d-145">Si vuelve a implementar una máquina virtual, se programa un evento con el tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="2116d-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2116d-146">Actualmente se puede programar sumultáneamente un máximo de 10 operaciones de mantenimiento iniciadas por el usuario.</span><span class="sxs-lookup"><span data-stu-id="2116d-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="2116d-147">Este límite será más flexible antes de la disponibilidad general de eventos programados.</span><span class="sxs-lookup"><span data-stu-id="2116d-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="2116d-148">Actualmente no se puede configurar ningún mantenimiento iniciado por el usuario que dé lugar a eventos programados.</span><span class="sxs-lookup"><span data-stu-id="2116d-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="2116d-149">Está planeado que esta capacidad de configuración se lance en el futuro.</span><span class="sxs-lookup"><span data-stu-id="2116d-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="2116d-150">Uso de API de Hola</span><span class="sxs-lookup"><span data-stu-id="2116d-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="2116d-151">Consulta de eventos</span><span class="sxs-lookup"><span data-stu-id="2116d-151">Query for events</span></span>
<span data-ttu-id="2116d-152">Puede consultar para los eventos programados basta con realizar Hola siguiente llamada:</span><span class="sxs-lookup"><span data-stu-id="2116d-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="2116d-153">Una respuesta contiene una matriz de eventos programados.</span><span class="sxs-lookup"><span data-stu-id="2116d-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="2116d-154">Una matriz vacía significa que actualmente no hay eventos programados.</span><span class="sxs-lookup"><span data-stu-id="2116d-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="2116d-155">En caso de hello donde hay eventos programados, respuesta de hello contiene una matriz de eventos:</span><span class="sxs-lookup"><span data-stu-id="2116d-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="2116d-156">Propiedades de evento</span><span class="sxs-lookup"><span data-stu-id="2116d-156">Event properties</span></span>
|<span data-ttu-id="2116d-157">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2116d-157">Property</span></span>  |  <span data-ttu-id="2116d-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="2116d-158">Description</span></span> |
| - | - |
| <span data-ttu-id="2116d-159">EventId</span><span class="sxs-lookup"><span data-stu-id="2116d-159">EventId</span></span> | <span data-ttu-id="2116d-160">Es un identificador único global del evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="2116d-161">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2116d-161">Example:</span></span> <br><ul><li><span data-ttu-id="2116d-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="2116d-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="2116d-163">EventType</span><span class="sxs-lookup"><span data-stu-id="2116d-163">EventType</span></span> | <span data-ttu-id="2116d-164">Es el impacto causado por el evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="2116d-165">Valores:</span><span class="sxs-lookup"><span data-stu-id="2116d-165">Values:</span></span> <br><ul><li> <span data-ttu-id="2116d-166">`Freeze`: Hola Máquina Virtual es toopause programada para algunos segundos.</span><span class="sxs-lookup"><span data-stu-id="2116d-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="2116d-167">Hola CPU está suspendido, pero no hay ningún impacto en la memoria, los archivos abiertos o conexiones de red.</span><span class="sxs-lookup"><span data-stu-id="2116d-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="2116d-168">`Reboot`: Hola Máquina Virtual está programada para reiniciar el sistema (memoria no persistente se pierde).</span><span class="sxs-lookup"><span data-stu-id="2116d-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="2116d-169">`Redeploy`: Hola Máquina Virtual está programada toomove tooanother nodo (discos efímeros se pierden).</span><span class="sxs-lookup"><span data-stu-id="2116d-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="2116d-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="2116d-170">ResourceType</span></span> | <span data-ttu-id="2116d-171">Es el tipo de recurso al que afecta este evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="2116d-172">Valores:</span><span class="sxs-lookup"><span data-stu-id="2116d-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="2116d-173">Recursos</span><span class="sxs-lookup"><span data-stu-id="2116d-173">Resources</span></span>| <span data-ttu-id="2116d-174">Es la lista de recursos a la que afecta este evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-174">List of resources this event impacts.</span></span> <span data-ttu-id="2116d-175">Esto se garantiza toocontain máquinas a lo sumo una [Actualizar dominio](manage-availability.md), pero no puede contener todas las máquinas de hello UD.</span><span class="sxs-lookup"><span data-stu-id="2116d-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="2116d-176">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2116d-176">Example:</span></span> <br><ul><li> <span data-ttu-id="2116d-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="2116d-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="2116d-178">Estado de evento</span><span class="sxs-lookup"><span data-stu-id="2116d-178">Event Status</span></span> | <span data-ttu-id="2116d-179">Es el estado de este evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-179">Status of this event.</span></span> <br><br> <span data-ttu-id="2116d-180">Valores:</span><span class="sxs-lookup"><span data-stu-id="2116d-180">Values:</span></span> <ul><li><span data-ttu-id="2116d-181">`Scheduled`: Este evento es toostart programada tarde Hola especificado en hello `NotBefore` propiedad.</span><span class="sxs-lookup"><span data-stu-id="2116d-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="2116d-182">`Started`: este evento se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="2116d-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="2116d-183">Ya no `Completed` o alguna vez se proporciona una situación similar; eventos Hola ya no se devolverá cuando se completa el evento Hola.</span><span class="sxs-lookup"><span data-stu-id="2116d-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="2116d-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="2116d-184">NotBefore</span></span>| <span data-ttu-id="2116d-185">Hora a partir de la que puede iniciarse este evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="2116d-186">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2116d-186">Example:</span></span> <br><ul><li> <span data-ttu-id="2116d-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="2116d-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="2116d-188">Programación de eventos</span><span class="sxs-lookup"><span data-stu-id="2116d-188">Event scheduling</span></span>
<span data-ttu-id="2116d-189">Cada evento se programa una cantidad mínima de tiempo en hello futuras según el tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="2116d-190">Este tiempo se refleja en la propiedad `NotBefore` de un evento.</span><span class="sxs-lookup"><span data-stu-id="2116d-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="2116d-191">EventType</span><span class="sxs-lookup"><span data-stu-id="2116d-191">EventType</span></span>  | <span data-ttu-id="2116d-192">Minimum Notice</span><span class="sxs-lookup"><span data-stu-id="2116d-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="2116d-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="2116d-193">Freeze</span></span>| <span data-ttu-id="2116d-194">15 minutos</span><span class="sxs-lookup"><span data-stu-id="2116d-194">15 minutes</span></span> |
| <span data-ttu-id="2116d-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="2116d-195">Reboot</span></span> | <span data-ttu-id="2116d-196">15 minutos</span><span class="sxs-lookup"><span data-stu-id="2116d-196">15 minutes</span></span> |
| <span data-ttu-id="2116d-197">Volver a implementar</span><span class="sxs-lookup"><span data-stu-id="2116d-197">Redeploy</span></span> | <span data-ttu-id="2116d-198">10 minutos</span><span class="sxs-lookup"><span data-stu-id="2116d-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="2116d-199">Inicio de un evento</span><span class="sxs-lookup"><span data-stu-id="2116d-199">Starting an event</span></span> 

<span data-ttu-id="2116d-200">Una vez haya aprendido de próximos eventos y completado su lógica de cierre correcto, puede aprobar eventos pendientes de hello realizando una `POST` llamar al servicio de metadatos de toohello con hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="2116d-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="2116d-201">Esto indica tooAzure que puede reducir notificación mínima Hola tiempo (cuando sea posible).</span><span class="sxs-lookup"><span data-stu-id="2116d-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="2116d-202">Confirmación de un evento permite Hola evento tooproceed para todos los `Resources` en el caso de hello, no solo Hola máquina virtual que reconoce el evento Hola.</span><span class="sxs-lookup"><span data-stu-id="2116d-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="2116d-203">Por lo tanto, puede elegir tooelect una confirmación de líder toocoordinate hello, que puede ser tan simple como máquina primera Hola Hola `Resources` campo.</span><span class="sxs-lookup"><span data-stu-id="2116d-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="2116d-204">Ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2116d-204">PowerShell sample</span></span> 

<span data-ttu-id="2116d-205">Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.</span><span class="sxs-lookup"><span data-stu-id="2116d-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="2116d-206">Ejemplo de C\#</span><span class="sxs-lookup"><span data-stu-id="2116d-206">C\# sample</span></span> 

<span data-ttu-id="2116d-207">Hello en el ejemplo siguiente es de un cliente que se comunica con el servicio de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2116d-207">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="2116d-208">Eventos programados se pueden representar utilizando Hola siguiendo las estructuras de datos:</span><span class="sxs-lookup"><span data-stu-id="2116d-208">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="2116d-209">Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.</span><span class="sxs-lookup"><span data-stu-id="2116d-209">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="2116d-210">Ejemplo de Python</span><span class="sxs-lookup"><span data-stu-id="2116d-210">Python sample</span></span> 

<span data-ttu-id="2116d-211">Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.</span><span class="sxs-lookup"><span data-stu-id="2116d-211">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="2116d-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2116d-212">Next steps</span></span> 

- <span data-ttu-id="2116d-213">Obtener más información acerca de la API a disposición de Hola Hola [servicio de metadatos de la instancia](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="2116d-213">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="2116d-214">Obtenga información sobre cómo realizar [el mantenimiento planeado para máquinas virtuales Windows en Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="2116d-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

