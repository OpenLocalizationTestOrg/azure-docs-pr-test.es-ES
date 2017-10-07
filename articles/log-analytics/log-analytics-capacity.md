---
title: "aaaCapacity y solución de rendimiento en el análisis de registros de Azure | Documentos de Microsoft"
description: "Hola capacidad de uso y solución de rendimiento en toohelp de análisis de registros que comprenda Hola capacidad de los servidores de Hyper-V."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Planear la capacidad de máquina virtual de Hyper-V con capacidad de hello y solución de rendimiento (versión preliminar)

![Símbolo de capacidad y rendimiento](./media/log-analytics-capacity/capacity-solution.png)

Puede utilizar la capacidad de Hola y solución de rendimiento en toohelp de análisis de registros que comprenda Hola capacidad de los servidores de Hyper-V. solución de Hello proporciona información sobre el entorno de Hyper-V mostrándole Hola utilización global (CPU, memoria y disco) de hosts de Hola y Hola máquinas virtuales en ejecución en los hosts de Hyper-V. Se recopilan las métricas de CPU, memoria y discos en todos los hosts y máquinas virtuales de Hola que se ejecutan en ellos.

solución de Hello:

-   Muestra los hosts con el uso máximo y mínimo de la CPU y de la memoria
-   Muestra las máquinas virtuales con el uso máximo y mínimo de la CPU y de la memoria
-   Muestra las máquinas virtuales con el uso máximo y mínimo de las IOPS y del rendimiento
-   Muestra qué máquinas virtuales se ejecutan en los hosts
-   Muestra de Hola discos superiores con un alto rendimiento, IOPS, y volúmenes compartidos de latencia en clúster
- Le permite toocustomize y filtro basado en grupos

> [!NOTE]
> versión anterior de Hola de hello capacidad y solución de rendimiento denominado Administración de capacidad requiere System Center Operations Manager y System Center Virtual Machine Manager. Esta solución actualizada no tiene esas dependencias.


## <a name="connected-sources"></a>Orígenes conectados

Hello en la tabla siguiente describe los orígenes de hello conectado que son compatibles con esta solución.

| Origen conectado | Soporte técnico | Descripción |
|---|---|---|
| [Agentes de Windows](log-analytics-windows-agents.md) | Sí | solución de Hello recopila información de datos de rendimiento y capacidad de los agentes de Windows. |
| [Agentes de Linux](log-analytics-linux-agents.md) | No    | solución de Hello no recopila información de datos de rendimiento y capacidad de agentes Linux directa.|
| [Grupo de administración de SCOM](log-analytics-om-agents.md) | Sí |solución de Hello recopila datos de capacidad y rendimiento de agentes en un grupo de administración de SCOM conectado. No se requiere una conexión directa de tooOMS de agente SCOM Hola. Datos se reenvían desde el repositorio de OMS de toohello del grupo de administración de Hola.|
| [Cuenta de Almacenamiento de Azure](log-analytics-azure-storage.md) | No | Azure Storage no incluye datos de capacidad y rendimiento.|

## <a name="prerequisites"></a>Requisitos previos

- Los agentes de Windows o de Operations Manager deben instalarse en hosts de Hyper-V, no máquinas virtuales, con Windows Server 2012, o cualquier versión superior.


## <a name="configuration"></a>Configuración

Realizar Hola siguiendo el paso tooadd Hola capacidad y rendimiento solución tooyour área de trabajo.

- Agregar Hola capacidad y rendimiento solución tooyour OMS área de trabajo mediante el proceso de Hola se describe en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Módulos de administración

Si el grupo de administración de SCOM es el área de trabajo OMS tooyour conectado, Hola después de módulos de administración se instalará en SCOM cuando se agrega esta solución. No es necesario realizar tareas de configuración o mantenimiento de estos módulos de administración.

- Microsoft.IntelligencePacks.CapacityPerformance

evento de Hello 1201 es similar:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Cuando se actualiza Hola solución de capacidad y rendimiento, el número de versión de Hola cambiará.

Para obtener más información sobre cómo se actualizan los módulos de administración de soluciones, consulte [tooLog de conexión de Operations Manager análisis](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>Uso de solución de Hola

Cuando agrega Hola capacidad y rendimiento solución tooyour área de trabajo, hello capacidad y rendimiento se agrega toohello panel general. Este icono muestra el recuento del número de Hola de hosts de Hyper-V activos actualmente y número de Hola de máquinas virtuales activas que se han supervisado para hello período de tiempo seleccionado.

![Icono Capacidad y rendimiento](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Revisión de la utilización

Haga clic en hello capacidad y rendimiento mosaico tooopen Hola capacidad y rendimiento del panel. panel de Hello incluye columnas de hello en hello en la tabla siguiente. Cada columna se enumera los elementos de tooten coincidentes que han especificado criterios de la columna para hello ámbito y el tiempo de intervalo. Puede ejecutar una búsqueda de registros que devuelve todos los registros, haga clic en **ver todas** en parte inferior de la columna de Hola o haciendo clic en el encabezado de columna de Hola de Hola.

- **Hosts**
    - **Utilización de CPU de host** muestra una tendencia gráfica de utilización de CPU de Hola de equipos host y una lista de hosts, en función de hello período de tiempo seleccionado. Mantenga el mouse sobre detalles de tooview de gráfico de línea de Hola para un punto específico en el tiempo. Haga clic en hello gráfico tooview más detalles en la búsqueda de registros. Haga clic en cualquier búsqueda de registros de tooopen de nombre de host y ver los datos del contador de CPU para máquinas virtuales hospedadas.
    - **Utilización de memoria de host** muestra una tendencia gráfica de uso de memoria de Hola de equipos host y una lista de hosts, en función de hello período de tiempo seleccionado. Mantenga el mouse sobre detalles de tooview de gráfico de línea de Hola para un punto específico en el tiempo. Haga clic en hello gráfico tooview más detalles en la búsqueda de registros. Haga clic en cualquier host nombre tooopen registro búsqueda y visualización memoria los datos del contador de máquinas virtuales hospedadas.
- **Máquinas virtuales**
    - **Uso de CPU de VM** muestra una tendencia gráfica de utilización de CPU de Hola de máquinas virtuales y una lista de máquinas virtuales, en función de hello período de tiempo seleccionado. Mantenga el mouse sobre detalles de tooview de gráfico de línea de Hola para un punto específico en el tiempo para hello principales 3 máquinas virtuales. Haga clic en hello gráfico tooview más detalles en la búsqueda de registros. Haga clic en cualquier búsqueda de registros de tooopen de nombre de máquina virtual y ver los datos del contador CPU agregados para hello VM.
    - **Utilización de memoria de VM** muestra un gráfico tendencias de uso de memoria de Hola de máquinas virtuales y una lista de máquinas virtuales, en función de hello período de tiempo seleccionado. Mantenga el mouse sobre detalles de tooview de gráfico de línea de Hola para un punto específico en el tiempo para hello principales 3 máquinas virtuales. Haga clic en hello gráfico tooview más detalles en la búsqueda de registros. Haga clic en cualquier búsqueda de registros de tooopen de nombre de máquina virtual y ver los detalles de contador de memoria agregada de hello máquina virtual.
    - **IOPS de disco Total de VM** muestra una gráfica tendencia de hello total IOPS del disco para máquinas virtuales y una lista de máquinas virtuales con hello IOPS para cada uno, según Hola período de tiempo seleccionado. Mantenga el mouse sobre detalles de tooview de gráfico de línea de Hola para un punto específico en el tiempo para hello principales 3 máquinas virtuales. Haga clic en hello gráfico tooview más detalles en la búsqueda de registros. Haga clic en cualquier búsqueda de registros de tooopen de nombre de máquina virtual y la vista de detalles de hello VM de contador de IOPS del disco agregados.
    - **Capacidad Total de disco de máquina virtual** muestra una tendencia gráfica de rendimiento de disco total de Hola para máquinas virtuales y una lista de máquinas virtuales con un rendimiento de disco total de Hola para cada uno, hello en función de período de tiempo seleccionado. Mantenga el mouse sobre detalles de tooview de gráfico de línea de Hola para un punto específico en el tiempo para hello principales 3 máquinas virtuales. Haga clic en hello gráfico tooview más detalles en la búsqueda de registros. Haga clic en cualquier búsqueda de registros de tooopen de nombre de máquina virtual y ver los datos del contador de rendimiento agregado total en disco para hello máquina virtual.
- **Volúmenes compartidos en clúster**
    - **Total de rendimiento** muestra la suma de Hola de las lecturas y escrituras en volúmenes compartidos en clúster.
    - **Total de IOPS** suma de Hola de muestra de operaciones de entrada/salida por segundo en volúmenes compartidos en clúster.
    - **Latencia total** muestra la latencia total de hello en volúmenes compartidos en clúster.
- **Hospedar densidad** icono superior de hello muestra número total de Hola de solución disponible toohello hosts y máquinas virtuales. Haga clic en el icono superior de Hola de los detalles de tooview adicionales en búsqueda de registros. También se enumeran todos los hosts y número de Hola de máquinas virtuales que se hospedan. Haga clic en un host toodrill en los resultados de la máquina virtual de hello en una búsqueda de registros.


![Hoja Hosts de panel](./media/log-analytics-capacity/dashboard-hosts.png)

![Hoja Máquinas virtuales de panel](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Evaluación del rendimiento

Entornos de producción de computación difieren mucho de una organización tooanother. Además, la capacidad y las cargas de trabajo de rendimiento pueden depender del funcionamiento de las máquinas virtuales y de lo que se considere normal. Probablemente no se aplicaría tooyour entorno toohelp procedimientos concretos medir el rendimiento. Por lo tanto, más generalizada instrucciones preceptivas es mejor toohelp adecuado. Microsoft publica una variedad de instrucciones preceptivas artículos toohelp medir el rendimiento.

toosummarize, solución Hola recopila datos de capacidad y rendimiento de una variedad de orígenes, incluidos los contadores de rendimiento. Usar esos datos de capacidad y rendimiento que se presentan en distintas superficies en soluciones de Hola y comparar su toothose resultados en hello [medir el rendimiento en Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) artículo. Aunque el artículo de Hola se publicó hace bastante tiempo, directrices, consideraciones y las métricas de hello continúen siendo válidas. artículo de Hello contiene recursos útiles de tooother de vínculos.


## <a name="sample-log-searches"></a>Búsquedas de registros de ejemplo

Hello en la tabla siguiente proporciona búsquedas de registros de ejemplo para la capacidad y rendimiento datos recopilados y calculado por esta solución.

| Consultar | Descripción |
|---|---|
| Todas las configuraciones de memoria del host | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Todas las configuraciones de memoria de la máquina virtual | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Desglose de E/S por segundo total del disco en todas las máquinas virtuales | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Desglose del rendimiento total del disco en todas las máquinas virtuales | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Desglose de E/S por segundo total en todos los CSV | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Desglose del rendimiento total del disco en todos los CSV | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Desglose de la latencia total en todos los CSV | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.

> | Consultar | Descripción |
|:--- |:--- |
| Todas las configuraciones de memoria del host | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "Host Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Todas las configuraciones de memoria de la máquina virtual | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "VM Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Desglose de E/S por segundo total del disco en todas las máquinas virtuales | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Reads/s" or CounterName == "VHD Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Desglose del rendimiento total del disco en todas las máquinas virtuales | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Read MB/s" or CounterName == "VHD Write MB/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Desglose de E/S por segundo total en todos los CSV | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Desglose del rendimiento total del disco en todos los CSV | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Desglose de la latencia total en todos los CSV | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Read Latency" or CounterName == "CSV Write Latency") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |


## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de capacidad y rendimiento.
