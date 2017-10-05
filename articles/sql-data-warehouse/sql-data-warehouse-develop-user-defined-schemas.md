---
title: Esquemas definidos por el usuario en SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="80717-103">Esquemas definidos por el usuario en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="80717-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="80717-104">Los almacenamientos de datos tradicionales suelen utilizar bases de datos independientes para crear los límites de la aplicación en función de la carga de trabajo, el dominio o la seguridad.</span><span class="sxs-lookup"><span data-stu-id="80717-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="80717-105">Por ejemplo, un almacenamiento de datos de SQL Server tradicional podría incluir una base de datos provisional, una base de datos de almacenamiento de datos y algunas bases de datos data mart.</span><span class="sxs-lookup"><span data-stu-id="80717-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="80717-106">En esta topología, cada base de datos funciona como una carga de trabajo y el límite de seguridad de la arquitectura.</span><span class="sxs-lookup"><span data-stu-id="80717-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="80717-107">Por el contrario, el Almacenamiento de datos SQL ejecuta la carga de trabajo completa del almacenamiento de datos dentro de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="80717-108">No se permiten las combinaciones entre bases de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="80717-109">Por lo tanto, el Almacenamiento de datos SQL espera que todas las tablas que el almacenamiento utiliza se almacenen en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="80717-110">El Almacenamiento de datos SQL no admite consultas entre bases de datos de cualquier tipo.</span><span class="sxs-lookup"><span data-stu-id="80717-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="80717-111">En consecuencia, deben revisarse las implementaciones de almacenamiento de datos que utilizan este patrón.</span><span class="sxs-lookup"><span data-stu-id="80717-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="80717-112">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="80717-112">Recommendations</span></span>
<span data-ttu-id="80717-113">Se trata de recomendaciones para consolidar los límites de cargas de trabajo, seguridad, dominio y funcionales con esquemas definidos por el usuario.</span><span class="sxs-lookup"><span data-stu-id="80717-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="80717-114">Use una base de datos de Almacenamiento de datos SQL para ejecutar la carga de trabajo completa del almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="80717-115">Consolide el entorno de almacenamiento de datos existente para utilizar una base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="80717-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="80717-116">Utilice **esquemas definidos por el usuario** para proporcionar el límite implementado anteriormente con las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="80717-117">Si los esquemas definidos por el usuario no se han utilizado anteriormente, tendrá una pizarra limpia.</span><span class="sxs-lookup"><span data-stu-id="80717-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="80717-118">Utilice simplemente el nombre anterior de la base de datos como base para los esquemas definidos por el usuario en la base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="80717-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="80717-119">Si ya se han utilizado los esquemas, tienen algunas opciones:</span><span class="sxs-lookup"><span data-stu-id="80717-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="80717-120">Quitar los nombres de esquemas heredados y empezar desde cero.</span><span class="sxs-lookup"><span data-stu-id="80717-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="80717-121">Conservar los nombres de esquemas heredados anteponiendo el nombre de esquema heredado al nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="80717-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="80717-122">Conservar los nombres de esquemas heredados mediante la implementación de vistas sobre la tabla en un esquema adicional para volver a crear la estructura del esquema anterior.</span><span class="sxs-lookup"><span data-stu-id="80717-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="80717-123">En la primera inspección, la opción 3 puede resultar la opción más atractiva.</span><span class="sxs-lookup"><span data-stu-id="80717-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="80717-124">No obstante, el problema radica en los detalles.</span><span class="sxs-lookup"><span data-stu-id="80717-124">However, the devil is in the detail.</span></span> <span data-ttu-id="80717-125">Las vistas son de solo lectura en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="80717-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="80717-126">Cualquier modificación de datos o tablas tendría que realizarse según la tabla de base.</span><span class="sxs-lookup"><span data-stu-id="80717-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="80717-127">La opción 3 también introduce una capa de vistas en el sistema.</span><span class="sxs-lookup"><span data-stu-id="80717-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="80717-128">Desea incorporar algunas más a pesar de que ya utiliza vistas en la arquitectura.</span><span class="sxs-lookup"><span data-stu-id="80717-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="80717-129">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="80717-129">Examples:</span></span>
<span data-ttu-id="80717-130">Implementar los esquemas definidos por el usuario en función de los nombres de base de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="80717-131">Conservar los nombres de esquemas heredados anteponiendo estos nombres al nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="80717-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="80717-132">Utilizar esquemas para el límite de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="80717-132">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="80717-133">Conservar los nombres de esquemas heredados con vistas.</span><span class="sxs-lookup"><span data-stu-id="80717-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="80717-134">Cualquier cambio en la estrategia de esquema necesita una revisión del modelo de seguridad de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="80717-135">En muchos casos puede simplificar el modelo de seguridad mediante la asignación de permisos a nivel de esquema.</span><span class="sxs-lookup"><span data-stu-id="80717-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="80717-136">Si se requieren permisos más granulares, puede utilizar funciones de base de datos.</span><span class="sxs-lookup"><span data-stu-id="80717-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="80717-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80717-137">Next steps</span></span>
<span data-ttu-id="80717-138">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="80717-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
