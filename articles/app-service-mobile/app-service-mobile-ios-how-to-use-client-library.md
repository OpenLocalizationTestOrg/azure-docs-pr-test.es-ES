---
title: "Uso del SDK de iOS para Aplicaciones móviles de Azure"
description: "Uso del SDK de iOS para Aplicaciones móviles de Azure"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="7b900-103">Uso de la biblioteca de cliente de iOS para Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="7b900-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="7b900-104">Esta guía muestra cómo realizar algunas tareas comunes a través del [SDK de iOS de Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="7b900-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="7b900-105">Si está familiarizado con Aplicaciones móviles de Azure, complete primero [Inicio rápido de Aplicaciones móviles de Azure] para crear un back-end, crear una tabla y descargar un proyecto de Xcode para iOS pregenerada.</span><span class="sxs-lookup"><span data-stu-id="7b900-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="7b900-106">En esta guía, nos centramos en el SDK de iOS de cliente.</span><span class="sxs-lookup"><span data-stu-id="7b900-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="7b900-107">Para obtener más información sobre el SDK de servidor para el back-end, consulte los procedimientos del SDK de servidor.</span><span class="sxs-lookup"><span data-stu-id="7b900-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="7b900-108">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="7b900-108">Reference documentation</span></span>
<span data-ttu-id="7b900-109">La documentación de referencia para el SDK de cliente de iOS se encuentra aquí: [Referencia de cliente de iOS de Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="7b900-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="7b900-110">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="7b900-110">Supported Platforms</span></span>
<span data-ttu-id="7b900-111">El SDK de iOS admite proyectos de Objective-C, Swift 2.2 y Swift 2.3 para iOS 8.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7b900-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="7b900-112">La autenticación de flujo de servidor utiliza una vista web para la interfaz de usuario presentada.</span><span class="sxs-lookup"><span data-stu-id="7b900-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="7b900-113">Si el dispositivo no puede presentar una interfaz de usuario de vista web, hay que utilizar otros métodos de autenticación que están fuera del ámbito del producto.</span><span class="sxs-lookup"><span data-stu-id="7b900-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="7b900-114">Por tanto, este SDK no es adecuado para dispositivos de tipo reloj o con restricciones similares.</span><span class="sxs-lookup"><span data-stu-id="7b900-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="7b900-115"><a name="Setup"></a>Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b900-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="7b900-116">En esta guía se asume que ha creado un back-end con una tabla.</span><span class="sxs-lookup"><span data-stu-id="7b900-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="7b900-117">En esta guía se asume que la tabla tiene el mismo esquema que las tablas de dichos tutoriales.</span><span class="sxs-lookup"><span data-stu-id="7b900-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="7b900-118">En esta guía también se supone que en el código se hace referencia a `MicrosoftAzureMobile.framework` e importa `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="7b900-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="7b900-119"><a name="create-client"></a>Creación del cliente</span><span class="sxs-lookup"><span data-stu-id="7b900-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="7b900-120">Para obtener acceso al back-end de Aplicaciones móviles de Azure en el proyecto, cree un `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="7b900-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="7b900-121">Reemplace `AppUrl` por la dirección URL de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b900-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="7b900-122">Puede dejar `gatewayURLString` y `applicationKey` vacías.</span><span class="sxs-lookup"><span data-stu-id="7b900-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="7b900-123">Si configura una puerta de enlace para la autenticación, rellene `gatewayURLString` con la dirección URL de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="7b900-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="7b900-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="7b900-125">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="7b900-126"><a name="table-reference"></a>Creación de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="7b900-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="7b900-127">Para acceder a los datos o actualizarlos, cree una referencia a la tabla de back-end.</span><span class="sxs-lookup"><span data-stu-id="7b900-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="7b900-128">Reemplace `TodoItem` por el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="7b900-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="7b900-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="7b900-130">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="7b900-131"><a name="querying"></a>Consulta de datos</span><span class="sxs-lookup"><span data-stu-id="7b900-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="7b900-132">Para crear una consulta de base de datos, consulte el objeto `MSTable` .</span><span class="sxs-lookup"><span data-stu-id="7b900-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="7b900-133">La consulta siguiente obtiene todos los elementos de `TodoItem` y registra el texto de cada elemento.</span><span class="sxs-lookup"><span data-stu-id="7b900-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="7b900-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="7b900-135">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="7b900-136"><a name="filtering"></a>Filtro de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="7b900-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="7b900-137">Para filtrar los resultados, hay muchas opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="7b900-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="7b900-138">Para filtrar mediante un predicado, use un `NSPredicate` y `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="7b900-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="7b900-139">Los siguientes filtros devolvieron datos para buscar solo los elementos Todo incompletos.</span><span class="sxs-lookup"><span data-stu-id="7b900-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="7b900-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="7b900-141">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="7b900-142"><a name="query-object"></a>Uso de MSQuery</span><span class="sxs-lookup"><span data-stu-id="7b900-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="7b900-143">Para realizar una consulta compleja (como de ordenación y paginación), cree un objeto `MSQuery` directamente o mediante un predicado:</span><span class="sxs-lookup"><span data-stu-id="7b900-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="7b900-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="7b900-145">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="7b900-146">`MSQuery` permite controlar varios comportamientos de consulta.</span><span class="sxs-lookup"><span data-stu-id="7b900-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="7b900-147">Especificar el orden de los resultados</span><span class="sxs-lookup"><span data-stu-id="7b900-147">Specify order of results</span></span>
* <span data-ttu-id="7b900-148">Limitar qué campos se devuelven</span><span class="sxs-lookup"><span data-stu-id="7b900-148">Limit which fields to return</span></span>
* <span data-ttu-id="7b900-149">Limitar el número de registros que se devolverán</span><span class="sxs-lookup"><span data-stu-id="7b900-149">Limit how many records to return</span></span>
* <span data-ttu-id="7b900-150">Especificar el recuento total en la respuesta</span><span class="sxs-lookup"><span data-stu-id="7b900-150">Specify total count in response</span></span>
* <span data-ttu-id="7b900-151">Especificar parámetros de la cadena de consulta personalizados en la solicitud</span><span class="sxs-lookup"><span data-stu-id="7b900-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="7b900-152">Aplicar funciones adicionales</span><span class="sxs-lookup"><span data-stu-id="7b900-152">Apply additional functions</span></span>

<span data-ttu-id="7b900-153">Ejecutar una consulta `MSQuery` llamando a `readWithCompletion` en el objeto.</span><span class="sxs-lookup"><span data-stu-id="7b900-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="7b900-154"><a name="sorting"></a>Ordenación de datos con MSQuery</span><span class="sxs-lookup"><span data-stu-id="7b900-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="7b900-155">Para ordenar los resultados, echemos un vistazo a un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7b900-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="7b900-156">Para ordenar por orden ascendente el campo text y, luego, por orden descendente el campo complete, invoque `MSQuery` de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="7b900-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="7b900-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="7b900-158">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="7b900-159"><a name="selecting"></a><a name="parameters"></a>Limitación de campos y expansión de los parámetros de cadena de consulta con MSQuery</span><span class="sxs-lookup"><span data-stu-id="7b900-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="7b900-160">Para limitar los campos que se devolverán en una consulta, especifique los nombres de los campos en la propiedad **selectFields** .</span><span class="sxs-lookup"><span data-stu-id="7b900-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="7b900-161">En este ejemplo solamente se devuelven los campos de texto y aquellos que se hayan rellenado:</span><span class="sxs-lookup"><span data-stu-id="7b900-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="7b900-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="7b900-163">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="7b900-164">Para incluir parámetros de cadena de consulta adicionales en la solicitud al servidor (por ejemplo, porque los utiliza un script de servidor personalizado), introduzca `query.parameters` :</span><span class="sxs-lookup"><span data-stu-id="7b900-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="7b900-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="7b900-166">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="7b900-167"><a name="paging"></a>Procedimiento: configuración del tamaño de página</span><span class="sxs-lookup"><span data-stu-id="7b900-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="7b900-168">Con Azure Mobile Apps, el tamaño de página controla el número de registros que se extraen de las tablas de back-end al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="7b900-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="7b900-169">Luego, una llamada a los datos de `pull` enviaría dichos datos en lotes, basándose en este tamaño de página, hasta que no haya más registros para extraer.</span><span class="sxs-lookup"><span data-stu-id="7b900-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="7b900-170">Es posible configurar un tamaño de página con **MSPullSettings** tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="7b900-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="7b900-171">El tamaño de página predeterminado es 50 y en el ejemplo siguiente se cambia a 3.</span><span class="sxs-lookup"><span data-stu-id="7b900-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="7b900-172">Para mejorar el rendimiento es posible configurar otro tamaño de página.</span><span class="sxs-lookup"><span data-stu-id="7b900-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="7b900-173">Si tiene un gran número de registros de datos pequeños, un tamaño de página elevado reduce el número de idas y vueltas del servidor.</span><span class="sxs-lookup"><span data-stu-id="7b900-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="7b900-174">Este valor controla el tamaño de página en el cliente.</span><span class="sxs-lookup"><span data-stu-id="7b900-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="7b900-175">Si el cliente pide un tamaño de página mayor que el que admite el back-end de Mobile Apps, se limita al máximo que el back-end está configurado para admitir.</span><span class="sxs-lookup"><span data-stu-id="7b900-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="7b900-176">Este valor es también el *número* de registros de datos, no el *tamaño en bytes*.</span><span class="sxs-lookup"><span data-stu-id="7b900-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="7b900-177">Si aumenta el tamaño de página del cliente, también debe aumentar el tamaño de página en el servidor.</span><span class="sxs-lookup"><span data-stu-id="7b900-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="7b900-178">Para saber qué pasos debe dar para hacerlo, consulte ["Cómo ajustar el tamaño de paginación de la tabla"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7b900-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="7b900-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="7b900-180">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="7b900-181"><a name="inserting"></a>Insertar datos</span><span class="sxs-lookup"><span data-stu-id="7b900-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="7b900-182">Para insertar una nueva fila en la tabla, cree un elemento `NSDictionary` e invoque `table insert`.</span><span class="sxs-lookup"><span data-stu-id="7b900-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="7b900-183">Si el [esquema dinámico] está habilitado, el back-end móvil de Azure App Service genera automáticamente columnas nuevas basadas en `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="7b900-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="7b900-184">Si no se proporciona `id` , el backend genera automáticamente un nuevo identificador único.</span><span class="sxs-lookup"><span data-stu-id="7b900-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="7b900-185">Proporcione su propio `id` para utilizar direcciones de correo electrónico, nombres de usuario o sus propios valores personalizados como Id.</span><span class="sxs-lookup"><span data-stu-id="7b900-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="7b900-186">Proporcionar su propio ID puede facilitar las combinaciones y la lógica de la base de datos de tipo empresarial.</span><span class="sxs-lookup"><span data-stu-id="7b900-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="7b900-187">`result` contiene el nuevo elemento insertado.</span><span class="sxs-lookup"><span data-stu-id="7b900-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="7b900-188">En función de la lógica del servidor, puede tener datos modificados o adicionales en comparación con lo que se pasó al servidor.</span><span class="sxs-lookup"><span data-stu-id="7b900-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="7b900-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="7b900-190">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="7b900-191"><a name="modifying"></a>Modificación de datos</span><span class="sxs-lookup"><span data-stu-id="7b900-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="7b900-192">Para actualizar una fila existente, modifique un elemento y llame a `update`:</span><span class="sxs-lookup"><span data-stu-id="7b900-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="7b900-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="7b900-194">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="7b900-195">Como alternativa, proporcione el identificador de fila y el campo actualizado:</span><span class="sxs-lookup"><span data-stu-id="7b900-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="7b900-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="7b900-197">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="7b900-198">Como mínimo, debe establecerse el atributo `id` al realizar actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="7b900-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="7b900-199"><a name="deleting"></a>Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="7b900-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="7b900-200">Para eliminar un elemento, invoque `delete` con el elemento:</span><span class="sxs-lookup"><span data-stu-id="7b900-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="7b900-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="7b900-202">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="7b900-203">O bien elimínelo proporcionando un identificador de fila:</span><span class="sxs-lookup"><span data-stu-id="7b900-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="7b900-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="7b900-205">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="7b900-206">Como mínimo, el atributo `id` debe establecerse a la hora de efectuar eliminaciones.</span><span class="sxs-lookup"><span data-stu-id="7b900-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="7b900-207"><a name="customapi"></a>Llamada a una API personalizada</span><span class="sxs-lookup"><span data-stu-id="7b900-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="7b900-208">Con una API personalizada, puede exponer cualquier funcionalidad de back-end.</span><span class="sxs-lookup"><span data-stu-id="7b900-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="7b900-209">No necesita asignar a una operación de tabla.</span><span class="sxs-lookup"><span data-stu-id="7b900-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="7b900-210">No solo obtendrá más control sobre la mensajería, también podrá leer o establecer encabezados y cambiar el formato del cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="7b900-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="7b900-211">Para aprender cómo crear una API personalizada en el back-end, lea [API personalizadas](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="7b900-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="7b900-212">Para invocar a una API personalizada, llame a `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="7b900-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="7b900-213">El contenido de la solicitud y la respuesta se tratan como JSON.</span><span class="sxs-lookup"><span data-stu-id="7b900-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="7b900-214">Para utilizar otros tipos de soportes físicos, [use la otra sobrecarga de `invokeAPI`][5].</span><span class="sxs-lookup"><span data-stu-id="7b900-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="7b900-215">Para realizar una solicitud `GET` en lugar de una solicitud `POST`, establezca el parámetro `HTTPMethod` en `"GET"` y el parámetro `body` en `nil` (puesto que las solicitudes GET no tienen cuerpos de mensaje). Si la API personalizada es compatible con otros verbos HTTP, cambie `HTTPMethod` de acuerdo a ello.</span><span class="sxs-lookup"><span data-stu-id="7b900-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="7b900-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="7b900-217">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="7b900-218"><a name="templates"></a>Procedimiento: Registro de plantillas push para enviar notificaciones entre plataformas</span><span class="sxs-lookup"><span data-stu-id="7b900-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="7b900-219">Para registrar plantillas, pase las plantillas con el método **client.push registerDeviceToken** en la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="7b900-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="7b900-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="7b900-221">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="7b900-222">Las plantillas serán de tipo NSDictionary y pueden contener varias plantillas con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b900-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="7b900-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="7b900-224">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="7b900-225">Por seguridad, se eliminan todas las etiquetas de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="7b900-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="7b900-226">Para agregar etiquetas a las instalaciones o a las plantillas de las instalaciones, consulte [Trabajar con el SDK del servidor back-end de .NET para Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="7b900-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="7b900-227">Para enviar notificaciones mediante estas plantillas registradas, trabaje con [API de Notification Hubs][3].</span><span class="sxs-lookup"><span data-stu-id="7b900-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="7b900-228"><a name="errors"></a>Gestión de errores</span><span class="sxs-lookup"><span data-stu-id="7b900-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="7b900-229">Al realizar una llamada a un back-end móvil de Azure App Service, el bloque de finalización contiene un parámetro `NSError` .</span><span class="sxs-lookup"><span data-stu-id="7b900-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="7b900-230">En caso de producirse un error, este parámetro no será nulo.</span><span class="sxs-lookup"><span data-stu-id="7b900-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="7b900-231">En su código, debe marcar este parámetro y administrar el error según sea necesario, como se muestra en los fragmentos de código anteriores.</span><span class="sxs-lookup"><span data-stu-id="7b900-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="7b900-232">El archivo [`<WindowsAzureMobileServices/MSError.h>`][6] define las constantes `MSErrorResponseKey`, `MSErrorRequestKey` y `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="7b900-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="7b900-233">Para obtener más datos relacionados con el error:</span><span class="sxs-lookup"><span data-stu-id="7b900-233">To get more data related to the error:</span></span>

<span data-ttu-id="7b900-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="7b900-235">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="7b900-236">Además, el archivo define constantes para cada código de error:</span><span class="sxs-lookup"><span data-stu-id="7b900-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="7b900-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="7b900-238">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="7b900-239"><a name="adal"></a>Autenticación de usuarios con la biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b900-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="7b900-240">Puede utilizar la biblioteca de autenticación de Active Directory (ADAL) para iniciar la sesión de los usuarios en su aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7b900-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="7b900-241">Se prefiere la autenticación de flujo de cliente mediante un SDK de proveedor de identidades al uso del método `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="7b900-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="7b900-242">Este tipo de autenticación proporciona una experiencia de usuario más nativa y permite realizar más personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="7b900-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="7b900-243">Configure su back-end de aplicación móvil para el inicio de sesión en AAD siguiendo el tutorial [Configuración de la aplicación de App Service para usar el inicio de sesión de Azure Active Directory][7].</span><span class="sxs-lookup"><span data-stu-id="7b900-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="7b900-244">Asegúrese de completar el paso opcional de registrar una aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="7b900-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="7b900-245">Para iOS, se recomienda que el URI de redireccionamiento tenga el formato `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="7b900-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="7b900-246">Para más información, consulte la [guía de inicio rápido de iOS para ADAL][8].</span><span class="sxs-lookup"><span data-stu-id="7b900-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="7b900-247">Instale ADAL mediante Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="7b900-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="7b900-248">Edite el podfile para incluir la siguiente definición; sustituya **YOUR-PROJECT** por el nombre de su proyecto de Xcode:</span><span class="sxs-lookup"><span data-stu-id="7b900-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="7b900-249">y el POD:</span><span class="sxs-lookup"><span data-stu-id="7b900-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="7b900-250">Mediante el Terminal, ejecute `pod install` desde el directorio que contiene el proyecto y abra el área de trabajo del Xcode generado (no el proyecto).</span><span class="sxs-lookup"><span data-stu-id="7b900-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="7b900-251">Agregue el siguiente código a la aplicación, según el lenguaje que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="7b900-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="7b900-252">En cada uno, realice estas sustituciones:</span><span class="sxs-lookup"><span data-stu-id="7b900-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="7b900-253">Reemplace **INSERT-AUTHORITY-HERE** por el nombre del inquilino en el que aprovisionó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b900-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="7b900-254">El formato debería ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7b900-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="7b900-255">Este valor se puede copiar de la pestaña Dominio de Azure Active Directory en el [Portal de Azure clásico].</span><span class="sxs-lookup"><span data-stu-id="7b900-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="7b900-256">Reemplace **INSERT-RESOURCE-ID-HERE** por el Id. de cliente del back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="7b900-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="7b900-257">El Id. de cliente en la pestaña **Opciones avanzadas** de **Configuración de Azure Active Directory** en el portal.</span><span class="sxs-lookup"><span data-stu-id="7b900-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="7b900-258">Reemplace **INSERT-CLIENT-ID-HERE** por el Id. de cliente que copió de la aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="7b900-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="7b900-259">Reemplace **INSERT-REDIRECT-URI-HERE** por el punto de conexión */.auth/login/done* del sitio, mediante el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7b900-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="7b900-260">Este valor debe ser similar a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="7b900-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="7b900-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-261">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="7b900-262">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="7b900-263"><a name="facebook-sdk"></a>Autenticación de usuarios con SDK de Facebook para iOS</span><span class="sxs-lookup"><span data-stu-id="7b900-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="7b900-264">Puede usar el SDK de Facebook para iOS para que los usuarios inicien sesión en su aplicación con Facebook.</span><span class="sxs-lookup"><span data-stu-id="7b900-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="7b900-265">Es preferible usar la autenticación de flujo de cliente al método `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="7b900-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="7b900-266">Este tipo de autenticación proporciona una experiencia de usuario más nativa y permite realizar más personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="7b900-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="7b900-267">Configure el back-end de aplicación móvil para el inicio de sesión en Facebook siguiendo el tutorial [Configuración de la aplicación de App Service para usar el inicio de sesión de Facebook][9].</span><span class="sxs-lookup"><span data-stu-id="7b900-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="7b900-268">Instale el SDK de Facebook para iOS siguiendo la documentación [SDK de Facebook para iOS: primeros pasos][10].</span><span class="sxs-lookup"><span data-stu-id="7b900-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="7b900-269">En lugar de crear una aplicación, puede agregar la plataforma iOS en el registro existente.</span><span class="sxs-lookup"><span data-stu-id="7b900-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="7b900-270">La documentación de Facebook incluye algún código de Objective-C en el delegado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b900-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="7b900-271">Si utiliza **Swift**, puede usar las siguientes traducciones para AppDelegate.swift:</span><span class="sxs-lookup"><span data-stu-id="7b900-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="7b900-272">Además de agregar `FBSDKCoreKit.framework` al proyecto, también puede agregar una referencia a `FBSDKLoginKit.framework` de la misma manera.</span><span class="sxs-lookup"><span data-stu-id="7b900-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="7b900-273">Agregue el siguiente código a la aplicación, según el lenguaje que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="7b900-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="7b900-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-274">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="7b900-275">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="7b900-276"><a name="twitter-fabric"></a>Autenticación de usuarios con Fabric de Twitter para iOS</span><span class="sxs-lookup"><span data-stu-id="7b900-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="7b900-277">Puede usar Fabric para iOS para que los usuarios inicien sesión en su aplicación con Twitter.</span><span class="sxs-lookup"><span data-stu-id="7b900-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="7b900-278">La autenticación de flujo de cliente es preferible al uso del método `loginWithProvider:completion:` , ya que proporciona una experiencia de usuario más nativa y permite realizar más personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="7b900-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="7b900-279">Configure su back-end de aplicación móvil para el inicio de sesión en Twitter siguiendo el tutorial [Configuración de la aplicación Servicio de aplicaciones para usar el inicio de sesión de Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="7b900-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="7b900-280">Agregue Fabric al proyecto siguiendo el documento [Fabric for iOS - Getting Started] (Primeros pasos en Fabric para iOS) y configurando TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="7b900-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b900-281">De forma predeterminada, Fabric creará automáticamente una aplicación de Twitter.</span><span class="sxs-lookup"><span data-stu-id="7b900-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="7b900-282">Puede evitar que se cree registrando la clave de usuario y el secreto de consumidor que creó anteriormente mediante los fragmentos de código siguientes.</span><span class="sxs-lookup"><span data-stu-id="7b900-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="7b900-283">Asimismo, puede reemplazar los valores de clave de usuario y de secreto de consumidor que proporcione al Servicio de aplicaciones por los valores que aparecen en [Fabric Dashboard](Panel de Fabric).</span><span class="sxs-lookup"><span data-stu-id="7b900-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="7b900-284">Si elige esta opción, asegúrese de establecer la dirección URL de devolución de llamada en un valor de marcador de posición, como `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="7b900-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="7b900-285">Si decide utilizar los secretos que creó anteriormente, agregue el siguiente código al delegado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7b900-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="7b900-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-286">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="7b900-287">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="7b900-288">Agregue el siguiente código a la aplicación, según el lenguaje que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="7b900-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="7b900-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-289">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="7b900-290">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-290">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="7b900-291"><a name="google-sdk"></a>Autenticación de usuarios con el SDK de inicio de sesión de Google para iOS</span><span class="sxs-lookup"><span data-stu-id="7b900-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="7b900-292">Puede usar el SDK de inicio de sesión de Google para iOS para que los usuarios inicien sesión en su aplicación con una cuenta de Google.</span><span class="sxs-lookup"><span data-stu-id="7b900-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="7b900-293">Google anunció recientemente cambios en sus directivas de seguridad de OAuth.</span><span class="sxs-lookup"><span data-stu-id="7b900-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="7b900-294">Estos cambios obligarán a usar el SDK de Google en el futuro.</span><span class="sxs-lookup"><span data-stu-id="7b900-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="7b900-295">Configure su back-end de aplicación móvil para el inicio de sesión en Google siguiendo el tutorial [Configuración de la aplicación Servicio de aplicaciones para usar el inicio de sesión de Google](app-service-mobile-how-to-configure-google-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="7b900-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="7b900-296">Instale el SDK de Google para iOS siguiendo la documentación de [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) (Inicio de sesión de Google para iOS: Empiece a integrar).</span><span class="sxs-lookup"><span data-stu-id="7b900-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="7b900-297">Puede omitir la sección Authenticate with a Backend Server (Autenticar con un servidor back-end).</span><span class="sxs-lookup"><span data-stu-id="7b900-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="7b900-298">Agregue el siguiente código al método `signIn:didSignInForUser:withError:` del delegado según el lenguaje que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="7b900-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="7b900-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="7b900-300">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="7b900-301">Asegúrese de agregar también lo siguiente a `application:didFinishLaunchingWithOptions:` en el delegado de la aplicación, reemplazando "SERVER_CLIENT_ID" por el mismo identificador que usó para configurar el Servicio de aplicaciones en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="7b900-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="7b900-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="7b900-303">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="7b900-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="7b900-304">Agregue el siguiente código a la aplicación en un UIViewController que permita implementar el protocolo `GIDSignInUIDelegate` según el lenguaje que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="7b900-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="7b900-305">La sesión se cierra antes de volver a iniciar sesión y, aunque no es necesario que vuelva a escribir sus credenciales, verá un cuadro de diálogo de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="7b900-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="7b900-306">Solo llame a este método si el token de sesión ha expirado.</span><span class="sxs-lookup"><span data-stu-id="7b900-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="7b900-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="7b900-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="7b900-308">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="7b900-308">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="7b900-309">[Inicio rápido de Aplicaciones móviles de Azure]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="7b900-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="7b900-310">[esquema dinámico]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="7b900-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="7b900-311">[Fabric Dashboard]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="7b900-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="7b900-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="7b900-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
