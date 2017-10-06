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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Toocontinue de servicios con experiencia de usuario de una interrupción mínima toohello permiten supervisar, detectar, diagnosticar y solucionar problemas. La supervisión y el diagnóstico resultan fundamentales en un entorno de producción implementado real. Adoptar un modelo similar durante el desarrollo de servicios garantiza que esa canalización diagnóstico Hola funciona cuando se mueve el entorno de producción de tooa. Service Fabric facilita a los diagnósticos del servicio a los desarrolladores tooimplement que funcionan sin problemas a través de configuraciones de desarrollo local sola máquina y configuraciones de clúster de producción reales.


## <a name="debugging-service-fabric-java-applications"></a>Depuración de aplicaciones Java de Service Fabric

Para aplicaciones Java, hay [varias plataformas de registro](http://en.wikipedia.org/wiki/Java_logging_framework) disponibles. Puesto que `java.util.logging` es la opción predeterminada de hello con hello JRE, también se usa para hello [ejemplos de código de github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Hello en los párrafos siguientes se explican cómo tooconfigure hello `java.util.logging` framework.

Uso de java.util.logging puede redirigir la aplicación registros toomemory, flujos de salida, archivos de la consola o sockets. Para cada una de estas opciones, hay controladores predeterminados ya proporcionados en el marco de trabajo de Hola. Puede crear un `app.properties` controlador de archivo de archivo tooconfigure Hola para su tooredirect aplicación todos los registros de archivo local tooa.

Hola siguiente fragmento de código contiene una configuración de ejemplo:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

Hola de Hello carpeta apunta tooby `app.properties` archivo debe existir. Después de hello `app.properties` se crea el archivo, deberá tooalso modificar el script de punto de entrada, `entrypoint.sh` en hello `<applicationfolder>/<servicePkg>/Code/` propiedad Hola de carpeta tooset `java.util.logging.config.file` demasiado`app.propertes` archivo. entrada de Hello debería ser similar Hola siguiente fragmento de código:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Esta configuración hace que se recopilen los registros por orden de rotación en `/tmp/servicefabric/logs/`. archivo de registro de Hello en este caso se denomina mysfapp%u.%g.log donde:
* **%u** es un único tooresolve número conflictos entre procesos simultáneos de Java.
* **%g** es toodistinguish de número de generación de hello entre la rotación de registros.

De forma predeterminada si no hay ningún controlador se configura explícitamente, el controlador de la consola de hello está registrado. Uno puede ver registros de hello en syslog en /var/log/syslog.

Para obtener más información, vea hello [ejemplos de código de github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Depuración de aplicaciones C# de Service Fabric


Hay varios marcos disponibles para realizar un seguimiento de aplicaciones de CoreCLR en Linux. Para obtener más información, consulte [GitHub: logging](http:/github.com/aspnet/logging) (registro).  Puesto que EventSource es los desarrolladores familiarizados tooC #' EventSource este artículo utiliza para realizar el seguimiento en los ejemplos de CoreCLR en Linux.

Hola primer paso es tooinclude System.Diagnostics.Tracing para que pueda escribir los registros toomemory, flujos de salida o archivos de la consola.  Para el registro mediante EventSource, agregue Hola después proyecto tooyour project.json:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Puede usar un toolisten EventListener personalizado para eventos del servicio de hello y, a continuación, adecuadamente redirigirá tootrace archivos. Hello fragmento de código siguiente muestra una implementación de ejemplo de registro mediante EventSource y un EventListener personalizado:


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


Hello fragmento de código anterior genera tooa archivo de registros de hello en `/tmp/MyServiceLog.txt`. Este nombre de archivo debe toobe actualizado correctamente. En caso de que desee tooredirect Hola registros tooconsole, use Hola siguiente fragmento de código en la clase EventListener personalizada:

```csharp
public static TextWriter Out = Console.Out;
```

Hola ejemplos en [ejemplos de C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) usar EventSource y un archivo de tooa de eventos de toolog EventListener personalizado.



## <a name="next-steps"></a>Pasos siguientes
Hola el mismo código de seguimiento agregado tooyour aplicación también funciona con los diagnósticos de saludo de la aplicación en un clúster de Azure. Consultar estos artículos que trata las diferentes opciones de Hola para herramientas de Hola y describen cómo tooset su seguridad.
* [Funcionamiento de los registros toocollect con diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-lad.md)
