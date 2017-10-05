---
title: "Automatización de procesos de Azure Log Analytics con Microsoft Flow"
description: "Obtenga información acerca de cómo puede utilizar Microsoft Flow para automatizar rápidamente los procesos repetibles mediante el conector de Azure Log Analytics."
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
ms.openlocfilehash: 4955f90de06cd720d78c5bb60c0adcd7dc633245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="automate-log-analytics-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="0d0bd-103">Automatización de procesos de Log Analytics con el conector para Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="0d0bd-103">Automate Log Analytics processes with the connector for Microsoft Flow</span></span>
<span data-ttu-id="0d0bd-104">[Microsoft Flow](https://ms.flow.microsoft.com) le permite crear flujos de trabajo automatizados, con cientos de acciones para diversos servicios.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="0d0bd-105">La salida de una acción se puede utilizar como entrada de otra lo que le permite crear una integración entre los diferentes servicios.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-105">Output from one action can be used as input to another allowing you to create integration between different services.</span></span>  <span data-ttu-id="0d0bd-106">El conector de Azure Log Analytics para Microsoft Flow le permite compilar flujos de trabajo que incluyen datos recuperados de las búsquedas de registros de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="0d0bd-107">Por ejemplo, puede utilizar Microsoft Flow para usar los datos de Log Analytics incluidos en una notificación de correo electrónico de Office 365, crear un error en Visual Studio Team Services o publicar un mensaje de Slack.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="0d0bd-108">Puede desencadenar un flujo de trabajo mediante una programación simple o a partir de alguna acción de un servicio conectado, como cuando se recibe un correo electrónico o un tweet.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="0d0bd-109">El conector de Azure Log Analytics para Microsoft Flow requiere que el área de trabajo se actualice al nuevo lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-109">The Azure Log Analytics connector for Microsoft Flow requires your workspace to be upgraded to the new Log Analytics query language.</span></span> <span data-ttu-id="0d0bd-110">Puede obtener más información sobre el nuevo lenguaje y conocer el procedimiento para actualizar el área de trabajo en [Actualización del área de trabajo de Azure Log Analytics para la nueva búsqueda de registros](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="0d0bd-110">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="0d0bd-111">El tutorial de este artículo le muestra cómo crear un flujo que envíe automáticamente los resultados de una búsqueda de registros de Log Analytics por correo electrónico, lo cual es solo un ejemplo de cómo puede usar Log Analytics en Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-111">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="0d0bd-112">Paso 1: Creación de un almacén</span><span class="sxs-lookup"><span data-stu-id="0d0bd-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="0d0bd-113">Inicie sesión en [Microsoft Flow](http://flow.microsoft.com) y seleccione **Mis flujos**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-113">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="0d0bd-114">Haga clic en **+ Crear desde cero**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="0d0bd-115">Paso 2: Creación de un desencadenador para el flujo</span><span class="sxs-lookup"><span data-stu-id="0d0bd-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="0d0bd-116">Haga clic en **Search hundreds of connectors and triggers** (Buscar cientos de conectores y desencadenadores).</span><span class="sxs-lookup"><span data-stu-id="0d0bd-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="0d0bd-117">Escriba **programación** en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-117">Type **Schedule** in the search box.</span></span>
3. <span data-ttu-id="0d0bd-118">Elija **Programación** y, a continuación, **Programación: Periodicidad**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="0d0bd-119">En el cuadro **Frecuencia**, seleccione **Día** y, en el cuadro **Intervalo**, escriba **1**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-119">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="0d0bd-120">![Cuadro de diálogo del desencadenador de Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="0d0bd-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="0d0bd-121">Paso 3: Adición de una acción de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0bd-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="0d0bd-122">Haga clic en **+ Nuevo paso** y, a continuación, en **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="0d0bd-123">Busque **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="0d0bd-124">Haga clic en **Azure Log Analytics: ejecutar consulta y ver resultados**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="0d0bd-125">![Ventana Ejecutar consulta de Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="0d0bd-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-the-log-analytics-action"></a><span data-ttu-id="0d0bd-126">Paso 4: Configuración de la acción de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d0bd-126">Step 4: Configure the Log Analytics action</span></span>

1. <span data-ttu-id="0d0bd-127">Especifique los detalles del área de trabajo incluido el identificador de suscripción, el grupo de recursos y el nombre del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-127">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="0d0bd-128">En la ventana **Consulta** , agregue la siguiente consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-128">Add the following Log Analytics query to the **Query** window.</span></span>  <span data-ttu-id="0d0bd-129">Esta es solo una consulta de ejemplo y puede reemplazarla por cualquier otra que devuelva datos.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="0d0bd-130">En el cuadro **Tipo de gráfico**, seleccione **Tabla HTML**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-130">Select **HTML Table** for the **Chart Type**.</span></span><br><br><span data-ttu-id="0d0bd-131">![Acción de Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="0d0bd-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-the-flow-to-send-email"></a><span data-ttu-id="0d0bd-132">Paso 5: Configuración del flujo para enviar correo electrónico</span><span class="sxs-lookup"><span data-stu-id="0d0bd-132">Step 5: Configure the flow to send email</span></span>

1. <span data-ttu-id="0d0bd-133">Haga clic en **Nuevo paso** y, a continuación, en **+ Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="0d0bd-134">Busque **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="0d0bd-135">Haga clic en **Office 365 Outlook: Enviar un correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="0d0bd-136">![Ventana de selección de Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="0d0bd-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="0d0bd-137">Especifique la dirección de correo electrónico de un destinatario en la ventana **Para** y un asunto para el correo electrónico en **Asunto**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-137">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span></span>
5. <span data-ttu-id="0d0bd-138">Haga clic en cualquier lugar del cuadro **Cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-138">Click anywhere in the **Body** box.</span></span>  <span data-ttu-id="0d0bd-139">Se abre una ventana de **contenido dinámico** con los valores de las acciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="0d0bd-140">Seleccione **Cuerpo**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-140">Select **Body**.</span></span>  <span data-ttu-id="0d0bd-141">Estos son los resultados de la consulta de la acción de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-141">This is the results of the query in the Log Analytics action.</span></span>
6. <span data-ttu-id="0d0bd-142">Haga clic en **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="0d0bd-143">En el campo **Es HTML**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-143">In the **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="0d0bd-144">![Ventana de configuración de correo electrónico de Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="0d0bd-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="0d0bd-145">Paso 6: Guardado y prueba del flujo</span><span class="sxs-lookup"><span data-stu-id="0d0bd-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="0d0bd-146">En el cuadro **Nombre de flujo**, agregue un nombre para el flujo y, a continuación, haga clic en **Crear flujo**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-146">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="0d0bd-147">![Guardar flujo](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="0d0bd-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="0d0bd-148">El flujo ya se ha creado y se ejecutará una vez transcurrido un día, que es la programación que especificó.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-148">The flow is now created and will run after a day which is the schedule you specified.</span></span> 
3. <span data-ttu-id="0d0bd-149">Para probar el flujo de inmediato, haga clic en **Ejecutar ahora** y, a continuación, en **Ejecutar flujo**.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-149">To immediately test the flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="0d0bd-150">![Ejecutar flujo](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="0d0bd-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="0d0bd-151">Cuando se complete el flujo, compruebe el correo electrónico del destinatario que especificó.</span><span class="sxs-lookup"><span data-stu-id="0d0bd-151">When the flow completes, check the mail of the recipient that you specified.</span></span>  <span data-ttu-id="0d0bd-152">Debe haber recibido un correo electrónico con un cuerpo similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="0d0bd-152">You should have received a mail with a body similar to the following:</span></span><br><br>![Correo electrónico de ejemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="0d0bd-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d0bd-154">Next steps</span></span>

- <span data-ttu-id="0d0bd-155">Más información sobre [búsquedas de registros en Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="0d0bd-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="0d0bd-156">Más información sobre [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0d0bd-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



