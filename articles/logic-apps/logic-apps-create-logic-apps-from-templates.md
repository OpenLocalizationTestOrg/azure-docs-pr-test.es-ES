---
title: "Creación de flujos de trabajo a partir de plantillas (Azure Logic Apps) | Microsoft Docs"
description: "Compilar flujos de trabajo más rápido mediante el uso de plantillas de aplicaciones lógicas"
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/15/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 49b4bbfda4518b03ef6080bec1e2a493933af4f5
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="create-logic-app-workflows-from-prebuilt-templates"></a>Creación de flujos de trabajo de aplicaciones lógicas a partir de plantillas precompiladas

Para que pueda empezar a crear flujos de trabajo más rápidamente, Logic Apps proporciona plantillas, que son aplicaciones lógicas precompiladas que siguen patrones de uso frecuente. Use estas plantillas tal como se proporcionan o edítelas para ajustarlas a su escenario.

Estas son algunas categorías de plantillas:

| Tipo de plantilla | DESCRIPCIÓN | 
| ------------- | ----------- | 
| Plantillas de empresa en la nube | Para integrar Azure Blob, Dynamics CRM, Salesforce, Box y el blob de Azure; y también incluyen otros conectores para sus necesidades empresariales en la nube. Por ejemplo, puede usar estas plantillas para organizar clientes potenciales de empresa o realizar copias de seguridad de datos de archivos corporativos. | 
| Plantillas de productividad personal | Mejore la productividad personal al establecer avisos diarios, convertir los elementos de trabajo importantes en listas de tareas pendientes y automatizar las tareas largas con un único paso de aprobación de usuario. | 
| Plantillas en la nube del consumidor | Para integrar servicios de medios sociales como Twitter, Slack y correos electrónicos. Resulta útil para reforzar las iniciativas de marketing de medios sociales. Estas plantillas también incluyen tareas como la copia de la nube, que permite aumentar la productividad mediante el ahorro del tiempo invertido en tareas habitualmente repetitivas. | 
| Plantillas de Enterprise Integration Pack | Para configurar canalizaciones VETER (validación, extracción, transformación, enriquecimiento, enrutamiento), la recepción de documentos X12 EDI a través de AS2 y la transformación en XML, así como el control de mensajes X12, EDIFACT y AS2. | 
| Plantillas de patrón de protocolo | Para implementar patrones de protocolo, como el patrón solicitud-respuesta a través de HTTP, e integraciones a través de FTP y SFTP. Use estas plantillas tal como se proporcionan, o compile a partir de estas para obtener patrones de protocolo complejos. | 
||| 

Si no tiene ninguna suscripción a Azure, [cree una cuenta gratuita de Azure](https://azure.microsoft.com/free/) antes de empezar. Para obtener más información acerca de cómo compilar una aplicación lógica, consulte [Crear una aplicación de lógica](../logic-apps/quickstart-create-first-logic-app-workflow.md).

## <a name="create-logic-apps-from-templates"></a>Creación de aplicaciones lógicas a partir de plantillas

1. Si aún no lo ha hecho, inicie sesión en [Azure Portal](https://portal.azure.com "Azure Portal").

2. En el menú principal de Azure, elija **Nuevo** > **Enterprise Integration** > **Logic App**.

   ![Portal de Azure, Nuevo, Enterprise Integration, Logic App](./media/logic-apps-create-logic-apps-from-templates/azure-portal-create-logic-app.png)

3. Cree la aplicación lógica con la configuración que se incluye en la tabla situada bajo la imagen:

   ![Proporcione los detalles de la aplicación lógica](./media/logic-apps-create-logic-apps-from-templates/logic-app-settings.png)

   | Configuración | Valor | DESCRIPCIÓN | 
   | ------- | ----- | ----------- | 
   | **Name** | *nombre-de-la-aplicación-lógica* | Proporcione un nombre único de aplicación lógica. | 
   | **Suscripción** | *your-Azure-subscription-name* | Seleccione la suscripción de Azure que quiera usar. | 
   | **Grupos de recursos** | *your-Azure-resource-group-name* | Cree o seleccione un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) para esta aplicación lógica y organice todos los recursos asociados a esta aplicación. | 
   | **Ubicación** | *your-Azure-datacenter-region* | Seleccione la región del centro de datos para implementar la aplicación lógica, por ejemplo, Oeste de EE.UU. | 
   | **Log Analytics** | **Off** (Desactivar) (valor predeterminado) o **On** (Activar) | Activar el [registro de diagnóstico](../logic-apps/logic-apps-monitor-your-logic-apps.md#turn-on-diagnostics-logging-for-your-logic-app) para la aplicación lógica a través de [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Esta acción requiere que tenga un área de trabajo de [Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md). | 
   |||| 

4. Cuando esté listo, elija **Anclar al panel**. De este modo, la aplicación lógica aparecerá automáticamente en el panel de Azure y se abrirá después de la implementación. Seleccione **Create**.

   > [!NOTE]
   > Si no quiere anclar la aplicación lógica, búsquela y ábrala manualmente después de la implementación para continuar.

   Una vez que Azure ha implementado la aplicación lógica, el Diseñador de Logic Apps se abre y muestra una página con un vídeo de introducción. 
   Bajo el vídeo encontrará plantillas de los patrones de aplicación lógica más comunes. 

5. Pase el vídeo de introducción y los desencadenadores comunes hasta **Plantillas**. Elija una plantilla precompilada. Por ejemplo: 

   ![Elegir una plantilla de aplicación lógica](./media/logic-apps-create-logic-apps-from-templates/choose-logic-app-template.png)

   > [!TIP]
   > Para crear la aplicación lógica desde cero, elija **Aplicación lógica en blanco**.

   Cuando se selecciona una plantilla precompilada, puede ver más información acerca de dicha plantilla. 
   Por ejemplo: 

   ![Elegir una plantilla precompilada](./media/logic-apps-create-logic-apps-from-templates/logic-app-choose-prebuilt-template.png)

6. Para continuar con la plantilla seleccionada, elija **Usar esta plantilla**. 

7. En función de los conectores de la plantilla, se le solicitará que realice cualquiera de estos pasos:

   * Inicie sesión con sus credenciales en los sistemas o servicios a los que la plantilla hace referencia.

   * Cree conexiones para todos los servicios o sistemas a los que hace referencia la plantilla. Para crear una conexión, proporcione un nombre para la conexión y, si es necesario, seleccione el recurso que quiere usar. 

   * Si ya configuró estas conexiones, elija **Continuar**.

   Por ejemplo: 

   ![Crear conexiones](./media/logic-apps-create-logic-apps-from-templates/logic-app-create-connection.png)

   Cuando haya terminado, la aplicación lógica se abrirá y aparecerá en el Diseñador de Logic Apps.

   > [!TIP]
   > Para volver al visor de plantillas, elija **Plantillas** en la barra de herramientas del diseñador. Esta acción descarta los cambios no guardados, por lo que aparece un mensaje de advertencia para confirmar la solicitud.

8. Siga compilando su aplicación lógica.

   > [!NOTE] 
   > Muchas de las plantillas incluyen conectores que puede que ya se hayan rellenado previamente con las propiedades necesarias. Sin embargo, es posible que algunas plantillas todavía necesiten proporcionar valores antes de que pueda implementar correctamente la aplicación lógica. Si intenta implementar sin completar los campos de propiedades que faltan, recibirá un mensaje de error. 

## <a name="update-logic-apps-with-templates"></a>Actualizar aplicaciones lógicas con plantillas

1. En [Azure Portal](https://portal.azure.com "Azure Portal"), busque y abra la aplicación lógica en el Diseñador de aplicaciones lógicas.

2. En la barra de herramientas del diseñador, haga clic en **Plantillas**. Esta acción descarta los cambios no guardados, por lo que aparece un mensaje de advertencia para confirmar que quiere continuar. Para confirmar, elija **Aceptar**. Por ejemplo: 

   ![Elegir "Plantillas"](./media/logic-apps-create-logic-apps-from-templates/logic-app-update-existing-with-template.png)

3. Pase el vídeo de introducción y los desencadenadores comunes hasta **Plantillas**. Elija una plantilla precompilada. Por ejemplo: 

   ![Elegir una plantilla de aplicación lógica](./media/logic-apps-create-logic-apps-from-templates/choose-logic-app-template.png)

   Cuando se selecciona una plantilla precompilada, puede ver más información acerca de dicha plantilla. 
   Por ejemplo: 

   ![Elegir una plantilla precompilada](./media/logic-apps-create-logic-apps-from-templates/logic-app-choose-prebuilt-template.png)

4. Para continuar con la plantilla seleccionada, elija **Usar esta plantilla**. 

5. En función de los conectores de la plantilla, se le solicitará que realice cualquiera de estos pasos:

   * Inicie sesión con sus credenciales en los sistemas o servicios a los que la plantilla hace referencia.

   * Cree conexiones para todos los servicios o sistemas a los que hace referencia la plantilla. Para crear una conexión, proporcione un nombre para la conexión y, si es necesario, seleccione el recurso que quiere usar. 

   * Si ya configuró estas conexiones, elija **Continuar**.

   ![Crear conexiones](./media/logic-apps-create-logic-apps-from-templates/logic-app-create-connection.png)

   La aplicación lógica se abrirá y aparecerá en el Diseñador de Logic Apps.

8. Siga compilando su aplicación lógica. 

   > [!TIP]
   > Si no guardó los cambios, puede descartar el trabajo y volver a la aplicación lógica anterior. En la barra de herramientas del diseñador, haga clic en **Descartar**.

> [!NOTE] 
> Muchas de las plantillas incluyen conectores que puede que ya hayan rellenado previamente las propiedades necesarias. Sin embargo, es posible que algunas plantillas todavía necesiten proporcionar valores antes de que pueda implementar correctamente la aplicación lógica. Si intenta implementar sin completar los campos de propiedades que faltan, recibirá un mensaje de error.

## <a name="deploy-logic-apps-built-from-templates"></a>Implementar aplicaciones lógicas compiladas a partir de plantillas

Después de realizar los cambios en la plantilla, puede guardarlos. Esta acción también publica automáticamente la aplicación lógica.

En la barra de herramientas del diseñador, haga clic en **Guardar**.

![Guardar y publicar la aplicación lógica](./media/logic-apps-create-logic-apps-from-templates/logic-app-save.png)  

## <a name="get-support"></a>Obtención de soporte técnico

* Si tiene alguna duda, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).
* Para enviar ideas sobre características o votar sobre ellas, visite el [sitio de comentarios de los usuarios de Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>pasos siguientes

Obtenga información acerca de cómo compilar aplicaciones lógicas a través de ejemplos, escenarios, casos de clientes y tutoriales.

> [!div class="nextstepaction"]
> [Escenarios comunes, ejemplos, tutoriales y guías detalladas de Azure Logic Apps](../logic-apps/logic-apps-examples-and-scenarios.md)