---
title: "enlaces de aplicaciones móviles de funciones aaaAzure | Documentos de Microsoft"
description: "Comprender cómo toouse enlaces de aplicaciones móviles de Azure en las funciones de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Enlaces de Aplicaciones móviles en funciones de Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se explica cómo tooconfigure y código [aplicaciones móviles de Azure](../app-service-mobile/app-service-mobile-value-prop.md) enlaces en las funciones de Azure. Azure Functions admite enlaces de entrada y salida para Mobile Apps.

Hello aplicaciones móviles de entrada y salida enlaces le permiten [de lectura y escritura de tablas de toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) en su aplicación móvil.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Enlace de entrada de Mobile Apps
Hola enlace de entrada de aplicaciones móviles carga un registro desde un punto de conexión de tabla móvil y lo pasa a la función. En C# y F # funciones, todos los registros de toohello los cambios realizados se envían automáticamente toohello atrás tabla cuando finalice correctamente la función de Hola.

Hola aplicaciones móviles de entrada tooa función usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

Tenga en cuenta los siguiente hello:

* `id`puede ser estático o se puede basar en desencadenador de Hola que invoca la función hello. Por ejemplo, si utiliza un [desencadenador cola]() para la función, a continuación, `"id": "{queueTrigger}"` utiliza Hola valor de cadena de mensaje de la cola de saludo como Hola tooretrieve de Id. de registro.
* `connection`debe contener el nombre de Hola de una configuración de aplicación en la aplicación de la función, que a su vez contiene la dirección URL de saludo de la aplicación móvil. función Hello usa este operaciones de REST de dirección URL tooconstruct Hola necesario en su aplicación móvil. Se [crear una configuración de aplicación en la aplicación de la función]() que contiene la dirección URL de la aplicación móvil (qué aspecto `http://<appname>.azurewebsites.net`), a continuación, especifique el nombre de Hola de configuración de la aplicación hello en hello `connection` propiedad en el enlace de entrada. 
* Necesita toospecify `apiKey` si se [implementar una clave de API en el back-end de aplicación móvil de Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementar una clave de API en el back-end de .NET aplicación móvil](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, le [crear una configuración de aplicación en la aplicación de la función]() que contiene la clave de API de hello, a continuación, agregue hello `apiKey` propiedad en el enlace de entrada con el nombre de Hola de configuración de la aplicación hello. 
  
  > [!IMPORTANT]
  > Esta clave de API no se debe compartir con los clientes de aplicación móvil. Solo debe ser clientes de forma segura tooservice lado distribuidos, como las funciones de Azure. 
  > 
  > [!NOTE]
  > Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente. Esto protege la información confidencial.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso de entradas
Esta sección muestra cómo toouse las aplicaciones móviles de entrada en el código de función de enlace. 

Al registro de hello con hello especificado se encuentra el Id. de tabla y registro, se pasa a Hola denominado [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parámetro (o, en Node.js, se pasa a hello `context.bindings.<name>` objeto). Cuando no se encuentra el registro de hello, parámetro hello es `null`. 

En las funciones de C# y F #, cualquier cambio que realice el registro de toohello de entrada (parámetro de entrada) se envía automáticamente atrás toohello tabla de aplicaciones móviles cuando finalice correctamente la función de Hola. En las funciones de Node.js, utilice `context.bindings.<name>` tooaccess Hola registro de entrada. No se puede modificar un registro en Node.js.

<a name="inputsample"></a>

## <a name="input-sample"></a>Ejemplo de entrada
Suponga que tiene Hola después function.json, que recupera un registro de la tabla de aplicación móvil con el Id. de Hola Hola desencadenador del mensaje de cola:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

Vea ejemplo de Hola a específicos del idioma que utiliza el registro de entrada de Hola desde el enlace de Hola. ejemplos de C# y F # Hello también modificar del registro de hello `text` propiedad.

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Ejemplo de entrada en C# #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Ejemplo de entrada en Node.js

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Enlace de salida de Mobile Apps
Utilice Hola aplicaciones móviles salida enlace toowrite un nuevo extremo de tabla de registro tooa aplicaciones móviles.  

Hola aplicaciones móviles de salida para una función usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

Tenga en cuenta los siguiente hello:

* `connection`debe contener el nombre de Hola de una configuración de aplicación en la aplicación de la función, que a su vez contiene la dirección URL de saludo de la aplicación móvil. función Hello usa este operaciones de REST de dirección URL tooconstruct Hola necesario en su aplicación móvil. Se [crear una configuración de aplicación en la aplicación de la función]() que contiene la dirección URL de la aplicación móvil (qué aspecto `http://<appname>.azurewebsites.net`), a continuación, especifique el nombre de Hola de configuración de la aplicación hello en hello `connection` propiedad en el enlace de entrada. 
* Necesita toospecify `apiKey` si se [implementar una clave de API en el back-end de aplicación móvil de Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementar una clave de API en el back-end de .NET aplicación móvil](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, le [crear una configuración de aplicación en la aplicación de la función]() que contiene la clave de API de hello, a continuación, agregue hello `apiKey` propiedad en el enlace de entrada con el nombre de Hola de configuración de la aplicación hello. 
  
  > [!IMPORTANT]
  > Esta clave de API no se debe compartir con los clientes de aplicación móvil. Solo debe ser clientes de forma segura tooservice lado distribuidos, como las funciones de Azure. 
  > 
  > [!NOTE]
  > Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente. Esto protege la información confidencial.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de salidas
Esta sección muestra cómo toouse las aplicaciones móviles de salida en el código de función de enlace. 

En funciones de C#, utilice un parámetro de salida con nombre de tipo `out object` tooaccess Hola registro de salida. En las funciones de Node.js, utilice `context.bindings.<name>` tooaccess Hola registro de salida.

<a name="outputsample"></a>

## <a name="output-sample"></a>Ejemplo de salida
Suponga que tiene Hola después function.json, que define un desencadenador de cola y una salida de aplicaciones móviles:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

Vea el ejemplo de específica del lenguaje de Hola que crea un registro en el extremo de tabla de aplicaciones móviles de hello con contenido de hello del mensaje de bienvenida de cola.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Ejemplo de salida en C# #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Ejemplo de salida en Node.js

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

