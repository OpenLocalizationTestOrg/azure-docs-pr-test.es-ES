---
title: "aaaMigrate el almacenamiento de datos de solución tooSQL | Documentos de Microsoft"
description: "Guía de migración para poner la plataforma de almacenamiento de datos SQL de solución tooAzure."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="be047-103">Migrar el almacenamiento de datos SQL de solución tooAzure</span><span class="sxs-lookup"><span data-stu-id="be047-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="be047-104">Vea las implicaciones de migrar un tooAzure de solución de base de datos almacén de datos SQL existente.</span><span class="sxs-lookup"><span data-stu-id="be047-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="be047-105">Generación del perfil de la carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="be047-105">Profile your workload</span></span>
<span data-ttu-id="be047-106">Antes de migrar, desea toobe seguro de que almacenamiento de datos SQL es la solución correcta de hello para la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="be047-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="be047-107">Almacén de datos de SQL es un sistema distribuido diseñado tooperform analizar los datos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="be047-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="be047-108">Almacenamiento de datos de migración tooSQL requiere algunos cambios de diseño que no son demasiado difíciles de toounderstand pero pueden tardar algún tiempo tooimplement.</span><span class="sxs-lookup"><span data-stu-id="be047-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="be047-109">Si su empresa requiere un almacenamiento de datos de clase empresarial, Hola ventajas son la pena Hola.</span><span class="sxs-lookup"><span data-stu-id="be047-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="be047-110">Sin embargo, si no necesita la potencia de Hola de almacenamiento de datos SQL, resulta más rentable toouse SQL Server o base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="be047-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="be047-111">Considere usar SQL Data Warehouse cuando:</span><span class="sxs-lookup"><span data-stu-id="be047-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="be047-112">Tenga uno o varios terabytes de datos</span><span class="sxs-lookup"><span data-stu-id="be047-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="be047-113">Análisis de plan toorun en grandes cantidades de datos</span><span class="sxs-lookup"><span data-stu-id="be047-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="be047-114">Necesita almacenamiento y proceso de hello capacidad tooscale</span><span class="sxs-lookup"><span data-stu-id="be047-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="be047-115">Desea que los costos de toosave colocando los recursos informáticos cuando no se necesitan.</span><span class="sxs-lookup"><span data-stu-id="be047-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="be047-116">No use SQL Data Warehouse para las cargas de trabajo operativas (OLTP) que tengan:</span><span class="sxs-lookup"><span data-stu-id="be047-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="be047-117">Una elevada frecuencia de lecturas y escrituras</span><span class="sxs-lookup"><span data-stu-id="be047-117">High frequency reads and writes</span></span>
- <span data-ttu-id="be047-118">Gran número de selecciones de singleton</span><span class="sxs-lookup"><span data-stu-id="be047-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="be047-119">Grandes volúmenes de inserción de filas únicas</span><span class="sxs-lookup"><span data-stu-id="be047-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="be047-120">Necesidades de procesamiento fila por fila</span><span class="sxs-lookup"><span data-stu-id="be047-120">Row by row processing needs</span></span>
- <span data-ttu-id="be047-121">Formatos incompatibles (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="be047-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="be047-122">Migración del plan de Hola</span><span class="sxs-lookup"><span data-stu-id="be047-122">Plan hello migration</span></span>

<span data-ttu-id="be047-123">Una vez que haya decidido toomigrate un tooSQL de solución almacenamiento de datos existente, es importante tooplan migración de hello antes de comenzar.</span><span class="sxs-lookup"><span data-stu-id="be047-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="be047-124">Uno de los objetivos de la planificación es tooensure los datos, los esquemas de tabla, y el código son compatibles con el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="be047-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="be047-125">Hay algunas diferencias de compatibilidad toowork alrededor de entre el sistema actual y el almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="be047-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="be047-126">Además, la migración de grandes cantidades de datos tooAzure lleva tiempo.</span><span class="sxs-lookup"><span data-stu-id="be047-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="be047-127">Un planeamiento cuidadoso acelera obtener su tooAzure de datos.</span><span class="sxs-lookup"><span data-stu-id="be047-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="be047-128">Otro objetivo de diseño es el diseño de toomake tooensure ajustes que la solución aprovecha las ventajas de rendimiento de las consultas alta Hola que almacenamiento de datos de SQL está diseñado tooprovide.</span><span class="sxs-lookup"><span data-stu-id="be047-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="be047-129">Diseñar los almacenes de datos para la escala presenta los patrones de diseño diferentes y enfoques tradicionales por lo que no siempre están Hola mejor.</span><span class="sxs-lookup"><span data-stu-id="be047-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="be047-130">Aunque puede realizar algunos ajustes de diseño después de la migración, realizar cambios antes de proceso de hello guardará más tarde.</span><span class="sxs-lookup"><span data-stu-id="be047-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="be047-131">tooperform una migración correcta, debe toomigrate los esquemas de tabla, el código y los datos.</span><span class="sxs-lookup"><span data-stu-id="be047-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="be047-132">Para instrucciones sobre estos temas de migración, consulte:</span><span class="sxs-lookup"><span data-stu-id="be047-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="be047-133">Migración de los esquemas</span><span class="sxs-lookup"><span data-stu-id="be047-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="be047-134">Migración del código</span><span class="sxs-lookup"><span data-stu-id="be047-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="be047-135">[Migración de los datos](sql-data-warehouse-migrate-data.md)</span><span class="sxs-lookup"><span data-stu-id="be047-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="be047-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be047-136">Next steps</span></span>
<span data-ttu-id="be047-137">Hola CAT (equipo de asesoramiento al cliente) también tiene alguna orientación excelente de almacenamiento de datos SQL, que publique a través de blogs.</span><span class="sxs-lookup"><span data-stu-id="be047-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="be047-138">Eche un vistazo a su artículo [migrar datos tooAzure almacenamiento de datos SQL en la práctica] [ Migrating data tooAzure SQL Data Warehouse in practice] para obtener instrucciones adicionales sobre la migración.</span><span class="sxs-lookup"><span data-stu-id="be047-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
