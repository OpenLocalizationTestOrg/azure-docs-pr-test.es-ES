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
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Azure Cosmos DB: Cómo tooquery con API para MongoDB?

base de datos de Azure Cosmos Hello [API para MongoDB](mongodb-introduction.md) admite [consultas de shell de MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/). 

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Consulta de datos con MongoDB

## <a name="sample-document"></a>Documento de ejemplo

las consultas de Hello en este artículo usan Hola siguiente documento de ejemplo.

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
## <a id="examplequery1"></a> Consulta 1 de ejemplo 

Dado anterior de documento familia de ejemplo de Hola, Hola siguiente consulta se devuelve documentos de Hola que coincide con el campo de Id. de hello `WakefieldFamily`.

**Consultar**
    
    db.families.find({ id: “WakefieldFamily”})

**Resultados**

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

## <a id="examplequery2"></a>Consulta 2 de ejemplo 

consulta siguiente Hola devuelve a todos los elementos secundarios de hello en la familia de Hola. 

**Consultar**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**Resultados**

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


## <a id="examplequery3"></a>Consulta 3 de ejemplo 

consulta de Hello siguiente devuelve todas las familias de Hola que están registradas. 

**Consultar**
    
    db.families.find( { "isRegistered" : true })
**Resultados** no se devolverá ningún documento. 

## <a id="examplequery4"></a>Consulta 4 de ejemplo

consulta de Hello siguiente devuelve todas las familias de Hola que no están registradas. 

**Consultar**
    
    db.families.find( { "isRegistered" : false })
**Resultados**

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
}

## <a id="examplequery5"></a>Consulta 5 de ejemplo

consulta de Hello siguiente devuelve todas las familias de Hola que no están registradas y el estado es NY. 

**Consultar**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**Resultados**

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
}


## <a id="examplequery6"></a>Consulta 6 de ejemplo

consulta siguiente Hola devuelve todas las familias de Hola donde grados de elementos secundarios son 8.

**Consultar**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**Resultados**

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
}

## <a id="examplequery7"></a>Consulta 7 de ejemplo

consulta de Hello siguiente devuelve todas las familias de Hola donde el tamaño de matriz de elementos secundarios es 3.

**Consultar**
  
      db.Family.find( {children: { $size:3} } )

**Resultados**

No se devolverá ningún resultado, ya que no tenemos más de dos elementos secundarios. Solo cuando el parámetro es 2 esta consulta se realizará correctamente y devolver documento "hello" completo.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Ha aprendido cómo tooquery con MongoDB 

Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.

> [!div class="nextstepaction"]
> [Distribución de datos global](tutorial-global-distribution-documentdb.md)

