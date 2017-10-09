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
# <a name="azure-functions-c-script-developer-reference"></a>Referencia para desarrolladores de scripts de C# de Azure Functions
> [!div class="op_single_selector"]
> * [Script de C#](functions-reference-csharp.md)
> * [Script de F#](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
>
>

Hola experiencia en C# script para las funciones de Azure se basa en hello SDK de WebJobs de Azure. Los datos fluyen en la función de C# a través de los argumentos de método. Nombres de los argumentos se especifican en `function.json`, y hay nombres predefinidos para tener acceso a acciones como Hola función registrador y tokens de cancelación.

En este artículo se da por supuesto que ya ha leído hello [material de referencia de funciones de Azure](functions-reference.md).

Para obtener información sobre el uso de las bibliotecas de clases de C#, vea [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (Uso de bibliotecas de clases de .NET con Azure Functions).

## <a name="how-csx-works"></a>Funcionamiento de .csx
Hola `.csx` formato permite toowrite menos "reutilizable" y centrarse en la escritura simplemente una función de C#. Incluir las referencias a ensamblados y espacios de nombres al principio de Hola de archivo hello como de costumbre. En lugar de encapsular todo en un espacio de nombres y una clase, defina solamente un método `Run`. Si necesita tooinclude todas las clases, para objetos de objetos CLR antiguos (POCO), puede incluir una clase dentro de instancia toodefine simple Hola mismo archivo.   

## <a name="binding-tooarguments"></a>Enlace tooarguments
Hello varios enlaces son función dependiente tooa C# a través de hello `name` propiedad Hola *function.json* configuración. Cada enlace tiene sus propios tipos admitidos; por ejemplo, un desencadenador de blob puede admitir una cadena, un objeto POCO o un CloudBlockBlob. tipos de Hello admitida se documentan en referencia de Hola para cada enlace. Un objeto POCO debe tener un captador y establecedor definidos para cada propiedad.

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

## <a name="using-method-return-value-for-output-binding"></a>Uso del valor devuelto del método para el enlace de salida

Puede usar un valor devuelto del método de un enlace de salida, utilizando el nombre de hello `$return` en *function.json*:

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

## <a name="writing-multiple-output-values"></a>Escribir varios valores de salida

toowrite tooan de varios valores de salida de enlace, use hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) tipos. Estos tipos son colecciones de solo escritura que están toohello escrito el enlace de salida cuando se completa el método hello.

En este ejemplo se escriben varios mensajes en cola mediante `ICollector`:

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a>Registro
toolog salida tooyour los registros de streaming en C#, incluya un argumento de tipo `TraceWriter`. Es recomendable que lo denomine `log`. Evite el uso de `Console.Write` en Azure Functions. 

`TraceWriter`se define en hello [SDK de WebJobs de Azure](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs). Hola a nivel de registro para `TraceWriter` pueden configurarse en [host\.json].

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a>Async
toomake una función asincrónica, usar hello `async` palabra clave y valor devuelto una `Task` objeto.

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a>Token de cancelación
Algunas operaciones requieren un cierre estable. Aunque siempre es mejor código toowrite que puede controlar el bloqueo, en casos donde desea que las solicitudes de apagado ordenado de toohandle, defina un [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) con el tipo de argumento.  Un `CancellationToken` se proporciona toosignal que se desencadena un cierre del host.

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

## <a name="importing-namespaces"></a>Importación de espacios de nombres
Si necesita tooimport espacios de nombres, puede hacerlo como de costumbre, con hello `using` cláusula.

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello siguientes espacios de nombres se importan automáticamente y, por tanto, son opcionales:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a>Referencia a ensamblados externos
Para los ensamblados de framework, agregue referencias mediante el uso de hello `#r "AssemblyName"` directiva.

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

Hello siguientes ensamblados se agregan automáticamente las funciones de Azure Hola entorno de hospedaje:

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

Hello siguientes pueden hacer referencia a ensamblados por nombre simple (por ejemplo, `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a>Hacer referencia a ensamblados personalizados

tooreference un ensamblado personalizado, puede usar un *compartido* ensamblado o un *privada* ensamblado:
- Los ensamblados compartidos se comparten en todas las funciones dentro de una aplicación de función. tooreference un ensamblado personalizado, cargar ensamblado tooyour función aplicación de hello, como en un `bin` carpeta del directorio raíz de aplicación de función de Hola. 
- Los ensamblados privados forman parte del contexto de una función determinada y admiten la instalación de prueba de versiones diferentes. Se deben cargar ensamblados privados en un `bin` carpeta en el directorio de la función de Hola. Referencia mediante el nombre de archivo de hello, como `#r "MyAssembly.dll"`. 

Para obtener información sobre cómo los archivos de carpeta de la función tooyour tooupload, vea Hola siguiendo la sección sobre administración de paquetes.

### <a name="watched-directories"></a>Directorios inspeccionados

directorio de Hola que contiene el archivo de script de función hello automáticamente se observa tooassemblies de cambios. toowatch cambios de ensamblado en otros directorios, agréguelos toohello `watchDirectories` lista [host\.json].

## <a name="using-nuget-packages"></a>Uso de paquetes NuGet
cargar paquetes de NuGet toouse en una función de C#, un *project.json* carpeta de la función toohello de archivos en el sistema de archivos de la aplicación de la función de Hola. Este es un ejemplo *project.json* archivo que se agrega una versión de tooMicrosoft.ProjectOxford.Face 1.1.0 de referencia:

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

Solo hello .NET Framework 4.6 es compatible, por lo tanto asegúrese de que su *project.json* archivo especifica `net46` como se muestra aquí.

Al cargar un *project.json* de archivos, obtiene los paquetes de saludo hello en tiempo de ejecución y agrega automáticamente los ensamblados del paquete toohello referencias. No es necesario tooadd `#r "AssemblyName"` directivas. tipos de hello toouse definidos en los paquetes de NuGet hello, agregar Hola necesario `using` instrucciones tooyour *run.csx* archivo 

En tiempo de ejecución de funciones de hello, restauración de NuGet funciona comparando `project.json` y `project.lock.json`. Si Hola marcas de fecha y hora de los archivos de hello **no** una restauración de NuGet de coincidencia, se ejecuta y descargas de NuGet actualizan paquetes. Sin embargo, si hello marcas de fecha y hora de los archivos de hello **hacer** coincidencia, NuGet no lleva a cabo una restauración. Por lo tanto, `project.lock.json` no deben implementarse como hace que la restauración del paquete NuGet tooskip. tooavoid implementar bloqueo hello, agregue hello `project.lock.json` toohello `.gitignore` archivo.

toouse una fuente de NuGet personalizada, especificar hello de la fuente en un *Nuget.Config* archivo en la raíz de la aplicación de la función de Hola. Para más información, vea [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior) (Configuración del comportamiento de NuGet).

### <a name="using-a-projectjson-file"></a>Uso de un archivo project.json
1. Abra la función hello en hello portal de Azure. Hola registra la salida de instalación del paquete de pestaña muestra Hola.
2. tooupload un archivo project.json, utilice uno de los métodos de hello descritos en hello [forma en que funcionan los archivos de aplicación tooupdate](functions-reference.md#fileupdate) en el tema de referencia para desarrolladores de hello las funciones de Azure.
3. Después de hello *project.json* archivo se carga, verá resultados similares a Hola siguiente ejemplo en la función de streaming del registro:

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
tooget una variable de entorno o un valor de configuración de aplicación, utilice `System.Environment.GetEnvironmentVariable`, tal y como se muestra en el siguiente código de ejemplo de Hola:

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

## <a name="reusing-csx-code"></a>Reutilización del código .csx
Puede usar las clases y los métodos definidos en otros archivos *.csx* con el archivo *run.csx*. toodo que usan `#load` directivas en su *run.csx* archivo. En el siguiente ejemplo de Hola, una rutina de registro denominado `MyLogger` se comparte en *myLogger.csx* y se cargan en *run.csx* con hello `#load` directiva:

Archivo *run.csx*de ejemplo:

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

Archivo *mylogger.csx*de ejemplo:

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

Mediante un compartido *.csx* es un patrón común cuando se desea toostrongly escriba los argumentos entre funciones mediante un objeto POCO. Hola siguiente ejemplo simplificado, un desencadenador HTTP y el desencadenador de cola compartan un objeto POCO denominado `Order` datos de pedidos de toostrongly tipo hello:

Por ejemplo, *run.csx* para el desencadenador HTTP:

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

Por ejemplo, *run.csx* para el desencadenador de cola:

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

Por ejemplo, *order.csx*:

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

Puede usar una ruta de acceso relativa con hello `#load` directiva:

* `#load "mylogger.csx"`carga un archivo que se encuentra en la carpeta de la función de Hola.
* `#load "loadedfiles\mylogger.csx"`carga un archivo que se encuentra en una carpeta de función hello.
* `#load "..\shared\mylogger.csx"`carga un archivo que se encuentra en una carpeta en el mismo nivel como carpeta de la función de hello, es decir, el Hola directamente bajo *wwwroot*.

Hola `#load` directiva solo funciona con *.csx* archivos (C# script), no con *.cs* archivos.

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a>Enlace en tiempo de ejecución a través de enlaces imperativos

En C# y otros lenguajes. NET, puede usar un [imperativo](https://en.wikipedia.org/wiki/Imperative_programming) patrón de enlace, como opuesto toohello [ *declarativa* ](https://en.wikipedia.org/wiki/Declarative_programming) enlaces en *function.json*. Enlace imperativa es útil cuando los parámetros de enlace necesitan toobe calcula en tiempo de ejecución en lugar de diseño. Con este modelo, puede enlazar toosupported entrada y salida enlace sobre la marcha en el código de función.

Defina un enlace imperativo como se indica a continuación:

- **No** incluya una entrada en *function.json* para los enlaces imperativos deseados.
- Pase un parámetro de entrada [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) o [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).
- Usar hello después de enlace de datos de C# patrón tooperform Hola.

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

donde `BindingTypeAttribute` es Hola .NET atributo que define el enlace y `T` es Hola tipo de entrada o de salida que sea compatible con ese tipo de enlace. `T` no puede ser también un tipo de parámetro `out` (como `out JObject`). Por ejemplo, el enlace de salida de la tabla de Mobile Apps admite [seis tipos de salida](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), pero solo se puede utilizar [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) o [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) para `T`.

Hola siguiendo el ejemplo de código crea un [enlace de salida blob de almacenamiento](functions-bindings-storage-blob.md#using-a-blob-output-binding) con blob ruta de acceso que se define en tiempo de ejecución, a continuación, escribe un blob de toohello de cadena.

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

[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) define hello [blob de almacenamiento](functions-bindings-storage-blob.md) entrada o salida de enlace, y [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) es un tipo de enlace de salida compatible.
Tal cual, código de hello Obtiene la configuración de la aplicación hello predeterminado para la cadena de conexión de cuenta de almacenamiento de Hola (que es `AzureWebJobsStorage`). Puede especificar un toouse de configuración de aplicación personalizada mediante la adición de la [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) y pasar la matriz de atributos de hello en `BindAsync<T>()`. Por ejemplo,

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

Hello tabla siguiente enumeran los atributos de .NET de Hola para cada enlace hello y tipo de los paquetes en el que se definen.

> [!div class="mx-codeBreakAll"]
| Enlace | Atributo | Agregar referencia |
|------|------|------|
| Cosmos DB | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| Event Hubs | [`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| Mobile Apps | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| Notification Hubs | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| Service Bus | [`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs) | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| Cola de almacenamiento | [`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Blob de almacenamiento | [`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Tabla de almacenamiento | [`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) | |
| Twilio | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes:

* [Procedimientos recomendados de Azure Functions](functions-best-practices.md)
* [Azure Functions developer reference](functions-reference.md)
* [Referencia para desarrolladores de F# de Azure Functions](functions-reference-fsharp.md)
* [Referencia para desarrolladores de NodeJS de Funciones de Azure](functions-reference-node.md)
* [Enlaces y desencadenadores de las Funciones de azure](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
