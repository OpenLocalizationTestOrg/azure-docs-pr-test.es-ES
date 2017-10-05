---
title: "Tutorial de distribución global de Azure Cosmos DB para la API de DocumentDB | Microsoft Docs"
description: "Obtenga información sobre cómo configurar la distribución global de Azure Cosmos DB con la API de DocumentDB."
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
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="8345b-104">Configuración de la distribución global de Azure Cosmos DB con la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8345b-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="8345b-105">En este artículo se muestra cómo usar Azure Portal para configurar la distribución global de Azure Cosmos DB y luego conectarse con la API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8345b-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="8345b-106">En este artículo se tratan las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="8345b-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="8345b-107">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8345b-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="8345b-108">Configuración de la distribución global con las [API de DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8345b-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="8345b-109">Conexión a una región de preferencia con la API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8345b-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="8345b-110">Para aprovechar las ventajas de la [distribución global](distribute-data-globally.md), las aplicaciones cliente pueden especificar la lista del orden de preferencia de regiones que se usará para llevar a cabo operaciones de documentos.</span><span class="sxs-lookup"><span data-stu-id="8345b-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="8345b-111">Esto puede hacerse estableciendo la directiva de conexión.</span><span class="sxs-lookup"><span data-stu-id="8345b-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="8345b-112">Según la configuración de la cuenta de Azure Cosmos DB, la disponibilidad regional actual y la lista de preferencias especificada, el SDK de DocumentDB elegirá el punto de conexión óptimo para realizar las operaciones de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="8345b-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="8345b-113">Esta lista de preferencias se especifica cuando se inicializa una conexión mediante los SDK de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8345b-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="8345b-114">Los SDK aceptan un parámetro opcional "PreferredLocations", que es una lista ordenada de regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="8345b-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="8345b-115">El SDK enviará automáticamente todas las escrituras a la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="8345b-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="8345b-116">Todas las lecturas se enviarán a la primera región disponible en la lista de PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="8345b-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="8345b-117">Si se produce un error en la solicitud, el cliente pasará a la siguiente región de la lista y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="8345b-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="8345b-118">Los SDK solo intentarán leer en las regiones especificadas en PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="8345b-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="8345b-119">Así que, por ejemplo, si la cuenta de base de datos está disponible en tres regiones, pero el cliente solo especifica dos de las regiones de no escritura para PreferredLocations, no se atenderá ninguna lectura desde la región de escritura, incluso en caso de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="8345b-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="8345b-120">La aplicación puede comprobar los puntos de conexión de escritura y lectura actuales elegidos por el SDK. Para ello, comprueba dos propiedades, WriteEndpoint y ReadEndpoint, disponibles en el SDK 1.8 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="8345b-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="8345b-121">Si la propiedad PreferredLocations no está establecida, atenderá todas las solicitudes procedentes de la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="8345b-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="8345b-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="8345b-122">.NET SDK</span></span>
<span data-ttu-id="8345b-123">Se puede usar el SDK sin cambiar el código.</span><span class="sxs-lookup"><span data-stu-id="8345b-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="8345b-124">En este caso, el SDK dirige automáticamente tanto las lecturas como las escrituras a la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="8345b-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="8345b-125">En la versión 1.8 y posteriores del SDK de .NET, el parámetro ConnectionPolicy para el constructor DocumentClient tiene una propiedad denominada Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="8345b-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="8345b-126">Esta propiedad es del tipo Collection `<string>` y debería contener una lista de nombres de región.</span><span class="sxs-lookup"><span data-stu-id="8345b-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="8345b-127">Se da formato a los valores de cadena según la columna Nombre de región en la página [Regiones de Azure][regions], sin espacios antes ni después del primer y el último carácter, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8345b-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="8345b-128">Los puntos de conexión de lectura y escritura actuales están disponibles en DocumentClient.ReadEndpoint y DocumentClient.WriteEndpoint, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8345b-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="8345b-129">Las direcciones URL de los puntos de conexión no deben considerarse constantes de larga duración.</span><span class="sxs-lookup"><span data-stu-id="8345b-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="8345b-130">El servicio puede actualizarlas en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="8345b-130">The service may update these at any point.</span></span> <span data-ttu-id="8345b-131">El SDK administra este cambio automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8345b-131">The SDK handles this change automatically.</span></span>
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="8345b-132">SDK de NodeJS, JavaScript y Python</span><span class="sxs-lookup"><span data-stu-id="8345b-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="8345b-133">Se puede usar el SDK sin cambiar el código.</span><span class="sxs-lookup"><span data-stu-id="8345b-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="8345b-134">En este caso, el SDK dirigirá automáticamente tanto las lecturas como las escrituras a la región de escritura actual.</span><span class="sxs-lookup"><span data-stu-id="8345b-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="8345b-135">En la versión 1.8 y posteriores de cada SDK, el parámetro ConnectionPolicy para el constructor DocumentClient tiene una nueva propiedad denominada DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="8345b-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="8345b-136">Este parámetro es una matriz de cadenas que acepta una lista de nombres de región.</span><span class="sxs-lookup"><span data-stu-id="8345b-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="8345b-137">Se da formato a los nombres según la columna Nombre de región en la página [Regiones de Azure][regions].</span><span class="sxs-lookup"><span data-stu-id="8345b-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="8345b-138">También puede usar las constantes predefinidas en el objeto de conveniencia AzureDocuments.Regions.</span><span class="sxs-lookup"><span data-stu-id="8345b-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="8345b-139">Los puntos de conexión de lectura y escritura actuales están disponibles en DocumentClient.getReadEndpoint y DocumentClient.getWriteEndpoint, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8345b-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="8345b-140">Las direcciones URL de los puntos de conexión no deben considerarse constantes de larga duración.</span><span class="sxs-lookup"><span data-stu-id="8345b-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="8345b-141">El servicio puede actualizarlas en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="8345b-141">The service may update these at any point.</span></span> <span data-ttu-id="8345b-142">El SDK administrará este cambio automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8345b-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="8345b-143">A continuación, se muestra un ejemplo de código para JavaScript y NodeJS.</span><span class="sxs-lookup"><span data-stu-id="8345b-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="8345b-144">Python y Java siguen el mismo patrón.</span><span class="sxs-lookup"><span data-stu-id="8345b-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="8345b-145">REST</span><span class="sxs-lookup"><span data-stu-id="8345b-145">REST</span></span>
<span data-ttu-id="8345b-146">Una vez que una cuenta de base de datos está disponible en varias regiones, los clientes pueden consultar su disponibilidad llevando a cabo una solicitud GET en el siguiente URI.</span><span class="sxs-lookup"><span data-stu-id="8345b-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="8345b-147">El servicio devolverá una lista de regiones y los URI de punto de conexión de Azure Cosmos DB correspondientes para las réplicas.</span><span class="sxs-lookup"><span data-stu-id="8345b-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="8345b-148">Se indicará la región de escritura actual en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="8345b-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="8345b-149">Después, el cliente puede seleccionar el punto de conexión adecuado para las demás solicitudes de API de REST como sigue.</span><span class="sxs-lookup"><span data-stu-id="8345b-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="8345b-150">Respuesta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8345b-150">Example response</span></span>

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


* <span data-ttu-id="8345b-151">Todas las solicitudes PUT, POST y DELETE deben ir al URI de escritura indicado.</span><span class="sxs-lookup"><span data-stu-id="8345b-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="8345b-152">Todas las solicitudes GET y las demás solicitudes de solo lectura (como las consultas) pueden ir a cualquier punto de conexión elegido por el cliente.</span><span class="sxs-lookup"><span data-stu-id="8345b-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="8345b-153">Las solicitudes de escritura a regiones de solo lectura producirán un error con el código de error HTTP 403 ("Prohibido").</span><span class="sxs-lookup"><span data-stu-id="8345b-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="8345b-154">Si la región de escritura cambia después de la fase de descubrimiento inicial del cliente, se producirá un error en las escrituras posteriores a la región de escritura anterior con el código de error HTTP 403 ("Prohibido").</span><span class="sxs-lookup"><span data-stu-id="8345b-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="8345b-155">A continuación, el cliente debería de nuevo conseguir con GET la lista de regiones para obtener la región de escritura actualizada.</span><span class="sxs-lookup"><span data-stu-id="8345b-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="8345b-156">De este modo finaliza este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8345b-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="8345b-157">Para información sobre cómo administrar la coherencia de la cuenta replicada globalmente, lea [Niveles de coherencia en Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8345b-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="8345b-158">Para más información sobre cómo funciona la replicación global de bases de datos en Azure Cosmos DB, consulte [Distribución global de datos con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="8345b-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8345b-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8345b-159">Next steps</span></span>

<span data-ttu-id="8345b-160">En este tutorial, ha hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8345b-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8345b-161">Configuración de la distribución global con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8345b-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="8345b-162">Configuración de la distribución global con las API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8345b-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="8345b-163">Ahora puede continuar en el tutorial siguiente para aprender a desarrollar localmente con el emulador local de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8345b-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8345b-164">Desarrollo local con el emulador</span><span class="sxs-lookup"><span data-stu-id="8345b-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

