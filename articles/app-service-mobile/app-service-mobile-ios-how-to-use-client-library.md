---
title: "aaaHow tooUse iOS SDK para aplicaciones móviles de Azure"
description: "¿Cómo tooUse iOS SDK para aplicaciones móviles de Azure"
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
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="4e8cd-103">¿Cómo tooUse iOS biblioteca de cliente para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="4e8cd-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="4e8cd-104">Esta guía le enseña con hello más reciente de escenarios comunes de tooperform [iOS de aplicaciones móviles de Azure SDK][1].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="4e8cd-105">Si estás nuevas aplicaciones de Mobile tooAzure, complete primero [inicio rápido de Azure Mobile Apps] toocreate un back-end, cree una tabla y descargar un proyecto de Xcode pregenerado iOS.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="4e8cd-106">En esta guía se centra en SDK de iOS de Hola de cliente.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="4e8cd-107">toolearn Obtenga más información sobre Hola SDK de servidor de back-end de hello, vea Hola Server SDK explicativa.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="4e8cd-108">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="4e8cd-108">Reference documentation</span></span>
<span data-ttu-id="4e8cd-109">Hello documentación de referencia de SDK de cliente de iOS de Hola se encuentra aquí: [aplicaciones móviles de Azure iOS referencia de cliente][2].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4e8cd-110">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="4e8cd-110">Supported Platforms</span></span>
<span data-ttu-id="4e8cd-111">SDK de iOS de Hello admite proyectos Objective-C, Swift 2.2 proyectos y proyectos de Swift 2.3 para iOS versiones 8.0 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="4e8cd-112">la autenticación de "flujo de servidor" Hello usa un WebView para hello presentada la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="4e8cd-113">Si el dispositivo de hello no es capaz de toopresent una UI WebView, se requiere el otro método de autenticación es fuera Hola ámbito del producto Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="4e8cd-114">Por tanto, este SDK no es adecuado para dispositivos de tipo reloj o con restricciones similares.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="4e8cd-115"><a name="Setup"></a>Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4e8cd-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="4e8cd-116">En esta guía se asume que ha creado un back-end con una tabla.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="4e8cd-117">Esta guía se da por supuesto que esa tabla hello tiene el mismo esquema como tablas de hello en los tutoriales.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="4e8cd-118">En esta guía también se supone que en el código se hace referencia a `MicrosoftAzureMobile.framework` e importa `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="4e8cd-119"><a name="create-client"></a>Creación del cliente</span><span class="sxs-lookup"><span data-stu-id="4e8cd-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="4e8cd-120">tooaccess un back-end de aplicaciones móviles de Azure en el proyecto, crear un `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="4e8cd-121">Reemplace `AppUrl` con la URL de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="4e8cd-122">Puede dejar `gatewayURLString` y `applicationKey` vacías.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="4e8cd-123">Si configura una puerta de enlace para la autenticación, rellenar `gatewayURLString` con la dirección URL de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="4e8cd-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="4e8cd-125">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="4e8cd-126"><a name="table-reference"></a>Creación de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="4e8cd-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="4e8cd-127">tooaccess o actualizar los datos, cree una tabla de referencia toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="4e8cd-128">Reemplace `TodoItem` con nombre hello de la tabla</span><span class="sxs-lookup"><span data-stu-id="4e8cd-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="4e8cd-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="4e8cd-130">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="4e8cd-131"><a name="querying"></a>Consulta de datos</span><span class="sxs-lookup"><span data-stu-id="4e8cd-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="4e8cd-132">toocreate una consulta de base de datos, Hola consulta `MSTable` objeto.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="4e8cd-133">Hello consulta siguiente obtiene todos los elementos de hello `TodoItem` y registros de Hola texto de cada elemento.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="4e8cd-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-134">**Objective-C**:</span></span>

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

<span data-ttu-id="4e8cd-135">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-135">**Swift**:</span></span>

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

## <span data-ttu-id="4e8cd-136"><a name="filtering"></a>Filtro de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="4e8cd-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="4e8cd-137">resultados de toofilter, hay muchas opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="4e8cd-138">toofilter mediante un predicado, use un `NSPredicate` y `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="4e8cd-139">siguiente Hola filtra los elementos de lista de tareas de datos devueltos toofind solo incompletos.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="4e8cd-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
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

<span data-ttu-id="4e8cd-141">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
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

## <span data-ttu-id="4e8cd-142"><a name="query-object"></a>Uso de MSQuery</span><span class="sxs-lookup"><span data-stu-id="4e8cd-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="4e8cd-143">tooperform crear una consulta compleja (incluida la clasificación y paginación), un `MSQuery` de objeto, directamente o mediante un predicado:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="4e8cd-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="4e8cd-145">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="4e8cd-146">`MSQuery` permite controlar varios comportamientos de consulta.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="4e8cd-147">Especificar el orden de los resultados</span><span class="sxs-lookup"><span data-stu-id="4e8cd-147">Specify order of results</span></span>
* <span data-ttu-id="4e8cd-148">Límite de campos tooreturn</span><span class="sxs-lookup"><span data-stu-id="4e8cd-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="4e8cd-149">Limitar el número de registros tooreturn</span><span class="sxs-lookup"><span data-stu-id="4e8cd-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="4e8cd-150">Especificar el recuento total en la respuesta</span><span class="sxs-lookup"><span data-stu-id="4e8cd-150">Specify total count in response</span></span>
* <span data-ttu-id="4e8cd-151">Especificar parámetros de la cadena de consulta personalizados en la solicitud</span><span class="sxs-lookup"><span data-stu-id="4e8cd-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="4e8cd-152">Aplicar funciones adicionales</span><span class="sxs-lookup"><span data-stu-id="4e8cd-152">Apply additional functions</span></span>

<span data-ttu-id="4e8cd-153">Ejecutar un `MSQuery` consulta mediante una llamada a `readWithCompletion` en el objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="4e8cd-154"><a name="sorting"></a>Ordenación de datos con MSQuery</span><span class="sxs-lookup"><span data-stu-id="4e8cd-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="4e8cd-155">resultados de toosort, echemos un vistazo a un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="4e8cd-156">invocar toosort por texto' campo' ascendente y luego por 'complete' en orden descendente, `MSQuery` así:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="4e8cd-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-157">**Objective-C**:</span></span>

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

<span data-ttu-id="4e8cd-158">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-158">**Swift**:</span></span>

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


## <span data-ttu-id="4e8cd-159"><a name="selecting"></a><a name="parameters"></a>Limitación de campos y expansión de los parámetros de cadena de consulta con MSQuery</span><span class="sxs-lookup"><span data-stu-id="4e8cd-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="4e8cd-160">toolimit toobe de campos devuelto en una consulta, se especifican nombres de Hola de campos de Hola Hola **selectFields** propiedad.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="4e8cd-161">Este ejemplo devuelve solo texto hello y campos completados:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="4e8cd-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="4e8cd-163">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="4e8cd-164">parámetros de cadena de consulta adicionales tooinclude en servidor hello solicitan (por ejemplo, porque utiliza un script de servidor personalizado), rellenar `query.parameters` así:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="4e8cd-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="4e8cd-166">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="4e8cd-167"><a name="paging"></a>Procedimiento: configuración del tamaño de página</span><span class="sxs-lookup"><span data-stu-id="4e8cd-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="4e8cd-168">Con aplicaciones de Azure Mobile, controles de tamaño de página de Hola Hola número de registros que se extraigan de tablas de back-end de hello al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="4e8cd-169">Llamar demasiado`pull` datos, a continuación, podrían crear lotes de datos, basada en este tamaño de página, hasta que no haya ningún más toopull de registros.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="4e8cd-170">Es posible tooconfigure un tamaño de página con **MSPullSettings** tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="4e8cd-171">tamaño de página predeterminado de Hello es 50 y ejemplo de Hola siguiente cambia too3.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="4e8cd-172">Para mejorar el rendimiento es posible configurar otro tamaño de página.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="4e8cd-173">Si tiene un gran número de registros de datos pequeños, un tamaño de página alta reduce el número de Hola de ida y vuelta del servidor.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="4e8cd-174">Esta configuración controla sólo tamaño de página de hello en el lado del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="4e8cd-175">Si el cliente de hello pide un tamaño de página que admite aplicaciones móviles de hello back-end, el tamaño de página de hello es limitado a back-end de Hola Hola máximo es toosupport configurado.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="4e8cd-176">Esta configuración también es hello *número* de registros de datos, no Hola *tamaño en bytes*.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="4e8cd-177">Si aumenta el tamaño de página de cliente hello, también debe aumentar el tamaño de página de hello en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="4e8cd-178">Vea ["Cómo: ajustar el tamaño de paginación de tabla Hola"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para hello pasos toodo esto.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="4e8cd-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="4e8cd-180">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="4e8cd-181"><a name="inserting"></a>Insertar datos</span><span class="sxs-lookup"><span data-stu-id="4e8cd-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="4e8cd-182">crear una nueva fila de tabla, tooinsert una `NSDictionary` e invocar `table insert`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="4e8cd-183">Si [esquema dinámico] está habilitada, back-end de hello servicio de aplicaciones de Azure mobile genera automáticamente nuevas columnas en función de hello `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="4e8cd-184">Si `id` es no siempre, Hola back-end genera automáticamente un nuevo identificador único.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="4e8cd-185">Proporcionar su propia `id` toouse de correo electrónico direcciones, nombres de usuario o sus propios valores personalizados como identificador.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="4e8cd-186">Proporcionar su propio ID puede facilitar las combinaciones y la lógica de la base de datos de tipo empresarial.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="4e8cd-187">Hola `result` contiene Hola nuevo elemento que se ha insertado.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="4e8cd-188">Según la lógica del servidor, toowhat de datos modificados en comparación con se ha pasado toohello server o puede tener adicionales.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="4e8cd-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-189">**Objective-C**:</span></span>

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

<span data-ttu-id="4e8cd-190">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-190">**Swift**:</span></span>

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

## <span data-ttu-id="4e8cd-191"><a name="modifying"></a>Modificación de datos</span><span class="sxs-lookup"><span data-stu-id="4e8cd-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="4e8cd-192">tooupdate una fila existente, modificar un elemento y la llamada `update`:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="4e8cd-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-193">**Objective-C**:</span></span>

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

<span data-ttu-id="4e8cd-194">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-194">**Swift**:</span></span>

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

<span data-ttu-id="4e8cd-195">O bien, especifique Id. de fila de Hola y campo Hola actualizado:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="4e8cd-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="4e8cd-197">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="4e8cd-198">Como mínimo, Hola `id` atributo debe establecerse al realizar las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="4e8cd-199"><a name="deleting"></a>Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="4e8cd-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="4e8cd-200">toodelete un elemento, invocar `delete` con elemento hello:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="4e8cd-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="4e8cd-202">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="4e8cd-203">O bien elimínelo proporcionando un identificador de fila:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="4e8cd-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="4e8cd-205">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="4e8cd-206">Como mínimo, Hola `id` atributo debe establecerse al hacer que se elimina.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="4e8cd-207"><a name="customapi"></a>Llamada a una API personalizada</span><span class="sxs-lookup"><span data-stu-id="4e8cd-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="4e8cd-208">Con una API personalizada, puede exponer cualquier funcionalidad de back-end.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="4e8cd-209">No tiene toomap tooa la operación de tabla.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="4e8cd-210">No sólo obtendrá más control sobre la mensajería, incluso puede leer o establecer los encabezados y cambiar el formato del cuerpo de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="4e8cd-211">toolearn cómo leer toocreate una API personalizada en el back-end de hello, [API personalizadas](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="4e8cd-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="4e8cd-212">llamar una API personalizada, toocall `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="4e8cd-213">solicitud de Hola y el contenido de la respuesta se tratan como JSON.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="4e8cd-214">toouse otros tipos de medios, [uso Hola otra sobrecarga de `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="4e8cd-215">toomake una `GET` solicitar en lugar de un `POST` solicitar, parámetro de conjunto de `HTTPMethod` demasiado`"GET"` y parámetro `body` demasiado`nil` (ya que las solicitudes GET no tener cuerpos de mensaje). Si la API personalizada es compatible con otros verbos HTTP, cambie `HTTPMethod` de acuerdo a ello.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="4e8cd-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-216">**Objective-C**:</span></span>

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

<span data-ttu-id="4e8cd-217">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-217">**Swift**:</span></span>

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

## <span data-ttu-id="4e8cd-218"><a name="templates"></a>Cómo: notificaciones de registro inserción plantillas toosend multiplataforma</span><span class="sxs-lookup"><span data-stu-id="4e8cd-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="4e8cd-219">plantillas de tooregister, pasar plantillas con su **client.push registerDeviceToken** método en la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="4e8cd-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="4e8cd-221">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="4e8cd-222">Las plantillas son del tipo NSDictionary y pueden contener varias plantillas en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="4e8cd-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="4e8cd-224">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="4e8cd-225">Se eliminan todas las etiquetas de solicitud de hello para la seguridad.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="4e8cd-226">tooadd etiquetas tooinstallations o plantillas en las instalaciones, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][4].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="4e8cd-227">notificaciones de toosend mediante estas plantillas registradas, trabajar con [API de los centros de notificación][3].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="4e8cd-228"><a name="errors"></a>Gestión de errores</span><span class="sxs-lookup"><span data-stu-id="4e8cd-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="4e8cd-229">Cuando se llama a un servicio de aplicaciones de Azure de back-end móvil, bloque de finalización de hello contiene un `NSError` parámetro.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="4e8cd-230">En caso de producirse un error, este parámetro no será nulo.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="4e8cd-231">En el código, debe comprobar este parámetro y controlar el error de hello según sea necesario, como se muestra en hello anterior fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="4e8cd-232">archivo hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] define las constantes de hello `MSErrorResponseKey`, `MSErrorRequestKey`, y `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="4e8cd-233">tooget más datos relacionados con error de toohello:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="4e8cd-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="4e8cd-235">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="4e8cd-236">Además, el archivo hello define constantes para cada código de error:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="4e8cd-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="4e8cd-238">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="4e8cd-239"><a name="adal"></a>Cómo: autenticar a los usuarios con hello biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e8cd-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="4e8cd-240">Puede usar los usuarios de toosign de hello biblioteca de autenticación de Active Directory (ADAL) en la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="4e8cd-241">Autenticación de flujo del cliente mediante un proveedor de identidades SDK es preferible toousing hello `loginWithProvider:completion:` método.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="4e8cd-242">Este tipo de autenticación proporciona una experiencia de usuario más nativa y permite realizar más personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="4e8cd-243">Configurar el aplicación móvil de back-end para el inicio de sesión AAD Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Active Directory] [ 7] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="4e8cd-244">Asegúrese de que paso opcional de Hola de toocomplete de registrar una aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="4e8cd-245">Para iOS, se recomienda que redirección Hola URI tiene forma de Hola `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="4e8cd-246">Para obtener más información, vea hello [inicio rápido de iOS ADAL][8].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="4e8cd-247">Instale ADAL mediante Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="4e8cd-248">Editar el Hola de tooinclude Podfile después de la definición, reemplazar **su proyecto** con nombre de Hola de su proyecto de Xcode:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="4e8cd-249">hello Pod y:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="4e8cd-250">Usar Hola Terminal, ejecute `pod install` desde el directorio de hello, que contiene el proyecto y abra Hola genera Xcode área de trabajo (no en proyecto de hello).</span><span class="sxs-lookup"><span data-stu-id="4e8cd-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="4e8cd-251">Agregar Hola tras la aplicación de código tooyour, según el idioma de toohello que está usando.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="4e8cd-252">En cada uno, realice estas sustituciones:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="4e8cd-253">Reemplace **aquí de autoridad de INSERCIÓN** por nombre de Hola de inquilino de hello en el que se aprovisiona la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="4e8cd-254">El formato debería ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Este valor se puede copiar desde la pestaña del dominio hello en Azure Active Directory en hello [portal de Azure clásico].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="4e8cd-255">Reemplace **Insertar recurso identificador aquí** con el identificador de cliente de Hola para su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="4e8cd-256">Puede obtener el identificador de cliente de hello **avanzadas** en la ficha **configuración de Azure Active Directory** en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="4e8cd-257">Reemplace **INSERT-CLIENT-ID-aquí** con el Id. de cliente de Hola que copió de la aplicación de cliente nativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="4e8cd-258">Reemplace **INSERT-REDIRECT-URI-aquí** con su sitio */.auth/login/done* punto de conexión, mediante el esquema de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="4e8cd-259">Este valor debe ser similar demasiado*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="4e8cd-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-260">**Objective-C**:</span></span>

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


<span data-ttu-id="4e8cd-261">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
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

## <span data-ttu-id="4e8cd-262"><a name="facebook-sdk"></a>Cómo: autenticar a los usuarios con hello Facebook SDK para iOS</span><span class="sxs-lookup"><span data-stu-id="4e8cd-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="4e8cd-263">Puede usar Hola Facebook SDK para los usuarios de toosign de iOS en la aplicación con Facebook.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="4e8cd-264">Mediante la autenticación de un flujo de cliente es preferible toousing hello `loginWithProvider:completion:` método.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="4e8cd-265">autenticación de flujo de cliente de Hello proporciona una idea UX más nativa y permite la personalización adicional.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="4e8cd-266">Configure su aplicación móvil de back-end para el inicio de sesión Facebook siguiendo el [cómo tooconfigure aplicación de servicio de inicio de sesión de Facebook] [ 9] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="4e8cd-267">Instalar Hola Facebook SDK para iOS por hello siguiente [Facebook SDK para iOS: Introducción a] [ 10] documentación.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="4e8cd-268">En lugar de crear una aplicación, puede agregar el registro existente de tooyour la plataforma iOS Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="4e8cd-269">Documentación de Facebook incluye algún código Objective-C en hello delegado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="4e8cd-270">Si utilizas **Swift**, puede usar Hola siguiendo las traducciones de AppDelegate.swift:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
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
4. <span data-ttu-id="4e8cd-271">En suma tooadding `FBSDKCoreKit.framework` tooyour proyecto de equipo y agregar una referencia demasiado`FBSDKLoginKit.framework` Hola igual.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="4e8cd-272">Agregar Hola tras la aplicación de código tooyour, según el idioma de toohello que está usando.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="4e8cd-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-273">**Objective-C**:</span></span>

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

<span data-ttu-id="4e8cd-274">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
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

## <span data-ttu-id="4e8cd-275"><a name="twitter-fabric"></a>Autenticación de usuarios con Fabric de Twitter para iOS</span><span class="sxs-lookup"><span data-stu-id="4e8cd-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="4e8cd-276">Puede usar a tejido para los usuarios de toosign de iOS en la aplicación con Twitter.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="4e8cd-277">Flujo de autenticación del cliente es preferible toousing hello `loginWithProvider:completion:` método, tal como se proporciona una idea UX más nativa y permite la personalización adicional.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="4e8cd-278">Configurar el aplicación móvil de back-end para el inicio de sesión Twitter Hola después [cómo tooconfigure aplicación de servicio de inicio de sesión de Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="4e8cd-279">Agregar proyecto de tejido tooyour Hola siguiente [tejidos para iOS: Getting Started] documentación y la configuración de TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4e8cd-280">De forma predeterminada, Fabric creará automáticamente una aplicación de Twitter.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="4e8cd-281">Puede evitar la creación de una aplicación registrando hello clave de consumidor y secreto de consumidor que se creó anteriormente con hello siguientes fragmentos de código.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="4e8cd-282">Como alternativa, puede reemplazar Hola clave de consumidor y valores de secreto de consumidor que proporcione valores tooApp servicio con hello, vea Hola [panel del tejido].</span><span class="sxs-lookup"><span data-stu-id="4e8cd-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="4e8cd-283">Si elige esta opción, ser seguro tooset Hola devolución de llamada URL tooa valor marcador de posición, como `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="4e8cd-284">Si elige toouse secretos de Hola que creó anteriormente, agregue Hola después código tooyour delegado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="4e8cd-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-285">**Objective-C**:</span></span>

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

    <span data-ttu-id="4e8cd-286">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="4e8cd-287">Agregar Hola tras la aplicación de código tooyour, según el idioma de toohello que está usando.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="4e8cd-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-288">**Objective-C**:</span></span>

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

<span data-ttu-id="4e8cd-289">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-289">**Swift**:</span></span>

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

## <span data-ttu-id="4e8cd-290"><a name="google-sdk"></a>Cómo: autenticar a los usuarios con hello SDK de inicio de sesión de Google para iOS</span><span class="sxs-lookup"><span data-stu-id="4e8cd-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="4e8cd-291">Puede usar Hola SDK de inicio de sesión de Google para los usuarios de toosign de iOS en su aplicación mediante una cuenta de Google.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="4e8cd-292">Google ha anunciado recientemente directivas de seguridad de OAuth de tootheir de cambios.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="4e8cd-293">Estos cambios de directiva requerirá el uso de hello del SDK de Google en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="4e8cd-294">Configurar el aplicación móvil de back-end para el inicio de sesión en Google Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Google](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="4e8cd-295">Instalar Hola Google SDK para iOS por hello siguiente [Google Sign-In for iOS: empezar a integrar](https://developers.google.com/identity/sign-in/ios/start-integrating) documentación.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="4e8cd-296">Puede omitir la sección de "Autenticar con un servidor de back-end" Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="4e8cd-297">Agregar Hola después del delegado tooyour `signIn:didSignInForUser:withError:` método, según el idioma de toohello que está usando.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="4e8cd-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="4e8cd-299">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="4e8cd-300">Asegúrese de que también agregar Hola después demasiado`application:didFinishLaunchingWithOptions:` en su aplicación, delegado, sustituyendo "SERVER_CLIENT_ID" hello mismo identificador que utilizó tooconfigure servicio de aplicaciones en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="4e8cd-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="4e8cd-302">**SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="4e8cd-303">Agregar Hola tras la aplicación de tooyour de código en un UIViewController que implementa hello `GIDSignInUIDelegate` protocolo, según el idioma de toohello que está usando.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="4e8cd-304">Cierre sesión antes de iniciar sesión nuevo y, aunque no es necesario tooenter sus credenciales de nuevo, verá un cuadro de diálogo de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="4e8cd-305">Solo llame a este método cuando ha expirado el token de sesión Hola.</span><span class="sxs-lookup"><span data-stu-id="4e8cd-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="4e8cd-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="4e8cd-307">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="4e8cd-307">**Swift**:</span></span>

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
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[inicio rápido de Azure Mobile Apps]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[esquema dinámico]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[panel del tejido]: https://www.fabric.io/home
[tejidos para iOS: Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html
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
