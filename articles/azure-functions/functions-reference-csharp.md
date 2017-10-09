---
title: aaaAzure material de referencia de funciones C# Script | Documentos de Microsoft
description: "Comprender cómo toodevelop las funciones de Azure mediante C#."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="6223e-104">Referencia para desarrolladores de scripts de C# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6223e-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6223e-105">Script de C#</span><span class="sxs-lookup"><span data-stu-id="6223e-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="6223e-106">Script de F#</span><span class="sxs-lookup"><span data-stu-id="6223e-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="6223e-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="6223e-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="6223e-108">Hola experiencia en C# script para las funciones de Azure se basa en hello SDK de WebJobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="6223e-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="6223e-109">Los datos fluyen en la función de C# a través de los argumentos de método.</span><span class="sxs-lookup"><span data-stu-id="6223e-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="6223e-110">Nombres de los argumentos se especifican en `function.json`, y hay nombres predefinidos para tener acceso a acciones como Hola función registrador y tokens de cancelación.</span><span class="sxs-lookup"><span data-stu-id="6223e-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="6223e-111">En este artículo se da por supuesto que ya ha leído hello [material de referencia de funciones de Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="6223e-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="6223e-112">Para obtener información sobre el uso de las bibliotecas de clases de C#, vea [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (Uso de bibliotecas de clases de .NET con Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="6223e-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="6223e-113">Funcionamiento de .csx</span><span class="sxs-lookup"><span data-stu-id="6223e-113">How .csx works</span></span>
<span data-ttu-id="6223e-114">Hola `.csx` formato permite toowrite menos "reutilizable" y centrarse en la escritura simplemente una función de C#.</span><span class="sxs-lookup"><span data-stu-id="6223e-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="6223e-115">Incluir las referencias a ensamblados y espacios de nombres al principio de Hola de archivo hello como de costumbre.</span><span class="sxs-lookup"><span data-stu-id="6223e-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="6223e-116">En lugar de encapsular todo en un espacio de nombres y una clase, defina solamente un método `Run`.</span><span class="sxs-lookup"><span data-stu-id="6223e-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="6223e-117">Si necesita tooinclude todas las clases, para objetos de objetos CLR antiguos (POCO), puede incluir una clase dentro de instancia toodefine simple Hola mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="6223e-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="6223e-118">Enlace tooarguments</span><span class="sxs-lookup"><span data-stu-id="6223e-118">Binding tooarguments</span></span>
<span data-ttu-id="6223e-119">Hello varios enlaces son función dependiente tooa C# a través de hello `name` propiedad Hola *function.json* configuración.</span><span class="sxs-lookup"><span data-stu-id="6223e-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="6223e-120">Cada enlace tiene sus propios tipos admitidos; por ejemplo, un desencadenador de blob puede admitir una cadena, un objeto POCO o un CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="6223e-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="6223e-121">tipos de Hello admitida se documentan en referencia de Hola para cada enlace.</span><span class="sxs-lookup"><span data-stu-id="6223e-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="6223e-122">Un objeto POCO debe tener un captador y establecedor definidos para cada propiedad.</span><span class="sxs-lookup"><span data-stu-id="6223e-122">A POCO object must have a getter and setter defined for each property.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="6223e-123">Uso del valor devuelto del método para el enlace de salida</span><span class="sxs-lookup"><span data-stu-id="6223e-123">Using method return value for output binding</span></span>

<span data-ttu-id="6223e-124">Puede usar un valor devuelto del método de un enlace de salida, utilizando el nombre de hello `$return` en *function.json*:</span><span class="sxs-lookup"><span data-stu-id="6223e-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a><span data-ttu-id="6223e-125">Escribir varios valores de salida</span><span class="sxs-lookup"><span data-stu-id="6223e-125">Writing multiple output values</span></span>

<span data-ttu-id="6223e-126">toowrite tooan de varios valores de salida de enlace, use hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) tipos.</span><span class="sxs-lookup"><span data-stu-id="6223e-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="6223e-127">Estos tipos son colecciones de solo escritura que están toohello escrito el enlace de salida cuando se completa el método hello.</span><span class="sxs-lookup"><span data-stu-id="6223e-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="6223e-128">En este ejemplo se escriben varios mensajes en cola mediante `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="6223e-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="6223e-129">Registro</span><span class="sxs-lookup"><span data-stu-id="6223e-129">Logging</span></span>
<span data-ttu-id="6223e-130">toolog salida tooyour los registros de streaming en C#, incluya un argumento de tipo `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="6223e-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="6223e-131">Es recomendable que lo denomine `log`.</span><span class="sxs-lookup"><span data-stu-id="6223e-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="6223e-132">Evite el uso de `Console.Write` en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="6223e-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="6223e-133">`TraceWriter`se define en hello [SDK de WebJobs de Azure](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="6223e-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="6223e-134">Hola a nivel de registro para `TraceWriter` pueden configurarse en [host\.json].</span><span class="sxs-lookup"><span data-stu-id="6223e-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="6223e-135">Async</span><span class="sxs-lookup"><span data-stu-id="6223e-135">Async</span></span>
<span data-ttu-id="6223e-136">toomake una función asincrónica, usar hello `async` palabra clave y valor devuelto una `Task` objeto.</span><span class="sxs-lookup"><span data-stu-id="6223e-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="6223e-137">Token de cancelación</span><span class="sxs-lookup"><span data-stu-id="6223e-137">Cancellation Token</span></span>
<span data-ttu-id="6223e-138">Algunas operaciones requieren un cierre estable.</span><span class="sxs-lookup"><span data-stu-id="6223e-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="6223e-139">Aunque siempre es mejor código toowrite que puede controlar el bloqueo, en casos donde desea que las solicitudes de apagado ordenado de toohandle, defina un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) con el tipo de argumento.</span><span class="sxs-lookup"><span data-stu-id="6223e-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="6223e-140">Un `CancellationToken` se proporciona toosignal que se desencadena un cierre del host.</span><span class="sxs-lookup"><span data-stu-id="6223e-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="6223e-141">Importación de espacios de nombres</span><span class="sxs-lookup"><span data-stu-id="6223e-141">Importing namespaces</span></span>
<span data-ttu-id="6223e-142">Si necesita tooimport espacios de nombres, puede hacerlo como de costumbre, con hello `using` cláusula.</span><span class="sxs-lookup"><span data-stu-id="6223e-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="6223e-143">Hello siguientes espacios de nombres se importan automáticamente y, por tanto, son opcionales:</span><span class="sxs-lookup"><span data-stu-id="6223e-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="6223e-144">Referencia a ensamblados externos</span><span class="sxs-lookup"><span data-stu-id="6223e-144">Referencing External Assemblies</span></span>
<span data-ttu-id="6223e-145">Para los ensamblados de framework, agregue referencias mediante el uso de hello `#r "AssemblyName"` directiva.</span><span class="sxs-lookup"><span data-stu-id="6223e-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="6223e-146">Hello siguientes ensamblados se agregan automáticamente las funciones de Azure Hola entorno de hospedaje:</span><span class="sxs-lookup"><span data-stu-id="6223e-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="6223e-147">Hello siguientes pueden hacer referencia a ensamblados por nombre simple (por ejemplo, `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="6223e-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="6223e-148">Hacer referencia a ensamblados personalizados</span><span class="sxs-lookup"><span data-stu-id="6223e-148">Referencing custom assemblies</span></span>

<span data-ttu-id="6223e-149">tooreference un ensamblado personalizado, puede usar un *compartido* ensamblado o un *privada* ensamblado:</span><span class="sxs-lookup"><span data-stu-id="6223e-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="6223e-150">Los ensamblados compartidos se comparten en todas las funciones dentro de una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="6223e-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="6223e-151">tooreference un ensamblado personalizado, cargar ensamblado tooyour función aplicación de hello, como en un `bin` carpeta del directorio raíz de aplicación de función de Hola.</span><span class="sxs-lookup"><span data-stu-id="6223e-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="6223e-152">Los ensamblados privados forman parte del contexto de una función determinada y admiten la instalación de prueba de versiones diferentes.</span><span class="sxs-lookup"><span data-stu-id="6223e-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="6223e-153">Se deben cargar ensamblados privados en un `bin` carpeta en el directorio de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="6223e-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="6223e-154">Referencia mediante el nombre de archivo de hello, como `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="6223e-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="6223e-155">Para obtener información sobre cómo los archivos de carpeta de la función tooyour tooupload, vea Hola siguiendo la sección sobre administración de paquetes.</span><span class="sxs-lookup"><span data-stu-id="6223e-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="6223e-156">Directorios inspeccionados</span><span class="sxs-lookup"><span data-stu-id="6223e-156">Watched directories</span></span>

<span data-ttu-id="6223e-157">directorio de Hola que contiene el archivo de script de función hello automáticamente se observa tooassemblies de cambios.</span><span class="sxs-lookup"><span data-stu-id="6223e-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="6223e-158">toowatch cambios de ensamblado en otros directorios, agréguelos toohello `watchDirectories` lista [host\.json].</span><span class="sxs-lookup"><span data-stu-id="6223e-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="6223e-159">Uso de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="6223e-159">Using NuGet packages</span></span>
<span data-ttu-id="6223e-160">cargar paquetes de NuGet toouse en una función de C#, un *project.json* carpeta de la función toohello de archivos en el sistema de archivos de la aplicación de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="6223e-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="6223e-161">Este es un ejemplo *project.json* archivo que se agrega una versión de tooMicrosoft.ProjectOxford.Face 1.1.0 de referencia:</span><span class="sxs-lookup"><span data-stu-id="6223e-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="6223e-162">Solo hello .NET Framework 4.6 es compatible, por lo tanto asegúrese de que su *project.json* archivo especifica `net46` como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="6223e-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="6223e-163">Al cargar un *project.json* de archivos, obtiene los paquetes de saludo hello en tiempo de ejecución y agrega automáticamente los ensamblados del paquete toohello referencias.</span><span class="sxs-lookup"><span data-stu-id="6223e-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="6223e-164">No es necesario tooadd `#r "AssemblyName"` directivas.</span><span class="sxs-lookup"><span data-stu-id="6223e-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="6223e-165">tipos de hello toouse definidos en los paquetes de NuGet hello, agregar Hola necesario `using` instrucciones tooyour *run.csx* archivo</span><span class="sxs-lookup"><span data-stu-id="6223e-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="6223e-166">En tiempo de ejecución de funciones de hello, restauración de NuGet funciona comparando `project.json` y `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="6223e-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="6223e-167">Si Hola marcas de fecha y hora de los archivos de hello **no** una restauración de NuGet de coincidencia, se ejecuta y descargas de NuGet actualizan paquetes.</span><span class="sxs-lookup"><span data-stu-id="6223e-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="6223e-168">Sin embargo, si hello marcas de fecha y hora de los archivos de hello **hacer** coincidencia, NuGet no lleva a cabo una restauración.</span><span class="sxs-lookup"><span data-stu-id="6223e-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="6223e-169">Por lo tanto, `project.lock.json` no deben implementarse como hace que la restauración del paquete NuGet tooskip.</span><span class="sxs-lookup"><span data-stu-id="6223e-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="6223e-170">tooavoid implementar bloqueo hello, agregue hello `project.lock.json` toohello `.gitignore` archivo.</span><span class="sxs-lookup"><span data-stu-id="6223e-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="6223e-171">toouse una fuente de NuGet personalizada, especificar hello de la fuente en un *Nuget.Config* archivo en la raíz de la aplicación de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="6223e-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="6223e-172">Para más información, vea [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Configuración del comportamiento de NuGet).</span><span class="sxs-lookup"><span data-stu-id="6223e-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="6223e-173">Uso de un archivo project.json</span><span class="sxs-lookup"><span data-stu-id="6223e-173">Using a project.json file</span></span>
1. <span data-ttu-id="6223e-174">Abra la función hello en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6223e-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="6223e-175">Hola registra la salida de instalación del paquete de pestaña muestra Hola.</span><span class="sxs-lookup"><span data-stu-id="6223e-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="6223e-176">tooupload un archivo project.json, utilice uno de los métodos de hello descritos en hello [forma en que funcionan los archivos de aplicación tooupdate](functions-reference.md#fileupdate) en el tema de referencia para desarrolladores de hello las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="6223e-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="6223e-177">Después de hello *project.json* archivo se carga, verá resultados similares a Hola siguiente ejemplo en la función de streaming del registro:</span><span class="sxs-lookup"><span data-stu-id="6223e-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="6223e-178">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="6223e-178">Environment variables</span></span>
<span data-ttu-id="6223e-179">tooget una variable de entorno o un valor de configuración de aplicación, utilice `System.Environment.GetEnvironmentVariable`, tal y como se muestra en el siguiente código de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="6223e-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a><span data-ttu-id="6223e-180">Reutilización del código .csx</span><span class="sxs-lookup"><span data-stu-id="6223e-180">Reusing .csx code</span></span>
<span data-ttu-id="6223e-181">Puede usar las clases y los métodos definidos en otros archivos *.csx* con el archivo *run.csx*.</span><span class="sxs-lookup"><span data-stu-id="6223e-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="6223e-182">toodo que usan `#load` directivas en su *run.csx* archivo.</span><span class="sxs-lookup"><span data-stu-id="6223e-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="6223e-183">En el siguiente ejemplo de Hola, una rutina de registro denominado `MyLogger` se comparte en *myLogger.csx* y se cargan en *run.csx* con hello `#load` directiva:</span><span class="sxs-lookup"><span data-stu-id="6223e-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="6223e-184">Archivo *run.csx*de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6223e-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="6223e-185">Archivo *mylogger.csx*de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6223e-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="6223e-186">Mediante un compartido *.csx* es un patrón común cuando se desea toostrongly escriba los argumentos entre funciones mediante un objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="6223e-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="6223e-187">Hola siguiente ejemplo simplificado, un desencadenador HTTP y el desencadenador de cola compartan un objeto POCO denominado `Order` datos de pedidos de toostrongly tipo hello:</span><span class="sxs-lookup"><span data-stu-id="6223e-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="6223e-188">Por ejemplo, *run.csx* para el desencadenador HTTP:</span><span class="sxs-lookup"><span data-stu-id="6223e-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="6223e-189">Por ejemplo, *run.csx* para el desencadenador de cola:</span><span class="sxs-lookup"><span data-stu-id="6223e-189">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="6223e-190">Por ejemplo, *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="6223e-190">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="6223e-191">Puede usar una ruta de acceso relativa con hello `#load` directiva:</span><span class="sxs-lookup"><span data-stu-id="6223e-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="6223e-192">`#load "mylogger.csx"`carga un archivo que se encuentra en la carpeta de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="6223e-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="6223e-193">`#load "loadedfiles\mylogger.csx"`carga un archivo que se encuentra en una carpeta de función hello.</span><span class="sxs-lookup"><span data-stu-id="6223e-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="6223e-194">`#load "..\shared\mylogger.csx"`carga un archivo que se encuentra en una carpeta en el mismo nivel como carpeta de la función de hello, es decir, el Hola directamente bajo *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="6223e-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="6223e-195">Hola `#load` directiva solo funciona con *.csx* archivos (C# script), no con *.cs* archivos.</span><span class="sxs-lookup"><span data-stu-id="6223e-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="6223e-196">Enlace en tiempo de ejecución a través de enlaces imperativos</span><span class="sxs-lookup"><span data-stu-id="6223e-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="6223e-197">En C# y otros lenguajes. NET, puede usar un [imperativo](https://en.wikipedia.org/wiki/Imperative_programming) patrón de enlace, como opuesto toohello [ *declarativa* ](https://en.wikipedia.org/wiki/Declarative_programming) enlaces en *function.json*.</span><span class="sxs-lookup"><span data-stu-id="6223e-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="6223e-198">Enlace imperativa es útil cuando los parámetros de enlace necesitan toobe calcula en tiempo de ejecución en lugar de diseño.</span><span class="sxs-lookup"><span data-stu-id="6223e-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="6223e-199">Con este modelo, puede enlazar toosupported entrada y salida enlace sobre la marcha en el código de función.</span><span class="sxs-lookup"><span data-stu-id="6223e-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="6223e-200">Defina un enlace imperativo como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="6223e-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="6223e-201">**No** incluya una entrada en *function.json* para los enlaces imperativos deseados.</span><span class="sxs-lookup"><span data-stu-id="6223e-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="6223e-202">Pase un parámetro de entrada [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) o [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="6223e-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="6223e-203">Usar hello después de enlace de datos de C# patrón tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="6223e-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="6223e-204">donde `BindingTypeAttribute` es Hola .NET atributo que define el enlace y `T` es Hola tipo de entrada o de salida que sea compatible con ese tipo de enlace.</span><span class="sxs-lookup"><span data-stu-id="6223e-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="6223e-205">`T` no puede ser también un tipo de parámetro `out` (como `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="6223e-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="6223e-206">Por ejemplo, el enlace de salida de la tabla de Mobile Apps admite [seis tipos de salida](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), pero solo se puede utilizar [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) para `T`.</span><span class="sxs-lookup"><span data-stu-id="6223e-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="6223e-207">Hola siguiendo el ejemplo de código crea un [enlace de salida blob de almacenamiento](functions-bindings-storage-blob.md#using-a-blob-output-binding) con blob ruta de acceso que se define en tiempo de ejecución, a continuación, escribe un blob de toohello de cadena.</span><span class="sxs-lookup"><span data-stu-id="6223e-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="6223e-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) define hello [blob de almacenamiento](functions-bindings-storage-blob.md) entrada o salida de enlace, y [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) es un tipo de enlace de salida compatible.</span><span class="sxs-lookup"><span data-stu-id="6223e-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="6223e-209">Tal cual, código de hello Obtiene la configuración de la aplicación hello predeterminado para la cadena de conexión de cuenta de almacenamiento de Hola (que es `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="6223e-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="6223e-210">Puede especificar un toouse de configuración de aplicación personalizada mediante la adición de la [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) y pasar la matriz de atributos de hello en `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="6223e-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="6223e-211">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="6223e-211">For example,</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="6223e-212">Hello tabla siguiente enumeran los atributos de .NET de Hola para cada enlace hello y tipo de los paquetes en el que se definen.</span><span class="sxs-lookup"><span data-stu-id="6223e-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="6223e-213">Enlace</span><span class="sxs-lookup"><span data-stu-id="6223e-213">Binding</span></span> | <span data-ttu-id="6223e-214">Atributo</span><span class="sxs-lookup"><span data-stu-id="6223e-214">Attribute</span></span> | <span data-ttu-id="6223e-215">Agregar referencia</span><span class="sxs-lookup"><span data-stu-id="6223e-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="6223e-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6223e-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="6223e-217">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6223e-217">Event Hubs</span></span> | <span data-ttu-id="6223e-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="6223e-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="6223e-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="6223e-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="6223e-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="6223e-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="6223e-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="6223e-221">Service Bus</span></span> | <span data-ttu-id="6223e-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="6223e-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="6223e-223">Cola de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6223e-223">Storage queue</span></span> | <span data-ttu-id="6223e-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="6223e-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="6223e-225">Blob de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6223e-225">Storage blob</span></span> | <span data-ttu-id="6223e-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="6223e-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="6223e-227">Tabla de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6223e-227">Storage table</span></span> | <span data-ttu-id="6223e-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="6223e-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="6223e-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="6223e-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="6223e-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6223e-230">Next steps</span></span>
<span data-ttu-id="6223e-231">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6223e-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="6223e-232">Procedimientos recomendados de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6223e-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="6223e-233">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="6223e-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="6223e-234">Referencia para desarrolladores de F# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6223e-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="6223e-235">Referencia para desarrolladores de NodeJS de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="6223e-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="6223e-236">Enlaces y desencadenadores de las Funciones de azure</span><span class="sxs-lookup"><span data-stu-id="6223e-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
