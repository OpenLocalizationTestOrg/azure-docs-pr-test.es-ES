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
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="e82cd-103">Enlaces de archivo externo de Azure Functions (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="e82cd-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="e82cd-104">Este artículo muestra cómo toomanipulate los archivos de SaaS diferentes proveedores (por ejemplo, OneDrive, Dropbox) dentro de la función de utilización de enlaces integrados.</span><span class="sxs-lookup"><span data-stu-id="e82cd-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="e82cd-105">Azure Functions admite enlaces de desencadenador, entrada y salida para un archivo externo.</span><span class="sxs-lookup"><span data-stu-id="e82cd-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="e82cd-106">Este enlace crea conexiones de API tooSaaS proveedores, o utiliza conexiones de API existentes del grupo de recursos de la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="e82cd-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="e82cd-107">Conexiones de archivos compatibles</span><span class="sxs-lookup"><span data-stu-id="e82cd-107">Supported File connections</span></span>

|<span data-ttu-id="e82cd-108">Conector</span><span class="sxs-lookup"><span data-stu-id="e82cd-108">Connector</span></span>|<span data-ttu-id="e82cd-109">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="e82cd-109">Trigger</span></span>|<span data-ttu-id="e82cd-110">Entrada</span><span class="sxs-lookup"><span data-stu-id="e82cd-110">Input</span></span>|<span data-ttu-id="e82cd-111">Salida</span><span class="sxs-lookup"><span data-stu-id="e82cd-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="e82cd-112">Box</span><span class="sxs-lookup"><span data-stu-id="e82cd-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="e82cd-113">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-113">x</span></span>|<span data-ttu-id="e82cd-114">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-114">x</span></span>|<span data-ttu-id="e82cd-115">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-115">x</span></span>
|[<span data-ttu-id="e82cd-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="e82cd-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="e82cd-117">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-117">x</span></span>|<span data-ttu-id="e82cd-118">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-118">x</span></span>|<span data-ttu-id="e82cd-119">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-119">x</span></span>
|[<span data-ttu-id="e82cd-120">FTP</span><span class="sxs-lookup"><span data-stu-id="e82cd-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="e82cd-121">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-121">x</span></span>|<span data-ttu-id="e82cd-122">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-122">x</span></span>|<span data-ttu-id="e82cd-123">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-123">x</span></span>
|[<span data-ttu-id="e82cd-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="e82cd-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="e82cd-125">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-125">x</span></span>|<span data-ttu-id="e82cd-126">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-126">x</span></span>|<span data-ttu-id="e82cd-127">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-127">x</span></span>
|[<span data-ttu-id="e82cd-128">OneDrive para la Empresa</span><span class="sxs-lookup"><span data-stu-id="e82cd-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="e82cd-129">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-129">x</span></span>|<span data-ttu-id="e82cd-130">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-130">x</span></span>|<span data-ttu-id="e82cd-131">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-131">x</span></span>
|[<span data-ttu-id="e82cd-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="e82cd-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="e82cd-133">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-133">x</span></span>|<span data-ttu-id="e82cd-134">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-134">x</span></span>|<span data-ttu-id="e82cd-135">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-135">x</span></span>
|[<span data-ttu-id="e82cd-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="e82cd-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="e82cd-137">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-137">x</span></span>|<span data-ttu-id="e82cd-138">x</span><span class="sxs-lookup"><span data-stu-id="e82cd-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="e82cd-139">También se pueden utilizar conexiones de archivos externos en [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="e82cd-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="e82cd-140">Enlace de desencadenador de archivo externo</span><span class="sxs-lookup"><span data-stu-id="e82cd-140">External File trigger binding</span></span>

<span data-ttu-id="e82cd-141">desencadenador de archivo externo Azure Hola le permite supervisar una carpeta remota y ejecutar el código de función cuando se detectan cambios.</span><span class="sxs-lookup"><span data-stu-id="e82cd-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="e82cd-142">desencadenador de archivo externo de Hello utiliza Hola siguientes objetos JSON en hello `bindings` matriz de function.json</span><span class="sxs-lookup"><span data-stu-id="e82cd-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

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

### <a name="name-patterns"></a><span data-ttu-id="e82cd-143">Patrones de nombre</span><span class="sxs-lookup"><span data-stu-id="e82cd-143">Name patterns</span></span>
<span data-ttu-id="e82cd-144">Puede especificar un patrón de nombre de archivo en hello `path` propiedad.</span><span class="sxs-lookup"><span data-stu-id="e82cd-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="e82cd-145">carpeta de Hello al que hace referencia debe existir en el proveedor de SaaS Hola.</span><span class="sxs-lookup"><span data-stu-id="e82cd-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="e82cd-146">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="e82cd-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="e82cd-147">Esta ruta de acceso podría encontrar un archivo denominado *original File1.txt* en hello *entrada* carpeta y el valor de Hola de hello `name` variable en el código de la función sería `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="e82cd-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="e82cd-148">Otro ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e82cd-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="e82cd-149">Esta ruta de acceso también podría encontrar un archivo denominado *original File1.txt*y el valor de Hola de hello `filename` y `fileextension` serían variables en el código de la función *original File1* y  *txt*.</span><span class="sxs-lookup"><span data-stu-id="e82cd-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="e82cd-150">Puede restringir el tipo de archivo de Hola de archivos mediante el uso de un valor fijo para la extensión de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="e82cd-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="e82cd-151">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e82cd-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="e82cd-152">En este caso, solo *.png* archivos Hola *ejemplos* función hello de desencadenador de carpeta.</span><span class="sxs-lookup"><span data-stu-id="e82cd-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="e82cd-153">Las llaves son caracteres especiales en los patrones de nombre.</span><span class="sxs-lookup"><span data-stu-id="e82cd-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="e82cd-154">nombres de archivo toospecify que tienen las llaves en nombre de hello, llaves dobles Hola.</span><span class="sxs-lookup"><span data-stu-id="e82cd-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="e82cd-155">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e82cd-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="e82cd-156">Esta ruta de acceso podría encontrar un archivo denominado *{20140101}-soundfile.mp3* en hello *imágenes* hello y carpeta `name` sería el valor de la variable en el código de la función hello *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="e82cd-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

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

### <a name="handling-poison-files"></a><span data-ttu-id="e82cd-157">Control de archivos dudosos</span><span class="sxs-lookup"><span data-stu-id="e82cd-157">Handling poison files</span></span>
<span data-ttu-id="e82cd-158">Cuando se produce un error en una función de desencadenador de archivo externo, las funciones de Azure vuelve a intentar esa función too5 horas de forma predeterminada (incluyendo el primer intento de hello) para un archivo determinado.</span><span class="sxs-lookup"><span data-stu-id="e82cd-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="e82cd-159">Si se produce un error en todos los intentos de 5, funciones agrega una cola de almacenamiento de tooa mensaje denominada *webjobs-apihubtrigger-dudosos*.</span><span class="sxs-lookup"><span data-stu-id="e82cd-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="e82cd-160">mensaje de la cola de Hola para archivos de mensajes dudosos es un objeto JSON que contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="e82cd-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="e82cd-161">FunctionId (en formato de hello  *&lt;nombre de la aplicación de función >*. Las funciones.  *&lt;nombre de función >*)</span><span class="sxs-lookup"><span data-stu-id="e82cd-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="e82cd-162">FileType</span><span class="sxs-lookup"><span data-stu-id="e82cd-162">FileType</span></span>
* <span data-ttu-id="e82cd-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="e82cd-163">FolderName</span></span>
* <span data-ttu-id="e82cd-164">FileName</span><span class="sxs-lookup"><span data-stu-id="e82cd-164">FileName</span></span>
* <span data-ttu-id="e82cd-165">ETag (un identificador de la versión del archivo, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="e82cd-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="e82cd-166">Uso del desencadenador</span><span class="sxs-lookup"><span data-stu-id="e82cd-166">Trigger usage</span></span>
<span data-ttu-id="e82cd-167">En funciones de C#, se enlazan los datos de archivo de entrada de toohello mediante un parámetro con nombre de la firma de función, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="e82cd-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="e82cd-168">Donde `T` es la que desea que toodeserialize Hola datos, el tipo de datos de Hola y `paramName` es nombre hello especificado en el [desencadenar JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="e82cd-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="e82cd-169">En las funciones de Node.js, se obtiene acceso mediante datos de archivo de entrada de hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e82cd-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e82cd-170">archivo Hello se puede deserializar en cualquiera de los siguientes tipos de hello:</span><span class="sxs-lookup"><span data-stu-id="e82cd-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="e82cd-171">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos de archivos serializados mediante JSON.</span><span class="sxs-lookup"><span data-stu-id="e82cd-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="e82cd-172">Si se declara un tipo de entrada personalizado (p. ej. `FooType`), las funciones de Azure intenta datos JSON de toodeserialize hello en el tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="e82cd-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="e82cd-173">Cadena: útil para los datos de archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="e82cd-173">String - useful for text file data.</span></span>

<span data-ttu-id="e82cd-174">En funciones de C#, también puede enlazar tooany de los siguientes tipos de Hola y en tiempo de ejecución de funciones de hello intenta deserializar los datos de archivo hello mediante ese tipo:</span><span class="sxs-lookup"><span data-stu-id="e82cd-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="e82cd-175">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="e82cd-175">Trigger sample</span></span>
<span data-ttu-id="e82cd-176">Suponga que tiene Hola después function.json, que define un desencadenador de archivo externo:</span><span class="sxs-lookup"><span data-stu-id="e82cd-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="e82cd-177">Vea el ejemplo específico del idioma de Hola que registra el contenido de Hola de cada archivo que se agrega la carpeta supervisada toohello.</span><span class="sxs-lookup"><span data-stu-id="e82cd-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="e82cd-178">C#</span><span class="sxs-lookup"><span data-stu-id="e82cd-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e82cd-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="e82cd-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="e82cd-180">Uso del desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="e82cd-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="e82cd-181">Uso del desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="e82cd-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="e82cd-182">Enlace de entrada de archivo externo</span><span class="sxs-lookup"><span data-stu-id="e82cd-182">External File input binding</span></span>
<span data-ttu-id="e82cd-183">enlace de entrada de archivo externo Azure Hola permite toouse un archivo desde una carpeta en la función externa.</span><span class="sxs-lookup"><span data-stu-id="e82cd-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="e82cd-184">función de entrada tooa archivo externo Hello usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="e82cd-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="e82cd-185">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e82cd-185">Note hello following:</span></span>

* <span data-ttu-id="e82cd-186">`path`debe contener el nombre de la carpeta de Hola y el nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e82cd-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="e82cd-187">Por ejemplo, si tiene un [desencadenador cola](functions-bindings-storage-queue.md) en la función, puede usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa archivo Hola `samples-workitems` carpeta con un nombre que coincida con el nombre de archivo de hello especificado en el mensaje de bienvenida de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="e82cd-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="e82cd-188">Uso de entradas</span><span class="sxs-lookup"><span data-stu-id="e82cd-188">Input usage</span></span>
<span data-ttu-id="e82cd-189">En funciones de C#, se enlazan los datos de archivo de entrada de toohello mediante un parámetro con nombre de la firma de función, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="e82cd-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="e82cd-190">Donde `T` es la que desea que toodeserialize Hola datos, el tipo de datos de Hola y `paramName` es nombre hello especificado en el [enlace de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="e82cd-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="e82cd-191">En las funciones de Node.js, se obtiene acceso mediante datos de archivo de entrada de hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e82cd-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e82cd-192">archivo Hello se puede deserializar en cualquiera de los siguientes tipos de hello:</span><span class="sxs-lookup"><span data-stu-id="e82cd-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="e82cd-193">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos de archivos serializados mediante JSON.</span><span class="sxs-lookup"><span data-stu-id="e82cd-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="e82cd-194">Si se declara un tipo de entrada personalizado (p. ej. `InputType`), las funciones de Azure intenta datos JSON de toodeserialize hello en el tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="e82cd-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="e82cd-195">Cadena: útil para los datos de archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="e82cd-195">String - useful for text file data.</span></span>

<span data-ttu-id="e82cd-196">En funciones de C#, también puede enlazar tooany de los siguientes tipos de Hola y en tiempo de ejecución de funciones de hello intenta deserializar los datos de archivo hello mediante ese tipo:</span><span class="sxs-lookup"><span data-stu-id="e82cd-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="e82cd-197">Enlace de salida de archivo externo</span><span class="sxs-lookup"><span data-stu-id="e82cd-197">External File output binding</span></span>
<span data-ttu-id="e82cd-198">Hello Azure archivo externo de salida enlace permite carpeta externo tooan de toowrite archivos en la función.</span><span class="sxs-lookup"><span data-stu-id="e82cd-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="e82cd-199">archivo externo Hola de salida para una función usa Hola siguientes objetos JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="e82cd-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="e82cd-200">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e82cd-200">Note hello following:</span></span>

* <span data-ttu-id="e82cd-201">`path`debe contener el nombre de la carpeta de Hola y Hola toowrite de nombre de archivo a.</span><span class="sxs-lookup"><span data-stu-id="e82cd-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="e82cd-202">Por ejemplo, si tiene un [desencadenador cola](functions-bindings-storage-queue.md) en la función, puede usar `"path": "samples-workitems/{queueTrigger}"` toopoint tooa archivo Hola `samples-workitems` carpeta con un nombre que coincida con el nombre de archivo de hello especificado en el mensaje de bienvenida de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="e82cd-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="e82cd-203">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="e82cd-203">Output usage</span></span>
<span data-ttu-id="e82cd-204">En funciones de C#, enlazar toohello archivo de salida mediante el uso de hello denominado `out` como parámetro en la firma de la función, `out <T> <name>`, donde `T` es de tipo de datos de Hola que desea tooserialize Hola datos, y `paramName` es Hola nombre se especifica en el [el enlace de salida](#output).</span><span class="sxs-lookup"><span data-stu-id="e82cd-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="e82cd-205">En las funciones de Node.js, se obtiene acceso mediante archivo de salida de hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e82cd-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e82cd-206">Puede escribir el archivo de salida de toohello mediante cualquiera de los siguientes tipos de hello:</span><span class="sxs-lookup"><span data-stu-id="e82cd-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="e82cd-207">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para la serialización mediante JSON.</span><span class="sxs-lookup"><span data-stu-id="e82cd-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="e82cd-208">Si se declara un tipo de resultado personalizado (p. ej. `out OutputType paramName`), las funciones de Azure intenta tooserialize objeto a JSON.</span><span class="sxs-lookup"><span data-stu-id="e82cd-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="e82cd-209">Si el parámetro de salida de hello es null cuando sale de la función hello, en tiempo de ejecución de funciones de hello crea un archivo como un objeto null.</span><span class="sxs-lookup"><span data-stu-id="e82cd-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="e82cd-210">Cadena: (`out string paramName`) útil para los datos de archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="e82cd-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="e82cd-211">en tiempo de ejecución de funciones de Hello crea un archivo sólo si el parámetro de cadena es distinto de null cuando sale de la función hello.</span><span class="sxs-lookup"><span data-stu-id="e82cd-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="e82cd-212">En las funciones de C# también puede generar tooany de hello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="e82cd-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="e82cd-213">Ejemplo de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="e82cd-213">Input + Output sample</span></span>
<span data-ttu-id="e82cd-214">Suponga que tiene Hola después function.json, que define un [desencadenador de cola de almacenamiento](functions-bindings-storage-queue.md), un archivo externo de entrada y salida de un archivo externo:</span><span class="sxs-lookup"><span data-stu-id="e82cd-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="e82cd-215">Vea el ejemplo de específica del lenguaje de Hola que copia el archivo de salida de hello archivo de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="e82cd-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="e82cd-216">C#</span><span class="sxs-lookup"><span data-stu-id="e82cd-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="e82cd-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="e82cd-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="e82cd-218">Uso en C#</span><span class="sxs-lookup"><span data-stu-id="e82cd-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="e82cd-219">Uso en Node.js</span><span class="sxs-lookup"><span data-stu-id="e82cd-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="e82cd-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e82cd-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
