---
title: "Habilitación del registro de diagnóstico en eventos de Batch - Azure | Microsoft Docs"
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
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="cf8f2-103">Eventos de registro para la evaluación de diagnósticos y la supervisión de soluciones de Batch</span><span class="sxs-lookup"><span data-stu-id="cf8f2-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="cf8f2-104">Como ocurre con muchos de los servicios de Azure, el servicio Batch emite eventos de registro para determinados recursos mientras dure el recurso.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="cf8f2-105">Puede habilitar los registros de diagnóstico de Azure Batch para registrar los eventos de los recursos, como los grupos y las tareas y, después, utilizar los registros para la evaluación y supervisión de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="cf8f2-106">En los registros de diagnóstico de Batch se incluyen eventos como la creación de grupos, la eliminación de grupos, el inicio de tareas y la finalización de tareas, entre otros.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8f2-107">En este artículo se explica el registro de eventos para los propios recursos de la cuenta de Batch, no lo datos de salida de tareas y trabajos.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="cf8f2-108">Para más información sobre el almacenamiento de los datos de salida de trabajos y tareas, consulte [Almacenamiento de la salida de trabajos y tareas de Azure Batch](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="cf8f2-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cf8f2-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cf8f2-109">Prerequisites</span></span>
* [<span data-ttu-id="cf8f2-110">Una cuenta de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cf8f2-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="cf8f2-111">Una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cf8f2-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="cf8f2-112">Para conservar los registros de diagnóstico de Batch, es preciso crear la cuenta de Azure Storage en la que Azure va a almacenar los registros.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="cf8f2-113">Especifique esta cuenta de Storage cuando [habilite el registro de diagnóstico](#enable-diagnostic-logging) para su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="cf8f2-114">La cuenta de Storage que especifique al habilitar la recopilación de registros no es la misma que la cuenta de almacenamiento vinculada a la que se hace referencia en los artículos sobre [paquetes de aplicación](batch-application-packages.md) y [persistencia de salida de tarea](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="cf8f2-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="cf8f2-115">Se le **cobra** por los datos almacenados en su cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="cf8f2-116">Aquí se incluyen los registros de diagnóstico que se describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="cf8f2-117">Téngalo en cuenta al diseñar su [directiva de retención de registro](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="cf8f2-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="cf8f2-118">Activación del registro de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="cf8f2-118">Enable diagnostic logging</span></span>
<span data-ttu-id="cf8f2-119">El registro de diagnóstico no está habilitado de manera predeterminada en la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="cf8f2-120">Por consiguiente, es preciso habilitarlo explícitamente en cada cuenta de Batch que se desea supervisar:</span><span class="sxs-lookup"><span data-stu-id="cf8f2-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="cf8f2-121">Cómo habilitar la recopilación de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="cf8f2-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="cf8f2-122">Se recomienda leer toda el artículo [Información general sobre los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) para conocer no solo cómo habilitar el registro, sino también las categorías de registro que admiten los diversos servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="cf8f2-123">Por ejemplo, actualmente Azure Batch admite una categoría de registro: **registros de servicio**.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="cf8f2-124">Registros de servicios</span><span class="sxs-lookup"><span data-stu-id="cf8f2-124">Service Logs</span></span>
<span data-ttu-id="cf8f2-125">Los registros de servicio de Azure Batch contienen los eventos emitidos por Azure Batch mientras dure un recurso de Batch como un grupo o una tarea.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="cf8f2-126">Cada evento que emite Batch se almacena en la cuenta de Storage especificada en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="cf8f2-127">Por ejemplo, este es el cuerpo de un **evento de creación de grupos** de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cf8f2-127">For example, this is the body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="cf8f2-128">Cada cuerpo del evento reside en un archivo .json de la cuenta de Azure Storage especificada.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="cf8f2-129">Si desea acceder directamente a los registros, puede revisar el [esquema de registros de diagnóstico en la cuenta de almacenamiento](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="cf8f2-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="cf8f2-130">Eventos del registro del servicio</span><span class="sxs-lookup"><span data-stu-id="cf8f2-130">Service Log events</span></span>
<span data-ttu-id="cf8f2-131">Actualmente, el servicio Batch emite los siguientes eventos del registro del servicio.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="cf8f2-132">Es posible que la lista no sea exhaustiva, ya que se pueden haber agregado eventos adicionales desde la última vez que se actualizó este artículo.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="cf8f2-133">**Eventos del registro del servicio**</span><span class="sxs-lookup"><span data-stu-id="cf8f2-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="cf8f2-134">[Creación de grupos][pool_create]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="cf8f2-135">[Inicio de eliminación de grupo][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="cf8f2-136">[Finalización de eliminaciones de grupo][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="cf8f2-137">[Inicio de cambio de tamaño de grupo][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="cf8f2-138">[Finalización de cambio de tamaño de grupo][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="cf8f2-139">[Inicio de tarea][task_start]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="cf8f2-140">[Tarea completada][task_complete]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="cf8f2-141">[Error en la tarea][task_fail]</span><span class="sxs-lookup"><span data-stu-id="cf8f2-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cf8f2-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf8f2-142">Next steps</span></span>
<span data-ttu-id="cf8f2-143">Además de almacenar los eventos de registro de diagnóstico en una cuenta de Azure Storage, los eventos del registro del servicio Batch también se pueden transmitir a un [Centro de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md) y enviarlos a [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf8f2-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="cf8f2-144">Transmita registros de diagnóstico de Azure a centros de eventos</span><span class="sxs-lookup"><span data-stu-id="cf8f2-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="cf8f2-145">Transmita eventos de diagnóstico de Batch al servicio de entrada de datos altamente escalable, Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="cf8f2-146">Event Hubs puede ingerir millones de eventos por segundo, que posteriormente se pueden transformar y almacenar con cualquier proveedor de análisis en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="cf8f2-147">Análisis de los registros de diagnóstico de Azure mediante Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cf8f2-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="cf8f2-148">Envíe los registros de diagnóstico a Log Analytics, donde puede analizarlos en el portal de Operations Management Suite (OMS), o bien exportarlos para su análisis en Power BI o Excel.</span><span class="sxs-lookup"><span data-stu-id="cf8f2-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
