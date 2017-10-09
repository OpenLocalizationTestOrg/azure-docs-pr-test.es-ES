---
title: "aaaView actividad de Azure se registra con análisis de registros | Documentos de Microsoft"
description: "Puede usar Hola tooanalyze de solución de los registros de actividad de Azure y registro de actividad de Azure de Hola de búsqueda en todas sus suscripciones de Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Ver los registros de actividad de Azure

![Símbolo de registros de actividad de Azure](./media/log-analytics-activity/activity-log-analytics.png)

Hola soluciones de análisis de registros de actividad le ayuda a analizar y buscar hello [registro de actividad de Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) en todas sus suscripciones de Azure. Hola registro de actividad de Azure es un registro que proporciona información sobre las operaciones de hello realizadas en recursos de sus suscripciones. Hello registro de actividad se denominaba anteriormente *los registros de auditoría* o *registros operativos* desde que notifica los eventos de las suscripciones.

Gracias a Hola registro de actividad, puede determinar hello *qué*, *que*, y *cuando* para cualquier operaciones de escritura (PUT, POST, DELETE) realizadas para los recursos de hello en su suscripción. También puede entender el estado Hola de operaciones de Hola y otras propiedades relevantes. Hola registro de actividad no incluye read operaciones (GET) o las operaciones de recursos que usan el modelo de implementación de hello clásico.

Cuando se conecta el tooLog de registros de actividad de Azure análisis, hacer lo siguiente:

- Analizar los registros de actividad de hello con vistas predefinidas
- Analizar y buscar en los registros de actividad de varias suscripciones de Azure
- Conservar registros de actividad durante más de 90 días<sup>1</sup>
- Correlacionar registros de actividad con otros datos de plataforma y aplicación de Azure
- Ver las actividades operativas agregadas por estado
- Ver las tendencias de las actividades que se producen en cada uno de los servicios de Azure
- Informar sobre los cambios de autorización en todos los recursos de Azure
- Identificar problemas de corte de suministro o estado del servicio que afecten a los recursos
- Usar actividades de usuario de toocorrelate de búsqueda de registros, las operaciones de escala automática, cambios de autorización y registros tooother del servicio de mantenimiento o las métricas de su entorno

<sup>1</sup>de forma predeterminada, análisis de registros conserva los registros de actividad de Azure durante 90 días, incluso si se encuentra en el nivel gratis Hola. O bien, si tiene una configuración de retención de área de trabajo de menos de 90 días. Si el área de trabajo que tenga una retención que tiene más de 90 días, registros de actividad de Hola se conservan durante el período de retención de hello del área de trabajo.

Análisis de registros recopila registros de actividad de forma gratuita y almacena los registros de Hola durante 90 días de forma gratuita. Si almacena los registros durante más de 90 días, incurrirá en cargos de retención de datos para los datos de hello almacenados durante más de 90 días.

Cuando esté en hello gratis el nivel de precios, registros de actividad no aplican tooyour Diario consumo de datos.

## <a name="connected-sources"></a>Orígenes conectados

A diferencia de la mayoría de las demás soluciones Log Analytics, los agentes no recopilan datos de los registros de actividad. Todos los datos utilizados por la solución de hello proceden directamente de Azure.

| Origen conectado | Compatible | Descripción |
| --- | --- | --- |
| [Agentes de Windows](log-analytics-windows-agents.md) | No | solución de Hello no recopila información de agentes de Windows. |
| [Agentes de Linux](log-analytics-linux-agents.md) | No | solución de Hello no recopilar información de agentes de Linux. |
| [Grupo de administración de SCOM](log-analytics-om-agents.md) | No | solución de Hello no recopila información de agentes en un grupo de administración de SCOM conectado. |
| [Cuenta de Almacenamiento de Azure](log-analytics-azure-storage.md) | No | solución de Hello no recopila información del almacenamiento de Azure. |

## <a name="prerequisites"></a>Requisitos previos

- tooaccess información del registro de actividad de Azure, debe tener una suscripción de Azure.

## <a name="configuration"></a>Configuración

Realizar Hola después de la solución de análisis de registros de actividad de pasos tooconfigure Hola para las áreas de trabajo.

1. Habilitar la solución de análisis de registros de actividad de Hola de hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. Configurar el área de trabajo de actividad registros toogo tooyour análisis de registros.
    1. En Hola portal de Azure, seleccione el área de trabajo y, a continuación, haga clic en **registro de actividad de Azure**.
    2. Para cada suscripción, haga clic en el nombre de la suscripción de Hola.  
        ![agregar suscripción](./media/log-analytics-activity/add-subscription.png)
    3. Hola *SubscriptionName* hoja, haga clic en **conectar**.  
        ![conectar suscripción](./media/log-analytics-activity/subscription-connect.png)

Si agrega solución hello mediante Hola portal OMS, verá icono Hola siguiente. Inicie sesión en toohello tooconnect portal Azure un área de trabajo de tooyour de suscripción de Azure.  
![realizar una evaluación](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Uso de solución de Hola

Cuando se agrega el área de trabajo tooyour soluciones de análisis de registros de actividad de hello, Hola **los registros de actividad de Azure** es agregar el icono de panel de información general de tooyour. Este icono muestra un recuento del número de Hola de registros de actividad de Azure para hello las suscripciones de Azure que Hola solución tiene el acceso a.

![Icono Registros de actividad de Azure](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Ver los registros de actividad de Azure

Haga clic en hello **los registros de actividad de Azure** icono tooopen hello **los registros de actividad de Azure** panel. panel de Hello incluye módulos de hello en hello en la tabla siguiente. Cada hoja se enumera los elementos de too10 coincidentes que han especificado criterios del módulo para hello ámbito y el tiempo de intervalo. Puede ejecutar una búsqueda de registros que devuelve todos los registros, haga clic en **ver todas** en parte inferior de la hoja de Hola o haciendo clic en el encabezado de la hoja de Hola de Hola.

Datos del registro de actividad solo aparecen *después* ha configurado la solución de toohello toogo de registros de actividad, por lo que no se puede ver los datos antes, a continuación.

| Hoja | Descripción |
| --- | --- |
| Entradas del registro de actividad de Azure | Muestra un gráfico de barras principales Hola entrada de registro de actividad de Azure registros totales de intervalo de fechas de Hola que ha seleccionado y muestra una lista de hello llamadores de actividad 10 superior. Haga clic en Hola gráfico de barras toorun una búsqueda de registros para <code>Type=AzureActivity</code>. Haga clic en un toorun de elemento de llamador una búsqueda de registros devuelve todas las entradas de registro de actividad para ese elemento. |
| Registros de actividad por estado | Muestra un gráfico de anillos para el estado de registro de actividad de Azure para el intervalo de fechas de Hola que ha seleccionado. También muestra una lista en una lista de registros de estado diez principales Hola. Haga clic en hello gráfico toorun una búsqueda de registros para <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Haga clic en un toorun de elemento de estado una búsqueda de registros devuelve todas las entradas de registro de actividad para ese registro de estado. |
| Registros de actividad por recurso | Muestra el número total de Hola de recursos con registros de actividad y muestra la parte superior de hello diez recursos con registro de cuenta para cada recurso. Haga clic en hello superficie total toorun una búsqueda de registros para <code>Type=AzureActivity &#124; measure count() by Resource</code>, que muestra todos los recursos de Azure solución toohello disponible. Haga clic en un recurso toorun una búsqueda de registros devuelve todos los registros de actividad para ese recurso. |
| Registros de actividad por proveedor de recursos | Muestra hello el número total de proveedores de recursos que producen actividad registra y muestra los diez primeros de Hola. Haga clic en hello superficie total toorun una búsqueda de registros para <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, que muestra todos los proveedores de recursos de Azure. Haga clic en un toorun de proveedor de recursos una búsqueda de registros devuelve todos los registros de actividad para el proveedor de Hola. |

![Panel Registros de actividad de Azure](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Pasos siguientes

- Cree una [alerta](log-analytics-alerts-creating.md) cuando se produzca una actividad determinada.
- Use [Log Search](log-analytics-log-searches.md) tooview obtener información de los registros de actividad.
