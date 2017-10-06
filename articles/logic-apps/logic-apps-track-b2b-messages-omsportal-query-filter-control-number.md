---
title: "aaaQuery para los mensajes B2B en Operations Management Suite: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: Crear consultas tootrack AS2, X 12 y EDIFACT mensajes de Hola Operations Management Suite
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>Consultar AS2, X 12 y EDIFACT mensajes de Hola Microsoft Operations Management Suite (OMS)

Hola toofind AS2, X 12 o mensajes EDIFACT que está realizando el seguimiento con [Azure Log Analytics](../log-analytics/log-analytics-overview.md) en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), puede crear consultas que filtran acciones basadas en específica criterios. Por ejemplo, puede encontrar mensajes según un número de control de intercambio específico.

## <a name="requirements"></a>Requisitos

* Una aplicación lógica configurada con registro de diagnósticos. Obtenga información acerca de [cómo una aplicación de la lógica de toocreate](../logic-apps/logic-apps-create-a-logic-app.md) y [cómo tooset el registro para esa aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Una cuenta de integración configurada con supervisión y registro. Obtenga información acerca de [cómo toocreate una cuenta de integración](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) y [cómo tooset supervisión y registro para esa cuenta](../logic-apps/logic-apps-monitor-b2b-message.md).

* Si no lo ha hecho ya, [publicar datos de diagnóstico tooLog análisis](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) y [configurar el seguimiento de mensajes en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> Después de que cumple los requisitos anteriores de hello, debe tener un área de trabajo en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Debe usar Hola la misma área de trabajo OMS para realizar el seguimiento de la comunicación B2B de OMS. 
>  
> Si no tiene un área de trabajo OMS, descubra [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Crear consultas de mensaje con los filtros en el portal de Operations Management Suite Hola

En este ejemplo se muestra cómo puede buscar mensajes según su número de control de intercambio.

> [!TIP] 
> Si conoce el nombre del área de trabajo OMS, ir a página de inicio de área de trabajo de tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) e iniciar en el paso 4. De lo contrario, empiece en el paso 1.

1. Hola [portal de Azure](https://portal.azure.com), elija **más servicios**. Busque "log analytics" y luego elija **Log Analytics** como se muestra aquí:

   ![Búsqueda de Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. En **Log Analytics**, busque y seleccione el área de trabajo de OMS.

   ![Selección del área de trabajo de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. En **Administración**, elija **Portal de OMS**.

   ![Selección de Portal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. En la página principal de OMS, seleccione **Búsqueda de registros**.

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   O bien

   ![En el menú OMS de hello, elija "Búsqueda de registros"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. En el cuadro de búsqueda de hello, escriba un campo que desea que toofind y presione **ENTRAR**. Cuando empiece a escribir, OMS le mostrará posibles coincidencias y operaciones que puede usar. Obtenga más información sobre [cómo toofind datos de análisis de registros](../log-analytics/log-analytics-log-searches.md).

   En este ejemplo se buscan eventos con **Type=AzureDiagnostics**.

   ![Empezar a escribir la cadena de consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. En la barra de la izquierda hello, elija el período de tiempo de Hola que desea tooview. tooadd una consulta de tooyour filtro, elija **+ agregar**.

   ![Agregar filtro tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. En **agregar filtros**, escriba el nombre de filtro de Hola para que pueda encontrar el filtro de Hola que desee. Seleccione el filtro de Hola y elija **+ agregar**.

   número de control de intercambio de hello toofind, este ejemplo busca palabra Hola "intercambio" y selecciona **event_record_messageProperties_interchangeControlNumber_s** como filtro de Hola.

   ![Selección de filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. En la barra de la izquierda hello, seleccione el valor de filtro de Hola que desee toouse y elija **aplicar**.

   Este ejemplo selecciona el número de control de intercambio de Hola para los mensajes de Hola que deseamos.

   ![Selección de valor de filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. Consulta de toohello devuelven ahora que va a compilar. La consulta se actualizó con el valor y el evento de filtro seleccionados. Los resultados anteriores también se filtraron.

    ![Devolver tooyour consulta con los resultados filtrados](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Guardar la consulta para futuro uso

1. De la consulta en hello **Log Search** página, elija **guardar**. Asigne un nombre a la consulta, seleccione una categoría y elija **Guardar**.

   ![Asignación de nombre y categoría a la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview la consulta, elija **favoritos**.

   ![Elegir "Favoritos"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. En **búsquedas guardadas**, seleccione la consulta para que pueda ver los resultados de Hola. consulta de hello tooupdate para que pueda encontrar resultados diferentes, en Editar consulta Hola.

   ![Selección de la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>Buscar y ejecutar las consultas guardadas en el portal de Operations Management Suite Hola

1. Abra la página principal del área de trabajo de OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) y elija **Búsqueda de registros**.

   ![Selección de "Búsqueda de registros" en la página principal de OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   O bien

   ![En el menú OMS de hello, elija "Búsqueda de registros"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. En hello **Log Search** página principal, elija **favoritos**.

   ![Elegir "Favoritos"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. En **búsquedas guardadas**, seleccione la consulta para que pueda ver los resultados de Hola. consulta de hello tooupdate para que pueda encontrar resultados diferentes, en Editar consulta Hola.

   ![Selección de la consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Pasos siguientes

* [Esquemas de seguimiento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Esquemas de seguimiento de X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Esquemas de seguimiento personalizados](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)