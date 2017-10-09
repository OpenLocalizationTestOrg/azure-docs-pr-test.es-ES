---
title: "solución de análisis de SQL de análisis de registros aaaAzure | Documentos de Microsoft"
description: "Hola solución de análisis de SQL Azure le ayuda a administrar las bases de datos de SQL Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Supervisión de Azure SQL Database mediante Azure SQL Analytics (versión preliminar) en Log Analytics

![Símbolo de Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Hola soluciones de análisis de SQL Azure en Azure Log Analytics recopila y muestra las métricas de rendimiento importantes de SQL Azure. Mediante el uso de las métricas de Hola que se recopilan con soluciones de hello, puede crear alertas y reglas de supervisión personalizadas. Y puede supervisar Azure SQL Database y las métricas de los grupos elásticos de varias suscripciones y grupos elásticos de Azure y visualizarlos. solución de Hello también ayuda a problemas de tooidentify en cada nivel de la pila de la aplicación.  Usa [métricas de diagnóstico de Azure](log-analytics-azure-storage.md) junto con el análisis de registros ve toopresent datos sobre todas las bases de datos SQL de Azure y los grupos elásticos en una sola área de trabajo de análisis de registros.

Actualmente, esta solución de vista previa admite hasta too150 000 bases de datos de SQL Azure y 5.000 grupos elásticos SQL por área de trabajo.

Hola soluciones de análisis de SQL Azure, al igual que otras personas disponibles para el análisis de registros, le ayuda a supervisar y recibir notificaciones sobre el estado de saludo de los recursos de Azure, en este caso, la base de datos de SQL Azure. Base de datos de SQL de Microsoft Azure es un servicio de base de datos relacional escalable que ofrece familiarizado tooapplications de capacidades de tipo de servidor de SQL ejecuta Hola nube de Azure. Análisis de registros permite toocollect, correlacionar y visualizar los datos estructurados y no estructurados.

## <a name="connected-sources"></a>Orígenes conectados

Hola solución de análisis de SQL Azure no usa agentes tooconnect toohello servicio de análisis de registros.

Hello en la tabla siguiente describe los orígenes de hello conectado que son compatibles con esta solución.

| Origen conectado | Soporte técnico | Descripción |
| --- | --- | --- |
| [Agentes de Windows](log-analytics-windows-agents.md) | No | Solución de hello no se utiliza agentes directa de Windows. |
| [Agentes de Linux](log-analytics-linux-agents.md) | No | No se utilizan agentes Linux directa solución Hola. |
| [Grupo de administración de SCOM](log-analytics-om-agents.md) | No | No se utiliza una conexión directa de hello SCOM agente tooLog análisis solución Hola. |
| [Cuenta de Almacenamiento de Azure](log-analytics-azure-storage.md) | No | Análisis de registros no leen datos de Hola desde una cuenta de almacenamiento. |
| [Diagnóstico de Azure](log-analytics-azure-storage.md) | Sí | Se envían datos de métrica Azure tooLog Analytics directamente en Azure. |

## <a name="prerequisites"></a>Requisitos previos

- Una suscripción de Azure. Si no tiene ninguna, puede crear una [gratis](https://azure.microsoft.com/free/).
- Un área de trabajo de Log Analytics. Puede usar una existente, o bien puede [crear una nueva](log-analytics-get-started.md) para empezar a usar esta solución.
- Habilitar los diagnósticos de Azure para sus bases de datos SQL de Azure y los grupos elásticos y [configurarlos toosend su análisis de datos tooLog](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Configuración

Realizar Hola después de área de trabajo tooyour de solución de análisis de SQL Azure de pasos tooadd Hola.

1. Agregar área de trabajo de hello análisis de SQL Azure solución tooyour de [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. Hola portal de Azure, haga clic en **New** (símbolo + hello), a continuación, en lista Hola de recursos, seleccione **supervisión + administración**.  
    ![Supervisión + Administración](./media/log-analytics-azure-sql/monitoring-management.png)
3. Hola **supervisión + administración** lista, haga clic **ver todas**.
4. Hola **recomendado** lista, haga clic en **más** y, a continuación, en la nueva lista de hello, busque **análisis de SQL Azure (vista previa)** y, a continuación, selecciónelo.  
    ![Solución Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. Hola **análisis de SQL Azure (vista previa)** hoja, haga clic en **crear**.  
    ![Creación](./media/log-analytics-azure-sql/portal-create.png)
6. Hola **crear nueva solución** hoja, área de trabajo de hello select que desea tooadd Hola solución tooand, a continuación, haga clic en **crear**.  
    ![Agregar tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure varias suscripciones de Azure

toosupport varias suscripciones, use el script de PowerShell de Hola desde [registro de las métricas de recursos de habilitar Azure mediante PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Proporcionar Id. de recurso del área de trabajo de Hola como un parámetro al ejecutar los datos de diagnóstico toosend hello secuencia de comandos de recursos del área de trabajo de una suscripción de Azure tooa en otra suscripción de Azure.

**Ejemplo**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>Uso de solución de Hola

Cuando se agrega el área de trabajo de hello solución tooyour, Hola icono de análisis de SQL Azure se agrega el área de trabajo de tooyour y aparece en información general. icono de Hello muestra hello de bases de datos SQL de Azure y grupos elásticos SQL de Azure que Hola solución está conectada a.

![Icono de Azure SQL Analytics](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Visualización de los datos de Azure SQL Analytics

Haga clic en hello **el análisis de SQL Azure** icono tooopen Hola o panel de análisis de SQL Azure. panel de Hello incluye módulos de hello definidas a continuación. Cada hoja se enumera los recursos de too15 (suscripción, server, grupo elástico y base de datos). Haga clic en cualquier panel de Hola Hola recursos tooopen para ese recurso específico. Base de datos o grupo elástico contiene gráficos de hello con métricas para un recurso seleccionado. Haga clic en un cuadro de diálogo de búsqueda de registros de gráfico tooopen Hola.

| Hoja | Descripción |
|---|---|
| Suscripciones | Lista de las suscripciones con el número de servidores conectados, los grupos y las bases de datos. |
| Servidores | Lista de servidores con el número de grupos conectados y las bases de datos. |
| Grupos elásticos | Lista de grupos elásticos conectados con máximo GB y eDTU Hola observados período. |
|Bases de datos | Lista de bases de datos conectadas con máximo GB y DTU en hello observados período.|


### <a name="analyze-data-and-create-alerts"></a>Análisis de datos y creación de alertas

Puede crear fácilmente alertas con datos de hello procedentes de recursos de base de datos de SQL Azure. Estas son un par de consultas de [búsqueda de registros](log-analytics-log-searches.md) útiles que puede usar para las alertas:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*DTU alta en Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*DTU alta en el grupo elástico de Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

Puede usar estos tooalert de las consultas basadas en la alerta en umbrales específicos para la base de datos de SQL Azure y grupos elásticos. tooconfigure una alerta para el área de trabajo OMS:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure una alerta para el área de trabajo

1. Vaya toohello [portal de OMS](http://mms.microsoft.com/) e inicie sesión.
2. Abra el área de trabajo de Hola que ha configurado para la solución de Hola.
3. En la página de información general de hello, haga clic en hello **análisis de SQL Azure (vista previa)** icono.
4. Ejecute una de las consultas de ejemplo de Hola.
5. En Búsqueda de registros, haga clic en **Alerta**.  
![crear alerta en la búsqueda](./media/log-analytics-azure-sql/create-alert01.png)
6. En hello **Agregar regla de alerta** página, configure las propiedades adecuadas de Hola y Hola umbrales específicos que desee y, a continuación, haga clic en **guardar**.  
![agregar regla de alerta](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Actuar sobre los datos de Azure SQL Analytics

Por ejemplo, una de las consultas más útiles Hola que puede realizar es uso de la DTU toocompare Hola para todos los grupos de elástico de SQL Azure en todas sus suscripciones de Azure. Unidad de rendimiento de base de datos (DTU) proporciona una manera toodescribe Hola capacidad relativa de un nivel de rendimiento de las bases de datos Basic, Standard y Premium y grupos. Las DTU se basan en una medición combinada de CPU, memoria y número de lecturas y escrituras. A medida que aumentan las Dtu, Hola potencia que ofrece aumenta de nivel de rendimiento de Hola. Por ejemplo, un nivel de rendimiento con 5 DTU es cinco veces más potente que un nivel de rendimiento con 1 DTU. Una cuota DTU máxima aplica tooeach grupo de servidor y flexible.

Al ejecutar Hola después de consulta de búsqueda de registros, puede indicar fácilmente si están utilizando poco o uso en los grupos elásticos de SQL Azure.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de la consulta cambiaría toohello siguiente.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

En el siguiente ejemplo de Hola, puede ver que un grupo elástico tiene un uso elevado de casi el 100% DTU mientras que otros tienen muy poco uso. Puede investigar más tootroubleshoot posibles cambios recientes en su entorno usando los registros de actividad de Azure.

![Resultados de la búsqueda de registros: uso intensivo](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Otras referencias

- Use [búsquedas de registros](log-analytics-log-searches.md) en tooview de análisis de registros detallados de datos de SQL Azure.
- [Cree sus propios paneles](log-analytics-dashboards.md) que muestren datos de Azure SQL.
- [Cree alertas](log-analytics-alerts.md) cuando se produzcan eventos específicos de Azure SQL.
