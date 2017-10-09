---
title: 'aaaAzure material de referencia de funciones F # | Documentos de Microsoft'
description: "Comprender cómo toodevelop funciones de Azure con F #."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure Functions, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor, F#"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="14585-104">Referencia para desarrolladores de F# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="14585-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14585-105">Script de C#</span><span class="sxs-lookup"><span data-stu-id="14585-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="14585-106">Script de F#</span><span class="sxs-lookup"><span data-stu-id="14585-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="14585-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="14585-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="14585-108">F # para las funciones de Azure es una solución para ejecutar fácilmente pequeños fragmentos de código, o "funciones", en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="14585-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="14585-109">Los datos fluyen en la función de F# a través de los argumentos de función.</span><span class="sxs-lookup"><span data-stu-id="14585-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="14585-110">Nombres de los argumentos se especifican en `function.json`, y hay nombres predefinidos para tener acceso a acciones como Hola función registrador y tokens de cancelación.</span><span class="sxs-lookup"><span data-stu-id="14585-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="14585-111">En este artículo se da por supuesto que ya ha leído hello [material de referencia de funciones de Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="14585-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="14585-112">Cómo funciona .fsx</span><span class="sxs-lookup"><span data-stu-id="14585-112">How .fsx works</span></span>
<span data-ttu-id="14585-113">Un archivo `.fsx` es un script de F#.</span><span class="sxs-lookup"><span data-stu-id="14585-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="14585-114">Se puede considerar como un proyecto de F# que se encuentra en un único archivo.</span><span class="sxs-lookup"><span data-stu-id="14585-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="14585-115">archivo Hello contiene código hello para el programa (en este caso, la función de Azure) y directivas para administrar las dependencias.</span><span class="sxs-lookup"><span data-stu-id="14585-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="14585-116">Cuando se usa un `.fsx` para una función de Azure, normalmente requiere ensamblados se incluyen automáticamente para usted, lo que le toofocus en el código de función en lugar de "reutilizable" Hola.</span><span class="sxs-lookup"><span data-stu-id="14585-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="14585-117">Enlace tooarguments</span><span class="sxs-lookup"><span data-stu-id="14585-117">Binding tooarguments</span></span>
<span data-ttu-id="14585-118">Cada enlace admite un conjunto de argumentos, como Hola detallada en [referencia del programador de desencadenadores y los enlaces de funciones de Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="14585-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="14585-119">Por ejemplo, uno de los enlaces de argumento hello es compatible con un desencadenador de blob es un POCO, que se puede expresar utilizando un registro de F #.</span><span class="sxs-lookup"><span data-stu-id="14585-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="14585-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="14585-121">La F# de Azure Functions tendrá uno o más argumentos.</span><span class="sxs-lookup"><span data-stu-id="14585-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="14585-122">Cuando hablamos sobre los argumentos de las funciones de Azure, nos referimos demasiado*entrada* argumentos y *salida* argumentos.</span><span class="sxs-lookup"><span data-stu-id="14585-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="14585-123">Un argumento de entrada es exactamente lo que parece: entrada tooyour Azure función de F #.</span><span class="sxs-lookup"><span data-stu-id="14585-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="14585-124">Un *salida* argumento es datos mutables o `byref<>` argumento que actúa como una manera toopass de datos nuevo *out* de la función.</span><span class="sxs-lookup"><span data-stu-id="14585-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="14585-125">En el ejemplo de Hola anterior, `blob` es un argumento de entrada, y `output` es un argumento de salida.</span><span class="sxs-lookup"><span data-stu-id="14585-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="14585-126">Observe que utilizamos `byref<>` para `output` (no hay ningún Hola de tooadd necesidad `[<Out>]` anotación).</span><span class="sxs-lookup"><span data-stu-id="14585-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="14585-127">Mediante un `byref<>` su toochange función registro u objeto Hola el argumento que hace referencia a que permite el tipo.</span><span class="sxs-lookup"><span data-stu-id="14585-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="14585-128">Cuando un registro de F # se usa como un tipo de entrada, definición de registro de hello debe estar marcado con `[<CLIMutable>]` en orden tooallow hello Azure funciones framework tooset campos Hola adecuadamente antes de pasar Hola registro tooyour función.</span><span class="sxs-lookup"><span data-stu-id="14585-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="14585-129">Bajo el paraguas de hello, `[<CLIMutable>]` genera establecedores de propiedades de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="14585-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="14585-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="14585-131">También puede utilizarse una clase F# tanto para argumentos de entrada como de salida.</span><span class="sxs-lookup"><span data-stu-id="14585-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="14585-132">Para una clase, las propiedades normalmente necesitan captadores y establecedores.</span><span class="sxs-lookup"><span data-stu-id="14585-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="14585-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="14585-134">Registro</span><span class="sxs-lookup"><span data-stu-id="14585-134">Logging</span></span>
<span data-ttu-id="14585-135">toolog salida tooyour [los registros de streaming](../app-service-web/web-sites-streaming-logs-and-console.md) en F #, la función debe tomar un argumento de tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="14585-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="14585-136">Por coherencia, se recomienda que se le dé el nombre `log`a este argumento.</span><span class="sxs-lookup"><span data-stu-id="14585-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="14585-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="14585-138">Async</span><span class="sxs-lookup"><span data-stu-id="14585-138">Async</span></span>
<span data-ttu-id="14585-139">Hola `async` puede utilizarse el flujo de trabajo, pero el resultado de hello debe tooreturn un `Task`.</span><span class="sxs-lookup"><span data-stu-id="14585-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="14585-140">Esto puede hacerse con `Async.StartAsTask`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="14585-141">Token de cancelación</span><span class="sxs-lookup"><span data-stu-id="14585-141">Cancellation Token</span></span>
<span data-ttu-id="14585-142">Si la función necesita toohandle cierre correctamente, puede asignarle un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumento.</span><span class="sxs-lookup"><span data-stu-id="14585-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="14585-143">Esto se puede combinar con `async`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="14585-144">Importación de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="14585-144">Importing namespaces</span></span>
<span data-ttu-id="14585-145">Espacios de nombres se pueden abrir en hello forma habitual:</span><span class="sxs-lookup"><span data-stu-id="14585-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="14585-146">Hola después de los espacios de nombres se abre automáticamente:</span><span class="sxs-lookup"><span data-stu-id="14585-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="14585-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="14585-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="14585-148">Referencia a ensamblados externos</span><span class="sxs-lookup"><span data-stu-id="14585-148">Referencing External Assemblies</span></span>
<span data-ttu-id="14585-149">De forma similar, el ensamblado de framework se agregan las referencias con hello `#r "AssemblyName"` directiva.</span><span class="sxs-lookup"><span data-stu-id="14585-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="14585-150">Hello siguientes ensamblados se agregan automáticamente las funciones de Azure Hola entorno de hospedaje:</span><span class="sxs-lookup"><span data-stu-id="14585-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="14585-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="14585-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="14585-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="14585-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="14585-153">Además, es especial Hola siguientes ensamblados las mayúsculas y minúsculas y puede hacer referencia mediante simplename (p. ej. `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="14585-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="14585-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="14585-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="14585-155">Si necesita tooreference un ensamblado privado, puede cargar el archivo de ensamblado de hello en un `bin` referencia mediante Hola (por ejemplo, nombre de archivo y función de carpeta tooyour relativa  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="14585-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="14585-156">Para obtener información sobre cómo los archivos de carpeta de la función tooyour tooupload, vea Hola siguiendo la sección sobre administración de paquetes.</span><span class="sxs-lookup"><span data-stu-id="14585-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="14585-157">Preludio del editor</span><span class="sxs-lookup"><span data-stu-id="14585-157">Editor Prelude</span></span>
<span data-ttu-id="14585-158">Un editor compatible con servicios de compilador de F # no tendrá constancia de espacios de nombres de Hola y ensamblados que se incluye automáticamente las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="14585-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="14585-159">Por lo tanto, puede ser útil tooinclude un paso previo que ayuda a editor Hola buscar ensamblados de Hola que utilice y tooexplicitly abrir espacios de nombres.</span><span class="sxs-lookup"><span data-stu-id="14585-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="14585-160">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-160">For example:</span></span>

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

<span data-ttu-id="14585-161">Cuando las funciones de Azure se ejecuta el código, lo procesa origen Hola con `COMPILED` definido, por lo que se pasará por alto preludio de editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="14585-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="14585-162">Administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="14585-162">Package management</span></span>
<span data-ttu-id="14585-163">paquetes de NuGet toouse en una función de F #, agregue un `project.json` carpeta de la función de toohello Hola de archivos en el sistema de archivos de la aplicación de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="14585-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="14585-164">Este es un ejemplo `project.json` archivo que agrega una referencia de paquete de NuGet demasiado`Microsoft.ProjectOxford.Face` versión 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="14585-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

<span data-ttu-id="14585-165">Solo hello .NET Framework 4.6 es compatible, por lo tanto asegúrese de que su `project.json` archivo especifica `net46` como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="14585-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="14585-166">Al cargar un `project.json` de archivos, obtiene los paquetes de saludo hello en tiempo de ejecución y agrega automáticamente los ensamblados del paquete toohello referencias.</span><span class="sxs-lookup"><span data-stu-id="14585-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="14585-167">No es necesario tooadd `#r "AssemblyName"` directivas.</span><span class="sxs-lookup"><span data-stu-id="14585-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="14585-168">Basta con agregar Hola necesario `open` instrucciones tooyour `.fsx` archivo.</span><span class="sxs-lookup"><span data-stu-id="14585-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="14585-169">Es recomendable tooput hará referencia automáticamente a los ensamblados en su preludio de editor, tooimprove interacción de su editor con servicios de compilación de F #.</span><span class="sxs-lookup"><span data-stu-id="14585-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="14585-170">¿Cómo tooadd un `project.json` archivo tooyour Azure (función)</span><span class="sxs-lookup"><span data-stu-id="14585-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="14585-171">BEGIN asegurándose de que la aplicación de la función se está ejecutando, lo que puede hacer abriendo la función de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="14585-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="14585-172">Esto también proporciona acceso toohello los registros de streaming donde se mostrará la salida de instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="14585-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="14585-173">tooupload una `project.json` de archivos, utilice uno de los métodos de hello descritos en [forma en que funcionan los archivos de aplicación tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="14585-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="14585-174">Si utilizas [implementación continua para las funciones de Azure](functions-continuous-deployment.md), puede agregar un `project.json` tooyour rama en orden tooexperiment con él antes de agregarlo tooyour rama de implementación de almacenamiento provisional de archivos.</span><span class="sxs-lookup"><span data-stu-id="14585-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="14585-175">Después de hello `project.json` se agrega el archivo, verá toohello similar de salida siguiente ejemplo en la función de streaming del registro:</span><span class="sxs-lookup"><span data-stu-id="14585-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a><span data-ttu-id="14585-176">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="14585-176">Environment variables</span></span>
<span data-ttu-id="14585-177">tooget una variable de entorno o un valor de configuración de aplicación, utilice `System.Environment.GetEnvironmentVariable`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="14585-178">Reutilización del código .fsx</span><span class="sxs-lookup"><span data-stu-id="14585-178">Reusing .fsx code</span></span>
<span data-ttu-id="14585-179">Puede utilizar el código de otros archivos `.fsx` mediante una directiva `#load`.</span><span class="sxs-lookup"><span data-stu-id="14585-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="14585-180">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14585-180">For example:</span></span>

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

<span data-ttu-id="14585-181">Las rutas de acceso proporciona toohello `#load` directiva son ubicación relativa toohello de su `.fsx` archivo.</span><span class="sxs-lookup"><span data-stu-id="14585-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="14585-182">`#load "logger.fsx"`carga un archivo que se encuentra en la carpeta de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="14585-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="14585-183">`#load "package\logger.fsx"`carga un archivo que se encuentra en hello `package` carpeta en la carpeta de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="14585-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="14585-184">`#load "..\shared\mylogger.fsx"`carga un archivo que se encuentra en hello `shared` carpeta en el mismo nivel como carpeta de la función de hello, es decir, el Hola directamente bajo `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="14585-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="14585-185">Hola `#load` directiva solo funciona con `.fsx` archivos (script de F #) y no con `.fs` archivos.</span><span class="sxs-lookup"><span data-stu-id="14585-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14585-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14585-186">Next steps</span></span>
<span data-ttu-id="14585-187">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="14585-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="14585-188">Guía de F#</span><span class="sxs-lookup"><span data-stu-id="14585-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="14585-189">Procedimientos recomendados de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="14585-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="14585-190">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="14585-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="14585-191">Referencia para desarrolladores de C# de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="14585-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="14585-192">Referencia para desarrolladores de NodeJS de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="14585-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="14585-193">Enlaces y desencadenadores de las Funciones de azure</span><span class="sxs-lookup"><span data-stu-id="14585-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="14585-194">Prueba de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="14585-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="14585-195">Escalado de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="14585-195">Azure Functions scaling</span></span>](functions-scale.md)

