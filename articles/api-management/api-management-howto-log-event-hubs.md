---
title: "aaaHow toolog eventos tooAzure concentradores de eventos de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>¿Cómo toolog eventos tooAzure concentradores de eventos de administración de API de Azure
Centros de eventos de Azure es un servicio de entrada de datos altamente escalable que puede introducir millones de eventos por segundo para que le permitirán procesar y analizar Hola grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones. Los concentradores de eventos actúa como Hola "puerta principal" para una canalización de eventos, y una vez que se recopilan los datos en un centro de eventos, se pueden transformar y almacenado con cualquier proveedor de análisis en tiempo real o adaptadores de almacenamiento y procesamiento por lotes. Los concentradores de eventos desacopla producción de hello de una secuencia de eventos de consumo de Hola de esos eventos, para que los consumidores de eventos pueden tener acceso a los eventos de hello en su propia programación.

Este artículo es una toohello complementaria [integrar la administración de API de Azure con los concentradores de eventos](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vídeo y se describe cómo los eventos de administración de API de toolog con los concentradores de eventos de Azure.

## <a name="create-an-azure-event-hub"></a>Crear un centro de eventos de Azure
un nuevo centro de eventos, inicio de sesión toohello toocreate [portal de Azure clásico](https://manage.windowsazure.com) y haga clic en **New**->**servicios de aplicaciones**->**Bus de servicio**  -> **Concentrador de eventos**->**creación rápida**. Escriba un nombre para el centro de eventos y la región. Seleccione una suscripción y elija un espacio de nombres. Si anteriormente no ha creado un espacio de nombres puede crear uno, escriba un nombre en hello **Namespace** cuadro de texto. Una vez configuradas todas las propiedades, haga clic en **crear un nuevo concentrador de eventos** toocreate Hola concentrador de eventos.

![Creación de un centro de eventos][create-event-hub]

A continuación, navegue toohello **configurar** pestaña para el nuevo centro de eventos y cree dos **directivas de acceso compartido**. Nombre hello primero **envío** y asígnele **enviar** permisos.

![Directiva de envío][sending-policy]

Nombre hello otra **recibir**, asígnele **escuchar** permisos y haga clic en **guardar**.

![Directiva de recepción][receiving-policy]

Cada directiva de acceso compartido permite que las aplicaciones toosend y recibir eventos tooand de hello concentrador de eventos. cadenas de conexión de hello tooaccess para estas directivas, vaya toohello **panel** ficha de hello centro de eventos y haga clic en **información de conexión**.

![Cadena de conexión][event-hub-dashboard]

Hola **envío** cadena de conexión se usa cuando el registro de eventos, hello y **recibir** se utiliza la cadena de conexión al descargar los eventos de hello concentrador de eventos.

![Cadena de conexión][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Creación de un registrador de administración de API
Ahora que tiene un concentrador de eventos, Hola siguiente paso es tooconfigure una [registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) en la administración de API de servicio para que puedan iniciar eventos toohello concentrador de eventos.

Registradores de administración de API se configuran mediante hello [API de REST de administración](http://aka.ms/smapi). Antes de usar Hola API de REST para hello primera vez, revise hello [requisitos previos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) y asegúrese de que tiene [habilitado acceso toohello API de REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate un registrador, asegúrese de una solicitud HTTP PUT con hello después de la plantilla de dirección URL.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Reemplace `{your service}` con el nombre de saludo de la instancia de servicio de administración de API.
* Reemplace `{new logger name}` con el nombre elegido hello para el registrador nuevo. Se hará referencia a este nombre cuando se configura hello [registro a eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) directiva

Agregar Hola después encabezados toohello solicitud.

* Content-Type : application/json
* Authorization : SharedAccessSignature 58...
  * Para obtener instrucciones acerca de cómo generar hello `SharedAccessSignature` vea [autenticación de API de REST de administración de API de Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Especifique el cuerpo de la solicitud de hello mediante Hola después de la plantilla.

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* `type`debe establecerse demasiado`AzureEventHub`.
* `description`Proporciona una descripción opcional del registrador de Hola y puede ser una cadena de longitud cero si lo desea.
* `credentials`contiene Hola `name` y `connectionString` de su centro de eventos de Azure.

Cuando se realiza la solicitud hello, si registrador Hola se crea un código de estado `201 Created` se devuelve.

> [!NOTE]
> Para conocer otros posibles códigos de retorno y sus razones, vea [Creación de un registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee cómo realizan otras operaciones, como la lista, update y delete, vea hello [registrador](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentación de entidad.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Configuración de directivas log-to-eventhubs
Una vez que el registrador está configurado en administración de API, puede configurar los eventos de registro para eventhubs directivas toolog Hola deseado. Hello registro a eventhubs directiva se puede usar en cualquier Hola sección de directiva de correo entrante o saliente directiva Hola.

las directivas tooconfigure, inicio de sesión toohello [portal de Azure](https://portal.azure.com), navegar por el servicio de administración de API de tooyour y haga clic en **portal para desarrolladores de** tooaccess Hola portal para desarrolladores.

![Portal del publicador][publisher-portal]

Haga clic en **directivas** en el menú de administración de API de Hola Hola izquierda, seleccione producto deseado hello y API y haga clic en **Agregar directiva**. En este ejemplo estamos agregando una directiva toohello **API de eco** en hello **Unlimited** producto.

![Add policy][add-policy]

Coloque el cursor en hello `inbound` directiva de sección y haga clic en hello **registro tooEventHub** hello tooinsert de directiva `log-to-eventhub` plantilla de directiva de instrucción.

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Reemplace `logger-id` con el nombre de Hola de registrador de administración de API de Hola que configuró en el paso anterior de Hola.

Puede usar cualquier expresión que devuelve una cadena como valor de Hola de hello `log-to-eventhub` elemento. En este ejemplo se registra una cadena que contiene Hola fecha y hora, nombre del servicio, Id. de solicitud, dirección ip de solicitud y nombre de la operación.

Haga clic en **guardar** toosave Hola actualiza la configuración de directiva. Tan pronto como se guarda Hola directivas estén activas y los eventos son toohello registrado designado concentrador de eventos.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de los centros de eventos de Azure
  * [Introducción a los centros de eventos de Azure](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Recepción de mensajes con EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guía de programación de Centros de eventos](../event-hubs/event-hubs-programming-guide.md)
* Obtener más información acerca de la integración de Administración de API y centros de eventos
  * [Referencia de entidad del registrador](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [referencia de la directiva log-to-eventhub](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Supervisión de API con Administración de API de Azure, Centros de eventos y Runscope](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Ver un tutorial en vídeo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
