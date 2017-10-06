---
title: "aaaView datos analíticos de aplicaciones Web de Azure | Documentos de Microsoft"
description: "Puede usar información de toogain de solución de análisis de aplicaciones Web de Azure Hola sobre sus aplicaciones Web de Azure mediante la recopilación de métricas diferentes a través de todos los recursos de aplicación Web de Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>Visualización de datos de análisis para métricas en todos los recursos de aplicaciones web de Azure

![Símbolo de Web Apps](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Hola soluciones de análisis de aplicaciones Web de Azure (vista previa) proporciona información sobre la [aplicaciones Web de Azure](../app-service-web/app-service-web-overview.md) mediante la recopilación de métricas diferentes a través de todos los recursos de aplicación Web de Azure. Con la solución de hello, puede analizar y buscar datos de métrica de recursos de aplicación web.

Con la solución de hello, puede ver el:

- Aplicaciones Web principales con mayor tiempo de respuesta Hola
- El número de solicitudes en sus aplicaciones web, incluidas las solicitudes correctas y con errores
- Las principales aplicaciones web con mayor tráfico entrante y saliente
- Los principales planes de servicio con un uso intensivo de CPU y memoria
- Operaciones de registro de actividad de Azure Web Apps

## <a name="connected-sources"></a>Orígenes conectados

A diferencia de la mayoría de las demás soluciones Log Analytics, los agentes no recopilan datos para Azure Web Apps. Todos los datos utilizados por la solución de hello proceden directamente de Azure.

| Origen conectado | Compatible | Descripción |
| --- | --- | --- |
| [Agentes de Windows](log-analytics-windows-agents.md) | No | solución de Hello no recopila información de agentes de Windows. |
| [Agentes de Linux](log-analytics-linux-agents.md) | No | solución de Hello no recopilar información de agentes de Linux. |
| [Grupo de administración de SCOM](log-analytics-om-agents.md) | No | solución de Hello no recopila información de agentes en un grupo de administración de SCOM conectado. |
| [Cuenta de Almacenamiento de Azure](log-analytics-azure-storage.md) | No | solución de Hello no no información de recopilación del almacenamiento de Azure. |

## <a name="prerequisites"></a>Requisitos previos

- tooaccess información de métrica de recursos de aplicación Web de Azure, debe tener una suscripción de Azure.

## <a name="configuration"></a>Configuración

Realizar Hola después de la solución de análisis de aplicaciones Web de Azure de pasos tooconfigure Hola para las áreas de trabajo.

1. Habilitar la solución de análisis de aplicaciones Web de Azure Hola desde [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. [Habilitar tooOMS de registro de las métricas de recursos de Azure con PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

Hola soluciones de análisis de aplicaciones Web de Azure recopila dos conjuntos de métricas de Azure:

- Métricas de Azure Web Apps
  - Espacio de trabajo de memoria promedio
  - Tiempo de respuesta promedio
  - Bytes enviados/recibidos
  - Tiempo de CPU
  - Solicitudes
  - Espacio de trabajo de memoria
  - Httpxxx
- Métricas del plan de App Service
  - Bytes enviados/recibidos
  - Porcentaje de CPU
  - Longitud de la cola de disco
  - Longitud de la cola HTTP
  - Porcentaje de memoria

Solo se recopilan las métricas del plan de App Service si utiliza un plan de servicio dedicado. Esto no aplica toofree o compartido planes de servicio de aplicaciones.

Si agrega solución hello mediante Hola portal OMS, verá icono Hola siguiente. Necesita demasiado[habilitar tooOMS de registro de las métricas de recursos de Azure con PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

![Realización de una notificación de evaluación](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

Después de configurar la solución de hello, datos deberían iniciar flujo tooyour área de trabajo dentro de 15 minutos.

## <a name="using-hello-solution"></a>Uso de solución de Hola

Cuando se agrega el área de trabajo tooyour soluciones de análisis de aplicaciones Web de Azure de hello, Hola **análisis de aplicaciones Web de Azure** es agregar el icono de panel de información general de tooyour. Este icono muestra un recuento del número de Hola de aplicaciones Web de Azure que Hola solución no tiene acceso tooin su suscripción de Azure.

![Icono de Azure Web Apps Analytics](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Visualización de la información de Azure Web Apps Analytics

Haga clic en hello **análisis de aplicaciones Web de Azure** icono tooopen hello **análisis de aplicaciones Web de Azure** panel. panel de Hello incluye módulos de hello en hello en la tabla siguiente. Cada hoja se enumera los elementos de tooten coincidentes que han especificado criterios del módulo para hello ámbito y el tiempo de intervalo. Puede ejecutar una búsqueda de registros que devuelve todos los registros, haga clic en **ver todas** en parte inferior de la hoja de Hola o haciendo clic en el encabezado de la hoja de Hola de Hola.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| Columna | Descripción |
| --- | --- |
| Azure Web Apps |   |
| Tendencias de solicitud de Web Apps | Muestra un gráfico de líneas de tendencia de la solicitud de aplicaciones Web para el intervalo de fechas de Hola que ha seleccionado de hello y muestra una lista de solicitudes web diez principales de Hola. Haga clic en toorun de gráfico de línea de Hola para una búsqueda de registros<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>Haga clic en un toorun de elemento de solicitud web de hello web solicitud métrica tendencia que solicitan una búsqueda de registros. |
| Tiempo de respuesta de Web Apps | Muestra un gráfico de líneas del tiempo de respuesta de las aplicaciones Web de hello para el intervalo de fechas de Hola que ha seleccionado. También muestra una lista de una lista de hello veces superior diez Web respuesta de las aplicaciones. Haga clic en hello gráfico toorun una búsqueda de registros de<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> Haga clic en una aplicación Web toorun una búsqueda de registros devuelve tiempos de respuesta de hello Web App. |
| Tráfico de Web Apps | Muestra un gráfico de líneas para el tráfico de las aplicaciones Web, en MB y enumera superior Hola tráfico de las aplicaciones Web. Haga clic en hello gráfico toorun una búsqueda de registros de<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> Muestra todas las aplicaciones Web con tráfico de hello en el último minuto. Haga clic en un toorun de aplicación Web, una búsqueda de registros que muestra los bytes recibidos y enviados para hello Web App. |
| Planes de Azure App Service |   |
| Planes de App Service con un uso de CPU &gt; 80 % | Muestra el número total de Hola de planes de servicio de aplicaciones que tienen mayor que 80% y listas Hola planes de servicio de aplicación de 10 principales mediante el uso de CPU de uso de CPU. Haga clic en toorun del área total de Hola para una búsqueda de registros<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> Muestra una lista de los planes de App Service y su uso de CPU promedio. Haga clic en un Plan de servicio de aplicaciones toorun una búsqueda de registros que muestra su uso promedio de CPU. |
| Planes de App Service con un uso de memoria &gt; 80 % | Muestra el número total de Hola de planes de servicio de aplicaciones que tienen mayor que 80% y listas Hola planes de servicio de aplicación de 10 principales por uso de memoria de uso de memoria. Haga clic en toorun del área total de Hola para una búsqueda de registros<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> Muestra una lista de los planes de App Service y su uso de memoria promedio. Haga clic en un Plan de servicio de aplicaciones toorun una búsqueda de registros que muestra la utilización media de memoria. |
| Registros de actividad de Azure Web Apps |   |
| Auditoría de actividad de Azure Web Apps | Muestra el número total de las aplicaciones Web con Hola [registros de actividad](log-analytics-activity.md) y listas de hello las operaciones de registro de actividad de 10 mejores. Haga clic en toorun del área total de Hola para una búsqueda de registros<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> Muestra una lista de hello las operaciones de registro de actividad. Haga clic en una operación de registro actividad toorun una búsqueda de registros que enumera los registros de hello para la operación de Hola. |



### <a name="azure-web-apps"></a>Aplicaciones web de Azure 

En el panel de hello, puede explorar en profundidad tooget comprender mejor las métricas de las aplicaciones Web. Este primer conjunto de módulos de mostrar la tendencia de Hola de solicitudes de aplicaciones Web de hello, número de errores (por ejemplo, HTTP404), el tráfico y el tiempo medio de respuesta con el tiempo. También muestra un desglose de esas métricas para las diferentes Web Apps.

![Hojas de Azure Web Apps](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

La razón principal para mostrar esos datos es para que pueda identificar una aplicación Web con alto tiempo de respuesta e investigar la causa raíz de toofind Hola. Un límite de umbral también es toohelp aplicado es que más fácil de identificar Hola aquellos problemas.

- Las instancias de Web Apps que se muestran en rojo tienen un tiempo de respuesta superior a 1 segundo.
- Las instancias de Web Apps que se muestran en color naranja tienen un tiempo de respuesta superior a 0,7 segundos e inferior a 1 segundo.
- Las instancias de Web Apps que se muestran en verde tienen un tiempo de respuesta inferior a 0,7 segundos.

Hola después de la imagen de ejemplo de búsqueda de registro, puede ver que hello *anugup3* aplicación web tenía un tiempo de respuesta mucho mayor de Hola a otras aplicaciones web.

![ejemplo de búsqueda de registros](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>Planes del Servicio de aplicaciones

Si está usando planes de servicio dedicados, también puede recopilar métricas para los planes de App Service. En esta vista, verá los planes de App Service con un uso intensivo de CPU o memoria (&gt; 80 %). También muestra Hola superiores servicios de aplicaciones con un uso intensivo de memoria o CPU. De forma similar, un límite de umbral es toohelp aplicado es que más fácil de identificar Hola aquellos problemas.

- Los planes de App Service que se muestran en rojo tienen un uso de CPU/memoria superior al 80 %.
- Los planes de App Service que se muestran en naranja tienen un uso de CPU/memoria superior al 60 % e inferior al 80 %.
- Los planes de App Service que se muestran en verde tienen un uso de CPU/memoria inferior al 60 %.

![Hojas de planes de Azure App Service](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Búsquedas de registros de Azure Web Apps

Hola **consultas de lista de búsqueda más conocidos Azure Web aplicaciones** muestra todos los Hola relacionadas con los registros de actividad para las aplicaciones Web, que proporcionan información sobre las operaciones de Hola que se realizaron en los recursos de aplicaciones Web. También se muestran todos los Hola relacionados con las operaciones y el número de Hola de veces que se hayan ejecutado.

Con cualquiera de las consultas de búsqueda de registros de hello como punto de partida, puede crear fácilmente una alerta. Por ejemplo, puede toocreate una alerta cuando el tiempo de respuesta promedio de una métrica es mayor que 1 segundo.

## <a name="next-steps"></a>Pasos siguientes

- Cree un [alerta](log-analytics-alerts-creating.md) para una métrica específica.
- Use [Log Search](log-analytics-log-searches.md) tooview obtener información de los registros de actividad.
