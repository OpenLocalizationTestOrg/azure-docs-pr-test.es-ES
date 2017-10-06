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
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB: Cómo tooquery mediante SQL?

base de datos de Azure Cosmos Hola [DocumentDB API](documentdb-introduction.md) admite consultar documentos mediante SQL. En este artículo se proporciona un documento de ejemplo y dos consultas SQL de ejemplo y los resultados.

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Consulta de datos con SQL

## <a name="sample-document"></a>Documento de ejemplo

las consultas SQL de Hello en este artículo usan Hola siguiente documento de ejemplo.

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
## <a name="where-can-i-run-sql-queries"></a>¿Dónde puedo ejecutar consultas SQL?

Puede ejecutar las consultas que utilizan Hola Explorador de datos en el portal de Azure, a través de Hola Hola [REST API y SDK](documentdb-sdk-dotnet.md), incluso hello y [Query playground](https://www.documentdb.com/sql/demo), que ejecutan las consultas en un conjunto de datos de ejemplo existente.

Para obtener más información sobre las consultas SQL, vea:
* [Consulta SQL y sintaxis SQL](documentdb-sql-query.md)

## <a name="prerequisites"></a>Requisitos previos

En este tutorial se da por supuesto que tiene una colección y una cuenta de Azure Cosmos DB. ¿No tiene nada de lo anterior? Hola completa [inicio rápido de 5 minutos](create-mongodb-nodejs.md) o hello [tutorial de programadores](tutorial-develop-mongodb.md) toocreate una cuenta y una colección.

## <a name="example-query-1"></a>Consulta 1 de ejemplo

Dado anterior de documento familia de ejemplo de Hola, después de la consulta SQL devuelve documentos Hola que coincide con el campo de Id. de hello `WakefieldFamily`. Puesto que es un `SELECT *` instrucción, la salida de hello de consulta de hello es documento JSON completo de hello:

**Consultar**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Resultados**

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

## <a name="example-query-2"></a>Consulta 2 de ejemplo

consulta siguiente de Hello devuelve todos los nombres especificados de Hola de elementos secundarios de familia de hello cuyo identificador coincide con `WakefieldFamily` ordenadas por su calificación.

**Consultar**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Resultados**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Ha aprendido cómo tooquery mediante SQL  

Ahora puede continuar toohello siguiente tutorial toolearn cómo toodistribute los datos globales.

> [!div class="nextstepaction"]
> [Distribución de datos global](tutorial-global-distribution-documentdb.md)

