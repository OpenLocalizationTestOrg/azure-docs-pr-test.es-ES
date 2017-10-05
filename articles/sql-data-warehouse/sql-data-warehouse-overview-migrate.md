---
title: "Migración de la solución a SQL Data Warehouse | Microsoft Docs"
description: "Guía de migración para llevar una solución a la plataforma Almacenamiento de datos SQL de Azure."
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
ms.openlocfilehash: 771b9456e66b8a1e41f72340b695b19e2adaf793
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-solution-to-azure-sql-data-warehouse"></a><span data-ttu-id="4a277-103">Migración de una solución a Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4a277-103">Migrate your solution to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="4a277-104">Vea lo que supone migrar una solución de base de datos existente a Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a277-104">See what's involved in migrating an existing database solution to Azure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="4a277-105">Generación del perfil de la carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="4a277-105">Profile your workload</span></span>
<span data-ttu-id="4a277-106">Antes de migrar, debería estar seguro de que SQL Data Warehouse sea la solución adecuada para su carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4a277-106">Before migrating, you want to be certain SQL Data Warehouse is the right solution for your workload.</span></span> <span data-ttu-id="4a277-107">SQL Data Warehouse es un sistema distribuido diseñado para realizar análisis con datos de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="4a277-107">SQL Data Warehouse is a distributed system designed to perform analytics on large data.</span></span>  <span data-ttu-id="4a277-108">Para migrar a SQL Data Warehouse, son necesarios algunos cambios de diseño que no son demasiado difíciles de entender, pero que pueden tardar algún tiempo en implementarse.</span><span class="sxs-lookup"><span data-stu-id="4a277-108">Migrating to SQL Data Warehouse requires some design changes that are not too hard to understand but might take some time to implement.</span></span> <span data-ttu-id="4a277-109">Si su negocio requiere un almacenamiento de datos de clase empresarial, las ventajas merecen la pena.</span><span class="sxs-lookup"><span data-stu-id="4a277-109">If your business requires an enterprise-class data warehouse, the benefits are worth the effort.</span></span> <span data-ttu-id="4a277-110">Sin embargo, si no necesita la capacidad de SQL Data Warehouse, es más rentable usar SQL Server o Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4a277-110">However, if you don't need the power of SQL Data Warehouse, it is more cost-effective to use SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="4a277-111">Considere usar SQL Data Warehouse cuando:</span><span class="sxs-lookup"><span data-stu-id="4a277-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="4a277-112">Tenga uno o varios terabytes de datos</span><span class="sxs-lookup"><span data-stu-id="4a277-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="4a277-113">Planee ejecutar análisis en grandes cantidades de datos</span><span class="sxs-lookup"><span data-stu-id="4a277-113">Plan to run analytics on large amounts of data</span></span>
- <span data-ttu-id="4a277-114">Necesite la capacidad de escalar el almacenamiento y los procesos</span><span class="sxs-lookup"><span data-stu-id="4a277-114">Need the ability to scale compute and storage</span></span> 
- <span data-ttu-id="4a277-115">Desee ahorrar costos pausando los recursos de procesos cuando no los necesite.</span><span class="sxs-lookup"><span data-stu-id="4a277-115">Want to save costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="4a277-116">No use SQL Data Warehouse para las cargas de trabajo operativas (OLTP) que tengan:</span><span class="sxs-lookup"><span data-stu-id="4a277-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="4a277-117">Una elevada frecuencia de lecturas y escrituras</span><span class="sxs-lookup"><span data-stu-id="4a277-117">High frequency reads and writes</span></span>
- <span data-ttu-id="4a277-118">Gran número de selecciones de singleton</span><span class="sxs-lookup"><span data-stu-id="4a277-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="4a277-119">Grandes volúmenes de inserción de filas únicas</span><span class="sxs-lookup"><span data-stu-id="4a277-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="4a277-120">Necesidades de procesamiento fila por fila</span><span class="sxs-lookup"><span data-stu-id="4a277-120">Row by row processing needs</span></span>
- <span data-ttu-id="4a277-121">Formatos incompatibles (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="4a277-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-the-migration"></a><span data-ttu-id="4a277-122">Planeamiento de la migración</span><span class="sxs-lookup"><span data-stu-id="4a277-122">Plan the migration</span></span>

<span data-ttu-id="4a277-123">Una vez que haya decidido migrar una solución existente a SQL Data Warehouse, es importante planear la migración antes de comenzar.</span><span class="sxs-lookup"><span data-stu-id="4a277-123">Once you have decided to migrate an existing solution to SQL Data Warehouse, it is important to plan the migration before getting started.</span></span> 

<span data-ttu-id="4a277-124">Uno de los objetivos del planeamiento es asegurarse de que los datos, los esquemas de tabla y el código sean compatibles con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a277-124">One goal of planning is to ensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="4a277-125">Existen algunas diferencias de compatibilidad que solventar entre el sistema actual y SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a277-125">There are some compatibility differences to work around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="4a277-126">Además, migrar grandes cantidades de datos a Azure lleva tiempo.</span><span class="sxs-lookup"><span data-stu-id="4a277-126">Plus, migrating large amounts of data to Azure takes time.</span></span> <span data-ttu-id="4a277-127">Un planeamiento cuidadoso permite pasar los datos a Azure más rápidamente.</span><span class="sxs-lookup"><span data-stu-id="4a277-127">Careful planning expedites getting your data to Azure.</span></span> 

<span data-ttu-id="4a277-128">Otro objetivo del planeamiento es realizar ajustes de diseño para asegurarse de que la solución aproveche el elevado rendimiento de consultas que SQL Data Warehouse está diseñado para proporcionar.</span><span class="sxs-lookup"><span data-stu-id="4a277-128">Another goal of planning is to make design adjustments to ensure your solution takes advantage of the high query performance SQL Data Warehouse is designed to provide.</span></span> <span data-ttu-id="4a277-129">El diseño del almacenamiento de datos para escala presenta diferentes patrones de diseño, de manera que los enfoques tradicionales no son siempre la mejor opción.</span><span class="sxs-lookup"><span data-stu-id="4a277-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="4a277-130">Aunque puede realizar algunos ajustes de diseño después de la migración, hacerlos antes en el proceso le ahorrará tiempo más adelante.</span><span class="sxs-lookup"><span data-stu-id="4a277-130">Although you can make some design adjustments after migration, making changes sooner in the process will save time later.</span></span>

<span data-ttu-id="4a277-131">Para llevar a cabo una migración correcta, debe migrar los esquemas de tabla, el código y los datos.</span><span class="sxs-lookup"><span data-stu-id="4a277-131">To perform a successful migration, you need to migrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="4a277-132">Para instrucciones sobre estos temas de migración, consulte:</span><span class="sxs-lookup"><span data-stu-id="4a277-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="4a277-133">Migración de los esquemas</span><span class="sxs-lookup"><span data-stu-id="4a277-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="4a277-134">Migración del código</span><span class="sxs-lookup"><span data-stu-id="4a277-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="4a277-135">[Migración de los datos](sql-data-warehouse-migrate-data.md)</span><span class="sxs-lookup"><span data-stu-id="4a277-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform the migration


## Deploy the solution


## Validate the migration

-->

## <a name="next-steps"></a><span data-ttu-id="4a277-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a277-136">Next steps</span></span>
<span data-ttu-id="4a277-137">El equipo de asesoramiento al cliente también cuenta con buenas directrices sobre SQL Data Warehouse, que publican a través de blogs.</span><span class="sxs-lookup"><span data-stu-id="4a277-137">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="4a277-138">Eche un vistazo a su artículo [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] (Migración de datos a Azure SQL Data Warehouse en la práctica) para obtener más instrucciones acerca de la migración.</span><span class="sxs-lookup"><span data-stu-id="4a277-138">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
