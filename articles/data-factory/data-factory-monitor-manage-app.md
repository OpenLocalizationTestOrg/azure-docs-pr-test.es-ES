---
title: aaaMonitor y administrar las canalizaciones de datos - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toomonitor de aplicación de supervisión y administración y administrar las canalizaciones y los generadores de datos de Azure."
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
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="6af57-103">Supervisar y administrar las canalizaciones de factoría de datos de Azure mediante la aplicación de supervisión y administración de hello</span><span class="sxs-lookup"><span data-stu-id="6af57-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6af57-104">Uso de Azure Portal/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6af57-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="6af57-105">Uso de la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="6af57-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="6af57-106">Este artículo describe cómo toouse Hola toomonitor de aplicación de supervisión y administración, administrar y depurar las canalizaciones de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="6af57-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="6af57-107">También se proporciona información sobre cómo toocreate alertas tooget una notificación cuando se produzcan errores.</span><span class="sxs-lookup"><span data-stu-id="6af57-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="6af57-108">Puede empezar con el uso de la aplicación hello por ver Hola después de vídeo:</span><span class="sxs-lookup"><span data-stu-id="6af57-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="6af57-109">interfaz de usuario de Hola que se muestra en hello vídeo puede no coincidir lo que se ve en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="6af57-110">Es ligeramente más antiguo, pero conceptos permanecen Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="6af57-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="6af57-111">Inicie la aplicación de supervisión y administración de hello</span><span class="sxs-lookup"><span data-stu-id="6af57-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="6af57-112">Hola toolaunch Monitor y la aplicación de administración, haga clic en hello **Monitor & administrar** icono hello **factoría de datos** hoja de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="6af57-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Icono página principal de hello factoría de datos de supervisión](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="6af57-114">Debería ver aplicación de supervisión y administración de hello abrir en una ventana independiente.</span><span class="sxs-lookup"><span data-stu-id="6af57-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![Aplicación de supervisión y administración](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="6af57-116">Si ve ese explorador web de hello está atascado en "Autorizar …", desactive hello **bloquear las cookies de terceros y datos de sitio** casilla de verificación--o mantener aún seleccionada, cree una excepción para **login.microsoftonline.com** y, a continuación, vuelva a intentarlo tooopen Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="6af57-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="6af57-117">En la lista de ventanas de la actividad de hello en el panel central de hello, verá una ventana de actividad para cada ejecución de una actividad.</span><span class="sxs-lookup"><span data-stu-id="6af57-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="6af57-118">Por ejemplo, si tiene Hola actividad programada toorun cada hora durante cinco horas, verá cinco ventanas de la actividad asociadas a segmentos de datos de cinco.</span><span class="sxs-lookup"><span data-stu-id="6af57-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="6af57-119">Si no ve las ventanas de la actividad en la lista de hello en parte inferior de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="6af57-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="6af57-120">Hola de actualización **hora de inicio** y **hora de finalización** filtros en Hola toomatch superior Hola inicio y finalización de la canalización y, a continuación, haga clic en hello **aplicar** botón.</span><span class="sxs-lookup"><span data-stu-id="6af57-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="6af57-121">lista de ventanas de la actividad de Hello no se actualiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6af57-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="6af57-122">Haga clic en hello **actualizar** botón de barra de herramientas Hola Hola **Windows actividad** lista.</span><span class="sxs-lookup"><span data-stu-id="6af57-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="6af57-123">Si no tiene un tootest de aplicación de la factoría de datos de estos pasos con, Hola tutorial: [copiar los datos de almacenamiento de blobs tooSQL con factoría de datos de la base de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6af57-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="6af57-124">Entender la aplicación de supervisión y administración de hello</span><span class="sxs-lookup"><span data-stu-id="6af57-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="6af57-125">Hay tres pestañas de hello izquierda: **Resource Explorer**, **vistas de supervisión de**, y **alertas**.</span><span class="sxs-lookup"><span data-stu-id="6af57-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="6af57-126">primera pestaña de Hello (**Resource Explorer**) está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6af57-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="6af57-127">Explorador de recursos</span><span class="sxs-lookup"><span data-stu-id="6af57-127">Resource Explorer</span></span>
<span data-ttu-id="6af57-128">Se ve Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="6af57-128">You see hello following:</span></span>

* <span data-ttu-id="6af57-129">Hola Resource Explorer **vista de árbol** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="6af57-130">Hola **vista de diagrama** en parte superior de hello en el panel central de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="6af57-131">Hola **Windows actividad** lista final hello en el panel central de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="6af57-132">Hola **propiedades**, **Explorer de la ventana de actividad**, y **Script** fichas en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="6af57-133">En el Explorador de recursos, verá todos los recursos (canalizaciones, los conjuntos de datos, servicios vinculados) de la factoría de datos de hello en una vista de árbol.</span><span class="sxs-lookup"><span data-stu-id="6af57-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="6af57-134">Al seleccionar un objeto en el Explorador de recursos:</span><span class="sxs-lookup"><span data-stu-id="6af57-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="6af57-135">Hola asociado factoría de datos de entidad se resalta en hello vista de diagrama.</span><span class="sxs-lookup"><span data-stu-id="6af57-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="6af57-136">[Asociados de ventanas de la actividad](data-factory-scheduling-and-execution.md) se resaltan en la lista de ventanas de la actividad de hello en parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="6af57-137">propiedades Hola del objeto seleccionado Hola se muestran en la ventana de propiedades de hello en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="6af57-138">se muestra la definición JSON del objeto seleccionado Hola Hola, si procede.</span><span class="sxs-lookup"><span data-stu-id="6af57-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="6af57-139">Por ejemplo: un servicio vinculado, un conjunto de datos o una canalización.</span><span class="sxs-lookup"><span data-stu-id="6af57-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Explorador de recursos](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="6af57-141">Vea hello [ejecución y programación](data-factory-scheduling-and-execution.md) artículo para obtener información conceptual detallada sobre las ventanas de actividad.</span><span class="sxs-lookup"><span data-stu-id="6af57-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="6af57-142">Vista de diagrama</span><span class="sxs-lookup"><span data-stu-id="6af57-142">Diagram View</span></span>
<span data-ttu-id="6af57-143">Hola vista de diagrama de una factoría de datos proporciona un único panel de vidrio toomonitor y administrar una factoría de datos y sus activos.</span><span class="sxs-lookup"><span data-stu-id="6af57-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="6af57-144">Cuando se selecciona una entidad de factoría de datos (conjunto de datos y canalización) en la vista de diagrama de hello:</span><span class="sxs-lookup"><span data-stu-id="6af57-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="6af57-145">entidad de factoría de datos de Hello está seleccionado en la vista de árbol de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="6af57-146">Hola asociado actividad windows se resaltan en la lista de ventanas de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="6af57-147">propiedades de Hello del objeto seleccionado Hola se muestran en la ventana de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="6af57-148">Cuando se habilita la canalización de hello (no en un estado pausado), se muestra con una línea verde:</span><span class="sxs-lookup"><span data-stu-id="6af57-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Canalización en ejecución](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="6af57-150">Puede pausar, reanudar o finalizar una canalización seleccionándolo en la vista de diagrama de Hola y con los botones de hello en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Pausar y reanudar en la barra de comandos de Hola](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="6af57-152">Hay tres botones de barra de comandos de la canalización de Hola Hola vista de diagrama.</span><span class="sxs-lookup"><span data-stu-id="6af57-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="6af57-153">Puede usar la canalización de hello segundo botón toopause Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="6af57-154">Pausar Hola actividades en ejecución, no termina y les permite continuar toocompletion.</span><span class="sxs-lookup"><span data-stu-id="6af57-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="6af57-155">tercer botón de Hola detiene la canalización de Hola y finaliza su ejecución de actividades existentes.</span><span class="sxs-lookup"><span data-stu-id="6af57-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="6af57-156">botón primera Hola reanuda la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="6af57-157">Cuando la canalización está en pausa, se cambia el color de Hola de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="6af57-158">Por ejemplo, una canalización en pausa es similar en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="6af57-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Canalización en pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="6af57-160">Puede seleccionar varias canalizaciones de dos o más mediante el uso de la tecla Ctrl de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="6af57-161">Puede usar botones de barra de comandos hello toopause/reanudar varias canalizaciones a la vez.</span><span class="sxs-lookup"><span data-stu-id="6af57-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="6af57-162">También puede hacer clic una canalización y seleccione las opciones toosuspend, reanudar o finalizar una canalización.</span><span class="sxs-lookup"><span data-stu-id="6af57-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Menú contextual de la canalización](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="6af57-164">Haga clic en hello **canalización abierto** opción toosee todas las actividades de hello en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![Menú Abrir canalización](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="6af57-166">En la vista de la canalización de hello abierto, verá todas las actividades de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="6af57-167">En este ejemplo, solamente hay una actividad: la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="6af57-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Canalización abierta](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="6af57-169">toogo realizar copias toohello vista anterior, haga clic en nombre de generador de datos de hello en el menú de la ruta de navegación de hello en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="6af57-170">En la vista de la canalización de hello, cuando se selecciona un conjunto de datos de salida o al mover el mouse sobre el conjunto de datos de salida de hello, vea ventana emergente de actividad Windows hello para ese conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="6af57-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Ventana emergente Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="6af57-172">Puede hacer clic en los detalles de toosee de ventana de una actividad para él en hello **propiedades** ventana en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Propiedades de la ventana de actividad](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="6af57-174">En el panel derecho de hello, cambie toohello **Explorer de la ventana de actividad** ficha toosee más detalles.</span><span class="sxs-lookup"><span data-stu-id="6af57-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="6af57-176">Consulte también **resuelve las variables** para cada intento de ejecución de una actividad en hello **intentos** sección.</span><span class="sxs-lookup"><span data-stu-id="6af57-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Variables resueltas](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="6af57-178">Cambiar toohello **Script** ficha Definición de script toosee Hola JSON para el objeto seleccionado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Pestaña de script](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="6af57-180">Puede ver las ventanas de actividad en tres lugares:</span><span class="sxs-lookup"><span data-stu-id="6af57-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="6af57-181">Hola ventanas emergentes Hola vista de diagrama (panel central) de la actividad.</span><span class="sxs-lookup"><span data-stu-id="6af57-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="6af57-182">Hola Explorador de la ventana de actividad en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="6af57-183">lista de ventanas de la actividad de Hello en el panel inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="6af57-184">En la ventana emergente de ventanas de la actividad de Hola y el Explorador de ventana de actividad, puede desplazarse a toohello la semana anterior y Hola semanas siguientes mediante el uso de Hola flechas izquierda y derecha.</span><span class="sxs-lookup"><span data-stu-id="6af57-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Flechas izquierda/derecha de Activity Window Explorer (Explorador de ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="6af57-186">En parte inferior de Hola de hello vista de diagrama, verá estos botones: Acercar, alejar, Zoom tooFit, Zoom 100%, diseño de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="6af57-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="6af57-187">Hola **diseño de bloqueo** botón impide que se muevan accidentalmente tablas y canalizaciones en hello vista de diagrama.</span><span class="sxs-lookup"><span data-stu-id="6af57-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="6af57-188">Está activado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6af57-188">It's on by default.</span></span> <span data-ttu-id="6af57-189">Puede desactivarla y mover las entidades en el diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="6af57-190">Cuando se lo desactiva, puede utilizar las canalizaciones y tablas de hello último botón tooautomatically posición.</span><span class="sxs-lookup"><span data-stu-id="6af57-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="6af57-191">También puede acercar o alejar mediante el uso de la rueda del mouse de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Comandos de ampliación de la vista de diagrama](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="6af57-193">Lista Activity Windows (Ventanas de actividad)</span><span class="sxs-lookup"><span data-stu-id="6af57-193">Activity Windows list</span></span>
<span data-ttu-id="6af57-194">Hola actividad Windows lista Hola parte inferior del panel central de hello muestra todas las ventanas de actividad de conjunto de datos de Hola que seleccionó en el Explorador de recursos de Hola o hello vista de diagrama.</span><span class="sxs-lookup"><span data-stu-id="6af57-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="6af57-195">De forma predeterminada, lista de hello está en orden descendente, lo que significa que aparece la ventana de actividad más reciente de hello en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="6af57-197">Esta lista no se actualiza automáticamente, por lo que el botón de actualización de uso hello en toomanually de barra de herramientas de hello actualizarlo.</span><span class="sxs-lookup"><span data-stu-id="6af57-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="6af57-198">Ventanas de la actividad pueden estar en uno de hello siguientes estados:</span><span class="sxs-lookup"><span data-stu-id="6af57-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="6af57-199">Estado</span><span class="sxs-lookup"><span data-stu-id="6af57-199">Status</span></span></th><th align="left"><span data-ttu-id="6af57-200">Subestado</span><span class="sxs-lookup"><span data-stu-id="6af57-200">Substatus</span></span></th><th align="left"><span data-ttu-id="6af57-201">Description</span><span class="sxs-lookup"><span data-stu-id="6af57-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="6af57-202">En espera</span><span class="sxs-lookup"><span data-stu-id="6af57-202">Waiting</span></span></td><td><span data-ttu-id="6af57-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="6af57-203">ScheduleTime</span></span></td><td><span data-ttu-id="6af57-204">no se ha llegado el momento de Hola para toorun de ventana de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="6af57-205">DatasetDependencies</span></span></td><td><span data-ttu-id="6af57-206">dependencias de nivel superior de Hello no están preparadas.</span><span class="sxs-lookup"><span data-stu-id="6af57-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="6af57-207">ComputeResources</span></span></td><td><span data-ttu-id="6af57-208">recursos de proceso de Hello no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="6af57-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="6af57-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="6af57-210">Todas las instancias de actividad de hello están ocupadas ejecutando otras ventanas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="6af57-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="6af57-211">ActivityResume</span></span></td><td><span data-ttu-id="6af57-212">actividad Hello está en pausa y no puede ejecutar windows de la actividad de hello hasta que se reanude.</span><span class="sxs-lookup"><span data-stu-id="6af57-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-213">Retry</span><span class="sxs-lookup"><span data-stu-id="6af57-213">Retry</span></span></td><td><span data-ttu-id="6af57-214">se vuelve a intentar la ejecución de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-215">Validación</span><span class="sxs-lookup"><span data-stu-id="6af57-215">Validation</span></span></td><td><span data-ttu-id="6af57-216">Aún no ha iniciado la validación.</span><span class="sxs-lookup"><span data-stu-id="6af57-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="6af57-217">ValidationRetry</span></span></td><td><span data-ttu-id="6af57-218">La validación es toobe espera vuelve a intentar.</span><span class="sxs-lookup"><span data-stu-id="6af57-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="6af57-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="6af57-219">InProgress</span></span></td><td><span data-ttu-id="6af57-220">Validating</span><span class="sxs-lookup"><span data-stu-id="6af57-220">Validating</span></span></td><td><span data-ttu-id="6af57-221">Validación en curso.</span><span class="sxs-lookup"><span data-stu-id="6af57-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="6af57-222">ventana de actividad de saludo se está procesando.</span><span class="sxs-lookup"><span data-stu-id="6af57-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="6af57-223">Con error</span><span class="sxs-lookup"><span data-stu-id="6af57-223">Failed</span></span></td><td><span data-ttu-id="6af57-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="6af57-224">TimedOut</span></span></td><td><span data-ttu-id="6af57-225">ejecución de la actividad de Hello ha tardado más de las permitidas por actividad hello.</span><span class="sxs-lookup"><span data-stu-id="6af57-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="6af57-226">Canceled</span></span></td><td><span data-ttu-id="6af57-227">ventana de actividad de Hello fue cancelada por acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="6af57-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-228">Validación</span><span class="sxs-lookup"><span data-stu-id="6af57-228">Validation</span></span></td><td><span data-ttu-id="6af57-229">Error de validación.</span><span class="sxs-lookup"><span data-stu-id="6af57-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="6af57-230">ventana de actividad de Hello no pudo toobe generado o validar.</span><span class="sxs-lookup"><span data-stu-id="6af57-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="6af57-231">Ready</span><span class="sxs-lookup"><span data-stu-id="6af57-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="6af57-232">ventana de actividad de Hello está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="6af57-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-233">Skipped</span><span class="sxs-lookup"><span data-stu-id="6af57-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="6af57-234">ventana de actividad de Hello no se procesa.</span><span class="sxs-lookup"><span data-stu-id="6af57-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6af57-235">None</span><span class="sxs-lookup"><span data-stu-id="6af57-235">None</span></span></td><td>-</td><td><span data-ttu-id="6af57-236">Una ventana de actividad utiliza tooexist con un estado diferente, pero se ha restablecido.</span><span class="sxs-lookup"><span data-stu-id="6af57-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="6af57-237">Al hacer clic en una ventana de actividad en la lista de hello, puede ver detalles sobre él en hello **el Explorador de Windows de actividad** o hello **propiedades** ventana en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="6af57-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="6af57-239">Actualizar las ventanas de actividad</span><span class="sxs-lookup"><span data-stu-id="6af57-239">Refresh activity windows</span></span>
<span data-ttu-id="6af57-240">detalles de Hello no se actualizan automáticamente, así que usa Hola actualización botón (Hola segundo) en la lista de windows de toomanually actualización Hola actividad de la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="6af57-241">Ventana Propiedades</span><span class="sxs-lookup"><span data-stu-id="6af57-241">Properties window</span></span>
<span data-ttu-id="6af57-242">ventana de propiedades de Hello es en panel de hello más a la derecha de la aplicación de supervisión y administración de hello.</span><span class="sxs-lookup"><span data-stu-id="6af57-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Ventana Propiedades](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="6af57-244">Muestra propiedades de elemento de Hola que seleccionó en hello Explorador de recursos (vista de árbol), vista de diagrama o la lista de ventanas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="6af57-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="6af57-245">Activity Window Explorer</span><span class="sxs-lookup"><span data-stu-id="6af57-245">Activity Window Explorer</span></span>
<span data-ttu-id="6af57-246">Hola **actividad ventana Explorer** ventana está en el panel de hello más a la derecha de la aplicación de supervisión y administración de hello.</span><span class="sxs-lookup"><span data-stu-id="6af57-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="6af57-247">Muestra detalles acerca de la ventana de actividad de Hola que seleccionó en la ventana emergente de ventanas de la actividad de Hola o una lista de ventanas de la actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="6af57-249">Puede cambiar la ventana de actividad de tooanother haciendo clic en él en la vista de calendario de hello en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="6af57-250">También puede usar los botones de flecha derecha o flecha izquierda hello en ventanas de la actividad de hello toosee superior de hello semana anterior u Hola semanas siguientes.</span><span class="sxs-lookup"><span data-stu-id="6af57-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="6af57-251">Puede usar botones de barra de herramientas de hello en ventana de actividad de hello toorerun del panel de la parte inferior Hola o actualizar los detalles de hello en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="6af57-252">Script</span><span class="sxs-lookup"><span data-stu-id="6af57-252">Script</span></span>
<span data-ttu-id="6af57-253">Puede usar hello **Script** Hola de tooview ficha Definición JSON de hello seleccionado entidad de la factoría de datos (el servicio vinculado, el conjunto de datos o la canalización).</span><span class="sxs-lookup"><span data-stu-id="6af57-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Pestaña de script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="6af57-255">Vistas de uso del sistema</span><span class="sxs-lookup"><span data-stu-id="6af57-255">Use system views</span></span>
<span data-ttu-id="6af57-256">Supervisión y administración de la aplicación Hello incluye vistas del sistema pregenerado (**ventanas de la actividad reciente**, **no se pudo ventanas de la actividad**, **ventanas de la actividad en curso**) que Permitir ventanas de la actividad reciente/error/en curso de tooview de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="6af57-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="6af57-257">Cambiar toohello **vistas de supervisión de** ficha izquierda Hola haciendo clic en él.</span><span class="sxs-lookup"><span data-stu-id="6af57-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![Pestaña Vistas de supervisión](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="6af57-259">Actualmente, hay tres vistas del sistema compatibles.</span><span class="sxs-lookup"><span data-stu-id="6af57-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="6af57-260">Seleccione una opción toosee ventanas de la actividad reciente, windows de una actividad con errores o ventanas de la actividad en curso en lista de ventanas de la actividad de hello (en hello parte inferior del panel central de hello).</span><span class="sxs-lookup"><span data-stu-id="6af57-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="6af57-261">Cuando selecciona hello **ventanas de la actividad reciente** opción, verá todas las ventanas de la actividad reciente en orden descendente de hello **último intento tiempo**.</span><span class="sxs-lookup"><span data-stu-id="6af57-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="6af57-262">Puede usar hello **no se pudo ventanas de la actividad** ver toosee error de todas las ventanas de la actividad en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="6af57-263">Seleccione una ventana de actividad con errores en hello lista toosee obtener información detallada sobre él en hello **propiedades** ventana o hello **Explorer de la ventana de actividad**.</span><span class="sxs-lookup"><span data-stu-id="6af57-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="6af57-264">También puede descargar los registros de una ventana de actividad con error.</span><span class="sxs-lookup"><span data-stu-id="6af57-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="6af57-265">Ordenado y filtrado de las ventanas de actividad</span><span class="sxs-lookup"><span data-stu-id="6af57-265">Sort and filter activity windows</span></span>
<span data-ttu-id="6af57-266">Hola de cambio **hora de inicio** y **hora de finalización** configuración de ventanas de la actividad de toofilter la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="6af57-267">Después de cambiar la hora de inicio de Hola y hora de finalización, haga clic en hello botón siguiente toohello final tiempo toorefresh Hola ventanas de la actividad.</span><span class="sxs-lookup"><span data-stu-id="6af57-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Horas de inicio y finalización](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="6af57-269">Actualmente, todas las horas están en formato UTC en la aplicación de supervisión y administración de hello.</span><span class="sxs-lookup"><span data-stu-id="6af57-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="6af57-270">Hola **lista de ventanas de la actividad**, haga clic en nombre de Hola de una columna (por ejemplo: estado).</span><span class="sxs-lookup"><span data-stu-id="6af57-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Menú de columna de la lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="6af57-272">Puede hacer siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6af57-272">You can do hello following:</span></span>

* <span data-ttu-id="6af57-273">Ordenar en orden ascendente.</span><span class="sxs-lookup"><span data-stu-id="6af57-273">Sort in ascending order.</span></span>
* <span data-ttu-id="6af57-274">Ordenar en orden descendente.</span><span class="sxs-lookup"><span data-stu-id="6af57-274">Sort in descending order.</span></span>
* <span data-ttu-id="6af57-275">Filtrar por uno o más valores (Ready [Listo], Waiting [En espera], etc.).</span><span class="sxs-lookup"><span data-stu-id="6af57-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="6af57-276">Cuando se especifica un filtro en una columna, verá el botón de filtro de hello habilitado para esa columna, lo que indica que los valores de hello en columna de hello son valores filtrados.</span><span class="sxs-lookup"><span data-stu-id="6af57-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Filtrar una columna de la lista de ventanas de la actividad de Hola](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="6af57-278">Puede usar Hola mismos filtros de tooclear de la ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="6af57-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="6af57-279">tooclear todos los filtros de la lista de ventanas de la actividad de hello, haga clic en el botón Borrar filtro de hello en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Borrar todos los filtros de la lista de ventanas de la actividad de Hola](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="6af57-281">Acciones por lotes</span><span class="sxs-lookup"><span data-stu-id="6af57-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="6af57-282">Volver a ejecutar las ventanas de actividad seleccionadas</span><span class="sxs-lookup"><span data-stu-id="6af57-282">Rerun selected activity windows</span></span>
<span data-ttu-id="6af57-283">Seleccione una ventana de actividad, haga clic en hello flecha abajo en el primer botón de barra de comandos hello y seleccione **vuelva a ejecutar** / **vuelva a ejecutar con en dirección ascendente de canalización**.</span><span class="sxs-lookup"><span data-stu-id="6af57-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="6af57-284">Cuando selecciona hello **vuelva a ejecutar con en dirección ascendente de canalización** opción, vuelve a ejecutar todas las ventanas de nivel superior de actividad.</span><span class="sxs-lookup"><span data-stu-id="6af57-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="6af57-285">![Volver a ejecutar una ventana de actividad](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="6af57-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="6af57-286">También puede seleccionar varias ventanas de la actividad en la lista de Hola y volver a ejecutarlos en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="6af57-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="6af57-287">Conviene ventanas de la actividad toofilter acuerdos con el estado de hello (por ejemplo: **error**)--y, a continuación, vuelva a ejecutar windows de la actividad de hello no se pudo después de corregir el problema de Hola que provoca Hola actividad windows toofail.</span><span class="sxs-lookup"><span data-stu-id="6af57-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="6af57-288">Vea Hola pasos de la sección para obtener más información acerca del filtrado de windows de la actividad en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="6af57-289">Pausar y reanudar varias canalizaciones</span><span class="sxs-lookup"><span data-stu-id="6af57-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="6af57-290">Puede realizar una selección múltiple canalizaciones de dos o más mediante el uso de la tecla Ctrl de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="6af57-291">Puede usar los botones de barra de comandos de hello (que se resaltan en el rectángulo rojo Hola Hola después de la imagen) toopause/reanudar ellos.</span><span class="sxs-lookup"><span data-stu-id="6af57-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Pausar y reanudar en la barra de comandos de Hola](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="6af57-293">Creación de alertas</span><span class="sxs-lookup"><span data-stu-id="6af57-293">Create alerts</span></span>
<span data-ttu-id="6af57-294">Hola **alertas** página le permite crear una alerta y ver, editar o eliminar las alertas existentes.</span><span class="sxs-lookup"><span data-stu-id="6af57-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="6af57-295">También puede habilitar o deshabilitar una alerta.</span><span class="sxs-lookup"><span data-stu-id="6af57-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="6af57-296">toosee Hola página de alertas, haga clic en hello **alertas** ficha.</span><span class="sxs-lookup"><span data-stu-id="6af57-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Pestaña Alertas](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="6af57-298">toocreate una alerta</span><span class="sxs-lookup"><span data-stu-id="6af57-298">toocreate an alert</span></span>
1. <span data-ttu-id="6af57-299">Haga clic en **Agregar alerta** tooadd una alerta.</span><span class="sxs-lookup"><span data-stu-id="6af57-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="6af57-300">Vea hello **detalles** página.</span><span class="sxs-lookup"><span data-stu-id="6af57-300">You see hello **Details** page.</span></span>

    ![Crear alertas: página de detalles](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="6af57-302">Especificar hello **nombre** y **descripción** alerta hello y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6af57-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="6af57-303">Debería ver Hola **filtros** página.</span><span class="sxs-lookup"><span data-stu-id="6af57-303">You should see hello **Filters** page.</span></span>

    ![Crear alertas: página de filtros](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="6af57-305">Seleccione hello **eventos**, **estado**, y **subestado** (opcional) que desea toocreate un servicio de factoría de datos de alertas para y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="6af57-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="6af57-306">Debería ver Hola **destinatarios** página.</span><span class="sxs-lookup"><span data-stu-id="6af57-306">You should see hello **Recipients** page.</span></span>

    ![Crear alertas: página de destinatarios](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="6af57-308">Seleccione hello **los administradores de suscripciones de correo electrónico** opción o escriba una **correo electrónico de administrador adicional**y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="6af57-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="6af57-309">Debería ver la alerta de hello en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6af57-309">You should see hello alert in hello list.</span></span>

    ![Lista de alertas](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="6af57-311">En la lista de alertas de hello, utilice los botones de Hola que están asociados a Hola alerta tooedit/delete/deshabilitar/Habilitar una alerta.</span><span class="sxs-lookup"><span data-stu-id="6af57-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="6af57-312">Evento/estado/subestado</span><span class="sxs-lookup"><span data-stu-id="6af57-312">Event/status/substatus</span></span>
<span data-ttu-id="6af57-313">Hello tabla siguiente proporciona Hola lista de eventos disponibles y Estados (y sub-estados).</span><span class="sxs-lookup"><span data-stu-id="6af57-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="6af57-314">Nombre del evento</span><span class="sxs-lookup"><span data-stu-id="6af57-314">Event name</span></span> | <span data-ttu-id="6af57-315">Estado</span><span class="sxs-lookup"><span data-stu-id="6af57-315">Status</span></span> | <span data-ttu-id="6af57-316">Subestado</span><span class="sxs-lookup"><span data-stu-id="6af57-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6af57-317">Ejecución de actividad iniciada</span><span class="sxs-lookup"><span data-stu-id="6af57-317">Activity Run Started</span></span> |<span data-ttu-id="6af57-318">Started</span><span class="sxs-lookup"><span data-stu-id="6af57-318">Started</span></span> |<span data-ttu-id="6af57-319">Iniciando</span><span class="sxs-lookup"><span data-stu-id="6af57-319">Starting</span></span> |
| <span data-ttu-id="6af57-320">Ejecución de actividad finalizada</span><span class="sxs-lookup"><span data-stu-id="6af57-320">Activity Run Finished</span></span> |<span data-ttu-id="6af57-321">Correcto</span><span class="sxs-lookup"><span data-stu-id="6af57-321">Succeeded</span></span> |<span data-ttu-id="6af57-322">Correcto</span><span class="sxs-lookup"><span data-stu-id="6af57-322">Succeeded</span></span> |
| <span data-ttu-id="6af57-323">Ejecución de actividad finalizada</span><span class="sxs-lookup"><span data-stu-id="6af57-323">Activity Run Finished</span></span> |<span data-ttu-id="6af57-324">Con error</span><span class="sxs-lookup"><span data-stu-id="6af57-324">Failed</span></span> |<span data-ttu-id="6af57-325">Asignación de recursos errónea</span><span class="sxs-lookup"><span data-stu-id="6af57-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="6af57-326">Ejecución con errores</span><span class="sxs-lookup"><span data-stu-id="6af57-326">Failed Execution</span></span><br/><br/><span data-ttu-id="6af57-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="6af57-327">Timed Out</span></span><br/><br/><span data-ttu-id="6af57-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="6af57-328">Failed Validation</span></span><br/><br/><span data-ttu-id="6af57-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="6af57-329">Abandoned</span></span> |
| <span data-ttu-id="6af57-330">Creación de clúster de HDI a petición iniciada</span><span class="sxs-lookup"><span data-stu-id="6af57-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="6af57-331">Started</span><span class="sxs-lookup"><span data-stu-id="6af57-331">Started</span></span> |-|
| <span data-ttu-id="6af57-332">Creación correcta de clúster de HDI a petición</span><span class="sxs-lookup"><span data-stu-id="6af57-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="6af57-333">Correcto</span><span class="sxs-lookup"><span data-stu-id="6af57-333">Succeeded</span></span> |-|
| <span data-ttu-id="6af57-334">Clúster de HDI a petición eliminado</span><span class="sxs-lookup"><span data-stu-id="6af57-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="6af57-335">Correcto</span><span class="sxs-lookup"><span data-stu-id="6af57-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="6af57-336">tooedit, eliminar o deshabilitar una alerta</span><span class="sxs-lookup"><span data-stu-id="6af57-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="6af57-337">Usar hello después tooedit botones (resaltados en rojo), eliminar o deshabilitar una alerta.</span><span class="sxs-lookup"><span data-stu-id="6af57-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Botones de alertas](./media/data-factory-monitor-manage-app/AlertButtons.png)
