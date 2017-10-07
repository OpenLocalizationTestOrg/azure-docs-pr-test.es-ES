---
title: aaaScheduled eventos con el servicio de metadatos de Azure | Documentos de Microsoft
description: "Reaccionar tooImpactful eventos en la máquina Virtual antes de que ocurran."
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
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="a3b47-103">Azure Metadata Service: eventos programados (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="a3b47-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="a3b47-104">Las vistas previas se realizan tooyou disponible en condición Hola acepta toohello términos de uso.</span><span class="sxs-lookup"><span data-stu-id="a3b47-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="a3b47-105">Para obtener más información, consulte [Términos de uso complementarios de las Versiones Preliminares de Microsoft Azure](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="a3b47-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="a3b47-106">Eventos programados es uno de los subservicios de hello en hello Azure metadatos de servicio.</span><span class="sxs-lookup"><span data-stu-id="a3b47-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="a3b47-107">Se encarga de mostrar información relacionada con eventos próximos (por ejemplo, un reinicio) para que la aplicación pueda prepararse para ellos y limitar las interrupciones.</span><span class="sxs-lookup"><span data-stu-id="a3b47-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="a3b47-108">Está disponible para todos los tipos de máquina virtual de Azure, incluso para IaaS y PaaS.</span><span class="sxs-lookup"><span data-stu-id="a3b47-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="a3b47-109">Eventos programados ofrece a las tareas de máquina Virtual tiempo tooperform preventivas efecto de hello toominimize de un evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="a3b47-110">Introducción: ¿Por qué Eventos programados?</span><span class="sxs-lookup"><span data-stu-id="a3b47-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="a3b47-111">Con los eventos programados, puede tomar medidas impacto de hello toolimit de mantenimiento de la plataforma intiated o las acciones iniciadas por el usuario en su servicio.</span><span class="sxs-lookup"><span data-stu-id="a3b47-111">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="a3b47-112">Las cargas de trabajo de varias instancias, que utilizan el estado de replicación técnicas toomaintain, pueden ser vulnerable toooutages sucediendo en varias instancias.</span><span class="sxs-lookup"><span data-stu-id="a3b47-112">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="a3b47-113">Esas interrupciones pueden dar lugar a tareas costosas (por ejemplo, volver a elaborar los índices) o, incluso, a una pérdida de las réplicas.</span><span class="sxs-lookup"><span data-stu-id="a3b47-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="a3b47-114">En muchos casos, hello general disponibilidad del servicio se puede mejorar mediante la realización de una secuencia de cierre como transacciones en curso se completan (o canceladas), reasignar tareas tooother máquinas virtuales en clúster de hello (conmutación por error manual), o quitar Hola Máquina virtual de un grupo de equilibradores de carga de red.</span><span class="sxs-lookup"><span data-stu-id="a3b47-114">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="a3b47-115">Hay casos donde notificando a un administrador sobre un evento próximo o registrar un evento de este tipo ayudará a mejorar la capacidad de servicio de Hola de las aplicaciones hospedadas en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3b47-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="a3b47-116">Casos de uso de Azure Metadata Service superficies programado los eventos en los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="a3b47-116">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="a3b47-117">Mantenimiento iniciado por la plataforma (por ejemplo, la implementación del SO del host)</span><span class="sxs-lookup"><span data-stu-id="a3b47-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="a3b47-118">Llamadas iniciadas por el usuario (por ejemplo, si el usuario reinicia una VM o la vuelve a implementar)</span><span class="sxs-lookup"><span data-stu-id="a3b47-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---hello-basics"></a><span data-ttu-id="a3b47-119">Eventos programados - Hola conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="a3b47-119">Scheduled Events - hello Basics</span></span>  

<span data-ttu-id="a3b47-120">Servicio de metadatos de Azure expone información acerca de cómo ejecutar máquinas virtuales con un extremo de REST accesible desde dentro de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3b47-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="a3b47-121">información de Hello está disponible a través de una dirección IP no enrutables para que no se expone fuera Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3b47-121">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="a3b47-122">Scope</span><span class="sxs-lookup"><span data-stu-id="a3b47-122">Scope</span></span>
<span data-ttu-id="a3b47-123">Eventos programados son tooall apareció máquinas virtuales en un servicio de nube o tooall máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="a3b47-123">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="a3b47-124">Como resultado, debe comprobar hello `Resources` campo Hola evento tooidentify que las máquinas virtuales van toobe afectado.</span><span class="sxs-lookup"><span data-stu-id="a3b47-124">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="a3b47-125">Punto de conexión de detección Hola</span><span class="sxs-lookup"><span data-stu-id="a3b47-125">Discovering hello Endpoint</span></span>
<span data-ttu-id="a3b47-126">En el caso de hello donde se crea una máquina Virtual en una red Virtual (VNet), está disponible en una dirección IP no enrutables estática, servicio de metadatos de hello `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="a3b47-126">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="a3b47-127">Si Hola Máquina Virtual no se crea dentro de una red Virtual, de los casos Hola predeterminados para los servicios de nube y máquinas virtuales de clásicas, lógica adicional es necesario toodiscover Hola extremo toouse.</span><span class="sxs-lookup"><span data-stu-id="a3b47-127">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="a3b47-128">Consulte cómo demasiado toothis ejemplo toolearn[detectar el extremo de host de hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="a3b47-128">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="a3b47-129">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="a3b47-129">Versioning</span></span> 
<span data-ttu-id="a3b47-130">Hola servicio de metadatos de instancia tiene una versión.</span><span class="sxs-lookup"><span data-stu-id="a3b47-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="a3b47-131">Versiones son obligatorias y la versión actual de hello es `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="a3b47-131">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="a3b47-132">Versiones anteriores de vista previa de los eventos programados formando Hola api-version {más reciente}.</span><span class="sxs-lookup"><span data-stu-id="a3b47-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="a3b47-133">Este formato ya no se admite y dejará de utilizarse en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="a3b47-133">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="a3b47-134">Uso de encabezados</span><span class="sxs-lookup"><span data-stu-id="a3b47-134">Using Headers</span></span>
<span data-ttu-id="a3b47-135">Al consultar Hola Metadata Service, debe proporcionar encabezado de hello `Metadata: true` solicitud de hello tooensure no se ha redirigido involuntariamente.</span><span class="sxs-lookup"><span data-stu-id="a3b47-135">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="a3b47-136">Habilitación de eventos programados</span><span class="sxs-lookup"><span data-stu-id="a3b47-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="a3b47-137">Hello primera vez que se realiza una solicitud para los eventos programados, Azure implícitamente habilita Hola característica en la máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="a3b47-137">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="a3b47-138">Como resultado, debe esperar una respuesta diferida en la primera llamada de seguridad tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="a3b47-138">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="a3b47-139">Mantenimiento iniciado por el usuario</span><span class="sxs-lookup"><span data-stu-id="a3b47-139">User Initiated Maintenance</span></span>
<span data-ttu-id="a3b47-140">Mantenimiento de máquinas virtuales a través de hello portal de Azure, API, CLI, iniciada por el usuario o PowerShell, se producirá en los eventos programados.</span><span class="sxs-lookup"><span data-stu-id="a3b47-140">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="a3b47-141">Esto le permite lógica de preparación de mantenimiento de tootest hello en la aplicación y permite la tooprepare de aplicación para el mantenimiento iniciada por el usuario.</span><span class="sxs-lookup"><span data-stu-id="a3b47-141">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="a3b47-142">Si se reinicia una máquina virtual, se programará un evento con el tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="a3b47-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="a3b47-143">Si se vuelve a implementar una máquina virtual, se programará un evento con el tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="a3b47-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="a3b47-144">Actualmente se puede programar sumultáneamente un máximo de 10 operaciones de mantenimiento iniciadas por el usuario.</span><span class="sxs-lookup"><span data-stu-id="a3b47-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="a3b47-145">Este límite será más flexible antes de la disponibilidad general de eventos programados.</span><span class="sxs-lookup"><span data-stu-id="a3b47-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="a3b47-146">Actualmente no se puede configurar ningún mantenimiento iniciado por el usuario que dé lugar a eventos programados.</span><span class="sxs-lookup"><span data-stu-id="a3b47-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="a3b47-147">Está planeado que esta capacidad de configuración se lance en el futuro.</span><span class="sxs-lookup"><span data-stu-id="a3b47-147">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="a3b47-148">Uso de API de Hola</span><span class="sxs-lookup"><span data-stu-id="a3b47-148">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="a3b47-149">Consulta de eventos</span><span class="sxs-lookup"><span data-stu-id="a3b47-149">Query for events</span></span>
<span data-ttu-id="a3b47-150">Puede consultar para los eventos programados basta con realizar Hola siguiente llamada:</span><span class="sxs-lookup"><span data-stu-id="a3b47-150">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="a3b47-151">Una respuesta contiene una matriz de eventos programados.</span><span class="sxs-lookup"><span data-stu-id="a3b47-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="a3b47-152">Una matriz vacía significa que actualmente no hay eventos programados.</span><span class="sxs-lookup"><span data-stu-id="a3b47-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="a3b47-153">En caso de hello donde hay eventos programados, respuesta de hello contiene una matriz de eventos:</span><span class="sxs-lookup"><span data-stu-id="a3b47-153">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="a3b47-154">Propiedades de evento</span><span class="sxs-lookup"><span data-stu-id="a3b47-154">Event Properties</span></span>
|<span data-ttu-id="a3b47-155">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a3b47-155">Property</span></span>  |  <span data-ttu-id="a3b47-156">Descripción</span><span class="sxs-lookup"><span data-stu-id="a3b47-156">Description</span></span> |
| - | - |
| <span data-ttu-id="a3b47-157">EventId</span><span class="sxs-lookup"><span data-stu-id="a3b47-157">EventId</span></span> | <span data-ttu-id="a3b47-158">Es un identificador único global del evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="a3b47-159">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a3b47-159">Example:</span></span> <br><ul><li><span data-ttu-id="a3b47-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="a3b47-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="a3b47-161">EventType</span><span class="sxs-lookup"><span data-stu-id="a3b47-161">EventType</span></span> | <span data-ttu-id="a3b47-162">Es el impacto causado por el evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="a3b47-163">Valores:</span><span class="sxs-lookup"><span data-stu-id="a3b47-163">Values:</span></span> <br><ul><li> <span data-ttu-id="a3b47-164">`Freeze`: Hola Máquina Virtual es toopause programada para algunos segundos.</span><span class="sxs-lookup"><span data-stu-id="a3b47-164">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="a3b47-165">Hola CPU se suspenderá, pero no hay ningún impacto en la memoria, los archivos abiertos o conexiones de red.</span><span class="sxs-lookup"><span data-stu-id="a3b47-165">hello CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="a3b47-166">`Reboot`: Hola Máquina Virtual está programada para reiniciar el sistema (memoria no persistente se pierde).</span><span class="sxs-lookup"><span data-stu-id="a3b47-166">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="a3b47-167">`Redeploy`: Hola Máquina Virtual está programada toomove tooanother nodo (discos efímeros se pierden).</span><span class="sxs-lookup"><span data-stu-id="a3b47-167">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="a3b47-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="a3b47-168">ResourceType</span></span> | <span data-ttu-id="a3b47-169">Es el tipo de recurso al que afecta este evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="a3b47-170">Valores:</span><span class="sxs-lookup"><span data-stu-id="a3b47-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="a3b47-171">Recursos</span><span class="sxs-lookup"><span data-stu-id="a3b47-171">Resources</span></span>| <span data-ttu-id="a3b47-172">Es la lista de recursos a la que afecta este evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-172">List of resources this event impacts.</span></span> <span data-ttu-id="a3b47-173">Esto se garantiza toocontain máquinas a lo sumo una [Actualizar dominio](windows/manage-availability.md), pero no puede contener todas las máquinas de hello UD.</span><span class="sxs-lookup"><span data-stu-id="a3b47-173">This is guaranteed toocontain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="a3b47-174">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a3b47-174">Example:</span></span> <br><ul><li> <span data-ttu-id="a3b47-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="a3b47-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="a3b47-176">Estado de evento</span><span class="sxs-lookup"><span data-stu-id="a3b47-176">Event Status</span></span> | <span data-ttu-id="a3b47-177">Es el estado de este evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-177">Status of this event.</span></span> <br><br> <span data-ttu-id="a3b47-178">Valores:</span><span class="sxs-lookup"><span data-stu-id="a3b47-178">Values:</span></span> <ul><li><span data-ttu-id="a3b47-179">`Scheduled`: Este evento es toostart programada tarde Hola especificado en hello `NotBefore` propiedad.</span><span class="sxs-lookup"><span data-stu-id="a3b47-179">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="a3b47-180">`Started`: este evento se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="a3b47-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="a3b47-181">Ya no `Completed` o alguna vez se proporciona una situación similar; eventos Hola ya no se devolverá cuando se completa el evento Hola.</span><span class="sxs-lookup"><span data-stu-id="a3b47-181">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="a3b47-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="a3b47-182">NotBefore</span></span>| <span data-ttu-id="a3b47-183">Hora a partir de la que puede iniciarse este evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="a3b47-184">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a3b47-184">Example:</span></span> <br><ul><li> <span data-ttu-id="a3b47-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="a3b47-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="a3b47-186">Programación de eventos</span><span class="sxs-lookup"><span data-stu-id="a3b47-186">Event Scheduling</span></span>
<span data-ttu-id="a3b47-187">Cada evento se programa una cantidad mínima de tiempo en hello futuras según el tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-187">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="a3b47-188">Este tiempo se refleja en la propiedad `NotBefore` de un evento.</span><span class="sxs-lookup"><span data-stu-id="a3b47-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="a3b47-189">EventType</span><span class="sxs-lookup"><span data-stu-id="a3b47-189">EventType</span></span>  | <span data-ttu-id="a3b47-190">Minimum Notice</span><span class="sxs-lookup"><span data-stu-id="a3b47-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="a3b47-191">Freeze</span><span class="sxs-lookup"><span data-stu-id="a3b47-191">Freeze</span></span>| <span data-ttu-id="a3b47-192">15 minutos</span><span class="sxs-lookup"><span data-stu-id="a3b47-192">15 minutes</span></span> |
| <span data-ttu-id="a3b47-193">Reboot</span><span class="sxs-lookup"><span data-stu-id="a3b47-193">Reboot</span></span> | <span data-ttu-id="a3b47-194">15 minutos</span><span class="sxs-lookup"><span data-stu-id="a3b47-194">15 minutes</span></span> |
| <span data-ttu-id="a3b47-195">Volver a implementar</span><span class="sxs-lookup"><span data-stu-id="a3b47-195">Redeploy</span></span> | <span data-ttu-id="a3b47-196">10 minutos</span><span class="sxs-lookup"><span data-stu-id="a3b47-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="a3b47-197">Inicio de un evento (acelerar)</span><span class="sxs-lookup"><span data-stu-id="a3b47-197">Starting an event (expedite)</span></span>

<span data-ttu-id="a3b47-198">Una vez haya aprendido de próximos eventos y completado su lógica de cierre correcto, puede aprobar eventos pendientes de hello realizando una `POST` llamar al servicio de metadatos de toohello con hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="a3b47-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="a3b47-199">Esto indica tooAzure que puede reducir notificación mínima Hola tiempo (cuando sea posible).</span><span class="sxs-lookup"><span data-stu-id="a3b47-199">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="a3b47-200">Confirmación de un evento permitirá Hola evento tooproceed para todos los `Resources` en el caso de hello, no solo Hola máquina virtual que reconoce el evento Hola.</span><span class="sxs-lookup"><span data-stu-id="a3b47-200">Acknowledging a event will allow hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="a3b47-201">Por lo tanto, puede elegir tooelect una confirmación de líder toocoordinate hello, que puede ser tan simple como máquina primera Hola Hola `Resources` campo.</span><span class="sxs-lookup"><span data-stu-id="a3b47-201">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="a3b47-202">Muestras</span><span class="sxs-lookup"><span data-stu-id="a3b47-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="a3b47-203">Ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3b47-203">PowerShell Sample</span></span> 

<span data-ttu-id="a3b47-204">Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.</span><span class="sxs-lookup"><span data-stu-id="a3b47-204">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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


### <a name="c-sample"></a><span data-ttu-id="a3b47-205">Ejemplo de C\#</span><span class="sxs-lookup"><span data-stu-id="a3b47-205">C\# Sample</span></span> 

<span data-ttu-id="a3b47-206">Hello en el ejemplo siguiente es de un cliente que se comunica con el servicio de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3b47-206">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

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

<span data-ttu-id="a3b47-207">Eventos programados se pueden representar utilizando Hola siguiendo las estructuras de datos:</span><span class="sxs-lookup"><span data-stu-id="a3b47-207">Scheduled Events can be represented using hello following data structures:</span></span>

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

<span data-ttu-id="a3b47-208">Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.</span><span class="sxs-lookup"><span data-stu-id="a3b47-208">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

### <a name="python-sample"></a><span data-ttu-id="a3b47-209">Ejemplo de Python</span><span class="sxs-lookup"><span data-stu-id="a3b47-209">Python Sample</span></span> 

<span data-ttu-id="a3b47-210">Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.</span><span class="sxs-lookup"><span data-stu-id="a3b47-210">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a3b47-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3b47-211">Next Steps</span></span> 

- <span data-ttu-id="a3b47-212">Obtener más información acerca de la API a disposición de Hola Hola [servicio de metadatos de instancia](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3b47-212">Read more about hello APIs available in hello [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="a3b47-213">Obtenga información sobre cómo realizar [el mantenimiento planeado para máquinas virtuales Windows en Azure](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="a3b47-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="a3b47-214">Obtenga información sobre cómo realizar [el mantenimiento planeado para máquinas virtuales Linux en Azure](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="a3b47-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
