---
title: enlaces de funciones Cosmos DB aaaAzure | Documentos de Microsoft
description: "Comprender cómo los enlaces de base de datos de Azure Cosmos toouse de funciones de Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a>Enlaces de Cosmos DB en Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se explica cómo enlaces de base de datos de Azure Cosmos tooconfigure y código en las funciones de Azure. Azure Functions admite enlaces de entrada y salida para Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Para obtener más información sobre la base de datos de Cosmos, consulte [Introducción tooCosmos DB](../documentdb/documentdb-introduction.md) y [compilar una aplicación de consola de base de datos de Cosmos](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>Enlace de entrada de API de DocumentDB
Recupera un documento de la base de datos de Cosmos Hola enlace de entrada de API de documentos y la pasa toohello con el nombre de parámetro de entrada de función hello. se puede determinar el identificador de documento de Hello basado en desencadenador de Hola que invoca la función hello. 

Hola enlace de entrada de API de documentos tiene Hola propiedades en siguientes *function.json*:

- `name`: Nombre identificador utilizado en el código de función para el documento de Hola
- `type`: se debe establecer demasiado "documentos"
- `databaseName`: base de datos de Hola que contiene el documento de Hola
- `collectionName`: colección de Hola que contiene el documento de Hola
- `id`: Hola Id. de hello documento tooretrieve. Esta propiedad es compatible con parámetros de enlaces; vea [enlazar las propiedades de entrada toocustom en una expresión de enlace](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) en el artículo hello [desencadenadores de las funciones de Azure y conceptos de enlaces](functions-triggers-bindings.md).
- `sqlQuery`: consulta SQL de Cosmos DB que se usa para recuperar varios documentos. consulta de Hello admite enlaces en tiempo de ejecución. Por ejemplo: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de base de datos de Cosmos
- `direction`: se debe establecer demasiado`"in"`.

Hola propiedades `id` y `sqlQuery` no pueden especificarse simultáneamente. Si no `id` ni `sqlQuery` está establecida, hello todo se recupera la colección.

## <a name="using-a-documentdb-api-input-binding"></a>Uso de un enlace de entrada de API de DocumentDB

* En C# y F # funciones, cuando finaliza correctamente, la función de Hola se conserva automáticamente cualquier cambio realizado toohello documento de entrada a través de los parámetros de entrada con nombre. 
* En las funciones de JavaScript, las actualizaciones no se realizan automáticamente al cerrar la función. En su lugar, use `context.bindings.<documentName>In` y `context.bindings.<documentName>Out` toomake actualizaciones. Vea hello [ejemplo JavaScript](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Ejemplo de entrada de documento único
Imagine que tiene Hola siguientes API de documentos de entrada enlace Hola `bindings` matriz de function.json:

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

Vea ejemplo de Hola a específicos del idioma que utiliza el valor de texto de enlace de entrada tooupdate Hola de este documento.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Ejemplo de entrada en C# #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Ejemplo de entrada en F# #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

Este ejemplo requiere un `project.json` archivo que especifica hello `FSharp.Interop.Dynamic` y `Dynamitey` las dependencias de NuGet:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

tooadd una `project.json` de archivos, consulte [administración de paquetes de F #](functions-reference-fsharp.md#package).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>Ejemplo de entrada en JavaScript

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Ejemplo de entrada con varios documentos

Suponga que desea tooretrieve varios documentos especificados por una consulta SQL, utilizando un parámetros de consulta de cola desencadenador toocustomize Hola. 

En este ejemplo, el desencadenador de la cola de hello proporciona un parámetro `departmentId`. Un mensaje de la cola de `{ "departmentId" : "Finance" }` devolverá todos los registros para el departamento de finanzas Hola. Utilizar siguiente hello en *function.json*:

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a>Ejemplo de entrada con varios documentos en C#

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a>Ejemplo de entrada con varios documentos en JavaScript

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <a id="docdboutput"></a>Enlace de salida de API de DocumentDB
Hola API de documentos de salida enlace le permite escribir una base de datos de base de datos de Azure Cosmos de tooan documento nuevo. Tiene Hola propiedades en siguientes *function.json*:

- `name`: Identificador utilizado en el código de función para el nuevo documento de Hola
- `type`: se debe establecer demasiado`"documentdb"`
- `databaseName`: base de datos de Hola que contiene la colección de Hola donde se creará el nuevo documento de Hola.
- `collectionName`: Hola colección donde se creará el nuevo documento de Hola.
- `createIfNotExists`: Un valor booleano tooindicate si la colección de Hola se creará si no existe. valor predeterminado de Hello es *false*. Hola razón para esto es una novedad colecciones se crean con un rendimiento reservado, lo que tiene implicaciones de precios. Para obtener más detalles, visite hello [página de precios](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de base de datos de Cosmos
- `direction`: se debe establecer demasiado`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Uso de un enlace de salida de API de DocumentDB
Esta sección muestra cómo toouse su API de documentos de salida en el código de función de enlace.

Cuando se escribe toohello parámetro de salida en la función, que se genera un nuevo documento en la base de datos de forma predeterminada, con un GUID generado automáticamente como Hola documentar identificador. Puede especificar Hola Id. de documento del documento de salida mediante la especificación de hello `id` parámetro de salida de la propiedad JSON en Hola. 

>[!Note]  
>Cuando se especifica el Id. de Hola de un documento existente, se sobrescribe por documento de salida nuevo de Hola. 

toooutput varios documentos, también puede enlazar demasiado`ICollector<T>` o `IAsyncCollector<T>` donde `T` es uno de los tipos de hello compatible.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>Ejemplo de enlace de salida de API de DocumentDB
Imagine que tiene Hola siguientes API de documentos de salida enlace Hola `bindings` matriz de function.json:

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

Y tienen un enlace de entrada de cola a una cola que recibe de JSON en hello siguiendo el formato:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Y desea que los documentos de base de datos de Cosmos toocreate Hola siguiendo el formato para cada registro:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Vea ejemplo de Hola a específicos del idioma que utiliza esta salida enlace tooadd documentos tooyour base de datos.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Ejemplo de salida en C# #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Ejemplo de salida en F# #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

Este ejemplo requiere un `project.json` archivo que especifica hello `FSharp.Interop.Dynamic` y `Dynamitey` las dependencias de NuGet:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

tooadd una `project.json` de archivos, consulte [administración de paquetes de F #](functions-reference-fsharp.md#package).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>Ejemplo de salida en JavaScript

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
