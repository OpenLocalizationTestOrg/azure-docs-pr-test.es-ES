---
title: aaaResolve problemas de sesgo de datos mediante el uso de Azure Data Lake Tools para Visual Studio | Documentos de Microsoft
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
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="2d2f8-103">Resuelva los problemas de asimetría de datos con Herramientas de Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d2f8-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="2d2f8-104">¿Qué es la asimetría de datos?</span><span class="sxs-lookup"><span data-stu-id="2d2f8-104">What is data skew?</span></span>

<span data-ttu-id="2d2f8-105">En pocas palabras, una asimetría de datos es un valor sobrerrepresentado.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="2d2f8-106">Imagine que haya asignado a 50 examinadores de impuestos tooaudit impuestos, uno examinador para cada estado de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="2d2f8-107">Examinador de Wyoming Hello, porque no existe la población de hello es muy pequeña, tiene poco toodo.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="2d2f8-108">En California, sin embargo, Examinador de Hola se mantiene muy ocupado debido a la población grande del estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="2d2f8-109">![Ejemplo de problema de asimetría de datos](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="2d2f8-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="2d2f8-110">En nuestro escenario, datos de Hola se distribuyen entre todos los examinadores de impuestos, lo que significa que algunos examinadores deben trabajar más que otros.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="2d2f8-111">En su propio trabajo experimenta con frecuencia situaciones como este ejemplo de Hola Examinador de impuestos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="2d2f8-112">En términos más técnicos, un vértice obtiene mucho más datos que sus elementos del mismo nivel, una situación que hace que los vértices Hola funcione más Hola otras y que finalmente se ralentiza un trabajo completo.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="2d2f8-113">¿Qué es lo que es peor, trabajo Hola puede producir un error, porque podrían tener vértices, por ejemplo, una limitación de tiempo de ejecución de 5 horas y una limitación de 6 GB de memoria.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="2d2f8-114">Resolución de problemas de asimetría de datos</span><span class="sxs-lookup"><span data-stu-id="2d2f8-114">Resolving data-skew problems</span></span>

<span data-ttu-id="2d2f8-115">Las Herramientas de Azure Data Lake para Visual Studio pueden ayudar a detectar si el trabajo tiene un problema de asimetría de datos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="2d2f8-116">Si existe algún problema, puede resolverlo realizando soluciones hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="2d2f8-117">Solución 1: Mejorar la partición de tabla</span><span class="sxs-lookup"><span data-stu-id="2d2f8-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="2d2f8-118">Opción 1: Hola filtro sesgado clave-valor de antemano</span><span class="sxs-lookup"><span data-stu-id="2d2f8-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="2d2f8-119">Si no afecta a la lógica de negocios, puede filtrar valores de hello más frecuente de antemano.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="2d2f8-120">Por ejemplo, si hay mucha 000-000-000, en la columna GUID, no puede tooaggregate ese valor.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="2d2f8-121">Antes de agregado, puede escribir "WHERE GUID! ="000-000 000"" valor de alta frecuencia de toofilter Hola.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="2d2f8-122">Opción 2: Seleccionar una clave de partición o distribución diferente</span><span class="sxs-lookup"><span data-stu-id="2d2f8-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="2d2f8-123">Hola anterior ejemplo, si desea que la carga de trabajo de solo toocheck Hola auditoría fiscal todos sobre Hola país, puede mejorar la distribución de datos de hello seleccionando el número de Id. de hello como su clave.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="2d2f8-124">Seleccionar una partición diferente o una clave de distribución puede a veces distribuir datos hello más uniformemente, pero debe toomake seguro de que esta opción no afecta a la lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="2d2f8-125">Por ejemplo, suma de impuestos de toocalculate Hola para cada estado, es recomendable toodesignate _estado_ como clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="2d2f8-126">Si sigues tooexperience este problema, pruebe a usar la opción 3.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="2d2f8-127">Opción 3: Agregar más claves de partición o distribución</span><span class="sxs-lookup"><span data-stu-id="2d2f8-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="2d2f8-128">En lugar de usar solo _Estado_ como clave de partición, puede usar más de una clave para las particiones.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="2d2f8-129">Por ejemplo, considere la posibilidad de agregar _código postal_ como una partición adicional tooreduce clave de partición de datos, tamaños y distribuir más uniformemente los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="2d2f8-130">Opción 4: Usar la distribución round robin</span><span class="sxs-lookup"><span data-stu-id="2d2f8-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="2d2f8-131">Si no se encuentra una clave adecuada para la partición y distribución, puede intentar toouse distribución por turnos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="2d2f8-132">La distribución round robin trata por igual cada fila y la coloca de forma aleatoria en el depósito correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="2d2f8-133">datos de Hello obtiene distribuyen uniformemente, pero pierde la información de localidad, un inconveniente de que también se puede reducir el rendimiento de trabajo para algunas operaciones.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="2d2f8-134">Además, si está realizando clave sesgados hello las agregaciones de todos modos, se conservará el problema de hello sesgo de datos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="2d2f8-135">toolearn más información acerca de la distribución por turnos, vea hello U-SQL tabla distribuciones sección [CREATE TABLE (U-SQL): crear una tabla con esquema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="2d2f8-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="2d2f8-136">Solución 2: Mejorar el plan de consulta de Hola</span><span class="sxs-lookup"><span data-stu-id="2d2f8-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="2d2f8-137">Opción 1: Usar la instrucción CREATE STATISTICS de Hola</span><span class="sxs-lookup"><span data-stu-id="2d2f8-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="2d2f8-138">U-SQL proporciona la instrucción CREATE STATISTICS de hello en tablas.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="2d2f8-139">Esta instrucción da el optimizador de consultas de toohello de más información acerca de características de datos de hello, como la distribución de valor, que se almacenan en una tabla.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="2d2f8-140">Para la mayoría de las consultas, el optimizador de consultas de hello ya genera las estadísticas que necesita para un plan de consulta de alta calidad Hola.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="2d2f8-141">En ocasiones, puede que tenga tooimprove rendimiento de las consultas creando estadísticas adicionales con CREATE STATISTICS o modificando el diseño de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="2d2f8-142">Para obtener más información, vea hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="2d2f8-143">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2d2f8-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="2d2f8-144">La información de estadísticas no se actualiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="2d2f8-145">Si actualiza datos hello en una tabla sin volver a crear las estadísticas de hello, puede rechazar el rendimiento de las consultas Hola.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="2d2f8-146">Opción 2: usar SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="2d2f8-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="2d2f8-147">Si desea que los impuestos hello toosum para cada estado, debe usar Agrupar por estado, un método que no evita el problema de hello sesgo de datos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="2d2f8-148">Sin embargo, puede proporcionar una sugerencia de datos en su tooidentify consulta sesgo de datos en las claves para que el optimizador de hello puede preparar un plan de ejecución automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="2d2f8-149">Por lo general, puede establecer el parámetro hello como 0,5 y 1, con lo que significa que no mucho sesgo pesada significado sesgo y 1 de 0,5.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="2d2f8-150">Porque la sugerencia de hello afecta a la optimización de plan de ejecución para la instrucción actual de Hola y todas las instrucciones de nivel inferiores, estar seguro de sugerencia de hello tooadd antes de Hola posible había sesgado agregación key-wise.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="2d2f8-151">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2d2f8-151">Code example:</span></span>

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

### <a name="option-3-use-rowcount"></a><span data-ttu-id="2d2f8-152">Opción 3: Usar ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="2d2f8-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="2d2f8-153">Además tooSKEWFACTOR para específico de clave asimétrica unir los casos, si sabe que Hola otro conjunto de filas combinadas es pequeño, puede indicar el optimizador Hola agregando una sugerencia de recuento de filas en la instrucción de SQL U Hola antes de la combinación.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="2d2f8-154">De esta manera, el optimizador puede elegir un toohelp de estrategia de combinación difusión mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="2d2f8-155">Tenga en cuenta que recuento de filas no resuelve el problema de hello sesgo de datos, pero puede ofrecer cierta ayuda adicional.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="2d2f8-156">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2d2f8-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="2d2f8-157">Solución 3: Mejorar Combinador y reductor de hello definido por el usuario</span><span class="sxs-lookup"><span data-stu-id="2d2f8-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="2d2f8-158">En ocasiones, puede escribir un toodeal operador definido por el usuario con la lógica de proceso complicado y un reductor bien escrito y Combinador podrían mitigar un problema de sesgo de datos en algunos casos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="2d2f8-159">Opción 1: Utilizar un reductor recursivo si es posible</span><span class="sxs-lookup"><span data-stu-id="2d2f8-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="2d2f8-160">De forma predeterminada, el reductor definido por el usuario se ejecuta como modo no recursivo, lo que significa que el trabajo reducido para una clave se va a distribuir a un solo vértice.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="2d2f8-161">Pero si se sesga los datos, conjuntos de datos muy grandes de Hola podría se procesan en un solo vértice y ejecutar durante mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="2d2f8-162">rendimiento de tooimprove, puede agregar un atributo en su toorun de código toodefine reductor de modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="2d2f8-163">A continuación, conjuntos de datos muy grandes de hello pueda toomultiple distribuida vértices y ejecutar en paralelo, lo que acelera el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="2d2f8-164">toochange un toorecursive de reductor no recursivo, debe toomake seguro de que el algoritmo es asociativo.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="2d2f8-165">Por ejemplo, es asociativo a la suma de Hola y Hola median no es.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="2d2f8-166">También necesita toomake seguro de que Hola de entrada y salida para el reductor mantienen Hola mismo esquema.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="2d2f8-167">Atributo del reductor recursivo:</span><span class="sxs-lookup"><span data-stu-id="2d2f8-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="2d2f8-168">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2d2f8-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="2d2f8-169">Opción 2: Utilizar el modo de combinador de nivel de fila si es posible</span><span class="sxs-lookup"><span data-stu-id="2d2f8-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="2d2f8-170">Sugerencia de recuento de filas toohello similar para los casos de combinación concreta de clave asimétrica, modo de Combinador intenta toodistribute valor de clave asimétrica grandes conjuntos de toomultiple vértices para que el trabajo de hello puede ejecutarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="2d2f8-171">El modo de combinador no puede resolver los problemas de asimetría de datos, pero puede proporcionar ayuda adicional para grandes conjuntos de valores de claves asimétricas.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="2d2f8-172">De forma predeterminada, el modo de Combinador hello es completo, lo que significa que Hola deja el conjunto de filas y no se puede separar el conjunto de filas secundario.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="2d2f8-173">Establecer el modo de hello como izquierda o derecha/interna permite la combinación de nivel de fila.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="2d2f8-174">sistema de Hello separa los conjuntos de filas correspondientes de Hola y distribuye en varios vértices que se ejecutan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="2d2f8-175">Sin embargo, antes de configurar el modo de Combinador hello, tenga cuidado tooensure que Hola conjuntos de filas correspondientes se puede separar.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="2d2f8-176">ejemplo de Hola que sigue muestra un conjunto de filas izquierdo separados.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="2d2f8-177">Cada fila de salida depende de una sola fila de entrada de hello izquierda, y potencialmente depende de todas las filas de hello derecha con hello mismo valor de clave.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="2d2f8-178">Si establece el modo de Combinador hello como left, sistema de hello separa Hola enorme izquierda-conjunto de filas en las pequeñas y las asigna toomultiple vértices.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Ilustración del modo de combinador](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="2d2f8-180">Si establece el modo de hello Combinador incorrecto, combinación de hello es menos eficaz y resultados de hello podrían ser incorrectos.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="2d2f8-181">Atributos del modo de combinador:</span><span class="sxs-lookup"><span data-stu-id="2d2f8-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="2d2f8-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Cada fila de salida depende de una sola fila de entrada de hello izquierda (y potencialmente todas las filas de hello derecha con hello mismo valor de clave).</span><span class="sxs-lookup"><span data-stu-id="2d2f8-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="2d2f8-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): cada fila de salida depende de una sola fila de entrada de hello derecho (y potencialmente todas las filas de hello izquierda con hello mismo valor de clave).</span><span class="sxs-lookup"><span data-stu-id="2d2f8-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="2d2f8-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Cada fila de salida depende de una sola fila de entrada de izquierda Hola y Hola derecha con hello mismo valor.</span><span class="sxs-lookup"><span data-stu-id="2d2f8-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="2d2f8-185">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="2d2f8-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
