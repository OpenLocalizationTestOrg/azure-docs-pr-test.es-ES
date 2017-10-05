---
title: "Enlaces de archivo externo de Azure Functions (versión preliminar) | Microsoft Docs"
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
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="f5df7-103">Enlaces de archivo externo de Azure Functions (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="f5df7-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="f5df7-104">Este artículo muestra cómo manipular archivos de diferentes proveedores de SaaS (por ejemplo, OneDrive y Dropbox) dentro de la función mediante enlaces integrados.</span><span class="sxs-lookup"><span data-stu-id="f5df7-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="f5df7-105">Azure Functions admite enlaces de desencadenador, entrada y salida para un archivo externo.</span><span class="sxs-lookup"><span data-stu-id="f5df7-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="f5df7-106">Este enlace crea conexiones de API para los proveedores de SaaS o utiliza conexiones de API existentes del grupo de recursos de Function App.</span><span class="sxs-lookup"><span data-stu-id="f5df7-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="f5df7-107">Conexiones de archivos compatibles</span><span class="sxs-lookup"><span data-stu-id="f5df7-107">Supported File connections</span></span>

|<span data-ttu-id="f5df7-108">Conector</span><span class="sxs-lookup"><span data-stu-id="f5df7-108">Connector</span></span>|<span data-ttu-id="f5df7-109">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="f5df7-109">Trigger</span></span>|<span data-ttu-id="f5df7-110">Entrada</span><span class="sxs-lookup"><span data-stu-id="f5df7-110">Input</span></span>|<span data-ttu-id="f5df7-111">Salida</span><span class="sxs-lookup"><span data-stu-id="f5df7-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="f5df7-112">Box</span><span class="sxs-lookup"><span data-stu-id="f5df7-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="f5df7-113">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-113">x</span></span>|<span data-ttu-id="f5df7-114">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-114">x</span></span>|<span data-ttu-id="f5df7-115">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-115">x</span></span>
|[<span data-ttu-id="f5df7-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="f5df7-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="f5df7-117">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-117">x</span></span>|<span data-ttu-id="f5df7-118">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-118">x</span></span>|<span data-ttu-id="f5df7-119">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-119">x</span></span>
|[<span data-ttu-id="f5df7-120">FTP</span><span class="sxs-lookup"><span data-stu-id="f5df7-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="f5df7-121">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-121">x</span></span>|<span data-ttu-id="f5df7-122">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-122">x</span></span>|<span data-ttu-id="f5df7-123">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-123">x</span></span>
|[<span data-ttu-id="f5df7-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="f5df7-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="f5df7-125">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-125">x</span></span>|<span data-ttu-id="f5df7-126">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-126">x</span></span>|<span data-ttu-id="f5df7-127">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-127">x</span></span>
|[<span data-ttu-id="f5df7-128">OneDrive para la Empresa</span><span class="sxs-lookup"><span data-stu-id="f5df7-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="f5df7-129">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-129">x</span></span>|<span data-ttu-id="f5df7-130">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-130">x</span></span>|<span data-ttu-id="f5df7-131">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-131">x</span></span>
|[<span data-ttu-id="f5df7-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="f5df7-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="f5df7-133">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-133">x</span></span>|<span data-ttu-id="f5df7-134">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-134">x</span></span>|<span data-ttu-id="f5df7-135">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-135">x</span></span>
|[<span data-ttu-id="f5df7-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="f5df7-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="f5df7-137">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-137">x</span></span>|<span data-ttu-id="f5df7-138">x</span><span class="sxs-lookup"><span data-stu-id="f5df7-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="f5df7-139">También se pueden utilizar conexiones de archivos externos en [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="f5df7-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="f5df7-140">Enlace de desencadenador de archivo externo</span><span class="sxs-lookup"><span data-stu-id="f5df7-140">External File trigger binding</span></span>

<span data-ttu-id="f5df7-141">El desencadenador de archivo externo de Azure permite supervisar una carpeta remota y ejecutar el código de función cuando se detectan cambios.</span><span class="sxs-lookup"><span data-stu-id="f5df7-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="f5df7-142">El desencadenador de archivo externo utiliza los siguientes objetos JSON en la matriz `bindings` de function.json.</span><span class="sxs-lookup"><span data-stu-id="f5df7-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="f5df7-143">Patrones de nombre</span><span class="sxs-lookup"><span data-stu-id="f5df7-143">Name patterns</span></span>
<span data-ttu-id="f5df7-144">Puede especificar un patrón de nombre de archivo en la propiedad `path` .</span><span class="sxs-lookup"><span data-stu-id="f5df7-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="f5df7-145">La carpeta a la que se hace referencia debe existir en el proveedor de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f5df7-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="f5df7-146">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="f5df7-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="f5df7-147">Esta ruta de acceso encontraría un archivo denominado *original-File1.txt* en la carpeta *input* y el valor de la variable `name` en el código de la función sería `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="f5df7-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="f5df7-148">Otro ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5df7-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="f5df7-149">Esta ruta de acceso también encontraría un archivo denominado *original-File1.txt* y el valor de las variables `filename` y `fileextension` en el código de la función sería *original-File1* y *txt*.</span><span class="sxs-lookup"><span data-stu-id="f5df7-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="f5df7-150">Puede restringir el tipo de archivo de los archivos mediante el uso de un valor fijo para la extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="f5df7-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="f5df7-151">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5df7-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="f5df7-152">En este caso, solo desencadenarán la función los archivos de tipo *.png* de la carpeta *samples*.</span><span class="sxs-lookup"><span data-stu-id="f5df7-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="f5df7-153">Las llaves son caracteres especiales en los patrones de nombre.</span><span class="sxs-lookup"><span data-stu-id="f5df7-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="f5df7-154">Si necesita especificar un nombre de archivo que contiene llaves, duplique las llaves.</span><span class="sxs-lookup"><span data-stu-id="f5df7-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="f5df7-155">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f5df7-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="f5df7-156">Esta ruta encontraría un archivo denominado *{20140101}-soundfile.mp3* en la carpeta *images* y el valor de la variable `name` del código de la función sería *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="f5df7-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="f5df7-157">Control de archivos dudosos</span><span class="sxs-lookup"><span data-stu-id="f5df7-157">Handling poison files</span></span>
<span data-ttu-id="f5df7-158">Si se produce un error en una función del desencadenador de archivo externo, Azure Functions volverá a intentar esa función hasta 5 veces de forma predeterminada (incluido el primer intento) para un determinado archivo.</span><span class="sxs-lookup"><span data-stu-id="f5df7-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="f5df7-159">Si se produce un error en los cinco intentos, Functions agregará un mensaje a una cola de Storage denominada *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="f5df7-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="f5df7-160">El mensaje de cola para los archivos dudosos es un objeto JSON que contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="f5df7-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="f5df7-161">FunctionId (con el formato *&lt;nombre de aplicación de función>*.Functions.*&lt;nombre de función>*)</span><span class="sxs-lookup"><span data-stu-id="f5df7-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="f5df7-162">FileType</span><span class="sxs-lookup"><span data-stu-id="f5df7-162">FileType</span></span>
* <span data-ttu-id="f5df7-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="f5df7-163">FolderName</span></span>
* <span data-ttu-id="f5df7-164">FileName</span><span class="sxs-lookup"><span data-stu-id="f5df7-164">FileName</span></span>
* <span data-ttu-id="f5df7-165">ETag (un identificador de la versión del archivo, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="f5df7-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="f5df7-166">Uso del desencadenador</span><span class="sxs-lookup"><span data-stu-id="f5df7-166">Trigger usage</span></span>
<span data-ttu-id="f5df7-167">En las funciones de C#, puede enlazar con los datos de entrada de archivo mediante un parámetro con nombre en la firma de la función, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="f5df7-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="f5df7-168">Donde `T` es el tipo de datos en el que desea deserializar los datos, y `paramName` es el nombre que especificó en el [desencadenador JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="f5df7-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="f5df7-169">En las funciones de Node.js, puede obtener acceso a los datos de entrada del archivo mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f5df7-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f5df7-170">El archivo se puede deserializar en cualquiera de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f5df7-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="f5df7-171">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos de archivos serializados mediante JSON.</span><span class="sxs-lookup"><span data-stu-id="f5df7-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="f5df7-172">Si declara un tipo de entrada personalizado (por ejemplo, `FooType`), Azure Functions intentará deserializar los datos JSON en el tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="f5df7-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="f5df7-173">Cadena: útil para los datos de archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="f5df7-173">String - useful for text file data.</span></span>

<span data-ttu-id="f5df7-174">En las funciones de C#, también puede enlazar con cualquiera de los siguientes tipos y el entorno de tiempo de ejecución de Functions intenta deserializar los datos del archivo mediante ese tipo:</span><span class="sxs-lookup"><span data-stu-id="f5df7-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="f5df7-175">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="f5df7-175">Trigger sample</span></span>
<span data-ttu-id="f5df7-176">Suponga que tiene el siguiente function.json que define un desencadenador de archivo externo:</span><span class="sxs-lookup"><span data-stu-id="f5df7-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="f5df7-177">Consulte el ejemplo de código específico del lenguaje que registra el contenido de cada archivo que se agrega a la carpeta supervisada.</span><span class="sxs-lookup"><span data-stu-id="f5df7-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="f5df7-178">C#</span><span class="sxs-lookup"><span data-stu-id="f5df7-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="f5df7-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="f5df7-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="f5df7-180">Uso del desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="f5df7-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="f5df7-181">Uso del desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="f5df7-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="f5df7-182">Enlace de entrada de archivo externo</span><span class="sxs-lookup"><span data-stu-id="f5df7-182">External File input binding</span></span>
<span data-ttu-id="f5df7-183">El enlace de entrada de archivo externo de Azure le permite utilizar un archivo de una carpeta externa en la función.</span><span class="sxs-lookup"><span data-stu-id="f5df7-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="f5df7-184">La entrada del archivo externo a una función utiliza los siguientes objetos JSON en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="f5df7-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="f5df7-185">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5df7-185">Note the following:</span></span>

* <span data-ttu-id="f5df7-186">`path` debe contener el nombre de archivo y el nombre de carpeta.</span><span class="sxs-lookup"><span data-stu-id="f5df7-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="f5df7-187">Por ejemplo, si tiene un [desencadenador de cola](functions-bindings-storage-queue.md) en la función, puede usar `"path": "samples-workitems/{queueTrigger}"` para apuntar a un archivo de la carpeta `samples-workitems` con un nombre que coincida con el nombre de archivo especificado en el mensaje desencadenador.</span><span class="sxs-lookup"><span data-stu-id="f5df7-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="f5df7-188">Uso de entradas</span><span class="sxs-lookup"><span data-stu-id="f5df7-188">Input usage</span></span>
<span data-ttu-id="f5df7-189">En las funciones de C#, puede enlazar con los datos de entrada de archivo mediante un parámetro con nombre en la firma de la función, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="f5df7-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="f5df7-190">Donde `T` es el tipo de datos en el que desea deserializar los datos, y `paramName` es el nombre que especificó en el [enlace de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="f5df7-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="f5df7-191">En las funciones de Node.js, puede obtener acceso a los datos de entrada del archivo mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f5df7-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f5df7-192">El archivo se puede deserializar en cualquiera de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f5df7-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="f5df7-193">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos de archivos serializados mediante JSON.</span><span class="sxs-lookup"><span data-stu-id="f5df7-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="f5df7-194">Si declara un tipo de entrada personalizado (por ejemplo, `InputType`), Azure Functions intentará deserializar los datos JSON en el tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="f5df7-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="f5df7-195">Cadena: útil para los datos de archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="f5df7-195">String - useful for text file data.</span></span>

<span data-ttu-id="f5df7-196">En las funciones de C#, también puede enlazar con cualquiera de los siguientes tipos y el entorno de tiempo de ejecución de Functions intenta deserializar los datos del archivo mediante ese tipo:</span><span class="sxs-lookup"><span data-stu-id="f5df7-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="f5df7-197">Enlace de salida de archivo externo</span><span class="sxs-lookup"><span data-stu-id="f5df7-197">External File output binding</span></span>
<span data-ttu-id="f5df7-198">El enlace de salida de archivo externo de Azure le permite escribir archivos en una carpeta externa en la función.</span><span class="sxs-lookup"><span data-stu-id="f5df7-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="f5df7-199">La salida de archivo externo para una función utiliza los siguientes objetos JSON en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="f5df7-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="f5df7-200">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5df7-200">Note the following:</span></span>

* <span data-ttu-id="f5df7-201">`path` debe contener el nombre de archivo y el nombre de carpeta en la que se va a escribir.</span><span class="sxs-lookup"><span data-stu-id="f5df7-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="f5df7-202">Por ejemplo, si tiene un [desencadenador de cola](functions-bindings-storage-queue.md) en la función, puede usar `"path": "samples-workitems/{queueTrigger}"` para apuntar a un archivo de la carpeta `samples-workitems` con un nombre que coincida con el nombre de archivo especificado en el mensaje desencadenador.</span><span class="sxs-lookup"><span data-stu-id="f5df7-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="f5df7-203">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="f5df7-203">Output usage</span></span>
<span data-ttu-id="f5df7-204">En las funciones de C#, puede enlazar al archivo de salida mediante el parámetro con nombre `out` de la firma de la función, como `out <T> <name>`, donde `T` es el tipo de datos en el que desea serializar los datos y `paramName` es el nombre que especificó en el [enlace de salida](#output).</span><span class="sxs-lookup"><span data-stu-id="f5df7-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="f5df7-205">En las funciones de Node.js, puede obtener acceso al archivo de salida mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f5df7-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f5df7-206">Puede escribir en el archivo de salida mediante cualquiera de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f5df7-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="f5df7-207">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para la serialización mediante JSON.</span><span class="sxs-lookup"><span data-stu-id="f5df7-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="f5df7-208">Si declara un tipo de salida personalizado (por ejemplo, `out OutputType paramName`), Azure Functions intentará serializar el objeto en JSON.</span><span class="sxs-lookup"><span data-stu-id="f5df7-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="f5df7-209">Si el parámetro de salida es nulo cuando sale la función, el entorno de tiempo de ejecución de Functions creará un archivo como objeto nulo.</span><span class="sxs-lookup"><span data-stu-id="f5df7-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="f5df7-210">Cadena: (`out string paramName`) útil para los datos de archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="f5df7-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="f5df7-211">El entorno de tiempo de ejecución de Functions genera un archivo solo si el parámetro de cadena no es nulo cuando sale la función.</span><span class="sxs-lookup"><span data-stu-id="f5df7-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="f5df7-212">En las funciones de C# también puede enviar la salida a cualquiera de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f5df7-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="f5df7-213">Ejemplo de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="f5df7-213">Input + Output sample</span></span>
<span data-ttu-id="f5df7-214">Suponga que tiene el siguiente objeto function.json que define un [desencadenador de cola de Storage](functions-bindings-storage-queue.md), una entrada de archivo externo y una salida de archivo externo:</span><span class="sxs-lookup"><span data-stu-id="f5df7-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="f5df7-215">Vea el ejemplo específico del lenguaje que copia el archivo de entrada en el archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="f5df7-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="f5df7-216">C#</span><span class="sxs-lookup"><span data-stu-id="f5df7-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="f5df7-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="f5df7-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="f5df7-218">Uso en C#</span><span class="sxs-lookup"><span data-stu-id="f5df7-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="f5df7-219">Uso en Node.js</span><span class="sxs-lookup"><span data-stu-id="f5df7-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="f5df7-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5df7-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
