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
# <a name="azure-functions-storage-table-bindings"></a>Enlaces de tablas de Storage en Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo explica cómo tooconfigure y el código de almacenamiento de Azure tabla enlaces en las funciones de Azure. Azure Functions admite enlaces de entrada y salida para tablas de Azure Storage.

enlace de tablas de almacenamiento de Hello admite Hola los escenarios siguientes:

* **Lectura de una sola fila de una función de C# o Node.js**. Establezca `partitionKey` y `rowKey`. Hola `filter` y `take` propiedades no se usan en este escenario.
* **Leer varias filas en una función de C#** -tiempo de ejecución de funciones de hello proporciona un `IQueryable<T>` toohello tabla enlazado el objeto. El tipo `T` debe derivar de `TableEntity` o implementar `ITableEntity`. Hola `partitionKey`, `rowKey`, `filter`, y `take` propiedades no se usan en este escenario; puede usar hello `IQueryable` objeto toodo ningún filtrado necesarios. 
* **Leer varias filas en una función de nodo** : hello establezca `filter` y `take` propiedades. No establezca `partitionKey` o `rowKey`.
* **Escribir una o varias filas en una función de C#** -proporciona en tiempo de ejecución de funciones de Hola un `ICollector<T>` o `IAsyncCollector<T>` enlazados toohello tabla, donde `T` especifica el esquema de Hola de entidades de hello desea tooadd. Normalmente, el tipo `T` deriva de `TableEntity` o implementa `ITableEntity`, pero no tiene por qué ser así. Hola `partitionKey`, `rowKey`, `filter`, y `take` propiedades no se usan en este escenario.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Enlace de entrada de tabla de Azure Storage
Hola enlace de entrada de tabla de almacenamiento de Azure permite toouse una tabla de almacenamiento en la función. 

Hola tooa entrada función de almacenamiento de tabla usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:

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

Tenga en cuenta los siguiente hello: 

* Use `partitionKey` y `rowKey` tooread conjuntamente una sola entidad. Estas propiedades son opcionales. 
* `connection`debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento. Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de la aplicación para que cuando se crea un almacenamiento de la cuenta o selecciona uno ya existente. También puede [configurar esta aplicación manualmente](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso de entradas
En funciones de C#, enlazar toohello entrada tabla entidad (o entidades) mediante un parámetro con nombre en la firma de la función, como `<T> <name>`.
Donde `T` es la que desea que toodeserialize Hola datos, el tipo de datos de Hola y `paramName` es nombre hello especificado en hello [enlace de entrada](#input). En las funciones de Node.js, accederás a Hola entrada tabla entidad (o entidades) mediante `context.bindings.<name>`.

datos de entrada de Hola se pueden deserializar en funciones de Node.js o C#. Hola deserializar objetos tienen `RowKey` y `PartitionKey` propiedades.

En funciones de C#, también puede enlazar tooany de hello siguientes tipos y funciones hello en tiempo de ejecución intentará demasiado deserializar los datos de la tabla de hello mediante ese tipo de:

* Cualquier tipo que implemente `ITableEntity`
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Ejemplo de entrada
Debe que tener Hola después function.json, que utiliza un tooread de desencadenador de la cola una sola fila de tabla. Especifica Hello JSON `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`indica que esa clave de fila Hola procede de la cadena de mensaje de cola de Hola.

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

Vea ejemplo de Hola a específicos del idioma que se lee de una entidad de tabla única.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Ejemplo de entrada en C# #
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

### <a name="input-sample-in-f"></a>Ejemplo de entrada en F# #
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

### <a name="input-sample-in-nodejs"></a>Ejemplo de entrada en Node.js
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Enlace de salida de tabla de Azure Storage
Hola tabla de almacenamiento de Azure de salida enlace le permite la tabla de almacenamiento tooa toowrite de entidades en la función. 

Hola de salida de la tabla de almacenamiento para una función usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:

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

Tenga en cuenta los siguiente hello: 

* Use `partitionKey` y `rowKey` toowrite conjuntamente una sola entidad. Estas propiedades son opcionales. También puede especificar `PartitionKey` y `RowKey` cuando creas Hola objetos de entidad en el código de función.
* `connection`debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento. Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de la aplicación para que cuando se crea un almacenamiento de la cuenta o selecciona uno ya existente. También puede [configurar esta aplicación manualmente](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de salidas
En funciones de C#, enlazar toohello salida de la tabla mediante el uso de hello denominado `out` como parámetro en la firma de la función, `out <T> <name>`, donde `T` es de tipo de datos de Hola que desea tooserialize Hola datos, y `paramName` es Hola nombre especificado en hello [el enlace de salida](#output). En las funciones de Node.js, tener acceso a resultados de tabla de hello `context.bindings.<name>`.

Puede serializar objetos en las funciones de Node.js o C#. Funciones de C#, también puede enlazar toohello siguientes tipos:

* Cualquier tipo que implemente `ITableEntity`
* `ICollector<T>`(toooutput varias entidades. Vea el [ejemplo](#outcsharp)).
* `IAsyncCollector<T>` (versión asincrónica de `ICollector<T>`)
* `CloudTable`(uso de hello SDK de almacenamiento de Azure. Vea el [ejemplo](#readmulti)).

<a name="outputsample"></a>

## <a name="output-sample"></a>Ejemplo de salida
siguiente Hello *function.json* y *run.csx* en el ejemplo se muestra cómo toowrite varias entidades de tabla.

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

Vea el ejemplo específico del idioma de Hola que crea varias entidades de tabla.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Ejemplo de salida en C# #
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

### <a name="output-sample-in-f"></a>Ejemplo de salida en F# #
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

### <a name="output-sample-in-nodejs"></a>Ejemplo de salida en Node.js
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

## <a name="sample-read-multiple-table-entities-in-c"></a>Ejemplo: lectura de varias entidades de tabla en C#  #
siguiente Hello *function.json* y ejemplo de código de C# lee las entidades de una clave de partición que se especifica en el mensaje de bienvenida de cola.

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

Hola código C# agrega un toohello referencia SDK de almacenamiento de Azure para que el tipo de entidad de hello puede derivar de `TableEntity`.

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

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

