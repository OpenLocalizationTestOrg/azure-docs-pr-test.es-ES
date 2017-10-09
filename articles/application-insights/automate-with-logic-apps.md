---
title: aaaAutomate Azure Application Insights procesa mediante Logic Apps.
description: "Obtenga información acerca de cómo automatizar rápidamente procesos repetibles mediante la adición de aplicación lógica de hello Application Insights connector tooyour."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Automatización de procesos de Application Insights con Logic Apps

¿Verá que su ejecución repetida de hello mismas consultas en su toocheck de datos de telemetría si el servicio está funcionando correctamente? ¿Es estas consultas para buscar tendencias y las anomalías de tooautomate de aspecto y, a continuación, crear sus propios flujos de trabajo a su alrededor? Conector de Hello Azure Application Insights (vista previa) para las aplicaciones lógicas es herramienta adecuada de Hola para este propósito.

Con esta integración, se pueden automatizar numerosos procesos sin tener que escribir una sola línea de código. Puede crear una aplicación de lógica con hello Application Insights conector tooquickly automatizar cualquier proceso de Application Insights. 

También puede agregar acciones adicionales. característica de las aplicaciones lógicas de Hola de servicio de aplicaciones de Azure, cientos de acciones disponibles. Por ejemplo, si usa una aplicación lógica, puede enviar automáticamente una notificación por correo electrónico o crear un error en Visual Studio Team Services. También puede usar uno de hello muchas disponibles [plantillas](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp acelerar el proceso de Hola de creación de la aplicación lógica. 

## <a name="create-a-logic-app-for-application-insights"></a>Creación de una aplicación lógica para Application Insights

En este tutorial, aprenderá cómo toocreate atributos de una aplicación de la lógica que utiliza Hola análisis autocluster algoritmo toogroup en datos de Hola para una aplicación web. flujo de Hello automáticamente envía los resultados de Hola por correo electrónico, solo un ejemplo de cómo puede usar análisis de visión de aplicaciones y aplicaciones lógicas conjuntamente. 

### <a name="step-1-create-a-logic-app"></a>Paso 1: Creación de una aplicación lógica
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Hola **New** panel, seleccione **Web y móvil**y, a continuación, seleccione **aplicación lógica**.

    ![Ventana de la aplicación lógica nueva](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Paso 2: Creación de un desencadenador para la aplicación lógica
1. Hola **lógica de aplicación diseñador** ventana, en **comenzar con un desencadenador común**, seleccione **periodicidad**.

    ![Ventana del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/logicapp2.png)

2. Hola **frecuencia** cuadro, seleccione **día** y, a continuación, en hello **intervalo** , escriba **1**.

    ![Ventana "Recurrencia" del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Paso 3: Incorporación de una acción de Application Insights
1. Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.

2. Hola **elegir una acción** cuadro de búsqueda, escriba **Azure Application Insights**.

3. En **Acciones**, haga clic en **Azure Application Insights: Visualizar consulta de análisis Versión preliminar**.

    ![Ventana "Elegir una acción" del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Paso 4: Conectarse a recursos de Application Insights tooan

toocomplete este paso, necesita un identificador de la aplicación y una clave de API para el recurso. Puede recuperarlos de hello portal de Azure, como se muestra en hello siguiente diagrama:

![Identificador de la aplicación Hola portal de Azure](./media/automate-with-logic-apps/appid.png) 

Proporcione un nombre para la conexión, el identificador de la aplicación hello y la clave de API de Hola.

![Ventana de conexión del flujo del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Paso 5: Especificar Hola consulta de análisis y el tipo de gráfico
En el siguiente ejemplo de Hola, consulta Hola selecciona solicitudes hello no se pudo Hola último día y pone en correlación con las excepciones que se ha producido como parte de la operación de Hola. Análisis de correlacionan las solicitudes de hello no se pudo, basadas en el identificador de operation_Id Hola. consulta de Hello segmentos, a continuación, resultados de hello mediante hello autocluster algoritmo. 

Cuando cree sus propias consultas, compruebe que estén funcionando correctamente en el análisis antes de agregar tooyour flujo.

1. Hola **consulta** , agregue Hola después de consulta de análisis: 

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

2. Hola **tipo de gráfico** cuadro, seleccione **tabla Html**.

    ![Pantalla de configuración de consulta de Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Paso 6: Configurar el correo electrónico toosend de aplicación de lógica de Hola

1. Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.

2. En el cuadro de búsqueda de hello, escriba **Office 365 Outlook**.

3. Haga clic en **Office 365 Outlook: Enviar un correo electrónico**.

    ![Selección de Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. Hola **enviar un correo electrónico** ventana, Hola siguientes:

   a. Escriba la dirección de correo electrónico de saludo del destinatario de Hola.

   b. Escriba a un asunto de correo electrónico de Hola.

   c. Haga clic en cualquier lugar en hello **cuerpo** cuadro y, a continuación, en hello contenido menú dinámico que se abre en hello derecho, seleccione **cuerpo**.

   d. Haga clic en **Mostrar opciones avanzadas**.

      ![Configuración de Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. En el menú de contenido dinámico de hello, Hola siguientes:

    a. Seleccione **Nombre de datos adjuntos**.

    b. Seleccione **Contenido de datos adjuntos**.
    
    c. Hola **es HTML** cuadro, seleccione **Sí**.

      ![Pantalla de configuración de correo electrónico de Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Paso 7: Guardado y prueba de la aplicación lógica
* Haga clic en **guardar** toosave los cambios.

Puede esperar a la aplicación lógica de hello desencadenador toorun hello, o puede ejecutar aplicación de lógica de hello inmediatamente seleccionando **ejecutar**.

![Pantalla de creación de la aplicación lógica](./media/automate-with-logic-apps/step7.png)

Cuando se ejecuta la lógica de aplicación, los destinatarios de Hola que especificó en la lista de correo electrónico de hello recibirán un correo electrónico que parece Hola siguiente:

![Mensaje de correo electrónico de la aplicación lógica](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Pasos siguientes

- Obtenga más información sobre cómo crear [consultas de análisis](app-insights-analytics-using.md).
- Más información acerca de [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





