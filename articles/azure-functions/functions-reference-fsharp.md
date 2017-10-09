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
# <a name="azure-functions-f-developer-reference"></a>Referencia para desarrolladores de F# de Azure Functions
> [!div class="op_single_selector"]
> * [Script de C#](functions-reference-csharp.md)
> * [Script de F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # para las funciones de Azure es una solución para ejecutar fácilmente pequeños fragmentos de código, o "funciones", en la nube de Hola. Los datos fluyen en la función de F# a través de los argumentos de función. Nombres de los argumentos se especifican en `function.json`, y hay nombres predefinidos para tener acceso a acciones como Hola función registrador y tokens de cancelación.

En este artículo se da por supuesto que ya ha leído hello [material de referencia de funciones de Azure](functions-reference.md).

## <a name="how-fsx-works"></a>Cómo funciona .fsx
Un archivo `.fsx` es un script de F#. Se puede considerar como un proyecto de F# que se encuentra en un único archivo. archivo Hello contiene código hello para el programa (en este caso, la función de Azure) y directivas para administrar las dependencias.

Cuando se usa un `.fsx` para una función de Azure, normalmente requiere ensamblados se incluyen automáticamente para usted, lo que le toofocus en el código de función en lugar de "reutilizable" Hola.

## <a name="binding-tooarguments"></a>Enlace tooarguments
Cada enlace admite un conjunto de argumentos, como Hola detallada en [referencia del programador de desencadenadores y los enlaces de funciones de Azure](functions-triggers-bindings.md). Por ejemplo, uno de los enlaces de argumento hello es compatible con un desencadenador de blob es un POCO, que se puede expresar utilizando un registro de F #. Por ejemplo:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

La F# de Azure Functions tendrá uno o más argumentos. Cuando hablamos sobre los argumentos de las funciones de Azure, nos referimos demasiado*entrada* argumentos y *salida* argumentos. Un argumento de entrada es exactamente lo que parece: entrada tooyour Azure función de F #. Un *salida* argumento es datos mutables o `byref<>` argumento que actúa como una manera toopass de datos nuevo *out* de la función.

En el ejemplo de Hola anterior, `blob` es un argumento de entrada, y `output` es un argumento de salida. Observe que utilizamos `byref<>` para `output` (no hay ningún Hola de tooadd necesidad `[<Out>]` anotación). Mediante un `byref<>` su toochange función registro u objeto Hola el argumento que hace referencia a que permite el tipo.

Cuando un registro de F # se usa como un tipo de entrada, definición de registro de hello debe estar marcado con `[<CLIMutable>]` en orden tooallow hello Azure funciones framework tooset campos Hola adecuadamente antes de pasar Hola registro tooyour función. Bajo el paraguas de hello, `[<CLIMutable>]` genera establecedores de propiedades de registro de hello. Por ejemplo:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

También puede utilizarse una clase F# tanto para argumentos de entrada como de salida. Para una clase, las propiedades normalmente necesitan captadores y establecedores. Por ejemplo:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Registro
toolog salida tooyour [los registros de streaming](../app-service-web/web-sites-streaming-logs-and-console.md) en F #, la función debe tomar un argumento de tipo `TraceWriter`. Por coherencia, se recomienda que se le dé el nombre `log`a este argumento. Por ejemplo:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Async
Hola `async` puede utilizarse el flujo de trabajo, pero el resultado de hello debe tooreturn un `Task`. Esto puede hacerse con `Async.StartAsTask`, por ejemplo:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>Token de cancelación
Si la función necesita toohandle cierre correctamente, puede asignarle un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumento. Esto se puede combinar con `async`, por ejemplo:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Importación de espacios de nombres
Espacios de nombres se pueden abrir en hello forma habitual:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hola después de los espacios de nombres se abre automáticamente:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Referencia a ensamblados externos
De forma similar, el ensamblado de framework se agregan las referencias con hello `#r "AssemblyName"` directiva.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Hello siguientes ensamblados se agregan automáticamente las funciones de Azure Hola entorno de hospedaje:

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`.

Además, es especial Hola siguientes ensamblados las mayúsculas y minúsculas y puede hacer referencia mediante simplename (p. ej. `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Si necesita tooreference un ensamblado privado, puede cargar el archivo de ensamblado de hello en un `bin` referencia mediante Hola (por ejemplo, nombre de archivo y función de carpeta tooyour relativa  `#r "MyAssembly.dll"`). Para obtener información sobre cómo los archivos de carpeta de la función tooyour tooupload, vea Hola siguiendo la sección sobre administración de paquetes.

## <a name="editor-prelude"></a>Preludio del editor
Un editor compatible con servicios de compilador de F # no tendrá constancia de espacios de nombres de Hola y ensamblados que se incluye automáticamente las funciones de Azure. Por lo tanto, puede ser útil tooinclude un paso previo que ayuda a editor Hola buscar ensamblados de Hola que utilice y tooexplicitly abrir espacios de nombres. Por ejemplo:

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

Cuando las funciones de Azure se ejecuta el código, lo procesa origen Hola con `COMPILED` definido, por lo que se pasará por alto preludio de editor de Hola.

<a name="package"></a>

## <a name="package-management"></a>Administración de paquetes
paquetes de NuGet toouse en una función de F #, agregue un `project.json` carpeta de la función de toohello Hola de archivos en el sistema de archivos de la aplicación de la función de Hola. Este es un ejemplo `project.json` archivo que agrega una referencia de paquete de NuGet demasiado`Microsoft.ProjectOxford.Face` versión 1.1.0:

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

Solo hello .NET Framework 4.6 es compatible, por lo tanto asegúrese de que su `project.json` archivo especifica `net46` como se muestra aquí.

Al cargar un `project.json` de archivos, obtiene los paquetes de saludo hello en tiempo de ejecución y agrega automáticamente los ensamblados del paquete toohello referencias. No es necesario tooadd `#r "AssemblyName"` directivas. Basta con agregar Hola necesario `open` instrucciones tooyour `.fsx` archivo.

Es recomendable tooput hará referencia automáticamente a los ensamblados en su preludio de editor, tooimprove interacción de su editor con servicios de compilación de F #.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>¿Cómo tooadd un `project.json` archivo tooyour Azure (función)
1. BEGIN asegurándose de que la aplicación de la función se está ejecutando, lo que puede hacer abriendo la función de hello portal de Azure. Esto también proporciona acceso toohello los registros de streaming donde se mostrará la salida de instalación del paquete.
2. tooupload una `project.json` de archivos, utilice uno de los métodos de hello descritos en [forma en que funcionan los archivos de aplicación tooupdate](functions-reference.md#fileupdate). Si utilizas [implementación continua para las funciones de Azure](functions-continuous-deployment.md), puede agregar un `project.json` tooyour rama en orden tooexperiment con él antes de agregarlo tooyour rama de implementación de almacenamiento provisional de archivos.
3. Después de hello `project.json` se agrega el archivo, verá toohello similar de salida siguiente ejemplo en la función de streaming del registro:

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

## <a name="environment-variables"></a>Variables de entorno
tooget una variable de entorno o un valor de configuración de aplicación, utilice `System.Environment.GetEnvironmentVariable`, por ejemplo:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>Reutilización del código .fsx
Puede utilizar el código de otros archivos `.fsx` mediante una directiva `#load`. Por ejemplo:

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

Las rutas de acceso proporciona toohello `#load` directiva son ubicación relativa toohello de su `.fsx` archivo.

* `#load "logger.fsx"`carga un archivo que se encuentra en la carpeta de la función de Hola.
* `#load "package\logger.fsx"`carga un archivo que se encuentra en hello `package` carpeta en la carpeta de la función de Hola.
* `#load "..\shared\mylogger.fsx"`carga un archivo que se encuentra en hello `shared` carpeta en el mismo nivel como carpeta de la función de hello, es decir, el Hola directamente bajo `wwwroot`.

Hola `#load` directiva solo funciona con `.fsx` archivos (script de F #) y no con `.fs` archivos.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes:

* [Guía de F#](/dotnet/articles/fsharp/index)
* [Procedimientos recomendados de Azure Functions](functions-best-practices.md)
* [Azure Functions developer reference](functions-reference.md)
* [Referencia para desarrolladores de C# de Funciones de Azure](functions-reference-csharp.md)
* [Referencia para desarrolladores de NodeJS de Funciones de Azure](functions-reference-node.md)
* [Enlaces y desencadenadores de las Funciones de azure](functions-triggers-bindings.md)
* [Prueba de Azure Functions](functions-test-a-function.md)
* [Escalado de Azure Functions](functions-scale.md)

