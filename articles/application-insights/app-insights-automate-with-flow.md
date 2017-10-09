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
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="9dfd0-103">Automatizar los procesos de visión de la aplicación de Azure con el conector de Hola para Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="9dfd0-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="9dfd0-104">¿Verá que su ejecución repetida Hola mismas consultas en su toocheck de datos de telemetría que el servicio está funcionando correctamente?</span><span class="sxs-lookup"><span data-stu-id="9dfd0-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="9dfd0-105">¿Es estas consultas para buscar tendencias y las anomalías de tooautomate de aspecto y, a continuación, crear sus propios flujos de trabajo a su alrededor? Conector de Hello Azure Application Insights (vista previa) para Microsoft Flow es la herramienta adecuada de Hola para estos fines.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="9dfd0-106">Con esta integración, ahora se pueden automatizar numerosos procesos sin tener que escribir una sola línea de código.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="9dfd0-107">Después de crear un flujo mediante el uso de una acción de Application Insights, flujo de hello ejecuta automáticamente la consulta de análisis de visión de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="9dfd0-108">También puede agregar acciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-108">You can add additional actions as well.</span></span> <span data-ttu-id="9dfd0-109">Microsoft Flow pone a su disposición cientos de acciones.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="9dfd0-110">Por ejemplo, puede utilizar Microsoft Flow tooautomatically enviar una notificación por correo electrónico o crear un error en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="9dfd0-111">También puede usar uno de hello muchas [plantillas](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) que están disponibles para el conector de Hola para Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="9dfd0-112">Estas plantillas acelerar el proceso de Hola de creación de un flujo.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="9dfd0-113">Creación de un flujo para Application Insights</span><span class="sxs-lookup"><span data-stu-id="9dfd0-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="9dfd0-114">En este tutorial, aprenderá cómo toocreate un flujo que usa Hola análisis automático clúster algoritmo toogroup atributos en datos de Hola para una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="9dfd0-115">flujo Hola envía automáticamente los resultados de Hola por correo electrónico, solo un ejemplo de cómo puede usar conjuntamente Microsoft Flow y análisis de visión de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="9dfd0-116">Paso 1: Creación de un almacén</span><span class="sxs-lookup"><span data-stu-id="9dfd0-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="9dfd0-117">Inicie sesión en demasiado[Microsoft Flow](http://flow.microsoft.com)y, a continuación, seleccione **fluye mi**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="9dfd0-118">Haga clic en **Crear un flujo a partir de un documento en blanco**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="9dfd0-119">Paso 2: Creación de un desencadenador para el flujo</span><span class="sxs-lookup"><span data-stu-id="9dfd0-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="9dfd0-120">Elija **Programación** y, a continuación, **Programación: Periodicidad**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="9dfd0-121">Hola **frecuencia** cuadro, seleccione **día**y en hello **intervalo** cuadro, escriba **1**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Cuadro de diálogo del desencadenador de Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="9dfd0-123">Paso 3: Incorporación de una acción de Application Insights</span><span class="sxs-lookup"><span data-stu-id="9dfd0-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="9dfd0-124">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="9dfd0-125">Busque **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="9dfd0-126">Haga clic en **Azure Application Insights: Visualize Analytics query Preview** [Visualizar consulta de Analytics (Versión preliminar)].</span><span class="sxs-lookup"><span data-stu-id="9dfd0-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Ventana Ejecutar consulta de Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="9dfd0-128">Paso 4: Conectarse a recursos de Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="9dfd0-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="9dfd0-129">toocomplete este paso, necesita un identificador de la aplicación y una clave de API para el recurso.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="9dfd0-130">Puede recuperarlos de hello portal de Azure, como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="9dfd0-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Identificador de la aplicación Hola portal de Azure](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="9dfd0-132">Proporcione un nombre para la conexión, junto con la clave de API e Id. de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Ventana de conexión de Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="9dfd0-134">Paso 5: Especificar Hola consulta de análisis y el tipo de gráfico</span><span class="sxs-lookup"><span data-stu-id="9dfd0-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="9dfd0-135">Esta consulta de ejemplo selecciona solicitudes hello no se pudo Hola último día y pone en correlación con las excepciones que se ha producido como parte de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="9dfd0-136">Correlacionan análisis basado en el identificador de operation_Id Hola.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="9dfd0-137">consulta de Hello segmentos, a continuación, resultados de hello mediante hello autocluster algoritmo.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="9dfd0-138">Cuando cree sus propias consultas, compruebe que estén funcionando correctamente en el análisis antes de agregar tooyour flujo.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="9dfd0-139">Agregar Hola después de consulta de análisis y, a continuación, seleccione el tipo de gráfico de tabla HTML de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

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

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="9dfd0-141">Paso 6: Configurar el correo electrónico de toosend de flujo de Hola</span><span class="sxs-lookup"><span data-stu-id="9dfd0-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="9dfd0-142">Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="9dfd0-143">Busque **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="9dfd0-144">Haga clic en **Office 365 Outlook: Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Ventana de selección de Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="9dfd0-146">Hola **enviar un correo electrónico** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9dfd0-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="9dfd0-147">a.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-147">a.</span></span> <span data-ttu-id="9dfd0-148">Escriba la dirección de correo electrónico de saludo del destinatario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="9dfd0-149">b.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-149">b.</span></span> <span data-ttu-id="9dfd0-150">Escriba a un asunto de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="9dfd0-151">c.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-151">c.</span></span> <span data-ttu-id="9dfd0-152">Haga clic en cualquier lugar en hello **cuerpo** cuadro y, a continuación, en hello contenido menú dinámico que se abre en hello derecho, seleccione **cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="9dfd0-153">d.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-153">d.</span></span> <span data-ttu-id="9dfd0-154">Haga clic en **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-154">Click **Show advanced options**.</span></span>

    ![Configuración de Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="9dfd0-156">En el menú de contenido dinámico de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9dfd0-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="9dfd0-157">a.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-157">a.</span></span> <span data-ttu-id="9dfd0-158">Seleccione **Nombre de datos adjuntos**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="9dfd0-159">b.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-159">b.</span></span> <span data-ttu-id="9dfd0-160">Seleccione **Contenido de datos adjuntos**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="9dfd0-161">c.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-161">c.</span></span> <span data-ttu-id="9dfd0-162">Hola **es HTML** cuadro, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Pantalla de configuración de correo electrónico de Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="9dfd0-164">Paso 7: Guardado y prueba del flujo</span><span class="sxs-lookup"><span data-stu-id="9dfd0-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="9dfd0-165">Hola **nombre de flujo de** cuadro, agregue un nombre para el flujo y, a continuación, haga clic en **Crear flujo**.</span><span class="sxs-lookup"><span data-stu-id="9dfd0-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Ventana de creación de flujo](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="9dfd0-167">Se puede esperar Hola desencadenador toorun esta acción, o puede ejecutar el flujo de hello inmediatamente por [ejecución desencadenador Hola a petición](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="9dfd0-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="9dfd0-168">Cuando se ejecuta el flujo de hello, los destinatarios de Hola que ha especificado en la lista de correo electrónico de Hola reciban un mensaje de correo electrónico similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9dfd0-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Correo electrónico de ejemplo](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="9dfd0-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9dfd0-170">Next steps</span></span>

- <span data-ttu-id="9dfd0-171">Más información sobre cómo crear [consultas de análisis](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="9dfd0-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="9dfd0-172">Más información sobre [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9dfd0-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





