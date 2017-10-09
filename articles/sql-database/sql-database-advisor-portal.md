---
title: recomendaciones de rendimiento aaaApply - base de datos de SQL de Azure | Documentos de Microsoft
description: "Puede utilizar las recomendaciones de rendimiento de Azure toofind portal Hola que pueden optimizar el rendimiento de la base de datos de SQL Azure o toocorrect algún problema identificado en la carga de trabajo."
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
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="f8a1e-103">Búsqueda y aplicación de recomendaciones de rendimiento</span><span class="sxs-lookup"><span data-stu-id="f8a1e-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="f8a1e-104">Puede utilizar las recomendaciones de rendimiento de Azure toofind portal Hola que pueden optimizar el rendimiento de la base de datos de SQL Azure o toocorrect algún problema identificado en la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="f8a1e-105">**Recomendación de rendimiento** página de portal de Azure le permite toofind hello las mejores recomendaciones en función de su impacto potencial.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="f8a1e-106">Visualización de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="f8a1e-106">Viewing recommendations</span></span>

<span data-ttu-id="f8a1e-107">tooview y aplicar recomendaciones de rendimiento, necesita Hola correcto [el control de acceso basado en roles](../active-directory/role-based-access-control-what-is.md) permisos en Azure.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="f8a1e-108">**Lector**, **colaborador de la base de datos de SQL** permisos son necesarios tooview recomendaciones, y **propietario**, **colaborador de la base de datos de SQL** se requieren permisos tooexecute ninguna acción; crear o quitar índices y cancelar la creación del índice.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="f8a1e-109">Usar hello siguiendo las recomendaciones de rendimiento de toofind de pasos en el portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="f8a1e-110">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f8a1e-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f8a1e-111">Vaya demasiado**más servicios** > **bases de datos SQL**y seleccione la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="f8a1e-112">Navegue demasiado**recomendación de rendimiento** tooview recomendaciones disponibles para la base de datos seleccionada de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="f8a1e-113">Recomendaciones de rendimiento son shonw en hello tabla toohello similares que se muestra en hello figura siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Recomendaciones](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="f8a1e-115">Las recomendaciones se ordenan por su posible impacto en el rendimiento en hello siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="f8a1e-116">Impacto</span><span class="sxs-lookup"><span data-stu-id="f8a1e-116">Impact</span></span> | <span data-ttu-id="f8a1e-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8a1e-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8a1e-118">Alto</span><span class="sxs-lookup"><span data-stu-id="f8a1e-118">High</span></span> |<span data-ttu-id="f8a1e-119">Recomendaciones de alto impacto deben proporcionar el impacto de rendimiento más importante de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="f8a1e-120">Mediano</span><span class="sxs-lookup"><span data-stu-id="f8a1e-120">Medium</span></span> |<span data-ttu-id="f8a1e-121">Las recomendaciones de impacto moderado deben mejorar el rendimiento, pero no de manera significativa.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="f8a1e-122">Bajo</span><span class="sxs-lookup"><span data-stu-id="f8a1e-122">Low</span></span> |<span data-ttu-id="f8a1e-123">Las recomendaciones de bajo impacto deben proporcionar un mejor rendimiento que el que se produciría sin ellas, pero es posible que las mejoras no sean significativas.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="f8a1e-124">La base de datos de SQL Azure debe toomonitor actividades al menos un día en orden tooidentify algunas recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="f8a1e-125">Hola base de datos de SQL Azure puede optimizar más fácilmente para patrones de consulta coherente que sea posible para ráfagas irregular aleatorios de actividad.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="f8a1e-126">Si las recomendaciones no están disponible corrently, Hola **recomendación de rendimiento** página proporciona un mensaje que explica por qué.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="f8a1e-127">También puede ver el estado de Hola de operaciones históricas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="f8a1e-128">Seleccione una recomendación o estado toosee más detalles.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="f8a1e-129">Este es un ejemplo de la recomendación "Crear el índice" Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Creación de índice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="f8a1e-131">Aplicación de las recomendaciones</span><span class="sxs-lookup"><span data-stu-id="f8a1e-131">Applying recommendations</span></span>
<span data-ttu-id="f8a1e-132">La base de datos de SQL Azure proporciona control total sobre cómo se recomendaciones habilitado mediante cualquiera de hello tres opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="f8a1e-133">Aplicar recomendaciones individuales una a una.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="f8a1e-134">Habilitar hello tooautomatically optimización automática aplicar recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="f8a1e-135">tooimplement una recomendación manualmente, ejecute hello recomienda script de T-SQL en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="f8a1e-136">Seleccione cualquier tooview recomendación sus detalles y, a continuación, haga clic en **Ver script** tooreview Hola detalles exactos de la creación de recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="f8a1e-137">base de datos de Hello permanece en línea mientras se aplica la recomendación de hello: usar recomendación de rendimiento o el ajuste automático de nunca deja sin conexión una base de datos.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="f8a1e-138">Aplicar una recomendación individual</span><span class="sxs-lookup"><span data-stu-id="f8a1e-138">Apply an individual recommendation</span></span>
<span data-ttu-id="f8a1e-139">Puede revisar y aceptar recomendaciones una a una.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="f8a1e-140">En hello **recomendaciones** hoja, seleccione una recomendación.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="f8a1e-141">En hello **detalles** hoja haga clic en **aplicar** botón.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![Aplicar recomendaciones](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="f8a1e-143">Recomendación seleccionado se aplicará en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="f8a1e-144">Quitar las recomendaciones de la lista de Hola</span><span class="sxs-lookup"><span data-stu-id="f8a1e-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="f8a1e-145">Si la lista de recomendaciones contiene elementos que desee tooremove de lista de hello, puede descartar la recomendación de hello:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="f8a1e-146">Seleccione una recomendación en la lista de Hola de **recomendaciones** detalles de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="f8a1e-147">Haga clic en **descartar** en hello **detalles** hoja.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="f8a1e-148">Si lo desea, puede agregar elementos descartados de atrás toohello **recomendaciones** lista:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="f8a1e-149">En hello **recomendaciones** hoja haga clic en **vista descartada**.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="f8a1e-150">Seleccione un elemento descartado de hello lista tooview sus detalles.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="f8a1e-151">Si lo desea, haga clic en **deshacer descartar** tooadd Hola índice toohello atrás lista principal de **recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="f8a1e-152">Habilitación del ajuste automático</span><span class="sxs-lookup"><span data-stu-id="f8a1e-152">Enable automatic tuning</span></span>
<span data-ttu-id="f8a1e-153">Puede establecer las recomendaciones de tooimplement de base de datos de SQL Azure Hola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="f8a1e-154">A medida que las recomendaciones estén disponibles, estas se aplicarán de manera automática.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="f8a1e-155">Como con todas las recomendaciones administradas por hello servicio si impacto en el rendimiento hello es la recomendación de hello negativo se revertirán.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="f8a1e-156">En hello **recomendaciones** hoja, haga clic en **automatizar**:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Configuración del asesor](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="f8a1e-158">Seleccione tooautomate de acciones:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-158">Select actions tooautomate:</span></span>
   
    ![Índices recomendados](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="f8a1e-160">Ejecutar manualmente Hola recomendada script T-SQL</span><span class="sxs-lookup"><span data-stu-id="f8a1e-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="f8a1e-161">Seleccione cualquier recomendación y haga clic en **Ver script**.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="f8a1e-162">Ejecute este script en la base de datos toomanually aplique la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="f8a1e-163">*Índices que se ejecutan manualmente no se supervisan y validados para el impacto de rendimiento servicio hello* por lo que se sugiere que supervisar estos índices después de la creación tooverify proporcionan mejoras de rendimiento y ajustar o eliminarlos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="f8a1e-164">Si desea conocer detalles sobre la creación de índices, consulte [CREAR ÍNDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8a1e-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="f8a1e-165">Cancelación de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="f8a1e-165">Canceling recommendations</span></span>
<span data-ttu-id="f8a1e-166">Las recomendaciones que se encuentran en estado **Pending**, **Verifying** o **Success** pueden cancelarse.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="f8a1e-167">Las recomendaciones con estado **Executing** no se pueden cancelar.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="f8a1e-168">Seleccione una recomendación en hello **historial para la optimización** Hola de área tooopen **detalles recomendaciones** hoja.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="f8a1e-169">Haga clic en **cancelar** tooabort proceso de Hola de aplicando la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="f8a1e-170">Supervisión de operaciones</span><span class="sxs-lookup"><span data-stu-id="f8a1e-170">Monitoring operations</span></span>
<span data-ttu-id="f8a1e-171">Puede que una recomendación no se aplique de manera inmediata.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="f8a1e-172">portal de Hello proporciona detalles sobre el estado de saludo de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="f8a1e-173">siguiente Hola es Estados posibles que puede ser un índice en:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="f8a1e-174">Estado</span><span class="sxs-lookup"><span data-stu-id="f8a1e-174">Status</span></span> | <span data-ttu-id="f8a1e-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="f8a1e-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8a1e-176">Pending</span><span class="sxs-lookup"><span data-stu-id="f8a1e-176">Pending</span></span> |<span data-ttu-id="f8a1e-177">El comando de aplicación de recomendaciones se ha recibido y su ejecución está programada.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="f8a1e-178">Executing</span><span class="sxs-lookup"><span data-stu-id="f8a1e-178">Executing</span></span> |<span data-ttu-id="f8a1e-179">se está aplicando la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="f8a1e-180">Comprobando</span><span class="sxs-lookup"><span data-stu-id="f8a1e-180">Verifying</span></span> |<span data-ttu-id="f8a1e-181">Recomendación se aplicó correctamente y servicio Hola está midiendo las ventajas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="f8a1e-182">Correcto</span><span class="sxs-lookup"><span data-stu-id="f8a1e-182">Success</span></span> |<span data-ttu-id="f8a1e-183">La recomendación se aplicó correctamente y se han medido ventajas.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="f8a1e-184">Error</span><span class="sxs-lookup"><span data-stu-id="f8a1e-184">Error</span></span> |<span data-ttu-id="f8a1e-185">Se produjo un error durante el proceso de Hola de aplicando la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="f8a1e-186">Esto puede ser un problema transitorio, o posiblemente una tabla de toohello de cambios de esquema y script de Hola ya no es válido.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="f8a1e-187">En reversión</span><span class="sxs-lookup"><span data-stu-id="f8a1e-187">Reverting</span></span> |<span data-ttu-id="f8a1e-188">recomendación de Hola se aplicó, pero consideró no eficiente y se está revirtiendo automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="f8a1e-189">Reverted</span><span class="sxs-lookup"><span data-stu-id="f8a1e-189">Reverted</span></span> |<span data-ttu-id="f8a1e-190">recomendación de Hola se revirtió.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="f8a1e-191">Haga clic en una recomendación en proceso de hello lista toosee más detalles:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Índices recomendados](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="f8a1e-193">Reversión de una recomendación</span><span class="sxs-lookup"><span data-stu-id="f8a1e-193">Reverting a recommendation</span></span>
<span data-ttu-id="f8a1e-194">Si ha usado la recomendación de hello rendimiento recomendaciones tooapply Hola (es decir, que no ejecutó el script de Hola T-SQL manualmente) revertirá automáticamente se si encuentra toobe de impacto de rendimiento de hello negativo.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="f8a1e-195">Si por alguna razón, sencillamente, toorevert una recomendación para ello siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="f8a1e-196">Seleccione una recomendación aplicada en hello **para la optimización historial** área.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="f8a1e-197">Haga clic en **Revert** en hello **detalles de recomendación** hoja.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Índices recomendados](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="f8a1e-199">Supervisión del impacto en el rendimiento de las recomendaciones de índices</span><span class="sxs-lookup"><span data-stu-id="f8a1e-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="f8a1e-200">Después de que se han implementado correctamente recomendaciones (actualmente, las operaciones de índice y solo las recomendaciones de las consultas se parametrizan) puede hacer clic en **consulta visión** en hello recomendación detalles hoja tooopen [consulta Información del rendimiento](sql-database-query-performance.md) y ver el impacto en el rendimiento de las consultas principales Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Supervisar el impacto en el rendimiento](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="f8a1e-202">Resumen</span><span class="sxs-lookup"><span data-stu-id="f8a1e-202">Summary</span></span>
<span data-ttu-id="f8a1e-203">Azure SQL Database ofrece recomendaciones para mejorar el rendimiento de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="f8a1e-204">Al proporcionar scripts T-SQL, así como opciones de ejecución individual y completamente automática, consigue ayuda útil para optimizar la base de datos y, en última instancia, para mejorar el rendimiento de las consultas.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8a1e-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8a1e-205">Next steps</span></span>
<span data-ttu-id="f8a1e-206">Supervisar sus recomendaciones y continuar tooapply les toorefine rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="f8a1e-207">Las cargas de trabajo de bases de datos son dinámicas y cambian con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="f8a1e-208">La base de datos de SQL Azure continuará toomonitor y se proporcionan recomendaciones que pueden mejorar el rendimiento de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="f8a1e-209">Vea [el ajuste automático](sql-database-automatic-tuning.md) Hola de toolearn más información sobre el ajuste automático de la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="f8a1e-210">Consulte [Recomendaciones de rendimiento](sql-database-advisor.md) para ver información general sobre las recomendaciones de rendimiento de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="f8a1e-211">Vea [información de rendimiento de consultas](sql-database-query-performance.md) toolearn acerca de cómo ver el impacto en el rendimiento de las consultas principales Hola.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8a1e-212">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f8a1e-212">Additional resources</span></span>
* [<span data-ttu-id="f8a1e-213">Almacén de consultas</span><span class="sxs-lookup"><span data-stu-id="f8a1e-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="f8a1e-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="f8a1e-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="f8a1e-215">Control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="f8a1e-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

