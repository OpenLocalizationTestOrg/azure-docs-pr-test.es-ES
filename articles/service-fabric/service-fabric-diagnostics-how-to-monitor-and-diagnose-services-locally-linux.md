---
title: aaaDebug microservicios Azure en Linux | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor y diagnosticar los servicios escritos mediante Microsoft Azure Service Fabric en un equipo de desarrollo local."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="ce020-103">Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local</span><span class="sxs-lookup"><span data-stu-id="ce020-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce020-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ce020-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="ce020-105">Linux</span><span class="sxs-lookup"><span data-stu-id="ce020-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="ce020-106">Toocontinue de servicios con experiencia de usuario de una interrupción mínima toohello permiten supervisar, detectar, diagnosticar y solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="ce020-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="ce020-107">La supervisión y el diagnóstico resultan fundamentales en un entorno de producción implementado real.</span><span class="sxs-lookup"><span data-stu-id="ce020-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="ce020-108">Adoptar un modelo similar durante el desarrollo de servicios garantiza que esa canalización diagnóstico Hola funciona cuando se mueve el entorno de producción de tooa.</span><span class="sxs-lookup"><span data-stu-id="ce020-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="ce020-109">Service Fabric facilita a los diagnósticos del servicio a los desarrolladores tooimplement que funcionan sin problemas a través de configuraciones de desarrollo local sola máquina y configuraciones de clúster de producción reales.</span><span class="sxs-lookup"><span data-stu-id="ce020-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="ce020-110">Depuración de aplicaciones Java de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ce020-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="ce020-111">Para aplicaciones Java, hay [varias plataformas de registro](http://en.wikipedia.org/wiki/Java_logging_framework) disponibles.</span><span class="sxs-lookup"><span data-stu-id="ce020-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="ce020-112">Puesto que `java.util.logging` es la opción predeterminada de hello con hello JRE, también se usa para hello [ejemplos de código de github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ce020-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="ce020-113">Hello en los párrafos siguientes se explican cómo tooconfigure hello `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="ce020-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="ce020-114">Uso de java.util.logging puede redirigir la aplicación registros toomemory, flujos de salida, archivos de la consola o sockets.</span><span class="sxs-lookup"><span data-stu-id="ce020-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="ce020-115">Para cada una de estas opciones, hay controladores predeterminados ya proporcionados en el marco de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce020-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="ce020-116">Puede crear un `app.properties` controlador de archivo de archivo tooconfigure Hola para su tooredirect aplicación todos los registros de archivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="ce020-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="ce020-117">Hola siguiente fragmento de código contiene una configuración de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce020-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="ce020-118">Hola de Hello carpeta apunta tooby `app.properties` archivo debe existir.</span><span class="sxs-lookup"><span data-stu-id="ce020-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="ce020-119">Después de hello `app.properties` se crea el archivo, deberá tooalso modificar el script de punto de entrada, `entrypoint.sh` en hello `<applicationfolder>/<servicePkg>/Code/` propiedad Hola de carpeta tooset `java.util.logging.config.file` demasiado`app.propertes` archivo.</span><span class="sxs-lookup"><span data-stu-id="ce020-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="ce020-120">entrada de Hello debería ser similar Hola siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="ce020-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="ce020-121">Esta configuración hace que se recopilen los registros por orden de rotación en `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="ce020-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="ce020-122">archivo de registro de Hello en este caso se denomina mysfapp%u.%g.log donde:</span><span class="sxs-lookup"><span data-stu-id="ce020-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="ce020-123">**%u** es un único tooresolve número conflictos entre procesos simultáneos de Java.</span><span class="sxs-lookup"><span data-stu-id="ce020-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="ce020-124">**%g** es toodistinguish de número de generación de hello entre la rotación de registros.</span><span class="sxs-lookup"><span data-stu-id="ce020-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="ce020-125">De forma predeterminada si no hay ningún controlador se configura explícitamente, el controlador de la consola de hello está registrado.</span><span class="sxs-lookup"><span data-stu-id="ce020-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="ce020-126">Uno puede ver registros de hello en syslog en /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="ce020-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="ce020-127">Para obtener más información, vea hello [ejemplos de código de github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ce020-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="ce020-128">Depuración de aplicaciones C# de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ce020-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="ce020-129">Hay varios marcos disponibles para realizar un seguimiento de aplicaciones de CoreCLR en Linux.</span><span class="sxs-lookup"><span data-stu-id="ce020-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="ce020-130">Para obtener más información, consulte [GitHub: logging](http:/github.com/aspnet/logging) (registro).</span><span class="sxs-lookup"><span data-stu-id="ce020-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="ce020-131">Puesto que EventSource es los desarrolladores familiarizados tooC #' EventSource este artículo utiliza para realizar el seguimiento en los ejemplos de CoreCLR en Linux.</span><span class="sxs-lookup"><span data-stu-id="ce020-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="ce020-132">Hola primer paso es tooinclude System.Diagnostics.Tracing para que pueda escribir los registros toomemory, flujos de salida o archivos de la consola.</span><span class="sxs-lookup"><span data-stu-id="ce020-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="ce020-133">Para el registro mediante EventSource, agregue Hola después proyecto tooyour project.json:</span><span class="sxs-lookup"><span data-stu-id="ce020-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="ce020-134">Puede usar un toolisten EventListener personalizado para eventos del servicio de hello y, a continuación, adecuadamente redirigirá tootrace archivos.</span><span class="sxs-lookup"><span data-stu-id="ce020-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="ce020-135">Hello fragmento de código siguiente muestra una implementación de ejemplo de registro mediante EventSource y un EventListener personalizado:</span><span class="sxs-lookup"><span data-stu-id="ce020-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="ce020-136">Hello fragmento de código anterior genera tooa archivo de registros de hello en `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="ce020-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="ce020-137">Este nombre de archivo debe toobe actualizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ce020-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="ce020-138">En caso de que desee tooredirect Hola registros tooconsole, use Hola siguiente fragmento de código en la clase EventListener personalizada:</span><span class="sxs-lookup"><span data-stu-id="ce020-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="ce020-139">Hola ejemplos en [ejemplos de C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) usar EventSource y un archivo de tooa de eventos de toolog EventListener personalizado.</span><span class="sxs-lookup"><span data-stu-id="ce020-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ce020-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce020-140">Next steps</span></span>
<span data-ttu-id="ce020-141">Hola el mismo código de seguimiento agregado tooyour aplicación también funciona con los diagnósticos de saludo de la aplicación en un clúster de Azure.</span><span class="sxs-lookup"><span data-stu-id="ce020-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="ce020-142">Consultar estos artículos que trata las diferentes opciones de Hola para herramientas de Hola y describen cómo tooset su seguridad.</span><span class="sxs-lookup"><span data-stu-id="ce020-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="ce020-143">Funcionamiento de los registros toocollect con diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="ce020-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
