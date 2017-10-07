---
title: "aaaAutomate los procesos de análisis de registros de Azure con Microsoft Flow"
description: "Obtenga información acerca de cómo puede utilizar Microsoft Flow tooquickly automatizar procesos repetibles mediante el conector de Azure Log Analytics Hola."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="e5fec-103">Automatizar los procesos de análisis de registros con el conector de Hola para Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="e5fec-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="e5fec-104">[Microsoft Flow](https://ms.flow.microsoft.com) permite los flujos de trabajo toocreate automatizada con cientos de acciones para una variedad de servicios.</span><span class="sxs-lookup"><span data-stu-id="e5fec-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="e5fec-105">Salida de una acción puede utilizarse como entrada tooanother permitiéndole toocreate integración entre diferentes servicios.</span><span class="sxs-lookup"><span data-stu-id="e5fec-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="e5fec-106">Conector de Azure Log Analytics Hola para Microsoft Flow permitir que los flujos de trabajo de toobuild que incluyen datos recuperados por las búsquedas de registros de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="e5fec-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="e5fec-107">Por ejemplo, puede usar datos de análisis de registros de Microsoft Flow toouse en una notificación de correo electrónico de Office 365, crear un error en Visual Studio Team Services o publicar un mensaje demora.</span><span class="sxs-lookup"><span data-stu-id="e5fec-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="e5fec-108">Puede desencadenar un flujo de trabajo mediante una programación simple o a partir de alguna acción de un servicio conectado, como cuando se recibe un correo electrónico o un tweet.</span><span class="sxs-lookup"><span data-stu-id="e5fec-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="e5fec-109">Conector de Azure Log Analytics Hola para Microsoft Flow requiere su área de trabajo toobe actualizado toohello nuevo análisis de registros lenguaje de consulta.</span><span class="sxs-lookup"><span data-stu-id="e5fec-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="e5fec-110">Puede obtener más información sobre el nuevo lenguaje de Hola y obtener Hola procedimiento tooupgrade el área de trabajo en [actualizar la búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="e5fec-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="e5fec-111">tutorial de Hello en este artículo muestra cómo Hola toocreate un flujo que envía automáticamente los resultados de una búsqueda de registros de análisis de registros por correo electrónico, solo un ejemplo de cómo puede usar análisis de registros en Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="e5fec-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="e5fec-112">Paso 1: Creación de un almacén</span><span class="sxs-lookup"><span data-stu-id="e5fec-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="e5fec-113">Inicie sesión en demasiado[Microsoft Flow](http://flow.microsoft.com)y seleccione **fluye mi**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="e5fec-114">Haga clic en **+ Crear desde cero**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="e5fec-115">Paso 2: Creación de un desencadenador para el flujo</span><span class="sxs-lookup"><span data-stu-id="e5fec-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="e5fec-116">Haga clic en **Search hundreds of connectors and triggers** (Buscar cientos de conectores y desencadenadores).</span><span class="sxs-lookup"><span data-stu-id="e5fec-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="e5fec-117">Tipo de **programación** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5fec-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="e5fec-118">Elija **Programación** y, a continuación, **Programación: Periodicidad**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="e5fec-119">Hola **frecuencia** cuadro Active **día** y Hola **intervalo** cuadro, escriba **1**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="e5fec-120">![Cuadro de diálogo del desencadenador de Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="e5fec-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="e5fec-121">Paso 3: Adición de una acción de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e5fec-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="e5fec-122">Haga clic en **+ Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="e5fec-123">Busque **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="e5fec-124">Haga clic en **Azure Log Analytics: ejecutar consulta y ver resultados**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="e5fec-125">![Ventana Ejecutar consulta de Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="e5fec-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="e5fec-126">Paso 4: Configurar la acción de análisis de registros de Hola</span><span class="sxs-lookup"><span data-stu-id="e5fec-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="e5fec-127">Especifique los detalles de hello para el área de trabajo incluidos Hola Id. de suscripción, grupo de recursos y el nombre de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e5fec-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="e5fec-128">Agregar Hola después toohello de consultas de análisis de registros **consulta** ventana.</span><span class="sxs-lookup"><span data-stu-id="e5fec-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="e5fec-129">Esta es solo una consulta de ejemplo y puede reemplazarla por cualquier otra que devuelva datos.</span><span class="sxs-lookup"><span data-stu-id="e5fec-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="e5fec-130">Seleccione **tabla HTML** para hello **tipo de gráfico**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="e5fec-131">![Acción de Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="e5fec-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="e5fec-132">Paso 5: Configurar el correo electrónico de toosend de flujo de Hola</span><span class="sxs-lookup"><span data-stu-id="e5fec-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="e5fec-133">Haga clic en **Nuevo paso** y, a continuación, en **+ Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="e5fec-134">Busque **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="e5fec-135">Haga clic en **Office 365 Outlook: Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="e5fec-136">![Ventana de selección de Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="e5fec-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="e5fec-137">Especifique la dirección de un destinatario de correo electrónico de Hola Hola **a** ventana y el asunto de correo electrónico de hello en **asunto**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="e5fec-138">Haga clic en cualquier lugar en hello **cuerpo** cuadro.</span><span class="sxs-lookup"><span data-stu-id="e5fec-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="e5fec-139">Se abre una ventana de **contenido dinámico** con los valores de las acciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="e5fec-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="e5fec-140">Seleccione **Cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-140">Select **Body**.</span></span>  <span data-ttu-id="e5fec-141">Se trata de resultados de Hola de consulta Hola Hola acción de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="e5fec-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="e5fec-142">Haga clic en **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="e5fec-143">Hola **es HTML** cuadro, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="e5fec-144">![Ventana de configuración de correo electrónico de Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="e5fec-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="e5fec-145">Paso 6: Guardado y prueba del flujo</span><span class="sxs-lookup"><span data-stu-id="e5fec-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="e5fec-146">Hola **nombre de flujo de** cuadro, agregue un nombre para el flujo y, a continuación, haga clic en **Crear flujo**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="e5fec-147">![Guardar flujo](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="e5fec-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="e5fec-148">flujo de Hello ahora se crea y se ejecutará después de un día que es la programación de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="e5fec-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="e5fec-149">tooimmediately prueba Hola flujo, haga clic en **ejecutar ahora** y, a continuación, **ejecutar flujo**.</span><span class="sxs-lookup"><span data-stu-id="e5fec-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="e5fec-150">![Ejecutar flujo](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="e5fec-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="e5fec-151">Cuando se completa el flujo de hello, comprobar correo Hola del destinatario de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="e5fec-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="e5fec-152">Debe haber recibido un correo electrónico con una continuación de toohello similar de cuerpo:</span><span class="sxs-lookup"><span data-stu-id="e5fec-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Correo electrónico de ejemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="e5fec-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5fec-154">Next steps</span></span>

- <span data-ttu-id="e5fec-155">Más información sobre [búsquedas de registros en Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="e5fec-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="e5fec-156">Más información sobre [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e5fec-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



