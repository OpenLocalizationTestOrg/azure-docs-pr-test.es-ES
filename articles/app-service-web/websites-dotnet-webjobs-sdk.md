---
title: aaaWhat es hello SDK de WebJobs de Azure
description: "Un toohello introducción del SDK de WebJobs de Azure. Explica qué Hola SDK, resulta útil para los escenarios típicos y ejemplos de código."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>¿Qué es hello SDK de WebJobs de Azure
## <a id="overview"></a>Información general
Este artículo explica qué Hola SDK de WebJobs es, revisa algunos escenarios comunes es útil para y ofrezca una visión general de cómo utilizarlo en el código.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Trabajos Web](websites-webjobs-resources.md) es una característica del servicio de aplicaciones de Azure que le permite toorun un programa o script en hello mismo contexto que una aplicación web, una aplicación de API o aplicación móvil. Hola propósito de hello [SDK de WebJobs](websites-webjobs-resources.md) es código de hello toosimplify que se escribe para las tareas comunes que puede realizar un trabajo Web, como procesamiento de imágenes, procesamiento de colas, agregación de RSS, mantenimiento del archivo y enviar mensajes de correo electrónico. Hola SDK de WebJobs tiene características integradas para trabajar con el almacenamiento de Azure y Bus de servicio, para programar tareas y control de errores y para muchos otros escenarios comunes. Además, se ha diseñado toobe extensible. Hola [SDK de WebJobs es código abierto](https://github.com/Azure/azure-webjobs-sdk/)y no hay un [repositorio de código abierto para las extensiones](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Hola SDK de WebJobs incluye Hola de los componentes siguientes:

* **Paquetes NuGet**. Paquetes de NuGet que agregar proyecto de aplicación de consola de Visual Studio tooa proporcionan un marco que utiliza el código decorando los métodos con atributos de SDK de WebJobs.
* **Panel**. Parte del SDK de WebJobs de Hola se incluye en el servicio de aplicación de Azure y proporciona supervisión enriquecida y diagnósticos para programas que utilizan paquetes de NuGet Hola. No es necesario toowrite código toouse estas características de supervisión y diagnóstico.

## <a id="scenarios"></a>Escenarios
Estos son algunos escenarios típicos que se puede controlar más fácilmente con hello SDK de WebJobs de Azure:

* Procesamiento de imágenes u otros trabajos de uso intensivo de CPU. Una característica común de los sitios Web es Hola capacidad tooupload imágenes o vídeos. A menudo desea toomanipulate Hola contenido después de cargarse, pero no desea toomake Hola usuario espera mientras lo hace.
* Procesamiento de colas. Una forma habitual para un toocommunicate de front-end web con un servicio back-end es toouse colas. Al sitio Web de hello necesita tooget trabajo, inserta un mensaje en una cola. Un servicio back-end extrae los mensajes de la cola de Hola y Hola trabajo. Puede usar las colas para el procesamiento de imagen: por ejemplo, después de usuario de hello carga un número de archivos, coloque los nombres de archivo de hello en un toobe de mensaje de cola recogido Hola back-end para el procesamiento. O bien, puede usar la capacidad de respuesta del sitio de tooimprove de colas. Por ejemplo, en lugar de escribir directamente la base de datos SQL tooa, tooa cola de escritura, informar al usuario de hello terminado y permiten Hola back-end servicio controlador de latencia alta bases de datos relacionales de trabajo. Para obtener un ejemplo de cola de procesamiento con el proceso de la imagen, vea hello [WebJobs Introducción SDK tutorial](websites-dotnet-webjobs-sdk-get-started.md).
* Agregación de fuentes RSS. Si tiene un sitio que mantiene una lista de fuentes RSS, puede extraer en todos los artículos de Hola desde fuentes de hello en un proceso en segundo plano.
* Mantenimiento de archivos, como el agregado o limpieza de archivos de registro.  Puede tener archivos de registro que se va a crear entre varios sitios o para independiente intervalos de tiempo que desee toocombine en orden toorun trabajos de análisis en ellos. También puede tooschedule un toorun de tarea semanal tooclean los archivos de registro antiguos.
* Entradas en tablas de Azure. Podría tener archivos almacenados y los blobs y desea tooparse ellos y almacenar datos de hello en tablas. función de entrada de Hello podría hacerlo escribiendo una gran cantidad de filas (millones en algunos casos) y Hola SDK de WebJobs hace posible tooimplement esta funcionalidad fácilmente. Hola SDK también proporciona supervisión en tiempo real de los indicadores de progreso como el número de filas escritas en la tabla de Hola Hola.
* Otras tareas de larga duración que desea toorun en un subproceso en segundo plano, como [enviar correos electrónicos](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Las tareas que desea toorun según una programación, como realizar una operación de copia de seguridad cada noche.

En muchos de estos escenarios puede tooscale un toorun de aplicación web en varias máquinas virtuales, lo que podría ejecutar simultáneamente varios trabajos Web. En algunos casos esto podría resultar en hello igual al procesamiento de datos varias veces, pero esto no es un problema cuando se usan la cola integrados de hello, blob y desencadenadores de Bus de servicio de SDK de WebJobs Hola. Hola SDK garantiza que las funciones se procesará una sola vez para cada mensaje o blob.

Hola SDK de WebJobs también resulta fácil toohandle escenarios de control de errores comunes. Puede configurar alertas toosend notificaciones cuando se produce un error en una función, y puede establecer los tiempos de espera para que una función se cancela automáticamente si no se completa dentro de un límite de tiempo especificado.

## <a id="code"></a> Ejemplos de código
código de Hello para el tratamiento de las tareas habituales que funcionen con el almacenamiento de Azure es sencillo. En la aplicación de consola `Main` método crea un `JobHost` objeto que coordina Hola llama toomethods se escribe. Hello framework SDK de WebJobs sabe cuando toocall los métodos y valores de los parámetros toouse basándose en hello SDK de WebJobs de atributos utilizar en ellos. Hello SDK proporciona *desencadenadores* que especifican las condiciones que causan Hola función toobe llamado, y *enlazadores* que especifican cómo tooget información dentro y fuera de los parámetros de método.

Por ejemplo, hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) atributo da lugar a un toobe de función que se llama cuando se recibe un mensaje en una cola, y si el formato del mensaje de Hola es JSON para un tipo personalizado o una matriz de bytes, mensaje de saludo se deserializa automáticamente. Hola [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) atributo desencadena un proceso cada vez que se crea un nuevo blob en una cuenta de almacenamiento de Azure.

Este es un simple programa que sondea una cola y crea un blob para cada mensaje de la cola recibido:

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

Hola `JobHost` objeto es un contenedor para un conjunto de funciones en segundo plano. Hola `JobHost` objeto monitores hello las funciones, inspecciona los eventos que activan dichas y ejecuta las funciones hello cuando se producen eventos de desencadenador. Se llama a un `JobHost` tooindicate método si desea que toorun de proceso del contenedor de hello en Hola subproceso actual o un subproceso en segundo plano. En el ejemplo de Hola, Hola `RunAndBlock` método ejecuta el proceso de hello continuamente en el subproceso actual Hola.

Dado que hello `ProcessQueueMessage` en este ejemplo tiene un `QueueTrigger` atributo, el desencadenador de Hola para esa función es recepción Hola de un nuevo mensaje de cola. Hola `JobHost` objeto inspecciona los nuevos mensajes en cola en la cola especificada de hello ("webjobsqueue" en este ejemplo) y cuando se encuentra uno, se llama a `ProcessQueueMessage`. 

Hola `QueueTrigger` atributo enlaza hello `inputText` toohello valor del parámetro de mensaje de bienvenida de cola. Hello y `Blob` atributo enlaza un `TextWriter` tooa de objetos blob denominado "blobname" en un contenedor denominado "containername".  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

función Hello, a continuación, usa estos parámetros toowrite Hola valo blob de toohello de mensajes de Hola cola:

        writer.WriteLine(inputText);

características de desencadenador y el enlazador de Hola de hello SDK de WebJobs simplifican considerablemente el código de hello tiene toowrite. Hola código de bajo nivel necesario tooprocess colas, blobs, o archivos o tooinitiate programar tareas, se realiza automáticamente por hello framework SDK de WebJobs. Por ejemplo, el marco de trabajo de hello crea colas que aún no existen, se abre Hola cola, lecturas cola los mensajes, eliminaciones en cola los mensajes cuando el procesamiento se ha completado, crea los contenedores de blob que no existen todavía, escribe tooblobs y así sucesivamente.

Hello ejemplo de código siguiente muestra una variedad de desencadenadores en un trabajo Web: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, y `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a> Programación
Hola `TimerTrigger` atributo proporciona Hola capacidad tootrigger funciones toorun según una programación. Puede programar un trabajo Web como un todo a Azure o programación funciones individuales de un trabajo Web utilizando Hola SDK de WebJobs `TimerTrigger`. A continuación se presenta un ejemplo de código.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Para obtener más código de ejemplo, vea [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) en el repositorio de azure-trabajos Web: extensiones de sdk de hello en GitHub.com.

## <a name="extensibility"></a>Extensibilidad
No está limitado en toobuilt funcionalidad--hello SDK de WebJobs permite enlazadores y desencadenadores personalizados de toowrite.  Por ejemplo, puede escribir desencadenadores de eventos de caché y programaciones periódicas. Un [repositorio de código abierto](https://github.com/Azure/azure-webjobs-sdk-extensions) contiene un [guía detallada sobre extensibilidad de SDK de WebJobs](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) y toohelp de código de ejemplo permiten comenzar a escribir sus propios desencadenadores y enlazadores.

## <a id="workerrole"></a>Uso de hello SDK de WebJobs fuera de trabajos Web
Un programa que utiliza Hola Hola SDK de WebJobs es una aplicación de consola estándar y puede ejecutarse en cualquier lugar, no tiene toorun como un trabajo Web. Puede probar el programa de hello localmente en el equipo de desarrollo y de producción que se puede ejecutar en un rol de trabajo de servicio en la nube o un servicio de Windows si prefiere uno de estos entornos. 

Sin embargo, el panel de hello solo está disponible como una extensión de una aplicación web de servicio de aplicaciones de Azure. Si desea toorun fuera de un trabajo Web y seguir usando Hola panel, puede configurar un servidor web toouse aplicación Hola la misma cuenta de almacenamiento que la cadena de conexión del panel de SDK de WebJobs hace referencia a, y panel del dicha aplicación de WebJobs, a continuación, mostrará datos acerca de la función ejecución desde el programa que se está ejecutando en otro lugar. Puede obtener toohello panel mediante Hola dirección URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Para obtener más información, consulte [obtener un panel para el desarrollo local con hello SDK de WebJobs](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), pero tenga en cuenta que la entrada de blog de hello muestra un nombre de cadena de conexión anterior. 

## <a id="nostorage"></a>Características del panel
Hola SDK de WebJobs proporciona varias ventajas incluso si no utiliza desencadenadores de SDK de WebJobs o enlazadores:

* Se pueden invocar funciones de hello panel.
* Puede reproducir las funciones de hello panel.
* Puede ver registros en hello panel, vinculado toohello trabajo Web determinado (registros de aplicación, escritos con Console.Out, Console.Error, seguimiento, etc.) o se vinculan de invocación de función determinada toohello que generó la (registros escritos mediante un `TextWriter` objeto que Hola que SDK pasa toohello función como un parámetro). 

Para obtener más información, consulte [cómo toomanually invocar una función](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) y [cómo registra toowrite](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Pasos siguientes
Para obtener más información acerca de hello SDK de WebJobs, consulte [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).

Para obtener información sobre hello más recientes mejoras toohello SDK de WebJobs, vea hello [notas de la versión](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

