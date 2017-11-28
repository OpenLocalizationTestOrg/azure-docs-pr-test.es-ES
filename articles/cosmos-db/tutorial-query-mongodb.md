---
title: "Azure Cosmos DB: ¿cómo realizar consultas mediante DocumentDB API? | Microsoft Docs"
description: Aprenda a realizar consultas con la DocumentDB API para Azure Cosmos DB
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: feffc553a9aa931d96cec71c101674fce08a466b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-with-api-for-mongodb"></a><span data-ttu-id="829e8-104">Azure Cosmos DB: ¿cómo realizar consultas con la API para MongoDB?</span><span class="sxs-lookup"><span data-stu-id="829e8-104">Azure Cosmos DB: How to query with API for MongoDB?</span></span>

<span data-ttu-id="829e8-105">La [API para MongoDB](mongodb-introduction.md) de Azure Cosmos DB admite las [consultas de shell de MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="829e8-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="829e8-106">En este artículo se tratan las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="829e8-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="829e8-107">Consulta de datos con MongoDB</span><span class="sxs-lookup"><span data-stu-id="829e8-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="829e8-108">Documento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-108">Sample document</span></span>

<span data-ttu-id="829e8-109">En las consultas de este artículo se usa el documento de ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="829e8-109">The queries in this article use the following sample document.</span></span>

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
## <span data-ttu-id="829e8-110"><a id="examplequery1"></a> Consulta 1 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="829e8-111">Dado el documento de familia de ejemplo anterior, la consulta siguiente devuelve los documentos donde el campo Id. coincide con `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="829e8-111">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="829e8-112">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="829e8-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="829e8-113">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="829e8-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="829e8-114"><a id="examplequery2"></a>Consulta 2 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="829e8-115">La consulta siguiente devuelve todos los elementos secundarios de la familia.</span><span class="sxs-lookup"><span data-stu-id="829e8-115">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="829e8-116">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="829e8-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="829e8-117">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="829e8-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <span data-ttu-id="829e8-118"><a id="examplequery3"></a>Consulta 3 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="829e8-119">La consulta siguiente devuelve todas las familias que están registradas.</span><span class="sxs-lookup"><span data-stu-id="829e8-119">The next query returns all the families which are registered.</span></span> 

<span data-ttu-id="829e8-120">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="829e8-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="829e8-121">**Resultados** no se devolverá ningún documento.</span><span class="sxs-lookup"><span data-stu-id="829e8-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="829e8-122"><a id="examplequery4"></a>Consulta 4 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="829e8-123">La consulta siguiente devuelve todas las familias que no están registradas.</span><span class="sxs-lookup"><span data-stu-id="829e8-123">The next query returns all the families which are not registered.</span></span> 

<span data-ttu-id="829e8-124">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="829e8-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="829e8-125">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="829e8-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="829e8-126">}</span><span class="sxs-lookup"><span data-stu-id="829e8-126">}</span></span>

## <span data-ttu-id="829e8-127"><a id="examplequery5"></a>Consulta 5 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="829e8-128">La consulta siguiente devuelve todas las familias que no están registradas y el estado es NY.</span><span class="sxs-lookup"><span data-stu-id="829e8-128">The next query returns all the families which are not registered and state is NY.</span></span> 

<span data-ttu-id="829e8-129">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="829e8-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="829e8-130">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="829e8-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="829e8-131">}</span><span class="sxs-lookup"><span data-stu-id="829e8-131">}</span></span>


## <span data-ttu-id="829e8-132"><a id="examplequery6"></a>Consulta 6 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="829e8-133">La consulta siguiente devuelve todas las familias en las que los grados de los elementos secundarios son 8.</span><span class="sxs-lookup"><span data-stu-id="829e8-133">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="829e8-134">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="829e8-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="829e8-135">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="829e8-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="829e8-136">}</span><span class="sxs-lookup"><span data-stu-id="829e8-136">}</span></span>

## <span data-ttu-id="829e8-137"><a id="examplequery7"></a>Consulta 7 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="829e8-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="829e8-138">La consulta siguiente devuelve todas las familias en las que el valor de tamaño de la matriz secundaria es 3.</span><span class="sxs-lookup"><span data-stu-id="829e8-138">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="829e8-139">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="829e8-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="829e8-140">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="829e8-140">**Results**</span></span>

<span data-ttu-id="829e8-141">No se devolverá ningún resultado, ya que no tenemos más de dos elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="829e8-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="829e8-142">Solo si el parámetro es 2, esta consulta se realizará correctamente y devolverá el documento completo.</span><span class="sxs-lookup"><span data-stu-id="829e8-142">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="829e8-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="829e8-143">Next steps</span></span>

<span data-ttu-id="829e8-144">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="829e8-144">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="829e8-145">Ha obtenido información sobre cómo realizar consultas con MongoDB</span><span class="sxs-lookup"><span data-stu-id="829e8-145">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="829e8-146">Ahora puede continuar con el tutorial siguiente para obtener información sobre cómo distribuir sus datos globalmente.</span><span class="sxs-lookup"><span data-stu-id="829e8-146">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="829e8-147">Distribución de datos global</span><span class="sxs-lookup"><span data-stu-id="829e8-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

