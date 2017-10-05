---
title: "¿Cómo consultar datos de tabla en Azure Cosmos DB? | Microsoft Docs"
description: Aprender a consultar datos de tabla en Azure Cosmos DB
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
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="dcb25-104">Azure Cosmos DB: instrucciones de realización de consultas de tablas de datos con Table API (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="dcb25-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="dcb25-105">[Table API](table-introduction.md) (versión preliminar) de Azure Cosmos DB admite consultas de OData y [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) en los datos de clave-valor (tabla).</span><span class="sxs-lookup"><span data-stu-id="dcb25-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="dcb25-106">En este artículo se tratan las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="dcb25-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="dcb25-107">Consulta de datos con Table API</span><span class="sxs-lookup"><span data-stu-id="dcb25-107">Querying data with the Table API</span></span>

<span data-ttu-id="dcb25-108">En las consultas de este artículo se usa la tabla `People` de ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dcb25-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="dcb25-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="dcb25-109">PartitionKey</span></span> | <span data-ttu-id="dcb25-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="dcb25-110">RowKey</span></span> | <span data-ttu-id="dcb25-111">Email</span><span class="sxs-lookup"><span data-stu-id="dcb25-111">Email</span></span> | <span data-ttu-id="dcb25-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="dcb25-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dcb25-113">Harp</span><span class="sxs-lookup"><span data-stu-id="dcb25-113">Harp</span></span> | <span data-ttu-id="dcb25-114">Walter</span><span class="sxs-lookup"><span data-stu-id="dcb25-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="dcb25-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="dcb25-115">425-555-0101</span></span> |
| <span data-ttu-id="dcb25-116">Smith</span><span class="sxs-lookup"><span data-stu-id="dcb25-116">Smith</span></span> | <span data-ttu-id="dcb25-117">Ben</span><span class="sxs-lookup"><span data-stu-id="dcb25-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="dcb25-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="dcb25-118">425-555-0102</span></span> |
| <span data-ttu-id="dcb25-119">Smith</span><span class="sxs-lookup"><span data-stu-id="dcb25-119">Smith</span></span> | <span data-ttu-id="dcb25-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="dcb25-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="dcb25-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="dcb25-121">425-555-0104</span></span> | 

<span data-ttu-id="dcb25-122">Puesto que Azure Cosmos DB es compatible con las API de Azure Table Storage, consulte [Consulta de tablas y entidades](https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) para obtener información sobre cómo realizar consultas con Table API.</span><span class="sxs-lookup"><span data-stu-id="dcb25-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="dcb25-123">Para obtener más información sobre las funcionalidades premium que ofrece Azure Cosmos DB, consulte [Azure Cosmos DB: Table API](table-introduction.md) y [Azure Cosmos DB: desarrollo con Table API en .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dcb25-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dcb25-124">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dcb25-124">Prerequisites</span></span>

<span data-ttu-id="dcb25-125">Para que estas consultas funcionen, debe tener una cuenta de Azure Cosmos DB, así como datos de la entidad en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="dcb25-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="dcb25-126">¿No tiene nada de lo anterior?</span><span class="sxs-lookup"><span data-stu-id="dcb25-126">Don't have any of those?</span></span> <span data-ttu-id="dcb25-127">Efectúe el [inicio rápido en cinco minutos](https://aka.ms/acdbtnetqs) o siga el [tutorial de desarrolladores](https://aka.ms/acdbtabletut) para crear una cuenta y rellenar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dcb25-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="dcb25-128">Consultas en PartitionKey y RowKey</span><span class="sxs-lookup"><span data-stu-id="dcb25-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="dcb25-129">Dado que las propiedades PartitionKey y RowKey forman la clave principal de una entidad, puede usar la siguiente sintaxis especial para identificar dicha entidad:</span><span class="sxs-lookup"><span data-stu-id="dcb25-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="dcb25-130">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="dcb25-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="dcb25-131">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="dcb25-131">**Results**</span></span>

| <span data-ttu-id="dcb25-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="dcb25-132">PartitionKey</span></span> | <span data-ttu-id="dcb25-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="dcb25-133">RowKey</span></span> | <span data-ttu-id="dcb25-134">Email</span><span class="sxs-lookup"><span data-stu-id="dcb25-134">Email</span></span> | <span data-ttu-id="dcb25-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="dcb25-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dcb25-136">Harp</span><span class="sxs-lookup"><span data-stu-id="dcb25-136">Harp</span></span> | <span data-ttu-id="dcb25-137">Walter</span><span class="sxs-lookup"><span data-stu-id="dcb25-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="dcb25-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="dcb25-138">425-555-0104</span></span> |

<span data-ttu-id="dcb25-139">Como alternativa, puede especificar estas propiedades como parte de la opción `$filter`, tal y como se muestra en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="dcb25-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="dcb25-140">Tenga en cuenta que los nombres de propiedad de clave y los valores constantes distinguen entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="dcb25-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="dcb25-141">Las propiedades PartitionKey y RowKey son de tipo String.</span><span class="sxs-lookup"><span data-stu-id="dcb25-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="dcb25-142">Consultas mediante un filtro de OData</span><span class="sxs-lookup"><span data-stu-id="dcb25-142">Query by using an OData filter</span></span>
<span data-ttu-id="dcb25-143">Al construir una cadena de filtro, tenga en cuenta estas reglas:</span><span class="sxs-lookup"><span data-stu-id="dcb25-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="dcb25-144">Utilice los operadores lógicos definidos por la especificación del protocolo OData para comparar una propiedad con un valor.</span><span class="sxs-lookup"><span data-stu-id="dcb25-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="dcb25-145">Tenga en cuenta que no puede comparar una propiedad con un valor dinámico.</span><span class="sxs-lookup"><span data-stu-id="dcb25-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="dcb25-146">Un lado de la expresión debe ser una constante.</span><span class="sxs-lookup"><span data-stu-id="dcb25-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="dcb25-147">El nombre de la propiedad, el operador y el valor constante se deben separar por espacios con codificación URL.</span><span class="sxs-lookup"><span data-stu-id="dcb25-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="dcb25-148">Para codificar un espacio con codificación URL se usa `%20`.</span><span class="sxs-lookup"><span data-stu-id="dcb25-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="dcb25-149">Todas las partes de la cadena de filtro distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="dcb25-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="dcb25-150">Para que el filtro devuelva resultados válidos, el valor constante debe ser del mismo tipo de datos que la propiedad.</span><span class="sxs-lookup"><span data-stu-id="dcb25-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="dcb25-151">Para obtener más información sobre los tipos de propiedades que se admiten, consulte [Introducción al modelo de datos del servicio Tabla](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="dcb25-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="dcb25-152">Esta es una consulta de ejemplo en la que se muestra cómo filtrar por propiedades PartitionKey e Email con un elemento `$filter` de OData.</span><span class="sxs-lookup"><span data-stu-id="dcb25-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="dcb25-153">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="dcb25-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="dcb25-154">Para obtener más información sobre cómo construir expresiones de filtro para diferentes tipos de datos, consulte [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities) (Consulta de tablas y entidades).</span><span class="sxs-lookup"><span data-stu-id="dcb25-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="dcb25-155">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="dcb25-155">**Results**</span></span>

| <span data-ttu-id="dcb25-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="dcb25-156">PartitionKey</span></span> | <span data-ttu-id="dcb25-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="dcb25-157">RowKey</span></span> | <span data-ttu-id="dcb25-158">Email</span><span class="sxs-lookup"><span data-stu-id="dcb25-158">Email</span></span> | <span data-ttu-id="dcb25-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="dcb25-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dcb25-160">Ben</span><span class="sxs-lookup"><span data-stu-id="dcb25-160">Ben</span></span> |<span data-ttu-id="dcb25-161">Smith</span><span class="sxs-lookup"><span data-stu-id="dcb25-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="dcb25-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="dcb25-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="dcb25-163">Consultas con LINQ</span><span class="sxs-lookup"><span data-stu-id="dcb25-163">Query by using LINQ</span></span> 
<span data-ttu-id="dcb25-164">También puede realizar consultas con LINQ, que se traduce a las correspondientes expresiones de consulta de OData.</span><span class="sxs-lookup"><span data-stu-id="dcb25-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="dcb25-165">Este es un ejemplo de cómo compilar consultas mediante el SDK de .NET:</span><span class="sxs-lookup"><span data-stu-id="dcb25-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dcb25-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dcb25-166">Next steps</span></span>

<span data-ttu-id="dcb25-167">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dcb25-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dcb25-168">Ha aprendido a realizar consultas mediante Table API (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="dcb25-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="dcb25-169">Ahora puede continuar con el tutorial siguiente para obtener información sobre cómo distribuir sus datos globalmente.</span><span class="sxs-lookup"><span data-stu-id="dcb25-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dcb25-170">Distribución de datos global</span><span class="sxs-lookup"><span data-stu-id="dcb25-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
