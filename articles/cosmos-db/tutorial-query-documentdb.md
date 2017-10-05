---
title: "¿Cómo realizar consultas con SQL en Azure Cosmos DB? | Microsoft Docs"
description: Aprenda a realizar consultas con datos de DocumentDB con SQL en Azure Cosmos DB
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="e752f-104">Azure Cosmos DB: ¿cómo realizar consultas mediante SQL?</span><span class="sxs-lookup"><span data-stu-id="e752f-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="e752f-105">La [API de DocumentDB](documentdb-introduction.md) de Azure Cosmos DB admite la consulta de documentos mediante SQL.</span><span class="sxs-lookup"><span data-stu-id="e752f-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="e752f-106">En este artículo se proporciona un documento de ejemplo y dos consultas SQL de ejemplo y los resultados.</span><span class="sxs-lookup"><span data-stu-id="e752f-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="e752f-107">En este artículo se tratan las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="e752f-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e752f-108">Consulta de datos con SQL</span><span class="sxs-lookup"><span data-stu-id="e752f-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="e752f-109">Documento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e752f-109">Sample document</span></span>

<span data-ttu-id="e752f-110">En las consultas SQL de este artículo se usa el documento de ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e752f-110">The SQL queries in this article use the following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="e752f-111">¿Dónde puedo ejecutar consultas SQL?</span><span class="sxs-lookup"><span data-stu-id="e752f-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="e752f-112">Puede ejecutar consultas mediante el Explorador de datos en Azure Portal, a través de la [API de REST y los SDK](documentdb-sdk-dotnet.md) e incluso el [Query playground](https://www.documentdb.com/sql/demo) (Área de consultas), que ejecuta consultas sobre un conjunto existente de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e752f-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="e752f-113">Para obtener más información sobre las consultas SQL, vea:</span><span class="sxs-lookup"><span data-stu-id="e752f-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="e752f-114">Consulta SQL y sintaxis SQL</span><span class="sxs-lookup"><span data-stu-id="e752f-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="e752f-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e752f-115">Prerequisites</span></span>

<span data-ttu-id="e752f-116">En este tutorial se da por supuesto que tiene una colección y una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e752f-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="e752f-117">¿No tiene nada de lo anterior?</span><span class="sxs-lookup"><span data-stu-id="e752f-117">Don't have any of those?</span></span> <span data-ttu-id="e752f-118">Complete el [inicio rápido en 5 minutos](create-mongodb-nodejs.md) o el [tutorial de desarrolladores](tutorial-develop-mongodb.md) para crear una cuenta y una colección.</span><span class="sxs-lookup"><span data-stu-id="e752f-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="e752f-119">Consulta 1 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e752f-119">Example query 1</span></span>

<span data-ttu-id="e752f-120">Dado el documento de familia de ejemplo anterior, la consulta SQL siguiente devuelve los documentos donde el campo Id. coincide con `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="e752f-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="e752f-121">Puesto que es una instrucción `SELECT *`, la salida de la consulta es el documento JSON completo:</span><span class="sxs-lookup"><span data-stu-id="e752f-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="e752f-122">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e752f-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="e752f-123">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e752f-123">**Results**</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a><span data-ttu-id="e752f-124">Consulta 2 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e752f-124">Example query 2</span></span>

<span data-ttu-id="e752f-125">La consulta siguiente devuelve todos los nombres proporcionados de los elementos secundarios de la familia cuyo id. coincida con `WakefieldFamily`, ordenados por su grado.</span><span class="sxs-lookup"><span data-stu-id="e752f-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="e752f-126">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e752f-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="e752f-127">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e752f-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="e752f-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e752f-128">Next steps</span></span>

<span data-ttu-id="e752f-129">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e752f-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e752f-130">Ha obtenido información sobre cómo realizar consultas con SQL</span><span class="sxs-lookup"><span data-stu-id="e752f-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="e752f-131">Ahora puede continuar con el tutorial siguiente para obtener información sobre cómo distribuir sus datos globalmente.</span><span class="sxs-lookup"><span data-stu-id="e752f-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e752f-132">Distribución de datos global</span><span class="sxs-lookup"><span data-stu-id="e752f-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

