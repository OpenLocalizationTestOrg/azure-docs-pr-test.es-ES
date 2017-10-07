---
title: "tecnologías de base de datos de SQL en memoria aaaAzure | Documentos de Microsoft"
description: "Las tecnologías de base de datos de SQL en memoria Azure mejoran considerablemente el rendimiento Hola de transaccional y cargas de trabajo de análisis. Obtenga información acerca de cómo tootake aprovechar estas tecnologías."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="a1e7f-104">Optimización del rendimiento mediante las tecnologías en memoria de SQL Database</span><span class="sxs-lookup"><span data-stu-id="a1e7f-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="a1e7f-105">Mediante el uso de tecnologías en memoria en Azure SQL Database, puede lograr mejoras de rendimiento con diversas cargas de trabajo: transaccionales (procesamiento de transacciones en línea [OLTP]), analíticas (procesamiento analítico en línea [OLAP]) y mixtas (procesamiento analítico y transaccional híbrido [HTAP]).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="a1e7f-106">Causa de Hola más eficiente de las consultas y procesamiento de transacciones, tecnologías en memoria también le ayudarán a tooreduce costo.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="a1e7f-107">Normalmente no es necesario hello tooupgrade tarifa de mejoras de rendimiento de tooachieve de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="a1e7f-108">En algunos casos, es posible que incluso pueda reducir Hola tarifa, mientras se sigue viendo mejoras de rendimiento con tecnologías en memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="a1e7f-109">Estos son dos ejemplos de cómo OLTP en memoria ayudó a toosignificantly a mejorar el rendimiento:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="a1e7f-110">Mediante el uso de OLTP en memoria, [quórum Business Solutions era capaz de toodouble la carga de trabajo mientras mejoran la Dtu en un 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="a1e7f-111">DTU significa *Unidad de transmisión de datos*, e incluye una medida del consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="a1e7f-112">Hello vídeo siguiente muestra mejora significativa del consumo de recursos con una carga de trabajo de ejemplo: [OLTP en memoria en el vídeo para la base de datos de SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="a1e7f-113">Para obtener más información, consulte el blog de hello: [OLTP en memoria en la entrada de Blog de base de datos de SQL de Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="a1e7f-114">Tecnologías en memoria están disponibles en todas las bases de datos de nivel Premium de hello, incluidas bases de datos en grupos elásticos Premium.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="a1e7f-115">Hello vídeo siguiente explica posibles mejoras de rendimiento con tecnologías en memoria en la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="a1e7f-116">Recuerde que la ganancia de rendimiento de Hola que siempre verá depende de muchos factores, como la naturaleza de Hola de carga de trabajo de Hola y de datos, el patrón de acceso de base de datos de hello y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="a1e7f-117">La base de datos de SQL Azure tiene Hola después de tecnologías en memoria:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="a1e7f-118">*OLTP en memoria* aumenta el rendimiento y reduce la latencia del procesamiento de transacciones.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="a1e7f-119">Estas son las situaciones en las que se obtienen ventajas con OLTP en memoria: procesamiento de transacciones de alto rendimiento, como operaciones comerciales y juegos, ingesta de datos de eventos o dispositivos de IoT, almacenamiento en caché, carga de datos y escenarios de tablas temporales y variables de tablas.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="a1e7f-120">*Índices de almacén de columnas clúster* reducen el consumo de almacenamiento (arriba too10 veces) y mejorar el rendimiento de las consultas de informes y análisis.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="a1e7f-121">Puede utilizarlo con las tablas de hechos en su toofit de los puestos de datos más datos en la base de datos y mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="a1e7f-122">Además, puede utilizarlo con datos históricos en la base de datos operativa tooarchive y ser capaz de tooquery too10 horas más datos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="a1e7f-123">*Los índices no agrupados* para obtener ayuda HTAP toogain información en tiempo real sobre su empresa mediante la consulta Hola operativa base de datos directamente, sin Hola necesidad toorun costoso extracción, transformación y el proceso de carga (ETL) y espere para toobe de almacenamiento de datos de hello rellena.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="a1e7f-124">Índices no agrupados permiten una ejecución muy rápida de las consultas de análisis en la base de datos OLTP hello, al tiempo que reduce el impacto de hello en la carga de trabajo operativa Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="a1e7f-125">También puede tener la combinación de Hola de una tabla con optimización para memoria con un índice de almacén.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="a1e7f-126">Esta combinación le permite tooperform muy rápido procesamiento de transacciones y demasiado*simultáneamente* análisis de ejecución consulta a muy rápidamente en hello mismo datos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="a1e7f-127">Los índices de almacén de columnas y OLTP en memoria han formado parte del producto de SQL Server de Hola desde 2012 y 2014, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="a1e7f-128">Base de datos SQL de Azure y SQL Server comparten Hola misma implementación de tecnologías en memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="a1e7f-129">A partir de ahora, las nuevas funciones para estas tecnologías se publican primero en Azure SQL Database y después, en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="a1e7f-130">En este tema se describe los aspectos de los índices de OLTP en memoria y almacén de columnas que están tooAzure específico de base de datos SQL y también incluye ejemplos:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="a1e7f-131">Podrá ver impacto Hola de estas tecnologías en límites de tamaño de almacenamiento y los datos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="a1e7f-132">Podrá ver cómo toomanage Hola movimiento de bases de datos que usan estas tecnologías entre Hola diferente niveles de precios.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="a1e7f-133">Podrá ver dos ejemplos que ilustran el uso de Hola de OLTP en memoria, así como los índices de almacén de columnas de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="a1e7f-134">Vea Hola siguientes recursos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-134">See hello following resources for more information.</span></span>

<span data-ttu-id="a1e7f-135">Obtener información detallada acerca de las tecnologías de hello:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="a1e7f-136">[Información general de OLTP en memoria y escenarios de uso](https://msdn.microsoft.com/library/mt774593.aspx) (incluye referencias toocustomer casos prácticos y tooget información iniciado)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="a1e7f-137">Documentación de In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="a1e7f-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="a1e7f-138">Descripción de los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="a1e7f-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="a1e7f-139">Procesamiento analítico y transaccional híbrido (HTAP), también conocido como [análisis operativo en tiempo real](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="a1e7f-140">Un texto elemental sobre rápido en OLTP en memoria: [inicio rápido 1: tecnologías de OLTP en memoria para el rendimiento de T-SQL con mayor rapidez](http://msdn.microsoft.com/library/mt694156.aspx) (empezar a otro artículo toohelp)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="a1e7f-141">Vídeos en profundidad acerca de las tecnologías de hello:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="a1e7f-142">[OLTP en memoria en la base de datos de SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (que contiene una demostración de rendimiento ventajas y los pasos tooreproduce estos resultados usted mismo)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="a1e7f-143">Vídeos OLTP en memoria: ¿Qué es/cómo y cuándo toouse,</span><span class="sxs-lookup"><span data-stu-id="a1e7f-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- <span data-ttu-id="a1e7f-144">[Columnstore Index: In-Memory Analytics Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/) (Índice de almacén de columnas: vídeos sobre análisis en memoria de Ignite 2016)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-144">[Columnstore Index: In-Memory Analytics Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)</span></span>

## <a name="storage-and-data-size"></a><span data-ttu-id="a1e7f-145">Almacenamiento y tamaño de datos</span><span class="sxs-lookup"><span data-stu-id="a1e7f-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="a1e7f-146">Límite de almacenamiento y tamaño de datos para OLTP en memoria</span><span class="sxs-lookup"><span data-stu-id="a1e7f-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="a1e7f-147">OLTP en memoria incluye tablas con optimización de memoria, que se usan para almacenar los datos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="a1e7f-148">Estas tablas forman toofit necesario en la memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="a1e7f-149">Dado que administra la memoria directamente en hello servicio de base de datos SQL, tenemos concepto Hola de una cuota para los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="a1e7f-150">Esta idea es que se hace referencia tooas *almacenamiento de OLTP en memoria*.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="a1e7f-151">Cada plan de tarifa de grupo elástico y de base de datos independiente admitido incluye una cantidad determinada de almacenamiento de OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="a1e7f-152">En tiempo de Hola de escritura, obtendrá un gigabyte de almacenamiento por cada 125 unidades de transacción de base de datos (Dtu) o la base de datos elástica unidades de transacción (Edtu).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="a1e7f-153">Hola [niveles de servicio de base de datos SQL](sql-database-service-tiers.md) artículo tiene lista oficial de Hola de almacenamiento de OLTP en memoria de Hola que está disponible para cada una de las base de datos independiente y nivel de precios de grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="a1e7f-154">Hola siguiendo el recuento de elementos hacia su límite de almacenamiento de OLTP en memoria:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="a1e7f-155">Las filas de datos de usuarios activos en tablas con optimización de memoria y variables de tabla.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="a1e7f-156">Tenga en cuenta que las versiones de fila anteriores no cuentan para el límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="a1e7f-157">Los índices de tablas con optimización de memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="a1e7f-158">La sobrecarga operacional de operaciones ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="a1e7f-159">Si alcanza el límite de hello, recibirá un error fuera de cuota y ya no es capaz de tooinsert o actualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="a1e7f-160">toomitigate este error, elimine datos o aumente Hola nivel de base de datos de Hola o un grupo de precios.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="a1e7f-161">Para obtener más información acerca de cómo supervisar la utilización de almacenamiento de OLTP en memoria y la configuración de alertas cuando se alcance casi cap hello, consulte [almacenamiento en memoria de Monitor](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="a1e7f-162">Acerca de los grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="a1e7f-162">About elastic pools</span></span>

<span data-ttu-id="a1e7f-163">Con grupos elásticos, Hola almacenamiento de OLTP en memoria se comparte entre todas las bases de datos en bloque de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="a1e7f-164">Por lo tanto, el uso de hello en una base de datos puede afectar a otras bases de datos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="a1e7f-165">Existen dos formas de mitigar este problema:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="a1e7f-166">Configurar un Max-eDTU para bases de datos que es menor que el número de eDTU de Hola para grupo de Hola como un todo.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="a1e7f-167">Este valor máximo limita la utilización del almacenamiento de OLTP en memoria de hello, en cualquier base de datos en el grupo de hello, tamaño de toohello que corresponde el número de eDTU de toohello.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="a1e7f-168">Configurar un valor de eDTU mín. que sea mayor que 0.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="a1e7f-169">Este mínimo garantiza que cada base de datos en bloque de hello tiene cantidad Hola del almacenamiento de OLTP en memoria disponible que corresponde toohello habían configurado Min eDTU.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="a1e7f-170">Almacenamiento y tamaño de datos para los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="a1e7f-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="a1e7f-171">Índices de almacén de columnas no son necesario toofit en la memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="a1e7f-172">Por lo tanto, Hola solo límite en el tamaño de Hola de índices de hello es el tamaño de base de datos total máximo de hello, que se documenta en hello [niveles de servicio de base de datos SQL](sql-database-service-tiers.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="a1e7f-173">Cuando se utilicen índices de almacén de columnas agrupado, compresión de columna se utiliza para el almacenamiento de tabla base Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="a1e7f-174">Esta compresión puede reducir significativamente el espacio de almacenamiento de información de Hola de los datos de usuario, lo que significa que caben más datos en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="a1e7f-175">Y compresión de hello puede aumentarse aún más con [compresión de archivo columna](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="a1e7f-176">cantidad de Hola de compresión que se puede lograr depende de naturaleza Hola de datos de hello, pero la compresión 10 veces hello no es raro que.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="a1e7f-177">Por ejemplo, si tiene una base de datos con un tamaño máximo de 1 terabyte (TB) y logran una compresión de hello 10 veces mediante el uso de índices de almacén de columnas, puede incluir un total de 10 TB de datos de usuario de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="a1e7f-178">Cuando utiliza los índices no agrupados, tabla de base de hello todavía se almacena en formato de almacén de filas tradicionales de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="a1e7f-179">Por lo tanto, no es tan grande como con índices de almacén de columnas agrupado Hola ahorro de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="a1e7f-180">Sin embargo, si desea reemplazar un número de índices no clúster tradicionales con un índice de almacén de columnas único, todavía puede ver un ahorro general en el espacio de almacenamiento de información de hello para la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="a1e7f-181">Movimiento de bases de datos que usan tecnologías en memoria entre planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="a1e7f-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="a1e7f-182">Hay nunca las incompatibilidades u otros problemas al actualizar tooa superior tarifa, como de tooPremium estándar.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="a1e7f-183">solo aumentan los recursos y la funcionalidad disponible Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="a1e7f-184">Pero instalar versiones anteriores Hola tarifa puede repercutir negativamente en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="a1e7f-185">impacto de Hello es especialmente aparente cuando degrade desde tooStandard Premium o Basic cuando la base de datos contiene objetos de OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="a1e7f-186">Tablas optimizadas en memoria e índices de almacén de columnas, no están disponibles después de la degradación de hello (aunque sigan siendo visibles).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="a1e7f-187">Hola mismas consideraciones se aplican al bajar la Hola tarifa de un grupo elástico, o mover una base de datos con tecnologías en memoria, en un estándar o básico grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="a1e7f-188">In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="a1e7f-188">In-Memory OLTP</span></span>

<span data-ttu-id="a1e7f-189">*Degradar tooBasic/Standard*: OLTP en memoria no se admite en bases de datos de hello nivel estándar o básico.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="a1e7f-190">Además, no es posible toomove una base de datos que tiene cualquier toohello de objetos de OLTP en memoria nivel estándar o básico.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="a1e7f-191">Antes de degradar la base de datos de hello tooStandard/Basic, quite todas las tablas optimizadas en memoria y tipos de tabla, así como todos los módulos T-SQL compilados de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="a1e7f-192">No hay un mecanismo de programación toounderstand si una base de datos es compatible con OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="a1e7f-193">Puede ejecutar Hola después de consulta de Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="a1e7f-194">Si consulta Hola devuelve **1**, OLTP en memoria se admite en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="a1e7f-195">*Degradar de nivel inferior de Premium de tooa*: datos en tablas optimizadas en memoria deben caber dentro del almacenamiento de OLTP en memoria de Hola que está asociado con hello tarifa de base de datos de Hola o está disponible en el grupo elástico Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="a1e7f-196">Si intente hello toolower tarifa o mover la base de datos de hello en un grupo que no tiene suficiente espacio disponible de OLTP en memoria, se produce un error en la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="a1e7f-197">Índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="a1e7f-197">Columnstore indexes</span></span>

<span data-ttu-id="a1e7f-198">*Degradar tooBasic o estándar*: los índices se admiten únicamente en el nivel de precios Premium hello y no en el almacén de columnas Hola niveles estándar o básico.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="a1e7f-199">Cuando degrade la base de datos tooStandard o Basic, el índice de almacén de columnas no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="a1e7f-200">sistema de Hello mantiene el índice de almacén de columnas, pero nunca aprovecha el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="a1e7f-201">Si más tarde actualiza tooPremium atrás, el índice de almacén de columnas es toobe inmediatamente listo aprovechado de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="a1e7f-202">Si tiene una **agrupado** índice de almacén de columnas, toda la tabla Hola deja de estar disponible después de la degradación de la capa.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="a1e7f-203">Por lo tanto, se recomienda quitar todas *agrupado* antes de degradar la base de datos por debajo del nivel Premium de Hola de índices de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="a1e7f-204">*Degradar de nivel inferior de Premium de tooa*: esta degradación se realiza correctamente si la base de datos completa de hello quepa dentro de tamaño de base de datos máximo de hello para el nivel de precios de destino de hello, o dentro del almacenamiento disponible de hello en grupo elástico de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="a1e7f-205">No hay ningún impacto específico de índices de almacén de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="a1e7f-206">1. Instalar el ejemplo de Hola a OLTP en memoria</span><span class="sxs-lookup"><span data-stu-id="a1e7f-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="a1e7f-207">Puede crear base de datos de ejemplo de Hola AdventureWorksLT con unos pocos clics en hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a1e7f-208">A continuación, hello en esta sección se explica cómo puede enriquecer la base de datos AdventureWorksLT con objetos de OLTP en memoria y mostrar las ventajas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="a1e7f-209">Si desea ver una demostración más simple, pero más atractiva visualmente, del rendimiento de OLTP en memoria, consulte:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="a1e7f-210">Versión: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="a1e7f-211">Código fuente: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="a1e7f-212">Pasos de instalación</span><span class="sxs-lookup"><span data-stu-id="a1e7f-212">Installation steps</span></span>

1. <span data-ttu-id="a1e7f-213">Hola [portal de Azure](https://portal.azure.com/), crear una base de datos Premium en un servidor.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="a1e7f-214">Conjunto hello **origen** toohello datos de ejemplo AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="a1e7f-215">Para obtener instrucciones detalladas, consulte [Creación de la primera Base de datos SQL de Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="a1e7f-216">Conectar la base de datos de toohello con SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="a1e7f-217">Hola copia [secuencia de comandos de Transact-SQL de OLTP en memoria](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="a1e7f-218">Hola script T-SQL crea Hola objetos necesarios en memoria Hola datos de ejemplo AdventureWorksLT que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="a1e7f-219">Pegue el script de T-SQL de hello en SSMS y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="a1e7f-220">Hola `MEMORY_OPTIMIZED = ON` instrucciones CREATE TABLE, cláusula son cruciales.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="a1e7f-221">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="a1e7f-222">Error 40536</span><span class="sxs-lookup"><span data-stu-id="a1e7f-222">Error 40536</span></span>


<span data-ttu-id="a1e7f-223">Si recibe el error 40536 al ejecutar script de Hola T-SQL, ejecute hello después tooverify de script de T-SQL si admite la base de datos de hello en memoria:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="a1e7f-224">Un resultado de **0** significa que no se admite en memoria, mientras que un resultado de **1** significa que se admite.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="a1e7f-225">problema de hello toodiagnose, asegurarse de esa base de datos de hello está en nivel de servicio Premium de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="a1e7f-226">Acerca de hello creó elementos optimizadas en memoria</span><span class="sxs-lookup"><span data-stu-id="a1e7f-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="a1e7f-227">**Tablas**: ejemplo de Hola contiene hello las tablas optimizadas en memoria siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="a1e7f-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="a1e7f-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="a1e7f-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="a1e7f-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="a1e7f-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="a1e7f-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="a1e7f-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="a1e7f-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="a1e7f-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="a1e7f-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="a1e7f-233">Puede inspeccionar las tablas optimizadas en memoria a través de hello **Explorador de objetos** en SSMS.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="a1e7f-234">Haga clic con el botón derecho en **Tablas** > **Filtro** > **Configuración de filtro** > **Con optimización para memoria**.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="a1e7f-235">valor de Hello es igual a 1.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-235">hello value equals 1.</span></span>


<span data-ttu-id="a1e7f-236">O bien, puede consultar vistas de catálogo de hello, como:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="a1e7f-237">**Procedimiento almacenado compilado de forma nativa**: puede inspeccionar SalesLT.usp_InsertSalesOrder_inmem mediante una consulta de la vista de catálogo:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="a1e7f-238">Ejecutar la carga de trabajo OLTP de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="a1e7f-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="a1e7f-239">Hola la única diferencia entre Hola siguiendo dos *procedimientos almacenados* es que el primer procedimiento de hello usa versiones optimizadas en memoria de tablas de hello, mientras Hola segundo procedimiento usa las tablas de hello normales en disco:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="a1e7f-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="a1e7f-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="a1e7f-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="a1e7f-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="a1e7f-242">En esta sección, verá cómo Hola práctica toouse **ostress.exe** tooexecute utilidad Hola dos procedimientos almacenados en los niveles de estrés.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="a1e7f-243">Puede comparar cuánto tiempo tarda Hola dos esfuerzo ejecuciones toofinish.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="a1e7f-244">Cuando se ejecuta ostress.exe, se recomienda pasar valores de parámetro diseñados para los dos procedimientos siguientes de Hola:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="a1e7f-245">Ejecute un gran número de conexiones simultáneas, mediante el uso de -n100.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="a1e7f-246">Haga que cada conexión se repita en bucle cientos de veces, mediante el uso de -r500.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="a1e7f-247">Sin embargo, conviene toostart con valores mucho más pequeños como - tooensure n10 y - r50 que todo funciona.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="a1e7f-248">Script para ostress.exe</span><span class="sxs-lookup"><span data-stu-id="a1e7f-248">Script for ostress.exe</span></span>


<span data-ttu-id="a1e7f-249">Esta sección muestra la secuencia de comandos de T-SQL de Hola que se incrusta en la línea de comandos ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="a1e7f-250">script de Hola usa elementos creados por hello script T-SQL que instaló con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="a1e7f-251">Hello secuencia de comandos siguiente inserta un pedido de ventas de ejemplo con cinco elementos de línea siguiente Hola optimizadas en memoria *tablas*:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="a1e7f-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="a1e7f-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="a1e7f-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="a1e7f-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="a1e7f-254">Hola toomake *_ondisk* versión de Hola anterior script T-SQL para ostress.exe, podría reemplazar las apariciones de hello *_inmem* substring con *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="a1e7f-255">Estos reemplazos afectan a los nombres de Hola de tablas y procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="a1e7f-256">Instalación de ostress y utilidades de RML</span><span class="sxs-lookup"><span data-stu-id="a1e7f-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="a1e7f-257">Idealmente, debería planear toorun ostress.exe en una máquina virtual (VM) de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="a1e7f-258">Debe crear un [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) Hola misma región geográfica Azure donde reside la base de datos AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="a1e7f-259">Pero puede ejecutar si lo desea ostress.exe en el equipo portátil.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="a1e7f-260">Hola VM o en cualquier host, elija, instalar utilidades de lenguaje de marcado de reproducción (RML) de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="a1e7f-261">Utilidades de Hello incluyen ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="a1e7f-262">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-262">For more information, see:</span></span>
- <span data-ttu-id="a1e7f-263">Hola ostress.exe discusión en [base de datos de ejemplo para OLTP en memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="a1e7f-264">[Base de datos de ejemplo para OLTP en memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="a1e7f-265">Hola [blog para la instalación de ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="a1e7f-266">Ejecute hello *_inmem* efectuar una carga de trabajo de esfuerzo en primer lugar</span><span class="sxs-lookup"><span data-stu-id="a1e7f-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="a1e7f-267">Puede usar un *RML Cmd Prompt* ventana toorun la línea de comandos ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="a1e7f-268">parámetros de línea de comandos de Hello directa ostress para:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="a1e7f-269">Ejecutar 100 conexiones simultáneamente (-n100).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="a1e7f-270">Dispone de cada conexión ejecutar script de Hola T-SQL 50 veces (-r50).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="a1e7f-271">Hola de toorun delante de la línea de comandos de ostress.exe:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="a1e7f-272">Restablecer contenido de datos de base de datos de hello ejecutando Hola siguiente comando en SSMS, toodelete todos los datos de Hola que fuera insertados por todas las ejecuciones anteriores:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="a1e7f-273">Copiar texto hello de hello anterior ostress.exe línea de comandos tooyour Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="a1e7f-274">Reemplace hello `<placeholders>` para hello parámetros -S - U -P -d con hello corregir valores reales.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="a1e7f-275">Ejecute la línea de comandos modificada en una ventana del símbolo del sistema de RML.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="a1e7f-276">El resultado es una duración</span><span class="sxs-lookup"><span data-stu-id="a1e7f-276">Result is a duration</span></span>


<span data-ttu-id="a1e7f-277">Cuando finaliza el ostress.exe, escribe Hola duración de la ejecución como su última línea de salida en la ventana de hello RML Cmd.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="a1e7f-278">Por ejemplo, una ejecución de prueba más corta duró aproximadamente 1,5 minutos:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="a1e7f-279">Restablezca y edite *_ondisk* y, después, vuelva a ejecutarlo</span><span class="sxs-lookup"><span data-stu-id="a1e7f-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="a1e7f-280">Una vez haya resultado Hola Hola *_inmem* ejecutar, lleve a cabo Hola siguiendo los pasos para hello *_ondisk* ejecutar:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="a1e7f-281">Restablecer la base de datos de hello ejecutando Hola siguiente comando en SSMS toodelete todos los datos de Hola que fuera insertados por hello anterior ejecutar:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="a1e7f-282">Editar la línea de comandos de hello ostress.exe tooreplace todos los *_inmem* con *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="a1e7f-283">Vuelva a ejecutar ostress.exe para hello por segunda vez y capturar los resultados de la duración de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="a1e7f-284">Restablecer de nuevo, base de datos de hello (de forma responsable eliminación cuál puede ser una gran cantidad de datos de prueba).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="a1e7f-285">Resultados de la comparación esperados</span><span class="sxs-lookup"><span data-stu-id="a1e7f-285">Expected comparison results</span></span>

<span data-ttu-id="a1e7f-286">Nuestras pruebas en memoria han demostrado que el rendimiento mejorado gracias a **nueve veces** para esta carga de trabajo simplista, con ostress se ejecuta en una máquina virtual de Azure en Hola misma región de Azure como base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="a1e7f-287">2. Instalar el ejemplo de Hola a análisis en memoria</span><span class="sxs-lookup"><span data-stu-id="a1e7f-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="a1e7f-288">En esta sección, comparar Hola E/S y los resultados de las estadísticas cuando se usa un índice de almacén frente a un índice de árbol b tradicional.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="a1e7f-289">Para realizar análisis en tiempo real en una carga de trabajo OLTP, suele ser mejor toouse un índice no clúster de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="a1e7f-290">Para obtener más información, consulte [Guía de índices de almacén de columnas](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1e7f-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="a1e7f-291">Preparar la prueba de análisis de almacén de columnas de Hola</span><span class="sxs-lookup"><span data-stu-id="a1e7f-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="a1e7f-292">Usar hello toocreate portal Azure una base de datos AdventureWorksLT actualizada de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="a1e7f-293">Use ese nombre exacto.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-293">Use that exact name.</span></span>
 - <span data-ttu-id="a1e7f-294">Elija un nivel de servicio Premium.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="a1e7f-295">Hola copia [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="a1e7f-296">Hola script T-SQL crea Hola objetos necesarios en memoria Hola datos de ejemplo AdventureWorksLT que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="a1e7f-297">script de Hola crea la tabla de dimensiones de Hola y dos tablas de hechos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="a1e7f-298">tablas de hechos de Hola se rellenan con 3,5 millones de filas cada uno.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="a1e7f-299">script de Hola podría tardar toocomplete de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="a1e7f-300">Pegue el script de T-SQL de hello en SSMS y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="a1e7f-301">Hola **almacén de columnas** palabra clave en hello **CREATE INDEX** instrucción es fundamental, como en:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="a1e7f-302">Establecer el nivel de toocompatibility AdventureWorksLT 130:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="a1e7f-303">Nivel de 130 no es características memoria tooIn está directamente relacionado.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="a1e7f-304">Pero el nivel 130 suele ofrecer un rendimiento de consultas más rápido que el nivel 120.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="a1e7f-305">Tablas e índices de almacén de columnas clave</span><span class="sxs-lookup"><span data-stu-id="a1e7f-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="a1e7f-306">dbo. FactResellerSalesXL_CCI es una tabla que tiene un índice de almacén de columnas agrupado, que se ha avanzado compresión en hello *datos* nivel.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="a1e7f-307">dbo. FactResellerSalesXL_PageCompressed es una tabla que tiene un equivalente índice normal en clúster se comprime solo en hello *página* nivel.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="a1e7f-308">Índice de almacén de columnas de clave consultas toocompare Hola</span><span class="sxs-lookup"><span data-stu-id="a1e7f-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="a1e7f-309">Hay [varios tipos de consulta de T-SQL que se pueden ejecutar](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="a1e7f-310">En el paso 2 en hello script T-SQL, paga par de toothis de atención de consultas.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="a1e7f-311">Difieren solo en una línea:</span><span class="sxs-lookup"><span data-stu-id="a1e7f-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="a1e7f-312">Es un índice de almacén de columnas agrupado en hello FactResellerSalesXL\_tabla CCI.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="a1e7f-313">Hello extracto de script de T-SQL siguiente imprime las estadísticas de E/S y el tiempo de consulta de Hola de cada tabla.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="a1e7f-314">En una base de datos con el nivel de precios de hello P2, puede esperar aproximadamente nueve veces el aumento del rendimiento de Hola para esta consulta utilizando el índice de almacén de columnas agrupado hello en comparación con índice tradicional de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="a1e7f-315">Con P15, puede esperar ganancia de rendimiento de aproximadamente 57 veces Hola utilizando el índice de almacén de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a1e7f-316">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1e7f-316">Next steps</span></span>

- [<span data-ttu-id="a1e7f-317">Inicio rápido 1: Tecnologías OLTP en memoria para acelerar el rendimiento de Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="a1e7f-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="a1e7f-318">Uso de OLTP en memoria para mejorar el rendimiento de las aplicaciones en Azure SQL</span><span class="sxs-lookup"><span data-stu-id="a1e7f-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="a1e7f-319">[Supervisión del almacenamiento de OLTP en memoria](sql-database-in-memory-oltp-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a1e7f-320">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a1e7f-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="a1e7f-321">Información más detallada</span><span class="sxs-lookup"><span data-stu-id="a1e7f-321">Deeper information</span></span>

- [<span data-ttu-id="a1e7f-322">Más información sobre cómo Quorum duplica cargas de trabajo clave de las bases de datos a la vez que reduce las DTU en un 70 % con OLTP en memoria en SQL Database</span><span class="sxs-lookup"><span data-stu-id="a1e7f-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- <span data-ttu-id="a1e7f-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (OLTP en memoria en la entrada de Blog de base de datos de SQL de Azure)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

- [<span data-ttu-id="a1e7f-324">Más información sobre OLTP en memoria</span><span class="sxs-lookup"><span data-stu-id="a1e7f-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="a1e7f-325">Más información sobre los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="a1e7f-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="a1e7f-326">Más información sobre los análisis operativos en tiempo real</span><span class="sxs-lookup"><span data-stu-id="a1e7f-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="a1e7f-327">Consulte [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (Patrones de cargas de trabajo comunes y consideraciones de migración), que describe los patrones de carga de trabajo donde In-Memory OLTP normalmente proporciona importantes mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a1e7f-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="a1e7f-328">Diseño de aplicación</span><span class="sxs-lookup"><span data-stu-id="a1e7f-328">Application design</span></span>

- [<span data-ttu-id="a1e7f-329">In-Memory OLTP (optimización In-Memory)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="a1e7f-330">Uso de OLTP en memoria para mejorar el rendimiento de las aplicaciones en Azure SQL</span><span class="sxs-lookup"><span data-stu-id="a1e7f-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="a1e7f-331">Herramientas</span><span class="sxs-lookup"><span data-stu-id="a1e7f-331">Tools</span></span>

- [<span data-ttu-id="a1e7f-332">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a1e7f-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="a1e7f-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="a1e7f-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="a1e7f-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
