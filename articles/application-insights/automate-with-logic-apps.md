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
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="9eb02-103">Automatización de procesos de Application Insights con Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9eb02-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="9eb02-104">¿Verá que su ejecución repetida de hello mismas consultas en su toocheck de datos de telemetría si el servicio está funcionando correctamente?</span><span class="sxs-lookup"><span data-stu-id="9eb02-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="9eb02-105">¿Es estas consultas para buscar tendencias y las anomalías de tooautomate de aspecto y, a continuación, crear sus propios flujos de trabajo a su alrededor? Conector de Hello Azure Application Insights (vista previa) para las aplicaciones lógicas es herramienta adecuada de Hola para este propósito.</span><span class="sxs-lookup"><span data-stu-id="9eb02-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="9eb02-106">Con esta integración, se pueden automatizar numerosos procesos sin tener que escribir una sola línea de código.</span><span class="sxs-lookup"><span data-stu-id="9eb02-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="9eb02-107">Puede crear una aplicación de lógica con hello Application Insights conector tooquickly automatizar cualquier proceso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9eb02-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="9eb02-108">También puede agregar acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="9eb02-108">You can add additional actions as well.</span></span> <span data-ttu-id="9eb02-109">característica de las aplicaciones lógicas de Hola de servicio de aplicaciones de Azure, cientos de acciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="9eb02-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="9eb02-110">Por ejemplo, si usa una aplicación lógica, puede enviar automáticamente una notificación por correo electrónico o crear un error en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9eb02-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="9eb02-111">También puede usar uno de hello muchas disponibles [plantillas](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp acelerar el proceso de Hola de creación de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9eb02-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="9eb02-112">Creación de una aplicación lógica para Application Insights</span><span class="sxs-lookup"><span data-stu-id="9eb02-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="9eb02-113">En este tutorial, aprenderá cómo toocreate atributos de una aplicación de la lógica que utiliza Hola análisis autocluster algoritmo toogroup en datos de Hola para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9eb02-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="9eb02-114">flujo de Hello automáticamente envía los resultados de Hola por correo electrónico, solo un ejemplo de cómo puede usar análisis de visión de aplicaciones y aplicaciones lógicas conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="9eb02-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="9eb02-115">Paso 1: Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="9eb02-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="9eb02-116">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9eb02-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9eb02-117">Hola **New** panel, seleccione **Web y móvil**y, a continuación, seleccione **aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Ventana de la aplicación lógica nueva](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="9eb02-119">Paso 2: Creación de un desencadenador para la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="9eb02-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="9eb02-120">Hola **lógica de aplicación diseñador** ventana, en **comenzar con un desencadenador común**, seleccione **periodicidad**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Ventana del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="9eb02-122">Hola **frecuencia** cuadro, seleccione **día** y, a continuación, en hello **intervalo** , escriba **1**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Ventana "Recurrencia" del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="9eb02-124">Paso 3: Incorporación de una acción de Application Insights</span><span class="sxs-lookup"><span data-stu-id="9eb02-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="9eb02-125">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="9eb02-126">Hola **elegir una acción** cuadro de búsqueda, escriba **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="9eb02-127">En **Acciones**, haga clic en **Azure Application Insights: Visualizar consulta de análisis Versión preliminar**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Ventana "Elegir una acción" del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="9eb02-129">Paso 4: Conectarse a recursos de Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="9eb02-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="9eb02-130">toocomplete este paso, necesita un identificador de la aplicación y una clave de API para el recurso.</span><span class="sxs-lookup"><span data-stu-id="9eb02-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="9eb02-131">Puede recuperarlos de hello portal de Azure, como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="9eb02-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Identificador de la aplicación Hola portal de Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="9eb02-133">Proporcione un nombre para la conexión, el identificador de la aplicación hello y la clave de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb02-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Ventana de conexión del flujo del Diseñador de aplicaciones lógicas](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="9eb02-135">Paso 5: Especificar Hola consulta de análisis y el tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="9eb02-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="9eb02-136">En el siguiente ejemplo de Hola, consulta Hola selecciona solicitudes hello no se pudo Hola último día y pone en correlación con las excepciones que se ha producido como parte de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb02-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="9eb02-137">Análisis de correlacionan las solicitudes de hello no se pudo, basadas en el identificador de operation_Id Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb02-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="9eb02-138">consulta de Hello segmentos, a continuación, resultados de hello mediante hello autocluster algoritmo.</span><span class="sxs-lookup"><span data-stu-id="9eb02-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="9eb02-139">Cuando cree sus propias consultas, compruebe que estén funcionando correctamente en el análisis antes de agregar tooyour flujo.</span><span class="sxs-lookup"><span data-stu-id="9eb02-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="9eb02-140">Hola **consulta** , agregue Hola después de consulta de análisis:</span><span class="sxs-lookup"><span data-stu-id="9eb02-140">In hello **Query** box, add hello following Analytics query:</span></span> 

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

2. <span data-ttu-id="9eb02-141">Hola **tipo de gráfico** cuadro, seleccione **tabla Html**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Pantalla de configuración de consulta de Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="9eb02-143">Paso 6: Configurar el correo electrónico toosend de aplicación de lógica de Hola</span><span class="sxs-lookup"><span data-stu-id="9eb02-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="9eb02-144">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="9eb02-145">En el cuadro de búsqueda de hello, escriba **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="9eb02-146">Haga clic en **Office 365 Outlook: Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Selección de Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="9eb02-148">Hola **enviar un correo electrónico** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9eb02-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="9eb02-149">a.</span><span class="sxs-lookup"><span data-stu-id="9eb02-149">a.</span></span> <span data-ttu-id="9eb02-150">Escriba la dirección de correo electrónico de saludo del destinatario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb02-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="9eb02-151">b.</span><span class="sxs-lookup"><span data-stu-id="9eb02-151">b.</span></span> <span data-ttu-id="9eb02-152">Escriba a un asunto de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="9eb02-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="9eb02-153">c.</span><span class="sxs-lookup"><span data-stu-id="9eb02-153">c.</span></span> <span data-ttu-id="9eb02-154">Haga clic en cualquier lugar en hello **cuerpo** cuadro y, a continuación, en hello contenido menú dinámico que se abre en hello derecho, seleccione **cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="9eb02-155">d.</span><span class="sxs-lookup"><span data-stu-id="9eb02-155">d.</span></span> <span data-ttu-id="9eb02-156">Haga clic en **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-156">Click **Show advanced options**.</span></span>

      ![Configuración de Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="9eb02-158">En el menú de contenido dinámico de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9eb02-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="9eb02-159">a.</span><span class="sxs-lookup"><span data-stu-id="9eb02-159">a.</span></span> <span data-ttu-id="9eb02-160">Seleccione **Nombre de datos adjuntos**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="9eb02-161">b.</span><span class="sxs-lookup"><span data-stu-id="9eb02-161">b.</span></span> <span data-ttu-id="9eb02-162">Seleccione **Contenido de datos adjuntos**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="9eb02-163">c.</span><span class="sxs-lookup"><span data-stu-id="9eb02-163">c.</span></span> <span data-ttu-id="9eb02-164">Hola **es HTML** cuadro, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Pantalla de configuración de correo electrónico de Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="9eb02-166">Paso 7: Guardado y prueba de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="9eb02-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="9eb02-167">Haga clic en **guardar** toosave los cambios.</span><span class="sxs-lookup"><span data-stu-id="9eb02-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="9eb02-168">Puede esperar a la aplicación lógica de hello desencadenador toorun hello, o puede ejecutar aplicación de lógica de hello inmediatamente seleccionando **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="9eb02-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Pantalla de creación de la aplicación lógica](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="9eb02-170">Cuando se ejecuta la lógica de aplicación, los destinatarios de Hola que especificó en la lista de correo electrónico de hello recibirán un correo electrónico que parece Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9eb02-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Mensaje de correo electrónico de la aplicación lógica](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="9eb02-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9eb02-172">Next steps</span></span>

- <span data-ttu-id="9eb02-173">Obtenga más información sobre cómo crear [consultas de análisis](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="9eb02-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="9eb02-174">Más información acerca de [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="9eb02-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





