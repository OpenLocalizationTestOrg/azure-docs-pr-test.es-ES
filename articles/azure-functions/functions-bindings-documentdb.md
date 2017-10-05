---
title: Enlaces de Cosmos DB en Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar enlaces de Cosmos DB en Azure Functions."
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
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="3a94b-104">Enlaces de Cosmos DB en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3a94b-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="3a94b-105">En este artículo se explica cómo configurar y programar enlaces de Azure Cosmos DB en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3a94b-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="3a94b-106">Azure Functions admite enlaces de entrada y salida para Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3a94b-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="3a94b-107">Para más información sobre Cosmos DB, consulte [Introducción a Cosmos DB](../documentdb/documentdb-introduction.md) y [Compilación de una aplicación de consola de Cosmos DB](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3a94b-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="3a94b-108">Enlace de entrada de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3a94b-108">DocumentDB API input binding</span></span>
<span data-ttu-id="3a94b-109">El enlace de entrada de API de DocumentDB recupera un documento de Cosmos DB y lo pasa al parámetro de entrada con nombre de la función.</span><span class="sxs-lookup"><span data-stu-id="3a94b-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="3a94b-110">Se puede determinar el identificador de documento según el desencadenador que invoca la función.</span><span class="sxs-lookup"><span data-stu-id="3a94b-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="3a94b-111">El enlace de entrada de API de DocumentDB tiene las siguientes propiedades en *function.json*:</span><span class="sxs-lookup"><span data-stu-id="3a94b-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="3a94b-112">`name`: nombre del identificador que se usa en el código de la función para el documento</span><span class="sxs-lookup"><span data-stu-id="3a94b-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="3a94b-113">`type`: se debe establecer en "documentdb"</span><span class="sxs-lookup"><span data-stu-id="3a94b-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="3a94b-114">`databaseName`: base de datos que contiene el documento</span><span class="sxs-lookup"><span data-stu-id="3a94b-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="3a94b-115">`collectionName`: colección que contiene el documento</span><span class="sxs-lookup"><span data-stu-id="3a94b-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="3a94b-116">`id` : el identificador del documento que se debe recuperar.</span><span class="sxs-lookup"><span data-stu-id="3a94b-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="3a94b-117">Esta propiedad admite parámetros de enlaces; vea [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) (Enlace a propiedades de entrada personalizadas en una expresión de enlace) en el artículo [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md) (Conceptos básicos sobre los enlaces y desencadenadores de Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="3a94b-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="3a94b-118">`sqlQuery`: consulta SQL de Cosmos DB que se usa para recuperar varios documentos.</span><span class="sxs-lookup"><span data-stu-id="3a94b-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="3a94b-119">La consulta admite enlaces en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3a94b-119">The query supports runtime bindings.</span></span> <span data-ttu-id="3a94b-120">Por ejemplo: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="3a94b-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="3a94b-121">`connection`: nombre de la configuración de aplicación que contiene la cadena de conexión de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3a94b-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="3a94b-122">`direction`: se debe establecer en `"in"`.</span><span class="sxs-lookup"><span data-stu-id="3a94b-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="3a94b-123">No se pueden establecer las propiedades `id` y `sqlQuery` al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="3a94b-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="3a94b-124">Si no están establecidas `id` ni `sqlQuery`, se recupera toda la colección.</span><span class="sxs-lookup"><span data-stu-id="3a94b-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="3a94b-125">Uso de un enlace de entrada de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3a94b-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="3a94b-126">En las funciones de C# y F#, cuando se sale de la función correctamente, los cambios realizados en el documento de entrada mediante parámetros de entrada con nombre se guardan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3a94b-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="3a94b-127">En las funciones de JavaScript, las actualizaciones no se realizan automáticamente al cerrar la función.</span><span class="sxs-lookup"><span data-stu-id="3a94b-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="3a94b-128">Por el contrario, use `context.bindings.<documentName>In` y `context.bindings.<documentName>Out` para realizar las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="3a94b-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="3a94b-129">Vea el [ejemplo de JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="3a94b-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="3a94b-130">Ejemplo de entrada de documento único</span><span class="sxs-lookup"><span data-stu-id="3a94b-130">Input sample for single document</span></span>
<span data-ttu-id="3a94b-131">Suponga que tiene el siguiente enlace de entrada de API de DocumentDB en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="3a94b-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="3a94b-132">Vea el ejemplo específico del idioma que utiliza este enlace de entrada para actualizar el valor de texto del documento.</span><span class="sxs-lookup"><span data-stu-id="3a94b-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="3a94b-133">C#</span><span class="sxs-lookup"><span data-stu-id="3a94b-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="3a94b-134">F#</span><span class="sxs-lookup"><span data-stu-id="3a94b-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="3a94b-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a94b-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="3a94b-136">Ejemplo de entrada en C#</span><span class="sxs-lookup"><span data-stu-id="3a94b-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="3a94b-137">Ejemplo de entrada en F#</span><span class="sxs-lookup"><span data-stu-id="3a94b-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="3a94b-138">Este ejemplo necesita un archivo `project.json` que especifique las dependencias de NuGet `FSharp.Interop.Dynamic` y `Dynamitey`:</span><span class="sxs-lookup"><span data-stu-id="3a94b-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="3a94b-139">Para agregar un archivo `project.json`, consulte la [administración de paquetes de F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="3a94b-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="3a94b-140">Ejemplo de entrada en JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a94b-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="3a94b-141">Ejemplo de entrada con varios documentos</span><span class="sxs-lookup"><span data-stu-id="3a94b-141">Input sample with multiple documents</span></span>

<span data-ttu-id="3a94b-142">Imagine que quiere recuperar varios documentos especificados por una consulta SQL con un desencadenador de cola para personalizar los parámetros de la consulta.</span><span class="sxs-lookup"><span data-stu-id="3a94b-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="3a94b-143">En este ejemplo, el desencadenador de cola proporciona un parámetro `departmentId`. Un mensaje de cola de `{ "departmentId" : "Finance" }` devolvería todos los registros del departamento de finanzas.</span><span class="sxs-lookup"><span data-stu-id="3a94b-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="3a94b-144">Use lo siguiente en *function.json*:</span><span class="sxs-lookup"><span data-stu-id="3a94b-144">Use the following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="3a94b-145">Ejemplo de entrada con varios documentos en C#</span><span class="sxs-lookup"><span data-stu-id="3a94b-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="3a94b-146">Ejemplo de entrada con varios documentos en JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a94b-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="3a94b-147"><a id="docdboutput"></a>Enlace de salida de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3a94b-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="3a94b-148">El enlace de salida de API de DocumentDB permite escribir un nuevo documento en una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3a94b-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="3a94b-149">Tiene las siguientes propiedades en *function.json*:</span><span class="sxs-lookup"><span data-stu-id="3a94b-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="3a94b-150">`name`: identificador que se usa en el código de la función para el nuevo documento</span><span class="sxs-lookup"><span data-stu-id="3a94b-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="3a94b-151">`type`: se debe establecer en `"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="3a94b-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="3a94b-152">`databaseName` : la base de datos que contiene la colección en la que se creará el nuevo documento.</span><span class="sxs-lookup"><span data-stu-id="3a94b-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="3a94b-153">`collectionName` : la colección en la que se creará el nuevo documento.</span><span class="sxs-lookup"><span data-stu-id="3a94b-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="3a94b-154">`createIfNotExists`: valor booleano que indica si la colección se creará si no existe.</span><span class="sxs-lookup"><span data-stu-id="3a94b-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="3a94b-155">El valor predeterminado es *false*.</span><span class="sxs-lookup"><span data-stu-id="3a94b-155">The default is *false*.</span></span> <span data-ttu-id="3a94b-156">Esto se debe a que se crean nuevas colecciones con rendimiento reservado, lo cual tiene implicaciones de precios.</span><span class="sxs-lookup"><span data-stu-id="3a94b-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="3a94b-157">Para obtener más información, visite la [página de precios](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="3a94b-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="3a94b-158">`connection`: nombre de la configuración de aplicación que contiene la cadena de conexión de Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3a94b-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="3a94b-159">`direction`: se debe establecer en `"out"`</span><span class="sxs-lookup"><span data-stu-id="3a94b-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="3a94b-160">Uso de un enlace de salida de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3a94b-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="3a94b-161">En esta sección se muestra cómo utilizar el enlace de salida de API de DocumentDB en el código de función.</span><span class="sxs-lookup"><span data-stu-id="3a94b-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="3a94b-162">Cuando se escribe en el parámetro de salida en la función, de forma predeterminada se genera un nuevo documento en la base de datos, con un GUID generado automáticamente como el identificador de documento.</span><span class="sxs-lookup"><span data-stu-id="3a94b-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="3a94b-163">Puede especificar el identificador de documento del documento de salida mediante la especificación de la propiedad JSON `id` en el parámetro de salida.</span><span class="sxs-lookup"><span data-stu-id="3a94b-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="3a94b-164">Cuando especifica el identificador de un documento existente, se sobrescribe con el nuevo documento de salida.</span><span class="sxs-lookup"><span data-stu-id="3a94b-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="3a94b-165">Para generar varios documentos, también puede enlazar a `ICollector<T>` o `IAsyncCollector<T>`, donde `T` es uno de los tipos admitidos.</span><span class="sxs-lookup"><span data-stu-id="3a94b-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="3a94b-166">Ejemplo de enlace de salida de API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3a94b-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="3a94b-167">Suponga que tiene el siguiente enlace de salida de API de DocumentDB en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="3a94b-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="3a94b-168">Y tienen un enlace de entrada de cola para una cola que recibe JSON en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="3a94b-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="3a94b-169">Y desea crear documentos de Cosmos DB en el formato siguiente para cada registro:</span><span class="sxs-lookup"><span data-stu-id="3a94b-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="3a94b-170">Vea el ejemplo específico del idioma que utiliza este enlace de salida para agregar documentos a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="3a94b-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="3a94b-171">C#</span><span class="sxs-lookup"><span data-stu-id="3a94b-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="3a94b-172">F#</span><span class="sxs-lookup"><span data-stu-id="3a94b-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="3a94b-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a94b-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="3a94b-174">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="3a94b-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="3a94b-175">Ejemplo de salida en F#</span><span class="sxs-lookup"><span data-stu-id="3a94b-175">Output sample in F#</span></span> #

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

<span data-ttu-id="3a94b-176">Este ejemplo necesita un archivo `project.json` que especifique las dependencias de NuGet `FSharp.Interop.Dynamic` y `Dynamitey`:</span><span class="sxs-lookup"><span data-stu-id="3a94b-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="3a94b-177">Para agregar un archivo `project.json`, consulte la [administración de paquetes de F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="3a94b-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="3a94b-178">Ejemplo de salida en JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a94b-178">Output sample in JavaScript</span></span>

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
