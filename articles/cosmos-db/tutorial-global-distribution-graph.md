---
title: "tutorial de distribución global de Cosmos DB aaaAzure para API Graph | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API Graph."
services: cosmos-db
keywords: "distribución global, graph, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>¿Cómo uso de distribución global de base de datos de Azure Cosmos toosetup Hola API Graph

En este artículo, le mostramos cómo toouse Hola distribución global de base de datos de Azure Cosmos toosetup de portal de Azure y, a continuación, conectarse con hello API Graph (versión preliminar).

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Configure la distribución global con hello portal de Azure
> * Configure la distribución global con hello [API de gráfico](graph-introduction.md) (versión preliminar)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>Conexión tooa región preferida mediante la API de Graph hello mediante Hola SDK para .NET

Hola API Graph se expone como una biblioteca de extensión en la parte superior hello DocumentDB SDK.

En orden tootake aprovechar [distribución global](distribute-data-globally.md), pueden especificar las aplicaciones cliente hello ordenada la lista de preferencias de regiones toobe usa operaciones de documento tooperform. Esto puede hacerse mediante el establecimiento de directivas de conexión de Hola. En función de la configuración de cuenta de base de datos de Azure Cosmos hello, disponibilidad regional actual y la lista de preferencias de hello especificado, Hola mayoría extremo óptimo se elegida por escritura de tooperform SDK de Hola y las operaciones de lectura.

Esta lista de preferencias se especifica al inicializar una conexión mediante el SDK de Hola. Hola SDK aceptan un parámetro opcional "PreferredLocations" que es una lista ordenada de regiones de Azure.

* **Escribe**: Hola SDK enviará automáticamente todas las escrituras toohello actual región de escritura.
* **Lee**: todas las lecturas se enviarán toohello primera región disponible en la lista de PreferredLocations Hola. Si se produce un error en la solicitud de Hola, cliente hello producirá un error hacia abajo de la región de hello lista toohello siguiente y así sucesivamente. Hola SDK sólo intentará tooread de regiones de hello especificado en PreferredLocations. Por lo tanto, por ejemplo, si Hola DB Cosmos cuenta está disponible en tres regiones, pero cliente hello especifica sólo dos de las regiones de escritura de Hola para PreferredLocations, a continuación, ningún lecturas se servirá fuera del área de escritura de hello, incluso en caso de hello de conmutación por error.

aplicación Hello puede comprobar el extremo de escritura actual de Hola y leer extremo elegido por hello SDK comprobación dos propiedades, WriteEndpoint y ReadEndpoint, disponible en la versión SDK 1.8 y versiones posteriores. Si no se establece la propiedad PreferredLocations hello, todas las solicitudes se servirá de región de escritura actual de Hola.

### <a name="using-hello-sdk"></a>Uso de hello SDK

Por ejemplo, en hello .NET SDK, Hola `ConnectionPolicy` parámetro hello `DocumentClient` constructor tiene una propiedad denominada `PreferredLocations`. Esta propiedad puede establecerse tooa lista de nombres de las regiones. nombres para mostrar de Hello [regiones de Azure] [ regions] puede especificarse como parte de `PreferredLocations`.

> [!NOTE]
> Hola las direcciones URL para los extremos de hello no deberían considerarse como constantes de larga duración. servicio de Hello puede actualizarlos en cualquier momento. Hola SDK controla automáticamente este cambio.
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
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

[regions]: https://azure.microsoft.com/regions/

