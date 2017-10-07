---
title: "registro de diagnóstico para eventos de lote - Azure aaaEnable | Documentos de Microsoft"
description: "Registre y analice los eventos de registro de diagnóstico de los recursos de la cuenta de Azure Batch como tareas y grupos."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="a8dfa-103">Eventos de registro para la evaluación de diagnósticos y la supervisión de soluciones de Batch</span><span class="sxs-lookup"><span data-stu-id="a8dfa-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="a8dfa-104">Como ocurre con muchos servicios de Azure, Hola servicio por lotes emite eventos de registro para determinados recursos durante Hola duración del recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="a8dfa-105">Puede habilitar los eventos de toorecord registros de diagnóstico de Azure Batch para recursos, como los grupos y las tareas y, a continuación, usar los registros de Hola para evaluación de diagnóstico y supervisión.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="a8dfa-106">En los registros de diagnóstico de Batch se incluyen eventos como la creación de grupos, la eliminación de grupos, el inicio de tareas y la finalización de tareas, entre otros.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="a8dfa-107">En este artículo se explica el registro de eventos para los propios recursos de la cuenta de Batch, no lo datos de salida de tareas y trabajos.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="a8dfa-108">Para obtener más información sobre cómo almacenar los datos de salida de hello de sus trabajos y tareas, consulte [salida de trabajos y tareas de lote de Azure se conservan](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="a8dfa-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a8dfa-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a8dfa-109">Prerequisites</span></span>
* [<span data-ttu-id="a8dfa-110">Una cuenta de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="a8dfa-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="a8dfa-111">cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a8dfa-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="a8dfa-112">registros de diagnóstico de toopersist por lotes, debe crear una cuenta de almacenamiento de Azure que Azure almacenará Hola registros.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="a8dfa-113">Especifique esta cuenta de Storage cuando [habilite el registro de diagnóstico](#enable-diagnostic-logging) para su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="a8dfa-114">Hola cuenta de almacenamiento que especifique cuando se habilita la recopilación de registros es Hola mismo no como un hello tooin que se hace referencia de cuenta de almacenamiento vinculadas [paquetes de aplicación](batch-application-packages.md) y [persistencia de salida de la tarea](batch-task-output.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="a8dfa-115">Está **cobra** para datos de hello almacenados en su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="a8dfa-116">Esto incluye los registros de diagnóstico Hola descritos en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="a8dfa-117">Téngalo en cuenta al diseñar su [directiva de retención de registro](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8dfa-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="a8dfa-118">Activación del registro de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="a8dfa-118">Enable diagnostic logging</span></span>
<span data-ttu-id="a8dfa-119">El registro de diagnóstico no está habilitado de manera predeterminada en la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="a8dfa-120">Debe habilitar explícitamente el registro de diagnóstico para cada cuenta de lote que desee toomonitor:</span><span class="sxs-lookup"><span data-stu-id="a8dfa-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="a8dfa-121">¿Cómo tooenable colección de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="a8dfa-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="a8dfa-122">Le recomendamos que lea Hola completa [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo toogain entender no solo cómo tooenable registro pero Hola registro categorías admite Hola varios servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="a8dfa-123">Por ejemplo, actualmente Azure Batch admite una categoría de registro: **registros de servicio**.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="a8dfa-124">Registros de servicios</span><span class="sxs-lookup"><span data-stu-id="a8dfa-124">Service Logs</span></span>
<span data-ttu-id="a8dfa-125">Registros de servicio de Azure por lotes contienen eventos emitidos por el servicio de Azure Batch Hola durante la duración de Hola de un recurso de proceso por lotes como un grupo o una tarea.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="a8dfa-126">Cada evento emitido por lote se almacena en hello especificada cuenta de almacenamiento en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="a8dfa-127">Por ejemplo, esto es cuerpo Hola de las muestras **eventos de creación de grupo de**:</span><span class="sxs-lookup"><span data-stu-id="a8dfa-127">For example, this is hello body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="a8dfa-128">Cada cuerpo de evento reside en un .json archivo Hola especifica la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="a8dfa-129">Si desea tooaccess Hola registros directamente, es recomendable hello tooreview [esquema de registros de diagnóstico en la cuenta de almacenamiento de hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a8dfa-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="a8dfa-130">Eventos del registro del servicio</span><span class="sxs-lookup"><span data-stu-id="a8dfa-130">Service Log events</span></span>
<span data-ttu-id="a8dfa-131">Hola servicio por lotes actualmente emite Hola después de los eventos de registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="a8dfa-132">Es posible que la lista no sea exhaustiva, ya que se pueden haber agregado eventos adicionales desde la última vez que se actualizó este artículo.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="a8dfa-133">**Eventos del registro del servicio**</span><span class="sxs-lookup"><span data-stu-id="a8dfa-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="a8dfa-134">[Creación de grupos][pool_create]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="a8dfa-135">[Inicio de eliminación de grupo][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="a8dfa-136">[Finalización de eliminaciones de grupo][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="a8dfa-137">[Inicio de cambio de tamaño de grupo][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="a8dfa-138">[Finalización de cambio de tamaño de grupo][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="a8dfa-139">[Inicio de tarea][task_start]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="a8dfa-140">[Tarea completada][task_complete]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="a8dfa-141">[Error en la tarea][task_fail]</span><span class="sxs-lookup"><span data-stu-id="a8dfa-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8dfa-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8dfa-142">Next steps</span></span>
<span data-ttu-id="a8dfa-143">En eventos de registro de diagnóstico de toostoring de adición de una cuenta de almacenamiento de Azure, también puede transmitir tooan de eventos de registro del servicio por lotes [concentrador de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md)y les envíe demasiado[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8dfa-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="a8dfa-144">Transmitir tooEvent centros de registros de diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="a8dfa-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="a8dfa-145">Secuencia de servicio de entrada de lote eventos de diagnóstico toohello datos altamente escalable, los concentradores de eventos.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="a8dfa-146">Event Hubs puede ingerir millones de eventos por segundo, que posteriormente se pueden transformar y almacenar con cualquier proveedor de análisis en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="a8dfa-147">Análisis de los registros de diagnóstico de Azure mediante Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a8dfa-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="a8dfa-148">Enviar su tooLog registros de diagnóstico análisis donde puede analizarlas en portal de Operations Management Suite (OMS) de Hola o exportarlos para su análisis en Power BI o Excel.</span><span class="sxs-lookup"><span data-stu-id="a8dfa-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
