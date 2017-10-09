---
title: "tutorial de distribución global de Cosmos DB aaaAzure de API de MongoDB | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de MongoDB."
services: cosmos-db
keywords: "distribución global, MongoDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de MongoDB

En este artículo, le mostramos cómo toouse Hola toosetup portal Azure distribución global de base de datos de Azure Cosmos y, a continuación, conectarse mediante la API de MongoDB Hola.

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Configure la distribución global con hello portal de Azure
> * Configure la distribución global con hello [API de MongoDB](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Comprobar la configuración regional mediante la API de MongoDB Hola
la manera más sencilla de Hola de doble comprobando su configuración global dentro de la API de MongoDB es hello toorun *isMaster()* comando de Shell de Mongo Hola.

Desde el Shell de Mongo:

   ```
      db.isMaster()
   ```
   
Resultados de ejemplo:

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Conexión tooa región preferida mediante Hola API de MongoDB

Hola MongoDB API permite toospecify preferencias de lectura de la colección para una base de datos distribuido globalmente. Para ambos bajo Lecturas de latencia y alta disponibilidad global, se recomienda establecer preferencias de lectura de la colección demasiado*más cercano*. Una preferencia de lectura de *más cercano* es tooread configurado de la región más cercana de Hola.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Para las aplicaciones con un elemento principal de lectura/escritura región y una región secundaria para la recuperación ante desastres (DR) escenarios, se recomienda establecer preferencias de lectura de la colección demasiado*secundaria preferido*. Una preferencia de lectura de *secundaria preferido* resulta tooread configurado de la región secundaria Hola región principal de hello no está disponible.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Por último, si como toomanually especificaría las regiones de lectura. Para establecer la región de hello etiqueta dentro de sus preferencias de lectura.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

De este modo finaliza este tutorial. Obtener información sobre cómo toomanage Hola coherencia de la cuenta replicada a nivel mundial leyendo [niveles de coherencia en la base de datos de Azure Cosmos](consistency-levels.md). Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha hecho siguiente de hello:

> [!div class="checklist"]
> * Configure la distribución global con hello portal de Azure
> * Configure la distribución global con hello DocumentDB APIs

Ahora puede continuar toohello siguiente tutorial toolearn cómo toodevelop localmente mediante Hola emulador local de base de datos de Azure Cosmos.

> [!div class="nextstepaction"]
> [Desarrollar localmente con el emulador de Hola](local-emulator.md)
