---
title: "aaaScheduler entidades, términos y conceptos | Documentos de Microsoft"
description: "Conceptos del Programador de Azure, terminología y jerarquía de entidades, incluidos trabajos y colecciones de trabajos.  Proporciona un ejemplo completo de un trabajo programado."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>Conceptos, terminología y jerarquía de entidades de Programador
## <a name="scheduler-entity-hierarchy"></a>Jerarquía de entidades del Programador
Hello tabla siguiente describe recursos principales de hello expuestos o utilizados por hello API del programador:

| Recurso | Description |
| --- | --- |
| **Colección de trabajos** |Una colección de trabajos contiene un grupo de trabajos y mantiene los valores, cuotas y aceleradores compartidos por los trabajos en la colección de Hola. La colección de trabajos la crea el propietario de la suscripción y agrupa los trabajos en función de los límites de uso o de la aplicación. Es región tooone restringida. También permite cumplimiento Hola de cuotas de uso de hello tooconstrain de todos los trabajos en esa colección. las cuotas de Hello incluyen MaxJobs y MaxRecurrence. |
| **Trabajo** |Un trabajo define una única acción periódica, con estrategias simples o complejas para su ejecución. Las acciones pueden incluir solicitudes HTTP, de cola de almacenamiento, de cola de bus de servicio o de tema de bus de servicio. |
| **Historial de trabajos** |Un historial de trabajos representa los detalles de una ejecución de un trabajo. Contiene los trabajos realizados correctamente y los errores, así como los detalles de las respuestas. |

## <a name="scheduler-entity-management"></a>Administración de entidades de Programador
En un nivel alto, programador de Hola y API de administración de servicios de hello exponen hello las siguientes operaciones en recursos de hello:

| Capacidad | Descripción y dirección URI |
| --- | --- |
| **Administración de la colección de trabajos** |GET, PUT y DELETE permiten la creación y modificación de las colecciones de trabajos y trabajos de hello contenidos en él. Una colección de trabajos es un contenedor para trabajos y asigna tooquotas y la configuración compartida. Ejemplos de cuotas, descritos más adelante, son el número máximo de trabajos y un intervalo menor de periodicidad. <p>PUT y DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **Administración de trabajos** |GET, PUT, POST, PATCH y DELETE permiten la creación y modificación de trabajos. Todos los trabajos deben pertenecer a colección de trabajos de tooa que ya existe, así que no hay ninguna creación implícita. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **Administración del historial de trabajos** |GET admite la recuperación de 60 días de historial de ejecución de trabajos, como el tiempo de trabajo transcurrido y los resultados de la ejecución del trabajo. Agrega compatibilidad de parámetros de cadena de consulta para filtrar basándose en el estado y la situación. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>Tipos de trabajo
Hay varios tipos de trabajos: trabajos HTTP (incluidos trabajos HTTPS que admiten SSL), trabajos de cola de almacenamiento, trabajos de cola de bus de servicio y trabajos de tema de bus de servicio. Los trabajos HTTP son perfectos si dispone de un extremo de una carga de trabajo o servicio existente. Puede utilizar la cola trabajos toopost mensajes toostorage las colas de almacenamiento, por lo que dichos trabajos son ideales para cargas de trabajo que utilizan colas de almacenamiento. De forma similar, los trabajos de bus de servicio son ideales para cargas de trabajo que usan temas y colas de bus de servicio.

## <a name="hello-job-entity-in-detail"></a>entidad de "trabajo" Hello en detalle
En un nivel básico, un trabajo programado cuenta con varias partes:

* Hola tooperform acción cuando se activa el temporizador de trabajo de Hola  
* Trabajo hello toorun Hola (opcional)  
* (Opcional) Cuándo y con qué frecuencia trabajo de hello toorepeat  
* (Opcional) Un toofire de acción si se produce un error en la acción principal de Hola  

Internamente, un trabajo programado contiene también datos proporcionados por el sistema como Hola siguiente hora de ejecución programada.

Hola siguiente código proporciona un ejemplo completo de un trabajo programado. En las secciones siguientes se proporcionan los detalles.

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

Tal como se muestra en la anterior de trabajo programado de ejemplo de Hola, una definición de trabajo tiene varias partes:

* Hora de inicio ("startTime")  
* Acción ("action"), que incluye la acción del error ("errorAction")
* Periodicidad ("recurrence")  
* Situación ("state")  
* Estado ("status")  
* Directiva de reintentos (“retryPolicy”)  

Examinemos cada uno de ellos en detalle:

## <a name="starttime"></a>startTime
Hola "startTime" es la hora de inicio de Hola y permite Hola llamador toospecify una zona horaria de desplazamiento en el cable hello en [formato ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).

## <a name="action-and-erroraction"></a>action y errorAction
Hola "action" es la acción de hello invocada cada vez y describe un tipo de invocación del servicio. acción de Hello es lo que se ejecutará en hello proporcionada programación. El Programador admite acciones HTTP, de cola de almacenamiento, de cola de bus de servicio y de tema de bus de servicio.

acción de Hello en el ejemplo de Hola anterior es una acción HTTP. A continuación se muestra un ejemplo de una acción de cola de almacenamiento:

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

A continuación se muestra un ejemplo de una acción de tema de bus de servicio.

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

A continuación se muestra un ejemplo de una acción de cola de bus de servicio.

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

Hola "errorAction" es el controlador de errores de hello, acción de Hola se invoca cuando se produce un error en la acción principal de Hola. Puede usar esta variable toocall un punto de conexión de control de errores o enviar una notificación al usuario. Esto se puede utilizar para llegar a un extremo secundario en caso de hello ese Hola principal no está disponible (p. ej., en caso de hello de un desastre en el sitio del punto de conexión de hello) o puede usarse para notificar a un punto de conexión de control de errores. Igual que la acción principal de hello, acción de error de hello puede ser lógica sencilla o compuesta basada en otras acciones. toolearn cómo toocreate un token de SAS, consulte demasiado[crear y usar una firma de acceso compartido](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="recurrence"></a>recurrence
La periodicidad tiene varias partes:

* Frecuencia: un minuto, hora, día, semana, mes, año  
* Intervalo: El intervalo en hello dada la frecuencia de repetición de Hola  
* Programación prescrita: especifique minutos, horas, días de la semana, meses y días mes para de periodicidad de Hola  
* Recuento: número de repeticiones  
* Hora de finalización: trabajos se ejecutarán después de hello especifica hora de finalización  

Un trabajo es periódico si tiene un objeto de periodicidad especificado en la definición de JSON. Si se especifican el recuento y la hora de finalización, se respeta la regla de finalización Hola que ocurra primero.

## <a name="state"></a>state
estado de Hello del trabajo de hello es uno de cuatro valores: habilitado, deshabilitado, completado o con errores. Puede colocar o revisión lo trabajos como tooupdate les toohello habilita o deshabilita el estado. Si un trabajo se ha completado o con errores, que es un estado final que no se puede actualizar (aunque todavía se puede eliminar el trabajo de hello). Un ejemplo de la propiedad state de hello es como sigue:

        "state": "disabled", // enabled, disabled, completed, or faulted
Los trabajos completados y con errores se eliminan después de 60 días.

## <a name="status"></a>status
Cuando se inicia un trabajo del programador, se devolverá información sobre el estado actual de Hola de trabajo de Hola. Este objeto no es configurable por el usuario de hello: se establece por sistema Hola. Sin embargo, se incluye en hello objeto de trabajo (en lugar de un recurso vinculado independiente) para que se pueda obtener estado de Hola de un trabajo fácilmente.

Estado del trabajo incluye el tiempo de Hola Hola anterior de la ejecución de (si existe) Hola momento de la siguiente ejecución programada hello (para los trabajos en curso) y el recuento de la ejecución del trabajo de Hola Hola.

## <a name="retrypolicy"></a>retryPolicy
Si se produce un error en un trabajo del programador, es posible toospecify un toodetermine de directiva de reintentos si y cómo se vuelve a intentar la acción de Hola. Esto viene determinado por hello **retryType** objeto: se establece demasiado**ninguno** si no hay ninguna directiva de reintentos, como se indicó anteriormente. Establézcalo demasiado**fijo** si hay una directiva de reintentos.

tooset una directiva de reintentos, se pueden especificar dos configuraciones adicionales: un intervalo de reintentos (**retryInterval**) y Hola número de reintentos (**retryCount**).

intervalo de reintento de Hello, especificado con hello **retryInterval** de objetos, es Hola intervalo entre reintentos. Su valor predeterminado es de 30 segundos, su valor configurable mínimo es de 15 segundos y su valor máximo es de 18 meses. Los trabajos de las colecciones de trabajos gratis tienen un valor configurable mínimo de 1 hora.  Se define en formato ISO 8601 Hola. De forma similar, Hola de número de Hola de reintentos se expresa con hello **retryCount** objeto; es Hola número de veces que se realiza un reintento. Su valor predeterminado es 4, y su valor máximo es 20\. Ambos **retryInterval** y **retryCount** son opcionales. Tienen sus valores predeterminados si **retryType** se establece demasiado**fijo** y se especifica explícitamente ningún valor.

## <a name="see-also"></a>Otras referencias
 [¿Qué es Programador?](scheduler-intro.md)

 [Empezar a usar a Scheduler en hello portal de Azure](scheduler-get-started-portal.md)

 [Planes y facturación en Programador de Azure](scheduler-plans-billing.md)

 [¿Cómo se programa toobuild complejo y periodicidad avanzada con el programador de Azure](scheduler-advanced-complexity.md)

 [Referencia de API de REST de Programador de Azure](https://msdn.microsoft.com/library/mt629143)

 [Referencia de cmdlets de PowerShell de Programador de Azure](scheduler-powershell-reference.md)

 [Alta disponibilidad y confiabilidad de Programador de Azure](scheduler-high-availability-reliability.md)

 [Límites, valores predeterminados y códigos de error de Programador de Azure](scheduler-limits-defaults-errors.md)

 [Autenticación de salida de Programador de Azure](scheduler-outbound-authentication.md)

