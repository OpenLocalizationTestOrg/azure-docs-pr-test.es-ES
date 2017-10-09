---
title: "aaaScheduled eventos para máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Eventos programados utilizando el servicio de metadatos de Azure de Hola para en las máquinas virtuales de Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a>Servicio Azure Metadata: eventos programados (versión preliminar) para VM Windows

> [!NOTE] 
> Las vistas previas se realizan tooyou disponible en condición Hola acepta toohello términos de uso. Para obtener más información, consulte [Términos de uso complementarios de las Versiones Preliminares de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Eventos programados es uno de los subservicios de hello en hello Azure metadatos de servicio. Se encarga de mostrar información relacionada con eventos próximos (por ejemplo, un reinicio) para que la aplicación pueda prepararse para ellos y limitar las interrupciones. Está disponible para todos los tipos de máquina virtual de Azure, incluso para IaaS y PaaS. Eventos programados ofrece a las tareas de máquina Virtual tiempo tooperform preventivas efecto de hello toominimize de un evento. 

Scheduled Events está disponible para máquinas virtuales Linux y Windows. Para más información acerca de Scheduled Events en Linux, consulte [Scheduled Events para máquinas virtuales Linux](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>¿Por qué Scheduled Events?

Con los eventos programados, puede tomar medidas impacto de hello toolimit de mantenimiento de la plataforma intiated o las acciones iniciadas por el usuario en su servicio. 

Las cargas de trabajo de varias instancias, que utilizan el estado de replicación técnicas toomaintain, pueden ser vulnerable toooutages sucediendo en varias instancias. Esas interrupciones pueden dar lugar a tareas costosas (por ejemplo, volver a elaborar los índices) o, incluso, a una pérdida de las réplicas. 

En muchos casos, hello general disponibilidad del servicio se puede mejorar mediante la realización de una secuencia de cierre como transacciones en curso se completan (o canceladas), reasignar tareas tooother máquinas virtuales en clúster de hello (conmutación por error manual), o quitar Hola Máquina virtual de un grupo de equilibradores de carga de red. 

Hay casos donde notificando a un administrador sobre un evento próximo o registrar un evento de este tipo ayudará a mejorar la capacidad de servicio de Hola de las aplicaciones hospedadas en la nube de Hola.

Casos de uso de Azure Metadata Service superficies programado los eventos en los siguientes hello:
-   Mantenimiento iniciado por la plataforma (por ejemplo, la implementación del SO del host)
-   Llamadas iniciadas por el usuario (por ejemplo, si el usuario reinicia una VM o la vuelve a implementar)


## <a name="hello-basics"></a>conceptos básicos de Hola  

Servicio de metadatos de Azure expone información acerca de cómo ejecutar máquinas virtuales con un extremo de REST accesible desde dentro de hello máquina virtual. información de Hello está disponible a través de una dirección IP no enrutables para que no se expone fuera Hola máquina virtual.

### <a name="scope"></a>Scope
Eventos programados son tooall apareció máquinas virtuales en un servicio de nube o tooall máquinas virtuales en un conjunto de disponibilidad. Como resultado, debe comprobar hello `Resources` campo Hola evento tooidentify que las máquinas virtuales van toobe afectado. 

### <a name="discovering-hello-endpoint"></a>Detección de punto de conexión de Hola
En el caso de hello donde se crea una máquina Virtual en una red Virtual (VNet), está disponible en una dirección IP no enrutables estática, servicio de metadatos de hello `169.254.169.254`.
Si Hola Máquina Virtual no se crea dentro de una red Virtual, de los casos Hola predeterminados para los servicios de nube y máquinas virtuales de clásicas, lógica adicional es necesario toodiscover Hola extremo toouse. Consulte cómo demasiado toothis ejemplo toolearn[detectar el extremo de host de hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Control de versiones 
Hola servicio de metadatos de instancia tiene una versión. Versiones son obligatorias y la versión actual de hello es `2017-03-01`.

> [!NOTE] 
> Versiones anteriores de vista previa de los eventos programados formando Hola api-version {más reciente}. Este formato ya no se admite y dejará de utilizarse en hello futuras.

### <a name="using-headers"></a>Uso de encabezados
Al consultar Hola Metadata Service, debe proporcionar encabezado de hello `Metadata: true` solicitud de hello tooensure no se ha redirigido involuntariamente.

### <a name="enabling-scheduled-events"></a>Habilitación de eventos programados
Hello primera vez que se realiza una solicitud para los eventos programados, Azure implícitamente habilita Hola característica en la máquina Virtual. Como resultado, debe esperar una respuesta diferida en la primera llamada de seguridad tootwo minutos.

### <a name="user-initiated-maintenance"></a>Mantenimiento iniciado por el usuario
Mantenimiento de máquinas virtuales a través de hello portal de Azure, API, CLI, iniciada por el usuario o PowerShell da como resultado un evento programado. Esto le permite lógica de preparación de mantenimiento de tootest hello en la aplicación y permite la tooprepare de aplicación para el mantenimiento iniciada por el usuario.

Si se reinicia una máquina virtual, se programa un evento con el tipo `Reboot`. Si vuelve a implementar una máquina virtual, se programa un evento con el tipo `Redeploy`.

> [!NOTE] 
> Actualmente se puede programar sumultáneamente un máximo de 10 operaciones de mantenimiento iniciadas por el usuario. Este límite será más flexible antes de la disponibilidad general de eventos programados.

> [!NOTE] 
> Actualmente no se puede configurar ningún mantenimiento iniciado por el usuario que dé lugar a eventos programados. Está planeado que esta capacidad de configuración se lance en el futuro.

## <a name="using-hello-api"></a>Uso de API de Hola

### <a name="query-for-events"></a>Consulta de eventos
Puede consultar para los eventos programados basta con realizar Hola siguiente llamada:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Una respuesta contiene una matriz de eventos programados. Una matriz vacía significa que actualmente no hay eventos programados.
En caso de hello donde hay eventos programados, respuesta de hello contiene una matriz de eventos: 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Propiedades de evento
|Propiedad  |  Descripción |
| - | - |
| EventId | Es un identificador único global del evento. <br><br> Ejemplo: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| EventType | Es el impacto causado por el evento. <br><br> Valores: <br><ul><li> `Freeze`: Hola Máquina Virtual es toopause programada para algunos segundos. Hola CPU está suspendido, pero no hay ningún impacto en la memoria, los archivos abiertos o conexiones de red. <li>`Reboot`: Hola Máquina Virtual está programada para reiniciar el sistema (memoria no persistente se pierde). <li>`Redeploy`: Hola Máquina Virtual está programada toomove tooanother nodo (discos efímeros se pierden). |
| ResourceType | Es el tipo de recurso al que afecta este evento. <br><br> Valores: <ul><li>`VirtualMachine`|
| Recursos| Es la lista de recursos a la que afecta este evento. Esto se garantiza toocontain máquinas a lo sumo una [Actualizar dominio](manage-availability.md), pero no puede contener todas las máquinas de hello UD. <br><br> Ejemplo: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Estado de evento | Es el estado de este evento. <br><br> Valores: <ul><li>`Scheduled`: Este evento es toostart programada tarde Hola especificado en hello `NotBefore` propiedad.<li>`Started`: este evento se ha iniciado.</ul> Ya no `Completed` o alguna vez se proporciona una situación similar; eventos Hola ya no se devolverá cuando se completa el evento Hola.
| NotBefore| Hora a partir de la que puede iniciarse este evento. <br><br> Ejemplo: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Programación de eventos
Cada evento se programa una cantidad mínima de tiempo en hello futuras según el tipo de evento. Este tiempo se refleja en la propiedad `NotBefore` de un evento. 

|EventType  | Minimum Notice |
| - | - |
| Freeze| 15 minutos |
| Reboot | 15 minutos |
| Volver a implementar | 10 minutos |

### <a name="starting-an-event"></a>Inicio de un evento 

Una vez haya aprendido de próximos eventos y completado su lógica de cierre correcto, puede aprobar eventos pendientes de hello realizando una `POST` llamar al servicio de metadatos de toohello con hello `EventId`. Esto indica tooAzure que puede reducir notificación mínima Hola tiempo (cuando sea posible). 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Confirmación de un evento permite Hola evento tooproceed para todos los `Resources` en el caso de hello, no solo Hola máquina virtual que reconoce el evento Hola. Por lo tanto, puede elegir tooelect una confirmación de líder toocoordinate hello, que puede ser tan simple como máquina primera Hola Hola `Resources` campo.


## <a name="powershell-sample"></a>Ejemplo de PowerShell 

Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a>Ejemplo de C\# 

Hello en el ejemplo siguiente es de un cliente que se comunica con el servicio de metadatos de Hola.

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

Eventos programados se pueden representar utilizando Hola siguiendo las estructuras de datos:

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a>Ejemplo de Python 

Hola consultas de ejemplo siguientes Hola servicio de metadatos para los eventos programados y aprueba cada evento pendiente.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Pasos siguientes 

- Obtener más información acerca de la API a disposición de Hola Hola [servicio de metadatos de la instancia](instance-metadata-service.md).
- Obtenga información sobre cómo realizar [el mantenimiento planeado para máquinas virtuales Windows en Azure](planned-maintenance.md).

