---
title: "las transacciones de aaaMonitor B2B y configurar el registro: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Supervisión de mensajes AS2, X12 y EDIFACT, inicio del registro de diagnóstico para la cuenta de integración"
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
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>Supervisión y configuración del registro de diagnóstico para la comunicación B2B en cuentas de integración

Después de configurar la comunicación B2B entre dos procesos o aplicaciones empresariales mediante la cuenta de integración, esas entidades pueden intercambiar mensajes entre sí. tooconfirm esta comunicación funciona según lo previsto, puede configurar la supervisión de AS2, X12, y mensajes EDIFACT, junto con el registro de diagnósticos para su cuenta de integración a través de hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) servicio. Este servicio en [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) supervisa los entornos locales y en la nube, lo que le permiten conservar la disponibilidad y el rendimiento, y también recopila detalles de entorno de tiempo de ejecución y eventos para lograr una depuración más completa. También puede [usar los datos de diagnóstico con otros servicios](#extend-diagnostic-data), como Azure Storage y Azure Event Hubs.

## <a name="requirements"></a>Requisitos

* Una aplicación lógica configurada con registro de diagnósticos. Obtenga información acerca de [cómo tooset el registro para esa aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

  > [!NOTE]
  > Después de que se ha cumplido este requisito, debe tener un área de trabajo en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Debe usar Hola la misma área de trabajo OMS al configurar el registro para la cuenta de integración. Si no tiene un área de trabajo OMS, descubra [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).

* Una cuenta de integración que se ha vinculado la aplicación lógica de tooyour. Obtenga información acerca de [cómo toocreate la integración de una cuenta con una aplicación de lógica de vínculo tooyour](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>Activación del registro de diagnóstico para la cuenta de integración

Puede activar el registro directamente desde su cuenta de integración o [a través de hello Azure supervisar servicio](#azure-monitor-service). Azure Monitor ofrece supervisión básica con datos de nivel de infraestructura. Más información sobre [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>Activación del registro de diagnóstico directamente desde la cuenta de integración

1. Hola [portal de Azure](https://portal.azure.com), busque y seleccione su cuenta de integración. En **Supervisión**, elija **Registros de diagnóstico** como se muestra a continuación:

   ![Buscar y seleccionar la cuenta de integración, elegir "Registros de diagnóstico"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. Después de seleccionar su cuenta de integración, Hola después de los valores se selecciona automáticamente. Si los valores son correctos, elija **Activar diagnóstico**. También puede seleccionar valores de hello que desee:

   1. En **suscripción**, seleccione Hola suscripción de Azure que se utiliza con su cuenta de integración.
   2. En **grupo de recursos**, seleccione grupo de recursos de Hola que se utiliza con su cuenta de integración.
   3. En **Tipo de recurso**, seleccione **Cuentas de integración**. 
   4. En **Resource**, seleccione la cuenta de integración. 
   5. Elija **Activar diagnóstico**.

   ![Configuración de diagnósticos para la cuenta de integración](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. En **Configuración de diagnóstico**, **Estado**, elija **Activado**.

   ![Activación de Diagnósticos de Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Ahora seleccione toouse de área de trabajo y los datos OMS de hello para el registro como se muestra:

   1. Seleccione **enviar tooLog análisis**. 
   2. En **Log Analytics**, elija **Configurar**. 
   3. En **áreas de trabajo de OMS**, seleccione toouse de área de trabajo OMS de hello para el registro.
   4. En **registro**, seleccione hello **IntegrationAccountTrackingEvents** categoría.
   5. Elija **Guardar**.

   ![Configurar el análisis de registros para poder enviar registros de tooa de datos de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Ahora [configure el seguimiento de los mensajes B2B en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>Activación del registro de diagnóstico mediante Azure Monitor

1. Hola [portal de Azure](https://portal.azure.com), en Hola menú principal de Azure, elija **Monitor**, **registros de diagnóstico**. Luego, seleccione la cuenta de integración como se muestra aquí:

   ![Elija "Supervisar", "Registros de diagnóstico", seleccione la cuenta de integración.](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. Después de seleccionar su cuenta de integración, Hola después de los valores se selecciona automáticamente. Si los valores son correctos, elija **Activar diagnóstico**. También puede seleccionar valores de hello que desee:

   1. En **suscripción**, seleccione Hola suscripción de Azure que se utiliza con su cuenta de integración.
   2. En **grupo de recursos**, seleccione grupo de recursos de Hola que se utiliza con su cuenta de integración.
   3. En **Tipo de recurso**, seleccione **Cuentas de integración**.
   4. En **Resource**, seleccione la cuenta de integración.
   5. Elija **Activar diagnóstico**.

   ![Configuración de diagnósticos para la cuenta de integración](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. En **Configuración de diagnóstico**, elija **Activado**.

   ![Activación de Diagnósticos de Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Ahora seleccione categoría de evento y el área de trabajo OMS de hello para el registro como se muestra:

   1. Seleccione **enviar tooLog análisis**. 
   2. En **Log Analytics**, elija **Configurar**. 
   3. En **áreas de trabajo de OMS**, seleccione toouse de área de trabajo OMS de hello para el registro.
   4. En **registro**, seleccione hello **IntegrationAccountTrackingEvents** categoría.
   5. Cuando termine, seleccione **Guardar**.

   ![Configurar el análisis de registros para poder enviar registros de tooa de datos de diagnóstico](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Ahora [configure el seguimiento de los mensajes B2B en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Extensión de cómo y dónde usa los datos de diagnóstico con otros servicios

Además de con Azure Log Analytics, puede usar los datos de diagnóstico de la aplicación lógica con otros servicios de Azure, por ejemplo: 

* [Archivar registros de Diagnósticos de Azure en Azure Storage](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Transmitir tooAzure centros de eventos de los registros de diagnóstico de Azure](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Luego puede obtener supervisión en tiempo real mediante la telemetría y los análisis de otros servicios, como [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) y [Power BI](../log-analytics/log-analytics-powerbi.md). Por ejemplo:

* [Datos de la secuencia de los centros de eventos tooStream análisis](../stream-analytics/stream-analytics-define-inputs.md)
* [Analizar datos que se están transmitiendo con Stream Analytics y crear un panel de análisis en tiempo real en Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

En función de las opciones de Hola que desee configurar, asegúrese de que se primera [crear una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md) o [crear un concentrador de eventos Azure](../event-hubs/event-hubs-create.md). A continuación, seleccione opciones de Hola para donde desea que los datos de diagnóstico de toosend:

![Enviar datos tooAzure almacenamiento cuenta o evento de un centro](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> Períodos de retención se aplican únicamente cuando elija toouse una cuenta de almacenamiento.

## <a name="supported-tracking-schemas"></a>Esquemas de seguimiento compatibles

Azure admite estos tipos de esquema, que se corrigieron esquemas excepto Hola tipo personalizado de seguimiento.

* [Esquema de seguimiento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Esquemas de seguimiento de X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Esquema de seguimiento personalizado](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>Pasos siguientes

* [Seguimiento de mensajes B2B en OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Seguimiento de mensajes B2B en OMS")
* [Obtener más información sobre Hola paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")

