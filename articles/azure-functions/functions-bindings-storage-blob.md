---
title: enlaces de almacenamiento de blobs de funciones aaaAzure | Documentos de Microsoft
description: "Comprender cómo se desencadena toouse almacenamiento de Azure y los enlaces de funciones de Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Enlaces de Blob Storage en Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se explica cómo tooconfigure y trabajar con enlaces de almacenamiento de blobs de Azure en las funciones de Azure. Azure Functions admite desencadenador y enlaces de entrada y salida para Azure Blob Storage. Para las características que estén disponibles en todos los enlaces, consulte [conceptos sobre desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> No se admite una [cuenta de almacenamiento solo de blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts). Los desencadenadores y enlaces de Blob Storage necesitan una cuenta de almacenamiento de uso general. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Desencadenadores y enlaces de Blob Storage

Usar desencadenador de almacenamiento de blobs de Azure hello, el código de la función se llama cuando se detecta un blob nuevo o actualizado. contenido de blob de Hola se proporciona como función de entrada toohello.

Definir un desencadenador de almacenamiento de blob mediante hello **integrar** Hola funciones portal de. portal de Hello crea Hola después de la definición de hello **enlaces** sección de *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

BLOB de entrada y salida enlaces se definen mediante `blob` como tipo de enlace de hello:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Hola `path` admite la propiedad de enlace expresiones y parámetros de filtro. Consulte [Patrones de nombre](#pattern).
* Hola `connection` propiedad debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento. Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de aplicación para cuando se selecciona una cuenta de almacenamiento.

> [!NOTE]
> Cuando se usa un desencadenador de blob en un plan de consumo, puede haber una demora de 10 minutos de tooa en el procesamiento de nuevos blobs después de una aplicación de la función ha quedado inactiva. Después de que se ejecuta la aplicación de la función de hello, blobs se procesan inmediatamente. tooavoid inicial este retraso, considere una de las siguientes opciones de hello:
> - Usar un plan de App Service con Always On habilitado
> - Utilice otro blob de hello tootrigger mecanismo de procesamiento, por ejemplo, un mensaje de la cola que contiene el nombre del blob Hola. Para ver un ejemplo, consulte [desencadenador de cola con enlace de entrada de blob](#input-sample).

<a name="pattern"></a>

### <a name="name-patterns"></a>Patrones de nombre
Puede especificar un patrón de nombre de blob en hello `path` propiedad, que puede ser una expresión de filtro o enlace. Consulte [Patrones y expresiones de enlace](functions-triggers-bindings.md#binding-expressions-and-patterns).

Por ejemplo, tooblobs toofilter que comienzan con hello cadena "original," usar hello después de la definición. Esta ruta de acceso busca un blob denominado *original Blob1.txt* en hello *entrada* contenedor y el valor de Hola de hello `name` la variable en el código de la función es `Blob1`.

```json
"path": "input/original-{name}",
```

extensión y nombre de archivo de blob de toobind toohello por separado, utilizan dos patrones. Esta ruta de acceso también busca un blob denominado *original Blob1.txt*y el valor de Hola de hello `blobname` y `blobextension` las variables en el código de función son *original Blob1* y *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

Puede restringir el tipo de archivo de Hola de blobs mediante el uso de un valor fijo para la extensión de archivo Hola. Por ejemplo, tootrigger solo en los archivos .png, Hola de uso siguiente patrón:

```json
"path": "samples/{name}.png",
```

Las llaves son caracteres especiales en los patrones de nombre. nombres de blob de toospecify que tienen las llaves en nombre de hello, puede omitir llaves hello mediante dos llaves. Hello en el ejemplo siguiente se busca un blob denominado *{20140101}-soundfile.mp3* en hello *imágenes* hello y contenedor `name` es el valor de la variable en el código de la función hello  *soundfile.mp3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Metadatos de desencadenador

desencadenador de blob de Hello proporciona varias propiedades de metadatos. Estas propiedades pueden usarse como parte de expresiones de enlace en otros enlaces o como parámetros del código. Estos valores no tienen Hola misma semántica que [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. Escriba `string`. ruta de acceso de blob desencadenadora Hola
- **Uri**. Escriba `System.Uri`. URI del blob de Hello para la ubicación principal Hola.
- **Properties**. Escriba `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`. Hola propiedades del sistema del blob.
- **Metadata**. Escriba `IDictionary<string,string>`. Hola metadatos definidos por el usuario para blob Hola.

<a name="receipts"></a>

### <a name="blob-receipts"></a>Recepciones de blobs
en tiempo de ejecución garantiza que ninguna función de desencadenador de blob se llama más de una vez para las funciones de Azure de Hola Hola mismo blob nuevo o actualizado. toodetermine si se ha procesado una versión determinada de blob, mantiene *blob confirmaciones*.

Almacenes de funciones de Azure blob confirmaciones en un contenedor denominado *hosts de webjobs de azure* Hola cuenta de almacenamiento de Azure para la aplicación de función (definida por la configuración de la aplicación hello `AzureWebJobsStorage`). Una confirmación de blob tiene Hola siguiente información:

* Hola desencadenó función ("*&lt;nombre de la aplicación de función >*. Las funciones.  *&lt;nombre de función >*", por ejemplo:"MyFunctionApp.Functions.CopyBlob")
* nombre del contenedor de Hola
* tipo de blob de Hello ("BlockBlob" o "PageBlob")
* nombre del blob Hola
* Hola ETag (un identificador de versión de blob, por ejemplo: "0x8D1DC6E70A277EF")

tooforce reprocesamiento de un blob, eliminar la confirmación de blob de Hola para ese blob de hello *hosts de webjobs de azure* contenedor manualmente.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Control de blobs dudosos
Si se produce un error en una función de desencadenador de blob, Azure Functions vuelve a intentar ejecutar esa función hasta 5 veces de forma predeterminada. 

Si se produce un error en todos los intentos de 5, las funciones de Azure agrega una cola de almacenamiento de tooa mensaje denominada *webjobs-blobtrigger-dudosos*. mensaje de la cola de Hola para blobs dudosos es un objeto JSON que contiene Hola propiedades siguientes:

* FunctionId (en formato de hello  *&lt;nombre de la aplicación de función >*. Las funciones.  *&lt;nombre de función >*)
* BlobType ("BlockBlob" o "PageBlob")
* ContainerName
* BlobName
* ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")

### <a name="blob-polling-for-large-containers"></a>Sondeo de blobs en contenedores grandes
Si el contenedor de blobs de Hola que se está supervisando contiene más de 10.000 blobs, funciones de hello en tiempo de ejecución examina inicie sesión toowatch de archivos para blobs nuevos o modificados. Este proceso no se lleva a cabo en tiempo real. Una función podría no obtener activada hasta varios minutos o más una vez creado el blob de Hola. Además, [se crean registros de almacenamiento basados en el principio del "mejor esfuerzo"](/rest/api/storageservices/About-Storage-Analytics-Logging). No hay ninguna garantía de que todos los eventos se capturen. En algunos casos, podrían faltar registros. Si necesita procesamiento de blob más rápida y confiable, considere la posibilidad de crear un [la cola de mensajes](../storage/queues/storage-dotnet-how-to-use-queues.md) cuando creas blob Hola. A continuación, utilice un [desencadenador cola](functions-bindings-storage-queue.md) en lugar de un blob de hello blob tooprocess de desencadenador.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Uso de un desencadenador de blob y un enlace de entrada
En las funciones. NET, tener acceso a datos de blob de hello mediante un parámetro de método como `Stream paramName`. En este caso, `paramName` es valor Hola especificado en hello [configuración de desencadenador](#trigger). En las funciones de Node.js, Hola de acceso de entrada de datos blob mediante `context.bindings.<name>`.

En. NET, puede enlazar tooany de tipos de hello en la siguiente lista de Hola. Si se usan como enlace de entrada, algunos de estos tipos necesitan una dirección de enlace `inout` en *function.json*. Esta dirección no es compatible con editor estándar de hello, por lo que debe usar Hola advanced editor.

* `TextReader`
* `Stream`
* `ICloudBlob` (necesita una dirección de enlace "inout")
* `CloudBlockBlob` (necesita una dirección de enlace "inout")
* `CloudPageBlob` (necesita una dirección de enlace "inout")
* `CloudAppendBlob` (necesita una dirección de enlace "inout")

Si se esperan que los blobs de texto, también puede enlazar tooa .NET `string` tipo. Esto solamente se recomienda si el tamaño del blob de hello es pequeño, como contenido de blob completo Hola se carga en memoria. Por lo general, es preferible toouse una `Stream` o `CloudBlockBlob` tipo.

## <a name="trigger-sample"></a>Ejemplo de desencadenador
Suponga que tiene Hola sigue function.json que define un desencadenador de almacenamiento de blobs:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

Vea el ejemplo de específica del lenguaje de Hola que registra el contenido de Hola de cada blob que se agrega toohello supervisado contenedor.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>Ejemplos de desencadenador de blobs en C# #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Ejemplo de desencadenador en Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Uso de un enlace de salida de blob

En las funciones. NET, debe utilizar un `out string` parámetro en la firma de la función o usar uno de los tipos de Hola Hola lista siguiente. En las funciones de Node.js, accederás a Hola salida blob mediante `context.bindings.<name>`.

En las funciones de .NET puede producir tooany de hello siguientes tipos:

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Ejemplo de desencadenador de cola con entrada y salida de blob
Suponga que tiene Hola después function.json, que define un [desencadenador de almacenamiento de cola](functions-bindings-storage-queue.md), un almacenamiento de blobs de entrada y salida de un almacenamiento de blobs. Uso de Hola de aviso de hello `queueTrigger` propiedad de metadatos. Hola BLOB de entrada y salida `path` propiedades:

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

Vea el ejemplo de específica del lenguaje de Hola que copia Hola blob de entrada toohello salida blob.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>Ejemplo de enlace de blob en C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Ejemplo de enlace de blob en Node.js

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

