---
title: aaaWork con desencadenadores y los enlaces de funciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse desencadenadores y los enlaces de funciones de Azure tooconnect los eventos de tooonline de ejecución de código y servicios en la nube."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Conceptos básicos sobre los enlaces y desencadenadores de Azure Functions
Las funciones de Azure permite toowrite código de respuesta tooevents en Azure y otros servicios a través de *desencadenadores* y *enlaces*. En este artículo, se ofrece una introducción conceptual a los desencadenadores y enlaces de todos los lenguajes de programación compatibles. Características que son comunes enlaces tooall se describen aquí.

## <a name="overview"></a>Información general

Desencadenadores y los enlaces son un toodefine de manera declarativa cómo se invoca una función y los datos que funciona con. Los *desencadenadores* establecen el modo de invocar una función. Cada función debe tener exactamente un desencadenador. Los desencadenadores tienen asociados datos, que suele ser carga Hola que desencadenó la función hello. 

Entrada y salida *enlaces* proporcionan un toodata de tooconnect de manera declarativa desde dentro del código. Tootriggers similar, puede especificar las cadenas de conexión y otras propiedades en la configuración de la función. Los enlaces son opcionales y cada función puede tener varios enlaces de entrada y de salida. 

Mediante enlaces y desencadenadores, puede escribir código que es más genérico y no codificar los detalles de hello de servicios de hello con la que interactúa. Los datos procedentes de los servicios se convierten simplemente en valores de entrada para el código de función. servicio de tooanother de datos toooutput (por ejemplo, para crear una nueva fila en el almacenamiento de tabla de Azure), utilice valor devuelto de hello del método hello. O bien, si necesita toooutput varios valores, use un objeto auxiliar. Desencadenadores y los enlaces tienen un **nombre** propiedad, que es un identificador que se utiliza en el enlace de Hola de tooaccess de código.

Puede configurar los desencadenadores y los enlaces de hello **integrar** ficha en el portal de Azure funciones hello. Tras bastidores de hello, Hola interfaz de usuario modifica un archivo denominado *function.json* archivo en el directorio de la función de Hola. Este archivo se puede modificar cambiando toohello **editor avanzado**.

Hello tabla siguiente muestran los desencadenadores de Hola y enlaces que son compatibles con las funciones de Azure. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Ejemplo: desencadenador de colas y enlace de salida de tablas

Imagine que desea toowrite una tooAzure fila nueva tabla de almacenamiento cada vez que un mensaje nuevo aparece en el almacenamiento de la cola de Azure. Este escenario puede implementarse mediante un desencadenador de colas de Azure y un enlace de salida de tablas. 

Un desencadenador de cola requiere Hola siguiendo la información de hello **integrar** ficha:

* nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de cuenta de almacenamiento de Hola para cola de Hola
* nombre de la cola de Hola
* Hola identificador en el contenido del código tooread Hola Hola del mensaje de cola, como `order`.

toowrite tooAzure almacenamiento de tabla, utilice un enlace de salida con hello detalles siguientes:

* nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de cuenta de almacenamiento de hello para la tabla de Hola
* nombre de la tabla de Hola
* identificador Hello en su toocreate de código de salida elementos u Hola de valor devuelto de función hello.

Enlaces de usan la configuración de aplicación para Hola de tooenforce de cadenas de conexión mejor práctica que *function.json* no contiene secretos de servicio.

A continuación, usar identificadores de hello proporcionados toointegrate con el almacenamiento de Azure en el código.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Aquí es hello *function.json* que corresponde toohello anterior el código. Tenga en cuenta que Hola misma configuración puede utilizarse, independientemente del lenguaje de Hola de implementación de la función de Hola.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
tooview y editar contenido de Hola de *function.json* en hello portal de Azure, haga clic en hello **editor avanzado** opción en hello **integrar** pestaña de la función.

Para obtener más ejemplos de código e información sobre la integración con Azure Storage, consulte el artículo sobre [desencadenadores y enlaces de Azure Functions para Azure Storage](functions-bindings-storage.md).

### <a name="binding-direction"></a>Dirección de los enlaces

Todos los desencadenadores y enlaces tienen la propiedad `direction`:

- Para los desencadenadores, dirección de hello es siempre`in`
- Los enlaces de entrada y de salida usan `in` y `out`
- Algunos enlaces admiten la dirección especial `inout`. Si usa `inout`, solo Hola **editor avanzado** está disponible en hello **integrar** ficha.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>Uso de tooreturn de tipo de valor devuelto de función hello una salida única

Hello en el ejemplo anterior se muestra cómo tooprovide de valor devuelto de función de hello toouse salida tooa enlace, que se consigue mediante el parámetro de nombre especial de hello `$return`. (Esto solo se admite en los lenguajes que presenten un valor devuelto, como C#, JavaScript y F#). Si una función tiene varios enlaces de salida, use `$return` para una sola Hola de enlaces de salida. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

ejemplos de Hello siguientes se muestra cómo devolución tipos se utilizan con enlaces de salida en C#, JavaScript y F #.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>Enlace de la propiedad DataType

En. NET, utilice tipos Hola Hola tipos toodefine para datos de entrada. Por ejemplo, usar `string` toobind toohello texto de un desencadenador de cola y una tooread de matriz de bytes como binario.

Para los idiomas que se escriben dinámicamente, como JavaScript, usar hello `dataType` propiedad en la definición de enlace de Hola. Por ejemplo, tooread Hola contenido de una solicitud HTTP en formato binario, usar tipo hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Otras opciones para `dataType` son `stream` y `string`.

## <a name="resolving-app-settings"></a>Resolver la configuración de la aplicación
Como procedimiento recomendado, los secretos y las cadenas de conexión deberían administrarse mediante los ajustes de la aplicación, en lugar de archivos de configuración. Esto limita el acceso toothese secretos y resulta seguro toostore *function.json* en un repositorio de control de código fuente pública.

Configuración de la aplicación también es útil cuando lo desee configuración toochange según el entorno de Hola. Por ejemplo, en un entorno de prueba, puede que desee toomonitor otro contenedor de almacenamiento cola o un blob.

Los ajustes de la aplicación se resuelven cuando un valor aparece entre símbolos de porcentaje; por ejemplo `%MyAppSetting%`. Tenga en cuenta que hello `connection` propiedad de desencadenadores y enlaces es un caso especial y soluciona automáticamente los valores de configuración de la aplicación. 

el ejemplo siguiente se Hello es un desencadenador de cola que usa una configuración de aplicación `%input-queue-name%` toodefine Hola cola tootrigger en.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Propiedades de metadatos de los desencadenadores

En la carga de datos de adición toohello proporcionada por un desencadenador (por ejemplo, el mensaje de cola de Hola que desencadenó una función), desencadenadores muchos proporcionan valores de metadatos adicionales. Estos valores se pueden usar como parámetros de entrada en C# y F # o propiedades en hello `context.bindings` objetos en JavaScript. 

Por ejemplo, un desencadenador de cola admite Hola propiedades siguientes:

* QueueTrigger (desencadena el contenido del mensaje si hay una cadena válida)
* DequeueCount
* ExpirationTime
* Id
* InsertionTime
* NextVisibleTime
* PopReceipt

Detalles de propiedades de metadatos para cada desencadenador se describen en el tema de referencia correspondiente de Hola. Documentación también está disponible en hello **integrar** ficha del portal Hola Hola **documentación** sección por debajo del área de configuración de enlace de Hola.  

Por ejemplo, dado que los desencadenadores de blob tienen algunos retrasos, puede usar un toorun de desencadenador de cola la función (vea [desencadenador de almacenamiento Blob](functions-bindings-storage-blob.md#storage-blob-trigger). mensaje de la cola de Hello contendría tootrigger de nombre de archivo de blob de hello en. Con hello `queueTrigger` propiedad de metadatos, este comportamiento se puede especificar en la configuración, en lugar de su código.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Propiedades de metadatos de un desencadenador también se pueden usar en un *expresión de enlace* para otro enlace, como se describe en hello pasos de la sección.

## <a name="binding-expressions-and-patterns"></a>Patrones y expresiones de enlace

Una de las características más eficaces de Hola de desencadenadores y enlaces es *expresiones de enlace*. En el enlace, puede definir expresiones de patrón que, después, podrán emplearse en otros enlaces o en el código. Metadatos de desencadenador también pueden utilizarse para enlazar las expresiones, como se muestra en el ejemplo de Hola Hola sección anterior.

Por ejemplo, imagine que desea tooresize imágenes de contenedor de almacenamiento de blob determinado, toohello similar **tamaño de imagen** plantilla Hola **nueva función** página. Vaya demasiado**nueva función** -> lenguaje **C#** -> escenario **ejemplos** -> **ImageResizer CSharp**. 

Aquí es hello *function.json* definición:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

Tenga en cuenta que hello `filename` parámetro se utiliza en la definición del desencadenador Hola blob así como blob de hello el enlace de salida. Este parámetro también puede incluirse en el código de la función.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>GUID aleatorios
Las funciones de Azure proporciona una sintaxis de conveniencia para generar GUID en sus enlaces a través de hello `{rand-guid}` expresión de enlace. Hello en el ejemplo siguiente se utiliza este toogenerate un nombre de blob único: 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Hora actual

Puede utilizar la expresión de enlace de hello `DateTime`, que se resuelve demasiado`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Enlazar las propiedades de entrada toocustom en una expresión de enlace

Expresiones de enlace pueden hacer referencia a propiedades que se definen en la carga de desencadenador de hello propio. Por ejemplo, puede que desee toodynamically enlace tooa: archivo de almacenamiento blob de un nombre de archivo proporcionado en un webhook.

Por ejemplo, Hola después *function.json* utiliza una propiedad denominada `BlobName` de carga de desencadenador de hello:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish este en C# y F #, debe definir un POCO que define los campos de Hola que se va a deserializar carga de desencadenador de Hola.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

En JavaScript, automáticamente se realiza la deserialización de JSON y puede usar las propiedades de hello directamente.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Configuración de datos de enlace en tiempo de ejecución

En C# y otros lenguajes. NET, puede utilizar un patrón de enlace imperativo, como opuestos toohello enlaces declarativos en *function.json*. Enlace imperativa es útil cuando los parámetros de enlace necesitan toobe calcula en tiempo de ejecución en lugar de diseño. más información, consulte toolearn [enlace en tiempo de ejecución a través de enlaces imperativos](functions-reference-csharp.md#imperative-bindings) en referencia del programador de hello C#.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre un enlace específico, vea Hola siguientes artículos:

- [HTTP y webhooks](functions-bindings-http-webhook.md)
- [Temporizador](functions-bindings-timer.md)
- [Queue Storage](functions-bindings-storage-queue.md)
- [Blob Storage](functions-bindings-storage-blob.md)
- [Table storage](functions-bindings-storage-table.md)
- [Event Hubs](functions-bindings-event-hubs.md)
- [Bus de servicio](functions-bindings-service-bus.md)
- [Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Notification Hubs](functions-bindings-notification-hubs.md)
- [Mobile Apps](functions-bindings-mobile-apps.md)
- [Archivo externo](functions-bindings-external-file.md)
