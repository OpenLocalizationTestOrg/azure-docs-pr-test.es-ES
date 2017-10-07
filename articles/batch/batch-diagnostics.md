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
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Eventos de registro para la evaluación de diagnósticos y la supervisión de soluciones de Batch

Como ocurre con muchos servicios de Azure, Hola servicio por lotes emite eventos de registro para determinados recursos durante Hola duración del recurso de Hola. Puede habilitar los eventos de toorecord registros de diagnóstico de Azure Batch para recursos, como los grupos y las tareas y, a continuación, usar los registros de Hola para evaluación de diagnóstico y supervisión. En los registros de diagnóstico de Batch se incluyen eventos como la creación de grupos, la eliminación de grupos, el inicio de tareas y la finalización de tareas, entre otros.

> [!NOTE]
> En este artículo se explica el registro de eventos para los propios recursos de la cuenta de Batch, no lo datos de salida de tareas y trabajos. Para obtener más información sobre cómo almacenar los datos de salida de hello de sus trabajos y tareas, consulte [salida de trabajos y tareas de lote de Azure se conservan](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
* [Una cuenta de Azure Batch](batch-account-create-portal.md)
* [cuenta de Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  registros de diagnóstico de toopersist por lotes, debe crear una cuenta de almacenamiento de Azure que Azure almacenará Hola registros. Especifique esta cuenta de Storage cuando [habilite el registro de diagnóstico](#enable-diagnostic-logging) para su cuenta de Batch. Hola cuenta de almacenamiento que especifique cuando se habilita la recopilación de registros es Hola mismo no como un hello tooin que se hace referencia de cuenta de almacenamiento vinculadas [paquetes de aplicación](batch-application-packages.md) y [persistencia de salida de la tarea](batch-task-output.md) artículos.
  
  > [!WARNING]
  > Está **cobra** para datos de hello almacenados en su cuenta de almacenamiento de Azure. Esto incluye los registros de diagnóstico Hola descritos en este artículo. Téngalo en cuenta al diseñar su [directiva de retención de registro](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Activación del registro de diagnóstico
El registro de diagnóstico no está habilitado de manera predeterminada en la cuenta de Batch. Debe habilitar explícitamente el registro de diagnóstico para cada cuenta de lote que desee toomonitor:

[¿Cómo tooenable colección de registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Le recomendamos que lea Hola completa [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo toogain entender no solo cómo tooenable registro pero Hola registro categorías admite Hola varios servicios de Azure. Por ejemplo, actualmente Azure Batch admite una categoría de registro: **registros de servicio**.

## <a name="service-logs"></a>Registros de servicios
Registros de servicio de Azure por lotes contienen eventos emitidos por el servicio de Azure Batch Hola durante la duración de Hola de un recurso de proceso por lotes como un grupo o una tarea. Cada evento emitido por lote se almacena en hello especificada cuenta de almacenamiento en formato JSON. Por ejemplo, esto es cuerpo Hola de las muestras **eventos de creación de grupo de**:

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

Cada cuerpo de evento reside en un .json archivo Hola especifica la cuenta de almacenamiento de Azure. Si desea tooaccess Hola registros directamente, es recomendable hello tooreview [esquema de registros de diagnóstico en la cuenta de almacenamiento de hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Eventos del registro del servicio
Hola servicio por lotes actualmente emite Hola después de los eventos de registro del servicio. Es posible que la lista no sea exhaustiva, ya que se pueden haber agregado eventos adicionales desde la última vez que se actualizó este artículo.

| **Eventos del registro del servicio** |
| --- |
| [Creación de grupos][pool_create] |
| [Inicio de eliminación de grupo][pool_delete_start] |
| [Finalización de eliminaciones de grupo][pool_delete_complete] |
| [Inicio de cambio de tamaño de grupo][pool_resize_start] |
| [Finalización de cambio de tamaño de grupo][pool_resize_complete] |
| [Inicio de tarea][task_start] |
| [Tarea completada][task_complete] |
| [Error en la tarea][task_fail] |

## <a name="next-steps"></a>Pasos siguientes
En eventos de registro de diagnóstico de toostoring de adición de una cuenta de almacenamiento de Azure, también puede transmitir tooan de eventos de registro del servicio por lotes [concentrador de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md)y les envíe demasiado[Azure Log Analytics](../log-analytics/log-analytics-overview.md).

* [Transmitir tooEvent centros de registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Secuencia de servicio de entrada de lote eventos de diagnóstico toohello datos altamente escalable, los concentradores de eventos. Event Hubs puede ingerir millones de eventos por segundo, que posteriormente se pueden transformar y almacenar con cualquier proveedor de análisis en tiempo real.
* [Análisis de los registros de diagnóstico de Azure mediante Log Analytics](../log-analytics/log-analytics-azure-storage.md)
  
  Enviar su tooLog registros de diagnóstico análisis donde puede analizarlas en portal de Operations Management Suite (OMS) de Hola o exportarlos para su análisis en Power BI o Excel.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
