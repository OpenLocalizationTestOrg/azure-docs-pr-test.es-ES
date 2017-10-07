---
title: "esquemas definidos por el aaaUser en el almacén de datos de SQL | Documentos de Microsoft"
description: Sugerencias para usar los esquemas Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="d67c4-103">Esquemas definidos por el usuario en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d67c4-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="d67c4-104">Almacenamientos de datos tradicionales suelen usar bases de datos independientes toocreate los límites de aplicación en función de la carga de trabajo, dominio o seguridad.</span><span class="sxs-lookup"><span data-stu-id="d67c4-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="d67c4-105">Por ejemplo, un almacenamiento de datos de SQL Server tradicional podría incluir una base de datos provisional, una base de datos de almacenamiento de datos y algunas bases de datos data mart.</span><span class="sxs-lookup"><span data-stu-id="d67c4-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="d67c4-106">En esta topología, cada base de datos funciona como una carga de trabajo y el límite de seguridad de la arquitectura de Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="d67c4-107">Por el contrario, el almacenamiento de datos SQL se ejecuta como carga de trabajo del almacenamiento de datos todo de hello dentro de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="d67c4-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="d67c4-108">No se permiten las combinaciones entre bases de datos.</span><span class="sxs-lookup"><span data-stu-id="d67c4-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="d67c4-109">Por lo tanto, almacenamiento de datos de SQL espera que todas las tablas utilizadas por hello toobe de almacenamiento almacenado en una base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="d67c4-110">El Almacenamiento de datos SQL no admite consultas entre bases de datos de cualquier tipo.</span><span class="sxs-lookup"><span data-stu-id="d67c4-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="d67c4-111">Por lo tanto, las implementaciones de almacenamiento de datos que aprovechan este patrón deberá toobe revisado.</span><span class="sxs-lookup"><span data-stu-id="d67c4-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="d67c4-112">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="d67c4-112">Recommendations</span></span>
<span data-ttu-id="d67c4-113">Se trata de recomendaciones para consolidar los límites de cargas de trabajo, seguridad, dominio y funcionales con esquemas definidos por el usuario.</span><span class="sxs-lookup"><span data-stu-id="d67c4-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="d67c4-114">Usar la carga de trabajo de almacenamiento de datos completo de toorun de base de datos de un almacén de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d67c4-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="d67c4-115">Consolidar los datos almacenamiento entorno toouse un almacenamiento de datos SQL base de datos existente</span><span class="sxs-lookup"><span data-stu-id="d67c4-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="d67c4-116">Aproveche **esquemas definidos por el usuario** límites de hello tooprovide previamente implementado mediante bases de datos.</span><span class="sxs-lookup"><span data-stu-id="d67c4-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="d67c4-117">Si los esquemas definidos por el usuario no se han utilizado anteriormente, tendrá una pizarra limpia.</span><span class="sxs-lookup"><span data-stu-id="d67c4-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="d67c4-118">Basta con usar nombre de base de datos anterior de hello como base de Hola para los esquemas definidos por el usuario de base de datos de almacenamiento de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="d67c4-119">Si ya se han utilizado los esquemas, tienen algunas opciones:</span><span class="sxs-lookup"><span data-stu-id="d67c4-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="d67c4-120">Quitar los nombres de esquema heredado de Hola y empezar de cero</span><span class="sxs-lookup"><span data-stu-id="d67c4-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="d67c4-121">Conservar los nombres de esquema heredado de Hola por nombre de tabla de hello previamente pendiente esquema heredado nombre toohello</span><span class="sxs-lookup"><span data-stu-id="d67c4-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="d67c4-122">Conservar los nombres de esquema heredado de hello mediante la implementación de vistas de tabla de hello en un esquema adicional toore-crear la estructura de esquema antigua Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="d67c4-123">En la primera inspección opción 3 puede parecer opción más atractiva Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="d67c4-124">Sin embargo, el demonio de hello es detalladamente Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="d67c4-125">Las vistas son de solo lectura en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d67c4-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="d67c4-126">Cualquier modificación de datos o tabla tendría toobe realizada en la tabla de base de Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="d67c4-127">La opción 3 también introduce una capa de vistas en el sistema.</span><span class="sxs-lookup"><span data-stu-id="d67c4-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="d67c4-128">Conviene toogive este algunas consideraciones adicionales si se utilizan vistas ya parte de la arquitectura.</span><span class="sxs-lookup"><span data-stu-id="d67c4-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="d67c4-129">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="d67c4-129">Examples:</span></span>
<span data-ttu-id="d67c4-130">Implementar los esquemas definidos por el usuario en función de los nombres de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d67c4-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="d67c4-131">Conservar esquema heredado les da un nombre por previamente pendiente toohello nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="d67c4-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="d67c4-132">Utilizar esquemas para límite de carga de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-132">Use schemas for hello workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="d67c4-133">Conservar los nombres de esquemas heredados con vistas.</span><span class="sxs-lookup"><span data-stu-id="d67c4-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="d67c4-134">Cualquier cambio en la estrategia de esquema necesita una revisión del modelo de seguridad de Hola para base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="d67c4-135">En muchos casos es posible que el modelo de seguridad de hello toosimplify capaz de mediante la asignación de permisos en el nivel del esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="d67c4-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="d67c4-136">Si se requieren permisos más granulares, puede utilizar funciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d67c4-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d67c4-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d67c4-137">Next steps</span></span>
<span data-ttu-id="d67c4-138">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="d67c4-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
