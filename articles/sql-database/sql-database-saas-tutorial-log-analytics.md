---
title: "aaaUse análisis de registros con una aplicación de varios inquilinos de la base de datos SQL | Documentos de Microsoft"
description: "Configurar y usar el análisis de registros (OMS) con la aplicación de SaaS Wingtip de ejemplo de Hola base de datos de SQL Azure"
keywords: tutorial de SQL Database
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>Configurar y usar el análisis de registros (OMS) con la aplicación de SaaS Wingtip hello

En este tutorial, instalaremos y usaremos *Log Analytics ([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* para supervisar bases de datos y grupos elásticos. Se basa en hello [tutorial de administración y supervisión del rendimiento](sql-database-saas-tutorial-performance-monitoring.md)y muestra cómo toouse *análisis de registros* tooaugment Hola supervisión y alertas que se proporcionan en hello portal de Azure. Log Analytics es especialmente adecuado para la supervisión y las alertas de escalado, ya que admite cientos de grupos y cientos de miles de bases de datos. También proporciona una única solución de supervisión, que puede integrar la supervisión de distintas aplicaciones y servicios de Azure en varias suscripciones de Azure.

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Instalar y configurar Log Analytics (OMS)
> * Usar bases de datos y grupos de toomonitor de análisis de registros

toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

* se implementa la aplicación de SaaS Wingtip Hello. vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

Vea hello [tutorial de administración y supervisión del rendimiento](sql-database-saas-tutorial-performance-monitoring.md) para obtener una descripción de escenarios de SaaS hello y patrones y cómo afectan a los requisitos de hello en una solución de supervisión.

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>Supervisión y administración del rendimiento con Log Analytics (OMS)

Para SQL Database, la supervisión y las alertas están disponibles para las bases de datos y los grupos. Este integradas de supervisión y alerta es específico del recurso y adecuada para pequeñas cantidades de recursos, pero es menos toomonitoring idóneo instalaciones de gran tamaño o para proporcionar una vista unificada a través de suscripciones y los distintos recursos.

Para escenarios de gran volumen, puede utilizarse Log Analytics. Se trata de un servicio de Azure independiente que proporciona análisis con respecto a los registros de diagnóstico emitidos y telemetría recopilado en un área de trabajo de análisis de registro, que puede recopilar la telemetría de muchos servicios y ser tooquery usado y establece alertas. Log Analytics proporciona herramientas de visualización de los datos y lenguaje de consulta integrados para el análisis y la visualización de datos operativos. Hola solución de análisis de SQL proporciona varias grupo elástico predefinido y base de datos de supervisión y alerta vistas y consultas y le permite agregar sus propias consultas ad hoc y guardar estos según sea necesario. OMS también ofrece un diseñador de vistas personalizadas.

Soluciones de áreas de trabajo y análisis de análisis de registro se pueden abrir en el portal de Azure de Hola y de OMS. Hola portal de Azure es el punto de acceso más reciente de hello, pero puede estar detrás de portal de OMS de hello en algunas áreas.

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>Iniciar Hola carga generador toocreate datos tooanalyze

1. Abra **demostración PerformanceMonitoringAndManagement.ps1** en hello **PowerShell ISE**. Mantenga esta secuencia de comandos abierta como desee toorun varios escenarios de generación de carga de Hola durante este tutorial.
1. Si tiene menos de cinco inquilinos, el aprovisionamiento de un lote de los inquilinos tooprovide un contexto de supervisión más interesante:
   1. Establezca **$DemoScenario = 1,** **Aprovisionamiento de un lote de inquilinos**
   1. Presione **F5** secuencia de comandos de toorun Hola.

1. Establezca **$DemoScenario** = 2, **Generación de una carga de intensidad normal (aprox. 40 DTU)**.
1. Presione **F5** secuencia de comandos de toorun Hola.

## <a name="get-hello-wingtip-application-scripts"></a>Obtener scripts de la aplicación hello Wingtip

Hello las secuencias de comandos de vales de Wingtip y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. Archivos de script se encuentran en hello [carpeta módulos de aprendizaje](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules). Descargar hello **módulos de aprendizaje** carpeta tooyour ordenador, mantener su estructura de carpetas.

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>Instalar y configurar hello solución de análisis de SQL Azure y análisis de registros

Análisis de registros es un servicio independiente que necesita toobe configurado. Log Analytics recopila datos del registro, y telemetría y métricas de un área de trabajo de análisis de registros. Un área de trabajo es un recurso y debe crearse, como otros de Azure. Mientras que el área de trabajo de hello no necesita toobe creado en hello mismo grupo de recursos como aplicaciones de Hola que está supervisando, esto suele tener sentido Hola mayoría. En caso de hello de aplicación de SaaS Wingtip hello, esto permite toobe de área de trabajo de hello eliminado fácilmente con la aplicación hello mediante la simple eliminación de grupo de recursos de Hola.

1. Abra... \\Módulos de aprendizaje\\administración y supervisión del rendimiento\\análisis de registros\\*demostración LogAnalytics.ps1* en hello **PowerShell ISE**.
1. Presione **F5** secuencia de comandos de toorun Hola.

En este momento debe ser capaz de análisis de registros abierto de portal de Azure de hello (o portal de OMS hello). Tardará unos minutos para toobe de telemetría recopilados en el área de trabajo de análisis de registros de Hola y toobecome visible. será Hello más que deje sistema Hola recopilar datos Hola experiencia de hello más interesante. Ahora es un buen momento toograb una bebida - simplemente asegúrese de que todavía se está ejecutando generador de carga de Hola!


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>Usar el análisis de registro y Hola bases de datos y grupos de toomonitor de solución de análisis de SQL


En este ejercicio, abra toolook de portal de OMS de hello en telemetría de Hola que se va a recopilar para los grupos y las bases de datos de Hola y de análisis de registros.

1. Examinar toohello [portal de Azure](https://portal.azure.com) y abra análisis de registros haciendo clic en servicios más, a continuación, busque el análisis de registros:

   ![apertura de Log Analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. Seleccionar área de trabajo de hello denominado *wtploganalytics -&lt;usuario&gt;*.

1. Seleccione **Introducción** tooopen Hola soluciones de análisis de registros en hello portal de Azure.
   ![vínculo a la introducción](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **IMPORTANTE**: puede tardar unos minutos antes de solución de hello está activo. Tenga paciencia.

1. Haga clic en hello tooopen de icono de análisis de SQL Azure.

    ![Información general](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![análisis](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. Hola vista en hello solución hoja se desplaza lateralmente, con su propia barra de desplazamiento final hello (actualización Hola hoja si es necesario).

1. Explorar Hola varias vistas haciendo clic en ellos o en los recursos individuales tooopen un exploración en profundidad el explorador, donde se puede utilizar el control deslizante horario de Hola Hola arriba a la izquierda o haga clic en vertical toofocus en la barra en un intervalo de tiempo más estrecho. Con esta vista, puede seleccionar toofocus individuales de las bases de datos o grupos de recursos específicos:

    ![gráfico](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. En la hoja de la solución de hello, si se desplaza toohello derecha verá algunas consultas guardadas que puede hacer clic en tooopen y explorar. Puede experimentar modificándolas y guardar las consultas interesantes que genere para después volver a abrirlas y usarlas con otros recursos.

1. En la hoja de área de trabajo de análisis de registros de hello, seleccione solución de Hola de tooopen de Portal de OMS no existe.

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. Portal de OMS de hello, puede configurar alertas. Haga clic en la parte de alerta de Hola de vista DTU de base de datos de Hola.

1. Hola búsqueda de registros que aparece, verá un gráfico de barras de las métricas de hello representados.

    ![búsqueda de registros](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. Si hace clic en la alerta en la barra de herramientas de hello será capaz de toosee configuración de alertas de Hola y puede cambiarlo.

    ![incorporación de regla de alerta](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

Hola de supervisión y alerta de análisis de registros y OMS se basa en las consultas sobre datos de hello en el área de trabajo de hello, a diferencia de hello las alertas relacionadas con cada hoja de recursos, que es específico del recurso. Por lo tanto, puede definir una alerta que se busque en todas las bases de datos, por ejemplo, en lugar de definir una por cada base de datos. También puede escribir una alerta que use una consulta compuesta para varios tipos de recursos. Las consultas sólo están limitadas por los datos de hello disponibles en el área de trabajo de Hola.

Análisis de registros de base de datos de SQL se cobran por basándose en el volumen de datos de hello en el área de trabajo de Hola. En este tutorial, creó un área de trabajo gratuita, que es too500MB limitado por día. Una vez alcanzado ese límite de datos ya no se agregan toohello área de trabajo.


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Instalar y configurar Log Analytics (OMS)
> * Usar bases de datos y grupos de toomonitor de análisis de registros

[Tutorial sobre el análisis de inquilinos](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>Recursos adicionales

* [Tutoriales adicionales que se basan en la implementación de aplicaciones de SaaS Wingtip inicial Hola](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
