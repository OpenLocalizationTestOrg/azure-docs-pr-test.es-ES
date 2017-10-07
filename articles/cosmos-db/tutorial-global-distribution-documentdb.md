---
title: "tutorial de distribución global de Cosmos DB aaaAzure de API de documentos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de documentos."
services: cosmos-db
keywords: "distribución global, documentdb"
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
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de documentos

En este artículo, le mostramos cómo toouse Hola toosetup portal Azure distribución global de base de datos de Azure Cosmos y, a continuación, conectarse con hello API de documentos.

En este artículo se trata Hola siguientes tareas: 

> [!div class="checklist"]
> * Configure la distribución global con hello portal de Azure
> * Configure la distribución global con hello [DocumentDB APIs](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Conexión tooa región preferida mediante Hola API de documentos

En orden tootake aprovechar [distribución global](distribute-data-globally.md), pueden especificar las aplicaciones cliente hello ordenada la lista de preferencias de regiones toobe usa operaciones de documento tooperform. Esto puede hacerse mediante el establecimiento de directivas de conexión de Hola. En función de la configuración de cuenta de base de datos de Azure Cosmos hello, disponibilidad regional actual y la lista de preferencias de hello especificado, Hola mayoría extremo óptimo se elegirá por hello DocumentDB SDK tooperform escribir y las operaciones de lectura.

Esta lista de preferencias se especifica al inicializar una conexión mediante el SDK de DocumentDB Hola. Hola SDK aceptan un parámetro opcional "PreferredLocations" que es una lista ordenada de regiones de Azure.

Hola SDK enviará automáticamente todas las escrituras toohello actual escritura región.

Todas las lecturas se enviarán toohello primera región disponible en la lista de PreferredLocations Hola. Si se produce un error en la solicitud de Hola, cliente hello producirá un error hacia abajo de la región de hello lista toohello siguiente y así sucesivamente.

Hola SDK sólo intentará tooread de regiones de hello especificado en PreferredLocations. Por lo tanto, por ejemplo, si Hola cuenta de base de datos está disponible en tres regiones, pero cliente hello especifica sólo dos de las regiones de escritura de Hola para PreferredLocations, a continuación, ninguna de las lecturas se servirá fuera del área de escritura de hello, incluso en caso de hello de conmutación por error.

aplicación Hello puede comprobar el extremo de escritura actual de Hola y leer extremo elegido por hello SDK comprobación dos propiedades, WriteEndpoint y ReadEndpoint, disponible en la versión SDK 1.8 y versiones posteriores.

Si no se establece la propiedad PreferredLocations hello, todas las solicitudes se servirá de región de escritura actual de Hola.

## <a name="net-sdk"></a>.NET SDK
Hola SDK se puede utilizar sin cambios de código. En este caso, Hola SDK automáticamente dirige las lecturas y escribe toohello actual región de escritura.

En la versión 1.8 y versiones posterior de hello .NET SDK, parámetro de ConnectionPolicy hello para el constructor de hello DocumentClient tiene una propiedad denominada Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations. Esta propiedad es del tipo Collection `<string>` y debería contener una lista de nombres de región. se da formato a valores de cadena de Hola por cada columna de nombre de la región de hello en hello [regiones de Azure] [ regions] página, sin espacios en blanco antes o después de hello primero y último carácter respectivamente.

escritura actual de Hola y de lecturas de puntos de conexión están disponibles en DocumentClient.WriteEndpoint y DocumentClient.ReadEndpoint respectivamente.

> [!NOTE]
> Hola las direcciones URL para los extremos de hello no deberían considerarse como constantes de larga duración. servicio de Hello puede actualizarlos en cualquier momento. Hola SDK controla automáticamente este cambio.
>
>

```csharp
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

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>SDK de NodeJS, JavaScript y Python
Hola SDK se puede utilizar sin cambios de código. En este caso, Hola que SDK dirigirá automáticamente lee tanto escribe toohello actual región de escritura.

En la versión 1.8 y posteriores de cada SDK hello ConnectionPolicy parámetro para hello DocumentClient constructor una nueva propiedad llamada DocumentClient.ConnectionPolicy.PreferredLocations. Este parámetro es una matriz de cadenas que acepta una lista de nombres de región. se da formato a los nombres de Hola por cada columna de nombre de la región de Hola Hola [regiones de Azure] [ regions] página. También puede utilizar constantes de hello predefinido en objeto de comodidad de hello AzureDocuments.Regions

escritura actual de Hola y de lecturas de puntos de conexión están disponibles en DocumentClient.getWriteEndpoint y DocumentClient.getReadEndpoint respectivamente.

> [!NOTE]
> Hola las direcciones URL para los extremos de hello no deberían considerarse como constantes de larga duración. servicio de Hello puede actualizarlos en cualquier momento. Hola SDK controlará este cambio automáticamente.
>
>

A continuación, se muestra un ejemplo de código para JavaScript y NodeJS. Python y Java seguirá Hola mismo patrón.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST
Una vez que una cuenta de base de datos pone a su disposición en varias regiones, los clientes pueden consultar la disponibilidad mediante la realización de una solicitud GET en hello después de URI.

    https://{databaseaccount}.documents.azure.com/

servicio de Hello devolverá una lista de regiones y su correspondiente base de datos de Azure Cosmos URI de extremo para las réplicas de Hola. región de escritura actual de Hola se indicará en la respuesta de Hola. cliente de Hola como se indica a continuación, a continuación, puede seleccionar un punto de conexión adecuado de Hola para todas las otras solicitudes de API de REST.

Respuesta de ejemplo

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* Las solicitudes de todos los PUT, POST y DELETE deben ir toohello indicado escribir URI
* Obtiene todos los y otras solicitudes de solo lectura (por ejemplo, las consultas) pueden enviarse extremo tooany de elección del cliente de Hola

Escribir solicitudes solo tooread regiones se producirá un error con código de error HTTP 403 "(prohibido).

Si cambia el área de escritura de hello después de la fase de detección inicial del cliente de hello, posterior escribe toohello anterior región de escritura se producirá un error con código de error HTTP 403 "(prohibido). cliente Hello debe, a continuación, obtener lista de Hola de regiones nuevo tooget Hola escritura actualizada región.

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

