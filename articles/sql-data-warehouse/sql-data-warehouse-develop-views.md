---
title: "vistas de aaaUsing T-SQL en el almacén de datos de SQL de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="35677-103">Vistas en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="35677-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="35677-104">Las vistas son especialmente útiles en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="35677-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="35677-105">Que se puedan utilizar en un número de maneras diferentes tooimprove Hola de calidad de la solución.</span><span class="sxs-lookup"><span data-stu-id="35677-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="35677-106">Este artículo resalta algunos ejemplos de cómo tooenrich la solución con vistas, así como las limitaciones de Hola que necesitan toobe considera.</span><span class="sxs-lookup"><span data-stu-id="35677-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="35677-107">En este artículo no se explica la sintaxis de `CREATE VIEW`.</span><span class="sxs-lookup"><span data-stu-id="35677-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="35677-108">Consulte toohello [CREATE VIEW] [ CREATE VIEW] artículo de MSDN para obtener esta información de referencia.</span><span class="sxs-lookup"><span data-stu-id="35677-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="35677-109">Abstracción de arquitectura</span><span class="sxs-lookup"><span data-stu-id="35677-109">Architectural abstraction</span></span>
<span data-ttu-id="35677-110">Un modelo de aplicación muy común es toore-crear tablas mediante Crear tabla AS seleccione (CTAS) seguido por un objeto de cambiar el nombre de modelo durante la carga de datos.</span><span class="sxs-lookup"><span data-stu-id="35677-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="35677-111">ejemplo de Hola siguiente agrega dimensión de fecha nuevos registros tooa date.</span><span class="sxs-lookup"><span data-stu-id="35677-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="35677-112">Tenga en cuenta cómo un nuevo tabble, DimDate_New, se crea por primera vez y, a continuación, cambiar el nombre de versión original de hello tooreplace de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="35677-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="35677-113">Sin embargo, este enfoque puede provocar que las tablas aparezcan y desaparezcan de la vista del usuario, así como mensajes de error del tipo "la tabla no existe".</span><span class="sxs-lookup"><span data-stu-id="35677-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="35677-114">Vistas pueden ser usuarios de tooprovide usado con una capa de presentación coherente mientras se cambia el nombre de los objetos subyacentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="35677-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="35677-115">Proporcionando acceso a los usuarios toohello datos a través de una vista, significa que los usuarios no tienen visibilidad toohave de tablas subyacentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="35677-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="35677-116">Esto proporciona una experiencia coherente al usuario y garantizar que los diseñadores de almacenes de datos de hello pueden evolucionar modelo de datos de Hola y maximizar el rendimiento mediante el uso de CTAS durante el proceso de carga de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="35677-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="35677-117">Optimización del rendimiento</span><span class="sxs-lookup"><span data-stu-id="35677-117">Performance optimization</span></span>
<span data-ttu-id="35677-118">Vistas también pueden ser usadas tooenforce rendimiento optimizado combinaciones entre tablas.</span><span class="sxs-lookup"><span data-stu-id="35677-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="35677-119">Por ejemplo, una vista puede incorporar una clave de distribución redundante como parte del programa Hola a unir el movimiento de datos de toominimize de criterios.</span><span class="sxs-lookup"><span data-stu-id="35677-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="35677-120">Otra ventaja de una vista podría ser tooforce una consulta específica o una sugerencia de combinación.</span><span class="sxs-lookup"><span data-stu-id="35677-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="35677-121">Mediante vistas de esta manera se garantiza que las combinaciones se realizan siempre de forma óptima, evitando la necesidad de hello for (construcción correcta hello) a los usuarios tooremember para sus combinaciones.</span><span class="sxs-lookup"><span data-stu-id="35677-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="35677-122">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="35677-122">Limitations</span></span>
<span data-ttu-id="35677-123">Las vistas en el almacenamiento de datos SQL son solo metadatos.</span><span class="sxs-lookup"><span data-stu-id="35677-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="35677-124">Por consiguiente Hola siguientes opciones no está disponible:</span><span class="sxs-lookup"><span data-stu-id="35677-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="35677-125">No hay ninguna opción de enlace de esquema.</span><span class="sxs-lookup"><span data-stu-id="35677-125">There is no schema binding option</span></span>
* <span data-ttu-id="35677-126">Tablas base no se puede actualizar a través de la vista de Hola</span><span class="sxs-lookup"><span data-stu-id="35677-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="35677-127">No se pueden crear vistas en tablas temporales.</span><span class="sxs-lookup"><span data-stu-id="35677-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="35677-128">No hay compatibilidad para hello expandir / sugerencias NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="35677-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="35677-129">No hay ninguna vista indexada en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="35677-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="35677-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35677-130">Next steps</span></span>
<span data-ttu-id="35677-131">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="35677-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="35677-132">Para `CREATE VIEW` sintaxis consulte demasiado[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="35677-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
