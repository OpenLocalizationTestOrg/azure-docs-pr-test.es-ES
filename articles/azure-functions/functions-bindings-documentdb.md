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
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="f762e-104">Enlaces de Cosmos DB en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f762e-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="f762e-105">Este artículo se explica cómo enlaces de base de datos de Azure Cosmos tooconfigure y código en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f762e-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="f762e-106">Azure Functions admite enlaces de entrada y salida para Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f762e-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="f762e-107">Para obtener más información sobre la base de datos de Cosmos, consulte [Introducción tooCosmos DB](../documentdb/documentdb-introduction.md) y [compilar una aplicación de consola de base de datos de Cosmos](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f762e-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="f762e-108">Enlace de entrada de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f762e-108">DocumentDB API input binding</span></span>
<span data-ttu-id="f762e-109">Recupera un documento de la base de datos de Cosmos Hola enlace de entrada de API de documentos y la pasa toohello con el nombre de parámetro de entrada de función hello.</span><span class="sxs-lookup"><span data-stu-id="f762e-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="f762e-110">se puede determinar el identificador de documento de Hello basado en desencadenador de Hola que invoca la función hello.</span><span class="sxs-lookup"><span data-stu-id="f762e-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="f762e-111">Hola enlace de entrada de API de documentos tiene Hola propiedades en siguientes *function.json*:</span><span class="sxs-lookup"><span data-stu-id="f762e-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="f762e-112">`name`: Nombre identificador utilizado en el código de función para el documento de Hola</span><span class="sxs-lookup"><span data-stu-id="f762e-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="f762e-113">`type`: se debe establecer demasiado "documentos"</span><span class="sxs-lookup"><span data-stu-id="f762e-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="f762e-114">`databaseName`: base de datos de Hola que contiene el documento de Hola</span><span class="sxs-lookup"><span data-stu-id="f762e-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="f762e-115">`collectionName`: colección de Hola que contiene el documento de Hola</span><span class="sxs-lookup"><span data-stu-id="f762e-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="f762e-116">`id`: Hola Id. de hello documento tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="f762e-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="f762e-117">Esta propiedad es compatible con parámetros de enlaces; vea [enlazar las propiedades de entrada toocustom en una expresión de enlace](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) en el artículo hello [desencadenadores de las funciones de Azure y conceptos de enlaces](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="f762e-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="f762e-118">`sqlQuery`: consulta SQL de Cosmos DB que se usa para recuperar varios documentos.</span><span class="sxs-lookup"><span data-stu-id="f762e-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="f762e-119">consulta de Hello admite enlaces en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f762e-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="f762e-120">Por ejemplo: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="f762e-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="f762e-121">`connection`: nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de base de datos de Cosmos</span><span class="sxs-lookup"><span data-stu-id="f762e-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="f762e-122">`direction`: se debe establecer demasiado`"in"`.</span><span class="sxs-lookup"><span data-stu-id="f762e-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="f762e-123">Hola propiedades `id` y `sqlQuery` no pueden especificarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="f762e-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="f762e-124">Si no `id` ni `sqlQuery` está establecida, hello todo se recupera la colección.</span><span class="sxs-lookup"><span data-stu-id="f762e-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="f762e-125">Uso de un enlace de entrada de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f762e-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="f762e-126">En C# y F # funciones, cuando finaliza correctamente, la función de Hola se conserva automáticamente cualquier cambio realizado toohello documento de entrada a través de los parámetros de entrada con nombre.</span><span class="sxs-lookup"><span data-stu-id="f762e-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="f762e-127">En las funciones de JavaScript, las actualizaciones no se realizan automáticamente al cerrar la función.</span><span class="sxs-lookup"><span data-stu-id="f762e-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="f762e-128">En su lugar, use `context.bindings.<documentName>In` y `context.bindings.<documentName>Out` toomake actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="f762e-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="f762e-129">Vea hello [ejemplo JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="f762e-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="f762e-130">Ejemplo de entrada de documento único</span><span class="sxs-lookup"><span data-stu-id="f762e-130">Input sample for single document</span></span>
<span data-ttu-id="f762e-131">Imagine que tiene Hola siguientes API de documentos de entrada enlace Hola `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="f762e-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="f762e-132">Vea ejemplo de Hola a específicos del idioma que utiliza el valor de texto de enlace de entrada tooupdate Hola de este documento.</span><span class="sxs-lookup"><span data-stu-id="f762e-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="f762e-133">C#</span><span class="sxs-lookup"><span data-stu-id="f762e-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="f762e-134">F#</span><span class="sxs-lookup"><span data-stu-id="f762e-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="f762e-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f762e-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="f762e-136">Ejemplo de entrada en C#</span><span class="sxs-lookup"><span data-stu-id="f762e-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="f762e-137">Ejemplo de entrada en F#</span><span class="sxs-lookup"><span data-stu-id="f762e-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="f762e-138">Este ejemplo requiere un `project.json` archivo que especifica hello `FSharp.Interop.Dynamic` y `Dynamitey` las dependencias de NuGet:</span><span class="sxs-lookup"><span data-stu-id="f762e-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="f762e-139">tooadd una `project.json` de archivos, consulte [administración de paquetes de F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="f762e-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="f762e-140">Ejemplo de entrada en JavaScript</span><span class="sxs-lookup"><span data-stu-id="f762e-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="f762e-141">Ejemplo de entrada con varios documentos</span><span class="sxs-lookup"><span data-stu-id="f762e-141">Input sample with multiple documents</span></span>

<span data-ttu-id="f762e-142">Suponga que desea tooretrieve varios documentos especificados por una consulta SQL, utilizando un parámetros de consulta de cola desencadenador toocustomize Hola.</span><span class="sxs-lookup"><span data-stu-id="f762e-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="f762e-143">En este ejemplo, el desencadenador de la cola de hello proporciona un parámetro `departmentId`. Un mensaje de la cola de `{ "departmentId" : "Finance" }` devolverá todos los registros para el departamento de finanzas Hola.</span><span class="sxs-lookup"><span data-stu-id="f762e-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="f762e-144">Utilizar siguiente hello en *function.json*:</span><span class="sxs-lookup"><span data-stu-id="f762e-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="f762e-145">Ejemplo de entrada con varios documentos en C#</span><span class="sxs-lookup"><span data-stu-id="f762e-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="f762e-146">Ejemplo de entrada con varios documentos en JavaScript</span><span class="sxs-lookup"><span data-stu-id="f762e-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="f762e-147"><a id="docdboutput"></a>Enlace de salida de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f762e-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="f762e-148">Hola API de documentos de salida enlace le permite escribir una base de datos de base de datos de Azure Cosmos de tooan documento nuevo.</span><span class="sxs-lookup"><span data-stu-id="f762e-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="f762e-149">Tiene Hola propiedades en siguientes *function.json*:</span><span class="sxs-lookup"><span data-stu-id="f762e-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="f762e-150">`name`: Identificador utilizado en el código de función para el nuevo documento de Hola</span><span class="sxs-lookup"><span data-stu-id="f762e-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="f762e-151">`type`: se debe establecer demasiado`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="f762e-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="f762e-152">`databaseName`: base de datos de Hola que contiene la colección de Hola donde se creará el nuevo documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f762e-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="f762e-153">`collectionName`: Hola colección donde se creará el nuevo documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f762e-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="f762e-154">`createIfNotExists`: Un valor booleano tooindicate si la colección de Hola se creará si no existe.</span><span class="sxs-lookup"><span data-stu-id="f762e-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="f762e-155">valor predeterminado de Hello es *false*.</span><span class="sxs-lookup"><span data-stu-id="f762e-155">hello default is *false*.</span></span> <span data-ttu-id="f762e-156">Hola razón para esto es una novedad colecciones se crean con un rendimiento reservado, lo que tiene implicaciones de precios.</span><span class="sxs-lookup"><span data-stu-id="f762e-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="f762e-157">Para obtener más detalles, visite hello [página de precios](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f762e-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="f762e-158">`connection`: nombre de Hola de configuración de la aplicación hello que contiene la cadena de conexión de base de datos de Cosmos</span><span class="sxs-lookup"><span data-stu-id="f762e-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="f762e-159">`direction`: se debe establecer demasiado`"out"`</span><span class="sxs-lookup"><span data-stu-id="f762e-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="f762e-160">Uso de un enlace de salida de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f762e-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="f762e-161">Esta sección muestra cómo toouse su API de documentos de salida en el código de función de enlace.</span><span class="sxs-lookup"><span data-stu-id="f762e-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="f762e-162">Cuando se escribe toohello parámetro de salida en la función, que se genera un nuevo documento en la base de datos de forma predeterminada, con un GUID generado automáticamente como Hola documentar identificador.</span><span class="sxs-lookup"><span data-stu-id="f762e-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="f762e-163">Puede especificar Hola Id. de documento del documento de salida mediante la especificación de hello `id` parámetro de salida de la propiedad JSON en Hola.</span><span class="sxs-lookup"><span data-stu-id="f762e-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="f762e-164">Cuando se especifica el Id. de Hola de un documento existente, se sobrescribe por documento de salida nuevo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f762e-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="f762e-165">toooutput varios documentos, también puede enlazar demasiado`ICollector<T>` o `IAsyncCollector<T>` donde `T` es uno de los tipos de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="f762e-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="f762e-166">Ejemplo de enlace de salida de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f762e-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="f762e-167">Imagine que tiene Hola siguientes API de documentos de salida enlace Hola `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="f762e-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="f762e-168">Y tienen un enlace de entrada de cola a una cola que recibe de JSON en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="f762e-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="f762e-169">Y desea que los documentos de base de datos de Cosmos toocreate Hola siguiendo el formato para cada registro:</span><span class="sxs-lookup"><span data-stu-id="f762e-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="f762e-170">Vea ejemplo de Hola a específicos del idioma que utiliza esta salida enlace tooadd documentos tooyour base de datos.</span><span class="sxs-lookup"><span data-stu-id="f762e-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="f762e-171">C#</span><span class="sxs-lookup"><span data-stu-id="f762e-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="f762e-172">F#</span><span class="sxs-lookup"><span data-stu-id="f762e-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="f762e-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f762e-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="f762e-174">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="f762e-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="f762e-175">Ejemplo de salida en F#</span><span class="sxs-lookup"><span data-stu-id="f762e-175">Output sample in F#</span></span> #

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

<span data-ttu-id="f762e-176">Este ejemplo requiere un `project.json` archivo que especifica hello `FSharp.Interop.Dynamic` y `Dynamitey` las dependencias de NuGet:</span><span class="sxs-lookup"><span data-stu-id="f762e-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="f762e-177">tooadd una `project.json` de archivos, consulte [administración de paquetes de F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="f762e-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="f762e-178">Ejemplo de salida en JavaScript</span><span class="sxs-lookup"><span data-stu-id="f762e-178">Output sample in JavaScript</span></span>

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
