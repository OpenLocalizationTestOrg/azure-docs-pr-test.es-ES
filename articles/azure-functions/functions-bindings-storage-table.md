---
title: Enlaces de tablas de Storage en Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar los enlaces de Azure Storage en Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "funciones de azure, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="04ad3-104">Enlaces de tablas de Storage en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="04ad3-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="04ad3-105">En este artículo, se explica cómo configurar y codificar enlaces de tablas de Azure Storage en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="04ad3-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="04ad3-106">Azure Functions admite enlaces de entrada y salida para tablas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="04ad3-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="04ad3-107">El enlace de tablas de Azure Storage admite los siguientes escenarios:</span><span class="sxs-lookup"><span data-stu-id="04ad3-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="04ad3-108">**Lectura de una sola fila de una función de C# o Node.js**. Establezca `partitionKey` y `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="04ad3-109">Las propiedades `filter` y `take` no se utilizan en este escenario.</span><span class="sxs-lookup"><span data-stu-id="04ad3-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="04ad3-110">**Lectura de varias filas de una función de C#**: el tiempo de ejecución de Functions proporciona un objeto `IQueryable<T>` enlazado a la tabla.</span><span class="sxs-lookup"><span data-stu-id="04ad3-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="04ad3-111">El tipo `T` debe derivar de `TableEntity` o implementar `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="04ad3-112">Las propiedades `partitionKey`, `rowKey`, `filter` y `take` no se utilizan en este escenario; puede utilizar el objeto `IQueryable` para realizar todo el filtrado requerido.</span><span class="sxs-lookup"><span data-stu-id="04ad3-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="04ad3-113">**Lectura de varias filas en una función de Node**. Establezca las propiedades `filter` y `take`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="04ad3-114">No establezca `partitionKey` o `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="04ad3-115">**Escritura de una o más filas en una función de C#**. El tiempo de ejecución de Functions proporciona un `ICollector<T>` o `IAsyncCollector<T>` enlazado a la tabla, donde `T` especifica el esquema de las entidades que desea agregar.</span><span class="sxs-lookup"><span data-stu-id="04ad3-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="04ad3-116">Normalmente, el tipo `T` deriva de `TableEntity` o implementa `ITableEntity`, pero no tiene por qué ser así.</span><span class="sxs-lookup"><span data-stu-id="04ad3-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="04ad3-117">Las propiedades `partitionKey`, `rowKey`, `filter` y `take` no se utilizan en este escenario.</span><span class="sxs-lookup"><span data-stu-id="04ad3-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="04ad3-118">Enlace de entrada de tabla de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="04ad3-118">Storage table input binding</span></span>
<span data-ttu-id="04ad3-119">El enlace de entrada de tabla de Azure Storage permite utilizar una tabla de almacenamiento en su función.</span><span class="sxs-lookup"><span data-stu-id="04ad3-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="04ad3-120">La entrada de tabla de Azure Storage a una función utiliza los siguientes objetos JSON en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="04ad3-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="04ad3-121">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04ad3-121">Note the following:</span></span> 

* <span data-ttu-id="04ad3-122">Use `partitionKey` y `rowKey` de forma conjunta para leer una entidad única.</span><span class="sxs-lookup"><span data-stu-id="04ad3-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="04ad3-123">Estas propiedades son opcionales.</span><span class="sxs-lookup"><span data-stu-id="04ad3-123">These properties are optional.</span></span> 
* <span data-ttu-id="04ad3-124">`connection`: debe contener el nombre de una configuración de aplicación que contiene una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="04ad3-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="04ad3-125">En Azure Portal, el editor estándar de la pestaña **Integrar** permite modificar esta configuración de aplicación cuando crea una cuenta de Azure Storage o selecciona una ya existente.</span><span class="sxs-lookup"><span data-stu-id="04ad3-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="04ad3-126">También puede [configurar esta aplicación manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="04ad3-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="04ad3-127">Uso de entradas</span><span class="sxs-lookup"><span data-stu-id="04ad3-127">Input usage</span></span>
<span data-ttu-id="04ad3-128">En las funciones de C#, enlaza con la entidad (o entidades) de la tabla de entradas mediante un parámetro con nombre en la firma de la función, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="04ad3-129">Donde `T` es el tipo de datos en el que desea deserializar los datos, y `paramName` es el nombre que especificó en el [enlace de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="04ad3-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="04ad3-130">En las funciones de Node.js, puede acceder a la entidad (o entidades) de la tabla de entradas mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="04ad3-131">Los datos de entrada se pueden deserializar en funciones de Node.js o C#.</span><span class="sxs-lookup"><span data-stu-id="04ad3-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="04ad3-132">Los objetos deserializados tienen las propiedades `RowKey` y `PartitionKey`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="04ad3-133">En las funciones de C#, también puede enlazar con cualquiera de los siguientes tipos y el tiempo de ejecución de Azure Functions intentará deserializar los datos de la tabla mediante ese tipo:</span><span class="sxs-lookup"><span data-stu-id="04ad3-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="04ad3-134">Cualquier tipo que implemente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="04ad3-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="04ad3-135">Ejemplo de entrada</span><span class="sxs-lookup"><span data-stu-id="04ad3-135">Input sample</span></span>
<span data-ttu-id="04ad3-136">Suponga que tiene el siguiente function.json que usa un desencadenador de cola para leer una única fila de tabla.</span><span class="sxs-lookup"><span data-stu-id="04ad3-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="04ad3-137">El archivo JSON especifica `PartitionKey` 
`RowKey`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="04ad3-138">`"rowKey": "{queueTrigger}"` indica que la clave de fila procede de la cadena del mensaje en la cola.</span><span class="sxs-lookup"><span data-stu-id="04ad3-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="04ad3-139">Consulte el ejemplo de lenguaje específico que lee una única entidad de tabla.</span><span class="sxs-lookup"><span data-stu-id="04ad3-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="04ad3-140">C#</span><span class="sxs-lookup"><span data-stu-id="04ad3-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="04ad3-141">F#</span><span class="sxs-lookup"><span data-stu-id="04ad3-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="04ad3-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="04ad3-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="04ad3-143">Ejemplo de entrada en C#</span><span class="sxs-lookup"><span data-stu-id="04ad3-143">Input sample in C#</span></span> #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="04ad3-144">Ejemplo de entrada en F#</span><span class="sxs-lookup"><span data-stu-id="04ad3-144">Input sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="04ad3-145">Ejemplo de entrada en Node.js</span><span class="sxs-lookup"><span data-stu-id="04ad3-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="04ad3-146">Enlace de salida de tabla de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="04ad3-146">Storage table output binding</span></span>
<span data-ttu-id="04ad3-147">El enlace de salida de tabla de Azure Storage le permite escribir entidades en una tabla de Azure Storage en su función.</span><span class="sxs-lookup"><span data-stu-id="04ad3-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="04ad3-148">La salida de tabla de Azure Storage para una función utiliza los siguientes objetos JSON en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="04ad3-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="04ad3-149">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="04ad3-149">Note the following:</span></span> 

* <span data-ttu-id="04ad3-150">Use `partitionKey` y `rowKey` de forma conjunta para escribir una entidad única.</span><span class="sxs-lookup"><span data-stu-id="04ad3-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="04ad3-151">Estas propiedades son opcionales.</span><span class="sxs-lookup"><span data-stu-id="04ad3-151">These properties are optional.</span></span> <span data-ttu-id="04ad3-152">También puede especificar `PartitionKey` y `RowKey` al crear los objetos de la entidad en el código de la función.</span><span class="sxs-lookup"><span data-stu-id="04ad3-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="04ad3-153">`connection`: debe contener el nombre de una configuración de aplicación que contiene una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="04ad3-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="04ad3-154">En Azure Portal, el editor estándar de la pestaña **Integrar** permite modificar esta configuración de aplicación cuando crea una cuenta de Azure Storage o selecciona una ya existente.</span><span class="sxs-lookup"><span data-stu-id="04ad3-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="04ad3-155">También puede [configurar esta aplicación manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="04ad3-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="04ad3-156">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="04ad3-156">Output usage</span></span>
<span data-ttu-id="04ad3-157">En las funciones de C#, puede enlazar a la salida de tabla mediante el parámetro con nombre `out` de la firma de la función, como `out <T> <name>`, donde `T` es el tipo de datos en el que desea serializar los datos y `paramName` es el nombre que especificó en el [enlace de salida](#output).</span><span class="sxs-lookup"><span data-stu-id="04ad3-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="04ad3-158">En las funciones de Node.js, puede acceder a la salida de tabla mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="04ad3-159">Puede serializar objetos en las funciones de Node.js o C#.</span><span class="sxs-lookup"><span data-stu-id="04ad3-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="04ad3-160">En las funciones de C#, también puede enlazar a los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="04ad3-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="04ad3-161">Cualquier tipo que implemente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="04ad3-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="04ad3-162">`ICollector<T>` (para la salida de varias entidades.</span><span class="sxs-lookup"><span data-stu-id="04ad3-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="04ad3-163">Vea el [ejemplo](#outcsharp)).</span><span class="sxs-lookup"><span data-stu-id="04ad3-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="04ad3-164">`IAsyncCollector<T>` (versión asincrónica de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="04ad3-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="04ad3-165">`CloudTable` (con el SDK de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="04ad3-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="04ad3-166">Vea el [ejemplo](#readmulti)).</span><span class="sxs-lookup"><span data-stu-id="04ad3-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="04ad3-167">Ejemplo de salida</span><span class="sxs-lookup"><span data-stu-id="04ad3-167">Output sample</span></span>
<span data-ttu-id="04ad3-168">El siguiente ejemplo de *function.json* y *run.csx* muestra cómo escribir varias entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="04ad3-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="04ad3-169">Consulte el ejemplo de lenguaje específico que permite crear varias entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="04ad3-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="04ad3-170">C#</span><span class="sxs-lookup"><span data-stu-id="04ad3-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="04ad3-171">F#</span><span class="sxs-lookup"><span data-stu-id="04ad3-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="04ad3-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="04ad3-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="04ad3-173">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="04ad3-173">Output sample in C#</span></span> #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="04ad3-174">Ejemplo de salida en F#</span><span class="sxs-lookup"><span data-stu-id="04ad3-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="04ad3-175">Ejemplo de salida en Node.js</span><span class="sxs-lookup"><span data-stu-id="04ad3-175">Output sample in Node.js</span></span>
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="04ad3-176">Ejemplo: lectura de varias entidades de tabla en C#</span><span class="sxs-lookup"><span data-stu-id="04ad3-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="04ad3-177">El siguiente ejemplo de *function.json* y de código de C# lee las entidades de una clave de partición que se especifica en el mensaje en cola.</span><span class="sxs-lookup"><span data-stu-id="04ad3-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="04ad3-178">El código de C# agrega una referencia al SDK de Almacenamiento de Azure con el fin de que el tipo de entidad pueda derivar de `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="04ad3-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="04ad3-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04ad3-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

