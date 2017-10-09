---
title: "aaaQuery información del rendimiento de base de datos de SQL de Azure | Documentos de Microsoft"
description: "Supervisión del rendimiento de consulta identifica Hola mayoría usan la CPU realiza consultas con una base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="7fb22-103">Query Performance Insight de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="7fb22-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="7fb22-104">Administrar y optimizar el rendimiento de Hola de bases de datos relacional son una tarea difícil que requiere conocimientos importantes e inversión de tiempo.</span><span class="sxs-lookup"><span data-stu-id="7fb22-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="7fb22-105">Información de rendimiento de consultas permite toospend menos tiempo a la solución de problemas de rendimiento de la base de datos proporcionando siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="7fb22-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="7fb22-106">Información más detallada sobre el consumo de recursos (DTU) de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="7fb22-107">Hola principales consultas por recuento de CPU/duración/ejecución, que pueden optimizarse para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7fb22-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="7fb22-108">Hola capacidad toodrill hacia abajo en los detalles de Hola de una consulta, ver su texto y el historial de utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="7fb22-109">Anotaciones de ajuste del rendimiento que muestran las acciones realizadas por el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="7fb22-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="7fb22-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7fb22-110">Prerequisites</span></span>
* <span data-ttu-id="7fb22-111">Información de rendimiento de consultas requiere que el [Almacén de consultas](https://msdn.microsoft.com/library/dn817826.aspx) esté activo en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="7fb22-112">Si no se está ejecutando el almacén de consultas, el portal de hello solicita tooturn en.</span><span class="sxs-lookup"><span data-stu-id="7fb22-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="7fb22-113">Permisos</span><span class="sxs-lookup"><span data-stu-id="7fb22-113">Permissions</span></span>
<span data-ttu-id="7fb22-114">siguiente Hello [el control de acceso basado en roles](../active-directory/role-based-access-control-what-is.md) permisos son necesario toouse Query Performance Insight:</span><span class="sxs-lookup"><span data-stu-id="7fb22-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="7fb22-115">**Lector**, **propietario**, **colaborador**, **colaborador de la base de datos de SQL**, o **SQL Server colaborador** permisos son tooview requiere Hola que consumen más recursos gráficos y las consultas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="7fb22-116">**Propietario**, **colaborador**, **colaborador de la base de datos de SQL**, o **SQL Server colaborador** permisos son necesarios tooview texto de la consulta.</span><span class="sxs-lookup"><span data-stu-id="7fb22-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="7fb22-117">Uso de Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="7fb22-117">Using Query Performance Insight</span></span>
<span data-ttu-id="7fb22-118">Información de rendimiento de consultas es fácil toouse:</span><span class="sxs-lookup"><span data-stu-id="7fb22-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="7fb22-119">Abra [portal de Azure](https://portal.azure.com/) y base de datos de búsqueda que desea tooexamine.</span><span class="sxs-lookup"><span data-stu-id="7fb22-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="7fb22-120">En el menú de la izquierda, bajo Soporte y solución de problemas, seleccione "Información de rendimiento de consultas".</span><span class="sxs-lookup"><span data-stu-id="7fb22-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="7fb22-121">En la primera ficha hello, revise la lista de Hola de las consultas principales de consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="7fb22-122">Seleccione una consulta individual tooview sus detalles.</span><span class="sxs-lookup"><span data-stu-id="7fb22-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="7fb22-123">Abra el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md) y compruebe si existen recomendaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="7fb22-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="7fb22-124">Usar controles deslizantes o zoom toochange iconos observado intervalo.</span><span class="sxs-lookup"><span data-stu-id="7fb22-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![panel de rendimiento](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="7fb22-126">Un par de horas de datos debe toobe capturado por el almacén de consultas para la información de rendimiento de consultas de base de datos SQL tooprovide.</span><span class="sxs-lookup"><span data-stu-id="7fb22-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="7fb22-127">Si no tiene ninguna actividad base de datos de Hola o almacén de consultas no estaba activo durante un período de tiempo determinado, gráficos de hello estará vacíos cuando se muestra ese período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="7fb22-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="7fb22-128">Puede habilitar el almacén de consulta en cualquier momento si no se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="7fb22-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="7fb22-129">Revisión de las consultas que más CPU consumen</span><span class="sxs-lookup"><span data-stu-id="7fb22-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="7fb22-130">Hola [portal](http://portal.azure.com) Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="7fb22-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="7fb22-131">Base de datos SQL tooa y haga clic en **toda la configuración de** > **soporte técnico y solución de problemas** > **consultar información de rendimiento de**.</span><span class="sxs-lookup"><span data-stu-id="7fb22-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Información de rendimiento de consultas][1]
   
    <span data-ttu-id="7fb22-133">se abre la vista de consultas top Hello y se muestran consultas de consumo de CPU superiores Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="7fb22-134">Haga clic en alrededor de gráfico de Hola para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7fb22-134">Click around hello chart for details.</span></span><br><span data-ttu-id="7fb22-135">Hello línea superior muestra total % DTU de base de datos de hello, mientras que las barras de hello muestran % de CPU utilizado en consultas de hello seleccionado durante el intervalo seleccionado de hello (por ejemplo, si **semana pasada** se selecciona cada barra representa un día).</span><span class="sxs-lookup"><span data-stu-id="7fb22-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![principales consultas][2]
   
    <span data-ttu-id="7fb22-137">cuadrícula de la parte inferior de Hello representa información agregada para las consultas de hello visible.</span><span class="sxs-lookup"><span data-stu-id="7fb22-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="7fb22-138">Id. de consulta: identificador único de la consulta en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="7fb22-139">CPU por consulta durante el intervalo observable (depende de la función de agregación).</span><span class="sxs-lookup"><span data-stu-id="7fb22-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="7fb22-140">Duración por consulta (depende de la función de agregación).</span><span class="sxs-lookup"><span data-stu-id="7fb22-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="7fb22-141">Número total de ejecuciones para una consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="7fb22-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="7fb22-142">Seleccionar o borrar tooinclude de las consultas individuales o excluirlos de gráfico de hello mediante las casillas de verificación.</span><span class="sxs-lookup"><span data-stu-id="7fb22-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="7fb22-143">Si los datos se convierte en obsoletos, haga clic en hello **actualizar** botón.</span><span class="sxs-lookup"><span data-stu-id="7fb22-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="7fb22-144">Puede usar controles deslizantes y el intervalo de observación de zoom botones toochange e investigar picos: ![configuración](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="7fb22-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="7fb22-145">Opcionalmente, si desea una vista diferente, puede seleccionar la pestaña **Personalizado** y establecer:</span><span class="sxs-lookup"><span data-stu-id="7fb22-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="7fb22-146">Métrica (CPU, duración, recuento de ejecuciones)</span><span class="sxs-lookup"><span data-stu-id="7fb22-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="7fb22-147">Intervalo de tiempo (últimas 24 horas, semana anterior, mes anterior).</span><span class="sxs-lookup"><span data-stu-id="7fb22-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="7fb22-148">Número de consultas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-148">Number of queries.</span></span>
   * <span data-ttu-id="7fb22-149">Función de agregación.</span><span class="sxs-lookup"><span data-stu-id="7fb22-149">Aggregation function.</span></span>
     
     ![Configuración](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="7fb22-151">Visualización de los detalles de las consultas individuales</span><span class="sxs-lookup"><span data-stu-id="7fb22-151">Viewing individual query details</span></span>
<span data-ttu-id="7fb22-152">detalles de la consulta tooview:</span><span class="sxs-lookup"><span data-stu-id="7fb22-152">tooview query details:</span></span>

1. <span data-ttu-id="7fb22-153">Haga clic en cualquier consulta en la lista de Hola de las consultas principales.</span><span class="sxs-lookup"><span data-stu-id="7fb22-153">Click any query in hello list of top queries.</span></span>
   
    ![details](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="7fb22-155">se abre la vista de detalles de Hola y recuento de consumo/duración/ejecución de CPU de hello las consultas se divide en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="7fb22-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="7fb22-156">Haga clic en alrededor de gráfico de Hola para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7fb22-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="7fb22-157">Gráfico superior muestra los línea con total % DTU de base de datos, y las barras de Hola % de CPU utilizado por la consulta seleccionada Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="7fb22-158">Segundo gráfico muestra la duración total por consulta seleccionada Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="7fb22-159">Gráfico de la parte inferior muestra el número total de ejecuciones por consulta seleccionada Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![detalles de consulta][3]
4. <span data-ttu-id="7fb22-161">Si lo desea, utilice los controles deslizantes, botones de zoom o haga clic en **configuración** toocustomize cómo se muestran los datos de consulta o toopick un período de tiempo diferente.</span><span class="sxs-lookup"><span data-stu-id="7fb22-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="7fb22-162">Revisión de las principales consultas por duración</span><span class="sxs-lookup"><span data-stu-id="7fb22-162">Review top queries per duration</span></span>
<span data-ttu-id="7fb22-163">En actualización reciente de Hola de Query Performance Insight, presentamos dos nuevas métricas que pueden ayudarle a identificar posibles cuellos de botella: recuento de ejecución y la duración.</span><span class="sxs-lookup"><span data-stu-id="7fb22-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="7fb22-164">Consultas de larga duración tienen mayor potencial de hello más recursos de bloqueo, bloquear a otros usuarios y limitar la escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="7fb22-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="7fb22-165">También son mejores candidatas para la optimización de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="7fb22-166">tooidentify consultas de larga ejecución:</span><span class="sxs-lookup"><span data-stu-id="7fb22-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="7fb22-167">Abra la pestaña **Personalizado** en Información de rendimiento de consultas para la base de datos seleccionada</span><span class="sxs-lookup"><span data-stu-id="7fb22-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="7fb22-168">Cambiar las métricas toobe **duración**</span><span class="sxs-lookup"><span data-stu-id="7fb22-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="7fb22-169">Seleccione el número de consultas y el intervalo de observación</span><span class="sxs-lookup"><span data-stu-id="7fb22-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="7fb22-170">Seleccione la función de agregación</span><span class="sxs-lookup"><span data-stu-id="7fb22-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="7fb22-171">**Sum** aumenta el tiempo de ejecución de todas las consultas durante todo el intervalo de observación.</span><span class="sxs-lookup"><span data-stu-id="7fb22-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="7fb22-172">**Max** busca consultas cuyo tiempo de ejecución era máximo en todo el intervalo de observación.</span><span class="sxs-lookup"><span data-stu-id="7fb22-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="7fb22-173">**AVG** busca el tiempo medio de ejecución de todas las ejecuciones de consulta y mostrarle Hola superior fuera de estos promedios.</span><span class="sxs-lookup"><span data-stu-id="7fb22-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![duración de la consulta][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="7fb22-175">Revisión de las principales consultas por recuento de ejecuciones</span><span class="sxs-lookup"><span data-stu-id="7fb22-175">Review top queries per execution count</span></span>
<span data-ttu-id="7fb22-176">Es posible que el elevado número de ejecuciones no afecte a la propia base de datos y el uso de recursos puede ser bajo, pero la aplicación general podría ralentizarse.</span><span class="sxs-lookup"><span data-stu-id="7fb22-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="7fb22-177">En algunos casos, recuento de ejecución muy alto puede provocar tooincrease de red de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="7fb22-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="7fb22-178">Los ciclos de ida y vuelta afectan significativamente al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7fb22-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="7fb22-179">Son latencia toonetwork de asunto y toodownstream latencia del servidor.</span><span class="sxs-lookup"><span data-stu-id="7fb22-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="7fb22-180">Por ejemplo, muchos sitios Web orientadas a datos con un alto grado tener acceso a base de datos de Hola para cada solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="7fb22-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="7fb22-181">Mientras que la agrupación de conexiones permite, hello aumenta el tráfico de red y la carga de procesamiento en el servidor de base de datos de hello pueden afectar negativamente al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7fb22-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="7fb22-182">Consejo general es tookeep mínimo absoluto de tooan de viajes de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="7fb22-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="7fb22-183">tooidentify se ejecutan con frecuencia consultas consultas ("locuaces"):</span><span class="sxs-lookup"><span data-stu-id="7fb22-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="7fb22-184">Abra la pestaña **Personalizado** en Información de rendimiento de consultas para la base de datos seleccionada</span><span class="sxs-lookup"><span data-stu-id="7fb22-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="7fb22-185">Cambiar las métricas toobe **recuento de ejecución**</span><span class="sxs-lookup"><span data-stu-id="7fb22-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="7fb22-186">Seleccione el número de consultas y el intervalo de observación</span><span class="sxs-lookup"><span data-stu-id="7fb22-186">Select number of queries and observation interval</span></span>
   
    ![recuento de ejecuciones de la consulta][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="7fb22-188">Descripción de las anotaciones de ajuste del rendimiento</span><span class="sxs-lookup"><span data-stu-id="7fb22-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="7fb22-189">Mientras se explora la carga de trabajo en Query Performance Insight, quizás haya notado iconos con una línea vertical en la parte superior gráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="7fb22-190">Estos iconos son anotaciones; representan el rendimiento que afecta a las acciones realizadas por el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="7fb22-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="7fb22-191">Al desplazamiento de anotación, obtendrá información básica acerca de la acción de hello:</span><span class="sxs-lookup"><span data-stu-id="7fb22-191">By hovering annotation, you get basic information about hello action:</span></span>

![anotación de la consulta][6]

<span data-ttu-id="7fb22-193">Si desea obtener más tooknow o aplicar la recomendación del asistente, haga clic en el icono de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="7fb22-194">Se abrirán los detalles de la acción.</span><span class="sxs-lookup"><span data-stu-id="7fb22-194">It will open details of action.</span></span> <span data-ttu-id="7fb22-195">Si se trata de una recomendación activa, puede aplicarla inmediatamente mediante el comando.</span><span class="sxs-lookup"><span data-stu-id="7fb22-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![detalles de la anotación de la consulta][7]

### <a name="multiple-annotations"></a><span data-ttu-id="7fb22-197">Varias anotaciones.</span><span class="sxs-lookup"><span data-stu-id="7fb22-197">Multiple annotations.</span></span>
<span data-ttu-id="7fb22-198">Es posible que debido a nivel de zoom, las anotaciones que se cierre tooeach otros obtener contraerá en uno.</span><span class="sxs-lookup"><span data-stu-id="7fb22-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="7fb22-199">Un icono especial representará este suceso y, al hacer clic en él, se abrirá una nueva hoja donde se mostrará una lista de las anotaciones agrupadas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="7fb22-200">Correlación de consultas y las acciones de optimización del rendimiento puede ayudar a toobetter a comprender la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7fb22-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="7fb22-201">Optimización de la configuración de almacén de consultas de Hola para Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="7fb22-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="7fb22-202">Durante el uso de información de rendimiento de consultas, pueden surgir Hola siguientes mensajes del almacén de consultas:</span><span class="sxs-lookup"><span data-stu-id="7fb22-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="7fb22-203">"El Almacén de consultas no está configurado correctamente en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="7fb22-204">Haga clic aquí toolearn más."</span><span class="sxs-lookup"><span data-stu-id="7fb22-204">Click here toolearn more."</span></span>
* <span data-ttu-id="7fb22-205">"El Almacén de consultas no está configurado correctamente en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="7fb22-206">Haga clic aquí toochange configuración."</span><span class="sxs-lookup"><span data-stu-id="7fb22-206">Click here toochange settings."</span></span> 

<span data-ttu-id="7fb22-207">Estos mensajes suelen aparecen al almacén de consultas no es capaz de toocollect nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="7fb22-208">El primer caso sucede si el Almacén de consultas está en estado de solo lectura y los parámetros están óptimamente establecidos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="7fb22-209">Para solucionarlo, puede aumentar el tamaño del Almacén de consultas o borrar el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![botón qds][8]

<span data-ttu-id="7fb22-211">El segundo caso sucede si el Almacén de consultas está desactivado o los parámetros no están óptimamente establecidos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="7fb22-212">Puede cambiar Hola captura y retención enable y directivas de almacén de consultas mediante la ejecución de comandos siguientes o directamente desde el portal:</span><span class="sxs-lookup"><span data-stu-id="7fb22-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![botón qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="7fb22-214">Directiva de retención y captura recomendada</span><span class="sxs-lookup"><span data-stu-id="7fb22-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="7fb22-215">Hay dos tipos de directivas de retención:</span><span class="sxs-lookup"><span data-stu-id="7fb22-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="7fb22-216">Tamaño basa - si se alcanza tooAUTO conjunto limpiará datos automáticamente si se encuentran cerca tamaño máximo.</span><span class="sxs-lookup"><span data-stu-id="7fb22-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="7fb22-217">Tiempo en la función: de forma predeterminada se establecerá too30 días, lo que significa que, si el almacén de consultas se quedará sin espacio, eliminará consultar información más de 30 días</span><span class="sxs-lookup"><span data-stu-id="7fb22-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="7fb22-218">La directiva de capturas se podría establecer como:</span><span class="sxs-lookup"><span data-stu-id="7fb22-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="7fb22-219">**Todas**: captura todas las consultas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="7fb22-220">**Automática**: se ignoran las consultas poco frecuentes y las consultas con una duración de ejecución y compilación insignificantes.</span><span class="sxs-lookup"><span data-stu-id="7fb22-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="7fb22-221">Los umbrales para la duración del tiempo de ejecución y de compilación y para el recuento de ejecuciones se determinan internamente.</span><span class="sxs-lookup"><span data-stu-id="7fb22-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="7fb22-222">Se trata de una opción predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fb22-222">This is hello default option.</span></span>
* <span data-ttu-id="7fb22-223">**Ninguna**: el Almacén de consultas deja de capturar nuevas consultas, pero las estadísticas en tiempo de ejecución de las consultas ya capturadas siguen recopilándose.</span><span class="sxs-lookup"><span data-stu-id="7fb22-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="7fb22-224">Se recomienda establecer todas las directivas tooAUTO y limpia directiva too30 días:</span><span class="sxs-lookup"><span data-stu-id="7fb22-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="7fb22-225">Aumentar el tamaño del almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-225">Increase size of Query Store.</span></span> <span data-ttu-id="7fb22-226">Esto podría ser realizadas por base de datos de conexión tooa y emitir consulta siguiente:</span><span class="sxs-lookup"><span data-stu-id="7fb22-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="7fb22-227">Aplicar esta configuración finalmente realizará el almacén de consultas recopilar nuevas consultas, sin embargo, si no desea toowait puede borrar el almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="7fb22-228">Ejecución de la consulta siguiente eliminará toda la información actual de hello almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="7fb22-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="7fb22-229">Resumen</span><span class="sxs-lookup"><span data-stu-id="7fb22-229">Summary</span></span>
<span data-ttu-id="7fb22-230">Información de rendimiento de consultas le ayudará a comprender el impacto de hello de la carga de trabajo de consulta y cómo se relaciona con toodatabase el consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7fb22-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="7fb22-231">Con esta característica, aprenderá acerca de las consultas que consumen más de hello y, identificar fácilmente hello las toofix antes de que resulten un problema.</span><span class="sxs-lookup"><span data-stu-id="7fb22-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fb22-232">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7fb22-232">Next steps</span></span>
<span data-ttu-id="7fb22-233">Para obtener más recomendaciones acerca de cómo mejorar el rendimiento de saludo de la base de datos SQL, haga clic en [recomendaciones](sql-database-advisor.md) en hello **Query Performance Insight** hoja.</span><span class="sxs-lookup"><span data-stu-id="7fb22-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

![Asesor de rendimiento](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

