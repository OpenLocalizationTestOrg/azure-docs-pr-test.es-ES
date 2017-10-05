---
title: "Depuración de microservicios de Azure en Linux | Microsoft Docs"
description: "Aprenda a supervisar y diagnosticar sus servicios creados con Service Fabric de Microsoft Azure en una máquina de desarrollo local."
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
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="ab2d7-103">Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local</span><span class="sxs-lookup"><span data-stu-id="ab2d7-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab2d7-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ab2d7-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="ab2d7-105">Linux</span><span class="sxs-lookup"><span data-stu-id="ab2d7-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="ab2d7-106">Acciones como supervisar, detectar, diagnosticar y solucionar problemas permiten a los servicios continuar con una interrupción mínima de la experiencia del usuario.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="ab2d7-107">La supervisión y el diagnóstico resultan fundamentales en un entorno de producción implementado real.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="ab2d7-108">La adopción de un modelo similar durante el desarrollo de servicios garantiza que la canalización del diagnóstico funcione cuando pasa a un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="ab2d7-109">Service Fabric facilita a los desarrolladores de servicio la implementación de diagnósticos que puede funcionar sin problemas en configuraciones de desarrollo local de máquina única y en configuraciones de clúster de producción del mundo real.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="ab2d7-110">Depuración de aplicaciones Java de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ab2d7-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="ab2d7-111">Para aplicaciones Java, hay [varias plataformas de registro](http://en.wikipedia.org/wiki/Java_logging_framework) disponibles.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="ab2d7-112">Puesto que `java.util.logging` es la opción predeterminada con JRE, también se usa para los [ejemplos de código en GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ab2d7-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="ab2d7-113">En la siguiente discusión se explica cómo configurar la plataforma `java.util.logging` .</span><span class="sxs-lookup"><span data-stu-id="ab2d7-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="ab2d7-114">Con java.util.logging puede redirigir los registros de aplicaciones a la memoria, flujos de salida, archivos de consolas o sockets.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="ab2d7-115">Para cada una de estas opciones, hay controladores predeterminados que se proporcionan en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="ab2d7-116">Puede crear un archivo `app.properties` para configurar el controlador de archivo para la aplicación a fin de redirigir todos los registros a un archivo local.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="ab2d7-117">El fragmento de código siguiente contiene una configuración de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab2d7-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="ab2d7-118">La carpeta señalada por el archivo `app.properties` debe existir.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="ab2d7-119">Una vez creado el archivo `app.properties`, debe modificar igualmente el script de punto de entrada, `entrypoint.sh` en la carpeta `<applicationfolder>/<servicePkg>/Code/` para establecer la propiedad `java.util.logging.config.file` en el archivo `app.propertes`.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="ab2d7-120">La entrada debería parecerse al siguiente fragmento:</span><span class="sxs-lookup"><span data-stu-id="ab2d7-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="ab2d7-121">Esta configuración hace que se recopilen los registros por orden de rotación en `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="ab2d7-122">El archivo de registro en este caso se denomina mysfapp%u.%g.log donde:</span><span class="sxs-lookup"><span data-stu-id="ab2d7-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="ab2d7-123">**%u** es un número único para resolver conflictos entre los procesos simultáneos de Java.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="ab2d7-124">**g** es el número de generación para distinguir entre los registros de rotación.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="ab2d7-125">De forma predeterminada, si no hay ningún controlador configurado explícitamente, se registra el controlador de la consola.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="ab2d7-126">Se pueden ver los registros de syslog en /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="ab2d7-127">Para más información, consulte los [ejemplos de código en GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ab2d7-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="ab2d7-128">Depuración de aplicaciones C# de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ab2d7-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="ab2d7-129">Hay varios marcos disponibles para realizar un seguimiento de aplicaciones de CoreCLR en Linux.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="ab2d7-130">Para obtener más información, consulte [GitHub: logging](http:/github.com/aspnet/logging) (registro).</span><span class="sxs-lookup"><span data-stu-id="ab2d7-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="ab2d7-131">Dado que los desarrolladores de C# ya conocen EventSource, este artículo utiliza EventSource para realizar un seguimiento en muestras de CoreCLR en Linux.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="ab2d7-132">El primer paso es incluir System.Diagnostics.Tracing para que pueda escribir los registros en la memoria, en flujos de salida o en archivos de consola.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="ab2d7-133">Para registrarse mediante EventSource, añada el siguiente proyecto a project.json:</span><span class="sxs-lookup"><span data-stu-id="ab2d7-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="ab2d7-134">Puede usar un EventListener personalizado para escuchar el evento de servicio y, a continuación, redirigirlos correctamente a los archivos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="ab2d7-135">El fragmento de código siguiente muestra un ejemplo de implementación de un registro con EventSource y un EventListener personalizado:</span><span class="sxs-lookup"><span data-stu-id="ab2d7-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need to add method for sample event.

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


<span data-ttu-id="ab2d7-136">El fragmento de código anterior genera los registros en un archivo en `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="ab2d7-137">Este nombre de archivo debe actualizarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="ab2d7-138">En caso de que desee redirigir los registros a la consola, use el siguiente fragmento de código en la clase de EventListener personalizada:</span><span class="sxs-lookup"><span data-stu-id="ab2d7-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="ab2d7-139">Los ejemplos de [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) (Ejemplos de C#) usan EventSource y un EventListener personalizado para registrar eventos en un archivo.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ab2d7-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab2d7-140">Next steps</span></span>
<span data-ttu-id="ab2d7-141">El mismo código de seguimiento que agregó a la aplicación también funciona con los diagnósticos de la aplicación en un clúster de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="ab2d7-142">Consulte estos artículos que tratan sobre las distintas opciones de las herramientas y describen cómo configurarlas.</span><span class="sxs-lookup"><span data-stu-id="ab2d7-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="ab2d7-143">Recopilación de registros con Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="ab2d7-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
