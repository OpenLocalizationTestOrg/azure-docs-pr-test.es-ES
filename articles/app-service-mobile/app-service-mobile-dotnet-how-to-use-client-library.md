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
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooperform escenarios comunes con hello administración la biblioteca de cliente para aplicaciones de la aplicación de Azure Mobile de servicio de aplicaciones para Windows y Xamarin. Si está tooMobile de nuevas aplicaciones, debe considerar primera Hola completando [inicio rápido de aplicaciones móviles de Azure] [ 1] tutorial. Esta guía se centra en hello-cliente administrado SDK. toolearn Obtenga más información sobre hello servidor SDK para aplicaciones móviles, consulte la documentación de Hola para hello [.NET Server SDK] [ 2] o [Node.js Server SDK] [ 3].

## <a name="reference-documentation"></a>Documentación de referencia
Hello documentación de referencia de SDK de cliente de Hola se encuentra aquí: [referencia de cliente de .NET de aplicaciones móviles de Azure][4].
También puede encontrar varios ejemplos de cliente hello [repositorio de GitHub de ejemplos de Azure][5].

## <a name="supported-platforms"></a>Plataformas compatibles
Hola plataforma .NET admite Hola siguientes plataformas:

* Versiones de Xamarin Android para niveles de API 19-24 (de KitKat a Nougat)
* Versiones de Xamarin iOS para iOS 8.0 y posterior
* Plataforma universal de Windows
* Windows Phone 8,1
* Windows Phone 8.0, salvo para aplicaciones de Silverlight

la autenticación de "flujo de servidor" Hello usa un WebView para hello presentada la interfaz de usuario.  Si el dispositivo de hello no es capaz de toopresent una UI WebView, se necesitan otros métodos de autenticación.  Por tanto, este SDK no es adecuado para dispositivos de tipo reloj o con restricciones similares.

## <a name="setup"></a>Configuración y requisitos previos
Se supone que ya ha creado y publicado el proyecto de back-end de la aplicación móvil, que incluye al menos una tabla.  En el código de hello utilizado en este tema, se denomina tabla de hello `TodoItem` y tiene Hola siguientes columnas: `Id`, `Text`, y `Complete`. Esta tabla es hello misma tabla se crea al completar la [inicio rápido de aplicaciones móviles de Azure][1].

tipo de cliente con tipo correspondiente del Hello en C# es hello después de clase:

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

Hola [JsonPropertyAttribute] [ 6] es toodefine usado hello *PropertyName* la asignación entre los campos de cliente de Hola y Hola tabla.

toolearn cómo toocreate tablas en el back-end de aplicaciones móviles, consulte hello [tema de SDK de .NET Server] [ 7] o hello [tema de SDK de servidor Node.js] [ 8] . Si ha creado su aplicación móvil de back-end en hello Azure portal con Hola inicio rápido, también puede usar hello **tablas fácil** en hello [portal de Azure].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Cómo: instalar Hola administra el paquete del SDK de cliente
Uso de hello después hello tooinstall de métodos administrados paquete SDK de cliente para aplicaciones móviles de [NuGet][9]:

* **Visual Studio** haga clic en el proyecto, haga clic en **administrar paquetes de NuGet**, busque hello `Microsoft.Azure.Mobile.Client` del paquete, a continuación, haga clic en **instalar**.
* **Xamarin Studio** haga clic en el proyecto, haga clic en **agregar** > **agregar paquetes de NuGet**, busque hello `Microsoft.Azure.Mobile.Client `del paquete y, a continuación, haga clic en **agregar Paquete**.

En el archivo de actividad principal, recuerde siguiente de Hola de tooadd **con** instrucción:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Trabajo con símbolos de depuración en Visual Studio
símbolos de Hello para el espacio de nombres de hello Microsoft.Azure.Mobile están disponibles en [SymbolSource][10].  Consulte toothe [SymbolSource instrucciones] [ 11] toointegrate SymbolSource con Visual Studio.

## <a name="create-client"></a>Crear el cliente de aplicaciones móviles de Hola
Hello siguiente código crea hello [MobileServiceClient] [ 12] objeto tooaccess usa su aplicación móvil de back-end.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

En el anterior código de hello, reemplace `MOBILE_APP_URL` por dirección URL de Hola de back-end de aplicación móvil de hello, que se encuentra en la hoja para su aplicación móvil de back-end en hello [portal de Azure]. MobileServiceClient (objeto) Hola debe ser un singleton.

## <a name="work-with-tables"></a>Trabajo con tablas
Hola la siguiente sección se detallan cómo toosearch y recuperar registros y modificar los datos de hello en la tabla de Hola.  se trata Hola temas siguientes:

* [referencia de tabla](#instantiating)
* [Datos de consulta](#querying)
* [Filtro de datos devueltos](#filtering)
* [Ordenar datos devueltos](#sorting)
* [Devolver datos en páginas](#paging)
* [Seleccionar columnas específicas](#selecting)
* [Buscar un registro por identificador](#lookingup)
* [Trabajar con consultas sin tipo](#untypedqueries)
* [Insertar datos](#inserting)
* [Actualizar datos](#updating)
* [Eliminar datos](#deleting)
* [Resolución de conflictos y simultaneidad optimista](#optimisticconcurrency)
* [Enlace tooa interfaz de usuario de Windows](#binding)
* [Cambiar tamaño de página de Hola](#pagesize)

### <a name="instantiating"></a>Creación de una referencia de tabla
Todo el código de hello que obtiene acceso o modifica los datos de una tabla de back-end llama a funciones en hello `MobileServiceTable` objeto. Obtener una tabla de referencia toohello Hola llamada [GetTable] método, tal como se indica a continuación:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Hola devuelve el objeto utiliza el modelo de serialización con tipo hello. También se admite un modelo de serialización sin tipo. En el ejemplo siguiente se [crea una tabla sin tipo de referencia tooan]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

En las consultas sin tipo, debe especificar Hola subyacente de la cadena de consulta de OData.

### <a name="querying"></a>Consulta de datos desde la aplicación móvil
Esta sección describe cómo tooissue las consultas toohello aplicación móvil back-end, que incluye Hola siguiente funcionalidad:

* [Filtro de datos devueltos](#filtering)
* [Ordenar datos devueltos](#sorting)
* [Devolver datos en páginas](#paging)
* [Seleccionar columnas específicas](#selecting)
* [Buscar datos por identificador](#lookingup)

> [!NOTE]
> Un tamaño de página controlado por el servidor es tooprevent aplica todas las filas se devuelva.  Paginación mantiene las solicitudes de manera predeterminada para grandes conjuntos de datos no afecten negativamente a servicio de Hola.  tooreturn más de 50 filas, utilice hello `Skip` y `Take` método, como se describe en [devolver datos en páginas](#paging).

### <a name="filtering"></a>Filtro de datos devueltos
Hello código siguiente muestra cómo toofilter datos mediante la inclusión de un `Where` cláusula en una consulta. Devuelve todos los elementos de `todoTable` cuyo `Complete` propiedad es igual demasiado`false`. Hola [donde] función aplica un predicado de consulta de hello en la tabla de Hola de filtrado de filas.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

Puede ver Hola URI de hello solicitud enviada toohello back-end mediante software de inspección de mensaje, como herramientas de desarrollo de explorador o [Fiddler]. Si observa en el URI de solicitud de hello, tenga en cuenta que se modifica la cadena de consulta de hello:

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

Esta solicitud de OData se convierte en una consulta SQL por hello SDK del servidor:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

Hola de función que se pasa toohello `Where` método puede tener un número arbitrario de condiciones.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

En este ejemplo se traduciría en una consulta SQL por hello SDK del servidor:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

Esta consulta también se puede dividir en varias cláusulas:

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Hola dos métodos son equivalentes y se pueden usar indistintamente.  Hola opción anterior&mdash;de concatenar varios predicados en una consulta&mdash;más compacto y recomendada.

Hola `Where` cláusula admite operaciones que pueden convertir en subconjunto de OData de Hola. Estas son algunas de las operaciones:

* Operadores relacionales (==, !=, <, <=, >, >=)
* Operadores aritméticos (+, -, /, *, %)
* Precisión numérica (Math.Floor, Math.Ceiling)
* Funciones de cadena (Length, Substring, Replace, IndexOf, StartsWith, EndsWith)
* Propiedades de fecha (Year, Month, Day, Hour, Minute, Second)
* Propiedades de acceso de un objeto
* Expresiones combinando cualquiera de estas operaciones

Si es compatible con teniendo en cuenta qué Hola Server SDK, puede considerar hello [OData v3 documentación].

### <a name="sorting"></a>Clasificación de datos devueltos
Hello código siguiente muestra cómo toosort datos mediante la inclusión de un [OrderBy] o [OrderByDescending] función de consulta de Hola. Devuelve elementos de `todoTable` ordena de forma ascendente por hello `Text` campo.

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

### <a name="paging"></a>Devolución de datos en páginas
De forma predeterminada, Hola back-end devuelve solo Hola primeras 50 filas. Puede aumentar Hola número de filas devueltas por llamada hello [tomar] método. Use `Take` junto con hello [omitir] método toorequest una "página específica" del conjunto de datos total Hola devuelta por la consulta de Hola. Hello consulta siguiente, cuando se ejecuta, devuelve Hola tres primeros elementos de tabla de Hola.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

omite la siguiente consulta revisada Hola Hola tres primeros resultados y devuelve Hola siguientes tres resultados. Esta consulta genera Hola segunda "página" de datos, donde el tamaño de página de hello es tres elementos.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hola [IncludeTotalCount] método solicita el recuento total de Hola de *todos los* Hola registros que se hubieran devuelto, se omitirá cualquier cláusula de paginación/límite especificada:

```
query = query.IncludeTotalCount();
```

En una aplicación del mundo real, puede usar consultas toohello similar anterior ejemplo con un control de paginación o la interfaz de usuario comparable para navegar entre las páginas.

> [!NOTE]
> límite de 50 filas de hello toooverride en un aplicación móvil de back-end, también debe aplicar hello [EnableQueryAttribute] toohello público GET (método) y especificar el comportamiento de paginación de Hola. Cuando método de toohello aplicado, Hola después establece el número máximo de filas devuelto too1000:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Selección de columnas específicas
Puede especificar qué conjunto de propiedades tooinclude Hola agregando un [seleccione] consulta tooyour de cláusula. Por ejemplo, Hola siguiente de código muestra cómo tooselect en un solo campo y también cómo tooselect y dar formato a varios campos:

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

Todos los Hola funciones descritas hasta ahora son aditivas, por lo que se pueden mantener el encadenamiento de ellos. Cada llamada encadenada afecta a más de consulta de Hola. A continuación se muestra un ejemplo más:

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Búsqueda de datos por identificador
Hola [LookupAsync] función puede ser toolook usa los objetos de base de datos de hello con un identificador determinado.

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Ejecución de consultas sin tipo
Cuando se ejecuta una consulta con un objeto de tabla sin tipo, debe especificar explícitamente cadena de consulta de OData de hello mediante una llamada a [ReadAsync], como en el siguiente ejemplo de Hola:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

Vuelva a obtener valores JSON que puede usar como un contenedor de propiedades. Para obtener más información sobre JToken y Newtonsoft Json.NET, vea hello [Json.NET] sitio.

### <a name="inserting"></a>Inserción de datos en el back-end de una aplicación móvil
Todos los tipos de cliente deben incluir un miembro llamado **Id**, que es una cadena de forma predeterminada. Esto **identificador** es necesaria para realizar operaciones CRUD y para la sincronización sin conexión. Hola siguiente código ilustra cómo hello toouse [InsertAsync] tooinsert nuevas filas en una tabla de método. parámetro Hello contiene Hola datos toobe insertado como un objeto. NET.

```
await todoTable.InsertAsync(todoItem);
```

Si no se incluye un único valor de identificador personalizado en hello `todoItem` durante una inserción, un GUID generado por el servidor de Hola.
Puede recuperar Hola genera identificador mediante la inspección objeto Hola después Hola llamada devuelve.

tooinsert sin tipo de datos, puede sacar partido de Json.NET:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

A continuación, se muestra un ejemplo en el que se usa una dirección de correo electrónico como identificador de cadena exclusivo:

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>Trabajar con valores de Id.
Aplicaciones móviles es compatible con los valores de cadena personalizado único para la tabla de hello **identificador** columna. Un valor de cadena permite que las aplicaciones toouse valores personalizados, como direcciones de correo electrónico o nombres de usuario para Id. de Hola.  Identificadores de cadena proporcionan Hola siguientes ventajas:

* Se generan identificadores sin crear una base de datos de toohello de ida y vuelta.
* Los registros son toomerge más fácil de diferentes tablas o bases de datos.
* Los valores de los identificadores pueden integrarse mejor con una lógica de aplicación.

Si no se establece un valor de identificador de cadena en un registro insertado, back-end de aplicación móvil de hello genera un valor único para el identificador. Puede usar hello [Guid.NewGuid] toogenerate método su propio Id. de valores, en el cliente de Hola o en hello back-end.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Modificación de datos en el back-end de una aplicación móvil
Hello código siguiente muestra cómo hello toouse [UpdateAsync] método tooupdate un registro existente con hello mismo identificador con la nueva información. parámetro Hello contiene hello toobe de datos actualizado como un objeto. NET.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate sin tipo de datos, puede sacar partido de [Json.NET] como se indica a continuación:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

Debe especificarse un campo `id` al realizar una actualización. Hola back-end utiliza hello `id` tooidentify de campo que tooupdate de fila. Hola `id` campo puede obtenerse de resultado de hello de hello `InsertAsync` llamar. Un `ArgumentException` se produce si intenta tooupdate un elemento sin proporcionar hello `id` valor.

### <a name="deleting"></a>Eliminación de datos del back-end de una aplicación móvil
Hello código siguiente muestra cómo hello toouse [DeleteAsync] método toodelete una instancia existente. Hola instancia se identifica por hello `id` campo establecido en hello `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete sin tipo de datos, puede sacar partido de Json.NET como se indica a continuación:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

Al realizar una solicitud de eliminación, debe especificarse un identificador. Otras propiedades no se pasan toohello servicio o se omiten al servicio de Hola. Hola resultado de un `DeleteAsync` suele ser llamada `null`. toopass de Id. de Hello en puede obtenerse de resultado de hello de hello `InsertAsync` llamar. A `MobileServiceInvalidOperationException` se produce cuando intenta toodelete un elemento sin especificar hello `id` campo.

### <a name="optimisticconcurrency"></a>Uso de la simultaneidad optimista para resolver conflictos
Dos o más clientes pueden escribir cambios toohello mismo elemento en hello mismo tiempo. Sin la detección de conflictos, última operación de escritura Hola reemplazaría las actualizaciones anteriores. **control de simultaneidad optimista** asume que cada transacción puede confirmarse y, por lo tanto, no usa ningún bloqueo de recursos.  Antes de confirmar una transacción, control de simultaneidad optimista comprueba que ninguna otra transacción ha modificado datos Hola. Si se han modificado los datos de hello, Hola confirmar la transacción se revierte.

Aplicaciones móviles admite el control de simultaneidad optimista al realizar un seguimiento de elemento de tooeach de cambios mediante hello `version` columna de propiedades del sistema que se define para cada tabla en el aplicación móvil de back-end. Cada vez que se actualiza un registro, aplicaciones móviles establece hello `version` propiedad para que registre tooa nuevo valor. Durante cada solicitud de actualización, Hola `version` propiedad del registro de hello incluido en la solicitud de hello es toohello comparado misma propiedad de registro de hello en el servidor de Hola. Si la versión que se pasa con solicitud hello no coincide con el back-end de Hola, Hola biblioteca de cliente genera un `MobileServicePreconditionFailedException<T>` excepción. tipo de Hello incluido con la excepción de hello es registro Hola de versión de servidores Hola contenedor de Hola de back-end de registro de hello. Hello aplicación puede utilizar esta información toodecide si tooexecute solicitud de actualización de hello nuevo con hello correcto `version` valor de los cambios de toocommit de hello back-end.

Definir una columna en la clase de tabla de Hola para hello `version` simultaneidad optimista de sistema propiedad tooenable. Por ejemplo:

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

Habilitar las aplicaciones que usan tablas sin tipo simultaneidad optimista establecer hello `Version` marca en el `SystemProperties` de hello tabla como se indica a continuación.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

En la suma tooenabling optimista de simultaneidad, que debe detectar hello `MobileServicePreconditionFailedException<T>` excepción en el código cuando se llama a [UpdateAsync].  Resolver conflicto de hello mediante la aplicación hello correcto `version` toothe actualizar registro y llame al método [UpdateAsync] con hello resolvió el registro. Hola siguiente código muestra cómo tooresolve un conflicto de escritura una vez detectado:

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

Para obtener más información, vea hello [sin conexión la sincronización de datos en aplicaciones móviles de Azure] tema.

### <a name="binding"></a>Cómo: interfaz de usuario de Windows tooa de aplicaciones móviles de enlace de datos
Esta sección muestra cómo toodisplay devuelve objetos de datos utilizando los elementos de interfaz de usuario de una aplicación de Windows.  El siguiente código de ejemplo enlaza origen toohello de lista de hello con una consulta para elementos incompletos. [MobileServiceCollection] crea una colección de enlaces compatible con Mobile Apps.

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

Algunos controles Hola administran compatibilidad en tiempo de ejecución llama a una interfaz [ISupportIncrementalLoading]. Esta interfaz permite a los controles toorequest datos adicionales cuando se desplaza por el usuario de Hola. No hay compatibilidad integrada para esta interfaz para aplicaciones universales de Windows a través de [MobileServiceIncrementalLoadingCollection], que controla automáticamente las llamadas de los controles de Hola. Use `MobileServiceIncrementalLoadingCollection` en aplicaciones Windows de la siguiente manera:

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse Hola nueva colección en aplicaciones de Windows Phone 8 y "Silverlight", use hello `ToCollection` métodos de extensión en `IMobileServiceTableQuery<T>` y `IMobileServiceTable<T>`. datos de tooload, llame a `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

Cuando se usa la colección de hello creada mediante una llamada a `ToCollectionAsync` o `ToCollection`, obtiene una colección que puede ser controles enlazados tooUI.  Esta colección es para la paginación.  Puesto que la colección de hello está cargando datos de la red, a veces no se puede cargar. toohandle tales errores, invalidar hello `OnException` método `MobileServiceIncrementalLoadingCollection` toohandle excepciones derivadas de llamadas demasiado`LoadMoreItemsAsync`.

Tenga en cuenta si la tabla tiene muchos campos, pero sólo desea toodisplay algunas de ellas en el control. Puede usar instrucciones de Hola Hola sección anterior "[seleccionar columnas específicas](#selecting)" tooselect columnas específicas toodisplay Hola interfaz de usuario.

### <a name="pagesize"></a>Hola cambiar tamaño de página
Mobile Apps de Azure devuelve un máximo de 50 elementos por cada solicitud de forma predeterminada.  Puede cambiar el tamaño de paginación de hello aumentando el tamaño de página máximo de hello en el cliente de Hola y el servidor.  tooincrease Hola tamaño de página solicitado, especifique `PullOptions` al usar `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Suponiendo que haya realizado hello `PageSize` tooor igual superior a 100 en el servidor de hello, una solicitud devuelve hasta 100 elementos.

## <a name="#offlinesync"></a>Trabajo con tablas sin conexión
Tablas sin conexión utilizan un almacén toostore datos local de SQLite para su uso sin conexión.  Tabla de todas las operaciones se realizan contra Hola SQLite local almacenar en lugar de almacén de servidor remoto de Hola.  toocreate una tabla sin conexión, preparar el proyecto:

1. En Visual Studio, haga clic en soluciones de hello > **administrar paquetes de NuGet para la solución...** , a continuación, buscar e instalar el **Microsoft.Azure.Mobile.Client.SQLiteStore** paquete NuGet para todos los proyectos de la solución de Hola.
2. Dispositivos de Windows toosupport (opcional), instale uno de los siguientes paquetes en tiempo de ejecución de código de hello:

   * **Runtime de Windows 8.1:** instale [SQLite para Windows 8.1][3].
   * **Windows Phone 8.1:** instale [SQLite para Windows Phone 8.1][4].
   * **Plataforma universal de Windows** instalar [SQLite para hello universales de Windows][5].
3. (Opcional). Para dispositivos de Windows, haga clic en **referencias** > **Agregar referencia...** , expanda hello **Windows** carpeta > **extensiones**, a continuación, habilite Hola adecuado **SQLite para Windows** SDK junto con hello  **Visual C++ 2013 en tiempo de ejecución para Windows** SDK.
    Hello SQLite SDK nombres varían ligeramente con cada plataforma de Windows.

Para poder crear una referencia de tabla, debe estar preparado almacén local de hello:

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

Inicialización del almacén se hace normalmente inmediatamente después de que se crea el cliente de Hola.  Hola **OfflineDbPath** debe ser un nombre de archivo adecuado para su uso en todas las plataformas que se admiten.  Si la ruta de acceso de hello es una ruta de acceso completa (es decir, se inicia con una barra diagonal), a continuación, se utiliza dicha ruta de acceso.  Si la ruta de acceso de hello no está completo, el archivo hello se coloca en una ubicación específica de la plataforma.

* Para dispositivos iOS y Android, ruta de acceso de hello predeterminada es la carpeta de "Archivos personales" de Hola.
* Para dispositivos de Windows, ruta de acceso de hello predeterminada es "AppData" carpeta de hello específica de la aplicación.

Puede obtener una referencia de tabla mediante hello `GetSyncTable<>` método:

```
var table = client.GetSyncTable<TodoItem>();
```

No es necesario tooauthenticate toouse una tabla sin conexión.  Solo debe tooauthenticate al que se está comunicando con el servicio back-end de Hola.

### <a name="syncoffline"></a>Sincronización de una tabla sin conexión
Tablas sin conexión no están sincronizadas con hello back-end de forma predeterminada.  La sincronización se divide en dos partes.  Mediante la descarga de elementos nuevos puede insertar los cambios por separado.  Éste es un método de sincronización típico:

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

Si Hola primer argumento demasiado`PullAsync` es null, no se utiliza la sincronización incremental.  Todas las operaciones de sincronización recuperan todos los registros.

Hola SDK realiza implícita `PushAsync()` antes de extraer registros.

El control de los conflictos se realiza en un método `PullAsync()`.  Se puede resolver los conflictos en hello igual manera que las tablas en línea.  se produce el conflicto de Hello cuando `PullAsync()` se llama en lugar de durante Hola insert, update o delete. Si se producen varios conflictos, se agrupan en una sola clase MobileServicePushFailedException.  Trate cada error por separado.

## <a name="#customapi"></a>Trabajo con una API personalizada
Una API personalizada le permite toodefine extremos personalizados que exponen la funcionalidad de servidor que no asigne tooan Insertar, actualizar, eliminar o la operación de lectura. Al usar una API personalizada, puede tener más control sobre la mensajería, incluida la lectura y el establecimiento de encabezados de mensajes HTTP y la definición del formato del cuerpo de un mensaje diferente de JSON.

Se llama a una API personalizada mediante una llamada a uno de hello [InvokeApiAsync] métodos en el cliente de Hola. Por ejemplo, después de la línea de código de hello envía una toohello de solicitud POST **completeAll** API en hello back-end:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Este formulario es una llamada de método con tipo y requiere que hello **MarkAllResult** devolver el tipo está definido. Se admiten métodos con y sin tipos.

Hola InvokeApiAsync() método antepone/api/toohello API que desea toocall a menos que Hola API comienza con un '/'.
Por ejemplo:

* `InvokeApiAsync("completeAll",...)`llama a /api/completeAll en hello back-end
* `InvokeApiAsync("/.auth/me",...)`llama a /.auth/me en hello back-end

Puede usar InvokeApiAsync toocall cualquier WebAPI, incluidos los que no estén definidos WebAPIs con aplicaciones de Azure Mobile.  Cuando usa InvokeApiAsync(), encabezados apropiados de hello, incluidos los encabezados de autenticación, se envían con la solicitud de Hola.

## <a name="authentication"></a>Autenticación de usuarios
Mobile Apps es compatible con la autenticación y la autorización de los usuarios de aplicaciones mediante diversos proveedores de identidades externas: Facebook, Google, cuenta de Microsoft, Twitter y Azure Active Directory. Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios. También puede utilizar la identidad de Hola de reglas de autorización de los usuarios autenticados tooimplement en scripts de servidor. Para obtener más información, vea el tutorial de hello [agregar autenticación tooyour aplicación].

Se admiten dos flujos de autenticación: *administrado por cliente* y *administrado por servidor*. flujo de servidor administrado de Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de autenticación del proveedor de hello web. flujo de Hello administrados por el cliente permite una integración más profunda con capacidades específicas del dispositivo tal y como se basa en el SDK de específica del proveedor específico del dispositivo.

> [!NOTE]
> En las aplicaciones de producción se recomienda usar un flujo administrado por el cliente.

tooset la autenticación, debe registrar la aplicación con uno o varios proveedores de identidad.  proveedor de identidades de Hello genera un identificador de cliente y un secreto de cliente para la aplicación.  Estos valores, a continuación, se establecen en su tooenable de back-end autenticación/autorización de servicio de aplicaciones de Azure.  Para obtener más información, siga Hola instrucciones detalladas en el tutorial [agregar autenticación tooyour aplicación].

Hola temas siguientes se trata en esta sección:

* [Autenticación administrada por el cliente](#clientflow)
* [Autenticación administrada por el servidor](#serverflow)
* [Token de autenticación de almacenamiento en caché Hola](#caching)

### <a name="clientflow"></a>Autenticación administrada por el cliente
La aplicación puede independientemente en contacto con el proveedor de identidades de hello y, a continuación, proporcionar token devuelto Hola durante el inicio de sesión con el back-end. Este flujo de cliente le permite tooprovide una experiencia de inicio de sesión única para los usuarios o los datos de usuario adicionales tooretrieve Hola del proveedor de identidades. Autenticación del cliente flujo es preferido toousing un flujo de servidor como proveedor de identidades de hello SDK proporciona una idea UX más nativa y permite la personalización adicional.

Se proporcionan ejemplos para hello siguientes patrones de autenticación de flujo de cliente:

* [Biblioteca de autenticación de Active Directory](#adal)
* [Facebook o Google](#client-facebook)
* [SDK de Live](#client-livesdk)

#### <a name="adal"></a>Autenticar a los usuarios con hello biblioteca de autenticación de Active Directory
Puede utilizar la autenticación de usuario de hello biblioteca de autenticación de Active Directory (ADAL) tooinitiate de cliente de hello mediante la autenticación de Azure Active Directory.

1. Configurar el aplicación móvil de back-end para el inicio de sesión en AAD Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Active Directory] tutorial. Asegúrese de que paso opcional de Hola de toocomplete de registrar una aplicación cliente nativa.
2. En Visual Studio o Xamarin Studio, abra el proyecto y agregar una referencia toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` paquete NuGet. Al buscar, incluya las versiones preliminares.
3. Agregar Hola tras la aplicación de código tooyour, según la plataforma de toohello que usa. En cada una, asegúrese de Hola después reemplazos:

   * Reemplace **aquí de autoridad de INSERCIÓN** por nombre de Hola de inquilino de hello en el que se aprovisiona la aplicación. El formato debería ser https://login.microsoftonline.com/contoso.onmicrosoft.com. Este valor se puede copiar desde la pestaña del dominio hello en Azure Active Directory en hello [portal de Azure clásico].
   * Reemplace **Insertar recurso identificador aquí** con el identificador de cliente de Hola para su aplicación móvil de back-end. Puede obtener Id. de cliente de Hola de hello **avanzadas** en la ficha **configuración de Azure Active Directory** en el portal de Hola.
   * Reemplace **INSERT-CLIENT-ID-aquí** con el Id. de cliente de Hola que copió de la aplicación de cliente nativo de Hola.
   * Reemplace **INSERT-REDIRECT-URI-aquí** con su sitio */.auth/login/done* punto de conexión, mediante el esquema de hello HTTPS. Este valor debe ser similar demasiado*https://contoso.azurewebsites.net/.auth/login/done*.

     código de Hello necesario para cada plataforma sigue:

     **Windows:**

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

     **Xamarin.iOS**

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

     **Xamarin.Android**

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

#### <a name="client-facebook"></a>Inicio de sesión único mediante un token de Facebook o Google
Puede usar flujo de cliente de hello tal y como se muestra en este fragmento de código para Facebook o Google.

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

#### <a name="client-livesdk"></a>Inicio de sesión único con Microsoft Account con Hola SDK de Live
los usuarios de tooauthenticate, debe registrar la aplicación en hello cuenta Centro para desarrolladores de Microsoft. Configure los detalles del registro en su back-end de aplicación móvil. toocreate Microsoft el registro de cuenta y conexión back-end de tooyour aplicación móvil, Hola completa los pasos de [registrar su toouse de aplicación un inicio de sesión de cuenta de Microsoft]. Si tiene las versiones de tienda Windows y Windows Phone 8/Silverlight de la aplicación, registre primero la versión de tienda Windows hello.

Hello código siguiente se autentica mediante Live SDK y utiliza Hola devuelve toosign token en el back-end de tooyour aplicación móvil.

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

Para obtener más información, vea hello [Windows Live SDK] documentación.

### <a name="serverflow"></a>Autenticación administrada por el servidor
Una vez que ha registrado el proveedor de identidad, llame a hello [LoginAsync] método en hello [MobileServiceClient] con hello [MobileServiceAuthenticationProvider] valor del proveedor. Por ejemplo, hello código siguiente inicia un inicio de sesión de flujo de servidor mediante el uso de Facebook.

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

Si está utilizando un proveedor de identidades distinto a Facebook, cambie el valor de Hola de [MobileServiceAuthenticationProvider] toohello valor para el proveedor.

En un flujo de servidor, servicio de aplicaciones de Azure administra el flujo de autenticación de OAuth de hello mostrando la página de inicio de sesión de Hola de proveedor seleccionado Hola.  Una vez devuelve de proveedor de identidad de hello, servicio de aplicaciones de Azure genera un token de autenticación de servicio de aplicaciones. Hola [LoginAsync] método devuelve un [MobileServiceUser], que proporciona ambos hello [UserId] de hello autenticado hello y usuario [ MobileServiceAuthenticationToken], como un token de web JSON (JWT). El token puede almacenarse en caché y volver a usarse hasta que expire. Para obtener más información, consulte [token de autenticación de almacenamiento en caché hello](#caching).

### <a name="caching"></a>Token de autenticación de almacenamiento en caché Hola
En algunos casos, se puede evitar método de inicio de sesión de hello llamada toohello después de la primera autenticación correcta de hello almacenando el token de autenticación de Hola de proveedor de Hola.  Pueden utilizar aplicaciones de la tienda Windows y UWP [PasswordVault] toocache la autenticación actual token después una correcta inicio de sesión, como se indica a continuación:

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Hola valor de identificador de usuario se almacena como nombre de usuario de la credencial de Hola Hola y token hello es hello almacenado como Hola contraseña. En las nuevas empresas posteriores, puede comprobar hello **PasswordVault** para credenciales almacenadas en caché. Hello en el ejemplo siguiente se usa credenciales almacenadas en caché cuando se encuentran y, en caso contrario, intente tooauthenticate nuevo con hello back-end:

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

Cuando inicia sesión un usuario, también debe quitar credencial Hola almacenado, como se indica a continuación:

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Aplicaciones Xamarin usan hello [Xamarin.Auth] las credenciales del almacén de toosecurely de API en un **cuenta** objeto. Para obtener un ejemplo del uso de estas API, consulte hello [AuthStore.cs] archivo de código en hello [ejemplo de uso compartido de fotografías de ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).

Al utilizar la autenticación de cliente administrada, también puede almacenar en caché los token de acceso de hello obtenido de su proveedor, como Facebook o Twitter. Este token puede ser proporcionado toorequest un nuevo token de autenticación de back-end de hello, como se indica a continuación:

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Notificaciones push
Hello en los temas siguientes tratan las notificaciones de inserción:

* [Registro de notificaciones push](#register-for-push)
* [Obtención del SID de un paquete de la Tienda Windows](#package-sid)
* [Registro con plantillas multiplataforma](#register-xplat)

### <a name="register-for-push"></a>Cómo registrarse para recibir notificaciones push
cliente de aplicaciones móviles de Hello permite tooregister para las notificaciones de inserción con centros de notificaciones de Azure. Al registrar, se obtiene un identificador que obtiene de hello específica de la plataforma servicio de notificación de inserción (PNS). A continuación, proporcionar este valor junto con las etiquetas cuando se crea el registro de hello. Hola de código siguiente registra la aplicación de Windows para las notificaciones de inserción con hello servicios de notificación de Windows (WNS):

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

Si va a insertar tooWNS, entonces debe [obtener un paquete de la tienda Windows SID](#package-sid).  Para obtener más información sobre aplicaciones de Windows, incluyendo cómo tooregister para registros de plantilla, consulte [aplicación de tooyour de notificaciones de inserción de agregar].

No se admite la solicitud de etiquetas de cliente de Hola.  Las solicitudes de etiquetas se quitan del registro en modo silencioso.
Si desea que el dispositivo con etiquetas tooregister, cree una API personalizada que utiliza el registro de hello API de bases de datos centrales de notificación tooperform hello en su nombre.  [Llamar a API personalizada hello](#customapi) en lugar de hello `RegisterNativeAsync()` método.

### <a name="package-sid"></a>Obtención del SID de un paquete de la Tienda Windows.
Se necesita un SID de paquete para habilitar las notificaciones push en aplicaciones de la Tienda Windows.  tooreceive un SID, del paquete registrando su aplicación con hello tienda Windows.

tooobtain este valor:

1. En Visual Studio Solution Explorer, el proyecto de aplicación de tienda de Windows de Hola de menú contextual, haga clic en **almacén** > **asociar aplicación con hello almacén...** .
2. En el Asistente de hello, haga clic en **siguiente**, inicie sesión con su cuenta de Microsoft, escriba un nombre para la aplicación en **reservar un nuevo nombre de aplicación**, a continuación, haga clic en **reserva**.
3. Después de registro de una aplicación Hola es el nombre de la aplicación se creó correctamente, seleccione hello, haga clic en **siguiente**y, a continuación, haga clic en **asociar**.
4. Inicie sesión en toohello [centro de desarrollo de Windows] con su Account de Microsoft. En **mis aplicaciones**, haga clic en el registro de una aplicación Hola que creó.
5. Haga clic en **la administración de aplicaciones** > **identidad de aplicación**y, a continuación, desplácese hacia abajo de toofind su **SID del paquete**.

Muchos usos de SID del paquete Hola tratan como un URI, en cuyo caso deberá toouse *ms-app: / /* como esquema de Hola. Tome nota de la versión de Hola de su formado concatenando este valor como prefijo el SID del paquete.

Las aplicaciones de Xamarin requieren algunos tooregister capaz de código adicional toobe aplicaciones que se ejecutan en plataformas de Android o iOS Hola. Para obtener más información, vea el tema de Hola para su plataforma:

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Cómo: notificaciones de registro inserción plantillas toosend multiplataforma
plantillas de tooregister, usar hello `RegisterAsync()` método con las plantillas de hello, como se indica a continuación:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

Las plantillas deben ser `JObject` tipos y pueden contener varias plantillas en hello siguiendo el formato JSON:

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

Hola método **RegisterAsync()** también acepta iconos secundarios:

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Por seguridad, todas las etiquetas se eliminan durante el registro. tooadd etiquetas tooinstallations o plantillas en las instalaciones, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure].

notificaciones de toosend utilización de estas plantillas registradas, consulte toohello [API de los centros de notificación].

## <a name="misc"></a>Temas variados
### <a name="errors"></a>Gestión de errores
Cuando se produce un error en el back-end de Hola, cliente hello SDK provoca un `MobileServiceInvalidOperationException`.  El siguiente ejemplo se muestra cómo toohandle una excepción que se devuelve por hello back-end:

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

Otro ejemplo de trabajar con las condiciones de error puede encontrarse en hello [ejemplo de archivos de aplicaciones móviles]. El [LoggingHandler] en el ejemplo se proporciona un delegado de registro de solicitudes de Hola de toolog de controlador que se realizan toohello back-end.

### <a name="headers"></a>Personalización de encabezados de solicitud
toosupport su escenario de aplicación específica, tendrá que toocustomize la comunicación con el back-end de hello aplicación móvil. Por ejemplo, puede desee tooadd una solicitud de salida de encabezado personalizado tooevery o incluso cambiar los códigos de estado de las respuestas. Puede utilizar un personalizado [DelegatingHandler], como en el siguiente ejemplo de Hola:

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
