---
title: "mensajes de aaaTrack B2B en Operations Management Suite: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Realice un seguimiento de la comunicación B2B de la cuenta de integración y las aplicaciones lógicas en Operations Management Suite (OMS) con Azure Log Analytics"
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
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Realizar un seguimiento de la comunicación B2B en hello Microsoft Operations Management Suite (OMS)

Después de configurar la comunicación B2B entre dos procesos o aplicaciones empresariales mediante la cuenta de integración, esas entidades pueden intercambiar mensajes entre sí. toocheck si estos mensajes se procesan correctamente, puede realizar un seguimiento de AS2, X12, y los mensajes EDIFACT con [Azure Log Analytics](../log-analytics/log-analytics-overview.md) en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Por ejemplo, puede usar estas capacidades de seguimiento basado en web para el seguimiento de mensajes:

* Número y estado de los mensajes
* Del estado de las confirmaciones
* Correlación de mensajes con confirmaciones
* Descripción detallada de errores
* De las funcionalidades de búsqueda

## <a name="requirements"></a>Requisitos

* Una aplicación lógica configurada con registro de diagnósticos. Obtenga información acerca de [cómo una aplicación de la lógica de toocreate](logic-apps-create-a-logic-app.md) y [cómo tooset el registro para esa aplicación lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Una cuenta de integración configurada con supervisión y registro. Obtenga información acerca de [cómo toocreate una cuenta de integración](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) y [cómo tooset supervisión y registro para esa cuenta](../logic-apps/logic-apps-monitor-b2b-message.md).

* Si no lo ha hecho ya, [publicar datos de diagnóstico tooLog análisis](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) de OMS.

> [!NOTE]
> Después de que cumple los requisitos anteriores de hello, debe tener un área de trabajo en hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Debe usar Hola la misma área de trabajo OMS para realizar el seguimiento de la comunicación B2B de OMS. 
>  
> Si no tiene un área de trabajo OMS, descubra [cómo toocreate un área de trabajo OMS](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Agregar Hola B2B de lógica de aplicaciones de la solución toohello Operations Management Suite (OMS)

toohave OMS controlar mensajes B2B para la aplicación lógica, debe agregar hello **lógica de aplicaciones B2B** portal de OMS de solución toohello. Obtenga más información sobre [agregar soluciones tooOMS](../log-analytics/log-analytics-get-started.md).

1. Hola [portal de Azure](https://portal.azure.com), elija **más servicios**. Busque "log analytics" y luego elija **Log Analytics** como se muestra aquí:

   ![Búsqueda de Log Analytics](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. En **Log Analytics**, busque y seleccione el área de trabajo de OMS. 

   ![Selección del área de trabajo de OMS](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. En **Administración**, elija **Portal de OMS**.

   ![Selección de Portal de OMS](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Cuando se abre la página principal OMS de hello, elija **Galería de soluciones**.    

   ![Selección de Galería de soluciones](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. En **Todas las soluciones**, busque y seleccione **Logic Apps B2B**.     

   ![Selección de Logic Apps B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. En **Logic Apps B2B**, elija **Agregar**.

   ![Elección de Agregar](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   En la página principal de OMS de hello, Hola mosaico para **lógica de aplicaciones B2B mensajes** aparece ahora. 
   Este icono actualiza el número de mensajes de Hola cuando se procesan los mensajes B2B.

   ![Página principal de OMS, icono de Mensajes B2B de Logic Apps](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>Realizar un seguimiento del estado del mensaje y los detalles en hello Operations Management Suite

1. Una vez procesados los mensajes B2B, puede ver estado de Hola y los detalles de esos mensajes. En la página principal de OMS de hello, elija hello **lógica de aplicaciones B2B mensajes** icono.

   ![Recuento de mensajes actualizado](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > De forma predeterminada, Hola **lógica de aplicaciones B2B mensajes** icono muestra datos basados en un solo día. definir el ámbito de datos de hello toochange tooa intervalo diferente, elija Hola ámbito control hello parte superior de la página OMS hello:
   > 
   > ![Cambio del ámbito de datos](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Después de estado del mensaje Hola aparecerá el panel, puede ver más detalles sobre un tipo de mensaje específico que muestre los datos basados en un solo día. Elija el icono de Hola para **AS2**, **X12**, o **EDIFACT**.

   ![Visualización del estado de los mensajes](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   Aparece una lista de mensajes para el icono seleccionado. 
   toolearn más información sobre propiedades de Hola para cada tipo de mensaje, se ven estas descripciones de propiedad de mensaje:

   * [Propiedades de mensajes AS2](#as2-message-properties)
   * [Propiedades de mensajes X12](#x12-message-properties)
   * [Propiedades de mensajes EDIFACT](#EDIFACT-message-properties)

   Por ejemplo, este podría ser el aspecto de una lista de mensajes AS2:

   ![Visualización de mensajes AS2](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. entradas de hello tooview o exportación salidas para mensajes específicos, seleccione los mensajes y elija **descargar**. Cuando se le pida, guarde el equipo local del tooyour de archivo .zip hello y, a continuación, extraer ese archivo. 

   carpeta extraída de Hello incluye una carpeta para cada mensaje seleccionado. 
   Si configuras confirmaciones, carpeta de mensajes de Hola también incluye archivos con detalles de confirmación. 
   Cada carpeta de mensaje tiene como mínimo estos archivos: 
   
   * Archivos de lenguaje natural con hello entrada carga y salida de los detalles de carga
   * Archivos codificados con hello entradas y salidas

   Para cada tipo de mensaje, puede encontrar la carpeta de Hola y formatos de nombre de archivo aquí:

   * [Formatos de nombre de carpeta y archivo AS2](#as2-folder-file-names)
   * [Formatos de nombre de carpeta y archivo X12](#x12-folder-file-names)
   * [Formatos de nombre de carpeta y archivo EDIFACT](#edifact-folder-file-names)

   ![Descarga de archivos de mensajes](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview todas las acciones que haya Hola mismo ID de ejecución, en hello **Log Search** página, elija un mensaje desde la lista de mensajes de Hola.

   Puede ordenar estas acciones por columna o buscar resultados concretos.

   ![Las acciones con hello mismo ejecutar Id.](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * resultados de toosearch con consultas predeterminadas, elija **favoritos**.

   * Obtenga información acerca de [cómo toobuild las consultas agregando filtros](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   U obtenga más información acerca de [cómo busca datos toofind con registro de análisis de registros](../log-analytics/log-analytics-log-searches.md).

   * consulta de toochange en el cuadro de búsqueda de hello, consulta de Hola de actualización con columnas de Hola y valores que desee toouse como filtros.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Descripciones de propiedades y formatos de nombre de los mensajes AS2, X12 y EDIFACT

Para cada tipo de mensaje, estas son las descripciones de propiedad de Hola y formatos de nombre de archivos de mensajes descargados.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>Descripciones de propiedades de los mensajes AS2

Estas son las descripciones de propiedad de Hola para cada mensaje de AS2.

| Propiedad | Descripción |
| --- | --- |
| Remitente | socio de invitado de Hello especificado en **configuración de recepción**, o socio del host Hola especificadas en **configuración de envío** para un acuerdo de AS2 |
| Receptor | socio del host Hola especificado en **configuración de recepción**, o socio invitado de hello especificadas en **configuración de envío** para un acuerdo de AS2 |
| Aplicación lógica | aplicación de la lógica de Hello donde se configuran las acciones de hello AS2 |
| Estado | Hola estado del mensaje AS2 <br>Correcto = recibido o enviado un mensaje AS2 válido. No se configura ninguna MDN. <br>Correcto = recibido o enviado un mensaje AS2 válido. Se configura y se recibe una MDN, o se envía. <br>Error = recibido un mensaje AS2 no válido. No se configura ninguna MDN. <br>Pendiente = recibido o enviado un mensaje AS2 válido. Se configura una MDN y se espera una MDN. |
| Ack | Hola estado del mensaje MDN <br>Aceptado = recibida o enviada una MDN positiva. <br>Pending = espera tooreceive o enviar un MDN. <br>Rechazado = recibida o enviada una MDN negativa. <br>No es necesario = MDN no está configurado en el acuerdo de Hola. |
| Dirección | Hola dirección del mensaje AS2 |
| Id. de correlación | Id. de Hola que pone en correlación todos los desencadenadores de Hola y acciones en una aplicación de lógica |
| Id. de mensaje | Id. de mensaje de Hola AS2 de encabezados del mensaje Hola AS2 |
| Timestamp | hora de Hola Hola AS2 acción procesó mensajes de bienvenida |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>Formatos de nombre AS2 para archivos de mensajes descargados

Estos son formatos de nombre de Hola para cada carpeta descargada de mensaje AS2 y archivos.

| Archivo o carpeta | Formato de nombre |
| :------------- | :---------- |
| Carpeta de mensajes | [sender]\_[receiver]\_AS2\_[correlation-ID]\_[message-ID]\_[timestamp] |
| Archivos de entrada, salida y, si se ha configurado, de confirmación | **Carga de entrada**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_input_payload.txt </p>**Carga de salida**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_output\_payload.txt </p></p>**Entradas**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_inputs.txt </p></p>**Salidas**: [sender]\_[receiver]\_AS2\_[correlation-ID]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>Descripciones de propiedades de los mensajes X12

Estas son las descripciones de propiedad de Hola para cada X12 mensaje.

| Propiedad | Descripción |
| --- | --- |
| Remitente | socio de invitado de Hello especificado en **configuración de recepción**, o socio del host Hola especificadas en **configuración de envío** para un X12 acuerdo |
| Receptor | socio del host Hola especificado en **configuración de recepción**, o su partner de invitado de hello especificado en **configuración de envío** para un X12 acuerdo |
| Aplicación lógica | aplicación de la lógica de Hello donde se configuran las acciones de hello X12 |
| Estado | estado del mensaje Hola X12 <br>Correcto = recibido o enviado un mensaje X12 válido. No se configura ninguna confirmación funcional. <br>Correcto = recibido o enviado un mensaje X12 válido. Se configura y se recibe una confirmación funcional, o se envía una confirmación funcional. <br>Error = recibido o enviado un mensaje X12 no válido. <br>Pendiente = recibido o enviado un mensaje X12 válido. Se configura una confirmación funcional y se espera una confirmación funcional. |
| Ack | Estado de confirmación funcional (997) <br>Aceptado = recibida o enviada una confirmación funcional positiva. <br>Rechazado = recibida o enviada una confirmación funcional negativa. <br>Pendiente = se espera una confirmación funcional, pero no se ha recibido. <br>Pendiente = genera una confirmación funcional, pero no se puede enviar toopartner. <br>No necesario = confirmación funcional no configurada. |
| Dirección | dirección del mensaje Hola X12 |
| Id. de correlación | Id. de Hola que pone en correlación todos los desencadenadores de Hola y acciones en una aplicación de lógica |
| Tipo de mensaje | tipo de EDI X 12 mensaje Hola |
| ICN | Hola número de Control de intercambio de mensajes de bienvenida X12 |
| TSCN | Hola número de Control de conjunto de transacciones para mensajes de bienvenida X12 |
| Timestamp | tiempo de Hello al procesar la acción de hello X12 mensajes de bienvenida |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>Formatos de nombre X12 para archivos de mensajes descargados

Estos son los formatos de nombres Hola para cada uno de ellos descargadas X12 carpetas y archivos de mensajes.

| Archivo o carpeta | Formato de nombre |
| :------------- | :---------- |
| Carpeta de mensajes | [sender]\_[receiver]\_X12\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp] |
| Archivos de entrada, salida y, si se ha configurado, de confirmación | **Carga de entrada**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_input_payload.txt </p>**Carga de salida**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_output\_payload.txt </p></p>**Entradas**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_inputs.txt </p></p>**Salidas**: [sender]\_[receiver]\_X12\_[interchange-control-number]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>Descripciones de propiedades de los mensajes EDIFACT

Estas son las descripciones de propiedad de Hola para cada mensaje EDIFACT.

| Propiedad | Descripción |
| --- | --- |
| Remitente | socio de invitado de Hello especificado en **configuración de recepción**, o socio del host Hola especificadas en **configuración de envío** para un acuerdo de EDIFACT |
| Receptor | socio del host Hola especificado en **configuración de recepción**, o socio invitado de hello especificadas en **configuración de envío** para un acuerdo de EDIFACT |
| Aplicación lógica | aplicación de la lógica de Hello donde se configuran las acciones de saludo EDIFACT |
| Estado | Hola estado del mensaje EDIFACT <br>Correcto = recibido o enviado un mensaje EDIFACT válido. No se configura ninguna confirmación funcional. <br>Correcto = recibido o enviado un mensaje EDIFACT válido. Se configura y se recibe una confirmación funcional, o se envía una confirmación funcional. <br>Error = recibido o enviado un mensaje EDIFACT no válido <br>Pendiente = recibido o enviado un mensaje EDIFACT válido. Se configura una confirmación funcional y se espera una confirmación funcional. |
| Ack | Estado de confirmación funcional (997) <br>Aceptado = recibida o enviada una confirmación funcional positiva. <br>Rechazado = recibida o enviada una confirmación funcional negativa. <br>Pendiente = se espera una confirmación funcional, pero no se ha recibido. <br>Pendiente = genera una confirmación funcional, pero no se puede enviar toopartner. <br>No necesario = confirmación funcional no configurada. |
| Dirección | Hola dirección del mensaje EDIFACT |
| Id. de correlación | Id. de Hola que pone en correlación todos los desencadenadores de Hola y acciones en una aplicación de lógica |
| Tipo de mensaje | tipo de mensaje EDIFACT Hola |
| ICN | Hola número de Control de intercambio de mensaje de saludo EDIFACT |
| TSCN | Hola número de Control de conjunto de transacciones para el mensaje de saludo EDIFACT |
| Timestamp | hora de Hola Hola acción EDIFACT procesó mensajes de bienvenida |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>Formatos de nombre EDIFACT para archivos de mensajes descargados

Estos son formatos de nombre de Hola para cada carpeta de mensaje EDIFACT descargada y archivos.

| Archivo o carpeta | Formato de nombre |
| :------------- | :---------- |
| Carpeta de mensajes | [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_[global-control-number]\_[transaction-set-control-number]\_[timestamp] |
| Archivos de entrada, salida y, si se ha configurado, de confirmación | **Carga de entrada**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_input_payload.txt </p>**Carga de salida**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_output\_payload.txt </p></p>**Entradas**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_inputs.txt </p></p>**Salidas**: [sender]\_[receiver]\_EDIFACT\_[interchange-control-number]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Pasos siguientes

* [Consulta de mensajes B2B en Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [Esquemas de seguimiento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Esquemas de seguimiento de X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Esquemas de seguimiento personalizados](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)