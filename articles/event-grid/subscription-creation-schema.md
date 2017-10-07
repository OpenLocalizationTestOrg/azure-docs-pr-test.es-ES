---
title: "esquema de suscripción de cuadrícula de eventos de aaaAzure"
description: "Describe las propiedades de Hola para suscribir el evento tooan con cuadrícula de eventos de Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>Esquema de suscripción de Event Grid

toocreate una suscripción de la cuadrícula de eventos, debe enviar una operación de suscripción de Create Event toohello de solicitud. Usar hello siguiendo el formato:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Por ejemplo, toocreate una suscripción de eventos para una cuenta de almacenamiento denominada `examplestorage` en un grupo de recursos denominado `examplegroup`, formato uso Hola siguiente:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Hola artículo describen propiedades Hola y el esquema de cuerpo de saludo de solicitud de Hola.
 
## <a name="event-subscription-properties"></a>Propiedades de la suscripción de eventos

| Propiedad | Escriba | Descripción |
| -------- | ---- | ----------- |
| de destino | objeto | objeto de Hola que define el punto de conexión de Hola. |
| filter | objeto | Un campo opcional para filtrar los tipos de Hola de eventos. |

### <a name="destination-object"></a>Objeto de destino

| Propiedad | Escriba | Descripción |
| -------- | ---- | ----------- |
| endpointType | cadena | tipo de Hola de punto de conexión para la suscripción de hello (webhook/HTTP, centro de eventos o cola). | 
| endpointUrl | cadena |  | 

### <a name="filter-object"></a>Objeto de filtro

| Propiedad | Escriba | Descripción |
| -------- | ---- | ----------- |
| includedEventTypes | array | Coincide con cuando el tipo de evento de hello en mensajes de bienvenida del evento es un tooone coincidencias exactas de estos nombres de tipo de evento. Genera un error cuando el nombre del evento no coincide con los nombres de tipo de evento de hello registrado para el origen del evento de Hola. El valor predeterminado coincide con todos los tipos de evento. |
| subjectBeginsWith | cadena | Un campo coincidencia de prefijo filtro toohello asunto en mensajes de bienvenida del evento. valor predeterminado de Hola o la cadena vacía se ajusta a todas. | 
| subjectEndsWith | cadena | Un sufijo-match filtro toohello campo de asunto en mensajes de bienvenida del evento. valor predeterminado de Hola o la cadena vacía se ajusta a todas. |
| subjectIsCaseSensitive | cadena | Controla la coincidencia que distingue mayúsculas de minúsculas en los filtros. |


## <a name="example-subscription-schema"></a>Esquema de suscripción de ejemplo

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>Pasos siguientes

* Para una cuadrícula de introducción tooEvent, consulte [¿qué es la cuadrícula de eventos?](overview.md)
