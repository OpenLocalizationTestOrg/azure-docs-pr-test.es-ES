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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="2f3b3-104">Cómo usar de distribución global de base de datos de Azure Cosmos toosetup Hola API de documentos</span><span class="sxs-lookup"><span data-stu-id="2f3b3-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="2f3b3-105">En este artículo, le mostramos cómo toouse Hola toosetup portal Azure distribución global de base de datos de Azure Cosmos y, a continuación, conectarse con hello API de documentos.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="2f3b3-106">En este artículo se trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="2f3b3-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2f3b3-107">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2f3b3-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="2f3b3-108">Configure la distribución global con hello [DocumentDB APIs](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2f3b3-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="2f3b3-109">Conexión tooa región preferida mediante Hola API de documentos</span><span class="sxs-lookup"><span data-stu-id="2f3b3-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="2f3b3-110">En orden tootake aprovechar [distribución global](distribute-data-globally.md), pueden especificar las aplicaciones cliente hello ordenada la lista de preferencias de regiones toobe usa operaciones de documento tooperform.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="2f3b3-111">Esto puede hacerse mediante el establecimiento de directivas de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="2f3b3-112">En función de la configuración de cuenta de base de datos de Azure Cosmos hello, disponibilidad regional actual y la lista de preferencias de hello especificado, Hola mayoría extremo óptimo se elegirá por hello DocumentDB SDK tooperform escribir y las operaciones de lectura.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="2f3b3-113">Esta lista de preferencias se especifica al inicializar una conexión mediante el SDK de DocumentDB Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="2f3b3-114">Hola SDK aceptan un parámetro opcional "PreferredLocations" que es una lista ordenada de regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="2f3b3-115">Hola SDK enviará automáticamente todas las escrituras toohello actual escritura región.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="2f3b3-116">Todas las lecturas se enviarán toohello primera región disponible en la lista de PreferredLocations Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="2f3b3-117">Si se produce un error en la solicitud de Hola, cliente hello producirá un error hacia abajo de la región de hello lista toohello siguiente y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="2f3b3-118">Hola SDK sólo intentará tooread de regiones de hello especificado en PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="2f3b3-119">Por lo tanto, por ejemplo, si Hola cuenta de base de datos está disponible en tres regiones, pero cliente hello especifica sólo dos de las regiones de escritura de Hola para PreferredLocations, a continuación, ninguna de las lecturas se servirá fuera del área de escritura de hello, incluso en caso de hello de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="2f3b3-120">aplicación Hello puede comprobar el extremo de escritura actual de Hola y leer extremo elegido por hello SDK comprobación dos propiedades, WriteEndpoint y ReadEndpoint, disponible en la versión SDK 1.8 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="2f3b3-121">Si no se establece la propiedad PreferredLocations hello, todas las solicitudes se servirá de región de escritura actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="2f3b3-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="2f3b3-122">.NET SDK</span></span>
<span data-ttu-id="2f3b3-123">Hola SDK se puede utilizar sin cambios de código.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="2f3b3-124">En este caso, Hola SDK automáticamente dirige las lecturas y escribe toohello actual región de escritura.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="2f3b3-125">En la versión 1.8 y versiones posterior de hello .NET SDK, parámetro de ConnectionPolicy hello para el constructor de hello DocumentClient tiene una propiedad denominada Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="2f3b3-126">Esta propiedad es del tipo Collection `<string>` y debería contener una lista de nombres de región.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="2f3b3-127">se da formato a valores de cadena de Hola por cada columna de nombre de la región de hello en hello [regiones de Azure] [ regions] página, sin espacios en blanco antes o después de hello primero y último carácter respectivamente.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="2f3b3-128">escritura actual de Hola y de lecturas de puntos de conexión están disponibles en DocumentClient.WriteEndpoint y DocumentClient.ReadEndpoint respectivamente.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="2f3b3-129">Hola las direcciones URL para los extremos de hello no deberían considerarse como constantes de larga duración.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="2f3b3-130">servicio de Hello puede actualizarlos en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-130">hello service may update these at any point.</span></span> <span data-ttu-id="2f3b3-131">Hola SDK controla automáticamente este cambio.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-131">hello SDK handles this change automatically.</span></span>
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

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="2f3b3-132">SDK de NodeJS, JavaScript y Python</span><span class="sxs-lookup"><span data-stu-id="2f3b3-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="2f3b3-133">Hola SDK se puede utilizar sin cambios de código.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="2f3b3-134">En este caso, Hola que SDK dirigirá automáticamente lee tanto escribe toohello actual región de escritura.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="2f3b3-135">En la versión 1.8 y posteriores de cada SDK hello ConnectionPolicy parámetro para hello DocumentClient constructor una nueva propiedad llamada DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="2f3b3-136">Este parámetro es una matriz de cadenas que acepta una lista de nombres de región.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="2f3b3-137">se da formato a los nombres de Hola por cada columna de nombre de la región de Hola Hola [regiones de Azure] [ regions] página.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="2f3b3-138">También puede utilizar constantes de hello predefinido en objeto de comodidad de hello AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="2f3b3-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="2f3b3-139">escritura actual de Hola y de lecturas de puntos de conexión están disponibles en DocumentClient.getWriteEndpoint y DocumentClient.getReadEndpoint respectivamente.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="2f3b3-140">Hola las direcciones URL para los extremos de hello no deberían considerarse como constantes de larga duración.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="2f3b3-141">servicio de Hello puede actualizarlos en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-141">hello service may update these at any point.</span></span> <span data-ttu-id="2f3b3-142">Hola SDK controlará este cambio automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="2f3b3-143">A continuación, se muestra un ejemplo de código para JavaScript y NodeJS.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="2f3b3-144">Python y Java seguirá Hola mismo patrón.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-144">Python and Java will follow hello same pattern.</span></span>

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

## <a name="rest"></a><span data-ttu-id="2f3b3-145">REST</span><span class="sxs-lookup"><span data-stu-id="2f3b3-145">REST</span></span>
<span data-ttu-id="2f3b3-146">Una vez que una cuenta de base de datos pone a su disposición en varias regiones, los clientes pueden consultar la disponibilidad mediante la realización de una solicitud GET en hello después de URI.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="2f3b3-147">servicio de Hello devolverá una lista de regiones y su correspondiente base de datos de Azure Cosmos URI de extremo para las réplicas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="2f3b3-148">región de escritura actual de Hola se indicará en la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="2f3b3-149">cliente de Hola como se indica a continuación, a continuación, puede seleccionar un punto de conexión adecuado de Hola para todas las otras solicitudes de API de REST.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="2f3b3-150">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2f3b3-150">Example response</span></span>

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


* <span data-ttu-id="2f3b3-151">Las solicitudes de todos los PUT, POST y DELETE deben ir toohello indicado escribir URI</span><span class="sxs-lookup"><span data-stu-id="2f3b3-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="2f3b3-152">Obtiene todos los y otras solicitudes de solo lectura (por ejemplo, las consultas) pueden enviarse extremo tooany de elección del cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="2f3b3-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="2f3b3-153">Escribir solicitudes solo tooread regiones se producirá un error con código de error HTTP 403 "(prohibido).</span><span class="sxs-lookup"><span data-stu-id="2f3b3-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="2f3b3-154">Si cambia el área de escritura de hello después de la fase de detección inicial del cliente de hello, posterior escribe toohello anterior región de escritura se producirá un error con código de error HTTP 403 "(prohibido).</span><span class="sxs-lookup"><span data-stu-id="2f3b3-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="2f3b3-155">cliente Hello debe, a continuación, obtener lista de Hola de regiones nuevo tooget Hola escritura actualizada región.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="2f3b3-156">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="2f3b3-157">Obtener información sobre cómo toomanage Hola coherencia de la cuenta replicada a nivel mundial leyendo [niveles de coherencia en la base de datos de Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2f3b3-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="2f3b3-158">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="2f3b3-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f3b3-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f3b3-159">Next steps</span></span>

<span data-ttu-id="2f3b3-160">En este tutorial, ha hecho siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="2f3b3-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2f3b3-161">Configure la distribución global con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2f3b3-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="2f3b3-162">Configure la distribución global con hello DocumentDB APIs</span><span class="sxs-lookup"><span data-stu-id="2f3b3-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="2f3b3-163">Ahora puede continuar toohello siguiente tutorial toolearn cómo toodevelop localmente mediante Hola emulador local de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2f3b3-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f3b3-164">Desarrollar localmente con el emulador de Hola</span><span class="sxs-lookup"><span data-stu-id="2f3b3-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

