---
title: Eventos programados para VM Windows en Azure| Microsoft Docs
description: "Eventos programados mediante el servicio Azure Metadata para las máquinas virtuales Windows."
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
ms.openlocfilehash: 7198fa8d1a512d10ca7022078aa2ea7bde3a4c02
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="0e2dd-103">Servicio Azure Metadata: eventos programados (versión preliminar) para VM Windows</span><span class="sxs-lookup"><span data-stu-id="0e2dd-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="0e2dd-104">Las versiones preliminares están a su disposición con la condición de que acepte los términos de uso.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="0e2dd-105">Para obtener más información, consulte [Términos de uso complementarios de las Versiones Preliminares de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="0e2dd-106">Scheduled Events es uno de los subservicios de Azure Metadata Service.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="0e2dd-107">Se encarga de mostrar información relacionada con eventos próximos (por ejemplo, un reinicio) para que la aplicación pueda prepararse para ellos y limitar las interrupciones.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="0e2dd-108">Está disponible para todos los tipos de máquina virtual de Azure, incluso para IaaS y PaaS.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="0e2dd-109">Scheduled Events permite que la máquina virtual tenga tiempo para realizar tareas de prevención y minimizar el efecto de un evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

<span data-ttu-id="0e2dd-110">Scheduled Events está disponible para máquinas virtuales Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="0e2dd-111">Para más información acerca de Scheduled Events en Linux, consulte [Scheduled Events para máquinas virtuales Linux](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="0e2dd-112">¿Por qué Scheduled Events?</span><span class="sxs-lookup"><span data-stu-id="0e2dd-112">Why Scheduled Events?</span></span>

<span data-ttu-id="0e2dd-113">Con Scheduled Events, puede tomar medidas para limitar el impacto del mantenimiento iniciado por la plataforma o de las acciones iniciadas por usuarios en el servicio.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-113">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="0e2dd-114">Las cargas de trabajo de varias instancias, que usan técnicas de replicación para mantener el estado, pueden ser vulnerables a las interrupciones que se producen en varias instancias.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-114">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="0e2dd-115">Esas interrupciones pueden dar lugar a tareas costosas (por ejemplo, volver a elaborar los índices) o, incluso, a una pérdida de las réplicas.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="0e2dd-116">En muchos otros casos, la disponibilidad global de los servicios puede mejorarse realizando una secuencia de apagado estable, por ejemplo, completando transacciones en curso (o cancelándolas), reasignando tareas a otras máquinas virtuales del clúster (conmutación por error manual) o eliminando la máquina virtual de un grupo de equilibradores de carga de red.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-116">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="0e2dd-117">Hay casos en los que notificar a un administrador sobre un evento próximo o registrar dicho evento puede mejorar el mantenimiento de las aplicaciones hospedadas en la nube.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="0e2dd-118">Azure Metadata Service muestra Eventos programados en los siguientes casos de uso:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-118">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="0e2dd-119">Mantenimiento iniciado por la plataforma (por ejemplo, la implementación del SO del host)</span><span class="sxs-lookup"><span data-stu-id="0e2dd-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="0e2dd-120">Llamadas iniciadas por el usuario (por ejemplo, si el usuario reinicia una VM o la vuelve a implementar)</span><span class="sxs-lookup"><span data-stu-id="0e2dd-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="the-basics"></a><span data-ttu-id="0e2dd-121">Conceptos básicos</span><span class="sxs-lookup"><span data-stu-id="0e2dd-121">The basics</span></span>  

<span data-ttu-id="0e2dd-122">Azure Metadata Service expone información sobre la ejecución de máquinas virtuales mediante un punto de conexión de REST accesible desde la propia máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="0e2dd-123">La información se encuentra disponible a través de una dirección IP no enrutable, de modo que no se expone fuera de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-123">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="0e2dd-124">Scope</span><span class="sxs-lookup"><span data-stu-id="0e2dd-124">Scope</span></span>
<span data-ttu-id="0e2dd-125">Los eventos programados se presentan a todas las máquinas virtuales en un servicio en la nube o a todas las máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-125">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="0e2dd-126">Por ello, debería revisar el campo `Resources` del evento para identificar cuáles son las máquinas virtuales que se verán afectadas.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-126">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="0e2dd-127">Detección del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="0e2dd-127">Discovering the endpoint</span></span>
<span data-ttu-id="0e2dd-128">Al crear una máquina virtual dentro de una red virtual (VNet), Metadata Service está disponible desde una dirección IP no enrutable (`169.254.169.254`).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-128">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="0e2dd-129">Si la máquina virtual no se crea dentro de una red virtual (lo habitual para servicios en la nube y VM clásicas), se necesita una lógica adicional para detectar el punto de conexión que vaya a usarse.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-129">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="0e2dd-130">Consulte esta muestra para obtener información sobre cómo [descubrir el punto de conexión de host](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-130">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="0e2dd-131">Control de versiones</span><span class="sxs-lookup"><span data-stu-id="0e2dd-131">Versioning</span></span> 
<span data-ttu-id="0e2dd-132">El servicio de metadatos de instancia tiene versiones.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-132">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="0e2dd-133">Las versiones son obligatorias y la versión actual es la `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-133">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0e2dd-134">Las versiones preliminares de eventos programados compatibles {más reciente} como la versión de api.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-134">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="0e2dd-135">Este formato ya no es compatible y dejará de utilizarse en el futuro.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-135">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="0e2dd-136">Uso de encabezados</span><span class="sxs-lookup"><span data-stu-id="0e2dd-136">Using headers</span></span>
<span data-ttu-id="0e2dd-137">Al realizar consultas a Metadata Service, debe proporcionar el encabezado `Metadata: true` para asegurarse de que la solicitud no se haya redirigido de manera involuntaria.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-137">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="0e2dd-138">Habilitación de eventos programados</span><span class="sxs-lookup"><span data-stu-id="0e2dd-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="0e2dd-139">La primera vez que efectúe una solicitud de eventos programados, Azure habilita de manera implícita la característica en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-139">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="0e2dd-140">Como resultado, debe esperar una respuesta diferida de hasta dos minutos en la primera llamada.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-140">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="0e2dd-141">Mantenimiento iniciado por el usuario</span><span class="sxs-lookup"><span data-stu-id="0e2dd-141">User initiated maintenance</span></span>
<span data-ttu-id="0e2dd-142">El mantenimiento de máquina virtual iniciado por el usuario a través de Azure Portal, API, CLI o PowerShell da lugar a un evento programado.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-142">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="0e2dd-143">Esto permite probar la lógica de preparación de mantenimiento en su aplicación. Asimismo, permite a su aplicación prepararse para el mantenimiento iniciado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-143">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="0e2dd-144">Si se reinicia una máquina virtual, se programa un evento con el tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="0e2dd-145">Si vuelve a implementar una máquina virtual, se programa un evento con el tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="0e2dd-146">Actualmente se puede programar sumultáneamente un máximo de 10 operaciones de mantenimiento iniciadas por el usuario.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="0e2dd-147">Este límite será más flexible antes de la disponibilidad general de eventos programados.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="0e2dd-148">Actualmente no se puede configurar ningún mantenimiento iniciado por el usuario que dé lugar a eventos programados.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="0e2dd-149">Está planeado que esta capacidad de configuración se lance en el futuro.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-149">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="0e2dd-150">Uso de la API</span><span class="sxs-lookup"><span data-stu-id="0e2dd-150">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="0e2dd-151">Consulta de eventos</span><span class="sxs-lookup"><span data-stu-id="0e2dd-151">Query for events</span></span>
<span data-ttu-id="0e2dd-152">Puede consultar los eventos programados; para ello, simplemente haga la siguiente llamada:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-152">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="0e2dd-153">Una respuesta contiene una matriz de eventos programados.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="0e2dd-154">Una matriz vacía significa que actualmente no hay eventos programados.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="0e2dd-155">En caso de que haya eventos programados, la respuesta contiene una matriz de eventos:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-155">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="0e2dd-156">Propiedades de evento</span><span class="sxs-lookup"><span data-stu-id="0e2dd-156">Event properties</span></span>
|<span data-ttu-id="0e2dd-157">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0e2dd-157">Property</span></span>  |  <span data-ttu-id="0e2dd-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="0e2dd-158">Description</span></span> |
| - | - |
| <span data-ttu-id="0e2dd-159">EventId</span><span class="sxs-lookup"><span data-stu-id="0e2dd-159">EventId</span></span> | <span data-ttu-id="0e2dd-160">Es un identificador único global del evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="0e2dd-161">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-161">Example:</span></span> <br><ul><li><span data-ttu-id="0e2dd-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="0e2dd-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="0e2dd-163">EventType</span><span class="sxs-lookup"><span data-stu-id="0e2dd-163">EventType</span></span> | <span data-ttu-id="0e2dd-164">Es el impacto causado por el evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="0e2dd-165">Valores:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-165">Values:</span></span> <br><ul><li> <span data-ttu-id="0e2dd-166">`Freeze`: la máquina virtual está programada para pausarse durante unos segundos.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-166">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="0e2dd-167">La CPU entra en estado de suspensión, pero esto no afecta a la memoria, a los archivos abiertos ni a las conexiones de red.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-167">The CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="0e2dd-168">`Reboot`: la máquina virtual está programada para reiniciarse (se borrará la memoria no persistente).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-168">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="0e2dd-169">`Redeploy`: la máquina virtual está programada para moverse a otro nodo (los discos efímeros se pierden).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-169">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="0e2dd-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="0e2dd-170">ResourceType</span></span> | <span data-ttu-id="0e2dd-171">Es el tipo de recurso al que afecta este evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="0e2dd-172">Valores:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="0e2dd-173">Recursos</span><span class="sxs-lookup"><span data-stu-id="0e2dd-173">Resources</span></span>| <span data-ttu-id="0e2dd-174">Es la lista de recursos a la que afecta este evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-174">List of resources this event impacts.</span></span> <span data-ttu-id="0e2dd-175">Se garantiza que contenga máquinas de un [dominio de actualización](manage-availability.md) como máximo, pero puede no contener todas las máquinas en el dominio.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-175">This is guaranteed to contain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="0e2dd-176">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-176">Example:</span></span> <br><ul><li> <span data-ttu-id="0e2dd-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="0e2dd-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="0e2dd-178">Estado de evento</span><span class="sxs-lookup"><span data-stu-id="0e2dd-178">Event Status</span></span> | <span data-ttu-id="0e2dd-179">Es el estado de este evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-179">Status of this event.</span></span> <br><br> <span data-ttu-id="0e2dd-180">Valores:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-180">Values:</span></span> <ul><li><span data-ttu-id="0e2dd-181">`Scheduled`: este evento está programado para iniciarse después de la hora especificada en la propiedad `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-181">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="0e2dd-182">`Started`: este evento se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="0e2dd-183">Nunca se proporcionan `Completed` ni ningún estado similar; el evento ya no se devolverá cuando finalice.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-183">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="0e2dd-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="0e2dd-184">NotBefore</span></span>| <span data-ttu-id="0e2dd-185">Hora a partir de la que puede iniciarse este evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="0e2dd-186">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-186">Example:</span></span> <br><ul><li> <span data-ttu-id="0e2dd-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="0e2dd-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="0e2dd-188">Programación de eventos</span><span class="sxs-lookup"><span data-stu-id="0e2dd-188">Event scheduling</span></span>
<span data-ttu-id="0e2dd-189">Cada evento se programa una cantidad mínima de tiempo en el futuro en función del tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-189">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="0e2dd-190">Este tiempo se refleja en la propiedad `NotBefore` de un evento.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="0e2dd-191">EventType</span><span class="sxs-lookup"><span data-stu-id="0e2dd-191">EventType</span></span>  | <span data-ttu-id="0e2dd-192">Minimum Notice</span><span class="sxs-lookup"><span data-stu-id="0e2dd-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="0e2dd-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="0e2dd-193">Freeze</span></span>| <span data-ttu-id="0e2dd-194">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0e2dd-194">15 minutes</span></span> |
| <span data-ttu-id="0e2dd-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="0e2dd-195">Reboot</span></span> | <span data-ttu-id="0e2dd-196">15 minutos</span><span class="sxs-lookup"><span data-stu-id="0e2dd-196">15 minutes</span></span> |
| <span data-ttu-id="0e2dd-197">Volver a implementar</span><span class="sxs-lookup"><span data-stu-id="0e2dd-197">Redeploy</span></span> | <span data-ttu-id="0e2dd-198">10 minutos</span><span class="sxs-lookup"><span data-stu-id="0e2dd-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="0e2dd-199">Inicio de un evento</span><span class="sxs-lookup"><span data-stu-id="0e2dd-199">Starting an event</span></span> 

<span data-ttu-id="0e2dd-200">Una vez que se haya enterado de un evento próximo y que haya completado la lógica para un apagado estable, puede aprobar el evento pendiente mediante una llamada de `POST` a Metadata Service con `EventId`.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="0e2dd-201">Esta indica a Azure que puede acortar el tiempo de notificación mínimo (cuando sea posible).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-201">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="0e2dd-202">Reconocer un evento permite a este continuar para todos sus elementos `Resources`, no solo para la máquina virtual que lo reconoce.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-202">Acknowledging an event allows the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="0e2dd-203">Por tanto, puede optar por elegir un líder para que coordine el reconocimiento. Este puede ser tan sencillo como la propia máquina del campo `Resources`.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-203">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="0e2dd-204">Ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e2dd-204">PowerShell sample</span></span> 

<span data-ttu-id="0e2dd-205">En el siguiente ejemplo se realiza una consulta a Metadata Service para eventos programados y se aprueban todos los eventos pendientes.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-205">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
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


## <a name="c-sample"></a><span data-ttu-id="0e2dd-206">Ejemplo de C\#</span><span class="sxs-lookup"><span data-stu-id="0e2dd-206">C\# sample</span></span> 

<span data-ttu-id="0e2dd-207">El siguiente ejemplo corresponde a un cliente sencillo que se comunica con Metadata Service.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-207">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="0e2dd-208">Scheduled Events puede representarse mediante las siguientes estructuras de datos:</span><span class="sxs-lookup"><span data-stu-id="0e2dd-208">Scheduled Events can be represented using the following data structures:</span></span>

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

<span data-ttu-id="0e2dd-209">En el siguiente ejemplo se realiza una consulta a Metadata Service para eventos programados y se aprueban todos los eventos pendientes.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-209">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter to approve executing events\n");
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

            Console.WriteLine("Complete. Press enter to repeat\n\n");
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

## <a name="python-sample"></a><span data-ttu-id="0e2dd-210">Ejemplo de Python</span><span class="sxs-lookup"><span data-stu-id="0e2dd-210">Python sample</span></span> 

<span data-ttu-id="0e2dd-211">En el siguiente ejemplo se realiza una consulta a Metadata Service para eventos programados y se aprueban todos los eventos pendientes.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-211">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0e2dd-212">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e2dd-212">Next steps</span></span> 

- <span data-ttu-id="0e2dd-213">En [Instance Metadata Service](instance-metadata-service.md) (Servicio Instance Metadata), puede obtener más información sobre las API disponibles.</span><span class="sxs-lookup"><span data-stu-id="0e2dd-213">Read more about the APIs available in the [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="0e2dd-214">Obtenga información sobre cómo realizar [el mantenimiento planeado para máquinas virtuales Windows en Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="0e2dd-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

