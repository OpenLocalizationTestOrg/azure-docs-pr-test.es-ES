---
title: "¿aaaHow tooquery con SQL en la base de datos de Azure Cosmos? | Microsoft Docs"
description: "Obtenga información acerca de tooquery con datos de documentos con SQL en la base de datos de Azure Cosmos"
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
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="96f97-104">Azure Cosmos DB: Cómo tooquery mediante SQL?</span><span class="sxs-lookup"><span data-stu-id="96f97-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="96f97-105">base de datos de Azure Cosmos Hola [DocumentDB API](documentdb-introduction.md) admite consultar documentos mediante SQL.</span><span class="sxs-lookup"><span data-stu-id="96f97-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="96f97-106">En este artículo se proporciona un documento de ejemplo y dos consultas SQL de ejemplo y los resultados.</span><span class="sxs-lookup"><span data-stu-id="96f97-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="96f97-107">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="96f97-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="96f97-108">Consulta de datos con SQL</span><span class="sxs-lookup"><span data-stu-id="96f97-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="96f97-109">Documento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="96f97-109">Sample document</span></span>

<span data-ttu-id="96f97-110">las consultas SQL de Hello en este artículo usan Hola siguiente documento de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96f97-110">hello SQL queries in this article use hello following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="96f97-111">¿Dónde puedo ejecutar consultas SQL?</span><span class="sxs-lookup"><span data-stu-id="96f97-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="96f97-112">Puede ejecutar las consultas que utilizan Hola Explorador de datos en el portal de Azure, a través de Hola Hola [REST API y SDK](documentdb-sdk-dotnet.md), incluso hello y [Query playground](https://www.documentdb.com/sql/demo), que ejecutan las consultas en un conjunto de datos de ejemplo existente.</span><span class="sxs-lookup"><span data-stu-id="96f97-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="96f97-113">Para obtener más información sobre las consultas SQL, vea:</span><span class="sxs-lookup"><span data-stu-id="96f97-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="96f97-114">Consulta SQL y sintaxis SQL</span><span class="sxs-lookup"><span data-stu-id="96f97-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="96f97-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="96f97-115">Prerequisites</span></span>

<span data-ttu-id="96f97-116">En este tutorial se da por supuesto que tiene una colección y una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="96f97-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="96f97-117">¿No tiene nada de lo anterior?</span><span class="sxs-lookup"><span data-stu-id="96f97-117">Don't have any of those?</span></span> <span data-ttu-id="96f97-118">Hola completa [inicio rápido de 5 minutos](create-mongodb-nodejs.md) o hello [tutorial de programadores](tutorial-develop-mongodb.md) toocreate una cuenta y una colección.</span><span class="sxs-lookup"><span data-stu-id="96f97-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="96f97-119">Consulta 1 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="96f97-119">Example query 1</span></span>

<span data-ttu-id="96f97-120">Dado anterior de documento familia de ejemplo de Hola, después de la consulta SQL devuelve documentos Hola que coincide con el campo de Id. de hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="96f97-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="96f97-121">Puesto que es un `SELECT *` instrucción, la salida de hello de consulta de hello es documento JSON completo de hello:</span><span class="sxs-lookup"><span data-stu-id="96f97-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="96f97-122">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="96f97-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="96f97-123">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="96f97-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="96f97-124">Consulta 2 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="96f97-124">Example query 2</span></span>

<span data-ttu-id="96f97-125">consulta siguiente de Hello devuelve todos los nombres especificados de Hola de elementos secundarios de familia de hello cuyo identificador coincide con `WakefieldFamily` ordenadas por su calificación.</span><span class="sxs-lookup"><span data-stu-id="96f97-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="96f97-126">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="96f97-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="96f97-127">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="96f97-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="96f97-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96f97-128">Next steps</span></span>

<span data-ttu-id="96f97-129">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="96f97-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96f97-130">Ha aprendido cómo tooquery mediante SQL</span><span class="sxs-lookup"><span data-stu-id="96f97-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="96f97-131">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.</span><span class="sxs-lookup"><span data-stu-id="96f97-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="96f97-132">Distribución de datos global</span><span class="sxs-lookup"><span data-stu-id="96f97-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

