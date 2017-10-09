---
title: "aaaAzure métricas comunes de escalado automático | Documentos de Microsoft"
description: "Aprenda qué métricas se utilizan normalmente para el escalado automático de Servicios en la nube, Máquinas virtuales y Aplicaciones web."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Métricas comunes de escalado automático de Azure Monitor
Azure Monitor escalado automático permite que se tooscale Hola número de instancias en ejecución hacia arriba o hacia abajo, en función de los datos de telemetría (métrica). Este documento describe las métricas comunes que podría interesarle toouse. Hola portal de Azure para servicios en la nube y las granjas de servidores, puede elegir métrica Hola de hello recursos tooscale por. Sin embargo, también puede elegir cualquier métrica de una tooscale de recursos distinto por.

Azure escalado automático de Monitor se aplica solo demasiado[conjuntos de escalas de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [servicios en la nube](https://azure.microsoft.com/services/cloud-services/), y [servicio de aplicaciones: aplicaciones Web](https://azure.microsoft.com/services/app-service/web/). Otros servicios de Azure usan distintos métodos de escalado.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Cálculo de métricas de máquinas virtuales basadas en Resource Manager
De forma predeterminada, las máquinas virtuales basadas en Resource Manager y los conjuntos de escalado de máquinas virtuales emiten métricas básicas (de nivel de host). Además, al configurar la recopilación de datos de diagnóstico para una máquina virtual de Azure y VMSS, Hola extensión de diagnóstico de Azure también emite los contadores de rendimiento de SO invitado (que normalmente se conoce como "Métricas de SO invitado").  Todas estas métricas se usan en reglas de escalado automático.

Puede usar hello `Get MetricDefinitions` PoSH/API/CLI tooview Hola métricas para el recurso VMSS.

Si está utilizando conjuntos de escalado de máquinas virtuales y no ve una métrica concreta enumerada, entonces es probable que esté *deshabilitada* en la extensión Diagnostics.

Si una métrica determinada no se está frecuencia Hola muestreado o transferidos en el que desee, puede actualizar la configuración de diagnóstico Hola.

Si se cumple cualquiera de los casos anterior, a continuación, revise [tooenable usar PowerShell diagnósticos de Azure en una máquina virtual ejecuta Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) sobre tooconfigure de PowerShell y actualizar su tooenable de extensión de diagnósticos de Azure VM Hola métrica. Ese artículo también incluye un archivo de configuración de diagnósticos de ejemplo.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Métricas de host para máquinas virtuales Windows y Linux basadas en Resource Manager
Hola siguiendo las métricas de nivel de host se emite de forma predeterminada para la máquina virtual de Azure y VMSS en instancias de Windows y Linux. Estas métricas describen la VM de Azure, pero se recopilan desde el host de máquina virtual de Azure de hello en lugar de a través de agente instalado en la máquina virtual invitada de Hola. Puede usar estas métricas en reglas de escalado automático.

- [Métricas de host para máquinas virtuales Windows y Linux basadas en Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Métricas de host para conjuntos de escalado de máquinas virtuales Windows y Linux basadas en Resource Manager](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>Métricas de SO invitado para máquinas virtuales Windows basadas en Resource Manager
Cuando se crea una máquina virtual en Azure, se habilitan los diagnósticos mediante el uso de la extensión de diagnósticos de Hola. extensión de diagnósticos de Hello emite un conjunto de métricas realizadas desde dentro de hello máquina virtual. Esto significa que puede escalar automáticamente fuera de las métricas que no se emiten de forma predeterminada.

Puede generar una lista de las métricas de hello mediante Hola siguiente comando de PowerShell.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Puede crear una alerta para hello siguientes métricas:

| Nombre de métrica | Unidad |
| --- | --- |
| Procesador(_Total)\% Hora del procesador |Percent |
| \Procesador(_Total)\% de tiempo con privilegios |Percent |
| \Procesador(_Total)\% de tiempo de usuario |Percent |
| \Información del procesador(_Total)\Frecuencia del procesador |Recuento |
| \Sistema\Procesos |Recuento |
| \Proceso(_Total)\Número de subprocesos |Recuento |
| \Proceso(_Total)\Número de identificadores |Recuento |
| \Memoria\% de bytes confirmados en uso |Percent |
| \Memoria\Bytes disponibles |Bytes |
| \Memoria\Bytes confirmados |Bytes |
| \Memoria\Límite de confirmación |Bytes |
| \Memoria\Bytes de bloque paginado |Bytes |
| \Memoria\Bytes de bloque no paginado |Bytes |
| \Disco físico(_Total)\% de tiempo de disco |Percent |
| \Disco físico(_Total)\%Tiempo de lectura de disco |Percent |
| \Disco físico(_Total)\% de tiempo de escritura de disco |Percent |
| \Disco físico(_Total)\Transferencias de disco/s |CountPerSecond |
| \Disco físico(_Total)\Lecturas de disco/s |CountPerSecond |
| \Disco físico(_Total)\Escrituras de disco/s |CountPerSecond |
| \Disco físico(_Total)\Bytes de disco/s |BytesPerSecond |
| \Disco físico(_Total)\Bytes de lectura de disco/s |BytesPerSecond |
| \Disco físico(_Total)\Bytes de escritura de disco/s |BytesPerSecond |
| \Disco físico(_Total)\Promedio Longitud de la cola de disco |Recuento |
| \Disco físico(_Total)\Promedio Longitud de la cola de lectura de disco |Recuento |
| \Disco físico(_Total)\Promedio Longitud de la cola de escritura de disco |Recuento |
| \Disco lógico(_Total)\% de espacio disponible |Percent |
| \Disco lógico(_Total)\Megabytes disponibles |Recuento |

### <a name="guest-os-metrics-linux-vms"></a>Métricas de SO invitado para máquinas virtuales Linux
Cuando crea una máquina virtual en Azure, los diagnósticos se habilitan de forma predeterminada mediante la extensión Diagnósticos.

Puede generar una lista de las métricas de hello mediante Hola siguiente comando de PowerShell.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 Puede crear una alerta para hello siguientes métricas:

| Nombre de métrica | Unidad |
| --- | --- |
| \Memory\AvailableMemory |Bytes |
| \Memory\PercentAvailableMemory |Percent |
| \Memory\UsedMemory |Bytes |
| \Memory\PercentUsedMemory |Percent |
| \Memory\PercentUsedByCache |Percent |
| \Memory\PagesPerSec |CountPerSecond |
| \Memory\PagesReadPerSec |CountPerSecond |
| \Memory\PagesWrittenPerSec |CountPerSecond |
| \Memory\AvailableSwap |Bytes |
| \Memory\PercentAvailableSwap |Percent |
| \Memory\UsedSwap |Bytes |
| \Memory\PercentUsedSwap |Percent |
| \Processor\PercentIdleTime |Percent |
| \Processor\PercentUserTime |Percent |
| \Processor\PercentNiceTime |Percent |
| \Processor\PercentPrivilegedTime |Percent |
| \Processor\PercentInterruptTime |Percent |
| \Processor\PercentDPCTime |Percent |
| \Processor\PercentProcessorTime |Percent |
| \Processor\PercentIOWaitTime |Percent |
| \PhysicalDisk\BytesPerSecond |BytesPerSecond |
| \PhysicalDisk\ReadBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\WriteBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\TransfersPerSecond |CountPerSecond |
| \PhysicalDisk\ReadsPerSecond |CountPerSecond |
| \PhysicalDisk\WritesPerSecond |CountPerSecond |
| \PhysicalDisk\AverageReadTime |Segundos |
| \PhysicalDisk\AverageWriteTime |Segundos |
| \PhysicalDisk\AverageTransferTime |Segundos |
| \PhysicalDisk\AverageDiskQueueLength |Recuento |
| \NetworkInterface\BytesTransmitted |Bytes |
| \NetworkInterface\BytesReceived |Bytes |
| \NetworkInterface\PacketsTransmitted |Recuento |
| \NetworkInterface\PacketsReceived |Recuento |
| \NetworkInterface\BytesTotal |Bytes |
| \NetworkInterface\TotalRxErrors |Recuento |
| \NetworkInterface\TotalTxErrors |Recuento |
| \NetworkInterface\TotalCollisions |Recuento |

## <a name="commonly-used-web-server-farm-metrics"></a>Métricas web comúnmente usadas (granja de servidores)
También puede realizar el escalado automático en función de métricas de servidor web comunes como Hola longitud de la cola de Http. El nombre de la métrica es **HttpQueueLength**.  Hola siguiendo las métricas de sección listas servidor disponible (aplicaciones Web) de la granja de servidores.

### <a name="web-apps-metrics"></a>Métricas de Aplicaciones web
Puede generar una lista de las métricas de las aplicaciones Web de hello mediante Hola siguiente comando de PowerShell.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Puede alertar sobre estas métricas o escalar por las mismas.

| Nombre de métrica | Unidad |
| --- | --- |
| CpuPercentage |Percent |
| MemoryPercentage |Percent |
| DiskQueueLength |Recuento |
| HttpQueueLength |Recuento |
| BytesReceived |Bytes |
| BytesSent |Bytes |

## <a name="commonly-used-storage-metrics"></a>Métricas de almacenamiento utilizadas comúnmente
Puede escalar por la longitud de la cola de almacenamiento, que es el número de Hola de mensajes en cola de almacenamiento de Hola. Longitud de la cola de almacenamiento es una medida especial y umbral de hello es el número de Hola de mensajes por instancia. Por ejemplo, si hay dos instancias, y si se establece el umbral de hello too100, ajuste de escala se produce cuando Hola número total de mensajes en cola de hello es 200. Que puede ser 100 mensajes por instancia, 120 y 80 o cualquier otra combinación que suma too200 o más.

Configurar esta opción en hello portal de Azure en hello **configuración** hoja. Para conjuntos de escalas de VM, puede actualizar la configuración de escalado automático de hello en toouse de plantilla del Administrador de recursos de hello *metricName* como *ApproximateMessageCount* y pasar el identificador de cola de almacenamiento de hello como hello  *metricResourceUri*.

Por ejemplo, con un hello clásico cuenta de almacenamiento metricTrigger de configuración de escalado automático incluiría:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

Para una cuenta de almacenamiento (no clásico), incluiría Hola metricTrigger:

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>Métricas más usadas de Bus de servicio
Puede escalar por la longitud de la cola de Bus de servicio, que es el número de Hola de mensajes en cola de Bus de servicio de Hola. Longitud de cola de Bus de servicio es una medida especial y umbral de hello es el número de Hola de mensajes por instancia. Por ejemplo, si hay dos instancias, y si se establece el umbral de hello too100, ajuste de escala se produce cuando Hola número total de mensajes en cola de hello es 200. Que puede ser 100 mensajes por instancia, 120 y 80 o cualquier otra combinación que suma too200 o más.

Para conjuntos de escalas de VM, puede actualizar la configuración de escalado automático de hello en toouse de plantilla del Administrador de recursos de hello *metricName* como *ApproximateMessageCount* y pasar el identificador de cola de almacenamiento de hello como hello  *metricResourceUri*.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> Bus de servicio, no existe el concepto de grupo de recursos de hello pero Azure Resource Manager crea un grupo de recursos predeterminado por región. grupo de recursos de Hello normalmente está en formato de hello 'Default - ServiceBus-[Región]'. Por ejemplo, 'Default-ServiceBus-EastUS', 'Default-ServiceBus-WestUS', 'Default-ServiceBus-AustraliaEast', etc.
>
>
