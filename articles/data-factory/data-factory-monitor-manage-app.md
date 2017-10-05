---
title: "Supervisión y administración de canalizaciones de datos - Azure | Microsoft Docs"
description: "Aprenda a usar la aplicación de supervisión y administración para supervisar y administrar factorías de datos y canalizaciones de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="5c47e-103">Supervisión y administración de canalizaciones de Azure Data Factory mediante la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="5c47e-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c47e-104">Uso de Azure Portal/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c47e-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="5c47e-105">Uso de la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="5c47e-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="5c47e-106">En este artículo se describe cómo usar la aplicación de supervisión y administración para supervisar, administrar y depurar las canalizaciones de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5c47e-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="5c47e-107">También proporciona información acerca de cómo crear alertas para recibir notificaciones cuando se produzcan errores.</span><span class="sxs-lookup"><span data-stu-id="5c47e-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="5c47e-108">Para empezar a usar la aplicación, vea el vídeo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c47e-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="5c47e-109">La interfaz de usuario que se muestra en el vídeo puede no coincidir exactamente con la que se ve en el portal.</span><span class="sxs-lookup"><span data-stu-id="5c47e-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="5c47e-110">Es algo anterior, pero los conceptos siguen siendo los mismos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="5c47e-111">Inicio de la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="5c47e-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="5c47e-112">Para iniciar la aplicación de supervisión y administración, haga clic en el icono **Monitoring & Manage** (Supervisión y administración), de la hoja **Factoría de datos** de su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Icono de supervisión en la página de inicio de Factoría de datos](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="5c47e-114">La aplicación de supervisión y administración debería abrirse en una ventana independiente.</span><span class="sxs-lookup"><span data-stu-id="5c47e-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![Aplicación de supervisión y administración](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="5c47e-116">Si ve que el explorador web está atascado en "Autorizando...", desactive la casilla **Block third party cookies and site data** (Bloquear cookies y datos de sitios de terceros), o déjela activada y cree una excepción para **login.microsoftonline.com** e intente volver a abrir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5c47e-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="5c47e-117">En la lista Activity Windows (Ventanas de actividad) del panel central, verá una ventana de actividad cada vez que se ejecuta una actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="5c47e-118">Por ejemplo, si la actividad está programada para ejecutarse cada hora durante cinco horas, verá cinco ventanas de actividad asociadas a cinco segmentos de datos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="5c47e-119">Si no ve las ventanas de actividad en la parte inferior de la lista, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c47e-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="5c47e-120">Actualice los filtros de **hora de inicio** y **hora de finalización** en la parte superior para que coincidan con las horas de inicio y finalización de la canalización y, después, haga clic en el botón **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="5c47e-121">La lista Activity Windows (Ventanas de actividad) no se actualiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5c47e-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="5c47e-122">Haga clic en el botón **Refresh** (Actualizar) de la barra de herramientas de la lista **Activity Windows** (Ventanas de actividad).</span><span class="sxs-lookup"><span data-stu-id="5c47e-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="5c47e-123">Si no tiene una aplicación de Data Factory con la que probar estos pasos, realice el tutorial: [Copia de datos de Blob Storage en SQL Database mediante Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="5c47e-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="5c47e-124">Descripción de la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="5c47e-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="5c47e-125">Hay tres pestañas a la izquierda: **Explorador de recursos**, **Vistas de supervisión de** y **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="5c47e-126">La primera pestaña (**Explorador de recursos**) está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5c47e-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="5c47e-127">Explorador de recursos</span><span class="sxs-lookup"><span data-stu-id="5c47e-127">Resource Explorer</span></span>
<span data-ttu-id="5c47e-128">Verá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5c47e-128">You see the following:</span></span>

* <span data-ttu-id="5c47e-129">La **vista de árbol** del Explorador de recursos en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="5c47e-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="5c47e-130">El **vista de diagrama** en la parte superior del panel central.</span><span class="sxs-lookup"><span data-stu-id="5c47e-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="5c47e-131">La lista **Activity Windows** (Ventanas de actividad) en la parte inferior del panel central.</span><span class="sxs-lookup"><span data-stu-id="5c47e-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="5c47e-132">Las pestañas **Properties** (Propiedades), **Activity Window Explorer** (Explorador de ventanas de actividad) y **Script** en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="5c47e-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="5c47e-133">En el Explorador de recursos, aparecen todos los recursos (canalizaciones, conjuntos de datos, servicios vinculados) de la factoría de datos en una vista de árbol.</span><span class="sxs-lookup"><span data-stu-id="5c47e-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="5c47e-134">Al seleccionar un objeto en el Explorador de recursos:</span><span class="sxs-lookup"><span data-stu-id="5c47e-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="5c47e-135">Se resalta la entidad de Factoría de datos asociada en la vista de diagrama.</span><span class="sxs-lookup"><span data-stu-id="5c47e-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="5c47e-136">Las [ventanas de actividad asociadas](data-factory-scheduling-and-execution.md) se resaltan en la lista Activity Windows (Ventanas de actividad) de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5c47e-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="5c47e-137">Las propiedades del objeto seleccionado aparecen en la ventana Propiedades (panel derecho).</span><span class="sxs-lookup"><span data-stu-id="5c47e-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="5c47e-138">Aparece la definición de JSON del objeto seleccionado, si procede.</span><span class="sxs-lookup"><span data-stu-id="5c47e-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="5c47e-139">Por ejemplo: un servicio vinculado, un conjunto de datos o una canalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Explorador de recursos](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="5c47e-141">Consulte el artículo sobre [programación y ejecución](data-factory-scheduling-and-execution.md) para información conceptual detallada sobre las ventanas de actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="5c47e-142">Vista de diagrama</span><span class="sxs-lookup"><span data-stu-id="5c47e-142">Diagram View</span></span>
<span data-ttu-id="5c47e-143">La vista de diagrama de una factoría de datos es un panel único para supervisar y administrar una factoría de datos y sus recursos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="5c47e-144">Cuando seleccione una entidad de Factoría de datos (conjunto de datos o canalización) en la vista de diagrama:</span><span class="sxs-lookup"><span data-stu-id="5c47e-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="5c47e-145">La entidad de la factoría de datos se selecciona en la vista de árbol.</span><span class="sxs-lookup"><span data-stu-id="5c47e-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="5c47e-146">Las ventanas de actividad asociadas se resaltan en la lista Activity Windows (Ventanas de actividad).</span><span class="sxs-lookup"><span data-stu-id="5c47e-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="5c47e-147">Las propiedades del objeto seleccionado aparecen en la ventana Propiedades.</span><span class="sxs-lookup"><span data-stu-id="5c47e-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="5c47e-148">Si la canalización está habilitada (es decir, no en estado de pausa), se indicará con una línea verde:</span><span class="sxs-lookup"><span data-stu-id="5c47e-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Canalización en ejecución](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="5c47e-150">Para pausar, reanudar o terminar una canalización, selecciónela en la vista de diagrama y utilice los botones de la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![Pausa/reanudación en la barra de comandos](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="5c47e-152">En la vista de diagrama hay tres botones en la barra de comandos para la canalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="5c47e-153">Puede usar el segundo botón para pausar la canalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="5c47e-154">La pausa no termina las actividades que se estén ejecutando, estas continúan hasta su finalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="5c47e-155">El tercer botón pausa la canalización y termina las actividades que se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="5c47e-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="5c47e-156">El primer botón reanuda la canalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="5c47e-157">Cuando la canalización está en pausa, su color cambia.</span><span class="sxs-lookup"><span data-stu-id="5c47e-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="5c47e-158">Por ejemplo, la siguiente imagen muestra una canalización en pausa:</span><span class="sxs-lookup"><span data-stu-id="5c47e-158">For example, a paused pipeline looks like in the following image:</span></span> 

![Canalización en pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="5c47e-160">Con la tecla Ctrl puede realizar una selección múltiple de dos o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="5c47e-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="5c47e-161">Puede utilizar los botones de la barra de comandos para pausar y reanudar varias canalizaciones a la vez.</span><span class="sxs-lookup"><span data-stu-id="5c47e-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="5c47e-162">También puede hacer clic con el botón derecho en una canalización y seleccionar las opciones apropiadas para suspender, reanudar o terminar una canalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![Menú contextual de la canalización](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="5c47e-164">Haga clic en la opción **Abrir canalización** para ver todas las actividades de la canalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![Menú Abrir canalización](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="5c47e-166">En la vista de canalización que se abre, verá todas las actividades de la canalización.</span><span class="sxs-lookup"><span data-stu-id="5c47e-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="5c47e-167">En este ejemplo, solamente hay una actividad: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="5c47e-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Canalización abierta](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="5c47e-169">Para volver a la vista anterior, haga clic en el nombre de la factoría de datos en el menú de la ruta de navegación en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="5c47e-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="5c47e-170">En la vista de canalización, cuando se selecciona un conjunto de datos de salida o cuando se pasa el mouse sobre él, se ve la ventana emergente Activity Windows (Ventanas de actividad) de dicho conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Ventana emergente Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="5c47e-172">Puede hacer clic en una ventana de actividad para ver sus detalles en la ventana **Propiedades** del panel derecho.</span><span class="sxs-lookup"><span data-stu-id="5c47e-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Propiedades de la ventana de actividad](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="5c47e-174">En el panel derecho, cambie a la pestaña **Activity Window Explorer** (Explorador de ventanas de actividad) para ver más información.</span><span class="sxs-lookup"><span data-stu-id="5c47e-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="5c47e-176">También verá las **variables resueltas** de cada intento de ejecución de una actividad en la sección **Intentos**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Variables resueltas](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="5c47e-178">Cambie a la pestaña **Script** para ver la definición del script de JSON del objeto seleccionado.</span><span class="sxs-lookup"><span data-stu-id="5c47e-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Pestaña de script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="5c47e-180">Puede ver las ventanas de actividad en tres lugares:</span><span class="sxs-lookup"><span data-stu-id="5c47e-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="5c47e-181">En el elemento emergente Activity Windows (Ventanas de actividad) en la vista de diagrama (panel central).</span><span class="sxs-lookup"><span data-stu-id="5c47e-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="5c47e-182">En Activity Window Explorer (Explorador de ventanas de actividad) en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="5c47e-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="5c47e-183">En la lista Activity Windows (Ventanas de actividad) en el panel inferior.</span><span class="sxs-lookup"><span data-stu-id="5c47e-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="5c47e-184">En el elemento emergente Activity Windows (Ventanas de actividad) y Activity Window Explorer (Explorador de ventanas de actividad) puede desplazarse a la semana anterior o siguiente con las flechas izquierda y derecha.</span><span class="sxs-lookup"><span data-stu-id="5c47e-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Flechas izquierda/derecha de Activity Window Explorer (Explorador de ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="5c47e-186">En la parte inferior de la vista de diagrama aparecen estos botones: acercar, alejar, ajustar, 100 % y bloquear el diseño.</span><span class="sxs-lookup"><span data-stu-id="5c47e-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="5c47e-187">El botón para **bloquear el diseño** mover tablas y canalizaciones por error en la vista de diagrama.</span><span class="sxs-lookup"><span data-stu-id="5c47e-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="5c47e-188">Está activado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5c47e-188">It's on by default.</span></span> <span data-ttu-id="5c47e-189">Puede desactivarlo y mover las entidades por el diagrama.</span><span class="sxs-lookup"><span data-stu-id="5c47e-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="5c47e-190">Si lo desactiva, puede usar el último botón para colocar automáticamente las tablas y las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="5c47e-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="5c47e-191">También puede acercar o alejar con la rueda del mouse.</span><span class="sxs-lookup"><span data-stu-id="5c47e-191">You can also zoom in or out by using the mouse wheel.</span></span>

![Comandos de ampliación de la vista de diagrama](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="5c47e-193">Lista Activity Windows (Ventanas de actividad)</span><span class="sxs-lookup"><span data-stu-id="5c47e-193">Activity Windows list</span></span>
<span data-ttu-id="5c47e-194">La lista Activity Windows (Ventanas de actividad) de la parte inferior del panel central muestra todas las ventanas de actividad del conjunto de datos seleccionado en el Explorador de recursos o en la vista de diagrama.</span><span class="sxs-lookup"><span data-stu-id="5c47e-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="5c47e-195">De forma predeterminada, la lista está en orden descendente, lo que significa que en la parte superior aparece la ventana de actividad más reciente.</span><span class="sxs-lookup"><span data-stu-id="5c47e-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="5c47e-197">Esta lista no se actualiza automáticamente, por lo que debe usar el botón Actualizar de la barra de herramientas para hacerlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="5c47e-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="5c47e-198">Las ventanas de actividad pueden estar en uno de los siguientes estados:</span><span class="sxs-lookup"><span data-stu-id="5c47e-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="5c47e-199">Estado</span><span class="sxs-lookup"><span data-stu-id="5c47e-199">Status</span></span></th><th align="left"><span data-ttu-id="5c47e-200">Subestado</span><span class="sxs-lookup"><span data-stu-id="5c47e-200">Substatus</span></span></th><th align="left"><span data-ttu-id="5c47e-201">Description</span><span class="sxs-lookup"><span data-stu-id="5c47e-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="5c47e-202">En espera</span><span class="sxs-lookup"><span data-stu-id="5c47e-202">Waiting</span></span></td><td><span data-ttu-id="5c47e-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="5c47e-203">ScheduleTime</span></span></td><td><span data-ttu-id="5c47e-204">Aún no es momento de ejecutar la ventana de actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="5c47e-205">DatasetDependencies</span></span></td><td><span data-ttu-id="5c47e-206">Las dependencias de nivel superior no están listas.</span><span class="sxs-lookup"><span data-stu-id="5c47e-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="5c47e-207">ComputeResources</span></span></td><td><span data-ttu-id="5c47e-208">No están disponibles los recursos de proceso.</span><span class="sxs-lookup"><span data-stu-id="5c47e-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="5c47e-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="5c47e-210">Todas las instancias de actividad están ocupadas con la ejecución de otras ventanas de actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="5c47e-211">ActivityResume</span></span></td><td><span data-ttu-id="5c47e-212">La actividad está en pausa y no puede ejecutar las ventanas de actividad hasta que se reanude.</span><span class="sxs-lookup"><span data-stu-id="5c47e-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-213">Retry</span><span class="sxs-lookup"><span data-stu-id="5c47e-213">Retry</span></span></td><td><span data-ttu-id="5c47e-214">Se está volviendo a intentar la ejecución de la actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-215">Validación</span><span class="sxs-lookup"><span data-stu-id="5c47e-215">Validation</span></span></td><td><span data-ttu-id="5c47e-216">Aún no ha iniciado la validación.</span><span class="sxs-lookup"><span data-stu-id="5c47e-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="5c47e-217">ValidationRetry</span></span></td><td><span data-ttu-id="5c47e-218">La validación está esperando un reintento.</span><span class="sxs-lookup"><span data-stu-id="5c47e-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="5c47e-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="5c47e-219">InProgress</span></span></td><td><span data-ttu-id="5c47e-220">Validating</span><span class="sxs-lookup"><span data-stu-id="5c47e-220">Validating</span></span></td><td><span data-ttu-id="5c47e-221">Validación en curso.</span><span class="sxs-lookup"><span data-stu-id="5c47e-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="5c47e-222">La ventana de actividad se está procesando.</span><span class="sxs-lookup"><span data-stu-id="5c47e-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="5c47e-223">Con error</span><span class="sxs-lookup"><span data-stu-id="5c47e-223">Failed</span></span></td><td><span data-ttu-id="5c47e-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="5c47e-224">TimedOut</span></span></td><td><span data-ttu-id="5c47e-225">La ejecución de la actividad tardó más tiempo del permitido por la actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="5c47e-226">Canceled</span></span></td><td><span data-ttu-id="5c47e-227">La ventana de actividad fue cancelada por acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="5c47e-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-228">Validación</span><span class="sxs-lookup"><span data-stu-id="5c47e-228">Validation</span></span></td><td><span data-ttu-id="5c47e-229">Error de validación.</span><span class="sxs-lookup"><span data-stu-id="5c47e-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="5c47e-230">No se pudo generar o validar la ventana de actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="5c47e-231">Ready</span><span class="sxs-lookup"><span data-stu-id="5c47e-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="5c47e-232">La ventana de actividad está lista para su uso.</span><span class="sxs-lookup"><span data-stu-id="5c47e-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="5c47e-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="5c47e-234">La ventana de actividad no se ha procesado.</span><span class="sxs-lookup"><span data-stu-id="5c47e-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5c47e-235">None</span><span class="sxs-lookup"><span data-stu-id="5c47e-235">None</span></span></td><td>-</td><td><span data-ttu-id="5c47e-236">Una ventana de actividad que existía con un estado distinto, pero que se ha restablecido.</span><span class="sxs-lookup"><span data-stu-id="5c47e-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="5c47e-237">Al hacer clic en una de las ventanas de actividad de la lista, verá sus detalles en **Activity Windows Explorer** (Explorador de ventanas de actividad) o en la ventana **Propiedades** de la derecha.</span><span class="sxs-lookup"><span data-stu-id="5c47e-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="5c47e-239">Actualizar las ventanas de actividad</span><span class="sxs-lookup"><span data-stu-id="5c47e-239">Refresh activity windows</span></span>
<span data-ttu-id="5c47e-240">Los detalles no se actualizan automáticamente, por lo que debe usar el segundo botón, Actualizar, de la barra de comandos para actualizar manualmente la lista de ventanas de actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="5c47e-241">Ventana Propiedades</span><span class="sxs-lookup"><span data-stu-id="5c47e-241">Properties window</span></span>
<span data-ttu-id="5c47e-242">La ventana Propiedades está en el panel del extremo derecho de la Aplicación de supervisión y administración.</span><span class="sxs-lookup"><span data-stu-id="5c47e-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Ventana Propiedades](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="5c47e-244">Muestra las propiedades del elemento seleccionado en el Explorador de recursos (en la vista de árbol), la vista de diagrama o la lista Activity Windows (Ventanas de actividad).</span><span class="sxs-lookup"><span data-stu-id="5c47e-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="5c47e-245">Activity Window Explorer</span><span class="sxs-lookup"><span data-stu-id="5c47e-245">Activity Window Explorer</span></span>
<span data-ttu-id="5c47e-246">La ventana **Activity Window Explorer** (Explorador de ventanas de actividad) se encuentra en el panel más a la derecha de la aplicación de supervisión y administración.</span><span class="sxs-lookup"><span data-stu-id="5c47e-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="5c47e-247">Muestra detalles de la ventana de actividad seleccionada en la ventana emergente Activity Windows (Ventanas de actividad) o en la lista Activity Windows (Ventanas de actividad).</span><span class="sxs-lookup"><span data-stu-id="5c47e-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="5c47e-249">Puede cambiar a una ventana de actividad diferente haciendo clic en ella en la vista de calendario de la parte superior.</span><span class="sxs-lookup"><span data-stu-id="5c47e-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="5c47e-250">También puede usar los botones de flecha izquierda/flecha derecha de la parte superior para ver las ventanas de actividad de la semana anterior o siguiente.</span><span class="sxs-lookup"><span data-stu-id="5c47e-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="5c47e-251">Puede usar los botones de la barra de herramientas del panel inferior para volver a ejecutar la ventana de actividad o actualizar los detalles del panel.</span><span class="sxs-lookup"><span data-stu-id="5c47e-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="5c47e-252">Script</span><span class="sxs-lookup"><span data-stu-id="5c47e-252">Script</span></span>
<span data-ttu-id="5c47e-253">Puede usar la pestaña **Script** para ver la definición de JSON de la entidad de Factoría de datos seleccionada (servicio vinculado, conjunto de datos o canalización).</span><span class="sxs-lookup"><span data-stu-id="5c47e-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Pestaña de script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="5c47e-255">Vistas de uso del sistema</span><span class="sxs-lookup"><span data-stu-id="5c47e-255">Use system views</span></span>
<span data-ttu-id="5c47e-256">La aplicación de supervisión y administración incluye vistas del sistema pregeneradas (**Recent activity windows** [Ventanas de actividad recientes], **Failed activity windows** [Ventanas de actividades con error] y **In-Progress activity windows** [Ventanas de actividad en curso]) que permiten ver las ventanas de actividad recientes, las que contienen errores o las que están en curso de su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="5c47e-257">Cambie a la pestaña **Monitoring Views** (Vistas de supervisión) de la izquierda haciendo clic en ella.</span><span class="sxs-lookup"><span data-stu-id="5c47e-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![Pestaña Vistas de supervisión](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="5c47e-259">Actualmente, hay tres vistas del sistema compatibles.</span><span class="sxs-lookup"><span data-stu-id="5c47e-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="5c47e-260">Seleccione una opción para ver las ventanas de actividad recientes, las ventanas de actividad con error o las ventanas de actividad en curso en la lista Activity Windows (Ventanas de actividad) (en la parte inferior del panel central).</span><span class="sxs-lookup"><span data-stu-id="5c47e-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="5c47e-261">Al seleccionar la opción **Recent activity windows** (Ventanas de actividad reciente), se ven todas las ventanas de actividad reciente en orden descendente de **hora del último intento**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="5c47e-262">Puede usar la vista **Failed activity windows** (Ventanas de actividad con error) para ver todas las ventanas de actividad que contengan errores de la lista.</span><span class="sxs-lookup"><span data-stu-id="5c47e-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="5c47e-263">Seleccione una ventana de actividad con error de la lista para ver sus detalles en la ventana **Propiedades** o en **Activity Window Explorer** (Explorador de ventanas de actividad).</span><span class="sxs-lookup"><span data-stu-id="5c47e-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="5c47e-264">También puede descargar los registros de una ventana de actividad con error.</span><span class="sxs-lookup"><span data-stu-id="5c47e-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="5c47e-265">Ordenado y filtrado de las ventanas de actividad</span><span class="sxs-lookup"><span data-stu-id="5c47e-265">Sort and filter activity windows</span></span>
<span data-ttu-id="5c47e-266">Cambie la configuración de **hora de inicio** y **hora de finalización** en la barra de comandos para filtrar las ventanas de actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="5c47e-267">Después de cambiar la hora de inicio y de finalización, haga clic en el botón situado junto a la hora de finalización para actualizar la lista Activity Windows (Ventanas de actividad).</span><span class="sxs-lookup"><span data-stu-id="5c47e-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Horas de inicio y finalización](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="5c47e-269">Actualmente, en la aplicación de supervisión y administración todas las horas están en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="5c47e-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="5c47e-270">En la **lista de ventanas de actividad**, haga clic en el nombre de una columna (por ejemplo, Estado).</span><span class="sxs-lookup"><span data-stu-id="5c47e-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Menú de columna de la lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="5c47e-272">Puede realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="5c47e-272">You can do the following:</span></span>

* <span data-ttu-id="5c47e-273">Ordenar en orden ascendente.</span><span class="sxs-lookup"><span data-stu-id="5c47e-273">Sort in ascending order.</span></span>
* <span data-ttu-id="5c47e-274">Ordenar en orden descendente.</span><span class="sxs-lookup"><span data-stu-id="5c47e-274">Sort in descending order.</span></span>
* <span data-ttu-id="5c47e-275">Filtrar por uno o más valores (Ready [Listo], Waiting [En espera], etc.).</span><span class="sxs-lookup"><span data-stu-id="5c47e-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="5c47e-276">Cuando especifique un filtro en una columna, verá que el botón de filtro se habilita para esa columna, lo cual indica que los valores de la columna están filtrados.</span><span class="sxs-lookup"><span data-stu-id="5c47e-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Filtro de columna de la lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="5c47e-278">Puede usar la misma ventana emergente para borrar filtros.</span><span class="sxs-lookup"><span data-stu-id="5c47e-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="5c47e-279">Para borrar todos los filtros de la lista Activity Windows (Ventanas de actividad), haga clic en el botón para borrar el filtro de la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="5c47e-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Borrado de todos los filtros de la lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="5c47e-281">Acciones por lotes</span><span class="sxs-lookup"><span data-stu-id="5c47e-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="5c47e-282">Volver a ejecutar las ventanas de actividad seleccionadas</span><span class="sxs-lookup"><span data-stu-id="5c47e-282">Rerun selected activity windows</span></span>
<span data-ttu-id="5c47e-283">Seleccione una ventana de actividad, haga clic en la flecha hacia abajo del primer botón de la barra de comandos y seleccione **Rerun** (Volver a ejecutar) / **Rerun with upstream in pipeline** (Volver a ejecutar con canal de subida en la canalización).</span><span class="sxs-lookup"><span data-stu-id="5c47e-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="5c47e-284">Al seleccionar la opción **Rerun with upstream in pipeline** (Volver a ejecutar con canal de subida en la canalización), también se vuelven a ejecutar todas las ventanas de actividad con canal de subida.</span><span class="sxs-lookup"><span data-stu-id="5c47e-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="5c47e-285">![Volver a ejecutar una ventana de actividad](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="5c47e-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="5c47e-286">También puede seleccionar varias ventanas de actividad en la lista y volver a ejecutarlas al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="5c47e-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="5c47e-287">Puede filtrar las ventanas de actividad según el estado (por ejemplo, **Failed** [Con error]) y volver a ejecutar las ventanas de actividad con error tras corregir el problema que provocaba el error en las ventanas de actividad.</span><span class="sxs-lookup"><span data-stu-id="5c47e-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="5c47e-288">Vea la siguiente sección para obtener más información sobre el filtrado de ventanas de actividad en la lista.</span><span class="sxs-lookup"><span data-stu-id="5c47e-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="5c47e-289">Pausar y reanudar varias canalizaciones</span><span class="sxs-lookup"><span data-stu-id="5c47e-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="5c47e-290">También puede realizar una selección múltiple de dos o más canalizaciones con la tecla Ctrl.</span><span class="sxs-lookup"><span data-stu-id="5c47e-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="5c47e-291">Puede utilizar los botones de la barra de comandos (que se resaltan en el rectángulo rojo en la imagen siguiente) para pausarlas o reanudarlas.</span><span class="sxs-lookup"><span data-stu-id="5c47e-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Pausa/reanudación en la barra de comandos](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="5c47e-293">Creación de alertas</span><span class="sxs-lookup"><span data-stu-id="5c47e-293">Create alerts</span></span>
<span data-ttu-id="5c47e-294">La página **Alertas** le permite crear una alerta nueva, así como ver, editar o eliminar las alertas existentes.</span><span class="sxs-lookup"><span data-stu-id="5c47e-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="5c47e-295">También puede habilitar o deshabilitar una alerta.</span><span class="sxs-lookup"><span data-stu-id="5c47e-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="5c47e-296">Haga clic en la pestaña Alertas para ver la pestaña **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![Pestaña Alertas](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="5c47e-298">Para crear una alerta</span><span class="sxs-lookup"><span data-stu-id="5c47e-298">To create an alert</span></span>
1. <span data-ttu-id="5c47e-299">Haga clic en **Agregar alerta** para agregar una alerta.</span><span class="sxs-lookup"><span data-stu-id="5c47e-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="5c47e-300">Verá la página **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-300">You see the **Details** page.</span></span>

    ![Crear alertas: página de detalles](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="5c47e-302">Especifique el **nombre** y la **descripción** de la alerta y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="5c47e-303">Verá la página **Filtros** .</span><span class="sxs-lookup"><span data-stu-id="5c47e-303">You should see the **Filters** page.</span></span>

    ![Crear alertas: página de filtros](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="5c47e-305">Seleccione el **evento**, el **estado** y el **subestado** (opcional) sobre los que desea que el servicio Data Factory le alerte y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="5c47e-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="5c47e-306">Verá la página **Destinatarios** .</span><span class="sxs-lookup"><span data-stu-id="5c47e-306">You should see the **Recipients** page.</span></span>

    ![Crear alertas: página de destinatarios](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="5c47e-308">Seleccione la opción **Email subscription admins** (Administradores de suscripciones de correo electrónico) o escriba un **correo electrónico de administrador adicional** y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="5c47e-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="5c47e-309">Debería ver la alerta en la lista.</span><span class="sxs-lookup"><span data-stu-id="5c47e-309">You should see the alert in the list.</span></span>

    ![Lista de alertas](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="5c47e-311">En la lista de alertas, use los botones asociados con la alerta para editarla, eliminarla, habilitarla o deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="5c47e-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="5c47e-312">Evento/estado/subestado</span><span class="sxs-lookup"><span data-stu-id="5c47e-312">Event/status/substatus</span></span>
<span data-ttu-id="5c47e-313">En la tabla siguiente se ofrece una lista de los eventos y los estados (y subestados) disponibles.</span><span class="sxs-lookup"><span data-stu-id="5c47e-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="5c47e-314">Nombre del evento</span><span class="sxs-lookup"><span data-stu-id="5c47e-314">Event name</span></span> | <span data-ttu-id="5c47e-315">Estado</span><span class="sxs-lookup"><span data-stu-id="5c47e-315">Status</span></span> | <span data-ttu-id="5c47e-316">Subestado</span><span class="sxs-lookup"><span data-stu-id="5c47e-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c47e-317">Ejecución de actividad iniciada</span><span class="sxs-lookup"><span data-stu-id="5c47e-317">Activity Run Started</span></span> |<span data-ttu-id="5c47e-318">Started</span><span class="sxs-lookup"><span data-stu-id="5c47e-318">Started</span></span> |<span data-ttu-id="5c47e-319">Iniciando</span><span class="sxs-lookup"><span data-stu-id="5c47e-319">Starting</span></span> |
| <span data-ttu-id="5c47e-320">Ejecución de actividad finalizada</span><span class="sxs-lookup"><span data-stu-id="5c47e-320">Activity Run Finished</span></span> |<span data-ttu-id="5c47e-321">Correcto</span><span class="sxs-lookup"><span data-stu-id="5c47e-321">Succeeded</span></span> |<span data-ttu-id="5c47e-322">Correcto</span><span class="sxs-lookup"><span data-stu-id="5c47e-322">Succeeded</span></span> |
| <span data-ttu-id="5c47e-323">Ejecución de actividad finalizada</span><span class="sxs-lookup"><span data-stu-id="5c47e-323">Activity Run Finished</span></span> |<span data-ttu-id="5c47e-324">Con error</span><span class="sxs-lookup"><span data-stu-id="5c47e-324">Failed</span></span> |<span data-ttu-id="5c47e-325">Asignación de recursos errónea</span><span class="sxs-lookup"><span data-stu-id="5c47e-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="5c47e-326">Ejecución con errores</span><span class="sxs-lookup"><span data-stu-id="5c47e-326">Failed Execution</span></span><br/><br/><span data-ttu-id="5c47e-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="5c47e-327">Timed Out</span></span><br/><br/><span data-ttu-id="5c47e-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="5c47e-328">Failed Validation</span></span><br/><br/><span data-ttu-id="5c47e-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="5c47e-329">Abandoned</span></span> |
| <span data-ttu-id="5c47e-330">Creación de clúster de HDI a petición iniciada</span><span class="sxs-lookup"><span data-stu-id="5c47e-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="5c47e-331">Started</span><span class="sxs-lookup"><span data-stu-id="5c47e-331">Started</span></span> |-|
| <span data-ttu-id="5c47e-332">Creación correcta de clúster de HDI a petición</span><span class="sxs-lookup"><span data-stu-id="5c47e-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="5c47e-333">Correcto</span><span class="sxs-lookup"><span data-stu-id="5c47e-333">Succeeded</span></span> |-|
| <span data-ttu-id="5c47e-334">Clúster de HDI a petición eliminado</span><span class="sxs-lookup"><span data-stu-id="5c47e-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="5c47e-335">Correcto</span><span class="sxs-lookup"><span data-stu-id="5c47e-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="5c47e-336">Edición, eliminación o deshabilitación de alertas</span><span class="sxs-lookup"><span data-stu-id="5c47e-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="5c47e-337">Utilice los siguientes botones (resaltados en rojo) para editar, eliminar o deshabilitar una alerta.</span><span class="sxs-lookup"><span data-stu-id="5c47e-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![Botones de alertas](./media/data-factory-monitor-manage-app/AlertButtons.png)
