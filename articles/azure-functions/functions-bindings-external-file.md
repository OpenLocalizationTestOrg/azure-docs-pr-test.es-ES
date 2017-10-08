---
title: "enlaces del archivo externo de las funciones de aaaAzure (versión preliminar) | Documentos de Microsoft"
description: Uso de enlaces de archivo externo en Azure Functions
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a>Enlaces de archivo externo de Azure Functions (versión preliminar)
Este artículo muestra cómo toomanipulate los archivos de SaaS diferentes proveedores (por ejemplo, OneDrive, Dropbox) dentro de la función de utilización de enlaces integrados. Azure Functions admite enlaces de desencadenador, entrada y salida para un archivo externo.

Este enlace crea conexiones de API tooSaaS proveedores, o utiliza conexiones de API existentes del grupo de recursos de la aplicación de la función.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Conexiones de archivos compatibles

|Conector|Desencadenador|Entrada|Salida|
|:-----|:---:|:---:|:---:|
|[Box](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive para la Empresa](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google Drive](https://www.google.com/drive/)||x|x|

> [!NOTE]
> También se pueden utilizar conexiones de archivos externos en [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).

## <a name="external-file-trigger-binding"></a>Enlace de desencadenador de archivo externo

desencadenador de archivo externo Azure Hola le permite supervisar una carpeta remota y ejecutar el código de función cuando se detectan cambios.

desencadenador de archivo externo de Hello utiliza Hola siguientes objetos JSON en hello `bindings` matriz de function.json

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a>Patrones de nombre
Puede especificar un patrón de nombre de archivo en hello `path` propiedad. carpeta de Hello al que hace referencia debe existir en el proveedor de SaaS Hola.
Ejemplos:

```json
"path": "input/original-{name}",
```

Esta ruta de acceso podría encontrar un archivo denominado *original File1.txt* en hello *entrada* carpeta y el valor de Hola de hello `name` variable en el código de la función sería `File1.txt`.

Otro ejemplo:

```json
"path": "input/{filename}.{fileextension}",
```

Esta ruta de acceso también podría encontrar un archivo denominado *original File1.txt*y el valor de Hola de hello `filename` y `fileextension` serían variables en el código de la función *original File1* y  *txt*.

Puede restringir el tipo de archivo de Hola de archivos mediante el uso de un valor fijo para la extensión de archivo Hola. Por ejemplo:

```json
"path": "samples/{name}.png",
```

En este caso, solo *.png* archivos Hola *ejemplos* función hello de desencadenador de carpeta.

Las llaves son caracteres especiales en los patrones de nombre. nombres de archivo toospecify que tienen las llaves en nombre de hello, llaves dobles Hola.
Por ejemplo:

```json
"path": "images/{{20140101}}-{name}",
```

Esta ruta de acceso podría encontrar un archivo denominado *{20140101}-soundfile.mp3* en hello *imágenes* hello y carpeta `name` sería el valor de la variable en el código de la función hello *soundfile.mp3*.

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a>Control de archivos dudosos
Cuando se produce un error en una función de desencadenador de archivo externo, las funciones de Azure vuelve a intentar esa función too5 horas de forma predeterminada (incluyendo el primer intento de hello) para un archivo determinado.
Si se produce un error en todos los intentos de 5, funciones agrega una cola de almacenamiento de tooa mensaje denominada *webjobs-apihubtrigger-dudosos*. mensaje de la cola de Hola para archivos de mensajes dudosos es un objeto JSON que contiene Hola propiedades siguientes:

* FunctionId (en formato de hello  *&lt;nombre de la aplicación de función >*. Las funciones.  *&lt;nombre de función >*)
* FileType
* FolderName
* FileName
* ETag (un identificador de la versión del archivo, por ejemplo: "0x8D1DC6E70A277EF")


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso del desencadenador
En funciones de C#, se enlazan los datos de archivo de entrada de toohello mediante un parámetro con nombre de la firma de función, como `<T> <name>`.
Donde `T` es la que desea que toodeserialize Hola datos, el tipo de datos de Hola y `paramName` es nombre hello especificado en el [desencadenar JSON](#trigger). En las funciones de Node.js, se obtiene acceso mediante datos de archivo de entrada de hello `context.bindings.<name>`.

archivo Hello se puede deserializar en cualquiera de los siguientes tipos de hello:

* Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos de archivos serializados mediante JSON.
  Si se declara un tipo de entrada personalizado (p. ej. `FooType`), las funciones de Azure intenta datos JSON de toodeserialize hello en el tipo especificado.
* Cadena: útil para los datos de archivo de texto.

En funciones de C#, también puede enlazar tooany de los siguientes tipos de Hola y en tiempo de ejecución de funciones de hello intenta deserializar los datos de archivo hello mediante ese tipo:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Ejemplo de desencadenador
Suponga que tiene Hola después function.json, que define un desencadenador de archivo externo:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

Vea el ejemplo específico del idioma de Hola que registra el contenido de Hola de cada archivo que se agrega la carpeta supervisada toohello.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>Uso del desencadenador en C# #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a>Uso del desencadenador en Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Enlace de entrada de archivo externo
enlace de entrada de archivo externo Azure Hola permite toouse un archivo desde una carpeta en la función externa.

función de entrada tooa archivo externo Hello usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Tenga en cuenta los siguiente hello:

* `path`debe contener el nombre de la carpeta de Hola y el nombre de archivo de Hola. Por ejemplo, si tiene un [desencadenador cola](functions-bindings-storage-queue.md) en la función, puede usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa archivo Hola `samples-workitems` carpeta con un nombre que coincida con el nombre de archivo de hello especificado en el mensaje de bienvenida de desencadenador.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso de entradas
En funciones de C#, se enlazan los datos de archivo de entrada de toohello mediante un parámetro con nombre de la firma de función, como `<T> <name>`.
Donde `T` es la que desea que toodeserialize Hola datos, el tipo de datos de Hola y `paramName` es nombre hello especificado en el [enlace de entrada](#input). En las funciones de Node.js, se obtiene acceso mediante datos de archivo de entrada de hello `context.bindings.<name>`.

archivo Hello se puede deserializar en cualquiera de los siguientes tipos de hello:

* Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos de archivos serializados mediante JSON.
  Si se declara un tipo de entrada personalizado (p. ej. `InputType`), las funciones de Azure intenta datos JSON de toodeserialize hello en el tipo especificado.
* Cadena: útil para los datos de archivo de texto.

En funciones de C#, también puede enlazar tooany de los siguientes tipos de Hola y en tiempo de ejecución de funciones de hello intenta deserializar los datos de archivo hello mediante ese tipo:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Enlace de salida de archivo externo
Hello Azure archivo externo de salida enlace permite carpeta externo tooan de toowrite archivos en la función.

archivo externo Hola de salida para una función usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Tenga en cuenta los siguiente hello:

* `path`debe contener el nombre de la carpeta de Hola y Hola toowrite de nombre de archivo a. Por ejemplo, si tiene un [desencadenador cola](functions-bindings-storage-queue.md) en la función, puede usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa archivo Hola `samples-workitems` carpeta con un nombre que coincida con el nombre de archivo de hello especificado en el mensaje de bienvenida de desencadenador.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de salidas
En funciones de C#, enlazar toohello archivo de salida mediante el uso de hello denominado `out` como parámetro en la firma de la función, `out <T> <name>`, donde `T` es de tipo de datos de Hola que desea tooserialize Hola datos, y `paramName` es Hola nombre se especifica en el [el enlace de salida](#output). En las funciones de Node.js, se obtiene acceso mediante archivo de salida de hello `context.bindings.<name>`.

Puede escribir el archivo de salida de toohello mediante cualquiera de los siguientes tipos de hello:

* Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para la serialización mediante JSON.
  Si se declara un tipo de resultado personalizado (p. ej. `out OutputType paramName`), las funciones de Azure intenta tooserialize objeto a JSON. Si el parámetro de salida de hello es null cuando sale de la función hello, en tiempo de ejecución de funciones de hello crea un archivo como un objeto null.
* Cadena: (`out string paramName`) útil para los datos de archivo de texto. en tiempo de ejecución de funciones de Hello crea un archivo sólo si el parámetro de cadena es distinto de null cuando sale de la función hello.

En las funciones de C# también puede generar tooany de hello siguientes tipos:

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Ejemplo de entrada y salida
Suponga que tiene Hola después function.json, que define un [desencadenador de cola de almacenamiento](functions-bindings-storage-queue.md), un archivo externo de entrada y salida de un archivo externo:

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Vea el ejemplo de específica del lenguaje de Hola que copia el archivo de salida de hello archivo de entrada toohello.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>Uso en C# #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a>Uso en Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
