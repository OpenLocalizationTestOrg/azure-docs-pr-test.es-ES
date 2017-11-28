---
title: "Aplicación de recomendaciones de rendimiento: Azure SQL Database | Microsoft Docs"
description: Puede usar Azure Portal para buscar recomendaciones de rendimiento que pueden optimizar el rendimiento de su instancia de Azure SQL Database o corregir un problema identificado en la carga de trabajo.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 018afaa8b08bd001e55693390e80c8e2c4f33a30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="bc691-103">Búsqueda y aplicación de recomendaciones de rendimiento</span><span class="sxs-lookup"><span data-stu-id="bc691-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="bc691-104">Puede usar Azure Portal para buscar recomendaciones de rendimiento que pueden optimizar el rendimiento de su instancia de Azure SQL Database o corregir un problema identificado en la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bc691-104">You can use the Azure portal to find performance recommendations that can optimize performance of your Azure SQL Database or to correct some issue identified in your workload.</span></span> <span data-ttu-id="bc691-105">La página **Recomendaciones de rendimiento** de Azure Portal permite buscar las principales recomendaciones en función de su impacto potencial.</span><span class="sxs-lookup"><span data-stu-id="bc691-105">**Performance recommendation** page in Azure portal enables you to find the top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="bc691-106">Visualización de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="bc691-106">Viewing recommendations</span></span>

<span data-ttu-id="bc691-107">Para ver y aplicar recomendaciones de rendimiento, necesita los permisos correctos de [control de acceso basado en rol](../active-directory/role-based-access-control-what-is.md) en Azure.</span><span class="sxs-lookup"><span data-stu-id="bc691-107">To view and apply performance recommendations, you need the correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="bc691-108">Se requieren permisos de **Lector** y **Colaborador de base de datos SQL** para ver recomendaciones, y permisos de **Propietario** y **Colaborador de base de datos SQL** para ejecutar acciones; por ejemplo, crear o quitar índices y cancelar la creación de índices.</span><span class="sxs-lookup"><span data-stu-id="bc691-108">**Reader**, **SQL DB Contributor** permissions are required to view recommendations, and **Owner**, **SQL DB Contributor** permissions are required to execute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="bc691-109">Use los pasos siguientes para buscar recomendaciones de rendimiento en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="bc691-109">Use the following steps to find performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="bc691-110">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bc691-110">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bc691-111">Vaya a **Más servicios** > **Bases de datos SQL** y seleccione la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bc691-111">Go to **More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="bc691-112">Vaya a **Recomendaciones de rendimiento** para ver las recomendaciones disponibles para la base de datos seleccionada.</span><span class="sxs-lookup"><span data-stu-id="bc691-112">Navigate to **Performance recommendation** to view available recommendations for the selected database.</span></span>

<span data-ttu-id="bc691-113">Las recomendaciones de rendimiento se muestran en una tabla similar a la de la siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="bc691-113">Performance recommendations are shonw in the table similar to the one shown on the following figure:</span></span>

![Recomendaciones](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="bc691-115">Las recomendaciones se ordenan en las siguientes categorías, según su impacto potencial sobre el rendimiento:</span><span class="sxs-lookup"><span data-stu-id="bc691-115">Recommendations are sorted by their potential impact on performance into the following categories:</span></span>

| <span data-ttu-id="bc691-116">Impacto</span><span class="sxs-lookup"><span data-stu-id="bc691-116">Impact</span></span> | <span data-ttu-id="bc691-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc691-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bc691-118">Alto</span><span class="sxs-lookup"><span data-stu-id="bc691-118">High</span></span> |<span data-ttu-id="bc691-119">Las recomendaciones de alto impacto debe tener el impacto más importante en el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="bc691-119">High impact recommendations should provide the most significant performance impact.</span></span> |
| <span data-ttu-id="bc691-120">Mediano</span><span class="sxs-lookup"><span data-stu-id="bc691-120">Medium</span></span> |<span data-ttu-id="bc691-121">Las recomendaciones de impacto moderado deben mejorar el rendimiento, pero no de manera significativa.</span><span class="sxs-lookup"><span data-stu-id="bc691-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="bc691-122">Bajo</span><span class="sxs-lookup"><span data-stu-id="bc691-122">Low</span></span> |<span data-ttu-id="bc691-123">Las recomendaciones de bajo impacto deben proporcionar un mejor rendimiento que el que se produciría sin ellas, pero es posible que las mejoras no sean significativas.</span><span class="sxs-lookup"><span data-stu-id="bc691-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="bc691-124">Azure SQL Database necesita supervisar actividades durante al menos un día para identificar algunas recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="bc691-124">Azure SQL Database needs to monitor activities at least for a day in order to identify some recommendations.</span></span> <span data-ttu-id="bc691-125">Azure SQL Database puede optimizar con patrones de consultas coherentes con más facilidad que en el caso de ráfagas irregulares de actividad.</span><span class="sxs-lookup"><span data-stu-id="bc691-125">The Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="bc691-126">Si no hay recomendaciones correctas disponibles, la página **Recomendaciones de rendimiento** proporciona un mensaje explicativo.</span><span class="sxs-lookup"><span data-stu-id="bc691-126">If recommendations are not corrently available, the **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="bc691-127">También puede ver el estado de las operaciones históricas.</span><span class="sxs-lookup"><span data-stu-id="bc691-127">You can also view the status of the historical operations.</span></span> <span data-ttu-id="bc691-128">Seleccione una recomendación o estado para ver sus detalles.</span><span class="sxs-lookup"><span data-stu-id="bc691-128">Select a recommendation or status to see  more details.</span></span>

<span data-ttu-id="bc691-129">Este es un ejemplo de la recomendación "Crear índice" de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bc691-129">Here is an example of "Create index" recommendation in the Azure portal.</span></span>

![Creación de índice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="bc691-131">Aplicación de las recomendaciones</span><span class="sxs-lookup"><span data-stu-id="bc691-131">Applying recommendations</span></span>
<span data-ttu-id="bc691-132">Azure SQL Database le proporciona un control total sobre el modo en que se habilitan las recomendaciones mediante una de las tres opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="bc691-132">Azure SQL Database gives you full control over how recommendations are enabled using any of the following three options:</span></span> 

* <span data-ttu-id="bc691-133">Aplicar recomendaciones individuales una a una.</span><span class="sxs-lookup"><span data-stu-id="bc691-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="bc691-134">Habilitar el ajuste automático para aplicar automáticamente recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="bc691-134">Enable the Automatic tuning to automatically apply recommendations.</span></span>
* <span data-ttu-id="bc691-135">Para implementar manualmente una recomendación, ejecute el script T-SQL recomendado en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bc691-135">To implement a recommendation manually, run the recommended T-SQL script against your database.</span></span>

<span data-ttu-id="bc691-136">Seleccione cualquier recomendación para ver sus detalles y, luego, haga clic en **Ver script** para revisar los detalles exactos del modo en que se crea la recomendación.</span><span class="sxs-lookup"><span data-stu-id="bc691-136">Select any recommendation to view its details and then click **View script** to review the exact details of how the recommendation is created.</span></span>

<span data-ttu-id="bc691-137">La base de datos permanece en línea mientras se aplica la recomendación; cuando se usa la recomendación de rendimiento o el ajuste automático, no se desconecta nunca una base de datos.</span><span class="sxs-lookup"><span data-stu-id="bc691-137">The database remains online while the recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="bc691-138">Aplicar una recomendación individual</span><span class="sxs-lookup"><span data-stu-id="bc691-138">Apply an individual recommendation</span></span>
<span data-ttu-id="bc691-139">Puede revisar y aceptar recomendaciones una a una.</span><span class="sxs-lookup"><span data-stu-id="bc691-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="bc691-140">En la hoja **Recomendaciones**, seleccione una recomendación.</span><span class="sxs-lookup"><span data-stu-id="bc691-140">On the **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="bc691-141">En la hoja **Detalles**, haga clic en el botón **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="bc691-141">On the **Details** blade click **Apply** button.</span></span>
   
    ![Aplicar recomendaciones](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="bc691-143">Se aplicará la recomendación seleccionada en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bc691-143">Selected recommendation will be applied on the database.</span></span>

### <a name="removing-recommendations-from-the-list"></a><span data-ttu-id="bc691-144">Eliminación de recomendaciones de la lista</span><span class="sxs-lookup"><span data-stu-id="bc691-144">Removing recommendations from the list</span></span>
<span data-ttu-id="bc691-145">Si la lista de recomendaciones contiene elementos que quiere quitar de la lista, puede descartar la recomendación:</span><span class="sxs-lookup"><span data-stu-id="bc691-145">If your list of recommendations contains items that you want to remove from the list, you can discard the recommendation:</span></span>

1. <span data-ttu-id="bc691-146">Seleccione una recomendación en la lista **Recomendaciones** para abrir los detalles.</span><span class="sxs-lookup"><span data-stu-id="bc691-146">Select a recommendation in the list of **Recommendations** to open the details.</span></span>
2. <span data-ttu-id="bc691-147">Haga clic en **Descartar** en la hoja **Detalles**.</span><span class="sxs-lookup"><span data-stu-id="bc691-147">Click **Discard** on the **Details** blade.</span></span>

<span data-ttu-id="bc691-148">Si quiere, puede volver a agregar elementos descartados a la lista **Recomendaciones** :</span><span class="sxs-lookup"><span data-stu-id="bc691-148">If desired, you can add discarded items back to the **Recommendations** list:</span></span>

1. <span data-ttu-id="bc691-149">En la hoja **Recomendaciones**, haga clic en **Ver descartados**.</span><span class="sxs-lookup"><span data-stu-id="bc691-149">On the **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="bc691-150">Seleccione un elemento descartado de la lista para ver los detalles.</span><span class="sxs-lookup"><span data-stu-id="bc691-150">Select a discarded item from the list to view its details.</span></span>
3. <span data-ttu-id="bc691-151">También puede hacer clic en **Deshacer Descartar** para volver a agregar el índice a la lista principal de **Recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="bc691-151">Optionally, click **Undo Discard** to add the index back to the main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="bc691-152">Habilitación del ajuste automático</span><span class="sxs-lookup"><span data-stu-id="bc691-152">Enable automatic tuning</span></span>
<span data-ttu-id="bc691-153">Puede establecer que Azure SQL Database implemente las recomendaciones de forma automática.</span><span class="sxs-lookup"><span data-stu-id="bc691-153">You can set the Azure SQL Database to implement recommendations automatically.</span></span> <span data-ttu-id="bc691-154">A medida que las recomendaciones estén disponibles, estas se aplicarán de manera automática.</span><span class="sxs-lookup"><span data-stu-id="bc691-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="bc691-155">Al igual que con todas las recomendaciones que administra el servicio, si el impacto en el rendimiento es negativo, se revertirá la recomendación.</span><span class="sxs-lookup"><span data-stu-id="bc691-155">As with all recommendations managed by the service if the performance impact is negative the recommendation will be reverted.</span></span>

1. <span data-ttu-id="bc691-156">En la hoja **Recomendaciones**, haga clic en **Automatizar**:</span><span class="sxs-lookup"><span data-stu-id="bc691-156">On the **Recommendations** blade, click **Automate**:</span></span>
   
    ![Configuración del asesor](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="bc691-158">Seleccione las acciones que desee automatizar:</span><span class="sxs-lookup"><span data-stu-id="bc691-158">Select actions to automate:</span></span>
   
    ![Índices recomendados](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-the-recommended-t-sql-script"></a><span data-ttu-id="bc691-160">Ejecutar manualmente el script T-SQL recomendado</span><span class="sxs-lookup"><span data-stu-id="bc691-160">Manually run the recommended T-SQL script</span></span>
<span data-ttu-id="bc691-161">Seleccione cualquier recomendación y haga clic en **Ver script**.</span><span class="sxs-lookup"><span data-stu-id="bc691-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="bc691-162">Ejecute este script en la base de datos para aplicar la recomendación manualmente.</span><span class="sxs-lookup"><span data-stu-id="bc691-162">Run this script against your database to manually apply the recommendation.</span></span>

<span data-ttu-id="bc691-163">*El servicio no supervisa ni valida los índices que se ejecutan de manera manual para conocer el impacto en el rendimiento* , por lo que se recomienda supervisar estos índices después de su creación para comprobar que proporcionen mejoras en el rendimiento y, en caso necesario, ajustarlos o eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="bc691-163">*Indexes that are manually executed are not monitored and validated for performance impact by the service* so it is suggested that you monitor these indexes after creation to verify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="bc691-164">Si desea conocer detalles sobre la creación de índices, consulte [CREAR ÍNDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc691-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="bc691-165">Cancelación de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="bc691-165">Canceling recommendations</span></span>
<span data-ttu-id="bc691-166">Las recomendaciones que se encuentran en estado **Pending**, **Verifying** o **Success** pueden cancelarse.</span><span class="sxs-lookup"><span data-stu-id="bc691-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="bc691-167">Las recomendaciones con estado **Executing** no se pueden cancelar.</span><span class="sxs-lookup"><span data-stu-id="bc691-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="bc691-168">Seleccione una recomendación en el área **Historial de ajuste** para abrir la hoja de **detalles de recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="bc691-168">Select a recommendation in the **Tuning History** area to open the **recommendations details** blade.</span></span>
2. <span data-ttu-id="bc691-169">Haga clic en **Cancelar** para anular el proceso de aplicación de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="bc691-169">Click **Cancel** to abort the process of applying the recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="bc691-170">Supervisión de operaciones</span><span class="sxs-lookup"><span data-stu-id="bc691-170">Monitoring operations</span></span>
<span data-ttu-id="bc691-171">Puede que una recomendación no se aplique de manera inmediata.</span><span class="sxs-lookup"><span data-stu-id="bc691-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="bc691-172">El portal proporciona detalles sobre el estado de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="bc691-172">The portal provides details regarding the status of recommendation.</span></span> <span data-ttu-id="bc691-173">A continuación se indican los posibles estados en los que un índice puede encontrarse:</span><span class="sxs-lookup"><span data-stu-id="bc691-173">The following are possible states that an index can be in:</span></span>

| <span data-ttu-id="bc691-174">Estado</span><span class="sxs-lookup"><span data-stu-id="bc691-174">Status</span></span> | <span data-ttu-id="bc691-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="bc691-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="bc691-176">Pending</span><span class="sxs-lookup"><span data-stu-id="bc691-176">Pending</span></span> |<span data-ttu-id="bc691-177">El comando de aplicación de recomendaciones se ha recibido y su ejecución está programada.</span><span class="sxs-lookup"><span data-stu-id="bc691-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="bc691-178">Executing</span><span class="sxs-lookup"><span data-stu-id="bc691-178">Executing</span></span> |<span data-ttu-id="bc691-179">La recomendación está aplicándose.</span><span class="sxs-lookup"><span data-stu-id="bc691-179">The recommendation is being applied.</span></span> |
| <span data-ttu-id="bc691-180">Comprobando</span><span class="sxs-lookup"><span data-stu-id="bc691-180">Verifying</span></span> |<span data-ttu-id="bc691-181">La recomendación se aplicó correctamente y el servicio está midiendo las ventajas.</span><span class="sxs-lookup"><span data-stu-id="bc691-181">Recommendation was successfully applied and the service is measuring the benefits.</span></span> |
| <span data-ttu-id="bc691-182">Correcto</span><span class="sxs-lookup"><span data-stu-id="bc691-182">Success</span></span> |<span data-ttu-id="bc691-183">La recomendación se aplicó correctamente y se han medido ventajas.</span><span class="sxs-lookup"><span data-stu-id="bc691-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="bc691-184">Error</span><span class="sxs-lookup"><span data-stu-id="bc691-184">Error</span></span> |<span data-ttu-id="bc691-185">Se produjo un error durante el proceso de aplicación de recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="bc691-185">An error occurred during the process of applying the recommendation.</span></span> <span data-ttu-id="bc691-186">Puede tratarse de un problema transitorio, o posiblemente se produjo un cambio de esquema en la tabla y el script ya no es válido.</span><span class="sxs-lookup"><span data-stu-id="bc691-186">This can be a transient issue, or possibly a schema change to the table and the script is no longer valid.</span></span> |
| <span data-ttu-id="bc691-187">En reversión</span><span class="sxs-lookup"><span data-stu-id="bc691-187">Reverting</span></span> |<span data-ttu-id="bc691-188">La recomendación se aplicó, pero se ha considerado que no tuvo rendimiento y se está revirtiendo automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bc691-188">The recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="bc691-189">Reverted</span><span class="sxs-lookup"><span data-stu-id="bc691-189">Reverted</span></span> |<span data-ttu-id="bc691-190">La recomendación se revirtió.</span><span class="sxs-lookup"><span data-stu-id="bc691-190">The recommendation was reverted.</span></span> |

<span data-ttu-id="bc691-191">Haga clic en una recomendación en proceso de la lista para ver más detalles:</span><span class="sxs-lookup"><span data-stu-id="bc691-191">Click an in-process recommendation from the list to see more details:</span></span>

![Índices recomendados](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="bc691-193">Reversión de una recomendación</span><span class="sxs-lookup"><span data-stu-id="bc691-193">Reverting a recommendation</span></span>
<span data-ttu-id="bc691-194">Si usó las recomendaciones de rendimiento para aplicar la recomendación (es decir, no ejecutó manualmente el script T-SQL), se revertirá automáticamente si detecta que afecta de manera negativa al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="bc691-194">If you used the performance recommendations to apply the recommendation (meaning you did not manually run the T-SQL script) it will automatically revert it if it finds the performance impact to be negative.</span></span> <span data-ttu-id="bc691-195">Si tan solo quiere revertir una recomendación, por el motivo que sea, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="bc691-195">If for any reason you simply want to revert a recommendation you can do the following:</span></span>

1. <span data-ttu-id="bc691-196">En el área **Historial de ajuste** , seleccione una recomendación que se haya aplicado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bc691-196">Select a successfully applied recommendation in the **Tuning history** area.</span></span>
2. <span data-ttu-id="bc691-197">Haga clic en **Revertir** en la hoja de **detalles de recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="bc691-197">Click **Revert** on the **recommendation details** blade.</span></span>

![Índices recomendados](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="bc691-199">Supervisión del impacto en el rendimiento de las recomendaciones de índices</span><span class="sxs-lookup"><span data-stu-id="bc691-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="bc691-200">Una vez implementadas correctamente las recomendaciones (actualmente, solo recomendaciones para indizar operaciones y parametrizar consultas), puede hacer clic en **Detalles de la consulta** en la hoja de detalles de recomendaciones para abrir [Información de rendimiento de consultas](sql-database-query-performance.md) y ver el impacto en el rendimiento de las consultas principales.</span><span class="sxs-lookup"><span data-stu-id="bc691-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on the recommendation details blade to open [Query Performance Insights](sql-database-query-performance.md) and see the performance impact of your top queries.</span></span>

![Supervisar el impacto en el rendimiento](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="bc691-202">Resumen</span><span class="sxs-lookup"><span data-stu-id="bc691-202">Summary</span></span>
<span data-ttu-id="bc691-203">Azure SQL Database ofrece recomendaciones para mejorar el rendimiento de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="bc691-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="bc691-204">Al proporcionar scripts T-SQL, así como opciones de ejecución individual y completamente automática, consigue ayuda útil para optimizar la base de datos y, en última instancia, para mejorar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="bc691-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc691-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bc691-205">Next steps</span></span>
<span data-ttu-id="bc691-206">Supervise las recomendaciones y siga aplicándolas para refinar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="bc691-206">Monitor your recommendations and continue to apply them to refine performance.</span></span> <span data-ttu-id="bc691-207">Las cargas de trabajo de bases de datos son dinámicas y cambian con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="bc691-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="bc691-208">Azure SQL Database seguirá supervisando y ofreciendo recomendaciones que podrían mejorar el rendimiento de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="bc691-208">Azure SQL Database will continue to monitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="bc691-209">Consulte [Ajuste automático](sql-database-automatic-tuning.md) para más información sobre el ajuste automático en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bc691-209">See [Automatic tuning](sql-database-automatic-tuning.md) to learn more about the automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="bc691-210">Consulte [Recomendaciones de rendimiento](sql-database-advisor.md) para ver información general sobre las recomendaciones de rendimiento de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bc691-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="bc691-211">Consulte [Query Performance Insight](sql-database-query-performance.md) para más información sobre el impacto en el rendimiento de las principales consultas.</span><span class="sxs-lookup"><span data-stu-id="bc691-211">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bc691-212">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bc691-212">Additional resources</span></span>
* [<span data-ttu-id="bc691-213">Almacén de consultas</span><span class="sxs-lookup"><span data-stu-id="bc691-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="bc691-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="bc691-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="bc691-215">Control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="bc691-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

