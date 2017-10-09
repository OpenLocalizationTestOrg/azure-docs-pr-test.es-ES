---
title: "¿aaaHow tooquery los datos de tabla en la base de datos de Azure Cosmos? | Microsoft Docs"
description: "Obtenga información acerca de los datos de la tabla en la base de datos de Azure Cosmos tooquery"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="ba84c-104">Azure Cosmos DB: Cómo Hola tooquery datos de la tabla mediante el uso de API de tabla (vista previa)?</span><span class="sxs-lookup"><span data-stu-id="ba84c-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="ba84c-105">base de datos de Azure Cosmos Hello [API de tabla](table-introduction.md) (vista previa) es compatible con OData y [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) consultas en los datos de clave/valor (tabla).</span><span class="sxs-lookup"><span data-stu-id="ba84c-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="ba84c-106">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="ba84c-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ba84c-107">Consultar datos con hello API de tabla</span><span class="sxs-lookup"><span data-stu-id="ba84c-107">Querying data with hello Table API</span></span>

<span data-ttu-id="ba84c-108">consultas de este artículo Hello usar Hola según muestra `People` tabla:</span><span class="sxs-lookup"><span data-stu-id="ba84c-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="ba84c-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="ba84c-109">PartitionKey</span></span> | <span data-ttu-id="ba84c-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="ba84c-110">RowKey</span></span> | <span data-ttu-id="ba84c-111">Email</span><span class="sxs-lookup"><span data-stu-id="ba84c-111">Email</span></span> | <span data-ttu-id="ba84c-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="ba84c-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba84c-113">Harp</span><span class="sxs-lookup"><span data-stu-id="ba84c-113">Harp</span></span> | <span data-ttu-id="ba84c-114">Walter</span><span class="sxs-lookup"><span data-stu-id="ba84c-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="ba84c-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="ba84c-115">425-555-0101</span></span> |
| <span data-ttu-id="ba84c-116">Smith</span><span class="sxs-lookup"><span data-stu-id="ba84c-116">Smith</span></span> | <span data-ttu-id="ba84c-117">Ben</span><span class="sxs-lookup"><span data-stu-id="ba84c-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="ba84c-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="ba84c-118">425-555-0102</span></span> |
| <span data-ttu-id="ba84c-119">Smith</span><span class="sxs-lookup"><span data-stu-id="ba84c-119">Smith</span></span> | <span data-ttu-id="ba84c-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="ba84c-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="ba84c-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="ba84c-121">425-555-0104</span></span> | 

<span data-ttu-id="ba84c-122">Dado que base de datos de Azure Cosmos es compatible con hello las API de almacenamiento de tabla de Azure, vea [consultar tablas y entidades] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) para obtener más información sobre cómo Hola tooquery mediante el uso de API de la tabla.</span><span class="sxs-lookup"><span data-stu-id="ba84c-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="ba84c-123">Para obtener más información sobre las capacidades de premium de Hola que ofrece la base de datos de Azure Cosmos, consulte [base de datos de Azure Cosmos: API de tabla](table-introduction.md) y [desarrollar con hello API de tabla en .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ba84c-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ba84c-124">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ba84c-124">Prerequisites</span></span>

<span data-ttu-id="ba84c-125">Para estos toowork consultas, debe tener una cuenta de base de datos de Azure Cosmos y tener datos de la entidad en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba84c-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="ba84c-126">¿No tiene nada de lo anterior?</span><span class="sxs-lookup"><span data-stu-id="ba84c-126">Don't have any of those?</span></span> <span data-ttu-id="ba84c-127">Hola completa [inicio rápido de cinco minutos](https://aka.ms/acdbtnetqs) o hello [tutorial de programadores](https://aka.ms/acdbtabletut) toocreate una cuenta y rellenar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ba84c-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="ba84c-128">Consultas en PartitionKey y RowKey</span><span class="sxs-lookup"><span data-stu-id="ba84c-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="ba84c-129">Dado que las propiedades PartitionKey y RowKey de hello forman la clave principal de una entidad, puede usar Hola después de la entidad de una sintaxis especial tooidentify hello:</span><span class="sxs-lookup"><span data-stu-id="ba84c-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="ba84c-130">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="ba84c-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="ba84c-131">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="ba84c-131">**Results**</span></span>

| <span data-ttu-id="ba84c-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="ba84c-132">PartitionKey</span></span> | <span data-ttu-id="ba84c-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="ba84c-133">RowKey</span></span> | <span data-ttu-id="ba84c-134">Email</span><span class="sxs-lookup"><span data-stu-id="ba84c-134">Email</span></span> | <span data-ttu-id="ba84c-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="ba84c-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba84c-136">Harp</span><span class="sxs-lookup"><span data-stu-id="ba84c-136">Harp</span></span> | <span data-ttu-id="ba84c-137">Walter</span><span class="sxs-lookup"><span data-stu-id="ba84c-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="ba84c-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="ba84c-138">425-555-0104</span></span> |

<span data-ttu-id="ba84c-139">Como alternativa, puede especificar estas propiedades como parte del programa Hola `$filter` opción, como se muestra en los pasos de la sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba84c-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="ba84c-140">Tenga en cuenta que los nombres de propiedad de clave de Hola y valores constantes distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ba84c-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="ba84c-141">Hola PartitionKey y RowKey propiedades son de tipo String.</span><span class="sxs-lookup"><span data-stu-id="ba84c-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="ba84c-142">Consultas mediante un filtro de OData</span><span class="sxs-lookup"><span data-stu-id="ba84c-142">Query by using an OData filter</span></span>
<span data-ttu-id="ba84c-143">Al construir una cadena de filtro, tenga en cuenta estas reglas:</span><span class="sxs-lookup"><span data-stu-id="ba84c-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="ba84c-144">Usar operadores lógicos Hola definidos por la especificación de Protocolo OData toocompare un valor de propiedad tooa Hola.</span><span class="sxs-lookup"><span data-stu-id="ba84c-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="ba84c-145">Tenga en cuenta que no se puede comparar un valor dinámico de tooa de propiedad.</span><span class="sxs-lookup"><span data-stu-id="ba84c-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="ba84c-146">Un lado de la expresión de hello debe ser una constante.</span><span class="sxs-lookup"><span data-stu-id="ba84c-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="ba84c-147">nombre de la propiedad de Hello, operador y valor constante deben estar separados por espacios codificados de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="ba84c-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="ba84c-148">Para codificar un espacio con codificación URL se usa `%20`.</span><span class="sxs-lookup"><span data-stu-id="ba84c-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="ba84c-149">Todas las partes de la cadena de filtro de hello distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ba84c-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="ba84c-150">valor constante de Hello debe ser de hello como propiedad Hola para resultados válidos de hello filtro tooreturn de tipo de datos mismas.</span><span class="sxs-lookup"><span data-stu-id="ba84c-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="ba84c-151">Para obtener más información acerca de los tipos de propiedad admitidos, consulte [Hola de entender el modelo de datos del servicio de tabla](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="ba84c-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="ba84c-152">Esta es una consulta de ejemplo que muestra cómo toofilter por Hola PartitionKey y propiedades de correo electrónico mediante el uso de una OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="ba84c-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="ba84c-153">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="ba84c-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="ba84c-154">Para obtener más información sobre cómo tooconstruct filtrar expresiones para diversos tipos de datos, vea [consultar tablas y entidades](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="ba84c-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="ba84c-155">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="ba84c-155">**Results**</span></span>

| <span data-ttu-id="ba84c-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="ba84c-156">PartitionKey</span></span> | <span data-ttu-id="ba84c-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="ba84c-157">RowKey</span></span> | <span data-ttu-id="ba84c-158">Email</span><span class="sxs-lookup"><span data-stu-id="ba84c-158">Email</span></span> | <span data-ttu-id="ba84c-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="ba84c-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba84c-160">Ben</span><span class="sxs-lookup"><span data-stu-id="ba84c-160">Ben</span></span> |<span data-ttu-id="ba84c-161">Smith</span><span class="sxs-lookup"><span data-stu-id="ba84c-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="ba84c-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="ba84c-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="ba84c-163">Consultas con LINQ</span><span class="sxs-lookup"><span data-stu-id="ba84c-163">Query by using LINQ</span></span> 
<span data-ttu-id="ba84c-164">También puede consultar mediante el uso de LINQ, que traduce las expresiones de consulta OData correspondientes toohello.</span><span class="sxs-lookup"><span data-stu-id="ba84c-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="ba84c-165">Este es un ejemplo de cómo toobuild consultas mediante Hola .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="ba84c-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a><span data-ttu-id="ba84c-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba84c-166">Next steps</span></span>

<span data-ttu-id="ba84c-167">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="ba84c-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ba84c-168">Aprender cómo tooquery mediante el uso de Hola API de tabla (vista previa)</span><span class="sxs-lookup"><span data-stu-id="ba84c-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="ba84c-169">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.</span><span class="sxs-lookup"><span data-stu-id="ba84c-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ba84c-170">Distribución de datos global</span><span class="sxs-lookup"><span data-stu-id="ba84c-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
