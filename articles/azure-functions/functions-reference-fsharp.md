---
title: Referencia para desarrolladores de F# de Azure Functions | Microsoft Docs
description: "Cómo desarrollar Azure Functions usando F#."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, cálculo dinámico, architecture sin servidor, F #"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1691d378263f6b4ce5072f5c621d8db02f774b5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="32a33-104">Referencia para desarrolladores de F# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="32a33-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32a33-105">Script de C#</span><span class="sxs-lookup"><span data-stu-id="32a33-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="32a33-106">Script de F#</span><span class="sxs-lookup"><span data-stu-id="32a33-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="32a33-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="32a33-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="32a33-108">F# para Azure Functions es una solución para ejecutar fácilmente pequeños fragmentos de código, o "funciones", en la nube.</span><span class="sxs-lookup"><span data-stu-id="32a33-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="32a33-109">Los datos fluyen en la función de F# a través de los argumentos de función.</span><span class="sxs-lookup"><span data-stu-id="32a33-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="32a33-110">Los nombres de los argumentos se especifican en `function.json`, y hay nombres predefinidos para acceder a cosas como el registrador de funciones y los tokens de cancelación.</span><span class="sxs-lookup"><span data-stu-id="32a33-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="32a33-111">En este artículo se supone que ya ha leído [Referencia para desarrolladores de Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="32a33-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="32a33-112">Cómo funciona .fsx</span><span class="sxs-lookup"><span data-stu-id="32a33-112">How .fsx works</span></span>
<span data-ttu-id="32a33-113">Un archivo `.fsx` es un script de F#.</span><span class="sxs-lookup"><span data-stu-id="32a33-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="32a33-114">Se puede considerar como un proyecto de F# que se encuentra en un único archivo.</span><span class="sxs-lookup"><span data-stu-id="32a33-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="32a33-115">El archivo contiene el código de programa (en este caso, Azure Function) y las directivas para la administración de dependencias.</span><span class="sxs-lookup"><span data-stu-id="32a33-115">The file contains both the code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="32a33-116">Cuando se usa un `.fsx` para Azure Function, normalmente se incluyen automáticamente los ensamblados necesarios, esto le permite a usted centrarse en la función en lugar de en códigos "reutilizables".</span><span class="sxs-lookup"><span data-stu-id="32a33-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you to focus on the function rather than "boilerplate" code.</span></span>

## <a name="binding-to-arguments"></a><span data-ttu-id="32a33-117">Enlace a argumentos</span><span class="sxs-lookup"><span data-stu-id="32a33-117">Binding to arguments</span></span>
<span data-ttu-id="32a33-118">Cada enlace admite un conjunto de argumentos, como se detalla en [Referencias para desarrolladores de desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="32a33-118">Each binding supports some set of arguments, as detailed in the [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="32a33-119">Por ejemplo, uno de los enlaces de argumento que un desencadenador de blob admite es un POCO, que se puede expresar utilizando un registro de F#.</span><span class="sxs-lookup"><span data-stu-id="32a33-119">For example, one of the argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="32a33-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="32a33-121">La F# de Azure Functions tendrá uno o más argumentos.</span><span class="sxs-lookup"><span data-stu-id="32a33-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="32a33-122">Al hablar de los argumentos de Azure Functions, se hace referencia a argumentos de *entrada* y argumentos de *salida*.</span><span class="sxs-lookup"><span data-stu-id="32a33-122">When we talk about Azure Functions arguments, we refer to *input* arguments and *output* arguments.</span></span> <span data-ttu-id="32a33-123">Un argumento de entrada es exactamente eso: una entrada a la F# de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="32a33-123">An input argument is exactly what it sounds like: input to your F# Azure Function.</span></span> <span data-ttu-id="32a33-124">Un argumento de *salida* es una serie de datos mutables o un argumento `byref<>` que sirve para volver a pasar datos de *salida* de la función.</span><span class="sxs-lookup"><span data-stu-id="32a33-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way to pass data back *out* of your function.</span></span>

<span data-ttu-id="32a33-125">En el ejemplo anterior, `blob` es un argumento de entrada, y `output` es un argumento de salida.</span><span class="sxs-lookup"><span data-stu-id="32a33-125">In the example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="32a33-126">Observe que hemos usado `byref<>` para `output` (no es necesario agregar la anotación `[<Out>]`).</span><span class="sxs-lookup"><span data-stu-id="32a33-126">Notice that we used `byref<>` for `output` (there's no need to add the `[<Out>]` annotation).</span></span> <span data-ttu-id="32a33-127">El uso de un tipo `byref<>` permite a la función cambiar el registro u objeto al que hace referencia el argumento.</span><span class="sxs-lookup"><span data-stu-id="32a33-127">Using a `byref<>` type allows your function to change which record or object the argument refers to.</span></span>

<span data-ttu-id="32a33-128">Cuando se utiliza un registro de F# como un tipo de entrada, la definición de registro tiene que marcarse con `[<CLIMutable>]` para permitir que el marco de Azure Functions establezca los campos de forma adecuada antes de pasar el registro a la función.</span><span class="sxs-lookup"><span data-stu-id="32a33-128">When an F# record is used as an input type, the record definition must be marked with `[<CLIMutable>]` in order to allow the Azure Functions framework to set the fields appropriately before passing the record to your function.</span></span> <span data-ttu-id="32a33-129">Internamente, `[<CLIMutable>]` genera métodos establecedores para las propiedades de registro.</span><span class="sxs-lookup"><span data-stu-id="32a33-129">Under the hood, `[<CLIMutable>]` generates setters for the record properties.</span></span> <span data-ttu-id="32a33-130">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="32a33-131">También puede utilizarse una clase F# tanto para argumentos de entrada como de salida.</span><span class="sxs-lookup"><span data-stu-id="32a33-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="32a33-132">Para una clase, las propiedades normalmente necesitan captadores y establecedores.</span><span class="sxs-lookup"><span data-stu-id="32a33-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="32a33-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="32a33-134">Registro</span><span class="sxs-lookup"><span data-stu-id="32a33-134">Logging</span></span>
<span data-ttu-id="32a33-135">Para registrar la salida en los [registros de streaming](../app-service-web/web-sites-streaming-logs-and-console.md) en F#, la función debe adoptar un argumento de tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="32a33-135">To log output to your [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="32a33-136">Por coherencia, se recomienda que se le dé el nombre `log`a este argumento.</span><span class="sxs-lookup"><span data-stu-id="32a33-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="32a33-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="32a33-138">Async</span><span class="sxs-lookup"><span data-stu-id="32a33-138">Async</span></span>
<span data-ttu-id="32a33-139">Se puede usar el flujo de trabajo `async`, pero el resultado tiene que devolver una `Task`.</span><span class="sxs-lookup"><span data-stu-id="32a33-139">The `async` workflow can be used, but the result needs to return a `Task`.</span></span> <span data-ttu-id="32a33-140">Esto puede hacerse con `Async.StartAsTask`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="32a33-141">Token de cancelación</span><span class="sxs-lookup"><span data-stu-id="32a33-141">Cancellation Token</span></span>
<span data-ttu-id="32a33-142">Si la función tiene que controlar el apagado correctamente, puede darle un argumento [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) .</span><span class="sxs-lookup"><span data-stu-id="32a33-142">If your function needs to handle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="32a33-143">Esto se puede combinar con `async`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="32a33-144">Importación de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="32a33-144">Importing namespaces</span></span>
<span data-ttu-id="32a33-145">Los espacios de nombres se pueden abrir en la manera habitual:</span><span class="sxs-lookup"><span data-stu-id="32a33-145">Namespaces can be opened in the usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="32a33-146">Los siguientes espacios de nombres se abren automáticamente:</span><span class="sxs-lookup"><span data-stu-id="32a33-146">The following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="32a33-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="32a33-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="32a33-148">Referencia a ensamblados externos</span><span class="sxs-lookup"><span data-stu-id="32a33-148">Referencing External Assemblies</span></span>
<span data-ttu-id="32a33-149">De forma similar, las referencias del ensamblado de Framework se agregan con la directiva `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="32a33-149">Similarly, framework assembly references be added with the `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="32a33-150">El entorno de hospedaje de las Funciones de Azure agrega automáticamente los siguientes ensamblados:</span><span class="sxs-lookup"><span data-stu-id="32a33-150">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

* <span data-ttu-id="32a33-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="32a33-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="32a33-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="32a33-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="32a33-153">Además, en los siguientes ensamblados se hace un uso especial de las mayúsculas y minúsculas y se puede hacer referencia a ellos con SimpleName (por ejemplo, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="32a33-153">In addition, the following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="32a33-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="32a33-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="32a33-155">Si necesita hacer referencia a un ensamblado privado, puede cargar el archivo de ensamblado en una carpeta `bin` relacionada con la función y hacer referencia a él mediante el nombre de archivo (por ejemplo, `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="32a33-155">If you need to reference a private assembly, you can upload the assembly file into a `bin` folder relative to your function and reference it by using the file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="32a33-156">Para más información acerca de cómo cargar archivos en su carpeta de función, consulte la sección siguiente sobre administración de paquetes.</span><span class="sxs-lookup"><span data-stu-id="32a33-156">For information on how to upload files to your function folder, see the following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="32a33-157">Preludio del editor</span><span class="sxs-lookup"><span data-stu-id="32a33-157">Editor Prelude</span></span>
<span data-ttu-id="32a33-158">Un editor que admita F# Compiler Services no será consciente de los espacios de nombres y ensamblados que Azure Functions incluye automáticamente.</span><span class="sxs-lookup"><span data-stu-id="32a33-158">An editor that supports F# Compiler Services will not be aware of the namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="32a33-159">Por lo tanto, puede resultar útil incluir un preludio que ayude al editor a encontrar los ensamblados que esté utilizando y a abrir explícitamente los espacios de nombre.</span><span class="sxs-lookup"><span data-stu-id="32a33-159">As such, it can be useful to include a prelude that helps the editor find the assemblies you are using, and to explicitly open namespaces.</span></span> <span data-ttu-id="32a33-160">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-160">For example:</span></span>

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

<span data-ttu-id="32a33-161">Cuando Azure Functions ejecuta el código, procesa el origen con `COMPILED` definido, por lo que se omitirá el preludio del editor.</span><span class="sxs-lookup"><span data-stu-id="32a33-161">When Azure Functions executes your code, it processes the source with `COMPILED` defined, so the editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="32a33-162">Administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="32a33-162">Package management</span></span>
<span data-ttu-id="32a33-163">Para utilizar paquetes de NuGet en una función de F#, agregue un archivo `project.json` a la carpeta de la función en el sistema de archivos de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="32a33-163">To use NuGet packages in an F# function, add a `project.json` file to the the function's folder in the function app's file system.</span></span> <span data-ttu-id="32a33-164">Este es un ejemplo de archivo `project.json` que agrega una referencia de paquetes de NuGet a `Microsoft.ProjectOxford.Face` versión 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="32a33-164">Here is an example `project.json` file that adds a NuGet package reference to `Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="32a33-165">Solo se admite .NET Framework 4.6, así que asegúrese de que su archivo `project.json` especifique `net46` como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="32a33-165">Only the .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="32a33-166">Al cargar un archivo `project.json` , el sistema en tiempo de ejecución obtiene los paquetes y agrega automáticamente las referencias a sus ensamblados.</span><span class="sxs-lookup"><span data-stu-id="32a33-166">When you upload a `project.json` file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="32a33-167">No es necesario agregar directivas `#r "AssemblyName"` .</span><span class="sxs-lookup"><span data-stu-id="32a33-167">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="32a33-168">Simplemente agregue las instrucciones `open` al archivo `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="32a33-168">Just add the required `open` statements to your `.fsx` file.</span></span>

<span data-ttu-id="32a33-169">Puede que desee colocar automáticamente ensamblados de referencias en el preludio del editor, para mejorar la interacción de su editor con F# Compiler Services.</span><span class="sxs-lookup"><span data-stu-id="32a33-169">You may wish to put automatically references assemblies in your editor prelude, to improve your editor's interaction with F# Compile Services.</span></span>

### <a name="how-to-add-a-projectjson-file-to-your-azure-function"></a><span data-ttu-id="32a33-170">Cómo agregar un archivo `project.json` a Azure Functions</span><span class="sxs-lookup"><span data-stu-id="32a33-170">How to add a `project.json` file to your Azure Function</span></span>
1. <span data-ttu-id="32a33-171">En primer lugar, asegúrese de que la aplicación de la función se está ejecutando, lo que puede hacer abriéndola en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="32a33-171">Begin by making sure your function app is running, which you can do by opening your function in the Azure portal.</span></span> <span data-ttu-id="32a33-172">Esto también proporciona acceso a los registros de streaming donde se mostrará la salida de la instalación del paquete.</span><span class="sxs-lookup"><span data-stu-id="32a33-172">This also gives access to the streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="32a33-173">Para cargar un archivo `project.json` , utilice uno de los métodos descritos en [Actualización de los archivos de aplicación de función](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="32a33-173">To upload a `project.json` file, use one of the methods described in [how to update function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="32a33-174">Si se usa [Implementación continua para Azure Functions](functions-continuous-deployment.md), se puede agregar un archivo `project.json` a la rama de ensayo para experimentar con él antes de agregarlo a la rama de implementación.</span><span class="sxs-lookup"><span data-stu-id="32a33-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file to your staging branch in order to experiment with it before adding it to your deployment branch.</span></span>
3. <span data-ttu-id="32a33-175">Una vez cargado el archivo `project.json` , verá un resultado similar al del ejemplo siguiente en el registro de streaming de la función:</span><span class="sxs-lookup"><span data-stu-id="32a33-175">After the `project.json` file is added, you will see output similar to the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="32a33-176">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="32a33-176">Environment variables</span></span>
<span data-ttu-id="32a33-177">Para obtener una variable de entorno o un valor de configuración de aplicación, use `System.Environment.GetEnvironmentVariable`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-177">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="32a33-178">Reutilización del código .fsx</span><span class="sxs-lookup"><span data-stu-id="32a33-178">Reusing .fsx code</span></span>
<span data-ttu-id="32a33-179">Puede utilizar el código de otros archivos `.fsx` mediante una directiva `#load`.</span><span class="sxs-lookup"><span data-stu-id="32a33-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="32a33-180">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="32a33-180">For example:</span></span>

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

<span data-ttu-id="32a33-181">Las rutas de acceso a la directiva `#load` son relativas a la ubicación del archivo `.fsx`.</span><span class="sxs-lookup"><span data-stu-id="32a33-181">Paths provides to the `#load` directive are relative to the location of your `.fsx` file.</span></span>

* <span data-ttu-id="32a33-182">`#load "logger.fsx"` carga un archivo que se encuentra en la carpeta de la función.</span><span class="sxs-lookup"><span data-stu-id="32a33-182">`#load "logger.fsx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="32a33-183">`#load "package\logger.fsx"` carga un archivo que se encuentra en la carpeta `package` dentro de la carpeta de la función.</span><span class="sxs-lookup"><span data-stu-id="32a33-183">`#load "package\logger.fsx"` loads a file located in the `package` folder in the function folder.</span></span>
* <span data-ttu-id="32a33-184">`#load "..\shared\mylogger.fsx"` carga un archivo ubicado en la carpeta `shared` al mismo nivel que la carpeta de la función, es decir, directamente en `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="32a33-184">`#load "..\shared\mylogger.fsx"` loads a file located in the `shared` folder at the same level as the function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="32a33-185">La directiva `#load` solo funciona con archivos `.fsx` (script de F#) y no con archivos `.fs`.</span><span class="sxs-lookup"><span data-stu-id="32a33-185">The `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32a33-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32a33-186">Next steps</span></span>
<span data-ttu-id="32a33-187">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="32a33-187">For more information, see the following resources:</span></span>

* [<span data-ttu-id="32a33-188">Guía de F#</span><span class="sxs-lookup"><span data-stu-id="32a33-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="32a33-189">Procedimientos recomendados de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="32a33-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="32a33-190">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="32a33-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="32a33-191">Referencia para desarrolladores de C# de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="32a33-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="32a33-192">Referencia para desarrolladores de NodeJS de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="32a33-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="32a33-193">Enlaces y desencadenadores de las Funciones de azure</span><span class="sxs-lookup"><span data-stu-id="32a33-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="32a33-194">Prueba de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="32a33-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="32a33-195">Escalado de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="32a33-195">Azure Functions scaling</span></span>](functions-scale.md)

