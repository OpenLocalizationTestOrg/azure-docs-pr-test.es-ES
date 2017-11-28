---
title: "Información de rendimiento de consultas para Azure SQL Database | Microsoft Docs"
description: "La supervisión del rendimiento de las consultas identifica las consultas que más CPU consumen en una base de datos SQL de Azure."
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
ms.openlocfilehash: 1925d4ff8f5b16a0df56de987f8653cfd8441c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="f4d38-103">Query Performance Insight de Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="f4d38-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="f4d38-104">La administración y ajuste del rendimiento de las bases de datos relacionales son tareas difíciles que requieren una gran inversión de tiempo y muchos conocimientos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="f4d38-105">Información de rendimiento de consultas permite dedicar menos tiempo a la solución de problemas de rendimiento de bases de datos, ya que proporciona:</span><span class="sxs-lookup"><span data-stu-id="f4d38-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="f4d38-106">Información más detallada sobre el consumo de recursos (DTU) de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="f4d38-107">Las consultas principales por CPU, duración y recuento de ejecuciones, que se pueden ajustar para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f4d38-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="f4d38-108">La capacidad de profundizar en los detalles de una consulta, ver su texto e historial de utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="f4d38-109">Anotaciones de ajuste del rendimiento que muestran las acciones realizadas por el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="f4d38-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="f4d38-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f4d38-110">Prerequisites</span></span>
* <span data-ttu-id="f4d38-111">Información de rendimiento de consultas requiere que el [Almacén de consultas](https://msdn.microsoft.com/library/dn817826.aspx) esté activo en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="f4d38-112">Si Almacén de consultas no está en ejecución, el portal le pedirá que lo active.</span><span class="sxs-lookup"><span data-stu-id="f4d38-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="f4d38-113">Permisos</span><span class="sxs-lookup"><span data-stu-id="f4d38-113">Permissions</span></span>
<span data-ttu-id="f4d38-114">Los siguientes permisos de [control de acceso basado en roles](../active-directory/role-based-access-control-what-is.md) se requieren para usar Query Performance Insight:</span><span class="sxs-lookup"><span data-stu-id="f4d38-114">The following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="f4d38-115">Se requieren permisos de **lector**, **propietario**, **colaborador**, **colaborador de base de datos SQL** o **colaborador de SQL Server** para ver las consultas y los gráficos que más recursos consumen.</span><span class="sxs-lookup"><span data-stu-id="f4d38-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="f4d38-116">Se requieren permisos de **propietario**, **colaborador**, **colaborador de base de datos SQL** o **colaborador de SQL Server** para ver el texto de la consulta.</span><span class="sxs-lookup"><span data-stu-id="f4d38-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="f4d38-117">Uso de Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="f4d38-117">Using Query Performance Insight</span></span>
<span data-ttu-id="f4d38-118">Query Performance Insight es fácil de usar:</span><span class="sxs-lookup"><span data-stu-id="f4d38-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="f4d38-119">Abra [Portal de Azure](https://portal.azure.com/) y busque la base de datos que desee examinar.</span><span class="sxs-lookup"><span data-stu-id="f4d38-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="f4d38-120">En el menú de la izquierda, bajo Soporte y solución de problemas, seleccione "Información de rendimiento de consultas".</span><span class="sxs-lookup"><span data-stu-id="f4d38-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="f4d38-121">En la primera pestaña, revise la lista de consultas que más recursos consumen.</span><span class="sxs-lookup"><span data-stu-id="f4d38-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="f4d38-122">Seleccione una consulta individual para ver sus detalles.</span><span class="sxs-lookup"><span data-stu-id="f4d38-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="f4d38-123">Abra el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md) y compruebe si existen recomendaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="f4d38-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="f4d38-124">Use controles deslizantes o iconos de zoom para cambiar el intervalo observado.</span><span class="sxs-lookup"><span data-stu-id="f4d38-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![panel de rendimiento](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="f4d38-126">Para proporcionar información de rendimiento de consultas, es preciso que el Almacén de consultas para Base de datos SQL capture un par de horas de datos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="f4d38-127">Si la base de datos no tiene actividad o Almacén de consultas no estuvo activo durante un período determinado, los gráficos estará vacíos al mostrar dicho período.</span><span class="sxs-lookup"><span data-stu-id="f4d38-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="f4d38-128">Puede habilitar el almacén de consulta en cualquier momento si no se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="f4d38-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="f4d38-129">Revisión de las consultas que más CPU consumen</span><span class="sxs-lookup"><span data-stu-id="f4d38-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="f4d38-130">En el [portal](http://portal.azure.com) , realice estas acciones:</span><span class="sxs-lookup"><span data-stu-id="f4d38-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="f4d38-131">Vaya a una base de datos SQL y haga clic en **Toda la configuración** > **Soporte y solución de problemas** > **Información de rendimiento de consultas**.</span><span class="sxs-lookup"><span data-stu-id="f4d38-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Información de rendimiento de consultas][1]
   
    <span data-ttu-id="f4d38-133">Se abre la vista de las principales consultas y aparece la lista de las consultas principales que más CPU consumen.</span><span class="sxs-lookup"><span data-stu-id="f4d38-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="f4d38-134">Para más detalles, haga clic alrededor del gráfico.</span><span class="sxs-lookup"><span data-stu-id="f4d38-134">Click around the chart for details.</span></span><br><span data-ttu-id="f4d38-135">La línea superior muestra el porcentaje general de DTU de la base de datos, mientras que las barras muestran el porcentaje de CPU consumido por las consultas seleccionadas durante el intervalo seleccionado (por ejemplo, si se selecciona **Semana anterior** , cada barra representa un día).</span><span class="sxs-lookup"><span data-stu-id="f4d38-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![principales consultas][2]
   
    <span data-ttu-id="f4d38-137">La cuadrícula inferior representa información agregada para las consultas visibles.</span><span class="sxs-lookup"><span data-stu-id="f4d38-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="f4d38-138">Id. de consulta: identificador único de la consulta en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="f4d38-139">CPU por consulta durante el intervalo observable (depende de la función de agregación).</span><span class="sxs-lookup"><span data-stu-id="f4d38-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="f4d38-140">Duración por consulta (depende de la función de agregación).</span><span class="sxs-lookup"><span data-stu-id="f4d38-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="f4d38-141">Número total de ejecuciones para una consulta determinada.</span><span class="sxs-lookup"><span data-stu-id="f4d38-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="f4d38-142">Seleccione o anule la selección de las consultas individuales para incluirlas o excluirlas del gráfico mediante casillas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="f4d38-143">Si los datos se quedan desusados, haga clic en el botón **Actualizar** .</span><span class="sxs-lookup"><span data-stu-id="f4d38-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="f4d38-144">Puede usar controles deslizantes y botones de zoom para cambiar el intervalo de observación e investigar los picos: ![configuración](./media/sql-database-query-performance/zoom.png).</span><span class="sxs-lookup"><span data-stu-id="f4d38-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="f4d38-145">Opcionalmente, si desea una vista diferente, puede seleccionar la pestaña **Personalizado** y establecer:</span><span class="sxs-lookup"><span data-stu-id="f4d38-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="f4d38-146">Métrica (CPU, duración, recuento de ejecuciones)</span><span class="sxs-lookup"><span data-stu-id="f4d38-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="f4d38-147">Intervalo de tiempo (últimas 24 horas, semana anterior, mes anterior).</span><span class="sxs-lookup"><span data-stu-id="f4d38-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="f4d38-148">Número de consultas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-148">Number of queries.</span></span>
   * <span data-ttu-id="f4d38-149">Función de agregación.</span><span class="sxs-lookup"><span data-stu-id="f4d38-149">Aggregation function.</span></span>
     
     ![Configuración](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="f4d38-151">Visualización de los detalles de las consultas individuales</span><span class="sxs-lookup"><span data-stu-id="f4d38-151">Viewing individual query details</span></span>
<span data-ttu-id="f4d38-152">Para ver los detalles de una consulta:</span><span class="sxs-lookup"><span data-stu-id="f4d38-152">To view query details:</span></span>

1. <span data-ttu-id="f4d38-153">Haga clic en cualquiera de las consultas de la lista de las principales consultas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-153">Click any query in the list of top queries.</span></span>
   
    ![detalles](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="f4d38-155">Se abre la vista de detalles y el consumo de CPU, la duración y el recuento de ejecuciones de las consultas se desglosan por tiempo.</span><span class="sxs-lookup"><span data-stu-id="f4d38-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="f4d38-156">Para más detalles, haga clic alrededor del gráfico.</span><span class="sxs-lookup"><span data-stu-id="f4d38-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="f4d38-157">El gráfico superior muestra la línea con el porcentaje general de DTU de la base de datos, mientras que las barras son el porcentaje de CPU consumido por la consulta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="f4d38-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="f4d38-158">El segundo gráfico muestra la duración total por la consulta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="f4d38-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="f4d38-159">El gráfico inferior muestra el número total de ejecuciones por la consulta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="f4d38-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![detalles de consulta][3]
4. <span data-ttu-id="f4d38-161">Opcionalmente, use controles deslizantes, botones de zoom o haga clic en **Configuración** para personalizar la forma en que se muestran los datos de consulta o para seleccionar otro período.</span><span class="sxs-lookup"><span data-stu-id="f4d38-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="f4d38-162">Revisión de las principales consultas por duración</span><span class="sxs-lookup"><span data-stu-id="f4d38-162">Review top queries per duration</span></span>
<span data-ttu-id="f4d38-163">En la reciente actualización de Información de rendimiento de consultas, presentamos dos nuevas métricas que pueden ayudarle a identificar posibles cuellos de botella: duración y recuento de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="f4d38-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="f4d38-164">Las consultas de larga ejecución tienen el máximo potencial para bloquear recursos durante más tiempo, bloquear otros usuarios y limitar la escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="f4d38-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="f4d38-165">También son las mejores candidatas para la optimización.</span><span class="sxs-lookup"><span data-stu-id="f4d38-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="f4d38-166">Para identificar consultas de larga ejecución:</span><span class="sxs-lookup"><span data-stu-id="f4d38-166">To identify long running queries:</span></span>

1. <span data-ttu-id="f4d38-167">Abra la pestaña **Personalizado** en Información de rendimiento de consultas para la base de datos seleccionada</span><span class="sxs-lookup"><span data-stu-id="f4d38-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="f4d38-168">Cambie las métricas por **duración**</span><span class="sxs-lookup"><span data-stu-id="f4d38-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="f4d38-169">Seleccione el número de consultas y el intervalo de observación</span><span class="sxs-lookup"><span data-stu-id="f4d38-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="f4d38-170">Seleccione la función de agregación</span><span class="sxs-lookup"><span data-stu-id="f4d38-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="f4d38-171">**Sum** aumenta el tiempo de ejecución de todas las consultas durante todo el intervalo de observación.</span><span class="sxs-lookup"><span data-stu-id="f4d38-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="f4d38-172">**Max** busca consultas cuyo tiempo de ejecución era máximo en todo el intervalo de observación.</span><span class="sxs-lookup"><span data-stu-id="f4d38-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="f4d38-173">**Avg** busca el tiempo medio de ejecución de todas las ejecuciones de consulta y le muestra el límite de estos promedios.</span><span class="sxs-lookup"><span data-stu-id="f4d38-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![duración de la consulta][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="f4d38-175">Revisión de las principales consultas por recuento de ejecuciones</span><span class="sxs-lookup"><span data-stu-id="f4d38-175">Review top queries per execution count</span></span>
<span data-ttu-id="f4d38-176">Es posible que el elevado número de ejecuciones no afecte a la propia base de datos y el uso de recursos puede ser bajo, pero la aplicación general podría ralentizarse.</span><span class="sxs-lookup"><span data-stu-id="f4d38-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="f4d38-177">En algunos casos, un recuento de ejecuciones muy alto puede dar lugar al aumento de los ciclos de ida y vuelta de red.</span><span class="sxs-lookup"><span data-stu-id="f4d38-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="f4d38-178">Los ciclos de ida y vuelta afectan significativamente al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f4d38-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="f4d38-179">Están sujetos a la latencia de red y a la latencia del servidor auxiliar.</span><span class="sxs-lookup"><span data-stu-id="f4d38-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="f4d38-180">Por ejemplo, muchos sitios web controlados por datos tienen acceso en gran medida a la base de datos para cada solicitud de usuario.</span><span class="sxs-lookup"><span data-stu-id="f4d38-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="f4d38-181">Mientras la agrupación de conexiones ayuda, el mayor tráfico de red y la carga de procesamiento del servidor de bases de datos pueden afectar de forma negativa al rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f4d38-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="f4d38-182">La recomendación general es reducir al mínimo los ciclos de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="f4d38-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="f4d38-183">Para identificar consultas ejecutadas de forma habitual (“consultas fragmentadas”):</span><span class="sxs-lookup"><span data-stu-id="f4d38-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="f4d38-184">Abra la pestaña **Personalizado** en Información de rendimiento de consultas para la base de datos seleccionada</span><span class="sxs-lookup"><span data-stu-id="f4d38-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="f4d38-185">Cambie las métricas por **recuento de ejecuciones**</span><span class="sxs-lookup"><span data-stu-id="f4d38-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="f4d38-186">Seleccione el número de consultas y el intervalo de observación</span><span class="sxs-lookup"><span data-stu-id="f4d38-186">Select number of queries and observation interval</span></span>
   
    ![recuento de ejecuciones de la consulta][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="f4d38-188">Descripción de las anotaciones de ajuste del rendimiento</span><span class="sxs-lookup"><span data-stu-id="f4d38-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="f4d38-189">Al explorar su carga de trabajo en Información de rendimiento de consultas, puede que observe iconos con línea vertical en la parte superior del gráfico.</span><span class="sxs-lookup"><span data-stu-id="f4d38-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="f4d38-190">Estos iconos son anotaciones; representan el rendimiento que afecta a las acciones realizadas por el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="f4d38-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="f4d38-191">Al desplazar el mouse sobre la anotación, obtiene información básica relativa a la acción:</span><span class="sxs-lookup"><span data-stu-id="f4d38-191">By hovering annotation, you get basic information about the action:</span></span>

![anotación de la consulta][6]

<span data-ttu-id="f4d38-193">Si desea obtener más información o aplicar las recomendaciones del asesor, haga clic en el icono.</span><span class="sxs-lookup"><span data-stu-id="f4d38-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="f4d38-194">Se abrirán los detalles de la acción.</span><span class="sxs-lookup"><span data-stu-id="f4d38-194">It will open details of action.</span></span> <span data-ttu-id="f4d38-195">Si se trata de una recomendación activa, puede aplicarla inmediatamente mediante el comando.</span><span class="sxs-lookup"><span data-stu-id="f4d38-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![detalles de la anotación de la consulta][7]

### <a name="multiple-annotations"></a><span data-ttu-id="f4d38-197">Varias anotaciones.</span><span class="sxs-lookup"><span data-stu-id="f4d38-197">Multiple annotations.</span></span>
<span data-ttu-id="f4d38-198">Es posible que, debido al nivel de zoom, las anotaciones que están cerca unas de otras se contraigan en una.</span><span class="sxs-lookup"><span data-stu-id="f4d38-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="f4d38-199">Un icono especial representará este suceso y, al hacer clic en él, se abrirá una nueva hoja donde se mostrará una lista de las anotaciones agrupadas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="f4d38-200">La correlación de consultas y acciones de ajuste del rendimiento puede ayudar a comprender mejor la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f4d38-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="f4d38-201">Optimización de la configuración del almacén de consultas para obtener información de rendimiento de consultas</span><span class="sxs-lookup"><span data-stu-id="f4d38-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="f4d38-202">Durante el uso de información de rendimiento de consultas, puede que encuentre los siguientes mensajes del almacén de consultas:</span><span class="sxs-lookup"><span data-stu-id="f4d38-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="f4d38-203">"El Almacén de consultas no está configurado correctamente en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="f4d38-204">Haga clic aquí para más información".</span><span class="sxs-lookup"><span data-stu-id="f4d38-204">Click here to learn more."</span></span>
* <span data-ttu-id="f4d38-205">"El Almacén de consultas no está configurado correctamente en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="f4d38-206">Haga clic aquí para cambiar la configuración".</span><span class="sxs-lookup"><span data-stu-id="f4d38-206">Click here to change settings."</span></span> 

<span data-ttu-id="f4d38-207">Estos mensajes suelen aparecer cuando el almacén de consultas no puede recopilar datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="f4d38-208">El primer caso sucede si el Almacén de consultas está en estado de solo lectura y los parámetros están óptimamente establecidos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="f4d38-209">Para solucionarlo, puede aumentar el tamaño del Almacén de consultas o borrar el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![botón qds][8]

<span data-ttu-id="f4d38-211">El segundo caso sucede si el Almacén de consultas está desactivado o los parámetros no están óptimamente establecidos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="f4d38-212">Puede cambiar la directiva de retención y captura y habilitar el Almacén de consultas ejecutando los comandos que aparecen a continuación o directamente desde el portal:</span><span class="sxs-lookup"><span data-stu-id="f4d38-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![botón qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="f4d38-214">Directiva de retención y captura recomendada</span><span class="sxs-lookup"><span data-stu-id="f4d38-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="f4d38-215">Hay dos tipos de directivas de retención:</span><span class="sxs-lookup"><span data-stu-id="f4d38-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="f4d38-216">Basada en tamaño: si se establece en AUTO, los datos se borrarán automáticamente cuando el tamaño casi haya alcanzado el tamaño máximo.</span><span class="sxs-lookup"><span data-stu-id="f4d38-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="f4d38-217">Basada en tiempo: de forma predeterminada, estableceremos esta opción en 30 días, lo que significa que, si el Almacén de consultas se queda sin espacio, eliminará la información de consulta anterior a los 30 días.</span><span class="sxs-lookup"><span data-stu-id="f4d38-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="f4d38-218">La directiva de capturas se podría establecer como:</span><span class="sxs-lookup"><span data-stu-id="f4d38-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="f4d38-219">**Todas**: captura todas las consultas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="f4d38-220">**Automática**: se ignoran las consultas poco frecuentes y las consultas con una duración de ejecución y compilación insignificantes.</span><span class="sxs-lookup"><span data-stu-id="f4d38-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="f4d38-221">Los umbrales para la duración del tiempo de ejecución y de compilación y para el recuento de ejecuciones se determinan internamente.</span><span class="sxs-lookup"><span data-stu-id="f4d38-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="f4d38-222">Esta es la opción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f4d38-222">This is the default option.</span></span>
* <span data-ttu-id="f4d38-223">**Ninguna**: el Almacén de consultas deja de capturar nuevas consultas, pero las estadísticas en tiempo de ejecución de las consultas ya capturadas siguen recopilándose.</span><span class="sxs-lookup"><span data-stu-id="f4d38-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="f4d38-224">Se recomienda establecer todas las directivas en AUTO y la directiva de limpieza en 30 días:</span><span class="sxs-lookup"><span data-stu-id="f4d38-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="f4d38-225">Aumentar el tamaño del almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-225">Increase size of Query Store.</span></span> <span data-ttu-id="f4d38-226">Esto puede realizarse mediante la conexión a una base de datos y la emisión de la consulta siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4d38-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="f4d38-227">La aplicación de estos valores hará que finalmente el Almacén de consultas recopile nuevas consultas, pero, si no quiere esperar, puede borrar el Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4d38-228">Al ejecutar la consulta siguiente, se eliminará toda la información actual del Almacén de consultas.</span><span class="sxs-lookup"><span data-stu-id="f4d38-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="f4d38-229">Resumen</span><span class="sxs-lookup"><span data-stu-id="f4d38-229">Summary</span></span>
<span data-ttu-id="f4d38-230">Query Performance Insight le ayuda a comprender el impacto de la carga de trabajo de las consultas y su relación con el consumo de recursos de base de datos.</span><span class="sxs-lookup"><span data-stu-id="f4d38-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="f4d38-231">Con esta característica, conocerá las consultas que más consumen e identificará fácilmente las que deben corregirse antes de que conviertan en un problema.</span><span class="sxs-lookup"><span data-stu-id="f4d38-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4d38-232">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4d38-232">Next steps</span></span>
<span data-ttu-id="f4d38-233">Para recomendaciones adicionales sobre cómo mejorar el rendimiento de la base de datos SQL, haga clic en [Recomendaciones](sql-database-advisor.md) en la hoja **Información de rendimiento de consultas** .</span><span class="sxs-lookup"><span data-stu-id="f4d38-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

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

