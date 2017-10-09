---
title: enlaces de la tabla de almacenamiento de las funciones de aaaAzure | Documentos de Microsoft
description: "Comprender cómo toouse enlaces de almacenamiento de Azure en las funciones de Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="e803b-104">Enlaces de tablas de Storage en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e803b-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e803b-105">Este artículo explica cómo tooconfigure y el código de almacenamiento de Azure tabla enlaces en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="e803b-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="e803b-106">Azure Functions admite enlaces de entrada y salida para tablas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e803b-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="e803b-107">enlace de tablas de almacenamiento de Hello admite Hola los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="e803b-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="e803b-108">**Lectura de una sola fila de una función de C# o Node.js**. Establezca `partitionKey` y `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="e803b-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="e803b-109">Hola `filter` y `take` propiedades no se usan en este escenario.</span><span class="sxs-lookup"><span data-stu-id="e803b-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="e803b-110">**Leer varias filas en una función de C#** -tiempo de ejecución de funciones de hello proporciona un `IQueryable<T>` toohello tabla enlazado el objeto.</span><span class="sxs-lookup"><span data-stu-id="e803b-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="e803b-111">El tipo `T` debe derivar de `TableEntity` o implementar `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="e803b-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="e803b-112">Hola `partitionKey`, `rowKey`, `filter`, y `take` propiedades no se usan en este escenario; puede usar hello `IQueryable` objeto toodo ningún filtrado necesarios.</span><span class="sxs-lookup"><span data-stu-id="e803b-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="e803b-113">**Leer varias filas en una función de nodo** : hello establezca `filter` y `take` propiedades.</span><span class="sxs-lookup"><span data-stu-id="e803b-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="e803b-114">No establezca `partitionKey` o `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="e803b-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="e803b-115">**Escribir una o varias filas en una función de C#** -proporciona en tiempo de ejecución de funciones de Hola un `ICollector<T>` o `IAsyncCollector<T>` enlazados toohello tabla, donde `T` especifica el esquema de Hola de entidades de hello desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="e803b-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="e803b-116">Normalmente, el tipo `T` deriva de `TableEntity` o implementa `ITableEntity`, pero no tiene por qué ser así.</span><span class="sxs-lookup"><span data-stu-id="e803b-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="e803b-117">Hola `partitionKey`, `rowKey`, `filter`, y `take` propiedades no se usan en este escenario.</span><span class="sxs-lookup"><span data-stu-id="e803b-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="e803b-118">Enlace de entrada de tabla de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e803b-118">Storage table input binding</span></span>
<span data-ttu-id="e803b-119">Hola enlace de entrada de tabla de almacenamiento de Azure permite toouse una tabla de almacenamiento en la función.</span><span class="sxs-lookup"><span data-stu-id="e803b-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="e803b-120">Hola tooa entrada función de almacenamiento de tabla usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="e803b-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="e803b-121">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e803b-121">Note hello following:</span></span> 

* <span data-ttu-id="e803b-122">Use `partitionKey` y `rowKey` tooread conjuntamente una sola entidad.</span><span class="sxs-lookup"><span data-stu-id="e803b-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="e803b-123">Estas propiedades son opcionales.</span><span class="sxs-lookup"><span data-stu-id="e803b-123">These properties are optional.</span></span> 
* <span data-ttu-id="e803b-124">`connection`debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e803b-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="e803b-125">Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de la aplicación para que cuando se crea un almacenamiento de la cuenta o selecciona uno ya existente.</span><span class="sxs-lookup"><span data-stu-id="e803b-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="e803b-126">También puede [configurar esta aplicación manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="e803b-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="e803b-127">Uso de entradas</span><span class="sxs-lookup"><span data-stu-id="e803b-127">Input usage</span></span>
<span data-ttu-id="e803b-128">En funciones de C#, enlazar toohello entrada tabla entidad (o entidades) mediante un parámetro con nombre en la firma de la función, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="e803b-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="e803b-129">Donde `T` es la que desea que toodeserialize Hola datos, el tipo de datos de Hola y `paramName` es nombre hello especificado en hello [enlace de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="e803b-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="e803b-130">En las funciones de Node.js, accederás a Hola entrada tabla entidad (o entidades) mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e803b-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e803b-131">datos de entrada de Hola se pueden deserializar en funciones de Node.js o C#.</span><span class="sxs-lookup"><span data-stu-id="e803b-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="e803b-132">Hola deserializar objetos tienen `RowKey` y `PartitionKey` propiedades.</span><span class="sxs-lookup"><span data-stu-id="e803b-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="e803b-133">En funciones de C#, también puede enlazar tooany de hello siguientes tipos y funciones hello en tiempo de ejecución intentará demasiado deserializar los datos de la tabla de hello mediante ese tipo de:</span><span class="sxs-lookup"><span data-stu-id="e803b-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="e803b-134">Cualquier tipo que implemente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="e803b-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="e803b-135">Ejemplo de entrada</span><span class="sxs-lookup"><span data-stu-id="e803b-135">Input sample</span></span>
<span data-ttu-id="e803b-136">Debe que tener Hola después function.json, que utiliza un tooread de desencadenador de la cola una sola fila de tabla.</span><span class="sxs-lookup"><span data-stu-id="e803b-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="e803b-137">Especifica Hello JSON `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="e803b-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="e803b-138">`"rowKey": "{queueTrigger}"`indica que esa clave de fila Hola procede de la cadena de mensaje de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="e803b-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="e803b-139">Vea ejemplo de Hola a específicos del idioma que se lee de una entidad de tabla única.</span><span class="sxs-lookup"><span data-stu-id="e803b-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="e803b-140">C#</span><span class="sxs-lookup"><span data-stu-id="e803b-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="e803b-141">F#</span><span class="sxs-lookup"><span data-stu-id="e803b-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="e803b-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="e803b-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="e803b-143">Ejemplo de entrada en C#</span><span class="sxs-lookup"><span data-stu-id="e803b-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="e803b-144">Ejemplo de entrada en F#</span><span class="sxs-lookup"><span data-stu-id="e803b-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="e803b-145">Ejemplo de entrada en Node.js</span><span class="sxs-lookup"><span data-stu-id="e803b-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="e803b-146">Enlace de salida de tabla de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e803b-146">Storage table output binding</span></span>
<span data-ttu-id="e803b-147">Hola tabla de almacenamiento de Azure de salida enlace le permite la tabla de almacenamiento tooa toowrite de entidades en la función.</span><span class="sxs-lookup"><span data-stu-id="e803b-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="e803b-148">Hola de salida de la tabla de almacenamiento para una función usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="e803b-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="e803b-149">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e803b-149">Note hello following:</span></span> 

* <span data-ttu-id="e803b-150">Use `partitionKey` y `rowKey` toowrite conjuntamente una sola entidad.</span><span class="sxs-lookup"><span data-stu-id="e803b-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="e803b-151">Estas propiedades son opcionales.</span><span class="sxs-lookup"><span data-stu-id="e803b-151">These properties are optional.</span></span> <span data-ttu-id="e803b-152">También puede especificar `PartitionKey` y `RowKey` cuando creas Hola objetos de entidad en el código de función.</span><span class="sxs-lookup"><span data-stu-id="e803b-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="e803b-153">`connection`debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e803b-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="e803b-154">Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de la aplicación para que cuando se crea un almacenamiento de la cuenta o selecciona uno ya existente.</span><span class="sxs-lookup"><span data-stu-id="e803b-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="e803b-155">También puede [configurar esta aplicación manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="e803b-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="e803b-156">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="e803b-156">Output usage</span></span>
<span data-ttu-id="e803b-157">En funciones de C#, enlazar toohello salida de la tabla mediante el uso de hello denominado `out` como parámetro en la firma de la función, `out <T> <name>`, donde `T` es de tipo de datos de Hola que desea tooserialize Hola datos, y `paramName` es Hola nombre especificado en hello [el enlace de salida](#output).</span><span class="sxs-lookup"><span data-stu-id="e803b-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="e803b-158">En las funciones de Node.js, tener acceso a resultados de tabla de hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e803b-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e803b-159">Puede serializar objetos en las funciones de Node.js o C#.</span><span class="sxs-lookup"><span data-stu-id="e803b-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="e803b-160">Funciones de C#, también puede enlazar toohello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="e803b-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="e803b-161">Cualquier tipo que implemente `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="e803b-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="e803b-162">`ICollector<T>`(toooutput varias entidades.</span><span class="sxs-lookup"><span data-stu-id="e803b-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="e803b-163">Vea el [ejemplo](#outcsharp)).</span><span class="sxs-lookup"><span data-stu-id="e803b-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="e803b-164">`IAsyncCollector<T>` (versión asincrónica de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="e803b-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="e803b-165">`CloudTable`(uso de hello SDK de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e803b-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="e803b-166">Vea el [ejemplo](#readmulti)).</span><span class="sxs-lookup"><span data-stu-id="e803b-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="e803b-167">Ejemplo de salida</span><span class="sxs-lookup"><span data-stu-id="e803b-167">Output sample</span></span>
<span data-ttu-id="e803b-168">siguiente Hello *function.json* y *run.csx* en el ejemplo se muestra cómo toowrite varias entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="e803b-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="e803b-169">Vea el ejemplo específico del idioma de Hola que crea varias entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="e803b-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="e803b-170">C#</span><span class="sxs-lookup"><span data-stu-id="e803b-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="e803b-171">F#</span><span class="sxs-lookup"><span data-stu-id="e803b-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="e803b-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="e803b-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="e803b-173">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="e803b-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="e803b-174">Ejemplo de salida en F#</span><span class="sxs-lookup"><span data-stu-id="e803b-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="e803b-175">Ejemplo de salida en Node.js</span><span class="sxs-lookup"><span data-stu-id="e803b-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="e803b-176">Ejemplo: lectura de varias entidades de tabla en C#</span><span class="sxs-lookup"><span data-stu-id="e803b-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="e803b-177">siguiente Hello *function.json* y ejemplo de código de C# lee las entidades de una clave de partición que se especifica en el mensaje de bienvenida de cola.</span><span class="sxs-lookup"><span data-stu-id="e803b-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="e803b-178">Hola código C# agrega un toohello referencia SDK de almacenamiento de Azure para que el tipo de entidad de hello puede derivar de `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="e803b-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e803b-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e803b-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

