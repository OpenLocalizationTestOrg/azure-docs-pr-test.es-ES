---
title: Biblioteca de cliente administrada de App Service Mobile Apps (Windows) | Microsoft Azure
description: "Aprenda a usar un cliente .NET para Aplicaciones móviles del Servicio de aplicaciones de Azure con aplicaciones de Windows y Xamarin."
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
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="c8e86-103">Uso del cliente administrado para Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="c8e86-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="c8e86-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c8e86-104">Overview</span></span>
<span data-ttu-id="c8e86-105">En esta guía se muestra cómo realizar escenarios comunes con la biblioteca de cliente administrada para Aplicaciones móviles del Servicio de aplicaciones de Azure para Windows y Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c8e86-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="c8e86-106">Si no tiene experiencia en el uso de Mobile Apps, considere primero la opción de completar el tutorial [Guía de inicio rápido de Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="c8e86-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="c8e86-107">En esta guía, nos centramos en el SDK administrado de cliente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="c8e86-108">Para obtener más información sobre los SDK para Mobile Apps del lado servidor, consulte la documentación de [SDK de servidor .NET][2] o de [SDK de servidor Node.js][3].</span><span class="sxs-lookup"><span data-stu-id="c8e86-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="c8e86-109">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="c8e86-109">Reference documentation</span></span>
<span data-ttu-id="c8e86-110">La documentación de referencia del SDK de cliente se encuentra aquí: [Referencia del cliente de .NET de Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="c8e86-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="c8e86-111">También encontrará varios ejemplos de cliente en el [repositorio de GitHub Azure-Samples][5].</span><span class="sxs-lookup"><span data-stu-id="c8e86-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="c8e86-112">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="c8e86-112">Supported Platforms</span></span>
<span data-ttu-id="c8e86-113">La plataforma de .NET es compatible con las siguientes plataformas:</span><span class="sxs-lookup"><span data-stu-id="c8e86-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="c8e86-114">Versiones de Xamarin Android para niveles de API 19-24 (de KitKat a Nougat)</span><span class="sxs-lookup"><span data-stu-id="c8e86-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="c8e86-115">Versiones de Xamarin iOS para iOS 8.0 y posterior</span><span class="sxs-lookup"><span data-stu-id="c8e86-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="c8e86-116">Plataforma universal de Windows</span><span class="sxs-lookup"><span data-stu-id="c8e86-116">Universal Windows Platform</span></span>
* <span data-ttu-id="c8e86-117">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="c8e86-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="c8e86-118">Windows Phone 8.0, salvo para aplicaciones de Silverlight</span><span class="sxs-lookup"><span data-stu-id="c8e86-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="c8e86-119">La autenticación de flujo de servidor utiliza una vista web para la interfaz de usuario presentada.</span><span class="sxs-lookup"><span data-stu-id="c8e86-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="c8e86-120">Si el dispositivo no puede presentar una interfaz de usuario de vista web, hay que utilizar otros métodos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="c8e86-121">Por tanto, este SDK no es adecuado para dispositivos de tipo reloj o con restricciones similares.</span><span class="sxs-lookup"><span data-stu-id="c8e86-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="c8e86-122"><a name="setup"></a>Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c8e86-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="c8e86-123">Se supone que ya ha creado y publicado el proyecto de back-end de la aplicación móvil, que incluye al menos una tabla.</span><span class="sxs-lookup"><span data-stu-id="c8e86-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="c8e86-124">En el código usado en este tema, el nombre de la tabla es `TodoItem` y dispondrá de las siguientes columnas: `Id`, `Text` y `Complete`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="c8e86-125">Esta tabla es la misma que se crea cuando se completa la [Guía de inicio rápido de Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="c8e86-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="c8e86-126">El tipo del cliente con tipo correspondiente en C# es la siguiente clase:</span><span class="sxs-lookup"><span data-stu-id="c8e86-126">The corresponding typed client-side type in C# is the following class:</span></span>

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

<span data-ttu-id="c8e86-127">Tenga en cuenta que [JsonPropertyAttribute][6] se usa para definir la asignación *PropertyName* entre el campo de cliente y de tabla.</span><span class="sxs-lookup"><span data-stu-id="c8e86-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="c8e86-128">Para aprender a crear tablas en el back-end de Mobile Apps, consulte el [tema del SDK de servidor .NET][7] o el tema del [SDK de servidor Node.js][8].</span><span class="sxs-lookup"><span data-stu-id="c8e86-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="c8e86-129">Si creó el back-end de aplicación móvil en Azure Portal mediante la guía de inicio rápido, también puede usar la opción **Tablas fáciles** en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c8e86-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="c8e86-130">Instalación del paquete del SDK de cliente administrado</span><span class="sxs-lookup"><span data-stu-id="c8e86-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="c8e86-131">Utilice uno de los métodos siguientes para instalar el paquete del SDK de cliente administrado para Mobile Apps desde [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="c8e86-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="c8e86-132">**Visual Studio** Haga clic con el botón derecho en el proyecto, haga clic en **Administrar paquetes NuGet**, busque el paquete `Microsoft.Azure.Mobile.Client` y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="c8e86-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="c8e86-133">**Xamarin Studio** Haga clic con el botón derecho en el proyecto, haga clic en **Add** (Agregar) > **Add NuGet Packages** (Agregar paquetes NuGet), busque el paquete `Microsoft.Azure.Mobile.Client ` y haga clic en **Add Package** (Agregar paquete).</span><span class="sxs-lookup"><span data-stu-id="c8e86-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="c8e86-134">En el archivo de la actividad principal, no olvide agregar la siguiente instrucción **using** :</span><span class="sxs-lookup"><span data-stu-id="c8e86-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="c8e86-135"><a name="symbolsource"></a>Trabajo con símbolos de depuración en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c8e86-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="c8e86-136">Los símbolos del espacio de nombres Microsoft.Azure.Mobile están disponibles en [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="c8e86-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="c8e86-137">Consulte las [instrucciones de SymbolSource][11] para integrar SymbolSource con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c8e86-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="c8e86-138"><a name="create-client"></a>Creación del cliente de Aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="c8e86-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="c8e86-139">El código siguiente crea el objeto [MobileServiceClient][12] que se usa para obtener acceso al back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c8e86-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="c8e86-140">En el código anterior, reemplace `MOBILE_APP_URL` por la dirección URL del back-end de aplicación móvil, que se encuentra en la hoja de la aplicación móvil en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="c8e86-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="c8e86-141">El objeto MobileServiceClient debe ser un singleton.</span><span class="sxs-lookup"><span data-stu-id="c8e86-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="c8e86-142">Trabajo con tablas</span><span class="sxs-lookup"><span data-stu-id="c8e86-142">Work with Tables</span></span>
<span data-ttu-id="c8e86-143">La siguiente sección describe cómo buscar y recuperar registros y modificar los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="c8e86-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="c8e86-144">Se tratan los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="c8e86-144">The following topics are covered:</span></span>

* [<span data-ttu-id="c8e86-145">referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="c8e86-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="c8e86-146">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="c8e86-146">Query data</span></span>](#querying)
* [<span data-ttu-id="c8e86-147">Filtro de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="c8e86-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="c8e86-148">Ordenar datos devueltos</span><span class="sxs-lookup"><span data-stu-id="c8e86-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="c8e86-149">Devolver datos en páginas</span><span class="sxs-lookup"><span data-stu-id="c8e86-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="c8e86-150">Seleccionar columnas específicas</span><span class="sxs-lookup"><span data-stu-id="c8e86-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="c8e86-151">Buscar un registro por identificador</span><span class="sxs-lookup"><span data-stu-id="c8e86-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="c8e86-152">Trabajar con consultas sin tipo</span><span class="sxs-lookup"><span data-stu-id="c8e86-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="c8e86-153">Insertar datos</span><span class="sxs-lookup"><span data-stu-id="c8e86-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="c8e86-154">Actualizar datos</span><span class="sxs-lookup"><span data-stu-id="c8e86-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="c8e86-155">Eliminar datos</span><span class="sxs-lookup"><span data-stu-id="c8e86-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="c8e86-156">Resolución de conflictos y simultaneidad optimista</span><span class="sxs-lookup"><span data-stu-id="c8e86-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="c8e86-157">Enlace a una interfaz de usuario de Windows</span><span class="sxs-lookup"><span data-stu-id="c8e86-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="c8e86-158">Cambio del tamaño de página</span><span class="sxs-lookup"><span data-stu-id="c8e86-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="c8e86-159"><a name="instantiating"></a>Creación de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="c8e86-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="c8e86-160">Todo el código que obtiene acceso a datos o los modifica en una tabla de back-end llama a las funciones del objeto `MobileServiceTable` .</span><span class="sxs-lookup"><span data-stu-id="c8e86-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="c8e86-161">Obtenga una referencia a la tabla llamando al método [GetTable] del modo indicado a continuación:</span><span class="sxs-lookup"><span data-stu-id="c8e86-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="c8e86-162">El objeto devuelto usa el modelo de serialización con tipo.</span><span class="sxs-lookup"><span data-stu-id="c8e86-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="c8e86-163">También se admite un modelo de serialización sin tipo.</span><span class="sxs-lookup"><span data-stu-id="c8e86-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="c8e86-164">El siguiente ejemplo [crea una referencia a una tabla sin tipo]:</span><span class="sxs-lookup"><span data-stu-id="c8e86-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="c8e86-165">En las consultas sin tipo, debe especificar la cadena de consulta de OData subyacente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="c8e86-166"><a name="querying"></a>Consulta de datos desde la aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="c8e86-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="c8e86-167">En esta sección se describe cómo generar consultas al back-end de la aplicación móvil, lo cual incluye la siguiente funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="c8e86-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="c8e86-168">Filtrar datos devueltos</span><span class="sxs-lookup"><span data-stu-id="c8e86-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="c8e86-169">Ordenar datos devueltos</span><span class="sxs-lookup"><span data-stu-id="c8e86-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="c8e86-170">Devolver datos en páginas</span><span class="sxs-lookup"><span data-stu-id="c8e86-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="c8e86-171">Seleccionar columnas específicas</span><span class="sxs-lookup"><span data-stu-id="c8e86-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="c8e86-172">Buscar datos por identificador</span><span class="sxs-lookup"><span data-stu-id="c8e86-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="c8e86-173">Se aplica el tamaño de página del servidor para evitar que se devuelvan todas las filas.</span><span class="sxs-lookup"><span data-stu-id="c8e86-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="c8e86-174">La paginación evita que las solicitudes predeterminadas de los conjuntos de datos de gran tamaño incidan negativamente en el servicio.</span><span class="sxs-lookup"><span data-stu-id="c8e86-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="c8e86-175">Para devolver más de 50 filas, use los métodos `Skip` y `Take`, como se describe en [Devolución de datos en páginas](#paging).</span><span class="sxs-lookup"><span data-stu-id="c8e86-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="c8e86-176"><a name="filtering"></a>Filtro de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="c8e86-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="c8e86-177">El siguiente código muestra cómo filtrar los datos incluyendo una cláusula `Where` en una consulta.</span><span class="sxs-lookup"><span data-stu-id="c8e86-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="c8e86-178">Devuelve todos los elementos de `todoTable` cuya propiedad `Complete` es igual a `false`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="c8e86-179">La función [Where] aplica un predicado de filtrado de filas a la consulta en relación con la tabla.</span><span class="sxs-lookup"><span data-stu-id="c8e86-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="c8e86-180">Puede ver el identificador URI de la solicitud que se ha enviado al back-end mediante el software de inspección de mensajes, como las herramientas para desarrolladores del explorador o [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="c8e86-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="c8e86-181">Si consulta el URI de solicitud, tenga en cuenta que se ha modificado la cadena de consulta:</span><span class="sxs-lookup"><span data-stu-id="c8e86-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="c8e86-182">El SDK de servidor traduce esta solicitud de OData a una consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="c8e86-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="c8e86-183">La función que se pasa al método `Where` puede disponer de un número arbitrario de condiciones.</span><span class="sxs-lookup"><span data-stu-id="c8e86-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="c8e86-184">El SDK de servidor traduciría este ejemplo a una consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="c8e86-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="c8e86-185">Esta consulta también se puede dividir en varias cláusulas:</span><span class="sxs-lookup"><span data-stu-id="c8e86-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="c8e86-186">Los dos métodos son equivalentes y pueden usarse indistintamente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="c8e86-187">La opción anterior&mdash;de concatenación de varios predicados en una consulta&mdash;es más compacta y es la que se recomienda.</span><span class="sxs-lookup"><span data-stu-id="c8e86-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="c8e86-188">La cláusula `Where` admite las operaciones que pueden traducirse en el subconjunto OData.</span><span class="sxs-lookup"><span data-stu-id="c8e86-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="c8e86-189">Estas son algunas de las operaciones:</span><span class="sxs-lookup"><span data-stu-id="c8e86-189">Operations include:</span></span>

* <span data-ttu-id="c8e86-190">Operadores relacionales (==, !=, <, <=, >, >=)</span><span class="sxs-lookup"><span data-stu-id="c8e86-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="c8e86-191">Operadores aritméticos (+, -, /, *, %)</span><span class="sxs-lookup"><span data-stu-id="c8e86-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="c8e86-192">Precisión numérica (Math.Floor, Math.Ceiling)</span><span class="sxs-lookup"><span data-stu-id="c8e86-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="c8e86-193">Funciones de cadena (Length, Substring, Replace, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="c8e86-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="c8e86-194">Propiedades de fecha (Year, Month, Day, Hour, Minute, Second)</span><span class="sxs-lookup"><span data-stu-id="c8e86-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="c8e86-195">Propiedades de acceso de un objeto</span><span class="sxs-lookup"><span data-stu-id="c8e86-195">Access properties of an object, and</span></span>
* <span data-ttu-id="c8e86-196">Expresiones combinando cualquiera de estas operaciones</span><span class="sxs-lookup"><span data-stu-id="c8e86-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="c8e86-197">Al tener en cuenta lo que admite el SDK de servidor, puede consultar la [documentación de OData v3].</span><span class="sxs-lookup"><span data-stu-id="c8e86-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="c8e86-198"><a name="sorting"></a>Clasificación de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="c8e86-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="c8e86-199">El siguiente código muestra cómo ordenar datos incluyendo una función [OrderBy] u [OrderByDescending] en la consulta.</span><span class="sxs-lookup"><span data-stu-id="c8e86-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="c8e86-200">Devuelve los elementos de `todoTable` ordenados de manera ascendente por el campo `Text`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

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

### <span data-ttu-id="c8e86-201"><a name="paging"></a>Devolución de datos en páginas</span><span class="sxs-lookup"><span data-stu-id="c8e86-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="c8e86-202">De manera predeterminada, el back-end devuelve solo las primeras 50 filas.</span><span class="sxs-lookup"><span data-stu-id="c8e86-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="c8e86-203">Aumente el número de filas devueltas llamando al método [Take] .</span><span class="sxs-lookup"><span data-stu-id="c8e86-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="c8e86-204">Use `Take` junto con el método [Skip] para solicitar una "página" específica del conjunto de datos total devuelto por la consulta.</span><span class="sxs-lookup"><span data-stu-id="c8e86-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="c8e86-205">Cuando se ejecuta la siguiente consulta, se devuelven los tres primeros elementos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="c8e86-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="c8e86-206">La siguiente consulta revisada omite los tres primeros resultados y devuelve los tres siguientes.</span><span class="sxs-lookup"><span data-stu-id="c8e86-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="c8e86-207">Esta consulta genera la segunda página de datos en la que el tamaño de página cuenta con tres elementos.</span><span class="sxs-lookup"><span data-stu-id="c8e86-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="c8e86-208">El método [IncludeTotalCount] solicita el recuento total de *todos* los registros que habría que devolver, con lo que se omite cualquier cláusula de limitación/paginación especificada:</span><span class="sxs-lookup"><span data-stu-id="c8e86-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="c8e86-209">En una aplicación real, puede usar consultas similares a las anteriores con un control de paginación o una interfaz de usuario comparable para permitir a los usuarios desplazarse entre las páginas.</span><span class="sxs-lookup"><span data-stu-id="c8e86-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e86-210">Para reemplazar el límite de 50 filas de un back-end de aplicación móvil, también debe aplicar [EnableQueryAttribute] al método público GET y especificar el comportamiento de paginación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="c8e86-211">Cuando se aplica al método, lo siguiente establece el máximo de filas devueltas a 1000:</span><span class="sxs-lookup"><span data-stu-id="c8e86-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="c8e86-212"><a name="selecting"></a>Selección de columnas específicas</span><span class="sxs-lookup"><span data-stu-id="c8e86-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="c8e86-213">Puede especificar qué conjunto de propiedades incluir en los resultados agregando una cláusula [Select] a su consulta.</span><span class="sxs-lookup"><span data-stu-id="c8e86-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="c8e86-214">Por ejemplo, el siguiente código muestra cómo seleccionar solo un campo y también cómo seleccionar varios campos y darle formato:</span><span class="sxs-lookup"><span data-stu-id="c8e86-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
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

<span data-ttu-id="c8e86-215">Todas las funciones descritas hasta ahora son aditivas, por lo que podemos mantener el encadenamiento.</span><span class="sxs-lookup"><span data-stu-id="c8e86-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="c8e86-216">Cada llamada encadenada afecta a más elementos aparte de la consulta.</span><span class="sxs-lookup"><span data-stu-id="c8e86-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="c8e86-217">A continuación se muestra un ejemplo más:</span><span class="sxs-lookup"><span data-stu-id="c8e86-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="c8e86-218"><a name="lookingup"></a>Búsqueda de datos por identificador</span><span class="sxs-lookup"><span data-stu-id="c8e86-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="c8e86-219">La función [LookupAsync] puede usarse para buscar objetos desde la base de datos con un identificador determinado.</span><span class="sxs-lookup"><span data-stu-id="c8e86-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="c8e86-220"><a name="untypedqueries"></a>Ejecución de consultas sin tipo</span><span class="sxs-lookup"><span data-stu-id="c8e86-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="c8e86-221">Al ejecutar una consulta mediante un objeto de tabla sin tipo, debe especificar explícitamente la cadena de consulta de OData llamando a [ReadAsync], como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8e86-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="c8e86-222">Vuelva a obtener valores JSON que puede usar como un contenedor de propiedades.</span><span class="sxs-lookup"><span data-stu-id="c8e86-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="c8e86-223">Para obtener más información sobre JToken y Newtonsoft Json.NET, visite el sitio de [Json.NET] .</span><span class="sxs-lookup"><span data-stu-id="c8e86-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="c8e86-224"><a name="inserting"></a>Inserción de datos en el back-end de una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="c8e86-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="c8e86-225">Todos los tipos de cliente deben incluir un miembro llamado **Id**, que es una cadena de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c8e86-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="c8e86-226">Este elemento **Id** es necesario para realizar operaciones CRUD y para trabajar sin conexión.</span><span class="sxs-lookup"><span data-stu-id="c8e86-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="c8e86-227">El siguiente código muestra cómo usar el método [InsertAsync] para insertar filas nuevas en una tabla.</span><span class="sxs-lookup"><span data-stu-id="c8e86-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="c8e86-228">El parámetro contiene los datos que se van a insertar como un objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="c8e86-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="c8e86-229">Si no se incluye un valor de identificador personalizado exclusivo en `todoItem` durante una inserción, el servidor genera un GUID.</span><span class="sxs-lookup"><span data-stu-id="c8e86-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="c8e86-230">Puede recuperar el identificador generado inspeccionando el objeto después de que se devuelva la llamada.</span><span class="sxs-lookup"><span data-stu-id="c8e86-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="c8e86-231">Para insertar datos sin tipo, puede utilizar Json.NET:</span><span class="sxs-lookup"><span data-stu-id="c8e86-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="c8e86-232">A continuación, se muestra un ejemplo en el que se usa una dirección de correo electrónico como identificador de cadena exclusivo:</span><span class="sxs-lookup"><span data-stu-id="c8e86-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="c8e86-233">Trabajar con valores de Id.</span><span class="sxs-lookup"><span data-stu-id="c8e86-233">Working with ID values</span></span>
<span data-ttu-id="c8e86-234">El servicio Aplicaciones móviles admite valores de cadena personalizados únicos para la columna **id** de la tabla.</span><span class="sxs-lookup"><span data-stu-id="c8e86-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="c8e86-235">Esto permite a las aplicaciones usar valores personalizados como direcciones de correo electrónico o nombres de usuario para el id.</span><span class="sxs-lookup"><span data-stu-id="c8e86-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="c8e86-236">Los identificadores de cadena proporcionan las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c8e86-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="c8e86-237">Se generan identificadores sin realizar una vuelta a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c8e86-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="c8e86-238">Los registros son más fáciles de fusionar desde diferentes tablas o bases de datos.</span><span class="sxs-lookup"><span data-stu-id="c8e86-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="c8e86-239">Los valores de los identificadores pueden integrarse mejor con una lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="c8e86-240">Cuando no se establece un valor de identificador de cadena en un registro insertado, el back-end de la aplicación móvil genera un valor único para el identificador.</span><span class="sxs-lookup"><span data-stu-id="c8e86-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="c8e86-241">Puede usar el método [Guid.NewGuid] para generar sus propios valores de identificador, ya sea en el cliente o en el back-end.</span><span class="sxs-lookup"><span data-stu-id="c8e86-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="c8e86-242"><a name="modifying"></a>Modificación de datos en el back-end de una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="c8e86-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="c8e86-243">El siguiente código muestra cómo usar el método [UpdateAsync] para actualizar un registro existente con el mismo identificador con nueva información.</span><span class="sxs-lookup"><span data-stu-id="c8e86-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="c8e86-244">El parámetro contiene los datos que se van a actualizar como un objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="c8e86-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="c8e86-245">Para actualizar datos sin tipo, puede usar [Json.NET] de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c8e86-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="c8e86-246">Debe especificarse un campo `id` al realizar una actualización.</span><span class="sxs-lookup"><span data-stu-id="c8e86-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="c8e86-247">El back-end utiliza el campo `id` para identificar qué fila actualizar.</span><span class="sxs-lookup"><span data-stu-id="c8e86-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="c8e86-248">El campo `id` puede obtenerse a partir del resultado de la llamada a `InsertAsync`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="c8e86-249">Se genera una excepción `ArgumentException` cuando trata de actualizar un elemento sin proporcionar el valor `id`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="c8e86-250"><a name="deleting"></a>Eliminación de datos del back-end de una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="c8e86-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="c8e86-251">El siguiente código muestra cómo usar el método [DeleteAsync] para eliminar una instancia existente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="c8e86-252">La instancia se identifica mediante el campo `id` establecido en `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="c8e86-253">Para eliminar datos sin tipo, puede aprovechar Json.NET de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c8e86-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="c8e86-254">Al realizar una solicitud de eliminación, debe especificarse un identificador.</span><span class="sxs-lookup"><span data-stu-id="c8e86-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="c8e86-255">Otras propiedades no se pasan al servicio o se omiten en este.</span><span class="sxs-lookup"><span data-stu-id="c8e86-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="c8e86-256">El resultado de una llamada `DeleteAsync` normalmente es `null`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="c8e86-257">El identificador puede obtenerse a partir del resultado de la llamada `InsertAsync` .</span><span class="sxs-lookup"><span data-stu-id="c8e86-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="c8e86-258">Se produce una excepción `MobileServiceInvalidOperationException` cuando se trata de eliminar un elemento sin especificar el campo `id`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="c8e86-259"><a name="optimisticconcurrency"></a>Uso de la simultaneidad optimista para resolver conflictos</span><span class="sxs-lookup"><span data-stu-id="c8e86-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="c8e86-260">Dos o más clientes pueden escribir cambios en el mismo elemento y al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="c8e86-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="c8e86-261">Si no se produjera la detección de conflictos, la última escritura sobrescribiría cualquier actualización anterior.</span><span class="sxs-lookup"><span data-stu-id="c8e86-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="c8e86-262">**control de simultaneidad optimista** asume que cada transacción puede confirmarse y, por lo tanto, no usa ningún bloqueo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c8e86-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="c8e86-263">Antes de confirmar una transacción, el control de simultaneidad optimista comprueba que ninguna otra transacción haya modificado los datos.</span><span class="sxs-lookup"><span data-stu-id="c8e86-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="c8e86-264">Si los datos se han modificado, la transacción de confirmación se desecha.</span><span class="sxs-lookup"><span data-stu-id="c8e86-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="c8e86-265">El servicio Aplicaciones móviles es compatible con el control de simultaneidad optimista gracias al seguimiento de cambios en cada elemento mediante la columna de propiedades del sistema `version` que se definió en cada tabla en el back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c8e86-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="c8e86-266">Cada vez que se actualiza un registro, el servicio Aplicaciones móviles establece la propiedad `version` de ese registro en un nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="c8e86-267">Durante cada solicitud de actualización, la propiedad `version` del registro incluido con la solicitud se compara con la misma propiedad del registro en el servidor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="c8e86-268">Si la versión que pasa con la solicitud no coincide con el back-end, la biblioteca de cliente genera una excepción `MobileServicePreconditionFailedException<T>` .</span><span class="sxs-lookup"><span data-stu-id="c8e86-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="c8e86-269">El tipo incluido con la excepción es el registro del back-end que contiene la versión del registro del servidor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="c8e86-270">A continuación, la aplicación puede usar esta información para decidir si ejecutar la solicitud de actualización de nuevo con el valor `version` correcto del back-end para confirmar los cambios.</span><span class="sxs-lookup"><span data-stu-id="c8e86-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="c8e86-271">Defina una columna en la clase de tabla para la propiedad del sistema `version` con el fin de habilitar la simultaneidad optimista.</span><span class="sxs-lookup"><span data-stu-id="c8e86-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="c8e86-272">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8e86-272">For example:</span></span>

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

<span data-ttu-id="c8e86-273">Las aplicaciones con tablas sin tipo permiten la simultaneidad optimista mediante el establecimiento de la marca `Version` en `SystemProperties` de la tabla de la siguiente forma.</span><span class="sxs-lookup"><span data-stu-id="c8e86-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="c8e86-274">Además de habilitar la simultaneidad optimista, se debe detectar la excepción `MobileServicePreconditionFailedException<T>` en el código al llamar a [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="c8e86-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="c8e86-275">Resuelva el conflicto aplicando el valor `version` correcto al registro actualizado y llame a [UpdateAsync] con el registro resuelto.</span><span class="sxs-lookup"><span data-stu-id="c8e86-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="c8e86-276">El siguiente código muestra cómo resolver un conflicto de escritura detectado:</span><span class="sxs-lookup"><span data-stu-id="c8e86-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
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
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="c8e86-277">Para obtener más información, consulte el tema [Sincronización de datos sin conexión en Aplicaciones móviles de Azure] .</span><span class="sxs-lookup"><span data-stu-id="c8e86-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="c8e86-278"><a name="binding"></a>Enlace de datos de Aplicaciones móviles a una interfaz de usuario de Windows</span><span class="sxs-lookup"><span data-stu-id="c8e86-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="c8e86-279">En esta sección se describe cómo mostrar objetos de datos devueltos mediante elementos de la interfaz de usuario en una aplicación Windows.</span><span class="sxs-lookup"><span data-stu-id="c8e86-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="c8e86-280">El ejemplo de código siguiente se enlaza al origen de la lista con una consulta de elementos incompletos.</span><span class="sxs-lookup"><span data-stu-id="c8e86-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="c8e86-281">[MobileServiceCollection] crea una colección de enlaces compatible con Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c8e86-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="c8e86-282">Algunos controles en tiempo de ejecución administrado admiten una interfaz denominada [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="c8e86-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="c8e86-283">Esta interfaz permite a los controles solicitar datos adicionales cuando el usuario se desplaza.</span><span class="sxs-lookup"><span data-stu-id="c8e86-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="c8e86-284">Las aplicaciones universales de Windows integran compatibilidad con esta interfaz mediante [MobileServiceIncrementalLoadingCollection], que administra automáticamente las llamadas desde los controles.</span><span class="sxs-lookup"><span data-stu-id="c8e86-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="c8e86-285">Use `MobileServiceIncrementalLoadingCollection` en aplicaciones Windows de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c8e86-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="c8e86-286">Para usar la nueva colección en aplicaciones de Windows Phone 8 y "Silverlight", use los métodos de extensión `ToCollection` en `IMobileServiceTableQuery<T>` y `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="c8e86-287">Para cargar datos, llame a `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="c8e86-288">Cuando use la colección creada mediante la llamada a `ToCollectionAsync` o `ToCollection`, obtendrá una colección que puede enlazarse a los controles de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="c8e86-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="c8e86-289">Esta colección es para la paginación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-289">This collection is paging-aware.</span></span>  <span data-ttu-id="c8e86-290">Como la colección está cargando datos desde la red, a veces, pueden producirse errores en este proceso.</span><span class="sxs-lookup"><span data-stu-id="c8e86-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="c8e86-291">Para gestionar esos errores, puede reemplazar el método `OnException` de `MobileServiceIncrementalLoadingCollection` con el fin de controlar las excepciones resultantes de las llamadas a `LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="c8e86-292">Imagine que la tabla contiene muchos campos, pero solo quiere que se muestren algunos en el control.</span><span class="sxs-lookup"><span data-stu-id="c8e86-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="c8e86-293">Puede usar la guía de la sección anterior[Selección de columnas específicas](#selecting)con el fin de elegir las columnas específicas que se mostrarán en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="c8e86-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="c8e86-294"><a name="pagesize"></a>Cambio del tamaño de página</span><span class="sxs-lookup"><span data-stu-id="c8e86-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="c8e86-295">Mobile Apps de Azure devuelve un máximo de 50 elementos por cada solicitud de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c8e86-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="c8e86-296">Puede cambiar el tamaño de paginación si aumenta el de página máximo en el cliente y el servidor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="c8e86-297">Para aumentar el tamaño de página solicitado, especifique `PullOptions` al usar `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="c8e86-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="c8e86-298">Suponiendo que ha establecido el valor de `PageSize` igual o mayor que 100 en el servidor, se devolverán hasta 100 elementos en cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="c8e86-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="c8e86-299"><a name="#offlinesync"></a>Trabajo con tablas sin conexión</span><span class="sxs-lookup"><span data-stu-id="c8e86-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="c8e86-300">Las tablas sin conexión utilizan un almacén SQLite local para almacenar datos para usarlos cuando estén sin conexión.</span><span class="sxs-lookup"><span data-stu-id="c8e86-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="c8e86-301">Todas las operaciones de las tablas se realizan en el almacén SQLite local, en lugar del almacén del servidor remoto.</span><span class="sxs-lookup"><span data-stu-id="c8e86-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="c8e86-302">Para crear una tabla sin conexión, prepare primero el proyecto:</span><span class="sxs-lookup"><span data-stu-id="c8e86-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="c8e86-303">En Visual Studio, haga clic con el botón derecho en la solución > **Administrar paquetes NuGet para la solución...** y, después, busque e instale el paquete NuGet **Microsoft.Azure.Mobile.Client.SQLiteStore** en todos los proyectos de la solución.</span><span class="sxs-lookup"><span data-stu-id="c8e86-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="c8e86-304">(Opcional) Para admitir dispositivos de Windows, instale uno de los siguientes paquetes en el sistema de tiempo de ejecución de SQLite:</span><span class="sxs-lookup"><span data-stu-id="c8e86-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="c8e86-305">**Runtime de Windows 8.1:** instale [SQLite para Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="c8e86-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="c8e86-306">**Windows Phone 8.1:** instale [SQLite para Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="c8e86-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="c8e86-307">**Plataforma universal de Windows** Instale [SQLite para la plataforma universal de Windows][5].</span><span class="sxs-lookup"><span data-stu-id="c8e86-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="c8e86-308">(Opcional).</span><span class="sxs-lookup"><span data-stu-id="c8e86-308">(Optional).</span></span> <span data-ttu-id="c8e86-309">En el caso de los dispositivos Windows, haga clic en **Referencias** > **Agregar referencia...**, expanda la carpeta **Windows** > **Extensiones** y habilite el SDK de **SQLite para Windows** apropiado, junto con el SDK de **Runtime de Visual C++ 2013 para Windows**.</span><span class="sxs-lookup"><span data-stu-id="c8e86-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="c8e86-310">Los nombres de SDK de SQLite varían ligeramente con cada plataforma de Windows.</span><span class="sxs-lookup"><span data-stu-id="c8e86-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="c8e86-311">Para poder crear una referencia de tabla, debe prepararse el almacén local:</span><span class="sxs-lookup"><span data-stu-id="c8e86-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="c8e86-312">Normalmente, la inicialización del almacén se realiza inmediatamente después de que se crea el cliente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="c8e86-313">**OfflineDbPath** debe ser un nombre de archivo adecuado para usarlo en todas las plataformas compatibles.</span><span class="sxs-lookup"><span data-stu-id="c8e86-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="c8e86-314">Si la ruta de acceso es completa (es decir, comienza con una barra diagonal), se utiliza dicha ruta.</span><span class="sxs-lookup"><span data-stu-id="c8e86-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="c8e86-315">Si la ruta de acceso no es completa, el archivo se coloca en una ubicación específica de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="c8e86-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="c8e86-316">En los dispositivos iOS y Android, la ruta de acceso predeterminada es la carpeta "Personal Files".</span><span class="sxs-lookup"><span data-stu-id="c8e86-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="c8e86-317">En los dispositivos de Windows, la ruta de acceso predeterminada es la carpeta "AppData" específica de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="c8e86-318">Un referencia de tabla se puede obtener mediante el método `GetSyncTable<>`:</span><span class="sxs-lookup"><span data-stu-id="c8e86-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="c8e86-319">No es necesario autenticarse para usar una tabla sin conexión.</span><span class="sxs-lookup"><span data-stu-id="c8e86-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="c8e86-320">Solo es preciso hacerlo cuando se establece comunicación con el servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="c8e86-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="c8e86-321"><a name="syncoffline"></a>Sincronización de una tabla sin conexión</span><span class="sxs-lookup"><span data-stu-id="c8e86-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="c8e86-322">Las tablas sin conexión no se sincronizan con el back-end de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c8e86-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="c8e86-323">La sincronización se divide en dos partes.</span><span class="sxs-lookup"><span data-stu-id="c8e86-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="c8e86-324">Mediante la descarga de elementos nuevos puede insertar los cambios por separado.</span><span class="sxs-lookup"><span data-stu-id="c8e86-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="c8e86-325">Éste es un método de sincronización típico:</span><span class="sxs-lookup"><span data-stu-id="c8e86-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
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

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting to server's copy.
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

<span data-ttu-id="c8e86-326">Si el primer argumento para `PullAsync` es nulo, no se usa la sincronización incremental.</span><span class="sxs-lookup"><span data-stu-id="c8e86-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="c8e86-327">Todas las operaciones de sincronización recuperan todos los registros.</span><span class="sxs-lookup"><span data-stu-id="c8e86-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="c8e86-328">El SDK realiza una tarea `PushAsync()` implícita antes de extraer registros.</span><span class="sxs-lookup"><span data-stu-id="c8e86-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="c8e86-329">El control de los conflictos se realiza en un método `PullAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="c8e86-330">Los conflictos se pueden tratar de la misma manera que las tablas en línea.</span><span class="sxs-lookup"><span data-stu-id="c8e86-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="c8e86-331">El conflicto se produce cuando se llama a `PullAsync()`, en lugar de durante la inserción, actualización o eliminación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="c8e86-332">Si se producen varios conflictos, se agrupan en una sola clase MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="c8e86-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="c8e86-333">Trate cada error por separado.</span><span class="sxs-lookup"><span data-stu-id="c8e86-333">Handle each failure separately.</span></span>

## <span data-ttu-id="c8e86-334"><a name="#customapi"></a>Trabajo con una API personalizada</span><span class="sxs-lookup"><span data-stu-id="c8e86-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="c8e86-335">Una API personalizada le permite definir extremos personalizados que exponen la funcionalidad del servidor que no se asigna a una operación de inserción, actualización, eliminación o lectura.</span><span class="sxs-lookup"><span data-stu-id="c8e86-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="c8e86-336">Al usar una API personalizada, puede tener más control sobre la mensajería, incluida la lectura y el establecimiento de encabezados de mensajes HTTP y la definición del formato del cuerpo de un mensaje diferente de JSON.</span><span class="sxs-lookup"><span data-stu-id="c8e86-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="c8e86-337">Puede llamar a una API personalizada al realizar una llamada a una de las sobrecargas del método [InvokeApiAsync] en el cliente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="c8e86-338">Por ejemplo, la siguiente línea de código envía una solicitud POST a la API **completeAll** en el back-end:</span><span class="sxs-lookup"><span data-stu-id="c8e86-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="c8e86-339">Se trata de una llamada de método con tipo que requiere que se defina el tipo de devolución de **MarkAllResult** .</span><span class="sxs-lookup"><span data-stu-id="c8e86-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="c8e86-340">Se admiten métodos con y sin tipos.</span><span class="sxs-lookup"><span data-stu-id="c8e86-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="c8e86-341">El método InvokeApiAsync() antepone "/api/" a la API a la que desea llamar, a menos que la API comience por "/".</span><span class="sxs-lookup"><span data-stu-id="c8e86-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="c8e86-342">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8e86-342">For example:</span></span>

* <span data-ttu-id="c8e86-343">`InvokeApiAsync("completeAll",...)`llama a /api/completeAll en el back-end</span><span class="sxs-lookup"><span data-stu-id="c8e86-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="c8e86-344">`InvokeApiAsync("/.auth/me",...)`llama a /.auth/me en el back-end</span><span class="sxs-lookup"><span data-stu-id="c8e86-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="c8e86-345">Puede usar InvokeApiAsync para llamar a cualquier WebAPI, incluidas las que no están definidas en Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c8e86-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="c8e86-346">Cuando usa InvokeApiAsync(), se envían los encabezados correspondientes, incluidos los encabezados de autenticación, con la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c8e86-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="c8e86-347"><a name="authentication"></a>Autenticación de usuarios</span><span class="sxs-lookup"><span data-stu-id="c8e86-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="c8e86-348">Mobile Apps es compatible con la autenticación y la autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externas: Facebook, Google, cuenta de Microsoft, Twitter y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c8e86-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="c8e86-349">Puede establecer permisos en tablas para restringir el acceso a operaciones específicas solo a usuarios autenticados.</span><span class="sxs-lookup"><span data-stu-id="c8e86-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="c8e86-350">También puede usar la identidad de usuarios autenticados para implementar reglas de autorización en scripts del servidor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="c8e86-351">Para obtener más información, consulte el tutorial [Incorporación de la autenticación a su aplicación].</span><span class="sxs-lookup"><span data-stu-id="c8e86-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="c8e86-352">Se admiten dos flujos de autenticación: *administrado por cliente* y *administrado por servidor*.</span><span class="sxs-lookup"><span data-stu-id="c8e86-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="c8e86-353">Este último ofrece la experiencia de autenticación más simple, ya que se basa en la interfaz de autenticación web del proveedor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="c8e86-354">El flujo administrado por cliente permite una mayor integración con funcionalidades específicas del dispositivo, ya que se basa en SDK específicos del dispositivo y específicos del proveedor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e86-355">En las aplicaciones de producción se recomienda usar un flujo administrado por el cliente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="c8e86-356">Para configurar la autenticación, debe registrar la aplicación en uno o varios proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="c8e86-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="c8e86-357">El proveedor de identidades generará un identificador y un secreto de cliente para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="c8e86-358">Estos valores se establecen en el back-end para habilitar la autenticación y autorización de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c8e86-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="c8e86-359">Para obtener más información, siga las instrucciones detalladas del tutorial [Incorporación de la autenticación a su aplicación].</span><span class="sxs-lookup"><span data-stu-id="c8e86-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="c8e86-360">En esta sección se tratan los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="c8e86-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="c8e86-361">Autenticación administrada por el cliente</span><span class="sxs-lookup"><span data-stu-id="c8e86-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="c8e86-362">Autenticación administrada por el servidor</span><span class="sxs-lookup"><span data-stu-id="c8e86-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="c8e86-363">Almacenamiento en caché del token de autenticación</span><span class="sxs-lookup"><span data-stu-id="c8e86-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="c8e86-364"><a name="clientflow"></a>Autenticación administrada por el cliente</span><span class="sxs-lookup"><span data-stu-id="c8e86-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="c8e86-365">La aplicación puede ponerse en contacto de manera independiente con el proveedor de identidades y proporcionar el token devuelto en el inicio de sesión junto con el back-end.</span><span class="sxs-lookup"><span data-stu-id="c8e86-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="c8e86-366">Este flujo de cliente permite proporcionar una experiencia de inicio de sesión único a los usuarios o recuperar datos de usuario adicionales del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="c8e86-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="c8e86-367">Se prefiere la autenticación de flujo de cliente al uso de una de flujo de servidor, ya que el SDK de proveedor de identidades proporciona una experiencia UX más nativa y permite realizar más personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="c8e86-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="c8e86-368">Se proporcionan ejemplos de los siguientes patrones de autenticación de flujo de cliente:</span><span class="sxs-lookup"><span data-stu-id="c8e86-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="c8e86-369">Biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8e86-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="c8e86-370">Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="c8e86-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="c8e86-371">SDK de Live</span><span class="sxs-lookup"><span data-stu-id="c8e86-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="c8e86-372"><a name="adal"></a>Autenticación de usuarios con la biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8e86-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="c8e86-373">La biblioteca de autenticación de Active Directory (ADAL) se puede usar para iniciar la autenticación de usuarios desde el cliente con la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c8e86-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="c8e86-374">Configure su back-end de aplicación móvil para el inicio de sesión en AAD siguiendo el tutorial [Configuración de App Service para usar el inicio de sesión de Azure Active Directory] .</span><span class="sxs-lookup"><span data-stu-id="c8e86-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="c8e86-375">Asegúrese de completar el paso opcional de registrar una aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="c8e86-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="c8e86-376">En Visual Studio o Xamarin Studio, abra el proyecto y agregue una referencia al paquete NuGet `Microsoft.IdentityModel.CLients.ActiveDirectory` .</span><span class="sxs-lookup"><span data-stu-id="c8e86-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="c8e86-377">Al buscar, incluya las versiones preliminares.</span><span class="sxs-lookup"><span data-stu-id="c8e86-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="c8e86-378">Agregue el siguiente código a la aplicación, según la plataforma que utilice.</span><span class="sxs-lookup"><span data-stu-id="c8e86-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="c8e86-379">En cada caso, realice las sustituciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="c8e86-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="c8e86-380">Reemplace **INSERT-AUTHORITY-HERE** por el nombre del inquilino en el que aprovisionó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c8e86-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="c8e86-381">El formato debería ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c8e86-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="c8e86-382">Este valor se puede copiar de la pestaña Dominio de Azure Active Directory en el [Portal de Azure clásico].</span><span class="sxs-lookup"><span data-stu-id="c8e86-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="c8e86-383">Reemplace **INSERT-RESOURCE-ID-HERE** por el Id. de cliente del back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c8e86-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="c8e86-384">El Id. de cliente en la pestaña **Opciones avanzadas** de **Configuración de Azure Active Directory** en el portal.</span><span class="sxs-lookup"><span data-stu-id="c8e86-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="c8e86-385">Reemplace **INSERT-CLIENT-ID-HERE** por el Id. de cliente que copió de la aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="c8e86-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="c8e86-386">Reemplace **INSERT-REDIRECT-URI-HERE** por el punto de conexión */.auth/login/done* del sitio, mediante el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c8e86-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="c8e86-387">Este valor debe ser similar a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="c8e86-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="c8e86-388">El código necesario para cada plataforma es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8e86-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="c8e86-389">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="c8e86-389">**Windows:**</span></span>

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

     <span data-ttu-id="c8e86-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="c8e86-390">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="c8e86-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="c8e86-391">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="c8e86-392"><a name="client-facebook"></a>Inicio de sesión único mediante un token de Facebook o Google</span><span class="sxs-lookup"><span data-stu-id="c8e86-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="c8e86-393">Puede usar el flujo de cliente como se muestra en este fragmento para Facebook o Google.</span><span class="sxs-lookup"><span data-stu-id="c8e86-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
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
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="c8e86-394"><a name="client-livesdk"></a>Inicio de sesión único mediante una cuenta Microsoft con el SDK de Live</span><span class="sxs-lookup"><span data-stu-id="c8e86-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="c8e86-395">Para autenticar usuarios, debe registrar la aplicación en el Centro para desarrolladores de la cuenta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8e86-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="c8e86-396">Configure los detalles del registro en su back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c8e86-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="c8e86-397">Complete los pasos del artículo sobre cómo [registrar la aplicación para usar el inicio de sesión de la cuenta Microsoft]para crear un registro de la cuenta Microsoft y conectarlo al back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c8e86-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="c8e86-398">Si dispone de ambas versiones de la aplicación, Tienda Windows y Windows Phone 8/Silverlight, registre primero la versión de Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="c8e86-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="c8e86-399">El siguiente código se autentica mediante el SDK de Live y usa el token devuelto para iniciar sesión en el back-end de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c8e86-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
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

<span data-ttu-id="c8e86-400">Para obtener más información, consulte la documentación del [SDK de Windows Live] .</span><span class="sxs-lookup"><span data-stu-id="c8e86-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="c8e86-401"><a name="serverflow"></a>Autenticación administrada por el servidor</span><span class="sxs-lookup"><span data-stu-id="c8e86-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="c8e86-402">Una vez que haya registrado el proveedor de identidades, llame al método [LoginAsync] de [MobileServiceClient] con el valor [MobileServiceAuthenticationProvider] del proveedor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="c8e86-403">Por ejemplo, el siguiente código activa un inicio de sesión de flujo de servidor mediante Facebook.</span><span class="sxs-lookup"><span data-stu-id="c8e86-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="c8e86-404">Si usa un proveedor de identidades que no sea Facebook, cambie el valor de [MobileServiceAuthenticationProvider] al valor de su proveedor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="c8e86-405">En un flujo de servidor, Azure App Service administra el flujo de autenticación OAuth mostrando la página de inicio de sesión del proveedor seleccionado.</span><span class="sxs-lookup"><span data-stu-id="c8e86-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="c8e86-406">Cuando se devuelve el proveedor de identidades, Azure App Service genera un token de autenticación de este servicio.</span><span class="sxs-lookup"><span data-stu-id="c8e86-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="c8e86-407">El método [LoginAsync] devuelve [MobileServiceUser], que proporciona el elemento [UserId] del usuario autenticado y [MobileServiceAuthenticationToken] como JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="c8e86-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="c8e86-408">El token puede almacenarse en caché y volver a usarse hasta que expire.</span><span class="sxs-lookup"><span data-stu-id="c8e86-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="c8e86-409">Para obtener más información, consulte [Almacenamiento en caché del token de autenticación](#caching).</span><span class="sxs-lookup"><span data-stu-id="c8e86-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="c8e86-410"><a name="caching"></a>Almacenamiento en caché del token de autenticación</span><span class="sxs-lookup"><span data-stu-id="c8e86-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="c8e86-411">En algunos casos, la llamada al método de inicio de sesión se puede evitar tras la primera autenticación correcta. Para ello, es preciso almacenar el token de autenticación del proveedor.</span><span class="sxs-lookup"><span data-stu-id="c8e86-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="c8e86-412">Las aplicaciones de Tienda Windows y UWP pueden usar [PasswordVault] para almacenar en caché el token de autenticación actual después de un inicio de sesión correcto, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c8e86-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="c8e86-413">El valor de UserId se almacena como el nombre de usuario de la credencial y el token se almacena como la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c8e86-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="c8e86-414">En los inicios posteriores, puede comprobar si **PasswordVault** tiene credenciales almacenadas en caché.</span><span class="sxs-lookup"><span data-stu-id="c8e86-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="c8e86-415">En el ejemplo siguiente se utilizan credenciales almacenadas en la caché cuando se encuentran y también se intenta volver a realizar la autenticación con el back-end:</span><span class="sxs-lookup"><span data-stu-id="c8e86-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="c8e86-416">Cuando se cierre la sesión de un usuario, también es preciso quitar la credencial almacenada, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="c8e86-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="c8e86-417">Las aplicaciones de Xamarin utilizan las API de [Xamarin.Auth] para almacenar de forma segura las credenciales en un objeto **Account**.</span><span class="sxs-lookup"><span data-stu-id="c8e86-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="c8e86-418">Para ver un ejemplo de cómo usar estas API, consulte el archivo de código [AuthStore.cs] en el [ejemplo de uso compartido de fotografías ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="c8e86-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="c8e86-419">Si utiliza la autenticación administrada por el cliente, también puede almacenar en caché el token de acceso obtenido del proveedor, como Facebook o Twitter.</span><span class="sxs-lookup"><span data-stu-id="c8e86-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="c8e86-420">Este token se puede especificar al solicitar un nuevo token de autenticación del back-end, tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="c8e86-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="c8e86-421"><a name="pushnotifications"></a>Notificaciones push</span><span class="sxs-lookup"><span data-stu-id="c8e86-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="c8e86-422">Los siguientes temas tratan sobre las notificaciones push:</span><span class="sxs-lookup"><span data-stu-id="c8e86-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="c8e86-423">Registro de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="c8e86-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="c8e86-424">Obtención del SID de un paquete de la Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="c8e86-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="c8e86-425">Registro con plantillas multiplataforma</span><span class="sxs-lookup"><span data-stu-id="c8e86-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="c8e86-426"><a name="register-for-push"></a>Cómo registrarse para recibir notificaciones push</span><span class="sxs-lookup"><span data-stu-id="c8e86-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="c8e86-427">El cliente de Aplicaciones móviles permite registrar las notificaciones push con Centros de notificaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8e86-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="c8e86-428">Al registrar, se obtiene un identificador del servicio de notificaciones push (PNS) específico de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="c8e86-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="c8e86-429">A continuación, proporcione este valor junto con las etiquetas cuando se cree el registro.</span><span class="sxs-lookup"><span data-stu-id="c8e86-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="c8e86-430">El código siguiente registra la aplicación de Windows para las notificaciones push en el Servicio de notificaciones de Windows.(WNS):</span><span class="sxs-lookup"><span data-stu-id="c8e86-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="c8e86-431">Si va a insertar en WNS, DEBE [obtener un SID del paquete de Tienda Windows](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="c8e86-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="c8e86-432">Para más información sobre las aplicaciones de Windows, incluyendo cómo registrarse para los registros de plantillas, vea [Agregar notificaciones de inserción a la aplicación].</span><span class="sxs-lookup"><span data-stu-id="c8e86-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="c8e86-433">Tenga en cuenta que no se admite la solicitud de etiquetas del cliente.</span><span class="sxs-lookup"><span data-stu-id="c8e86-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="c8e86-434">Las solicitudes de etiquetas se quitan del registro en modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="c8e86-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="c8e86-435">Si desea registrar el dispositivo con etiquetas, crear una API personalizada que use la API de los Centros de notificaciones para realizar el registro en su nombre.</span><span class="sxs-lookup"><span data-stu-id="c8e86-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="c8e86-436">[Llame a la API personalizada](#customapi), en lugar de al método `RegisterNativeAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="c8e86-437"><a name="package-sid"></a>Obtención del SID de un paquete de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="c8e86-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="c8e86-438">Se necesita un SID de paquete para habilitar las notificaciones push en aplicaciones de la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="c8e86-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="c8e86-439">Para recibir un SID del paquete. registre la aplicación en la Tienda Windows.</span><span class="sxs-lookup"><span data-stu-id="c8e86-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="c8e86-440">Para obtener este valor:</span><span class="sxs-lookup"><span data-stu-id="c8e86-440">To obtain this value:</span></span>

1. <span data-ttu-id="c8e86-441">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el proyecto de la aplicación de la Tienda Windows y haga clic en **Tienda** > **Asociar aplicación con la Tienda...**.</span><span class="sxs-lookup"><span data-stu-id="c8e86-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="c8e86-442">En el asistente, haga clic en **Siguiente**, inicie sesión con su cuenta Microsoft, escriba un nombre para la aplicación en **Reserve un nuevo nombre de aplicación** y haga clic en **Reservar**.</span><span class="sxs-lookup"><span data-stu-id="c8e86-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="c8e86-443">Después de que el registro de la aplicación se cree correctamente, seleccione el nombre de la aplicación, haga clic en **Siguiente** y, después, en **Asociar**.</span><span class="sxs-lookup"><span data-stu-id="c8e86-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="c8e86-444">Inicie sesión en el [Centro de desarrollo de Windows] con su cuenta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8e86-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="c8e86-445">En **Mis aplicaciones**, haga clic en el registro de la aplicación que ha creado.</span><span class="sxs-lookup"><span data-stu-id="c8e86-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="c8e86-446">Haga clic en **Administración de la aplicación** > **Identidad de la aplicación** y, después, desplácese hacia abajo para buscar el **SID del paquete**.</span><span class="sxs-lookup"><span data-stu-id="c8e86-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="c8e86-447">Muchos usos del SID del paquete lo tratan como un URI, en cuyo caso debe usar *ms-app://* como esquema.</span><span class="sxs-lookup"><span data-stu-id="c8e86-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="c8e86-448">Tome nota de la versión del SID del paquete que se forma concatenando este valor como prefijo.</span><span class="sxs-lookup"><span data-stu-id="c8e86-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="c8e86-449">Las aplicaciones de Xamarin requieren más código para poder registrar una aplicación que se ejecute en las plataformas Android o iOS.</span><span class="sxs-lookup"><span data-stu-id="c8e86-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="c8e86-450">Para obtener más información, consulte el tema sobre su plataforma:</span><span class="sxs-lookup"><span data-stu-id="c8e86-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="c8e86-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="c8e86-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="c8e86-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="c8e86-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="c8e86-453"><a name="register-xplat"></a>Procedimiento: Registro de plantillas push para enviar notificaciones entre plataformas</span><span class="sxs-lookup"><span data-stu-id="c8e86-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="c8e86-454">Para registrar plantillas, use el método `RegisterAsync()` con ellas, tal y como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c8e86-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="c8e86-455">Las plantillas serán de tipo `JObject` y pueden contener varias plantillas con el formato JSON siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8e86-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

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

<span data-ttu-id="c8e86-456">El método **RegisterAsync()** también acepta iconos secundarios:</span><span class="sxs-lookup"><span data-stu-id="c8e86-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="c8e86-457">Por seguridad, todas las etiquetas se eliminan durante el registro.</span><span class="sxs-lookup"><span data-stu-id="c8e86-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="c8e86-458">Para agregar etiquetas a las instalaciones o plantillas dentro de las instalaciones, consulte [Trabajar con el SDK del servidor back-end de .NET para Aplicaciones móviles de Azure].</span><span class="sxs-lookup"><span data-stu-id="c8e86-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="c8e86-459">Para enviar notificaciones mediante estas plantillas registradas, consulte [Referencias API].</span><span class="sxs-lookup"><span data-stu-id="c8e86-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="c8e86-460"><a name="misc"></a>Temas variados</span><span class="sxs-lookup"><span data-stu-id="c8e86-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="c8e86-461"><a name="errors"></a>Gestión de errores</span><span class="sxs-lookup"><span data-stu-id="c8e86-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="c8e86-462">Si se produce un error en el back-end, el SDK de cliente generará una excepción `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="c8e86-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="c8e86-463">En el ejemplo siguiente se muestra cómo controlar una excepción devuelta por el back-end:</span><span class="sxs-lookup"><span data-stu-id="c8e86-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
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

<span data-ttu-id="c8e86-464">Puede encontrar otro ejemplo de cómo tratar las condiciones de error en el [ejemplo de archivos de Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="c8e86-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="c8e86-465">El ejemplo de [LoggingHandler] proporciona un controlador delegado de registro para registrar las solicitudes realizadas al back-end.</span><span class="sxs-lookup"><span data-stu-id="c8e86-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="c8e86-466"><a name="headers"></a>Personalización de encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="c8e86-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="c8e86-467">Para admitir su escenario de aplicación específico, deberá personalizar la comunicación con el back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c8e86-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="c8e86-468">Por ejemplo, es posible que desee agregar un encabezado personalizado a cada solicitud saliente o cambiar los códigos de estado de las respuestas.</span><span class="sxs-lookup"><span data-stu-id="c8e86-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="c8e86-469">Puede hacer esto proporcionando un elemento [DelegatingHandler]personalizado, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8e86-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

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
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
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

<span data-ttu-id="c8e86-470">[Incorporación de la autenticación a su aplicación]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="c8e86-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="c8e86-471">[Sincronización de datos sin conexión en Aplicaciones móviles de Azure]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="c8e86-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="c8e86-472">[Agregar notificaciones de inserción a la aplicación]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="c8e86-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="c8e86-473">[registrar la aplicación para usar el inicio de sesión de la cuenta Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="c8e86-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="c8e86-474">[Configuración de App Service para usar el inicio de sesión de Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="c8e86-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="c8e86-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-481">[crea una referencia a una tabla sin tipo]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="c8e86-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="c8e86-497">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="c8e86-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="c8e86-498">[Portal de Azure clásico]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="c8e86-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="c8e86-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="c8e86-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="c8e86-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="c8e86-502">[Centro de desarrollo de Windows]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="c8e86-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="c8e86-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="c8e86-504">[SDK de Windows Live]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="c8e86-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="c8e86-506">[Referencias API]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="c8e86-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="c8e86-507">[ejemplo de archivos de Mobile Apps]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="c8e86-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="c8e86-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="c8e86-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="c8e86-509">[documentación de OData v3]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="c8e86-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="c8e86-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="c8e86-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="c8e86-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="c8e86-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="c8e86-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="c8e86-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="c8e86-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="c8e86-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
