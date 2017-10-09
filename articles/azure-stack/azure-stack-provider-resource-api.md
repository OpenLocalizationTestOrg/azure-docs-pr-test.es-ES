---
title: API de uso de recursos aaaProvider | Documentos de Microsoft
description: "Referencia de la API de uso de recursos, que recupera información de uso de Azure Stack."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b6055923-b6a6-45f0-8979-225b713150ae
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: alfredop
ms.openlocfilehash: 7cc2d7af27e6abc86e247b2ed0ab1bc236fdb1af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provider-resource-usage-api"></a>API de uso de recursos de proveedor
proveedor de Hello término aplica toohello Administrador de servicios y proveedores de tooany delegado. Administradores de servicios y proveedores de delegado pueden usar la API de uso de proveedor tooview Hola de uso de sus inquilinos directa. Por ejemplo, P0 puede llamar a la información de uso de tooget de API de proveedor de hello en el uso directo de P1 y de P2 y P1 puede llamar para obtener información de uso sobre P3 y P4.

![Modelo conceptual de la jerarquía de proveedores](media/azure-stack-provider-resource-api/image1.png)

## <a name="api-call-reference"></a>Referencia de llamadas a la API
### <a name="request"></a>Solicitud
Hola solicitud obtiene detalles del consumo de hello había solicitado suscripciones y Hola solicita el período de tiempo. No hay ningún cuerpo de solicitud.

Este uso de API es una API de proveedor, por lo que el llamador de hello debe asignarse a un rol de lector, Colaborador o propietario de la suscripción del proveedor de Hola.

| **Método** | **URI de solicitud** |
| --- | --- |
| GET |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&subscriberId={sub1.1}&api-version=2015-06-01-preview&continuationToken={token-value} |

### <a name="arguments"></a>Argumentos
| **Argumento** | **Descripción** |
| --- | --- |
| *armendpoint* |Punto de conexión de Azure Resource Manager del entorno de Azure Stack. Hola convención de pila de Azure es el nombre hello de Azure Resource Manager extremo está en formato de hello `https://adminmanagement.{domain-name}`. Por ejemplo, nombre de dominio es local.azurestack.external si hello, entonces es el punto de conexión de administrador de recursos de hello `https://adminmanagement.local.azurestack.external`. |
| *subId* |Identificador de suscripción del usuario de Hola que está realizando la llamada de Hola. |
| *reportedStartTime* |Hora de inicio de consulta de Hola. Hola valor para *DateTime* debe estar en hora UTC y al principio de Hola de hora de hello, por ejemplo, 13:00. Agregaciones diarias, establecer este medianoche tooUTC de valor. formato de Hello es *caracteres de escape* ISO 8601, por ejemplo, 2015-06-16T18% 3a53% 3a11% 2b00% 3a00Z, donde dos puntos se escapa demasiado % 3a y además se escapa demasiado % 2b para que esté URI descriptivo. |
| *reportedEndTime* |Hora de finalización de la consulta de Hola. Hola restricciones que se aplican demasiado*reportedStartTime* toothis argumento también se aplican. Hola valor para *reportedEndTime* no puede estar en el futuro de Hola o hello fecha actual. Si es así, el resultado de hello se establece demasiado "procesamiento no está completo." |
| *aggregationGranularity* |Parámetro opcional que tiene dos valores posibles discretos: días y horas. Como sugieren los valores de hello, uno devuelve datos Hola granularidad diaria y Hola otro es una resolución por horas. opción diario de Hello es Hola predeterminada. |
| *subscriberId* |Id. de suscripción. tooget de los datos filtrados, Hola Id. de suscripción de un inquilino directa del proveedor de hello es necesaria. Si no se especifica ningún parámetro de identificador de suscripción, llamada de hello devuelve datos de uso para inquilinos directa del proveedor de todos los Hola. |
| *api-version* |Versión del protocolo de hello es toomake usado esta solicitud. Este valor se establece too2015-06-01-versión preliminar. |
| *continuationToken* |Símbolo (token) recupera Hola última llamada toohello API de uso proveedor. Este token es necesario cuando una respuesta es superior a 1.000 líneas y actúa como un marcador para el progreso de Hola. Si no lo está, Hola principio de hello del día de Hola o de hora, en función de la granularidad de hello pasa se recuperan los datos. |

### <a name="response"></a>Response
GET /subscriptions/sub1/providers/Microsoft.Commerce/subscriberUsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&subscriberId=sub1.1&api-version=1.0

{

"value": \[

{

"id": "/subscriptions/sub1.1/providers/Microsoft.Commerce/UsageAggregate/sub1.1-

meterID1",

"name": "sub1.1-meterID1",

"type": "Microsoft.Commerce/UsageAggregate",

"properties": {

"subscriptionId":"sub1.1",

"usageStartTime": "2015-03-03T00:00:00+00:00",

"usageEndTime": "2015-03-04T00:00:00+00:00",

"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\

":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",

"quantity":2.4000000000,

"meterId":"meterID1"

}

},

…

### <a name="response-details"></a>Detalles de la respuesta
| **Argumento** | **Descripción** |
| --- | --- |
| *id* |Identificador único del uso de hello agregado |
| *name* |Nombre de agregado de uso de Hola |
| *type* |Definición de recursos |
| *subscriptionId* |Identificador de suscripción del usuario de la pila de Azure de Hola |
| *usageStartTime* |UTC hora de inicio de hello uso depósito toowhich pertenece este agregado de uso |
| *usageEndTime* |Hora de hello uso depósito toowhich pertenece este agregado de uso de finalización UTC |
| *instanceData* |Pares de clave y valor de los detalles de la instancia (con un formato nuevo):<br> *resourceUri*: nombre completo e incluir el identificador de recurso, que incluye grupos de recursos de Hola y el nombre de instancia de Hola <br> *location*: región en la que se ejecutó este servicio <br> *etiquetas*: las etiquetas del recurso que se especifican por usuario de Hola <br> *additionalInfo*: más detalles sobre los recursos de hello consumido, por ejemplo, tipo de imagen o la versión de sistema operativo |
| *quantity* |Cantidad de consumo de recursos que se produjo en este período de tiempo |
| *meterId* |Identificador único para el recurso de Hola que se consumió (también denominada *ResourceID*) |

## <a name="next-steps"></a>Pasos siguientes
[Referencia de la API de uso de recursos de inquilino](azure-stack-tenant-resource-usage-api.md)

[Preguntas más frecuentes relacionadas con la utilización](azure-stack-usage-related-faq.md)

