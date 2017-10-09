---
title: "Cosmos Azure DB: Cómo usar tooquery Hola API de documentos? | Microsoft Docs"
description: "Obtenga información acerca de tooquery con hello documentos API de base de datos de Azure Cosmos"
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
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="e867b-104">Azure Cosmos DB: Cómo tooquery con API para MongoDB?</span><span class="sxs-lookup"><span data-stu-id="e867b-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="e867b-105">base de datos de Azure Cosmos Hello [API para MongoDB](mongodb-introduction.md) admite [consultas de shell de MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="e867b-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="e867b-106">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e867b-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e867b-107">Consulta de datos con MongoDB</span><span class="sxs-lookup"><span data-stu-id="e867b-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="e867b-108">Documento de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-108">Sample document</span></span>

<span data-ttu-id="e867b-109">las consultas de Hello en este artículo usan Hola siguiente documento de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e867b-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="e867b-110"><a id="examplequery1"></a> Consulta 1 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="e867b-111">Dado anterior de documento familia de ejemplo de Hola, Hola siguiente consulta se devuelve documentos de Hola que coincide con el campo de Id. de hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="e867b-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="e867b-112">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e867b-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="e867b-113">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e867b-113">**Results**</span></span>

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

## <span data-ttu-id="e867b-114"><a id="examplequery2"></a>Consulta 2 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="e867b-115">consulta siguiente Hola devuelve a todos los elementos secundarios de hello en la familia de Hola.</span><span class="sxs-lookup"><span data-stu-id="e867b-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="e867b-116">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e867b-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="e867b-117">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e867b-117">**Results**</span></span>

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


## <span data-ttu-id="e867b-118"><a id="examplequery3"></a>Consulta 3 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="e867b-119">consulta de Hello siguiente devuelve todas las familias de Hola que están registradas.</span><span class="sxs-lookup"><span data-stu-id="e867b-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="e867b-120">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e867b-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="e867b-121">**Resultados** no se devolverá ningún documento.</span><span class="sxs-lookup"><span data-stu-id="e867b-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="e867b-122"><a id="examplequery4"></a>Consulta 4 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="e867b-123">consulta de Hello siguiente devuelve todas las familias de Hola que no están registradas.</span><span class="sxs-lookup"><span data-stu-id="e867b-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="e867b-124">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e867b-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="e867b-125">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e867b-125">**Results**</span></span>

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
<span data-ttu-id="e867b-126">}</span><span class="sxs-lookup"><span data-stu-id="e867b-126">}</span></span>

## <span data-ttu-id="e867b-127"><a id="examplequery5"></a>Consulta 5 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="e867b-128">consulta de Hello siguiente devuelve todas las familias de Hola que no están registradas y el estado es NY.</span><span class="sxs-lookup"><span data-stu-id="e867b-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="e867b-129">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e867b-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="e867b-130">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e867b-130">**Results**</span></span>

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
<span data-ttu-id="e867b-131">}</span><span class="sxs-lookup"><span data-stu-id="e867b-131">}</span></span>


## <span data-ttu-id="e867b-132"><a id="examplequery6"></a>Consulta 6 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="e867b-133">consulta siguiente Hola devuelve todas las familias de Hola donde grados de elementos secundarios son 8.</span><span class="sxs-lookup"><span data-stu-id="e867b-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="e867b-134">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e867b-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="e867b-135">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e867b-135">**Results**</span></span>

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
<span data-ttu-id="e867b-136">}</span><span class="sxs-lookup"><span data-stu-id="e867b-136">}</span></span>

## <span data-ttu-id="e867b-137"><a id="examplequery7"></a>Consulta 7 de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e867b-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="e867b-138">consulta de Hello siguiente devuelve todas las familias de Hola donde el tamaño de matriz de elementos secundarios es 3.</span><span class="sxs-lookup"><span data-stu-id="e867b-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="e867b-139">**Consultar**</span><span class="sxs-lookup"><span data-stu-id="e867b-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="e867b-140">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="e867b-140">**Results**</span></span>

<span data-ttu-id="e867b-141">No se devolverá ningún resultado, ya que no tenemos más de dos elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="e867b-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="e867b-142">Solo cuando el parámetro es 2 esta consulta se realizará correctamente y devolver documento "hello" completo.</span><span class="sxs-lookup"><span data-stu-id="e867b-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e867b-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e867b-143">Next steps</span></span>

<span data-ttu-id="e867b-144">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e867b-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e867b-145">Ha aprendido cómo tooquery con MongoDB</span><span class="sxs-lookup"><span data-stu-id="e867b-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="e867b-146">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.</span><span class="sxs-lookup"><span data-stu-id="e867b-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e867b-147">Distribución de datos global</span><span class="sxs-lookup"><span data-stu-id="e867b-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

