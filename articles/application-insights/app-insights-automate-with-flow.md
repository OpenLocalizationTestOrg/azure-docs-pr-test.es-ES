---
title: aaaAutomate Azure Application Insights procesa con Microsoft Flow
description: "Obtenga información acerca de cómo puede utilizar Microsoft Flow tooquickly automatizar procesos repetibles mediante el conector de Application Insights Hola."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Automatizar los procesos de visión de la aplicación de Azure con el conector de Hola para Microsoft Flow

¿Verá que su ejecución repetida Hola mismas consultas en su toocheck de datos de telemetría que el servicio está funcionando correctamente? ¿Es estas consultas para buscar tendencias y las anomalías de tooautomate de aspecto y, a continuación, crear sus propios flujos de trabajo a su alrededor? Conector de Hello Azure Application Insights (vista previa) para Microsoft Flow es la herramienta adecuada de Hola para estos fines.

Con esta integración, ahora se pueden automatizar numerosos procesos sin tener que escribir una sola línea de código. Después de crear un flujo mediante el uso de una acción de Application Insights, flujo de hello ejecuta automáticamente la consulta de análisis de visión de aplicaciones. 

También puede agregar acciones adicionales. Microsoft Flow pone a su disposición cientos de acciones. Por ejemplo, puede utilizar Microsoft Flow tooautomatically enviar una notificación por correo electrónico o crear un error en Visual Studio Team Services. También puede usar uno de hello muchas [plantillas](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) que están disponibles para el conector de Hola para Microsoft Flow. Estas plantillas acelerar el proceso de Hola de creación de un flujo. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Creación de un flujo para Application Insights

En este tutorial, aprenderá cómo toocreate un flujo que usa Hola análisis automático clúster algoritmo toogroup atributos en datos de Hola para una aplicación web. flujo Hola envía automáticamente los resultados de Hola por correo electrónico, solo un ejemplo de cómo puede usar conjuntamente Microsoft Flow y análisis de visión de aplicaciones. 

### <a name="step-1-create-a-flow"></a>Paso 1: Creación de un almacén
1. Inicie sesión en demasiado[Microsoft Flow](http://flow.microsoft.com)y, a continuación, seleccione **fluye mi**.
2. Haga clic en **Crear un flujo a partir de un documento en blanco**.

### <a name="step-2-create-a-trigger-for-your-flow"></a>Paso 2: Creación de un desencadenador para el flujo
1. Elija **Programación** y, a continuación, **Programación: Periodicidad**.
2. Hola **frecuencia** cuadro, seleccione **día**y en hello **intervalo** cuadro, escriba **1**.

    ![Cuadro de diálogo del desencadenador de Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>Paso 3: Incorporación de una acción de Application Insights
1. Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.
2. Busque **Azure Application Insights**.
3. Haga clic en **Azure Application Insights: Visualize Analytics query Preview** [Visualizar consulta de Analytics (Versión preliminar)].

    ![Ventana Ejecutar consulta de Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Paso 4: Conectarse a recursos de Application Insights tooan

toocomplete este paso, necesita un identificador de la aplicación y una clave de API para el recurso. Puede recuperarlos de hello portal de Azure, como se muestra en hello siguiente diagrama:

![Identificador de la aplicación Hola portal de Azure](./media/app-insights-automate-with-flow/appid.png) 

- Proporcione un nombre para la conexión, junto con la clave de API e Id. de aplicación de Hola.

    ![Ventana de conexión de Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Paso 5: Especificar Hola consulta de análisis y el tipo de gráfico
Esta consulta de ejemplo selecciona solicitudes hello no se pudo Hola último día y pone en correlación con las excepciones que se ha producido como parte de la operación de Hola. Correlacionan análisis basado en el identificador de operation_Id Hola. consulta de Hello segmentos, a continuación, resultados de hello mediante hello autocluster algoritmo. 

Cuando cree sus propias consultas, compruebe que estén funcionando correctamente en el análisis antes de agregar tooyour flujo.

- Agregar Hola después de consulta de análisis y, a continuación, seleccione el tipo de gráfico de tabla HTML de Hola. 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Pantalla de configuración de consulta de Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>Paso 6: Configurar el correo electrónico de toosend de flujo de Hola

1. Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.
2. Busque **Office 365 Outlook**.
3. Haga clic en **Office 365 Outlook: Enviar un correo electrónico**.

    ![Ventana de selección de Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. Hola **enviar un correo electrónico** ventana, Hola siguientes:

   a. Escriba la dirección de correo electrónico de saludo del destinatario de Hola.

   b. Escriba a un asunto de correo electrónico de Hola.

   c. Haga clic en cualquier lugar en hello **cuerpo** cuadro y, a continuación, en hello contenido menú dinámico que se abre en hello derecho, seleccione **cuerpo**.

   d. Haga clic en **Mostrar opciones avanzadas**.

    ![Configuración de Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. En el menú de contenido dinámico de hello, Hola siguientes:

    a. Seleccione **Nombre de datos adjuntos**.

    b. Seleccione **Contenido de datos adjuntos**.
    
    c. Hola **es HTML** cuadro, seleccione **Sí**.

    ![Pantalla de configuración de correo electrónico de Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>Paso 7: Guardado y prueba del flujo
- Hola **nombre de flujo de** cuadro, agregue un nombre para el flujo y, a continuación, haga clic en **Crear flujo**.

    ![Ventana de creación de flujo](./media/app-insights-automate-with-flow/flow8.png)

Se puede esperar Hola desencadenador toorun esta acción, o puede ejecutar el flujo de hello inmediatamente por [ejecución desencadenador Hola a petición](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

Cuando se ejecuta el flujo de hello, los destinatarios de Hola que ha especificado en la lista de correo electrónico de Hola reciban un mensaje de correo electrónico similar Hola siguiente:

![Correo electrónico de ejemplo](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Pasos siguientes

- Más información sobre cómo crear [consultas de análisis](app-insights-analytics-using.md).
- Más información sobre [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





