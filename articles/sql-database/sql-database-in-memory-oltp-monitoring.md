---
title: "Supervisión del almacenamiento en memoria de XTP | Microsoft Docs"
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
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="d5eb5-103">Supervisión del almacenamiento OLTP en memoria</span><span class="sxs-lookup"><span data-stu-id="d5eb5-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="d5eb5-104">Cuando se usa [OLTP en memoria](sql-database-in-memory.md), los datos de tablas con optimización de memoria y las variables de tabla residen en el almacenamiento OLTP en memoria.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="d5eb5-105">Cada nivel de servicio Premium tiene un tamaño máximo de almacenamiento OLTP en memoria, que se documenta en el artículo [Niveles de servicio de SQL Database](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="d5eb5-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="d5eb5-106">Una vez que se supera ese límite, las operaciones de inserción y actualización pueden empezar a producir errores (con el error 41823).</span><span class="sxs-lookup"><span data-stu-id="d5eb5-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="d5eb5-107">En ese momento se necesita eliminar los datos para reclamar memoria o actualizar el nivel de rendimiento de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="d5eb5-108">Determinación de si los datos se ajustan dentro del límite de almacenamiento en memoria</span><span class="sxs-lookup"><span data-stu-id="d5eb5-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="d5eb5-109">Determine el extremo de almacenamiento: consulte en el artículo [Niveles de servicio de SQL Database](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) los extremos de almacenamiento de los diferentes niveles de servicio Premium.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="d5eb5-110">La estimación de los requisitos de memoria para una tabla optimizada en memoria funciona de la misma manera para SQL Server tal y como se hace en la base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="d5eb5-111">Dedique algunos minutos a revisar ese tema en [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5eb5-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="d5eb5-112">Tenga en cuenta que la tabla y las filas de variables de tabla, así como los índices, se contarán para el tamaño de datos de usuario máx.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="d5eb5-113">Además, ALTER TABLE necesita suficiente espacio para crear una nueva versión de toda la tabla y sus índices.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="d5eb5-114">Supervisión y alertas</span><span class="sxs-lookup"><span data-stu-id="d5eb5-114">Monitoring and alerting</span></span>
<span data-ttu-id="d5eb5-115">Puede supervisar el uso del almacenamiento en memoria como un porcentaje del [extremo de almacenamiento para su nivel de rendimiento](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) en [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="d5eb5-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="d5eb5-116">En la hoja Base de datos, busque el cuadro de uso de recursos y haga clic en Editar.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="d5eb5-117">A continuación, seleccione la métrica `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="d5eb5-118">Para agregar una alerta, haga clic en el cuadro Uso de recursos para abrir la hoja de métricas y después haga clic en Agregar alerta.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="d5eb5-119">O bien, use la siguiente consulta para mostrar el uso del almacenamiento en memoria:</span><span class="sxs-lookup"><span data-stu-id="d5eb5-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="d5eb5-120">Corrección de situaciones de falta de memoria (error 41823)</span><span class="sxs-lookup"><span data-stu-id="d5eb5-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="d5eb5-121">Si el sistema se queda sin memoria, las operaciones INSERT, UPDATE y CREATE no se llevarán a cabo, y se mostrará el mensaje de error 41823.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="d5eb5-122">El mensaje de error 41823 indica que las variables de tabla y las tablas optimizadas para memoria han superado el tamaño máximo.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="d5eb5-123">Para resolver este error, haga uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5eb5-123">To resolve this error, either:</span></span>

* <span data-ttu-id="d5eb5-124">Elimine datos de las tablas optimizadas para memoria, lo que potencialmente descarga los datos a tablas tradicionales, basadas en disco; o bien,</span><span class="sxs-lookup"><span data-stu-id="d5eb5-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="d5eb5-125">Actualice el nivel de servicio a uno con suficiente espacio de almacenamiento en memoria para los datos que necesita mantener en tablas optimizadas en memoria.</span><span class="sxs-lookup"><span data-stu-id="d5eb5-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5eb5-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5eb5-126">Next steps</span></span>
<span data-ttu-id="d5eb5-127">Para obtener instrucciones sobre la supervisión, consulte [Supervisión de Azure SQL Database con vistas de administración dinámica](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="d5eb5-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
