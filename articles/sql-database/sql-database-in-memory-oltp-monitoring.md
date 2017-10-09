---
title: almacenamiento en memoria de aaaMonitor XTP | Documentos de Microsoft
description: Estimar y supervisar el uso y la capacidad del almacenamiento en memoria de XTP; resolver el error de capacidad 41823
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="7526f-103">Supervisión del almacenamiento OLTP en memoria</span><span class="sxs-lookup"><span data-stu-id="7526f-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="7526f-104">Cuando se usa [OLTP en memoria](sql-database-in-memory.md), los datos de tablas con optimización de memoria y las variables de tabla residen en el almacenamiento OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="7526f-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="7526f-105">Cada nivel de servicio Premium tiene un tamaño máximo de almacenamiento de OLTP en memoria, que se documenta en hello [artículo niveles de servicio de base de datos de SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="7526f-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="7526f-106">Una vez que se supera ese límite, las operaciones de inserción y actualización pueden empezar a producir errores (con el error 41823).</span><span class="sxs-lookup"><span data-stu-id="7526f-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="7526f-107">En ese momento se necesitan tooeither eliminar datos tooreclaim memoria o actualizar el nivel de rendimiento de saludo de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="7526f-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="7526f-108">Determinar si los datos se ajustan dentro del límite de almacenamiento en memoria de Hola</span><span class="sxs-lookup"><span data-stu-id="7526f-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="7526f-109">Determinar el límite de almacenamiento de hello: consulte hello [artículo niveles de servicio de base de datos de SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) para los límites de almacenamiento de Hola de distintos niveles de servicio Premium Hola.</span><span class="sxs-lookup"><span data-stu-id="7526f-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="7526f-110">Calcular la memoria requisitos para una tabla con optimización para memoria funciona igual Hola forma para SQL Server tal como se hace en la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7526f-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="7526f-111">Desconectar de ese tema tooreview unos minutos en [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="7526f-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="7526f-112">Tenga en cuenta que la tabla de Hola y filas de variables de tabla, así como índices, cuentan para tamaño de datos de usuario max Hola.</span><span class="sxs-lookup"><span data-stu-id="7526f-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="7526f-113">Además, ALTER TABLE necesita suficiente toocreate sala una nueva versión de toda la tabla hello y sus índices.</span><span class="sxs-lookup"><span data-stu-id="7526f-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="7526f-114">Supervisión y alertas</span><span class="sxs-lookup"><span data-stu-id="7526f-114">Monitoring and alerting</span></span>
<span data-ttu-id="7526f-115">Puede supervisar el uso de almacenamiento en memoria como un porcentaje de hello [límite de almacenamiento para el nivel de rendimiento](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) en hello Azure [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="7526f-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="7526f-116">En la hoja de la base de datos de hello, busque el cuadro de utilización de recursos de Hola y haga clic en Editar.</span><span class="sxs-lookup"><span data-stu-id="7526f-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="7526f-117">A continuación, seleccione la métrica de hello `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="7526f-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="7526f-118">tooadd una alerta, haga clic en la hoja de métricas de hello utilización de recursos cuadro tooopen hello, a continuación, haga clic en Agregar alerta.</span><span class="sxs-lookup"><span data-stu-id="7526f-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="7526f-119">O bien utilizar Hola después de utilización del almacenamiento en memoria de consulta tooshow hello:</span><span class="sxs-lookup"><span data-stu-id="7526f-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="7526f-120">Corrección de situaciones de falta de memoria (error 41823)</span><span class="sxs-lookup"><span data-stu-id="7526f-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="7526f-121">Si el sistema se queda sin memoria, las operaciones INSERT, UPDATE y CREATE no se llevarán a cabo, y se mostrará el mensaje de error 41823.</span><span class="sxs-lookup"><span data-stu-id="7526f-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="7526f-122">Mensaje de error 41823 indica que las tablas optimizadas en memoria de Hola y las variables de tabla han superado el tamaño máximo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7526f-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="7526f-123">tooresolve este error, ya sea:</span><span class="sxs-lookup"><span data-stu-id="7526f-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="7526f-124">Eliminar datos de tablas optimizadas en memoria de hello, potencialmente descarga Hola datos tootraditional, las tablas basadas en disco; o bien,</span><span class="sxs-lookup"><span data-stu-id="7526f-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="7526f-125">Actualizar tooone de nivel de servicio de hello con suficiente almacenamiento en memoria para los datos de hello debe tookeep en tablas optimizadas en memoria.</span><span class="sxs-lookup"><span data-stu-id="7526f-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7526f-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7526f-126">Next steps</span></span>
<span data-ttu-id="7526f-127">Para obtener instrucciones sobre la supervisión, consulte [Supervisión de Azure SQL Database con vistas de administración dinámica](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="7526f-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
