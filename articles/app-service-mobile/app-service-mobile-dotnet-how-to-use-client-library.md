---
title: "aaaWorking con hello aplicación del servicio de aplicaciones móviles administradas biblioteca de cliente (Windows | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse un cliente de .NET para aplicaciones de Azure aplicación servicio Mobile con aplicaciones de Windows y Xamarin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="88aa7-103">Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="88aa7-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="88aa7-104">Información general</span><span class="sxs-lookup"><span data-stu-id="88aa7-104">Overview</span></span>
<span data-ttu-id="88aa7-105">Esta guía le mostrará cómo tooperform escenarios comunes con hello administración la biblioteca de cliente para aplicaciones de la aplicación de Azure Mobile de servicio de aplicaciones para Windows y Xamarin.</span><span class="sxs-lookup"><span data-stu-id="88aa7-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="88aa7-106">Si está tooMobile de nuevas aplicaciones, debe considerar primera Hola completando [inicio rápido de aplicaciones móviles de Azure] [ 1] tutorial.</span><span class="sxs-lookup"><span data-stu-id="88aa7-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="88aa7-107">Esta guía se centra en hello-cliente administrado SDK.</span><span class="sxs-lookup"><span data-stu-id="88aa7-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="88aa7-108">toolearn Obtenga más información sobre hello servidor SDK para aplicaciones móviles, consulte la documentación de Hola para hello [.NET Server SDK] [ 2] o [Node.js Server SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="88aa7-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="88aa7-109">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="88aa7-109">Reference documentation</span></span>
<span data-ttu-id="88aa7-110">Hello documentación de referencia de SDK de cliente de Hola se encuentra aquí: [referencia de cliente de .NET de aplicaciones móviles de Azure][4].</span><span class="sxs-lookup"><span data-stu-id="88aa7-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="88aa7-111">También puede encontrar varios ejemplos de cliente hello [repositorio de GitHub de ejemplos de Azure][5].</span><span class="sxs-lookup"><span data-stu-id="88aa7-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="88aa7-112">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="88aa7-112">Supported Platforms</span></span>
<span data-ttu-id="88aa7-113">Hola plataforma .NET admite Hola siguientes plataformas:</span><span class="sxs-lookup"><span data-stu-id="88aa7-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="88aa7-114">Versiones de Xamarin Android para niveles de API 19-24 (de KitKat a Nougat)</span><span class="sxs-lookup"><span data-stu-id="88aa7-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="88aa7-115">Versiones de Xamarin iOS para iOS 8.0 y posterior</span><span class="sxs-lookup"><span data-stu-id="88aa7-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="88aa7-116">Plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="88aa7-116">Universal Windows Platform</span></span>
* <span data-ttu-id="88aa7-117">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="88aa7-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="88aa7-118">Windows Phone 8.0, salvo para aplicaciones de Silverlight</span><span class="sxs-lookup"><span data-stu-id="88aa7-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="88aa7-119">la autenticación de "flujo de servidor" Hello usa un WebView para hello presentada la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="88aa7-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="88aa7-120">Si el dispositivo de hello no es capaz de toopresent una UI WebView, se necesitan otros métodos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="88aa7-121">Por tanto, este SDK no es adecuado para dispositivos de tipo reloj o con restricciones similares.</span><span class="sxs-lookup"><span data-stu-id="88aa7-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="88aa7-122"><a name="setup"></a>Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="88aa7-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="88aa7-123">Se supone que ya ha creado y publicado el proyecto de back-end de la aplicación móvil, que incluye al menos una tabla.</span><span class="sxs-lookup"><span data-stu-id="88aa7-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="88aa7-124">En el código de hello utilizado en este tema, se denomina tabla de hello `TodoItem` y tiene Hola siguientes columnas: `Id`, `Text`, y `Complete`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="88aa7-125">Esta tabla es hello misma tabla se crea al completar la [inicio rápido de aplicaciones móviles de Azure][1].</span><span class="sxs-lookup"><span data-stu-id="88aa7-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="88aa7-126">tipo de cliente con tipo correspondiente del Hello en C# es hello después de clase:</span><span class="sxs-lookup"><span data-stu-id="88aa7-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="88aa7-127">Hola [JsonPropertyAttribute] [ 6] es toodefine usado hello *PropertyName* la asignación entre los campos de cliente de Hola y Hola tabla.</span><span class="sxs-lookup"><span data-stu-id="88aa7-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="88aa7-128">toolearn cómo toocreate tablas en el back-end de aplicaciones móviles, consulte hello [tema de SDK de .NET Server] [ 7] o hello [tema de SDK de servidor Node.js] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="88aa7-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="88aa7-129">Si ha creado su aplicación móvil de back-end en hello Azure portal con Hola inicio rápido, también puede usar hello **tablas fácil** en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="88aa7-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="88aa7-130">Cómo: instalar Hola administra el paquete del SDK de cliente</span><span class="sxs-lookup"><span data-stu-id="88aa7-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="88aa7-131">Uso de hello después hello tooinstall de métodos administrados paquete SDK de cliente para aplicaciones móviles de [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="88aa7-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="88aa7-132">**Visual Studio** haga clic en el proyecto, haga clic en **administrar paquetes de NuGet**, busque hello `Microsoft.Azure.Mobile.Client` del paquete, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="88aa7-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="88aa7-133">**Xamarin Studio** haga clic en el proyecto, haga clic en **agregar** > **agregar paquetes de NuGet**, busque hello `Microsoft.Azure.Mobile.Client `del paquete y, a continuación, haga clic en **agregar Paquete**.</span><span class="sxs-lookup"><span data-stu-id="88aa7-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="88aa7-134">En el archivo de actividad principal, recuerde siguiente de Hola de tooadd **con** instrucción:</span><span class="sxs-lookup"><span data-stu-id="88aa7-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="88aa7-135"><a name="symbolsource"></a>Trabajo con símbolos de depuración en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88aa7-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="88aa7-136">símbolos de Hello para el espacio de nombres de hello Microsoft.Azure.Mobile están disponibles en [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="88aa7-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="88aa7-137">Consulte toothe [SymbolSource instrucciones] [ 11] toointegrate SymbolSource con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88aa7-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="88aa7-138"><a name="create-client"></a>Crear el cliente de aplicaciones móviles de Hola</span><span class="sxs-lookup"><span data-stu-id="88aa7-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="88aa7-139">Hello siguiente código crea hello [MobileServiceClient] [ 12] objeto tooaccess usa su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="88aa7-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="88aa7-140">En el anterior código de hello, reemplace `MOBILE_APP_URL` por dirección URL de Hola de back-end de aplicación móvil de hello, que se encuentra en la hoja para su aplicación móvil de back-end en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="88aa7-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="88aa7-141">MobileServiceClient (objeto) Hola debe ser un singleton.</span><span class="sxs-lookup"><span data-stu-id="88aa7-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="88aa7-142">Trabajo con tablas</span><span class="sxs-lookup"><span data-stu-id="88aa7-142">Work with Tables</span></span>
<span data-ttu-id="88aa7-143">Hola la siguiente sección se detallan cómo toosearch y recuperar registros y modificar los datos de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="88aa7-144">se trata Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="88aa7-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="88aa7-145">referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="88aa7-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="88aa7-146">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="88aa7-146">Query data</span></span>](#querying)
* [<span data-ttu-id="88aa7-147">Filtro de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="88aa7-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="88aa7-148">Ordenar datos devueltos</span><span class="sxs-lookup"><span data-stu-id="88aa7-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="88aa7-149">Devolver datos en páginas</span><span class="sxs-lookup"><span data-stu-id="88aa7-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="88aa7-150">Seleccionar columnas específicas</span><span class="sxs-lookup"><span data-stu-id="88aa7-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="88aa7-151">Buscar un registro por identificador</span><span class="sxs-lookup"><span data-stu-id="88aa7-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="88aa7-152">Trabajar con consultas sin tipo</span><span class="sxs-lookup"><span data-stu-id="88aa7-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="88aa7-153">Insertar datos</span><span class="sxs-lookup"><span data-stu-id="88aa7-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="88aa7-154">Actualizar datos</span><span class="sxs-lookup"><span data-stu-id="88aa7-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="88aa7-155">Eliminar datos</span><span class="sxs-lookup"><span data-stu-id="88aa7-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="88aa7-156">Resolución de conflictos y simultaneidad optimista</span><span class="sxs-lookup"><span data-stu-id="88aa7-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="88aa7-157">Enlace tooa interfaz de usuario de Windows</span><span class="sxs-lookup"><span data-stu-id="88aa7-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="88aa7-158">Cambiar tamaño de página de Hola</span><span class="sxs-lookup"><span data-stu-id="88aa7-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="88aa7-159"><a name="instantiating"></a>Creación de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="88aa7-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="88aa7-160">Todo el código de hello que obtiene acceso o modifica los datos de una tabla de back-end llama a funciones en hello `MobileServiceTable` objeto.</span><span class="sxs-lookup"><span data-stu-id="88aa7-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="88aa7-161">Obtener una tabla de referencia toohello Hola llamada [GetTable] método, tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88aa7-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="88aa7-162">Hola devuelve el objeto utiliza el modelo de serialización con tipo hello.</span><span class="sxs-lookup"><span data-stu-id="88aa7-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="88aa7-163">También se admite un modelo de serialización sin tipo.</span><span class="sxs-lookup"><span data-stu-id="88aa7-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="88aa7-164">En el ejemplo siguiente se [crea una tabla sin tipo de referencia tooan]:</span><span class="sxs-lookup"><span data-stu-id="88aa7-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="88aa7-165">En las consultas sin tipo, debe especificar Hola subyacente de la cadena de consulta de OData.</span><span class="sxs-lookup"><span data-stu-id="88aa7-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="88aa7-166"><a name="querying"></a>Consulta de datos desde la aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="88aa7-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="88aa7-167">Esta sección describe cómo tooissue las consultas toohello aplicación móvil back-end, que incluye Hola siguiente funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="88aa7-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="88aa7-168">Filtro de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="88aa7-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="88aa7-169">Ordenar datos devueltos</span><span class="sxs-lookup"><span data-stu-id="88aa7-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="88aa7-170">Devolver datos en páginas</span><span class="sxs-lookup"><span data-stu-id="88aa7-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="88aa7-171">Seleccionar columnas específicas</span><span class="sxs-lookup"><span data-stu-id="88aa7-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="88aa7-172">Buscar datos por identificador</span><span class="sxs-lookup"><span data-stu-id="88aa7-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="88aa7-173">Un tamaño de página controlado por el servidor es tooprevent aplica todas las filas se devuelva.</span><span class="sxs-lookup"><span data-stu-id="88aa7-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="88aa7-174">Paginación mantiene las solicitudes de manera predeterminada para grandes conjuntos de datos no afecten negativamente a servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="88aa7-175">tooreturn más de 50 filas, utilice hello `Skip` y `Take` método, como se describe en [devolver datos en páginas](#paging).</span><span class="sxs-lookup"><span data-stu-id="88aa7-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="88aa7-176"><a name="filtering"></a>Filtro de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="88aa7-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="88aa7-177">Hello código siguiente muestra cómo toofilter datos mediante la inclusión de un `Where` cláusula en una consulta.</span><span class="sxs-lookup"><span data-stu-id="88aa7-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="88aa7-178">Devuelve todos los elementos de `todoTable` cuyo `Complete` propiedad es igual demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="88aa7-179">Hola [donde] función aplica un predicado de consulta de hello en la tabla de Hola de filtrado de filas.</span><span class="sxs-lookup"><span data-stu-id="88aa7-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="88aa7-180">Puede ver Hola URI de hello solicitud enviada toohello back-end mediante software de inspección de mensaje, como herramientas de desarrollo de explorador o [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="88aa7-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="88aa7-181">Si observa en el URI de solicitud de hello, tenga en cuenta que se modifica la cadena de consulta de hello:</span><span class="sxs-lookup"><span data-stu-id="88aa7-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="88aa7-182">Esta solicitud de OData se convierte en una consulta SQL por hello SDK del servidor:</span><span class="sxs-lookup"><span data-stu-id="88aa7-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="88aa7-183">Hola de función que se pasa toohello `Where` método puede tener un número arbitrario de condiciones.</span><span class="sxs-lookup"><span data-stu-id="88aa7-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="88aa7-184">En este ejemplo se traduciría en una consulta SQL por hello SDK del servidor:</span><span class="sxs-lookup"><span data-stu-id="88aa7-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="88aa7-185">Esta consulta también se puede dividir en varias cláusulas:</span><span class="sxs-lookup"><span data-stu-id="88aa7-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="88aa7-186">Hola dos métodos son equivalentes y se pueden usar indistintamente.</span><span class="sxs-lookup"><span data-stu-id="88aa7-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="88aa7-187">Hola opción anterior&mdash;de concatenar varios predicados en una consulta&mdash;más compacto y recomendada.</span><span class="sxs-lookup"><span data-stu-id="88aa7-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="88aa7-188">Hola `Where` cláusula admite operaciones que pueden convertir en subconjunto de OData de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="88aa7-189">Estas son algunas de las operaciones:</span><span class="sxs-lookup"><span data-stu-id="88aa7-189">Operations include:</span></span>

* <span data-ttu-id="88aa7-190">Operadores relacionales (==, !=, <, <=, >, >=)</span><span class="sxs-lookup"><span data-stu-id="88aa7-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="88aa7-191">Operadores aritméticos (+, -, /, *, %)</span><span class="sxs-lookup"><span data-stu-id="88aa7-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="88aa7-192">Precisión numérica (Math.Floor, Math.Ceiling)</span><span class="sxs-lookup"><span data-stu-id="88aa7-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="88aa7-193">Funciones de cadena (Length, Substring, Replace, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="88aa7-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="88aa7-194">Propiedades de fecha (Year, Month, Day, Hour, Minute, Second)</span><span class="sxs-lookup"><span data-stu-id="88aa7-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="88aa7-195">Propiedades de acceso de un objeto</span><span class="sxs-lookup"><span data-stu-id="88aa7-195">Access properties of an object, and</span></span>
* <span data-ttu-id="88aa7-196">Expresiones combinando cualquiera de estas operaciones</span><span class="sxs-lookup"><span data-stu-id="88aa7-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="88aa7-197">Si es compatible con teniendo en cuenta qué Hola Server SDK, puede considerar hello [OData v3 documentación].</span><span class="sxs-lookup"><span data-stu-id="88aa7-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="88aa7-198"><a name="sorting"></a>Clasificación de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="88aa7-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="88aa7-199">Hello código siguiente muestra cómo toosort datos mediante la inclusión de un [OrderBy] o [OrderByDescending] función de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="88aa7-200">Devuelve elementos de `todoTable` ordena de forma ascendente por hello `Text` campo.</span><span class="sxs-lookup"><span data-stu-id="88aa7-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="88aa7-201"><a name="paging"></a>Devolución de datos en páginas</span><span class="sxs-lookup"><span data-stu-id="88aa7-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="88aa7-202">De forma predeterminada, Hola back-end devuelve solo Hola primeras 50 filas.</span><span class="sxs-lookup"><span data-stu-id="88aa7-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="88aa7-203">Puede aumentar Hola número de filas devueltas por llamada hello [tomar] método.</span><span class="sxs-lookup"><span data-stu-id="88aa7-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="88aa7-204">Use `Take` junto con hello [omitir] método toorequest una "página específica" del conjunto de datos total Hola devuelta por la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="88aa7-205">Hello consulta siguiente, cuando se ejecuta, devuelve Hola tres primeros elementos de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="88aa7-206">omite la siguiente consulta revisada Hola Hola tres primeros resultados y devuelve Hola siguientes tres resultados.</span><span class="sxs-lookup"><span data-stu-id="88aa7-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="88aa7-207">Esta consulta genera Hola segunda "página" de datos, donde el tamaño de página de hello es tres elementos.</span><span class="sxs-lookup"><span data-stu-id="88aa7-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="88aa7-208">Hola [IncludeTotalCount] método solicita el recuento total de Hola de *todos los* Hola registros que se hubieran devuelto, se omitirá cualquier cláusula de paginación/límite especificada:</span><span class="sxs-lookup"><span data-stu-id="88aa7-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="88aa7-209">En una aplicación del mundo real, puede usar consultas toohello similar anterior ejemplo con un control de paginación o la interfaz de usuario comparable para navegar entre las páginas.</span><span class="sxs-lookup"><span data-stu-id="88aa7-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="88aa7-210">límite de 50 filas de hello toooverride en un aplicación móvil de back-end, también debe aplicar hello [EnableQueryAttribute] toohello público GET (método) y especificar el comportamiento de paginación de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="88aa7-211">Cuando método de toohello aplicado, Hola después establece el número máximo de filas devuelto too1000:</span><span class="sxs-lookup"><span data-stu-id="88aa7-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="88aa7-212"><a name="selecting"></a>Selección de columnas específicas</span><span class="sxs-lookup"><span data-stu-id="88aa7-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="88aa7-213">Puede especificar qué conjunto de propiedades tooinclude Hola agregando un [seleccione] consulta tooyour de cláusula.</span><span class="sxs-lookup"><span data-stu-id="88aa7-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="88aa7-214">Por ejemplo, Hola siguiente de código muestra cómo tooselect en un solo campo y también cómo tooselect y dar formato a varios campos:</span><span class="sxs-lookup"><span data-stu-id="88aa7-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="88aa7-215">Todos los Hola funciones descritas hasta ahora son aditivas, por lo que se pueden mantener el encadenamiento de ellos.</span><span class="sxs-lookup"><span data-stu-id="88aa7-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="88aa7-216">Cada llamada encadenada afecta a más de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="88aa7-217">A continuación se muestra un ejemplo más:</span><span class="sxs-lookup"><span data-stu-id="88aa7-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="88aa7-218"><a name="lookingup"></a>Búsqueda de datos por identificador</span><span class="sxs-lookup"><span data-stu-id="88aa7-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="88aa7-219">Hola [LookupAsync] función puede ser toolook usa los objetos de base de datos de hello con un identificador determinado.</span><span class="sxs-lookup"><span data-stu-id="88aa7-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="88aa7-220"><a name="untypedqueries"></a>Ejecución de consultas sin tipo</span><span class="sxs-lookup"><span data-stu-id="88aa7-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="88aa7-221">Cuando se ejecuta una consulta con un objeto de tabla sin tipo, debe especificar explícitamente cadena de consulta de OData de hello mediante una llamada a [ReadAsync], como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="88aa7-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="88aa7-222">Vuelva a obtener valores JSON que puede usar como un contenedor de propiedades.</span><span class="sxs-lookup"><span data-stu-id="88aa7-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="88aa7-223">Para obtener más información sobre JToken y Newtonsoft Json.NET, vea hello [Json.NET] sitio.</span><span class="sxs-lookup"><span data-stu-id="88aa7-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="88aa7-224"><a name="inserting"></a>Inserción de datos en el back-end de una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="88aa7-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="88aa7-225">Todos los tipos de cliente deben incluir un miembro llamado **Id**, que es una cadena de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="88aa7-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="88aa7-226">Esto **identificador** es necesaria para realizar operaciones CRUD y para la sincronización sin conexión. Hola siguiente código ilustra cómo hello toouse [InsertAsync] tooinsert nuevas filas en una tabla de método.</span><span class="sxs-lookup"><span data-stu-id="88aa7-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="88aa7-227">parámetro Hello contiene Hola datos toobe insertado como un objeto. NET.</span><span class="sxs-lookup"><span data-stu-id="88aa7-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="88aa7-228">Si no se incluye un único valor de identificador personalizado en hello `todoItem` durante una inserción, un GUID generado por el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="88aa7-229">Puede recuperar Hola genera identificador mediante la inspección objeto Hola después Hola llamada devuelve.</span><span class="sxs-lookup"><span data-stu-id="88aa7-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="88aa7-230">tooinsert sin tipo de datos, puede sacar partido de Json.NET:</span><span class="sxs-lookup"><span data-stu-id="88aa7-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="88aa7-231">A continuación, se muestra un ejemplo en el que se usa una dirección de correo electrónico como identificador de cadena exclusivo:</span><span class="sxs-lookup"><span data-stu-id="88aa7-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="88aa7-232">Trabajar con valores de Id.</span><span class="sxs-lookup"><span data-stu-id="88aa7-232">Working with ID values</span></span>
<span data-ttu-id="88aa7-233">Aplicaciones móviles es compatible con los valores de cadena personalizado único para la tabla de hello **identificador** columna.</span><span class="sxs-lookup"><span data-stu-id="88aa7-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="88aa7-234">Un valor de cadena permite que las aplicaciones toouse valores personalizados, como direcciones de correo electrónico o nombres de usuario para Id. de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="88aa7-235">Identificadores de cadena proporcionan Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="88aa7-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="88aa7-236">Se generan identificadores sin crear una base de datos de toohello de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="88aa7-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="88aa7-237">Los registros son toomerge más fácil de diferentes tablas o bases de datos.</span><span class="sxs-lookup"><span data-stu-id="88aa7-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="88aa7-238">Los valores de los identificadores pueden integrarse mejor con una lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="88aa7-239">Si no se establece un valor de identificador de cadena en un registro insertado, back-end de aplicación móvil de hello genera un valor único para el identificador.</span><span class="sxs-lookup"><span data-stu-id="88aa7-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="88aa7-240">Puede usar hello [Guid.NewGuid] toogenerate método su propio Id. de valores, en el cliente de Hola o en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="88aa7-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="88aa7-241"><a name="modifying"></a>Modificación de datos en el back-end de una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="88aa7-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="88aa7-242">Hello código siguiente muestra cómo hello toouse [UpdateAsync] método tooupdate un registro existente con hello mismo identificador con la nueva información.</span><span class="sxs-lookup"><span data-stu-id="88aa7-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="88aa7-243">parámetro Hello contiene hello toobe de datos actualizado como un objeto. NET.</span><span class="sxs-lookup"><span data-stu-id="88aa7-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="88aa7-244">tooupdate sin tipo de datos, puede sacar partido de [Json.NET] como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88aa7-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="88aa7-245">Debe especificarse un campo `id` al realizar una actualización.</span><span class="sxs-lookup"><span data-stu-id="88aa7-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="88aa7-246">Hola back-end utiliza hello `id` tooidentify de campo que tooupdate de fila.</span><span class="sxs-lookup"><span data-stu-id="88aa7-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="88aa7-247">Hola `id` campo puede obtenerse de resultado de hello de hello `InsertAsync` llamar.</span><span class="sxs-lookup"><span data-stu-id="88aa7-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="88aa7-248">Un `ArgumentException` se produce si intenta tooupdate un elemento sin proporcionar hello `id` valor.</span><span class="sxs-lookup"><span data-stu-id="88aa7-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="88aa7-249"><a name="deleting"></a>Eliminación de datos del back-end de una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="88aa7-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="88aa7-250">Hello código siguiente muestra cómo hello toouse [DeleteAsync] método toodelete una instancia existente.</span><span class="sxs-lookup"><span data-stu-id="88aa7-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="88aa7-251">Hola instancia se identifica por hello `id` campo establecido en hello `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="88aa7-252">toodelete sin tipo de datos, puede sacar partido de Json.NET como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88aa7-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="88aa7-253">Al realizar una solicitud de eliminación, debe especificarse un identificador.</span><span class="sxs-lookup"><span data-stu-id="88aa7-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="88aa7-254">Otras propiedades no se pasan toohello servicio o se omiten al servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="88aa7-255">Hola resultado de un `DeleteAsync` suele ser llamada `null`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="88aa7-256">toopass de Id. de Hello en puede obtenerse de resultado de hello de hello `InsertAsync` llamar.</span><span class="sxs-lookup"><span data-stu-id="88aa7-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="88aa7-257">A `MobileServiceInvalidOperationException` se produce cuando intenta toodelete un elemento sin especificar hello `id` campo.</span><span class="sxs-lookup"><span data-stu-id="88aa7-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="88aa7-258"><a name="optimisticconcurrency"></a>Uso de la simultaneidad optimista para resolver conflictos</span><span class="sxs-lookup"><span data-stu-id="88aa7-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="88aa7-259">Dos o más clientes pueden escribir cambios toohello mismo elemento en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="88aa7-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="88aa7-260">Sin la detección de conflictos, última operación de escritura Hola reemplazaría las actualizaciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="88aa7-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="88aa7-261">**control de simultaneidad optimista** asume que cada transacción puede confirmarse y, por lo tanto, no usa ningún bloqueo de recursos.</span><span class="sxs-lookup"><span data-stu-id="88aa7-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="88aa7-262">Antes de confirmar una transacción, control de simultaneidad optimista comprueba que ninguna otra transacción ha modificado datos Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="88aa7-263">Si se han modificado los datos de hello, Hola confirmar la transacción se revierte.</span><span class="sxs-lookup"><span data-stu-id="88aa7-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="88aa7-264">Aplicaciones móviles admite el control de simultaneidad optimista al realizar un seguimiento de elemento de tooeach de cambios mediante hello `version` columna de propiedades del sistema que se define para cada tabla en el aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="88aa7-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="88aa7-265">Cada vez que se actualiza un registro, aplicaciones móviles establece hello `version` propiedad para que registre tooa nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="88aa7-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="88aa7-266">Durante cada solicitud de actualización, Hola `version` propiedad del registro de hello incluido en la solicitud de hello es toohello comparado misma propiedad de registro de hello en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="88aa7-267">Si la versión que se pasa con solicitud hello no coincide con el back-end de Hola, Hola biblioteca de cliente genera un `MobileServicePreconditionFailedException<T>` excepción.</span><span class="sxs-lookup"><span data-stu-id="88aa7-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="88aa7-268">tipo de Hello incluido con la excepción de hello es registro Hola de versión de servidores Hola contenedor de Hola de back-end de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="88aa7-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="88aa7-269">Hello aplicación puede utilizar esta información toodecide si tooexecute solicitud de actualización de hello nuevo con hello correcto `version` valor de los cambios de toocommit de hello back-end.</span><span class="sxs-lookup"><span data-stu-id="88aa7-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="88aa7-270">Definir una columna en la clase de tabla de Hola para hello `version` simultaneidad optimista de sistema propiedad tooenable.</span><span class="sxs-lookup"><span data-stu-id="88aa7-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="88aa7-271">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="88aa7-271">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="88aa7-272">Habilitar las aplicaciones que usan tablas sin tipo simultaneidad optimista establecer hello `Version` marca en el `SystemProperties` de hello tabla como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="88aa7-273">En la suma tooenabling optimista de simultaneidad, que debe detectar hello `MobileServicePreconditionFailedException<T>` excepción en el código cuando se llama a [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="88aa7-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="88aa7-274">Resolver conflicto de hello mediante la aplicación hello correcto `version` toothe actualizar registro y llame al método [UpdateAsync] con hello resolvió el registro.</span><span class="sxs-lookup"><span data-stu-id="88aa7-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="88aa7-275">Hola siguiente código muestra cómo tooresolve un conflicto de escritura una vez detectado:</span><span class="sxs-lookup"><span data-stu-id="88aa7-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="88aa7-276">Para obtener más información, vea hello [sin conexión la sincronización de datos en aplicaciones móviles de Azure] tema.</span><span class="sxs-lookup"><span data-stu-id="88aa7-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="88aa7-277"><a name="binding"></a>Cómo: interfaz de usuario de Windows tooa de aplicaciones móviles de enlace de datos</span><span class="sxs-lookup"><span data-stu-id="88aa7-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="88aa7-278">Esta sección muestra cómo toodisplay devuelve objetos de datos utilizando los elementos de interfaz de usuario de una aplicación de Windows.</span><span class="sxs-lookup"><span data-stu-id="88aa7-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="88aa7-279">El siguiente código de ejemplo enlaza origen toohello de lista de hello con una consulta para elementos incompletos.</span><span class="sxs-lookup"><span data-stu-id="88aa7-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="88aa7-280">[MobileServiceCollection] crea una colección de enlaces compatible con Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="88aa7-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="88aa7-281">Algunos controles Hola administran compatibilidad en tiempo de ejecución llama a una interfaz [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="88aa7-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="88aa7-282">Esta interfaz permite a los controles toorequest datos adicionales cuando se desplaza por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="88aa7-283">No hay compatibilidad integrada para esta interfaz para aplicaciones universales de Windows a través de [MobileServiceIncrementalLoadingCollection], que controla automáticamente las llamadas de los controles de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="88aa7-284">Use `MobileServiceIncrementalLoadingCollection` en aplicaciones Windows de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="88aa7-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="88aa7-285">toouse Hola nueva colección en aplicaciones de Windows Phone 8 y "Silverlight", use hello `ToCollection` métodos de extensión en `IMobileServiceTableQuery<T>` y `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="88aa7-286">datos de tooload, llame a `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="88aa7-287">Cuando se usa la colección de hello creada mediante una llamada a `ToCollectionAsync` o `ToCollection`, obtiene una colección que puede ser controles enlazados tooUI.</span><span class="sxs-lookup"><span data-stu-id="88aa7-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="88aa7-288">Esta colección es para la paginación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-288">This collection is paging-aware.</span></span>  <span data-ttu-id="88aa7-289">Puesto que la colección de hello está cargando datos de la red, a veces no se puede cargar.</span><span class="sxs-lookup"><span data-stu-id="88aa7-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="88aa7-290">toohandle tales errores, invalidar hello `OnException` método `MobileServiceIncrementalLoadingCollection` toohandle excepciones derivadas de llamadas demasiado`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="88aa7-291">Tenga en cuenta si la tabla tiene muchos campos, pero sólo desea toodisplay algunas de ellas en el control.</span><span class="sxs-lookup"><span data-stu-id="88aa7-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="88aa7-292">Puede usar instrucciones de Hola Hola sección anterior "[seleccionar columnas específicas](#selecting)" tooselect columnas específicas toodisplay Hola interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="88aa7-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="88aa7-293"><a name="pagesize"></a>Hola cambiar tamaño de página</span><span class="sxs-lookup"><span data-stu-id="88aa7-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="88aa7-294">Mobile Apps de Azure devuelve un máximo de 50 elementos por cada solicitud de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="88aa7-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="88aa7-295">Puede cambiar el tamaño de paginación de hello aumentando el tamaño de página máximo de hello en el cliente de Hola y el servidor.</span><span class="sxs-lookup"><span data-stu-id="88aa7-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="88aa7-296">tooincrease Hola tamaño de página solicitado, especifique `PullOptions` al usar `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="88aa7-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="88aa7-297">Suponiendo que haya realizado hello `PageSize` tooor igual superior a 100 en el servidor de hello, una solicitud devuelve hasta 100 elementos.</span><span class="sxs-lookup"><span data-stu-id="88aa7-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="88aa7-298"><a name="#offlinesync"></a>Trabajo con tablas sin conexión</span><span class="sxs-lookup"><span data-stu-id="88aa7-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="88aa7-299">Tablas sin conexión utilizan un almacén toostore datos local de SQLite para su uso sin conexión.</span><span class="sxs-lookup"><span data-stu-id="88aa7-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="88aa7-300">Tabla de todas las operaciones se realizan contra Hola SQLite local almacenar en lugar de almacén de servidor remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="88aa7-301">toocreate una tabla sin conexión, preparar el proyecto:</span><span class="sxs-lookup"><span data-stu-id="88aa7-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="88aa7-302">En Visual Studio, haga clic en soluciones de hello > **administrar paquetes de NuGet para la solución...** , a continuación, buscar e instalar el **Microsoft.Azure.Mobile.Client.SQLiteStore** paquete NuGet para todos los proyectos de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="88aa7-303">Dispositivos de Windows toosupport (opcional), instale uno de los siguientes paquetes en tiempo de ejecución de código de hello:</span><span class="sxs-lookup"><span data-stu-id="88aa7-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="88aa7-304">**Runtime de Windows 8.1:** instale [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="88aa7-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="88aa7-305">**Windows Phone 8.1:** instale [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="88aa7-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="88aa7-306">**Plataforma universal de Windows** instalar [SQLite para hello universales de Windows][5].</span><span class="sxs-lookup"><span data-stu-id="88aa7-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="88aa7-307">(Opcional).</span><span class="sxs-lookup"><span data-stu-id="88aa7-307">(Optional).</span></span> <span data-ttu-id="88aa7-308">Para dispositivos de Windows, haga clic en **referencias** > **Agregar referencia...** , expanda hello **Windows** carpeta > **extensiones**, a continuación, habilite Hola adecuado **SQLite para Windows** SDK junto con hello  **Visual C++ 2013 en tiempo de ejecución para Windows** SDK.</span><span class="sxs-lookup"><span data-stu-id="88aa7-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="88aa7-309">Hello SQLite SDK nombres varían ligeramente con cada plataforma de Windows.</span><span class="sxs-lookup"><span data-stu-id="88aa7-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="88aa7-310">Para poder crear una referencia de tabla, debe estar preparado almacén local de hello:</span><span class="sxs-lookup"><span data-stu-id="88aa7-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="88aa7-311">Inicialización del almacén se hace normalmente inmediatamente después de que se crea el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="88aa7-312">Hola **OfflineDbPath** debe ser un nombre de archivo adecuado para su uso en todas las plataformas que se admiten.</span><span class="sxs-lookup"><span data-stu-id="88aa7-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="88aa7-313">Si la ruta de acceso de hello es una ruta de acceso completa (es decir, se inicia con una barra diagonal), a continuación, se utiliza dicha ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="88aa7-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="88aa7-314">Si la ruta de acceso de hello no está completo, el archivo hello se coloca en una ubicación específica de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="88aa7-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="88aa7-315">Para dispositivos iOS y Android, ruta de acceso de hello predeterminada es la carpeta de "Archivos personales" de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="88aa7-316">Para dispositivos de Windows, ruta de acceso de hello predeterminada es "AppData" carpeta de hello específica de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="88aa7-317">Puede obtener una referencia de tabla mediante hello `GetSyncTable<>` método:</span><span class="sxs-lookup"><span data-stu-id="88aa7-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="88aa7-318">No es necesario tooauthenticate toouse una tabla sin conexión.</span><span class="sxs-lookup"><span data-stu-id="88aa7-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="88aa7-319">Solo debe tooauthenticate al que se está comunicando con el servicio back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="88aa7-320"><a name="syncoffline"></a>Sincronización de una tabla sin conexión</span><span class="sxs-lookup"><span data-stu-id="88aa7-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="88aa7-321">Tablas sin conexión no están sincronizadas con hello back-end de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="88aa7-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="88aa7-322">La sincronización se divide en dos partes.</span><span class="sxs-lookup"><span data-stu-id="88aa7-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="88aa7-323">Mediante la descarga de elementos nuevos puede insertar los cambios por separado.</span><span class="sxs-lookup"><span data-stu-id="88aa7-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="88aa7-324">Éste es un método de sincronización típico:</span><span class="sxs-lookup"><span data-stu-id="88aa7-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="88aa7-325">Si Hola primer argumento demasiado`PullAsync` es null, no se utiliza la sincronización incremental.</span><span class="sxs-lookup"><span data-stu-id="88aa7-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="88aa7-326">Todas las operaciones de sincronización recuperan todos los registros.</span><span class="sxs-lookup"><span data-stu-id="88aa7-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="88aa7-327">Hola SDK realiza implícita `PushAsync()` antes de extraer registros.</span><span class="sxs-lookup"><span data-stu-id="88aa7-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="88aa7-328">El control de los conflictos se realiza en un método `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="88aa7-329">Se puede resolver los conflictos en hello igual manera que las tablas en línea.</span><span class="sxs-lookup"><span data-stu-id="88aa7-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="88aa7-330">se produce el conflicto de Hello cuando `PullAsync()` se llama en lugar de durante Hola insert, update o delete.</span><span class="sxs-lookup"><span data-stu-id="88aa7-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="88aa7-331">Si se producen varios conflictos, se agrupan en una sola clase MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="88aa7-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="88aa7-332">Trate cada error por separado.</span><span class="sxs-lookup"><span data-stu-id="88aa7-332">Handle each failure separately.</span></span>

## <span data-ttu-id="88aa7-333"><a name="#customapi"></a>Trabajo con una API personalizada</span><span class="sxs-lookup"><span data-stu-id="88aa7-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="88aa7-334">Una API personalizada le permite toodefine extremos personalizados que exponen la funcionalidad de servidor que no asigne tooan Insertar, actualizar, eliminar o la operación de lectura.</span><span class="sxs-lookup"><span data-stu-id="88aa7-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="88aa7-335">Al usar una API personalizada, puede tener más control sobre la mensajería, incluida la lectura y el establecimiento de encabezados de mensajes HTTP y la definición del formato del cuerpo de un mensaje diferente de JSON.</span><span class="sxs-lookup"><span data-stu-id="88aa7-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="88aa7-336">Se llama a una API personalizada mediante una llamada a uno de hello [InvokeApiAsync] métodos en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="88aa7-337">Por ejemplo, después de la línea de código de hello envía una toohello de solicitud POST **completeAll** API en hello back-end:</span><span class="sxs-lookup"><span data-stu-id="88aa7-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="88aa7-338">Este formulario es una llamada de método con tipo y requiere que hello **MarkAllResult** devolver el tipo está definido.</span><span class="sxs-lookup"><span data-stu-id="88aa7-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="88aa7-339">Se admiten métodos con y sin tipos.</span><span class="sxs-lookup"><span data-stu-id="88aa7-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="88aa7-340">Hola InvokeApiAsync() método antepone/api/toohello API que desea toocall a menos que Hola API comienza con un '/'.</span><span class="sxs-lookup"><span data-stu-id="88aa7-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="88aa7-341">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="88aa7-341">For example:</span></span>

* <span data-ttu-id="88aa7-342">`InvokeApiAsync("completeAll",...)`llama a /api/completeAll en hello back-end</span><span class="sxs-lookup"><span data-stu-id="88aa7-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="88aa7-343">`InvokeApiAsync("/.auth/me",...)`llama a /.auth/me en hello back-end</span><span class="sxs-lookup"><span data-stu-id="88aa7-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="88aa7-344">Puede usar InvokeApiAsync toocall cualquier WebAPI, incluidos los que no estén definidos WebAPIs con aplicaciones de Azure Mobile.</span><span class="sxs-lookup"><span data-stu-id="88aa7-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="88aa7-345">Cuando usa InvokeApiAsync(), encabezados apropiados de hello, incluidos los encabezados de autenticación, se envían con la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="88aa7-346"><a name="authentication"></a>Autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="88aa7-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="88aa7-347">Mobile Apps es compatible con la autenticación y la autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externas: Facebook, Google, cuenta de Microsoft, Twitter y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="88aa7-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="88aa7-348">Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="88aa7-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="88aa7-349">También puede utilizar la identidad de Hola de reglas de autorización de los usuarios autenticados tooimplement en scripts de servidor.</span><span class="sxs-lookup"><span data-stu-id="88aa7-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="88aa7-350">Para obtener más información, vea el tutorial de hello [agregar autenticación tooyour aplicación].</span><span class="sxs-lookup"><span data-stu-id="88aa7-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="88aa7-351">Se admiten dos flujos de autenticación: *administrado por cliente* y *administrado por servidor*.</span><span class="sxs-lookup"><span data-stu-id="88aa7-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="88aa7-352">flujo de servidor administrado de Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de autenticación del proveedor de hello web.</span><span class="sxs-lookup"><span data-stu-id="88aa7-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="88aa7-353">flujo de Hello administrados por el cliente permite una integración más profunda con capacidades específicas del dispositivo tal y como se basa en el SDK de específica del proveedor específico del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="88aa7-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="88aa7-354">En las aplicaciones de producción se recomienda usar un flujo administrado por el cliente.</span><span class="sxs-lookup"><span data-stu-id="88aa7-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="88aa7-355">tooset la autenticación, debe registrar la aplicación con uno o varios proveedores de identidad.</span><span class="sxs-lookup"><span data-stu-id="88aa7-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="88aa7-356">proveedor de identidades de Hello genera un identificador de cliente y un secreto de cliente para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="88aa7-357">Estos valores, a continuación, se establecen en su tooenable de back-end autenticación/autorización de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="88aa7-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="88aa7-358">Para obtener más información, siga Hola instrucciones detalladas en el tutorial [agregar autenticación tooyour aplicación].</span><span class="sxs-lookup"><span data-stu-id="88aa7-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="88aa7-359">Hola temas siguientes se trata en esta sección:</span><span class="sxs-lookup"><span data-stu-id="88aa7-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="88aa7-360">Autenticación administrada por el cliente</span><span class="sxs-lookup"><span data-stu-id="88aa7-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="88aa7-361">Autenticación administrada por el servidor</span><span class="sxs-lookup"><span data-stu-id="88aa7-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="88aa7-362">Token de autenticación de almacenamiento en caché Hola</span><span class="sxs-lookup"><span data-stu-id="88aa7-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="88aa7-363"><a name="clientflow"></a>Autenticación administrada por el cliente</span><span class="sxs-lookup"><span data-stu-id="88aa7-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="88aa7-364">La aplicación puede independientemente en contacto con el proveedor de identidades de hello y, a continuación, proporcionar token devuelto Hola durante el inicio de sesión con el back-end.</span><span class="sxs-lookup"><span data-stu-id="88aa7-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="88aa7-365">Este flujo de cliente le permite tooprovide una experiencia de inicio de sesión única para los usuarios o los datos de usuario adicionales tooretrieve Hola del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="88aa7-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="88aa7-366">Autenticación del cliente flujo es preferido toousing un flujo de servidor como proveedor de identidades de hello SDK proporciona una idea UX más nativa y permite la personalización adicional.</span><span class="sxs-lookup"><span data-stu-id="88aa7-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="88aa7-367">Se proporcionan ejemplos para hello siguientes patrones de autenticación de flujo de cliente:</span><span class="sxs-lookup"><span data-stu-id="88aa7-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="88aa7-368">Biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="88aa7-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="88aa7-369">Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="88aa7-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="88aa7-370">SDK de Live</span><span class="sxs-lookup"><span data-stu-id="88aa7-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="88aa7-371"><a name="adal"></a>Autenticar a los usuarios con hello biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="88aa7-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="88aa7-372">Puede utilizar la autenticación de usuario de hello biblioteca de autenticación de Active Directory (ADAL) tooinitiate de cliente de hello mediante la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="88aa7-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="88aa7-373">Configurar el aplicación móvil de back-end para el inicio de sesión en AAD Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Active Directory] tutorial.</span><span class="sxs-lookup"><span data-stu-id="88aa7-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="88aa7-374">Asegúrese de que paso opcional de Hola de toocomplete de registrar una aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="88aa7-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="88aa7-375">En Visual Studio o Xamarin Studio, abra el proyecto y agregar una referencia toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="88aa7-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="88aa7-376">Al buscar, incluya las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="88aa7-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="88aa7-377">Agregar Hola tras la aplicación de código tooyour, según la plataforma de toohello que usa.</span><span class="sxs-lookup"><span data-stu-id="88aa7-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="88aa7-378">En cada una, asegúrese de Hola después reemplazos:</span><span class="sxs-lookup"><span data-stu-id="88aa7-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="88aa7-379">Reemplace **aquí de autoridad de INSERCIÓN** por nombre de Hola de inquilino de hello en el que se aprovisiona la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="88aa7-380">El formato debería ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Este valor se puede copiar desde la pestaña del dominio hello en Azure Active Directory en hello [portal de Azure clásico].</span><span class="sxs-lookup"><span data-stu-id="88aa7-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="88aa7-381">Reemplace **Insertar recurso identificador aquí** con el identificador de cliente de Hola para su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="88aa7-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="88aa7-382">Puede obtener Id. de cliente de Hola de hello **avanzadas** en la ficha **configuración de Azure Active Directory** en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="88aa7-383">Reemplace **INSERT-CLIENT-ID-aquí** con el Id. de cliente de Hola que copió de la aplicación de cliente nativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="88aa7-384">Reemplace **INSERT-REDIRECT-URI-aquí** con su sitio */.auth/login/done* punto de conexión, mediante el esquema de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="88aa7-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="88aa7-385">Este valor debe ser similar demasiado*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="88aa7-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="88aa7-386">código de Hello necesario para cada plataforma sigue:</span><span class="sxs-lookup"><span data-stu-id="88aa7-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="88aa7-387">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="88aa7-387">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="88aa7-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="88aa7-388">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="88aa7-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="88aa7-389">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="88aa7-390"><a name="client-facebook"></a>Inicio de sesión único mediante un token de Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="88aa7-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="88aa7-391">Puede usar flujo de cliente de hello tal y como se muestra en este fragmento de código para Facebook o Google.</span><span class="sxs-lookup"><span data-stu-id="88aa7-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="88aa7-392"><a name="client-livesdk"></a>Inicio de sesión único con Microsoft Account con Hola SDK de Live</span><span class="sxs-lookup"><span data-stu-id="88aa7-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="88aa7-393">los usuarios de tooauthenticate, debe registrar la aplicación en hello cuenta Centro para desarrolladores de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="88aa7-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="88aa7-394">Configure los detalles del registro en su back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="88aa7-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="88aa7-395">toocreate Microsoft el registro de cuenta y conexión back-end de tooyour aplicación móvil, Hola completa los pasos de [registrar su toouse de aplicación un inicio de sesión de cuenta de Microsoft].</span><span class="sxs-lookup"><span data-stu-id="88aa7-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="88aa7-396">Si tiene las versiones de tienda Windows y Windows Phone 8/Silverlight de la aplicación, registre primero la versión de tienda Windows hello.</span><span class="sxs-lookup"><span data-stu-id="88aa7-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="88aa7-397">Hello código siguiente se autentica mediante Live SDK y utiliza Hola devuelve toosign token en el back-end de tooyour aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="88aa7-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="88aa7-398">Para obtener más información, vea hello [Windows Live SDK] documentación.</span><span class="sxs-lookup"><span data-stu-id="88aa7-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="88aa7-399"><a name="serverflow"></a>Autenticación administrada por el servidor</span><span class="sxs-lookup"><span data-stu-id="88aa7-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="88aa7-400">Una vez que ha registrado el proveedor de identidad, llame a hello [LoginAsync] método en hello [MobileServiceClient] con hello [MobileServiceAuthenticationProvider] valor del proveedor.</span><span class="sxs-lookup"><span data-stu-id="88aa7-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="88aa7-401">Por ejemplo, hello código siguiente inicia un inicio de sesión de flujo de servidor mediante el uso de Facebook.</span><span class="sxs-lookup"><span data-stu-id="88aa7-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="88aa7-402">Si está utilizando un proveedor de identidades distinto a Facebook, cambie el valor de Hola de [MobileServiceAuthenticationProvider] toohello valor para el proveedor.</span><span class="sxs-lookup"><span data-stu-id="88aa7-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="88aa7-403">En un flujo de servidor, servicio de aplicaciones de Azure administra el flujo de autenticación de OAuth de hello mostrando la página de inicio de sesión de Hola de proveedor seleccionado Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="88aa7-404">Una vez devuelve de proveedor de identidad de hello, servicio de aplicaciones de Azure genera un token de autenticación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="88aa7-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="88aa7-405">Hola [LoginAsync] método devuelve un [MobileServiceUser], que proporciona ambos hello [UserId] de hello autenticado hello y usuario [ MobileServiceAuthenticationToken], como un token de web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="88aa7-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="88aa7-406">El token puede almacenarse en caché y volver a usarse hasta que expire.</span><span class="sxs-lookup"><span data-stu-id="88aa7-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="88aa7-407">Para obtener más información, consulte [token de autenticación de almacenamiento en caché hello](#caching).</span><span class="sxs-lookup"><span data-stu-id="88aa7-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="88aa7-408"><a name="caching"></a>Token de autenticación de almacenamiento en caché Hola</span><span class="sxs-lookup"><span data-stu-id="88aa7-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="88aa7-409">En algunos casos, se puede evitar método de inicio de sesión de hello llamada toohello después de la primera autenticación correcta de hello almacenando el token de autenticación de Hola de proveedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="88aa7-410">Pueden utilizar aplicaciones de la tienda Windows y UWP [PasswordVault] toocache la autenticación actual token después una correcta inicio de sesión, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88aa7-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="88aa7-411">Hola valor de identificador de usuario se almacena como nombre de usuario de la credencial de Hola Hola y token hello es hello almacenado como Hola contraseña.</span><span class="sxs-lookup"><span data-stu-id="88aa7-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="88aa7-412">En las nuevas empresas posteriores, puede comprobar hello **PasswordVault** para credenciales almacenadas en caché.</span><span class="sxs-lookup"><span data-stu-id="88aa7-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="88aa7-413">Hello en el ejemplo siguiente se usa credenciales almacenadas en caché cuando se encuentran y, en caso contrario, intente tooauthenticate nuevo con hello back-end:</span><span class="sxs-lookup"><span data-stu-id="88aa7-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="88aa7-414">Cuando inicia sesión un usuario, también debe quitar credencial Hola almacenado, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88aa7-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="88aa7-415">Aplicaciones Xamarin usan hello [Xamarin.Auth] las credenciales del almacén de toosecurely de API en un **cuenta** objeto.</span><span class="sxs-lookup"><span data-stu-id="88aa7-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="88aa7-416">Para obtener un ejemplo del uso de estas API, consulte hello [AuthStore.cs] archivo de código en hello [ejemplo de uso compartido de fotografías de ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="88aa7-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="88aa7-417">Al utilizar la autenticación de cliente administrada, también puede almacenar en caché los token de acceso de hello obtenido de su proveedor, como Facebook o Twitter.</span><span class="sxs-lookup"><span data-stu-id="88aa7-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="88aa7-418">Este token puede ser proporcionado toorequest un nuevo token de autenticación de back-end de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88aa7-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="88aa7-419"><a name="pushnotifications"></a>Notificaciones push</span><span class="sxs-lookup"><span data-stu-id="88aa7-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="88aa7-420">Hello en los temas siguientes tratan las notificaciones de inserción:</span><span class="sxs-lookup"><span data-stu-id="88aa7-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="88aa7-421">Registro de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="88aa7-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="88aa7-422">Obtención del SID de un paquete de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="88aa7-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="88aa7-423">Registro con plantillas multiplataforma</span><span class="sxs-lookup"><span data-stu-id="88aa7-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="88aa7-424"><a name="register-for-push"></a>Cómo registrarse para recibir notificaciones push</span><span class="sxs-lookup"><span data-stu-id="88aa7-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="88aa7-425">cliente de aplicaciones móviles de Hello permite tooregister para las notificaciones de inserción con centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="88aa7-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="88aa7-426">Al registrar, se obtiene un identificador que obtiene de hello específica de la plataforma servicio de notificación de inserción (PNS).</span><span class="sxs-lookup"><span data-stu-id="88aa7-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="88aa7-427">A continuación, proporcionar este valor junto con las etiquetas cuando se crea el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="88aa7-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="88aa7-428">Hola de código siguiente registra la aplicación de Windows para las notificaciones de inserción con hello servicios de notificación de Windows (WNS):</span><span class="sxs-lookup"><span data-stu-id="88aa7-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="88aa7-429">Si va a insertar tooWNS, entonces debe [obtener un paquete de la tienda Windows SID](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="88aa7-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="88aa7-430">Para obtener más información sobre aplicaciones de Windows, incluyendo cómo tooregister para registros de plantilla, consulte [aplicación de tooyour de notificaciones de inserción de agregar].</span><span class="sxs-lookup"><span data-stu-id="88aa7-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="88aa7-431">No se admite la solicitud de etiquetas de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="88aa7-432">Las solicitudes de etiquetas se quitan del registro en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="88aa7-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="88aa7-433">Si desea que el dispositivo con etiquetas tooregister, cree una API personalizada que utiliza el registro de hello API de bases de datos centrales de notificación tooperform hello en su nombre.</span><span class="sxs-lookup"><span data-stu-id="88aa7-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="88aa7-434">[Llamar a API personalizada hello](#customapi) en lugar de hello `RegisterNativeAsync()` método.</span><span class="sxs-lookup"><span data-stu-id="88aa7-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="88aa7-435"><a name="package-sid"></a>Obtención del SID de un paquete de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="88aa7-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="88aa7-436">Se necesita un SID de paquete para habilitar las notificaciones push en aplicaciones de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="88aa7-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="88aa7-437">tooreceive un SID, del paquete registrando su aplicación con hello tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="88aa7-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="88aa7-438">tooobtain este valor:</span><span class="sxs-lookup"><span data-stu-id="88aa7-438">tooobtain this value:</span></span>

1. <span data-ttu-id="88aa7-439">En Visual Studio Solution Explorer, el proyecto de aplicación de tienda de Windows de Hola de menú contextual, haga clic en **almacén** > **asociar aplicación con hello almacén...** .</span><span class="sxs-lookup"><span data-stu-id="88aa7-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="88aa7-440">En el Asistente de hello, haga clic en **siguiente**, inicie sesión con su cuenta de Microsoft, escriba un nombre para la aplicación en **reservar un nuevo nombre de aplicación**, a continuación, haga clic en **reserva**.</span><span class="sxs-lookup"><span data-stu-id="88aa7-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="88aa7-441">Después de registro de una aplicación Hola es el nombre de la aplicación se creó correctamente, seleccione hello, haga clic en **siguiente**y, a continuación, haga clic en **asociar**.</span><span class="sxs-lookup"><span data-stu-id="88aa7-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="88aa7-442">Inicie sesión en toohello [centro de desarrollo de Windows] con su Account de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="88aa7-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="88aa7-443">En **mis aplicaciones**, haga clic en el registro de una aplicación Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="88aa7-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="88aa7-444">Haga clic en **la administración de aplicaciones** > **identidad de aplicación**y, a continuación, desplácese hacia abajo de toofind su **SID del paquete**.</span><span class="sxs-lookup"><span data-stu-id="88aa7-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="88aa7-445">Muchos usos de SID del paquete Hola tratan como un URI, en cuyo caso deberá toouse *ms-app: / /* como esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="88aa7-446">Tome nota de la versión de Hola de su formado concatenando este valor como prefijo el SID del paquete.</span><span class="sxs-lookup"><span data-stu-id="88aa7-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="88aa7-447">Las aplicaciones de Xamarin requieren algunos tooregister capaz de código adicional toobe aplicaciones que se ejecutan en plataformas de Android o iOS Hola.</span><span class="sxs-lookup"><span data-stu-id="88aa7-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="88aa7-448">Para obtener más información, vea el tema de Hola para su plataforma:</span><span class="sxs-lookup"><span data-stu-id="88aa7-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="88aa7-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="88aa7-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="88aa7-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="88aa7-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="88aa7-451"><a name="register-xplat"></a>Cómo: notificaciones de registro inserción plantillas toosend multiplataforma</span><span class="sxs-lookup"><span data-stu-id="88aa7-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="88aa7-452">plantillas de tooregister, usar hello `RegisterAsync()` método con las plantillas de hello, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="88aa7-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="88aa7-453">Las plantillas deben ser `JObject` tipos y pueden contener varias plantillas en hello siguiendo el formato JSON:</span><span class="sxs-lookup"><span data-stu-id="88aa7-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="88aa7-454">Hola método **RegisterAsync()** también acepta iconos secundarios:</span><span class="sxs-lookup"><span data-stu-id="88aa7-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="88aa7-455">Por seguridad, todas las etiquetas se eliminan durante el registro.</span><span class="sxs-lookup"><span data-stu-id="88aa7-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="88aa7-456">tooadd etiquetas tooinstallations o plantillas en las instalaciones, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="88aa7-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="88aa7-457">notificaciones de toosend utilización de estas plantillas registradas, consulte toohello [API de los centros de notificación].</span><span class="sxs-lookup"><span data-stu-id="88aa7-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="88aa7-458"><a name="misc"></a>Temas variados</span><span class="sxs-lookup"><span data-stu-id="88aa7-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="88aa7-459"><a name="errors"></a>Gestión de errores</span><span class="sxs-lookup"><span data-stu-id="88aa7-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="88aa7-460">Cuando se produce un error en el back-end de Hola, cliente hello SDK provoca un `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="88aa7-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="88aa7-461">El siguiente ejemplo se muestra cómo toohandle una excepción que se devuelve por hello back-end:</span><span class="sxs-lookup"><span data-stu-id="88aa7-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="88aa7-462">Otro ejemplo de trabajar con las condiciones de error puede encontrarse en hello [ejemplo de archivos de aplicaciones móviles].</span><span class="sxs-lookup"><span data-stu-id="88aa7-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="88aa7-463">El [LoggingHandler] en el ejemplo se proporciona un delegado de registro de solicitudes de Hola de toolog de controlador que se realizan toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="88aa7-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="88aa7-464"><a name="headers"></a>Personalización de encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="88aa7-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="88aa7-465">toosupport su escenario de aplicación específica, tendrá que toocustomize la comunicación con el back-end de hello aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="88aa7-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="88aa7-466">Por ejemplo, puede desee tooadd una solicitud de salida de encabezado personalizado tooevery o incluso cambiar los códigos de estado de las respuestas.</span><span class="sxs-lookup"><span data-stu-id="88aa7-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="88aa7-467">Puede utilizar un personalizado [DelegatingHandler], como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="88aa7-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[agregar autenticación tooyour aplicación]: app-service-mobile-windows-store-dotnet-get-started-users.md
[sin conexión la sincronización de datos en aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md
[aplicación de tooyour de notificaciones de inserción de agregar]: app-service-mobile-windows-store-dotnet-get-started-push.md
[registrar su toouse de aplicación un inicio de sesión de cuenta de Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[cómo tooconfigure aplicación de servicio de inicio de sesión de Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[crea una tabla sin tipo de referencia tooan]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[tomar]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[seleccione]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[omitir]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[donde]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[portal de Azure]: https://portal.azure.com/
[portal de Azure clásico]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[centro de desarrollo de Windows]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[API de los centros de notificación]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[ejemplo de archivos de aplicaciones móviles]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 documentación]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
