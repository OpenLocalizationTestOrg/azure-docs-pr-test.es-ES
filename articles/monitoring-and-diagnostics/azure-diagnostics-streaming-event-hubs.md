---
title: "datos de diagnóstico de Azure en hello ruta de acceso activa con los concentradores de eventos aaaStreaming | Documentos de Microsoft"
description: "Configuración de diagnóstico de Azure con los concentradores de eventos finalizar tooend, incluidos detalles de los escenarios comunes."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Transmisión de datos de diagnóstico de Azure en la ruta de acceso activa hello mediante el uso de los centros de eventos
Diagnósticos de Azure proporciona maneras flexibles toocollect métricas y los registros de servicios las máquinas virtuales (VM) en la nube y transferir tooAzure almacenamiento de resultados. A partir de período de tiempo de hello (SDK 2.9) de marzo de 2016, puede enviar diagnósticos toocustom orígenes de datos y transferir datos de ruta de acceso activa en segundos mediante [centros de eventos de Azure](https://azure.microsoft.com/services/event-hubs/).

Entre los tipos de datos admitidos se incluyen:

* Eventos de Seguimiento de eventos para Windows (ETW)
* Contadores de rendimiento
* Registros de eventos de Windows
* Registros de aplicación
* Registros de infraestructura de diagnóstico de Azure

Este artículo muestra cómo tooconfigure diagnósticos de Azure con los concentradores de eventos de finalización tooend. También se proporciona orientación para hello escenarios comunes siguientes:

* Funcionamiento de los registros toocustomize hello y métricas que se envíen los centros de tooEvent
* ¿Cómo toochange configuraciones en cada entorno
* Los concentradores de eventos de tooview cómo los datos de secuencia
* ¿Cómo tootroubleshoot Hola conexión  

## <a name="prerequisites"></a>Requisitos previos
Datos de receieving de concentradores de eventos de diagnósticos de Azure se admiten en los servicios en la nube, máquinas virtuales, conjuntos de escalas de máquina Virtual y Service Fabric a partir de Azure SDK 2.9 de Hola y Hola correspondiente Azure Tools para Visual Studio.

* La extensión de Diagnósticos de Azure 1.6 ([Azure SDK para .NET 2.9 o posterior](https://azure.microsoft.com/downloads/) sirve a este fin de forma predeterminada).
* [Visual Studio 2013 o posterior.](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Las configuraciones existentes de diagnósticos de Azure en una aplicación mediante el uso de un *wadcfgx* uno de los siguientes métodos de Hola y de archivo:
  * Visual Studio: [Configuración de Diagnósticos en Servicios en la nube y Máquinas virtuales de Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell: [Habilitar el diagnóstico en Servicios en la nube de Azure mediante PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)
* Espacio de nombres de los centros de eventos aprovisionado por artículo hello, [empezar a trabajar con concentradores de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>Conectar el receptor de los centros de tooEvent de diagnósticos de Azure
De forma predeterminada, diagnósticos de Azure siempre envía los registros y las métricas tooan cuenta de almacenamiento de Azure. Una aplicación también puede enviar tooEvent centros de datos agregando un nuevo **receptores** sección hello **PublicConfig** / **WadCfg** elemento de hello *wadcfgx* archivo. En Visual Studio, Hola *wadcfgx* archivo se almacena en hello siguiendo la ruta de acceso: **proyecto de servicio de nube** > **Roles** > **() RoleName)** > **diagnostics.wadcfgx** archivo.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

En este ejemplo, centro de eventos de Hola se establece URL toohello totalmente calificado de espacio de nombres del centro de eventos de hello: espacio de nombres de los centros de eventos + "/" + nombre de concentrador de eventos.  

Centro de eventos de Hello URL se visualiza en hello [portal de Azure](http://go.microsoft.com/fwlink/?LinkID=213885) en panel de hello centros de eventos.  

Hola **receptor** puede establecer nombre de cadena válida de tooany como hello mismo valor se usa siempre en el archivo de configuración de Hola.

> [!NOTE]
> Puede que haya más receptores configurados en esta sección, como *applicationInsights* . Diagnósticos de Azure permite uno o varios receptores toobe definida si cada receptor también se declara en hello **PrivateConfig** sección.  
>
>

Hello receptores de los centros de eventos deben también se declaran y se definen en hello **PrivateConfig** sección de hello *wadcfgx* el archivo de configuración.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

Hola `SharedAccessKeyName` valor debe coincidir con una clave de firma de acceso compartido (SAS) y la directiva que se ha definido en hello **centros de eventos** espacio de nombres. Examinar el panel de centros de eventos de toohello en hello [portal de Azure](https://manage.windowsazure.com), haga clic en hello **configurar** y a configurar una directiva con nombre (por ejemplo, "SendRule") que tiene *enviar* permisos. Hola **StorageAccount** también se declara en **PrivateConfig**. No hay valores toochange aquí si están funcionando. En este ejemplo, se deje Hola valores vacíos, que es un inicio de sesión que un recurso de nivel inferior establecerá los valores de hello. Por ejemplo, hello *ServiceConfiguration.Cloud.cscfg* archivo de configuración de entorno establece los nombres de entorno que le corresponda hello y las claves.  

> [!WARNING]
> clave de SAS de concentradores de eventos de Hola se almacena en texto sin formato en hello *wadcfgx* archivo. A menudo, esta clave se comprueba en el control de código de toosource o está disponible como un recurso en el servidor de compilación, por lo que debería proteger según corresponda. Se recomienda usar una clave de SAS con *solo enviar* permisos para que un usuario malintencionado puede escribir toohello concentrador de eventos, pero no escuchar tooit o administrarlo.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Configurar diagnósticos de Azure toosend registros y métricas tooEvent centros
Según lo descrito anteriormente, todos los datos de diagnóstico personalizado y predeterminado, es decir, las métricas y los registros, se envía automáticamente tooAzure almacenamiento en intervalos de hello configurado. Con los concentradores de eventos y cualquier receptor adicional, puede especificar cualquier nodo raíz u hoja en hello jerarquía toobe enviado toohello concentrador de eventos. Esto incluye eventos ETW, contadores de rendimiento, registros de eventos de Windows y registros de aplicaciones.   

Es importante tooconsider cuántos puntos de datos se deben transferir tooEvent concentradores. Normalmente, los desarrolladores transfieren datos de ruta de acceso activa y de baja latencia que deben consumirse e interpretarse rápidamente. Los sistemas que supervisan las alertas o las reglas de escalado automático son algunos ejemplos. Un desarrollador también puede configurar un almacén de búsqueda o un almacén de análisis alternativo (por ejemplo, Análisis de transmisiones de Azure, Elasticsearch, un sistema de supervisión personalizado o un sistema de supervisión favorito de terceros).

los siguientes Hola son algunas configuraciones de ejemplo.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

Hola ejemplo anterior, receptor de hello es toohello aplicado primario **PerformanceCounters** nodo en la jerarquía de hello, lo que significa que todos los secundarios **PerformanceCounters** enviará tooEvent concentradores.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

En el ejemplo anterior de hello, el receptor de hello es tooonly aplicado tres contadores: **solicitudes en cola**, **rechazar las solicitudes de**, y **% de tiempo de procesador**.  

Hello en el ejemplo siguiente se muestra cómo un programador puede limitar la cantidad de Hola de datos enviados toobe Hola métricas críticas que se usan para el estado de este servicio.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

En este ejemplo, receptores de hello es toologs aplicados y es filtrado seguimiento de nivel de tooerror solo.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Implementación y actualización de una aplicación de servicios en la nube y configuración de diagnósticos
Visual Studio proporciona la aplicación de Hola de ruta de acceso más fácil de hello toodeploy y configuración del receptor de los centros de eventos. tooview y editar archivo hello, abra hello *wadcfgx* un archivo en Visual Studio, editarlo y guardarlo. ruta de acceso de Hello es **proyecto de servicio de nube** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.  

En este momento, todos los e implementación actualizan acciones en Visual Studio, Visual Studio Team System y todos los comandos o scripts que se basan en MSBuild y usar hello **/t: publicar** destino incluyen hello *wadcfgx*  en proceso de empaquetado de Hola. Además, implementaciones y actualizaciones implementación hello tooAzure de archivo con extensión del agente de diagnósticos de Azure adecuada de hello en las máquinas virtuales.

Después de implementar la aplicación hello y la configuración de diagnósticos de Azure, verá inmediatamente actividad en el panel de Hola de concentrador de eventos de Hola. Esto indica que está listo toomove en los datos de ruta de acceso activa tooviewing hello en herramienta de cliente o los análisis de agente de escucha de Hola de su elección.  

Hola figura siguiente, panel de centros de eventos de hello muestra envío correcto de inicio de diagnóstico datos toohello evento concentrador algún tiempo después de 23: 00. Es decir, cuando se implementó la aplicación hello con un controlador actualizado, *wadcfgx* de archivos y Hola receptor se configuró correctamente.

![][0]  

> [!NOTE]
> Al realizar el archivo de configuración de diagnósticos de Azure actualizaciones toohello (.wadcfgx), se recomienda que realice una inserción Hola actualizaciones toohello toda aplicación, así como la configuración de hello mediante la publicación de Visual Studio o un script de Windows PowerShell.  
>
>

## <a name="view-hot-path-data"></a>Ver los datos de la ruta de acceso activa
Según lo descrito anteriormente, hay muchos casos de uso de escucha tooand procesamiento de datos de los centros de eventos.

Una estrategia sencilla consiste toocreate un concentrador de eventos de prueba pequeñas consola aplicación toolisten toohello y flujo de salida de impresión Hola. Puede colocar Hola siguiente código, que se explica con más detalle en [empezar a trabajar con concentradores de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), en una aplicación de consola.  

Tenga en cuenta que la aplicación de consola de hello debe incluir hello [paquete NuGet de Host de procesador de eventos](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Recuerde que los valores de hello tooreplace corchetes angulares en hello **Main** función con valores de los recursos.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Solución de problemas con los receptores de Event Hubs
* Centro de eventos de Hello no muestra la actividad de evento entrante o saliente según lo previsto.

    Compruebe que el centro de eventos esté correctamente aprovisionado. Toda la información de conexión en hello **PrivateConfig** sección de *wadcfgx* deben coincidir con los valores de hello de su recurso tal como se muestra en el portal de Hola. Asegúrese de que tiene una directiva SAS definida ("SendRule" en el ejemplo de Hola) en el portal de Hola y que *enviar* se concede el permiso.  
* Después de una actualización, centro de eventos de hello ya no muestra la actividad de evento entrante o saliente.

    En primer lugar, asegúrese de que ese concentrador de eventos de Hola y obtener información de configuración es correcta como se explicó anteriormente. A veces Hola **PrivateConfig** se restablece en una actualización de la implementación. Hola recomendado corrección es toomake cambios demasiado*wadcfgx* en Hola proyecto y, a continuación, insertar una actualización de la aplicación completa. Si esto no es posible, asegúrese de que esa actualización de diagnósticos de hello inserta una completa **PrivateConfig** que incluye la clave SAS Hola.  
* Se ha intentado sugerencias de Hola y centro de eventos de hello sigue sin funcionar.

    Pruebe a buscar en tabla de almacenamiento de Azure de Hola que contiene errores y los registros de diagnósticos de Azure propia: **WADDiagnosticInfrastructureLogsTable**. Una opción es toouse una herramienta como [Azure Storage Explorer](http://www.storageexplorer.com) cuenta de almacenamiento de tooconnect toothis, ver esta tabla y agregar una consulta de marca de tiempo en hello las últimas 24 horas. Puede usar la herramienta de hello tooexport un archivo .csv y ábralo en una aplicación como Microsoft Excel. Excel resulta fácil toosearch para las cadenas de tarjeta de llamada, como **EventHubs**, toosee se notifica el error.  

## <a name="next-steps"></a>Pasos siguientes
•    [Más información sobre Event Hubs](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Apéndice: Archivo de configuración completo de Diagnósticos de Azure (.wadcfgx): ejemplo
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

Hola complementario *ServiceConfiguration.Cloud.cscfg* para este ejemplo es similar a Hola siguiente.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

La configuración JSON equivalente para máquinas virtuales es la siguiente:
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](../event-hubs/event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
