---
title: "Tecnologías en memoria de Azure SQL Database | Microsoft Docs"
description: "Las tecnologías en memoria de Azure SQL Database mejoran notablemente el rendimiento de las cargas de trabajo transaccionales y de análisis. Aprenda a sacar partido de estas tecnologías."
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
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="873f8-104">Optimización del rendimiento mediante las tecnologías en memoria de SQL Database</span><span class="sxs-lookup"><span data-stu-id="873f8-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="873f8-105">Mediante el uso de tecnologías en memoria en Azure SQL Database, puede lograr mejoras de rendimiento con diversas cargas de trabajo: transaccionales (procesamiento de transacciones en línea [OLTP]), analíticas (procesamiento analítico en línea [OLAP]) y mixtas (procesamiento analítico y transaccional híbrido [HTAP]).</span><span class="sxs-lookup"><span data-stu-id="873f8-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="873f8-106">Gracias al procesamiento más eficiente de las consultas y las transacciones, las tecnologías en memoria también lo ayudan a reducir costos.</span><span class="sxs-lookup"><span data-stu-id="873f8-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="873f8-107">Normalmente no necesita actualizar el plan de tarifa de la base de datos para lograr mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="873f8-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="873f8-108">En algunos casos, tal vez pueda reducir incluso el plan de tarifa sin dejar de observar mejoras de rendimiento con las tecnologías en memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="873f8-109">A continuación se muestran dos ejemplos de cómo OLTP en memoria ayudó significativamente a mejorar el rendimiento:</span><span class="sxs-lookup"><span data-stu-id="873f8-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="873f8-110">Gracias al uso de OLTP en memoria, [Quorum Business Solutions pudo duplicar la carga de trabajo al mismo tiempo que mejoró las DTU en un 70 %](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="873f8-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="873f8-111">DTU significa *Unidad de transmisión de datos*, e incluye una medida del consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="873f8-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="873f8-112">El vídeo siguiente muestra la mejora significativa del consumo de recursos con una carga de trabajo de ejemplo: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (Vídeo sobre OLTP en memoria en Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="873f8-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="873f8-113">Para más información, consulte la entrada de blog: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (OLTP en memoria en la entrada de Blog de base de datos de SQL de Azure).</span><span class="sxs-lookup"><span data-stu-id="873f8-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="873f8-114">Las tecnologías en memoria están disponibles en todas las bases de datos del plan Premium, incluidas las de grupos elásticos Premium.</span><span class="sxs-lookup"><span data-stu-id="873f8-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="873f8-115">En el siguiente vídeo se explican posibles mejoras de rendimiento obtenidas con las tecnologías en memoria de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="873f8-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="873f8-116">Tenga presente que la mejora de rendimiento que obtenga depende siempre de muchos factores, como la naturaleza de la carga de trabajo y los datos, los patrones de acceso de la base de datos, etc.</span><span class="sxs-lookup"><span data-stu-id="873f8-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="873f8-117">Azure SQL Database cuenta con las siguientes tecnologías en memoria:</span><span class="sxs-lookup"><span data-stu-id="873f8-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="873f8-118">*OLTP en memoria* aumenta el rendimiento y reduce la latencia del procesamiento de transacciones.</span><span class="sxs-lookup"><span data-stu-id="873f8-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="873f8-119">Estas son las situaciones en las que se obtienen ventajas con OLTP en memoria: procesamiento de transacciones de alto rendimiento, como operaciones comerciales y juegos, ingesta de datos de eventos o dispositivos de IoT, almacenamiento en caché, carga de datos y escenarios de tablas temporales y variables de tablas.</span><span class="sxs-lookup"><span data-stu-id="873f8-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="873f8-120">Los *índices de almacén de columnas en clúster* reducen el espacio de almacenamiento necesario (hasta 10 veces) y mejoran el rendimiento de las consultas de análisis e informes.</span><span class="sxs-lookup"><span data-stu-id="873f8-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="873f8-121">Puede usarlos con las tablas de hechos de sus data marts para incluir más datos en la base de datos y mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="873f8-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="873f8-122">También puede usarlos con los datos históricos de la base de datos operativa para archivar hasta 10 veces más datos, así como para disfrutar de un incremento equivalente en el número de consultas realizadas sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="873f8-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="873f8-123">Con los *índices de almacén de columnas no clúster* para HTAP, podrá obtener información en tiempo real sobre su negocio realizando consultas directamente a la base de datos operativa, sin necesidad de ejecutar un caro proceso de extracción, transformación y carga (ETL) ni esperar a que se rellene el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="873f8-124">Los índices de almacén de columnas no clúster permiten una ejecución muy rápida de las consultas de análisis en la base de datos OLTP y, a la vez, reducen el impacto en la carga de trabajo operativa.</span><span class="sxs-lookup"><span data-stu-id="873f8-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="873f8-125">También puede tener la combinación de una tabla optimizada para memoria con un índice de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="873f8-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="873f8-126">Esta combinación le permite realizar el procesamiento de transacciones de manera muy rápida y ejecutar consultas de análisis *simultáneamente* de manera muy rápida en los mismos datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="873f8-127">Las opciones de índices de almacén de columnas y OLTP en memoria forman parte de SQL Server desde 2012 y 2014, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="873f8-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="873f8-128">Azure SQL Database y SQL Server comparten la misma implementación de tecnologías en memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="873f8-129">A partir de ahora, las nuevas funciones para estas tecnologías se publican primero en Azure SQL Database y después, en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="873f8-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="873f8-130">En este tema se describen aspectos de OLTP en memoria y los índices de almacén de columnas específicos de Azure SQL Database; además, se incluyen ejemplos:</span><span class="sxs-lookup"><span data-stu-id="873f8-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="873f8-131">Veremos la repercusión de estas tecnologías en el almacenamiento, así como en los límites de tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="873f8-132">Después trataremos cómo administrar el movimiento de bases de datos que usan estas tecnologías entre los distintos planes de tarifa.</span><span class="sxs-lookup"><span data-stu-id="873f8-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="873f8-133">Y también eremos dos ejemplos que ilustran el uso de OLTP en memoria y de los índices del almacén de columnas en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="873f8-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="873f8-134">Para obtener más información, consulte los siguientes recursos.</span><span class="sxs-lookup"><span data-stu-id="873f8-134">See the following resources for more information.</span></span>

<span data-ttu-id="873f8-135">Información detallada sobre las tecnologías:</span><span class="sxs-lookup"><span data-stu-id="873f8-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="873f8-136">[Información general y escenarios de uso de OLTP en memoria](https://msdn.microsoft.com/library/mt774593.aspx) (incluye referencias a información y casos prácticos de clientes para familiarizarse)</span><span class="sxs-lookup"><span data-stu-id="873f8-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="873f8-137">Documentación de In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="873f8-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="873f8-138">Descripción de los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="873f8-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="873f8-139">Procesamiento analítico y transaccional híbrido (HTAP), también conocido como [análisis operativo en tiempo real](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="873f8-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="873f8-140">Una guía rápida sobre OLTP en memoria: [Inicio rápido 1: Tecnologías OLTP en memoria para acelerar el rendimiento de Transact-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (es otro artículo que lo ayudará a empezar a trabajar)</span><span class="sxs-lookup"><span data-stu-id="873f8-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="873f8-141">Vídeos detallados sobre las tecnologías:</span><span class="sxs-lookup"><span data-stu-id="873f8-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="873f8-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (OLTP en memoria en Azure SQL Database), que contiene una demostración de las ventajas de rendimiento y los pasos para reproducir estos resultados</span><span class="sxs-lookup"><span data-stu-id="873f8-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- <span data-ttu-id="873f8-143">[In-Memory OLTP Videos: What it is and When/How to use it](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/) (Vídeos de OLTP en memoria: qué es y cuándo/cómo usarlo)</span><span class="sxs-lookup"><span data-stu-id="873f8-143">[In-Memory OLTP Videos: What it is and When/How to use it](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)</span></span>
- <span data-ttu-id="873f8-144">[Columnstore Index: In-Memory Analytics Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/) (Índice de almacén de columnas: vídeos sobre análisis en memoria de Ignite 2016)</span><span class="sxs-lookup"><span data-stu-id="873f8-144">[Columnstore Index: In-Memory Analytics Videos from Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)</span></span>

## <a name="storage-and-data-size"></a><span data-ttu-id="873f8-145">Almacenamiento y tamaño de datos</span><span class="sxs-lookup"><span data-stu-id="873f8-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="873f8-146">Límite de almacenamiento y tamaño de datos para OLTP en memoria</span><span class="sxs-lookup"><span data-stu-id="873f8-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="873f8-147">OLTP en memoria incluye tablas con optimización de memoria, que se usan para almacenar los datos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="873f8-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="873f8-148">Estas tablas deben caber en la memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="873f8-149">Dado que administra la memoria directamente en el servicio de SQL Database, tenemos el concepto de una cuota para datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="873f8-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="873f8-150">Esta idea se conoce como *almacenamiento de OLTP en memoria*.</span><span class="sxs-lookup"><span data-stu-id="873f8-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="873f8-151">Cada plan de tarifa de grupo elástico y de base de datos independiente admitido incluye una cantidad determinada de almacenamiento de OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="873f8-152">En el momento de escribir este artículo, obtiene un gigabyte de almacenamiento por cada 125 unidades de transacción de base de datos (DTU) o unidades de transacción de base de datos elástica (eDTU).</span><span class="sxs-lookup"><span data-stu-id="873f8-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="873f8-153">En el artículo sobre los [niveles de servicio de SQL Database](sql-database-service-tiers.md), podrá encontrar la lista oficial de almacenamiento de OLTP en memoria disponible para cada plan de tarifa de grupo elástico y de base de datos independiente admitido.</span><span class="sxs-lookup"><span data-stu-id="873f8-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="873f8-154">Los siguientes elementos cuentan para su límite de almacenamiento de OLTP en memoria:</span><span class="sxs-lookup"><span data-stu-id="873f8-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="873f8-155">Las filas de datos de usuarios activos en tablas con optimización de memoria y variables de tabla.</span><span class="sxs-lookup"><span data-stu-id="873f8-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="873f8-156">Tenga en cuenta que las versiones antiguas de las filas no cuentan para el límite.</span><span class="sxs-lookup"><span data-stu-id="873f8-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="873f8-157">Los índices de tablas con optimización de memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="873f8-158">La sobrecarga operacional de operaciones ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="873f8-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="873f8-159">Si alcanza el límite, recibirá un error que le notificará que se ha quedado sin cuota y no podrá volver a insertar o actualizar datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="873f8-160">Para mitigar este error, elimine datos o aumente el plan de tarifa de la base de datos o del grupo.</span><span class="sxs-lookup"><span data-stu-id="873f8-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="873f8-161">Para obtener más información sobre cómo supervisar la utilización del almacenamiento de OLTP en memoria y configurar alertas que se activen cuando casi haya alcanzado el límite, consulte [Supervisión del almacenamiento en memoria](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="873f8-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="873f8-162">Acerca de los grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="873f8-162">About elastic pools</span></span>

<span data-ttu-id="873f8-163">Con grupos elásticos, el almacenamiento de OLTP en memoria se comparte entre todas las bases de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="873f8-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="873f8-164">Por lo tanto, el uso de una base de datos puede afectar a otras bases de datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="873f8-165">Existen dos formas de mitigar este problema:</span><span class="sxs-lookup"><span data-stu-id="873f8-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="873f8-166">Establecer un valor de eDTU máx. para las bases de datos que sea inferior al número de eDTU del grupo en su conjunto.</span><span class="sxs-lookup"><span data-stu-id="873f8-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="873f8-167">De este modo, se limita la utilización del almacenamiento de OLTP en memoria en cualquier base de datos del grupo al tamaño correspondiente al número de eDTU.</span><span class="sxs-lookup"><span data-stu-id="873f8-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="873f8-168">Configurar un valor de eDTU mín. que sea mayor que 0.</span><span class="sxs-lookup"><span data-stu-id="873f8-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="873f8-169">Este mínimo garantiza que cada base de datos del grupo tenga la cantidad de almacenamiento de OLTP en memoria disponible que corresponde al valor configurado para eDTU mín.</span><span class="sxs-lookup"><span data-stu-id="873f8-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="873f8-170">Almacenamiento y tamaño de datos para los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="873f8-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="873f8-171">No se requiere que los índices de almacén de columnas quepan en la memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="873f8-172">Por lo tanto, el único límite del tamaño de los índices es el tamaño máximo global de la base de datos, que está documentado en el artículo sobre los [niveles de servicio de SQL Database](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="873f8-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="873f8-173">Al utilizar los índices de almacén de columnas en clúster, se emplea una compresión de columnas para el almacenamiento de la tabla base.</span><span class="sxs-lookup"><span data-stu-id="873f8-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="873f8-174">Esta compresión puede reducir considerablemente el consumo de almacenamiento de sus datos de usuario, lo que significa que la base de datos podrá albergar más información.</span><span class="sxs-lookup"><span data-stu-id="873f8-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="873f8-175">Y es posible aumentar este compresión aún más con la [compresión de archivo de columnas](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="873f8-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="873f8-176">La cantidad de compresión que puede lograr depende de la naturaleza de los datos, pero no es raro obtener una compresión que reduzca el tamaño en 10 veces.</span><span class="sxs-lookup"><span data-stu-id="873f8-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="873f8-177">Por ejemplo, si tiene una base de datos con el tamaño máximo de 1 terabyte (TB) y logra una compresión de 10 veces con índices de almacén de columnas, puede incluir un total de 10 TB de datos de usuario en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="873f8-178">Al utilizar índices de almacén de columnas no agrupados, la tabla base sigue almacenada en el formato de almacenamiento de filas tradicional.</span><span class="sxs-lookup"><span data-stu-id="873f8-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="873f8-179">Por lo tanto, el ahorro de almacenamiento no es tan grande como con los índices de almacén de columnas agrupados.</span><span class="sxs-lookup"><span data-stu-id="873f8-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="873f8-180">Pero si sustituye diversos índices no agrupados tradicionales por un único índice de almacén de columnas, aún podrá obtener un ahorro global en el espacio de almacenamiento de la tabla.</span><span class="sxs-lookup"><span data-stu-id="873f8-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="873f8-181">Movimiento de bases de datos que usan tecnologías en memoria entre planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="873f8-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="873f8-182">Nunca hay incompatibilidades u otros problemas al actualizar a un plan de tarifas superior, como de Estándar a Premium.</span><span class="sxs-lookup"><span data-stu-id="873f8-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="873f8-183">Solo aumenta la funcionalidad y los recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="873f8-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="873f8-184">Pero cambiar a un plan de tarifas inferior puede repercutir negativamente en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="873f8-185">El impacto es especialmente evidente al cambiar de Premium a Estándar o Básico cuando la base de datos contiene objetos de OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="873f8-186">Las tablas optimizadas para memoria y los índices de almacén de columnas no están disponibles después del cambio a una versión anterior (aunque sigan estando visibles).</span><span class="sxs-lookup"><span data-stu-id="873f8-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="873f8-187">Lo mismo se aplica al reducir el plan de tarifa de un grupo elástico o mover bases de datos con tecnologías en memoria a un grupo elástico Estándar o Básico.</span><span class="sxs-lookup"><span data-stu-id="873f8-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="873f8-188">In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="873f8-188">In-Memory OLTP</span></span>

<span data-ttu-id="873f8-189">*Reducción a Básico o Estándar*: OLTP en memoria no se admite en bases de datos que se encuentren en los planes Estándar o Básico.</span><span class="sxs-lookup"><span data-stu-id="873f8-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="873f8-190">Además, no es posible mover una base de datos con objetos de OLTP en memoria a los planes Estándar o Básico.</span><span class="sxs-lookup"><span data-stu-id="873f8-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="873f8-191">Antes de degradar el plan de tarifa de una base de datos a Estándar o Básico, quite todos los tipos de tabla y las tablas con optimización de memoria, así como todos los módulos de Transact-SQL compilados de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="873f8-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="873f8-192">No existe ningún mecanismo de programación para comprender si una base de datos específica admite OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="873f8-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="873f8-193">Puede ejecutar la siguiente consulta de Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="873f8-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="873f8-194">Si la consulta devuelve **1**, OLTP en memoria se admite en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="873f8-195">*Reducción a un plan Premium inferior*: los datos de las tablas con optimización de memoria deben caber en el almacenamiento de OLTP en memoria asociado al plan de tarifa de la base de datos o disponible en el grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="873f8-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="873f8-196">Si trata de reducir el plan de tarifa o mover la base de datos a un grupo que no disponga de almacenamiento de OLTP en memoria suficiente, la operación no se desarrolla correctamente.</span><span class="sxs-lookup"><span data-stu-id="873f8-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="873f8-197">Índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="873f8-197">Columnstore indexes</span></span>

<span data-ttu-id="873f8-198">*Cambiar a Básico o Estándar*: los índices de almacén de columnas solo se admiten en el plan de tarifa Premium y no en los planes Estándar o Básico.</span><span class="sxs-lookup"><span data-stu-id="873f8-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="873f8-199">Cuando se cambie la base de datos a Estándar o Básico, el índice de almacén de columnas no estará disponible.</span><span class="sxs-lookup"><span data-stu-id="873f8-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="873f8-200">El sistema mantiene el índice de almacén de columnas, pero no aprovecha el índice.</span><span class="sxs-lookup"><span data-stu-id="873f8-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="873f8-201">Si después actualiza a Premium, el índice de almacén de columnas está listo para volver a sacar el máximo partido.</span><span class="sxs-lookup"><span data-stu-id="873f8-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="873f8-202">Si tiene un índice de almacén de columnas **en clúster**, toda la tabla deja de estar disponible después del cambio a un nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="873f8-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="873f8-203">Por lo tanto, se recomienda quitar todos los índices de almacén de columnas *en clúster* antes de cambiar la base de datos por debajo del nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="873f8-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="873f8-204">*Cambio a un plan Premium inferior*: este cambio se realiza correctamente si toda la base de datos se adapta al tamaño máximo de la base de datos del plan de tarifa objetivo o al almacenamiento disponible en el grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="873f8-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="873f8-205">Los índices de almacén de columnas no tienen ningún impacto concreto en este caso.</span><span class="sxs-lookup"><span data-stu-id="873f8-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="873f8-206">1. Instalación del ejemplo de In-Memory OLTP.</span><span class="sxs-lookup"><span data-stu-id="873f8-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="873f8-207">La base de datos de ejemplo AdventureWorksLT se puede crear con unos pocos clics en el [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="873f8-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="873f8-208">Los pasos descritos en esta sección explican cómo puede enriquecer la base de datos AdventureWorksLT con objetos de OLTP en memoria y muestran las ventajas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="873f8-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="873f8-209">Si desea ver una demostración más simple, pero más atractiva visualmente, del rendimiento de OLTP en memoria, consulte:</span><span class="sxs-lookup"><span data-stu-id="873f8-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="873f8-210">Versión: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="873f8-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="873f8-211">Código fuente: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="873f8-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="873f8-212">Pasos de instalación</span><span class="sxs-lookup"><span data-stu-id="873f8-212">Installation steps</span></span>

1. <span data-ttu-id="873f8-213">En el [Azure Portal](https://portal.azure.com/), cree una base de datos Premium en un servidor.</span><span class="sxs-lookup"><span data-stu-id="873f8-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="873f8-214">Establezca el **Origen** en la base de datos de ejemplo de AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="873f8-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="873f8-215">Para obtener instrucciones detalladas, consulte [Creación de la primera Base de datos SQL de Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="873f8-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="873f8-216">Conéctese a la base de datos con SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="873f8-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="873f8-217">Copie el [script Transact-SQL de In-Memory OLTP](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="873f8-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="873f8-218">El script T-SQL crea los objetos en memoria necesarios en la base de datos de ejemplo AdventureWorksLT que se creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="873f8-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="873f8-219">Pegue el script T-SQL en SSMS.exe y, luego, ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="873f8-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="873f8-220">Es crucial la instrucción CREATE TABLE de la cláusula `MEMORY_OPTIMIZED = ON`.</span><span class="sxs-lookup"><span data-stu-id="873f8-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="873f8-221">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="873f8-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="873f8-222">Error 40536</span><span class="sxs-lookup"><span data-stu-id="873f8-222">Error 40536</span></span>


<span data-ttu-id="873f8-223">Si recibe el error 40536 cuando ejecuta el script T-SQL, ejecute el siguiente script de T-SQL para comprobar que la base de datos admite In-Memory:</span><span class="sxs-lookup"><span data-stu-id="873f8-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="873f8-224">Un resultado de **0** significa que no se admite en memoria, mientras que un resultado de **1** significa que se admite.</span><span class="sxs-lookup"><span data-stu-id="873f8-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="873f8-225">Para diagnosticar el problema, asegúrese de que la base de datos se encuentra en el nivel de servicio Premium.</span><span class="sxs-lookup"><span data-stu-id="873f8-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="873f8-226">Acerca de los elementos creados con optimización para memoria</span><span class="sxs-lookup"><span data-stu-id="873f8-226">About the created memory-optimized items</span></span>

<span data-ttu-id="873f8-227">**Tablas**: el ejemplo contiene las siguientes tablas con optimización para memoria:</span><span class="sxs-lookup"><span data-stu-id="873f8-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="873f8-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="873f8-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="873f8-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="873f8-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="873f8-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="873f8-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="873f8-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="873f8-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="873f8-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="873f8-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="873f8-233">Puede inspeccionar las tablas con optimización para memoria a través del **Explorador de objetos** en SSMS.</span><span class="sxs-lookup"><span data-stu-id="873f8-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="873f8-234">Haga clic con el botón derecho en **Tablas** > **Filtro** > **Configuración de filtro** > **Con optimización para memoria**.</span><span class="sxs-lookup"><span data-stu-id="873f8-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="873f8-235">El valor es igual a 1.</span><span class="sxs-lookup"><span data-stu-id="873f8-235">The value equals 1.</span></span>


<span data-ttu-id="873f8-236">O bien puede consultar las vistas de catálogo como:</span><span class="sxs-lookup"><span data-stu-id="873f8-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="873f8-237">**Procedimiento almacenado compilado de forma nativa**: puede inspeccionar SalesLT.usp_InsertSalesOrder_inmem mediante una consulta de la vista de catálogo:</span><span class="sxs-lookup"><span data-stu-id="873f8-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="873f8-238">Ejecución de la carga de trabajo de OLTP de ejemplo</span><span class="sxs-lookup"><span data-stu-id="873f8-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="873f8-239">La única diferencia entre los dos *procedimientos almacenados* siguientes es que el primer procedimiento usa las versiones de las tablas con optimización para memoria, mientras que el segundo procedimiento usa las tablas en disco habituales:</span><span class="sxs-lookup"><span data-stu-id="873f8-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="873f8-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="873f8-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="873f8-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="873f8-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="873f8-242">En esta sección verá cómo usar la práctica utilidad **ostress.exe** para ejecutar los dos procedimientos almacenados a niveles de esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="873f8-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="873f8-243">Puede comparar el tiempo que tardan en completarse las dos ejecuciones de esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="873f8-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="873f8-244">Cuando se ejecuta ostress.exe, le recomendamos pasar los valores de parámetros diseñados para estos dos casos:</span><span class="sxs-lookup"><span data-stu-id="873f8-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="873f8-245">Ejecute un gran número de conexiones simultáneas, mediante el uso de -n100.</span><span class="sxs-lookup"><span data-stu-id="873f8-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="873f8-246">Haga que cada conexión se repita en bucle cientos de veces, mediante el uso de -r500.</span><span class="sxs-lookup"><span data-stu-id="873f8-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="873f8-247">Pero es posible que quiera comenzar con valores mucho más pequeños, como -n10 y -r50, para garantizar que todo está funcionando.</span><span class="sxs-lookup"><span data-stu-id="873f8-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="873f8-248">Script para ostress.exe</span><span class="sxs-lookup"><span data-stu-id="873f8-248">Script for ostress.exe</span></span>


<span data-ttu-id="873f8-249">En esta sección se muestra el script de T-SQL que se inserta en la línea de comandos de ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="873f8-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="873f8-250">El script usa elementos creados por el script de T-SQL que instaló antes.</span><span class="sxs-lookup"><span data-stu-id="873f8-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="873f8-251">El siguiente script inserta un pedido de ventas de ejemplo con cinco elementos de línea en las siguientes *tablas*con optimización para memoria:</span><span class="sxs-lookup"><span data-stu-id="873f8-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="873f8-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="873f8-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="873f8-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="873f8-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="873f8-254">Para hacer que la versión *_ondisk* del script T-SQL anterior sirva para ostress.exe, hay que reemplazar ambas repeticiones de la subcadena *_inmem* por *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="873f8-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="873f8-255">Estos reemplazos afectan a los nombres de tablas y procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="873f8-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="873f8-256">Instalación de ostress y utilidades de RML</span><span class="sxs-lookup"><span data-stu-id="873f8-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="873f8-257">Lo ideal sería planear la ejecución de ostress.exe en una máquina virtual de Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="873f8-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="873f8-258">Se crearía una [VM de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) en la misma región geográfica de Azure en que reside la base de datos AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="873f8-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="873f8-259">Pero puede ejecutar si lo desea ostress.exe en el equipo portátil.</span><span class="sxs-lookup"><span data-stu-id="873f8-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="873f8-260">En la VM, o en cualquier host que elija, instale las utilidades de Replay Markup Language (RML).</span><span class="sxs-lookup"><span data-stu-id="873f8-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="873f8-261">Las utilidades incluyen ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="873f8-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="873f8-262">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="873f8-262">For more information, see:</span></span>
- <span data-ttu-id="873f8-263">La explicación de ostress.exe en [Base de datos de ejemplo para OLTP en memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="873f8-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="873f8-264">[Base de datos de ejemplo para OLTP en memoria](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="873f8-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="873f8-265">El [blog para instalar ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="873f8-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="873f8-266">Ejecute de la carga de trabajo de esfuerzo *_inmem* en primer lugar</span><span class="sxs-lookup"><span data-stu-id="873f8-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="873f8-267">Puede usar una ventana *del símbolo del sistema de RML* para ejecutar la línea de comandos de ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="873f8-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="873f8-268">Los parámetros de la línea de comandos dirigen ostress para:</span><span class="sxs-lookup"><span data-stu-id="873f8-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="873f8-269">Ejecutar 100 conexiones simultáneamente (-n100).</span><span class="sxs-lookup"><span data-stu-id="873f8-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="873f8-270">Hacer que cada conexión ejecute el script de T-SQL 50 veces (-r50).</span><span class="sxs-lookup"><span data-stu-id="873f8-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="873f8-271">Para ejecutar la línea de comandos ostress.exe anterior:</span><span class="sxs-lookup"><span data-stu-id="873f8-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="873f8-272">Restablezca el contenido de los datos de la base de datos mediante la ejecución del siguiente comando en SSMS para eliminar todos los datos que se insertaron en las ejecuciones anteriores:</span><span class="sxs-lookup"><span data-stu-id="873f8-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="873f8-273">Copie el texto de la línea de comandos ostress.exe anterior en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="873f8-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="873f8-274">Reemplace el `<placeholders>` de los parámetros -S -U -P -d por los valores reales correctos.</span><span class="sxs-lookup"><span data-stu-id="873f8-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="873f8-275">Ejecute la línea de comandos modificada en una ventana del símbolo del sistema de RML.</span><span class="sxs-lookup"><span data-stu-id="873f8-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="873f8-276">El resultado es una duración</span><span class="sxs-lookup"><span data-stu-id="873f8-276">Result is a duration</span></span>


<span data-ttu-id="873f8-277">Cuando finaliza ostress.exe, escribe la duración de la ejecución como la última línea de la salida en la ventana de símbolo del sistema de RML.</span><span class="sxs-lookup"><span data-stu-id="873f8-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="873f8-278">Por ejemplo, una ejecución de prueba más corta duró aproximadamente 1,5 minutos:</span><span class="sxs-lookup"><span data-stu-id="873f8-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="873f8-279">Restablezca y edite *_ondisk* y, después, vuelva a ejecutarlo</span><span class="sxs-lookup"><span data-stu-id="873f8-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="873f8-280">Una vez que tenga el resultado de la ejecución de *_inmem*, realice los pasos siguientes para la ejecución de *_ondisk*:</span><span class="sxs-lookup"><span data-stu-id="873f8-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="873f8-281">Restablezca la base de datos mediante la ejecución del siguiente comando en SSMS para eliminar todos los datos que insertó la ejecución anterior:</span><span class="sxs-lookup"><span data-stu-id="873f8-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="873f8-282">Edite la línea de comandos de ostress.exe para reemplazar todos los *_inmem* con *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="873f8-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="873f8-283">Ejecute ostress.exe por segunda vez y capture el resultado de la duración.</span><span class="sxs-lookup"><span data-stu-id="873f8-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="873f8-284">Vuelva a restablecer la base de datos (para la eliminación responsable de lo que puede constituir una gran cantidad de datos de prueba).</span><span class="sxs-lookup"><span data-stu-id="873f8-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="873f8-285">Resultados de la comparación esperados</span><span class="sxs-lookup"><span data-stu-id="873f8-285">Expected comparison results</span></span>

<span data-ttu-id="873f8-286">Las pruebas de en memoria demostraron tener un rendimiento **9 veces** mejor en esta carga de trabajo simplista, con ostress ejecutándose en una VM de Azure ubicada en la misma región de Azure que la base de datos.</span><span class="sxs-lookup"><span data-stu-id="873f8-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="873f8-287">2. Instalación del ejemplo de In-Memory Analytics.</span><span class="sxs-lookup"><span data-stu-id="873f8-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="873f8-288">En esta sección, compara los resultados de optimización de infraestructura y de estadísticas cuando usa un índice del almacén de columnas en lugar de un índice de árbol b tradicional.</span><span class="sxs-lookup"><span data-stu-id="873f8-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="873f8-289">Para realizar análisis en tiempo real en una carga de trabajo de OLTP, suele ser mejor usar un índice del almacén de columnas no agrupado.</span><span class="sxs-lookup"><span data-stu-id="873f8-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="873f8-290">Para obtener más información, consulte [Guía de índices de almacén de columnas](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="873f8-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="873f8-291">Preparación de la prueba de análisis del almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="873f8-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="873f8-292">Use el Portal de Azure para crear una nueva base de datos AdventureWorksLT a partir del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="873f8-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="873f8-293">Use ese nombre exacto.</span><span class="sxs-lookup"><span data-stu-id="873f8-293">Use that exact name.</span></span>
 - <span data-ttu-id="873f8-294">Elija un nivel de servicio Premium.</span><span class="sxs-lookup"><span data-stu-id="873f8-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="873f8-295">Copie [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) en el Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="873f8-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="873f8-296">El script T-SQL crea los objetos en memoria necesarios en la base de datos de ejemplo AdventureWorksLT que se creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="873f8-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="873f8-297">El script crea la tabla de dimensiones y dos tablas de hechos.</span><span class="sxs-lookup"><span data-stu-id="873f8-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="873f8-298">Las tablas de hechos se rellenan con 3,5 millones de filas cada una.</span><span class="sxs-lookup"><span data-stu-id="873f8-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="873f8-299">El script podría tardar 15 minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="873f8-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="873f8-300">Pegue el script T-SQL en SSMS.exe y, luego, ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="873f8-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="873f8-301">La palabra clave **COLUMNSTORE** es crucial en la instrucción **CREATE INDEX**, como en:</span><span class="sxs-lookup"><span data-stu-id="873f8-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="873f8-302">Establezca AdventureWorksLT en un nivel de compatibilidad 130:</span><span class="sxs-lookup"><span data-stu-id="873f8-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="873f8-303">El nivel 130 no está directamente relacionado con las características de In-Memory.</span><span class="sxs-lookup"><span data-stu-id="873f8-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="873f8-304">Pero el nivel 130 suele ofrecer un rendimiento de consultas más rápido que el nivel 120.</span><span class="sxs-lookup"><span data-stu-id="873f8-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="873f8-305">Tablas e índices de almacén de columnas clave</span><span class="sxs-lookup"><span data-stu-id="873f8-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="873f8-306">dbo.FactResellerSalesXL_CCI es una tabla con un índice de almacén de columnas agrupado que tiene una compresión avanzada a nivel de *datos*.</span><span class="sxs-lookup"><span data-stu-id="873f8-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="873f8-307">dbo.FactResellerSalesXL_PageCompressed es una tabla con un índice agrupado equivalente normal, que se comprime solo a nivel de *página*.</span><span class="sxs-lookup"><span data-stu-id="873f8-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="873f8-308">Consultas cruciales para comparar el índice de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="873f8-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="873f8-309">Aquí hay [varios tipos de consultas de T-SQL que se pueden ejecutar](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) para ver las mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="873f8-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="873f8-310">En el paso 2 del script T-SQL, preste atención a estas dos consultas.</span><span class="sxs-lookup"><span data-stu-id="873f8-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="873f8-311">Difieren solo en una línea:</span><span class="sxs-lookup"><span data-stu-id="873f8-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="873f8-312">Un índice de almacén de columnas en clúster se encuentra en la tabla FactResellerSalesXL\_CCI.</span><span class="sxs-lookup"><span data-stu-id="873f8-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="873f8-313">El siguiente fragmento de script de T-SQL imprime las estadísticas de IO y TIME para la consulta de cada tabla.</span><span class="sxs-lookup"><span data-stu-id="873f8-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
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


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
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

<span data-ttu-id="873f8-314">En una base de datos con el plan de tarifa P2, puede esperar un rendimiento nueve veces superior, aproximadamente, para esta consulta al usar el índice de almacén de columnas en clúster, en comparación con el índice tradicional.</span><span class="sxs-lookup"><span data-stu-id="873f8-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="873f8-315">Con P15, puede esperar, aproximadamente, un rendimiento 57 veces superior gracias al uso de índice de almacén de columnas.</span><span class="sxs-lookup"><span data-stu-id="873f8-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="873f8-316">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="873f8-316">Next steps</span></span>

- [<span data-ttu-id="873f8-317">Inicio rápido 1: Tecnologías OLTP en memoria para acelerar el rendimiento de Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="873f8-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="873f8-318">Uso de OLTP en memoria para mejorar el rendimiento de las aplicaciones en Azure SQL</span><span class="sxs-lookup"><span data-stu-id="873f8-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="873f8-319">[Supervisión del almacenamiento de OLTP en memoria](sql-database-in-memory-oltp-monitoring.md)</span><span class="sxs-lookup"><span data-stu-id="873f8-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="873f8-320">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="873f8-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="873f8-321">Información más detallada</span><span class="sxs-lookup"><span data-stu-id="873f8-321">Deeper information</span></span>

- [<span data-ttu-id="873f8-322">Más información sobre cómo Quorum duplica cargas de trabajo clave de las bases de datos a la vez que reduce las DTU en un 70 % con OLTP en memoria en SQL Database</span><span class="sxs-lookup"><span data-stu-id="873f8-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- <span data-ttu-id="873f8-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (OLTP en memoria en la entrada de Blog de base de datos de SQL de Azure)</span><span class="sxs-lookup"><span data-stu-id="873f8-323">[In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

- [<span data-ttu-id="873f8-324">Más información sobre OLTP en memoria</span><span class="sxs-lookup"><span data-stu-id="873f8-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="873f8-325">Más información sobre los índices de almacén de columnas</span><span class="sxs-lookup"><span data-stu-id="873f8-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="873f8-326">Más información sobre los análisis operativos en tiempo real</span><span class="sxs-lookup"><span data-stu-id="873f8-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="873f8-327">Consulte [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (Patrones de cargas de trabajo comunes y consideraciones de migración), que describe los patrones de carga de trabajo donde In-Memory OLTP normalmente proporciona importantes mejoras de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="873f8-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="873f8-328">Diseño de aplicación</span><span class="sxs-lookup"><span data-stu-id="873f8-328">Application design</span></span>

- [<span data-ttu-id="873f8-329">In-Memory OLTP (optimización In-Memory)</span><span class="sxs-lookup"><span data-stu-id="873f8-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="873f8-330">Uso de OLTP en memoria para mejorar el rendimiento de las aplicaciones en Azure SQL</span><span class="sxs-lookup"><span data-stu-id="873f8-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="873f8-331">Herramientas</span><span class="sxs-lookup"><span data-stu-id="873f8-331">Tools</span></span>

- [<span data-ttu-id="873f8-332">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="873f8-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="873f8-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="873f8-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="873f8-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="873f8-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
