---
title: API de uso de recursos aaaTenant | Documentos de Microsoft
description: "Referencia de la API de uso de recursos, que recupera información de uso de Azure Stack."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: b9d7c7ee-e906-4978-92a3-a2c52df16c36
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: eb826aba87b3b5b79155d9003162f2b5e6871f82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tenant-resource-usage-api"></a>API de uso de recursos de inquilino
Un inquilino puede utilizar datos de uso de recursos del inquilino de hello API de inquilinos tooview Hola. Esta API es coherente con hello API de uso de Azure (actualmente en private preview).

Puede usar el cmdlet de Windows PowerShell de hello **UsageAggregates Get** tooget los datos de uso, como en Azure.

## <a name="api-call"></a>Llamada a la API
### <a name="request"></a>Solicitud
Hola solicitud obtiene detalles del consumo de hello había solicitado suscripciones y Hola solicita el período de tiempo. No hay ningún cuerpo de solicitud.

| **Método** | **URI de solicitud** |
| --- | --- |
| GET |https://{armendpoint}/subscriptions/{subId}/providers/Microsoft.Commerce/usageAggregates?reportedStartTime={reportedStartTime}&reportedEndTime={reportedEndTime}&aggregationGranularity={granularity}&api-version=2015-06-01-preview&continuationToken={token-value} |

### <a name="arguments"></a>Argumentos
| **Argumento** | **Descripción** |
| --- | --- |
| *Armendpoint* |Punto de conexión de Azure Resource Manager del entorno de Azure Stack. Hola convención de pila de Azure es el nombre hello de Azure Resource Manager extremo está en formato de hello `https://management.{domain-name}`. Por ejemplo, nombre de dominio es local.azurestack.external si hello, entonces es el punto de conexión de administrador de recursos de hello `https://management.local.azurestack.external`. |
| *subId* |Identificador de suscripción del usuario de Hola que está realizando la llamada de Hola. Puede usar este tooquery única API para el uso de una sola suscripción. Proveedores pueden usar el uso de la API de uso de recursos de proveedor tooquery Hola para todos los inquilinos. |
| *reportedStartTime* |Hora de inicio de consulta de Hola. Hola valor para *DateTime* debe estar en hora UTC y al principio de Hola de hora de hello, por ejemplo, 13:00. Agregaciones diarias, establecer este medianoche tooUTC de valor. formato de Hello es *caracteres de escape* ISO 8601, por ejemplo, 2015-06-16T18% 3a53% 3a11% 2b00% 3a00Z, donde dos puntos se escapa demasiado % 3a y además se escapa demasiado % 2b para que esté URI descriptivo. |
| *reportedEndTime* |Hora de finalización de la consulta de Hola. Hola restricciones que se aplican demasiado*reportedStartTime* toothis argumento también se aplican. Hola valor para *reportedEndTime* no puede estar en hello futuras. |
| *aggregationGranularity* |Parámetro opcional que tiene dos valores posibles discretos: días y horas. Como sugieren los valores de hello, uno devuelve datos Hola granularidad diaria y Hola otro es una resolución por horas. opción diario de Hello es Hola predeterminada. |
| *api-version* |Versión del protocolo de hello es toomake usado esta solicitud. Debe usar 2015-06-01-preview. |
| *continuationToken* |Símbolo (token) recupera Hola última llamada toohello API de uso proveedor. Este token es necesario cuando una respuesta es superior a 1.000 líneas y actúa como un marcador para el progreso. Si no lo está, Hola principio de hello del día de Hola o de hora, en función de la granularidad de hello pasa se recuperan los datos. |

### <a name="response"></a>Response
GET /subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregates?reportedStartTime=reportedStartTime=2014-05-01T00%3a00%3a00%2b00%3a00&reportedEndTime=2015-06-01T00%3a00%3a00%2b00%3a00&aggregationGranularity=Daily&api-version=1.0

{

"value": \[

{

"id": "/subscriptions/sub1/providers/Microsoft.Commerce/UsageAggregate/sub1-meterID1",

"name": "sub1-meterID1",

"type": "Microsoft.Commerce/UsageAggregate",

"properties": {

"subscriptionId":"sub1",

"usageStartTime": "2015-03-03T00:00:00+00:00",

"usageEndTime": "2015-03-04T00:00:00+00:00",

"instanceData":"{\\"Microsoft.Resources\\":{\\"resourceUri\\":\\"resourceUri1\\",\\"location\\":\\"Alaska\\",\\"tags\\":null,\\"additionalInfo\\":null}}",

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
| *subscriptionId* |Identificador de la suscripción del programa Hola a usuario de Azure |
| *usageStartTime* |UTC hora de inicio de hello uso depósito toowhich pertenece este agregado de uso |
| *usageEndTime* |Hora de hello uso depósito toowhich pertenece este agregado de uso de finalización UTC |
| *instanceData* |Pares de clave y valor de los detalles de la instancia (con un formato nuevo):<br>  *resourceUri*: identificador de recurso completo, incluidos los grupos de recursos y el nombre de instancia <br>  *location*: región en la que se ejecutó este servicio <br>  *etiquetas*: especifica ese usuario Hola de las etiquetas del recurso <br>  *additionalInfo*: más detalles sobre los recursos de hello consumido, por ejemplo, tipo de imagen o la versión de sistema operativo |
| *quantity* |Cantidad de consumo de recursos que se produjo en este período de tiempo |
| *meterId* |Identificador único para el recurso de Hola que se consumió (también denominada *ResourceID*) |

## <a name="next-steps"></a>Pasos siguientes
[API de uso de recursos de proveedor](azure-stack-provider-resource-api.md)

[Preguntas más frecuentes relacionadas con la utilización](azure-stack-usage-related-faq.md)

