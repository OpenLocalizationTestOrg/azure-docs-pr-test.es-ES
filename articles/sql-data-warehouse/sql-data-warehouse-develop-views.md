---
title: Uso de vistas T-SQL en Azure SQL Data Warehouse | Microsoft Docs
description: Sugerencias para usar las vistas Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="a5d3b-103">Vistas en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a5d3b-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="a5d3b-104">Las vistas son especialmente útiles en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="a5d3b-105">Se pueden usar de formas diferentes para mejorar la calidad de la solución.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="a5d3b-106">Este artículo resalta algunos ejemplos de cómo enriquecer su solución con vistas, así como las limitaciones que se deben tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="a5d3b-107">En este artículo no se explica la sintaxis de `CREATE VIEW`.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="a5d3b-108">Consulte el artículo [CREATE VIEW][CREATE VIEW] de MSDN para esta información de referencia.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="a5d3b-109">Abstracción de arquitectura</span><span class="sxs-lookup"><span data-stu-id="a5d3b-109">Architectural abstraction</span></span>
<span data-ttu-id="a5d3b-110">Se trata de un patrón de aplicación muy común para volver a crear tablas con la característica CREATE TABLE AS SELECT (CTAS) seguida de un patrón de cambio de nombre de objetos mientras se cargan los datos.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="a5d3b-111">En el ejemplo siguiente se agregan registros de fecha nuevos a una dimensión de fecha.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="a5d3b-112">Observe cómo una nueva tabla, DimDate_New, se crea por primera vez y luego cambia de nombre para reemplazar la versión original de la tabla.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="a5d3b-113">Sin embargo, este enfoque puede provocar que las tablas aparezcan y desaparezcan de la vista del usuario, así como mensajes de error del tipo "la tabla no existe".</span><span class="sxs-lookup"><span data-stu-id="a5d3b-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="a5d3b-114">Las vistas pueden utilizarse para proporcionar una capa de presentación coherente mientras se cambia el nombre de los objetos subyacentes.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="a5d3b-115">Proporcionar a los usuarios acceso a los datos mediante vistas significa que los usuarios no necesitan tener visibilidad de las tablas subyacentes.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="a5d3b-116">Esto proporciona una experiencia de usuario coherente, al tiempo que garantiza que los diseñadores de almacenamiento de datos puedan desarrollar el modelo de datos y maximizar el rendimiento mediante el uso de CTAS durante el proceso de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="a5d3b-117">Optimización del rendimiento</span><span class="sxs-lookup"><span data-stu-id="a5d3b-117">Performance optimization</span></span>
<span data-ttu-id="a5d3b-118">Las vistas se pueden usar también para aplicar combinaciones de rendimiento optimizado entre tablas.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="a5d3b-119">Por ejemplo, una vista puede incorporar una clave de distribución redundante como parte de los criterios de combinación para minimizar el movimiento de datos.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="a5d3b-120">Otra ventaja de una vista podría ser forzar una consulta específica o una sugerencia de combinación.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="a5d3b-121">La utilización de vistas de esta manera garantiza que las combinaciones siempre se realizarán de manera óptima, evitando la necesidad de los usuarios de recordar la construcción correcta de sus combinaciones.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="a5d3b-122">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="a5d3b-122">Limitations</span></span>
<span data-ttu-id="a5d3b-123">Las vistas en el almacenamiento de datos SQL son solo metadatos.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="a5d3b-124">Por lo tanto, no están disponibles las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="a5d3b-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="a5d3b-125">No hay ninguna opción de enlace de esquema.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-125">There is no schema binding option</span></span>
* <span data-ttu-id="a5d3b-126">Las tablas base no se puede actualizar a través de la vista.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="a5d3b-127">No se pueden crear vistas en tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="a5d3b-128">No hay compatibilidad con las sugerencias EXPAND y NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="a5d3b-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="a5d3b-129">No hay ninguna vista indexada en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a5d3b-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5d3b-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5d3b-130">Next steps</span></span>
<span data-ttu-id="a5d3b-131">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a5d3b-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="a5d3b-132">Para la sintaxis de `CREATE VIEW`, consulte [CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="a5d3b-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
