---
title: "Resolución de problemas de asimetría de datos mediante Herramientas de Azure Data Lake para Visual Studio | Microsoft Docs"
description: "Posibles soluciones para problemas de asimetría de datos mediante el uso de Herramientas de Azure Data Lake para Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 9b284ef33be4b935569fc368d81ddf040b2c2b7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="e251c-103">Resuelva los problemas de asimetría de datos con Herramientas de Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e251c-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="e251c-104">¿Qué es la asimetría de datos?</span><span class="sxs-lookup"><span data-stu-id="e251c-104">What is data skew?</span></span>

<span data-ttu-id="e251c-105">En pocas palabras, una asimetría de datos es un valor sobrerrepresentado.</span><span class="sxs-lookup"><span data-stu-id="e251c-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="e251c-106">Imagine que se han asignado 50 inspectores para auditar impuestos, un inspector para cada estado de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="e251c-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="e251c-107">El inspector de Wyoming tiene poco que hacer, porque la población es muy pequeña.</span><span class="sxs-lookup"><span data-stu-id="e251c-107">The Wyoming examiner, because the population there is small, has little to do.</span></span> <span data-ttu-id="e251c-108">En California, sin embargo, el inspector está muy ocupado porque ese estado está densamente poblado.</span><span class="sxs-lookup"><span data-stu-id="e251c-108">In California, however, the examiner is kept very busy because of the state's large population.</span></span>
    <span data-ttu-id="e251c-109">![Ejemplo de problema de asimetría de datos](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="e251c-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="e251c-110">En nuestro escenario, los datos se distribuyen de forma desigual entre los inspectores de impuestos, lo que significa que algunos inspectores deben trabajar más que otros.</span><span class="sxs-lookup"><span data-stu-id="e251c-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="e251c-111">Seguro que en su propio trabajo experimenta con frecuencia situaciones como el ejemplo del inspector de impuestos.</span><span class="sxs-lookup"><span data-stu-id="e251c-111">In your own job, you frequently experience situations like the tax-examiner example here.</span></span> <span data-ttu-id="e251c-112">En términos más técnicos, un vértice recibe mucho más datos que otros elementos de su mismo nivel, por lo que debe trabajar más que los demás y puede llegar a ralentizar un trabajo completo.</span><span class="sxs-lookup"><span data-stu-id="e251c-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span></span> <span data-ttu-id="e251c-113">Y, lo que es peor, el trabajo puede producir un error, porque los vértices podrían tener, por ejemplo, una limitación de tiempo de ejecución de 5 horas y una limitación de 6 GB de memoria.</span><span class="sxs-lookup"><span data-stu-id="e251c-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="e251c-114">Resolución de problemas de asimetría de datos</span><span class="sxs-lookup"><span data-stu-id="e251c-114">Resolving data-skew problems</span></span>

<span data-ttu-id="e251c-115">Las Herramientas de Azure Data Lake para Visual Studio pueden ayudar a detectar si el trabajo tiene un problema de asimetría de datos.</span><span class="sxs-lookup"><span data-stu-id="e251c-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="e251c-116">Si es así, puede resolverlo probando las soluciones de esta sección.</span><span class="sxs-lookup"><span data-stu-id="e251c-116">If a problem exists, you can resolve it by trying the solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="e251c-117">Solución 1: Mejorar la partición de tabla</span><span class="sxs-lookup"><span data-stu-id="e251c-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-the-skewed-key-value-in-advance"></a><span data-ttu-id="e251c-118">Opción 1: filtrar el valor de la clave asimétrica de antemano</span><span class="sxs-lookup"><span data-stu-id="e251c-118">Option 1: Filter the skewed key value in advance</span></span>

<span data-ttu-id="e251c-119">Si esto no afecta a su lógica de negocios, puede filtrar los valores más frecuentes de antemano.</span><span class="sxs-lookup"><span data-stu-id="e251c-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span></span> <span data-ttu-id="e251c-120">Por ejemplo, si hay muchos 000-000-000 en la columna GUID, puede optar por no agregar ese valor.</span><span class="sxs-lookup"><span data-stu-id="e251c-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span></span> <span data-ttu-id="e251c-121">Antes de agregarlo, puede escribir "WHERE GUID != “000-000-000”” para filtrar el valor de alta frecuencia.</span><span class="sxs-lookup"><span data-stu-id="e251c-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="e251c-122">Opción 2: Seleccionar una clave de partición o distribución diferente</span><span class="sxs-lookup"><span data-stu-id="e251c-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="e251c-123">En el ejemplo anterior, si solo desea comprobar la carga de trabajo de auditoría fiscal de todo el país, puede mejorar la distribución de datos seleccionando el número de identificación como su clave.</span><span class="sxs-lookup"><span data-stu-id="e251c-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span></span> <span data-ttu-id="e251c-124">A veces, si elige una clave de partición o distribución diferente, puede distribuir los datos de manera más uniforme, aunque debe asegurarse de que esta elección no afecta a su lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="e251c-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="e251c-125">Por ejemplo, para calcular la suma de impuestos para cada estado, puede designar _Estado_ como la clave de partición.</span><span class="sxs-lookup"><span data-stu-id="e251c-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span></span> <span data-ttu-id="e251c-126">Si sigue apareciendo el problema, pruebe a utilizar la opción 3.</span><span class="sxs-lookup"><span data-stu-id="e251c-126">If you continue to experience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="e251c-127">Opción 3: Agregar más claves de partición o distribución</span><span class="sxs-lookup"><span data-stu-id="e251c-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="e251c-128">En lugar de usar solo _Estado_ como clave de partición, puede usar más de una clave para las particiones.</span><span class="sxs-lookup"><span data-stu-id="e251c-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="e251c-129">Por ejemplo, considere la posibilidad de agregar _Código postal_ como una clave de partición adicional para reducir los tamaños de particiones de datos y distribuir más uniformemente los datos.</span><span class="sxs-lookup"><span data-stu-id="e251c-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="e251c-130">Opción 4: Usar la distribución round robin</span><span class="sxs-lookup"><span data-stu-id="e251c-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="e251c-131">Si no encuentra una clave adecuada para la partición y distribución, puede intentar usar la distribución round robin.</span><span class="sxs-lookup"><span data-stu-id="e251c-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span></span> <span data-ttu-id="e251c-132">La distribución round robin trata por igual cada fila y la coloca de forma aleatoria en el depósito correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e251c-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="e251c-133">En este caso, los datos se distribuyen de manera uniforme, pero pierden información de localidad, un inconveniente que puede reducir el rendimiento de trabajo en algunas operaciones.</span><span class="sxs-lookup"><span data-stu-id="e251c-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="e251c-134">Además, si está realizando una agregación para la clave asimétrica, el problema de asimetría persistirá de todos modos.</span><span class="sxs-lookup"><span data-stu-id="e251c-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span></span> <span data-ttu-id="e251c-135">Para obtener más información acerca de la distribución round robin, vea la sección U-SQL Table Distributions (Distribuciones de la tabla U-SQL) en [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch) (CREATE TABLE (U-SQL): Creación de una tabla con esquema).</span><span class="sxs-lookup"><span data-stu-id="e251c-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-the-query-plan"></a><span data-ttu-id="e251c-136">Solución 2: Mejorar el plan de consulta</span><span class="sxs-lookup"><span data-stu-id="e251c-136">Solution 2: Improve the query plan</span></span>

### <a name="option-1-use-the-create-statistics-statement"></a><span data-ttu-id="e251c-137">Opción 1: Usar la instrucción CREATE STATISTICS</span><span class="sxs-lookup"><span data-stu-id="e251c-137">Option 1: Use the CREATE STATISTICS statement</span></span>

<span data-ttu-id="e251c-138">U-SQL proporciona la instrucción CREATE STATISTICS en las tablas.</span><span class="sxs-lookup"><span data-stu-id="e251c-138">U-SQL provides the CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="e251c-139">Esta instrucción proporciona más información al optimizador de consultas sobre las características de los datos, como la distribución de los valores que se almacenan en una tabla.</span><span class="sxs-lookup"><span data-stu-id="e251c-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="e251c-140">Para la mayoría de las consultas, el optimizador de consultas genera ya las estadísticas necesarias para un plan de consulta de alta calidad.</span><span class="sxs-lookup"><span data-stu-id="e251c-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="e251c-141">En ocasiones, tendrá que mejorar el rendimiento de las consultas creando estadísticas adicionales con CREATE STATISTICS o modificando el diseño de la consulta.</span><span class="sxs-lookup"><span data-stu-id="e251c-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span></span> <span data-ttu-id="e251c-142">Para obtener más información, consulte la página [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx).</span><span class="sxs-lookup"><span data-stu-id="e251c-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="e251c-143">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="e251c-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="e251c-144">La información de estadísticas no se actualiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e251c-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="e251c-145">Si actualiza los datos de una tabla sin volver a crear las estadísticas, el rendimiento de las consultas puede verse reducido.</span><span class="sxs-lookup"><span data-stu-id="e251c-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="e251c-146">Opción 2: usar SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="e251c-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="e251c-147">Si desea sumar el impuesto de cada estado, debe usar GROUP BY estado, un método que no evita el problema de asimetría de datos.</span><span class="sxs-lookup"><span data-stu-id="e251c-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span></span> <span data-ttu-id="e251c-148">Sin embargo, puede proporcionar una sugerencia de datos en la consulta para identificar asimetrías de datos en las claves, de modo que el optimizador pueda optimizar el plan de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e251c-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="e251c-149">Por lo general, puede establecer el parámetro como 0,5 y 1; 0,5 significa una ligera asimetría, mientras que 1 significa una gran asimetría.</span><span class="sxs-lookup"><span data-stu-id="e251c-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="e251c-150">Dado que la sugerencia afecta a la optimización de plan de ejecución de la instrucción actual y todas las instrucciones de nivel inferiores, no olvide agregar la sugerencia antes de la agregación con posible asimetría en la clave.</span><span class="sxs-lookup"><span data-stu-id="e251c-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that the given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="e251c-151">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="e251c-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="e251c-152">Opción 3: Usar ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="e251c-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="e251c-153">Además de SKEWFACTOR, en casos concretos de combinación de clave asimétrica, si sabe que el otro conjunto de filas combinadas es pequeño, puede indicárselo al optimizador agregando la sugerencia ROWCOUNT en la instrucción U-SQL antes de JOIN.</span><span class="sxs-lookup"><span data-stu-id="e251c-153">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span></span> <span data-ttu-id="e251c-154">De esta manera, el optimizador puede elegir una estrategia de combinación de difusión para ayudar a mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e251c-154">This way, optimizer can choose a broadcast join strategy to help improve performance.</span></span> <span data-ttu-id="e251c-155">Tenga en cuenta que ROWCOUNT no resuelve el problema de simetría de datos, pero pueda ofrecer cierta ayuda adicional.</span><span class="sxs-lookup"><span data-stu-id="e251c-155">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="e251c-156">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="e251c-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information to determine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-the-user-defined-reducer-and-combiner"></a><span data-ttu-id="e251c-157">Solución 3: Mejorar el combinador y el reductor definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="e251c-157">Solution 3: Improve the user-defined reducer and combiner</span></span>

<span data-ttu-id="e251c-158">Es habitual que escriba un operador definido por el usuario para tratar con una lógica de procesos complicada, y un combinador y un reductor bien escritos pueden mitigar el problema de asimetría de datos en algunos casos.</span><span class="sxs-lookup"><span data-stu-id="e251c-158">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="e251c-159">Opción 1: Utilizar un reductor recursivo si es posible</span><span class="sxs-lookup"><span data-stu-id="e251c-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="e251c-160">De forma predeterminada, el reductor definido por el usuario se ejecuta como modo no recursivo, lo que significa que el trabajo reducido para una clave se va a distribuir a un solo vértice.</span><span class="sxs-lookup"><span data-stu-id="e251c-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="e251c-161">Pero si hay asimetría de datos, los conjuntos de datos muy grandes pueden procesarse en un solo vértice y tener un tiempo de ejecución muy largo.</span><span class="sxs-lookup"><span data-stu-id="e251c-161">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="e251c-162">Para mejorar el rendimiento, puede agregar un atributo a su código para definir que el reductor se ejecute en modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="e251c-162">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span></span> <span data-ttu-id="e251c-163">A continuación, los conjuntos de datos muy grandes se puede distribuir a varios vértices y ejecutarse en paralelo, lo que acelera el trabajo.</span><span class="sxs-lookup"><span data-stu-id="e251c-163">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="e251c-164">Para cambiar un reductor no recursivo a recursivo, debe asegurarse de que el algoritmo sea asociativo.</span><span class="sxs-lookup"><span data-stu-id="e251c-164">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span></span> <span data-ttu-id="e251c-165">Por ejemplo, una suma es asociativa, mientras que una media no lo es.</span><span class="sxs-lookup"><span data-stu-id="e251c-165">For example, the sum is associative, and the median is not.</span></span> <span data-ttu-id="e251c-166">Además, debe asegurarse de que la entrada y la salida del reductor mantengan el mismo esquema.</span><span class="sxs-lookup"><span data-stu-id="e251c-166">You also need to make sure that the input and output for reducer keep the same schema.</span></span>

<span data-ttu-id="e251c-167">Atributo del reductor recursivo:</span><span class="sxs-lookup"><span data-stu-id="e251c-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="e251c-168">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="e251c-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="e251c-169">Opción 2: Utilizar el modo de combinador de nivel de fila si es posible</span><span class="sxs-lookup"><span data-stu-id="e251c-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="e251c-170">De forma similar a la sugerencia ROWCOUNT para casos específicos de combinación de claves asimétricas, el modo de combinador intenta distribuir el enorme conjunto de valores de claves asimétricas en varios vértices para que el trabajo se puede ejecutar simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="e251c-170">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span></span> <span data-ttu-id="e251c-171">El modo de combinador no puede resolver los problemas de asimetría de datos, pero puede proporcionar ayuda adicional para grandes conjuntos de valores de claves asimétricas.</span><span class="sxs-lookup"><span data-stu-id="e251c-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="e251c-172">De forma predeterminada, el modo de combinador es Full, lo que significa que el conjunto de filas izquierdo y el derecho no se pueden dividir.</span><span class="sxs-lookup"><span data-stu-id="e251c-172">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span></span> <span data-ttu-id="e251c-173">Establecer el modo como izquierda o derecha/interior permite la combinación de nivel de fila.</span><span class="sxs-lookup"><span data-stu-id="e251c-173">Setting the mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="e251c-174">El sistema separa los conjuntos de filas correspondientes y los distribuye en varios vértices que se ejecutan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="e251c-174">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="e251c-175">Sin embargo, antes de configurar el modo de combinador, debe tener cuidado y asegurarse de que se puede dividir el conjunto de filas correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e251c-175">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span></span>

<span data-ttu-id="e251c-176">El ejemplo siguiente muestra un conjunto de filas izquierdo separado.</span><span class="sxs-lookup"><span data-stu-id="e251c-176">The example that follows shows a separated left row set.</span></span> <span data-ttu-id="e251c-177">Cada fila de salida depende de una sola fila de entrada de la izquierda y, potencialmente, de todas las filas de la derecha con el mismo valor de clave.</span><span class="sxs-lookup"><span data-stu-id="e251c-177">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span></span> <span data-ttu-id="e251c-178">Si establece el modo de combinador como izquierdo, el sistema dividirá el enorme conjunto de filas izquierdo en otros más pequeños y los asignará a varios vértices.</span><span class="sxs-lookup"><span data-stu-id="e251c-178">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span></span>

![Ilustración del modo de combinador](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="e251c-180">Si establece un modo de combinador incorrecto, la combinación es menos eficaz y los resultados podrían ser incorrectos.</span><span class="sxs-lookup"><span data-stu-id="e251c-180">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span></span>

<span data-ttu-id="e251c-181">Atributos del modo de combinador:</span><span class="sxs-lookup"><span data-stu-id="e251c-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all the input rows from left and right with the same key value.

- <span data-ttu-id="e251c-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): cada fila de salida depende de una sola fila de entrada de la izquierda (y potencialmente de todas las filas de la derecha con el mismo valor de clave).</span><span class="sxs-lookup"><span data-stu-id="e251c-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span></span>

- <span data-ttu-id="e251c-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): cada fila de salida depende de una sola fila de entrada de la derecha (y potencialmente de todas las filas de la izquierda con el mismo valor de clave).</span><span class="sxs-lookup"><span data-stu-id="e251c-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span></span>

- <span data-ttu-id="e251c-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): cada fila de salida depende de una sola fila de entrada de la izquierda y la derecha con el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="e251c-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span></span>

<span data-ttu-id="e251c-185">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="e251c-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
