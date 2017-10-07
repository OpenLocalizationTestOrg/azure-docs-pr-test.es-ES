---
title: "aaaMonitor y obtener información acerca de la lógica de aplicación se ejecuta con OMS - Azure Logic Apps | Documentos de Microsoft"
description: "Supervisar se ejecuta la aplicación lógica con visión tooget de análisis de registros y Operations Management Suite (OMS) y los detalles de depuración más enriquecidas para solución de problemas y diagnóstico"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Supervise y obtenga información sobre las ejecuciones de aplicación lógica con Operations Management Suite (OMS) y Log Analytics.

Para obtener información de depuración más enriquecida y supervisión, puede activar el análisis de registros en hello vez cuando se crea una aplicación de lógica. Análisis de registros proporciona supervisión para la aplicación lógica y el registro de diagnóstico se ejecuta a través del portal de hello Operations Management Suite (OMS). Cuando se agrega tooOMS de solución de administración de aplicaciones de la lógica de hello, puede ver el estado agregado para sus ejecuciones de aplicación lógica y los detalles específicos como estado, tiempo de ejecución, estado de reenvío y el identificador de correlación.

Este tema muestra cómo tooturn en análisis de registros o instale Hola solución de administración de aplicaciones de la lógica de OMS por lo que puede ver los eventos en tiempo de ejecución y los datos para la aplicación lógica de ejecutarse.

 > [!TIP]
 > toomonitor sus aplicaciones existentes de lógica, siga estos pasos demasiado [activar registro de diagnóstico y enviar tooOMS de datos de tiempo de ejecución de aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Requisitos

Antes de empezar, deberá toohave un área de trabajo OMS. Obtenga información acerca de [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Activación del registro de diagnóstico al crear aplicaciones lógicas

1. En [Azure Portal](https://portal.azure.com), cree una aplicación lógica. Elija **Nueva** > **Enterprise Integration** > **Aplicación lógica** > **Crear**.

   ![Creación de una aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. Hola **crear lógica aplicación** página, lleve a cabo estas tareas como se muestra:

   1. Asigne un nombre a la aplicación lógica y seleccione su suscripción de Azure. 
   2. Cree o seleccione un grupo de recursos de Azure.
   3. Establecer **análisis de registros** demasiado**en**. 
   Área de trabajo OMS de hello SELECT en la que desea enviar demasiado datos para la aplicación lógica se ejecuta. 
   4. Cuando esté listo, elija **Pin toodashboard** > **crear**.

      ![Creación de la aplicación lógica](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Después de realizar este paso, Azure crea la aplicación lógica, que ahora está asociada al área de trabajo de OMS. 
      Además, este paso también instala automáticamente soluciones de administración de aplicaciones de la lógica de hello en el área de trabajo OMS.

3. tooview se ejecuta la aplicación de lógica de OMS, [continúe con estos pasos](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Instalar la solución de administración de aplicaciones de la lógica de Hola de OMS

Si ya activó Log Analytics cuando creó su aplicación lógica, omita este paso. Ya tiene instalada en OMS de solución de administración de aplicaciones de la lógica de Hola.

1. Hola [portal de Azure](https://portal.azure.com), elija **más servicios**. Busque "log analytics" como filtro y elija **Log Analytics** como se muestra:

   ![Selección de "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. En **Log Analytics**, busque y seleccione el área de trabajo de OMS. 

   ![Selección del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. En **Administración**, elija **Portal de OMS**.

   ![Selección de "Portal de OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. En la página principal OMS, si aparece el banner de actualización de hello, elija pancarta Hola para que primero actualizan el área de trabajo OMS. A continuación, elija **Galería de soluciones**.

   ![Selección de "Galería de soluciones"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. En **todas las soluciones**, buscar y elija el icono de Hola para hello **lógica de administración de aplicaciones** solución.

   ![Selección de "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. solución de hello tooinstall en el área de trabajo OMS, seleccione **agregar**.

   ![Selección de "Agregar" en "Logic Apps Management"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Visualización de ejecuciones de aplicación lógica en el área de trabajo de OMS

1. recuento de hello tooview y el estado de la aplicación lógica se ejecuta, vaya toohello página de información general para el área de trabajo OMS. Revise los detalles de hello en hello **lógica de administración de aplicaciones** icono.

   ![Icono de información general que muestra el recuento y el estado de la ejecución de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Si esta actualización pancarta aparece en lugar de icono de administración de aplicaciones de lógica de hello, elija pancarta Hola para que primero actualizan el área de trabajo OMS.
  
   > ![Actualización del área de trabajo de OMS](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview un resumen con más detalles acerca de cómo se ejecuta la aplicación de lógica, elija hello **lógica de administración de aplicaciones** icono.

   En este caso, las ejecuciones de aplicación lógica se agrupan por nombre y estado de ejecución.

   ![Resumen de estado de las ejecuciones de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. tooview que Hola a todos se ejecuta para una aplicación lógica específica o el estado, la fila de hello select para una aplicación de lógica o con el estado.

   Este es un ejemplo que muestra todas las ejecuciones de Hola para una aplicación de la lógica específica:

   ![Visualización de las ejecuciones de una aplicación lógica o el estado](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Hola **reenvío** columna muestra "Sí" para las ejecuciones que son el resultado de una ejecución reenviada.

4. toofilter estos resultados, puede realizar un filtrado de cliente y servidor.

   * El filtro del lado cliente: para cada columna, elija los filtros de Hola que desee. 
   Estos son algunos ejemplos:

     ![Ejemplo de filtros de columna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filtro de servidor: toochoose un hora específica ventana o toolimit Hola el número de ejecuciones que aparecen, usar el control del ámbito de hello al principio de Hola de página de Hola. 
   De forma predeterminada, solo aparecen 1000 registros a la vez. 
   
     ![Cambio de ventana de tiempo de Hola](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. tooview todos los Hola acciones y sus detalles para una ejecución, específica, seleccione una fila, que abre la página de búsqueda de registros de Hola. 

   * Esta información en una tabla, elija a tooview **tabla**.
   * consulta de hello toochange, puede editar cadena de consulta de hello en la barra de búsqueda de Hola. 
   Para una mejor experiencia, elija **Análisis avanzado**.

     ![Visualización de las acciones y los detalles de una ejecución de aplicación lógica](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Aquí en la página de análisis de registros de Azure de hello, puede actualizar las consultas y vista Hola resultante de la tabla de Hola. 
     Esta consulta utiliza [lenguaje de consulta de Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que se puede modificar si desea que los resultados diferentes tooview. 

     ![Azure Log Analytics: vista de consultas](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Pasos siguientes

* [Supervisión de mensajes B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
