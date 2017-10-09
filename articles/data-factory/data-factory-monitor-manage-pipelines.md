---
title: aaaMonitor y administrar las canalizaciones mediante hello portal de Azure y PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola portal de Azure y Azure PowerShell toomonitor y administrar factorías de datos de Azure de Hola y las canalizaciones que haya creado."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="baf24-103">Supervisar y administrar las canalizaciones de factoría de datos de Azure mediante Hola portal de Azure y PowerShell</span><span class="sxs-lookup"><span data-stu-id="baf24-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="baf24-104">Uso de Azure Portal/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="baf24-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="baf24-105">Uso de la aplicación de supervisión y administración</span><span class="sxs-lookup"><span data-stu-id="baf24-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="baf24-106">aplicación de administración y supervisión de Hello proporciona una mejor compatibilidad para supervisar y administrar sus canalizaciones de datos y solucionar los problemas.</span><span class="sxs-lookup"><span data-stu-id="baf24-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="baf24-107">Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="baf24-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="baf24-108">Este artículo describe cómo administrar toomonitor y depurar las canalizaciones mediante el portal de Azure y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="baf24-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="baf24-109">Hello artículo también proporciona información acerca de cómo toocreate alertas y obtener notificaciones acerca de los errores.</span><span class="sxs-lookup"><span data-stu-id="baf24-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="baf24-110">Descripción de las canalizaciones y los estados de actividad</span><span class="sxs-lookup"><span data-stu-id="baf24-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="baf24-111">Mediante el uso de hello portal de Azure, hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="baf24-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="baf24-112">Ver una factoría de datos como un diagrama.</span><span class="sxs-lookup"><span data-stu-id="baf24-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="baf24-113">Ver las actividades en una canalización.</span><span class="sxs-lookup"><span data-stu-id="baf24-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="baf24-114">Ver conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="baf24-114">View input and output datasets.</span></span>

<span data-ttu-id="baf24-115">Esta sección también describe cómo un segmento del conjunto de datos realiza la transición de estado de un estado tooanother.</span><span class="sxs-lookup"><span data-stu-id="baf24-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="baf24-116">Navegue tooyour factoría de datos</span><span class="sxs-lookup"><span data-stu-id="baf24-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="baf24-117">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="baf24-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="baf24-118">Haga clic en **factorías de datos** en menú Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="baf24-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="baf24-119">Si no lo ve, haga clic en **más servicios >**y, a continuación, haga clic en **factorías de datos** en hello **INTELLIGENCE + análisis** categoría.</span><span class="sxs-lookup"><span data-stu-id="baf24-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Examinar todo -> Factorías de datos](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="baf24-121">En hello **factorías de datos** hoja, factoría de datos seleccione Hola que le interesa.</span><span class="sxs-lookup"><span data-stu-id="baf24-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Selección de la factoría de datos](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="baf24-123">Debería ver la página principal de Hola de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-123">You should see hello home page for hello data factory.</span></span>

   ![Hoja Factoría de datos](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="baf24-125">Vista de diagrama de la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="baf24-125">Diagram view of your data factory</span></span>
<span data-ttu-id="baf24-126">Hola **diagrama** vista de una factoría de datos proporciona un único panel de vidrio toomonitor y administrar la factoría de datos de Hola y de sus activos.</span><span class="sxs-lookup"><span data-stu-id="baf24-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="baf24-127">Hola toosee **diagrama** ver de la factoría de datos, haga clic en **diagrama** en la portada de Hola de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Vista de diagrama](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="baf24-129">Puede acercar, alejar, zoom toofit, zoom too100%, diseño de Hola de bloqueo del diagrama de Hola y automáticamente Posicione canalizaciones y los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="baf24-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="baf24-130">También puede ver información de linaje de datos de hello (es decir, mostrar los elementos que preceden y siguen en la cadena de los elementos seleccionados).</span><span class="sxs-lookup"><span data-stu-id="baf24-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="baf24-131">Actividades en una canalización</span><span class="sxs-lookup"><span data-stu-id="baf24-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="baf24-132">Haga clic en canalización hello y, a continuación, haga clic en **canalización abierto** toosee todas las actividades de Hola de canalización, junto con los conjuntos de datos de entrada y salida para las actividades de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="baf24-133">Esta característica es útil cuando la canalización incluye más de una actividad y desea toounderstand Hola operativa acerca del linaje de una sola canalización.</span><span class="sxs-lookup"><span data-stu-id="baf24-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![Menú Abrir canalización](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="baf24-135">En el siguiente ejemplo de Hola, verá una actividad de copia de canalización de hello con una entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="baf24-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Actividades en una canalización](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="baf24-137">Puede navegar toohello atrás portada Hola factoría de datos haciendo clic en hello **factoría de datos** vínculo en la ruta de navegación de hello en la esquina superior izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Navegue generador toodata atrás](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="baf24-139">Estado de cada actividad dentro de una canalización de hello de vista</span><span class="sxs-lookup"><span data-stu-id="baf24-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="baf24-140">Puede ver estado actual de Hola de una actividad por ver el estado de Hola de cualquiera de los conjuntos de datos de hello producidos por actividad hello.</span><span class="sxs-lookup"><span data-stu-id="baf24-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="baf24-141">Haga doble clic en hello **OutputBlobTable** en hello **diagrama**, puede ver todos los sectores de Hola que se producen en ejecuciones de actividad diferente dentro de una canalización.</span><span class="sxs-lookup"><span data-stu-id="baf24-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="baf24-142">Puede ver que actividad de copia de Hola se ejecutó correctamente para hello últimas ocho horas y genera sectores Hola Hola **listo** estado.</span><span class="sxs-lookup"><span data-stu-id="baf24-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Estado de canalización de Hola](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="baf24-144">segmentos de conjunto de datos de Hola de factoría de datos de hello pueden tener uno de hello siguientes estados:</span><span class="sxs-lookup"><span data-stu-id="baf24-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="baf24-145">Estado</span><span class="sxs-lookup"><span data-stu-id="baf24-145">State</span></span></th><th align="left"><span data-ttu-id="baf24-146">Subestado</span><span class="sxs-lookup"><span data-stu-id="baf24-146">Substate</span></span></th><th align="left"><span data-ttu-id="baf24-147">Description</span><span class="sxs-lookup"><span data-stu-id="baf24-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="baf24-148">En espera</span><span class="sxs-lookup"><span data-stu-id="baf24-148">Waiting</span></span></td><td><span data-ttu-id="baf24-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="baf24-149">ScheduleTime</span></span></td><td><span data-ttu-id="baf24-150">no se ha llegado el momento de Hola para hello toorun de segmento.</span><span class="sxs-lookup"><span data-stu-id="baf24-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="baf24-151">DatasetDependencies</span></span></td><td><span data-ttu-id="baf24-152">dependencias de nivel superior de Hello no están preparadas.</span><span class="sxs-lookup"><span data-stu-id="baf24-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="baf24-153">ComputeResources</span></span></td><td><span data-ttu-id="baf24-154">recursos de proceso de Hello no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="baf24-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="baf24-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="baf24-156">Todas las instancias de actividad de hello están ocupadas ejecutando otros segmentos.</span><span class="sxs-lookup"><span data-stu-id="baf24-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="baf24-157">ActivityResume</span></span></td><td><span data-ttu-id="baf24-158">actividad Hello está en pausa y no puede ejecutar sectores Hola hasta que se reanude la actividad Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-159">Retry</span><span class="sxs-lookup"><span data-stu-id="baf24-159">Retry</span></span></td><td><span data-ttu-id="baf24-160">Se está volviendo a intentar la ejecución de la actividad.</span><span class="sxs-lookup"><span data-stu-id="baf24-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-161">Validación</span><span class="sxs-lookup"><span data-stu-id="baf24-161">Validation</span></span></td><td><span data-ttu-id="baf24-162">Aún no ha iniciado la validación.</span><span class="sxs-lookup"><span data-stu-id="baf24-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="baf24-163">ValidationRetry</span></span></td><td><span data-ttu-id="baf24-164">La validación es toobe espera vuelve a intentar.</span><span class="sxs-lookup"><span data-stu-id="baf24-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="baf24-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="baf24-165">InProgress</span></span></td><td><span data-ttu-id="baf24-166">Validating</span><span class="sxs-lookup"><span data-stu-id="baf24-166">Validating</span></span></td><td><span data-ttu-id="baf24-167">Validación en curso.</span><span class="sxs-lookup"><span data-stu-id="baf24-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="baf24-168">segmento de saludo se está procesando.</span><span class="sxs-lookup"><span data-stu-id="baf24-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="baf24-169">Con error</span><span class="sxs-lookup"><span data-stu-id="baf24-169">Failed</span></span></td><td><span data-ttu-id="baf24-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="baf24-170">TimedOut</span></span></td><td><span data-ttu-id="baf24-171">ejecución de la actividad de Hello ha tardado más de las permitidas por actividad hello.</span><span class="sxs-lookup"><span data-stu-id="baf24-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="baf24-172">Canceled</span></span></td><td><span data-ttu-id="baf24-173">segmento de Hello fue cancelada por acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="baf24-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-174">Validación</span><span class="sxs-lookup"><span data-stu-id="baf24-174">Validation</span></span></td><td><span data-ttu-id="baf24-175">Error de validación.</span><span class="sxs-lookup"><span data-stu-id="baf24-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="baf24-176">segmento de Hello no pudo toobe generado o validar.</span><span class="sxs-lookup"><span data-stu-id="baf24-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="baf24-177">Ready</span><span class="sxs-lookup"><span data-stu-id="baf24-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="baf24-178">segmento de Hello está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="baf24-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-179">Skipped</span><span class="sxs-lookup"><span data-stu-id="baf24-179">Skipped</span></span></td><td><span data-ttu-id="baf24-180">None</span><span class="sxs-lookup"><span data-stu-id="baf24-180">None</span></span></td><td><span data-ttu-id="baf24-181">segmento de Hello no está procesando.</span><span class="sxs-lookup"><span data-stu-id="baf24-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="baf24-182">None</span><span class="sxs-lookup"><span data-stu-id="baf24-182">None</span></span></td><td>-</td><td><span data-ttu-id="baf24-183">Un segmento utiliza tooexist con un estado diferente, pero se ha restablecido.</span><span class="sxs-lookup"><span data-stu-id="baf24-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="baf24-184">Puede ver detalles de hello sobre un segmento, haga clic en una entrada de segmento en hello **sectores actualizado recientemente** hoja.</span><span class="sxs-lookup"><span data-stu-id="baf24-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Detalles de segmento](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="baf24-186">Si el segmento de Hola se ha ejecutado varias veces, verá varias filas en hello **se ejecuta la actividad** lista.</span><span class="sxs-lookup"><span data-stu-id="baf24-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="baf24-187">Puede ver detalles sobre la actividad ejecutar haciendo clic en la entrada de hello ejecutar Hola **se ejecuta la actividad** lista.</span><span class="sxs-lookup"><span data-stu-id="baf24-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="baf24-188">lista de Hello muestra todos los archivos de registro de hello, junto con un mensaje de error si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="baf24-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="baf24-189">Esta característica es útiles registros de tooview y de depuración sin tener tooleave su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="baf24-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![Detalles de ejecución de actividad](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="baf24-191">Si no está segmento Hola Hola **listo** estado, puede ver segmentos ascendentes de Hola que no están preparados y están bloqueando el intervalo actual de Hola de ejecutarse en hello **segmentos ascendentes que no están listos** lista.</span><span class="sxs-lookup"><span data-stu-id="baf24-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="baf24-192">Esta característica es útil cuando el segmento está en **espera** estado y desea que está esperando dependencias ascendentes de toounderstand Hola que Hola segmento.</span><span class="sxs-lookup"><span data-stu-id="baf24-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Segmentos ascendentes que no están listos](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="baf24-194">Diagrama de estado del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="baf24-194">Dataset state diagram</span></span>
<span data-ttu-id="baf24-195">Después de implementar una factoría de datos y las canalizaciones de hello tienen un período activo válido, el conjunto de datos de hello segmentos de transición de un estado tooanother.</span><span class="sxs-lookup"><span data-stu-id="baf24-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="baf24-196">Actualmente, el estado del sector de hello sigue Hola después de diagrama de estado:</span><span class="sxs-lookup"><span data-stu-id="baf24-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Diagrama de estado](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="baf24-198">flujo de transición de estado del conjunto de datos en la factoría de datos Hello es siguiente de hello: espera -> en curso o en curso (Validating) -> Listo/fallido.</span><span class="sxs-lookup"><span data-stu-id="baf24-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="baf24-199">segmento de Hola se inicia en un **espera** estado, esperando toobe las condiciones previas cumplido antes de su ejecución.</span><span class="sxs-lookup"><span data-stu-id="baf24-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="baf24-200">A continuación, actividad de hello empieza a ejecutarse y segmento Hola entra en un **en curso** estado.</span><span class="sxs-lookup"><span data-stu-id="baf24-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="baf24-201">ejecución de la actividad de Hello podría succeed o fail.</span><span class="sxs-lookup"><span data-stu-id="baf24-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="baf24-202">segmento de Hello está marcada como **listo** o **error**, según el resultado de hello de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="baf24-203">Puede restablecer Hola segmento toogo de hello **listo** o **error** estado toohello **espera** estado.</span><span class="sxs-lookup"><span data-stu-id="baf24-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="baf24-204">También puede marcar el estado del segmento de hello**omitir**, lo que evita la actividad de hello de ejecución y no procesa el segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="baf24-205">Pausa y reanudación de canalizaciones</span><span class="sxs-lookup"><span data-stu-id="baf24-205">Pause and resume pipelines</span></span>
<span data-ttu-id="baf24-206">Puede administrar las canalizaciones usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="baf24-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="baf24-207">Por ejemplo, puede pausar y reanudar canalizaciones ejecutando cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="baf24-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="baf24-208">vista de diagrama de Hello no admite pausar y reanudar las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="baf24-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="baf24-209">Si desea que toouse una interfaz de usuario, utilice Hola de supervisión y administración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="baf24-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="baf24-210">Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="baf24-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="baf24-211">Puede pausar/suspender canalizaciones mediante el uso de hello **AzureRmDataFactoryPipeline Suspend** cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="baf24-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="baf24-212">Este cmdlet es útil cuando no desee que toorun sus canalizaciones hasta que se solucione un problema.</span><span class="sxs-lookup"><span data-stu-id="baf24-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="baf24-213">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="baf24-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="baf24-214">Una vez resuelto el problema de Hola con canalización de hello, puede reanudar canalización Hola suspendido ejecutando el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="baf24-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="baf24-215">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="baf24-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="baf24-216">Depuración de canalizaciones</span><span class="sxs-lookup"><span data-stu-id="baf24-216">Debug pipelines</span></span>
<span data-ttu-id="baf24-217">Factoría de datos de Azure proporciona amplias funciones de toodebug y solucionar problemas de canalizaciones mediante Hola portal de Azure y Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="baf24-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="baf24-218">[! Tenga en cuenta} es mucho más fácil tootroubleshot errores con Hola supervisión & aplicación de administración.</span><span class="sxs-lookup"><span data-stu-id="baf24-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="baf24-219">Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="baf24-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="baf24-220">Búsqueda de errores en una canalización</span><span class="sxs-lookup"><span data-stu-id="baf24-220">Find errors in a pipeline</span></span>
<span data-ttu-id="baf24-221">Si se produce un error en la ejecución de la actividad de hello en una canalización, conjunto de datos de hello generado por la canalización de hello es en un estado de error debido a un error de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="baf24-222">Puede depurar y solucionar los errores en Data Factory de Azure mediante el uso de hello siguiendo métodos.</span><span class="sxs-lookup"><span data-stu-id="baf24-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="baf24-223">Usar hello toodebug portal Azure un error</span><span class="sxs-lookup"><span data-stu-id="baf24-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="baf24-224">En hello **tabla** hoja, haga clic en el sector de problema de Hola que tiene hello **estado** establecido demasiado**error**.</span><span class="sxs-lookup"><span data-stu-id="baf24-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Hoja Tabla con segmentos con problemas](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="baf24-226">En hello **el segmento de datos** hoja, haga clic en la actividad de hello que no se pudo ejecutar.</span><span class="sxs-lookup"><span data-stu-id="baf24-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Segmento de datos con un error](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="baf24-228">En hello **detalles de ejecución de la actividad** hoja, puede descargar archivos Hola que están asociados con el procesamiento de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="baf24-229">Haga clic en **descargar** estado/stderr toodownload Hola error archivo de registro que contiene detalles sobre el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Hoja Detalles de ejecución de actividad con errores](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="baf24-231">Usar PowerShell toodebug un error</span><span class="sxs-lookup"><span data-stu-id="baf24-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="baf24-232">Inicie **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="baf24-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="baf24-233">Ejecute hello **Get AzureRmDataFactorySlice** comandos toosee sectores de Hola y sus Estados.</span><span class="sxs-lookup"><span data-stu-id="baf24-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="baf24-234">Debería ver un segmento con el estado de Hola de **error**.</span><span class="sxs-lookup"><span data-stu-id="baf24-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="baf24-235">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="baf24-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="baf24-236">Reemplace **StartDateTime** por la hora de inicio de la canalización.</span><span class="sxs-lookup"><span data-stu-id="baf24-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="baf24-237">Ahora, ejecute hello **AzureRmDataFactoryRun Get** ejecutaron cmdlet tooget detalles acerca de la actividad de hello para el segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="baf24-238">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="baf24-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="baf24-239">valor de Hola de StartDateTime es hora de inicio de Hola de segmento de error o problema de Hola que anotó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="baf24-240">Hola de fecha y hora debe ir entre comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="baf24-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="baf24-241">Debería ver resultados con detalles sobre los errores Hola similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="baf24-241">You should see output with details about hello error that is similar toohello following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="baf24-242">Puede ejecutar hello **guardar AzureRmDataFactoryLog** cmdlet con el valor de identificador que se produzcan de salida de hello y descargar archivos de registro de hello mediante Hola Hola **- DownloadLogsoption** Hola cmdlet.</span><span class="sxs-lookup"><span data-stu-id="baf24-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="baf24-243">Repetición de la ejecución de errores en una canalización</span><span class="sxs-lookup"><span data-stu-id="baf24-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="baf24-244">Es más fácil de errores de tootroubleshoot y vuelva a ejecutar sectores errores mediante el uso de Hola supervisión y administración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="baf24-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="baf24-245">Para obtener más información sobre el uso de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos mediante la aplicación de supervisión y administración de hello](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="baf24-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="baf24-246">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="baf24-246">Use hello Azure portal</span></span>
<span data-ttu-id="baf24-247">Después de solucionar problemas y depurar los errores en una canalización, puede volver a ejecutar errores navegar por segmento de error toohello y haciendo clic en hello **ejecutar** botón de barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Repetición de ejecución de un segmento con errores](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="baf24-249">En caso de segmento de hello no pudo validar debido a un error de directiva (por ejemplo, si datos no están disponibles), puede corregir el error de Hola y validar de nuevo haciendo clic en hello **validar** botón de barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Corrección de errores y validación](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="baf24-251">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="baf24-251">Use Azure PowerShell</span></span>
<span data-ttu-id="baf24-252">Puede volver a ejecutar errores mediante el uso de hello **AzureRmDataFactorySliceStatus conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="baf24-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="baf24-253">Vea hello [AzureRmDataFactorySliceStatus conjunto](https://msdn.microsoft.com/library/mt603522.aspx) tema para la sintaxis y otros detalles acerca del cmdlet Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="baf24-254">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="baf24-254">**Example:**</span></span>

<span data-ttu-id="baf24-255">Hello en el ejemplo siguiente se establece estado Hola de todos los sectores de hello tabla 'DAWikiAggregatedData' too'Waiting' en el generador de datos de Azure de hello 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="baf24-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="baf24-256">Hola 'tipo ' de actualización se establece too'UpstreamInPipeline ', lo que significa que los Estados de cada sector para la tabla de Hola y todas las tablas (ascendente) dependiente de Hola se establecen too'Waiting'.</span><span class="sxs-lookup"><span data-stu-id="baf24-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="baf24-257">Hola otro valor posible para este parámetro es "Individual".</span><span class="sxs-lookup"><span data-stu-id="baf24-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="baf24-258">Creación de alertas</span><span class="sxs-lookup"><span data-stu-id="baf24-258">Create alerts</span></span>
<span data-ttu-id="baf24-259">Azure registra eventos del usuario cuando se crea, actualiza o elimina un recurso de Azure (por ejemplo, una factoría de datos).</span><span class="sxs-lookup"><span data-stu-id="baf24-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="baf24-260">Puede crear alertas en estos eventos.</span><span class="sxs-lookup"><span data-stu-id="baf24-260">You can create alerts on these events.</span></span> <span data-ttu-id="baf24-261">Puede utilizar toocapture de factoría de datos diferentes métricas y crear alertas para las métricas.</span><span class="sxs-lookup"><span data-stu-id="baf24-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="baf24-262">Se recomienda que use los eventos con fines de supervisión en tiempo real y las métricas con fines históricos.</span><span class="sxs-lookup"><span data-stu-id="baf24-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="baf24-263">Alertas en eventos</span><span class="sxs-lookup"><span data-stu-id="baf24-263">Alerts on events</span></span>
<span data-ttu-id="baf24-264">Los eventos de Azure proporcionan información útil sobre lo que sucede en los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="baf24-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="baf24-265">Al usar Azure Data Factory, se generan eventos cuando:</span><span class="sxs-lookup"><span data-stu-id="baf24-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="baf24-266">Se crea, actualiza o elimina una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="baf24-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="baf24-267">Se inicia o finaliza el procesamiento de datos (su "ejecución").</span><span class="sxs-lookup"><span data-stu-id="baf24-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="baf24-268">Se crea o se elimina un clúster de HDInsight a petición.</span><span class="sxs-lookup"><span data-stu-id="baf24-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="baf24-269">Puede crear alertas para estos eventos de usuario y configurarlos en el Administrador de toohello de notificaciones de correo electrónico de toosend y coadministrators de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="baf24-270">Además, puede especificar direcciones de correo electrónico adicionales de los usuarios que necesitan tooreceive notificaciones de correo electrónico cuando se cumplen las condiciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="baf24-271">Esta característica es útil cuando desea tooget una notificación cuando se produzcan errores y no desea que el monitor de toocontinuously su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="baf24-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="baf24-272">Actualmente, portal de hello no mostrar alertas de eventos.</span><span class="sxs-lookup"><span data-stu-id="baf24-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="baf24-273">Hola de uso [aplicación de supervisión y administración](data-factory-monitor-manage-app.md) toosee todas las alertas.</span><span class="sxs-lookup"><span data-stu-id="baf24-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="baf24-274">Especificación de una definición de alerta</span><span class="sxs-lookup"><span data-stu-id="baf24-274">Specify an alert definition</span></span>
<span data-ttu-id="baf24-275">toospecify una definición de alerta, cree un archivo JSON que describe las operaciones de Hola que desee toobe alerta en.</span><span class="sxs-lookup"><span data-stu-id="baf24-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="baf24-276">En el siguiente ejemplo de Hola, alerta de hello envía una notificación de correo electrónico para hello RunFinished operación.</span><span class="sxs-lookup"><span data-stu-id="baf24-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="baf24-277">toobe específico, se envía una notificación de correo electrónico cuando se ha completado una ejecución de factoría de datos de Hola y Hola ejecutar ha fallado (estado = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="baf24-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="baf24-278">Puede quitar **subestado** de hello definición de JSON si no desea toobe alerta en un error específico.</span><span class="sxs-lookup"><span data-stu-id="baf24-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="baf24-279">Este ejemplo se configura la alerta de Hola para todos los generadores de datos en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="baf24-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="baf24-280">Si desea hello toobe alerta configurada para una factoría de datos determinado, puede especificar la factoría de datos **resourceUri** en hello **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="baf24-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="baf24-281">Hello tabla siguiente proporciona Hola lista de operaciones disponibles y Estados (y sub-estados).</span><span class="sxs-lookup"><span data-stu-id="baf24-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="baf24-282">Nombre de la operación</span><span class="sxs-lookup"><span data-stu-id="baf24-282">Operation name</span></span> | <span data-ttu-id="baf24-283">Estado</span><span class="sxs-lookup"><span data-stu-id="baf24-283">Status</span></span> | <span data-ttu-id="baf24-284">Subestado</span><span class="sxs-lookup"><span data-stu-id="baf24-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baf24-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="baf24-285">RunStarted</span></span> |<span data-ttu-id="baf24-286">Started</span><span class="sxs-lookup"><span data-stu-id="baf24-286">Started</span></span> |<span data-ttu-id="baf24-287">Iniciando</span><span class="sxs-lookup"><span data-stu-id="baf24-287">Starting</span></span> |
| <span data-ttu-id="baf24-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="baf24-288">RunFinished</span></span> |<span data-ttu-id="baf24-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="baf24-289">Failed / Succeeded</span></span> |<span data-ttu-id="baf24-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="baf24-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="baf24-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="baf24-291">Succeeded</span></span><br/><br/><span data-ttu-id="baf24-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="baf24-292">FailedExecution</span></span><br/><br/><span data-ttu-id="baf24-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="baf24-293">TimedOut</span></span><br/><br/><span data-ttu-id="baf24-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="baf24-294"><Canceled</span></span><br/><br/><span data-ttu-id="baf24-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="baf24-295">FailedValidation</span></span><br/><br/><span data-ttu-id="baf24-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="baf24-296">Abandoned</span></span> |
| <span data-ttu-id="baf24-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="baf24-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="baf24-298">Started</span><span class="sxs-lookup"><span data-stu-id="baf24-298">Started</span></span> | |
| <span data-ttu-id="baf24-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="baf24-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="baf24-300">Correcto</span><span class="sxs-lookup"><span data-stu-id="baf24-300">Succeeded</span></span> | |
| <span data-ttu-id="baf24-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="baf24-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="baf24-302">Correcto</span><span class="sxs-lookup"><span data-stu-id="baf24-302">Succeeded</span></span> | |

<span data-ttu-id="baf24-303">Vea [crear regla de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) para obtener más información acerca de los elementos JSON de Hola que se usan en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="baf24-304">Implementar alerta Hola</span><span class="sxs-lookup"><span data-stu-id="baf24-304">Deploy hello alert</span></span>
<span data-ttu-id="baf24-305">alerta de hello toodeploy, use el cmdlet de PowerShell de Azure hello **AzureRmResourceGroupDeployment nuevo**, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="baf24-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="baf24-306">Una vez que haya terminado correctamente la implementación de grupo de recursos de hello, verá Hola siguientes mensajes:</span><span class="sxs-lookup"><span data-stu-id="baf24-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="baf24-307">Puede usar hello [crear regla de alerta](https://msdn.microsoft.com/library/azure/dn510366.aspx) API de REST toocreate una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="baf24-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="baf24-308">carga JSON de Hello es ejemplo JSON toohello similar.</span><span class="sxs-lookup"><span data-stu-id="baf24-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="baf24-309">Recuperar la lista de Hola de implementaciones de grupos de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="baf24-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="baf24-310">lista de hello tooretrieve de implementa las implementaciones de grupo de recursos de Azure, use el cmdlet hello **AzureRmResourceGroupDeployment Get**, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="baf24-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="baf24-311">Solución de problemas de eventos del usuario</span><span class="sxs-lookup"><span data-stu-id="baf24-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="baf24-312">Puede ver todos los eventos de Hola que se generan después de hacer clic hello **métricas y las operaciones** icono.</span><span class="sxs-lookup"><span data-stu-id="baf24-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Icono Métricas y operaciones](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="baf24-314">Haga clic en hello **eventos** eventos de hello toosee en mosaico.</span><span class="sxs-lookup"><span data-stu-id="baf24-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Icono de eventos](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="baf24-316">En hello **eventos** hoja, puede ver detalles sobre eventos, eventos filtrados y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="baf24-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Hoja Eventos](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="baf24-318">Haga clic en un **operación** en lista de operaciones de Hola que se produzca un error.</span><span class="sxs-lookup"><span data-stu-id="baf24-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Seleccionar una operación](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="baf24-320">Haga clic en un **Error** toosee detalles del evento sobre error Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Evento de error](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="baf24-322">Vea [una visión general de Azure cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) para cmdlets de PowerShell que puede usar tooadd, obtener o quitar alertas.</span><span class="sxs-lookup"><span data-stu-id="baf24-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="baf24-323">Estos son algunos ejemplos del uso de hello **AlertRule Get** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="baf24-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="baf24-324">Ejecute hello después de get-help comandos toosee detalles y ejemplos relacionados con el cmdlet Get-AlertRule de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="baf24-325">Si ve eventos de generación de alertas de hello en hello hoja portal pero no recibe notificaciones de correo electrónico, compruebe si dirección de correo electrónico de hello especificado se ha establecido tooreceive los correos electrónicos de remitentes externos.</span><span class="sxs-lookup"><span data-stu-id="baf24-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="baf24-326">los mensajes de alerta de Hola se podrían haber bloqueado por la configuración de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="baf24-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="baf24-327">Alertas en métricas</span><span class="sxs-lookup"><span data-stu-id="baf24-327">Alerts on metrics</span></span>
<span data-ttu-id="baf24-328">Puede usar Data Factory para capturar diversas métricas y crear alertas sobre las métricas.</span><span class="sxs-lookup"><span data-stu-id="baf24-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="baf24-329">Puede supervisar y crear alertas para hello siguiendo las métricas para intervalos de saludo de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="baf24-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="baf24-330">**Ejecuciones con error**</span><span class="sxs-lookup"><span data-stu-id="baf24-330">**Failed Runs**</span></span>
* <span data-ttu-id="baf24-331">**Ejecuciones correctas**</span><span class="sxs-lookup"><span data-stu-id="baf24-331">**Successful Runs**</span></span>

<span data-ttu-id="baf24-332">Estas métricas son útiles y le ayudarán a tooget que una visión general de global correctos y erróneos se ejecuta en la factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="baf24-333">Las métricas se emiten cada vez que hay una ejecución del segmento.</span><span class="sxs-lookup"><span data-stu-id="baf24-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="baf24-334">En principio Hola de hora de hello, estas métricas se agregan e insertan tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="baf24-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="baf24-335">las métricas de tooenable, configure una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="baf24-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="baf24-336">Habilitación de métricas</span><span class="sxs-lookup"><span data-stu-id="baf24-336">Enable metrics</span></span>
<span data-ttu-id="baf24-337">las métricas de tooenable, haga clic en siguiente Hola de hello **factoría de datos** hoja:</span><span class="sxs-lookup"><span data-stu-id="baf24-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="baf24-338">**Supervisión** > **Métrica** > **Configuración de diagnóstico** > **Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="baf24-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Vínculo a Diagnóstico](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="baf24-340">En hello **diagnósticos** hoja, haga clic en **en**, seleccione la cuenta de almacenamiento de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="baf24-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Hoja Diagnósticos](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="baf24-342">Podría tardar hasta hora tooone Hola métricas toobe visible en hello **supervisión** hoja como agregación de métricas se realiza cada hora.</span><span class="sxs-lookup"><span data-stu-id="baf24-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="baf24-343">Configuración de alertas en métricas</span><span class="sxs-lookup"><span data-stu-id="baf24-343">Set up an alert on metrics</span></span>
<span data-ttu-id="baf24-344">Haga clic en hello **las métricas de la factoría de datos** icono:</span><span class="sxs-lookup"><span data-stu-id="baf24-344">Click hello **Data Factory metrics** tile:</span></span>

![Icono Métricas de la factoría de datos](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="baf24-346">En hello **métrica** hoja, haga clic en **+ Agregar alerta** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="baf24-347">![Hoja Métrica de la factoría de datos &gt; Agregar alerta](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="baf24-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="baf24-348">En hello **agregar una regla de alerta** página, Hola pasos y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="baf24-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="baf24-349">Escriba un nombre para la alerta de hello (ejemplo: "alerta de error de").</span><span class="sxs-lookup"><span data-stu-id="baf24-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="baf24-350">Escriba una descripción de alerta de hello (ejemplo: "enviar un correo electrónico cuando se produce un error").</span><span class="sxs-lookup"><span data-stu-id="baf24-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="baf24-351">Seleccione una métrica ("ejecuciones con error" frente a "ejecuciones correctas").</span><span class="sxs-lookup"><span data-stu-id="baf24-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="baf24-352">Especifique una condición y el valor del umbral.</span><span class="sxs-lookup"><span data-stu-id="baf24-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="baf24-353">Especificar el período de Hola de tiempo.</span><span class="sxs-lookup"><span data-stu-id="baf24-353">Specify hello period of time.</span></span>
* <span data-ttu-id="baf24-354">Especifica si se debe enviar un correo electrónico tooowners, contributors y readers.</span><span class="sxs-lookup"><span data-stu-id="baf24-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Hoja Métrica de la factoría de datos > Agregar regla de alerta](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="baf24-356">Después de regla de alerta de Hola se agrega correctamente, se cierra la hoja de Hola y verá la nueva alerta de hello en hello **métrica** hoja.</span><span class="sxs-lookup"><span data-stu-id="baf24-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Hoja Métrica de la factoría de datos > Nueva alerta agregada](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="baf24-358">También debería ver el número de Hola de alertas en hello **reglas de alerta** icono.</span><span class="sxs-lookup"><span data-stu-id="baf24-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="baf24-359">Haga clic en hello **reglas de alerta** icono.</span><span class="sxs-lookup"><span data-stu-id="baf24-359">Click hello **Alert rules** tile.</span></span>

![Hoja Métrica de la factoría de datos: Reglas de alerta](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="baf24-361">En hello **reglas de alertas** hoja, vea las alertas existentes.</span><span class="sxs-lookup"><span data-stu-id="baf24-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="baf24-362">tooadd una alerta, haga clic en **Agregar alerta** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Hoja Reglas de alertas](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="baf24-364">Notificaciones de alerta</span><span class="sxs-lookup"><span data-stu-id="baf24-364">Alert notifications</span></span>
<span data-ttu-id="baf24-365">Después de regla de alerta de hello coincide con la condición de hello, debería obtener un correo electrónico que indica que se activa la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="baf24-366">Después de que se resuelve el problema de Hola y condición de alerta de hello no coincide con ya, obtendrá un correo electrónico que dice Hola alerta se resuelve.</span><span class="sxs-lookup"><span data-stu-id="baf24-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="baf24-367">Este comportamiento es diferente al de eventos en los que se envía una notificación en todos los errores en los que la regla de alerta se cumple.</span><span class="sxs-lookup"><span data-stu-id="baf24-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="baf24-368">Establecimiento de alertas mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="baf24-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="baf24-369">Puede implementar las alertas para métricas Hola misma forma que para los eventos.</span><span class="sxs-lookup"><span data-stu-id="baf24-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="baf24-370">**Definición de la alerta**</span><span class="sxs-lookup"><span data-stu-id="baf24-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="baf24-371">Reemplace *subscriptionId*, *resourceGroupName*, y *dataFactoryName* en el ejemplo de Hola con los valores adecuados.</span><span class="sxs-lookup"><span data-stu-id="baf24-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="baf24-372">*metricName* admite actualmente dos valores:</span><span class="sxs-lookup"><span data-stu-id="baf24-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="baf24-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="baf24-373">FailedRuns</span></span>
* <span data-ttu-id="baf24-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="baf24-374">SuccessfulRuns</span></span>

<span data-ttu-id="baf24-375">**Implementar alerta Hola**</span><span class="sxs-lookup"><span data-stu-id="baf24-375">**Deploy hello alert**</span></span>

<span data-ttu-id="baf24-376">alerta de hello toodeploy, use el cmdlet de PowerShell de Azure hello **AzureRmResourceGroupDeployment nuevo**, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="baf24-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="baf24-377">Debería ver el siguiente mensaje después de una correcta implementación:</span><span class="sxs-lookup"><span data-stu-id="baf24-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="baf24-378">También puede usar hello **AlertRule agregar** cmdlet toodeploy una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="baf24-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="baf24-379">Vea hello [AlertRule agregar](https://msdn.microsoft.com/library/mt282468.aspx) tema para obtener información detallada y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="baf24-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="baf24-380">Mover un grupo de recursos distinto de tooa de factoría de datos o una suscripción</span><span class="sxs-lookup"><span data-stu-id="baf24-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="baf24-381">Puede mover un grupo de recursos diferente de tooa de generador de datos o una suscripción diferente mediante hello **mover** botón en la página principal de saludo de la factoría de datos de la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="baf24-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Mover factoría de datos](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="baf24-383">También puede mover cualquier recurso relacionado (por ejemplo, las alertas que están asociadas a la factoría de datos de hello), junto con la factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="baf24-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Cuadro de diálogo Mover recursos](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
