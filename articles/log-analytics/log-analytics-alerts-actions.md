---
title: "aaaResponses tooalerts en análisis de registros de OMS | Documentos de Microsoft"
description: "Alertas de análisis de registros identificar información importante en el repositorio OMS y se pueden proactivamente avisarle de problemas o invocar acciones tooattempt toocorrect ellos.  Este artículo describe cómo toocreate una regla de alerta y las diferentes acciones de Hola de detalles que pueden tomar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Agregue reglas de tooalert de acciones de análisis de registros
Cuando un [alerta se crea en el análisis de registros](log-analytics-alerts.md), tiene la opción de Hola de [configurar regla de alerta de hello](log-analytics-alerts.md) tooperform una o más acciones.  Este artículo describe hello las diferentes acciones que están disponibles y los detalles sobre la configuración de cada tipo.

| Acción | Descripción |
|:--|:--|
| [Correo electrónico](#email-actions) | Enviar un correo electrónico con detalles de Hola de tooone alerta Hola o más destinatarios. |
| [Webhook](#webhook-actions) | Invoca un proceso externo a través de una sola solicitud HTTP POST. |
| [Runbook](#runbook-actions) | Inicia un runbook en Azure Automation. |


## <a name="email-actions"></a>Acciones de correo electrónico
Acciones de correo electrónico envíen un correo electrónico con los detalles de Hola de tooone alerta Hola o más destinatarios.  Puede especificar a asunto Hola de correo electrónico de hello, pero su contenido es un formato estándar que se construye mediante el análisis de registros.  Incluye información de resumen, como nombre de Hola de alerta de hello toodetails de adición de registros de tooten devuelto por la búsqueda de registros de Hola.  También incluye una búsqueda de registros de vínculo tooa de análisis de registros que devolverá el conjunto completo de Hola de registros desde una consulta.   Hola remitente de correo electrónico de hello es *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* . 

Acciones de correo electrónico requieren propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Asunto |Asunto de correo electrónico de Hola.  No se puede modificar el cuerpo de saludo del mensaje de Hola. |
| Recipients |Direcciones de todos los destinatarios de correo electrónico.  Si especifica más de una dirección y, a continuación, direcciones de hello independiente con un punto y coma (;). |


## <a name="webhook-actions"></a>Acciones de webhook

Las acciones de Webhook permiten tooinvoke un proceso externo a través de una única solicitud HTTP POST.  servicio de Hola que se llama debe admitir webhooks y determinar cómo va a utilizar cualquier carga recibe.  También puede llamar a una API de REST que no admiten específicamente webhooks siempre que sea de solicitud de hello en un formato que Hola que API entiende.  Ejemplos de uso de un webhook de alerta de tooan de respuesta envían un mensaje [Slack](http://slack.com) o crear un incidente en [PagerDuty](http://pagerduty.com/).  Está disponible en un tutorial completo de creación de una regla de alerta con una demora de webhook toocall [Webhooks en las alertas de análisis de registros](log-analytics-alerts-webhooks.md).

Acciones de Webhook requieren propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Dirección URL de Webhook |dirección URL de Hola de hello webhook. |
| Carga de JSON personalizada |Carga personalizada toosend con hello webhook.  Consulte a continuación para más información. |


Webhooks incluir una dirección URL y una carga con el formato JSON que es datos de hello envía toohello de servicio externo.  De forma predeterminada, carga Hola incluirá los valores de hello en hello en la tabla siguiente.  Puede elegir tooreplace esta carga con uno personalizado propio.  En ese caso se puede utilizar Hola variables de tabla de Hola para cada uno de hello parámetros tooinclude su valor en la carga útil personalizada.

| Parámetro | Variable | Descripción |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Nombre de regla de alerta de Hola. |
| AlertThresholdOperator |#thresholdoperator |Operador de umbral para la regla de alerta de Hola.  *Mayor que* o *menor que*. |
| AlertThresholdValue |#thresholdvalue |Valor de umbral para la regla de alerta de Hola. |
| LinkToSearchResults |#linktosearchresults |Vincule la búsqueda de registros de análisis de tooLog que devuelve registros de Hola de consulta de Hola que creó la alerta de Hola. |
| ResultCount |#searchresultcount |Número de registros en los resultados de búsqueda de Hola. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Hora de finalización de la consulta de hello en formato UTC. |
| SearchIntervalInSeconds |#searchinterval |Período de tiempo para la regla de alerta de Hola. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Hora de inicio para consulta de hello en formato UTC. |
| SearchQuery |#searchquery |Consulta de búsqueda de registro utilizado por la regla de alerta de Hola. |
| SearchResults |Consulte a continuación |Registros devueltos por la consulta de hello en formato JSON.  Limitado toohello 5.000 primeros registros. |
| WorkspaceID |#workspaceid |Identificador del área de trabajo de OMS. |

Por ejemplo, podría especificar Hola después carga personalizada que incluya un parámetro único denominado *texto*.  servicio de Hola que llama a este webhook podría esperarse este parámetro.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Esta carga en el ejemplo se resolvería toosomething como Hola siguientes cuando envía toohello webhook.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

resultados de la búsqueda de tooinclude en una carga personalizada, agregue Hola después de línea como una propiedad de nivel superior en la carga de json de Hola.  

    "IncludeSearchResults":true

Por ejemplo, una carga personalizada que incluye solo nombre de la alerta hello y resultados de la búsqueda de hello toocreate, podría utilizar Hola después. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Puede comenzar con un ejemplo completo de creación de un servicio externo en una regla de alerta con un toostart webhook [crear una acción de alerta webhook en análisis de registros de OMS toosend mensaje tooSlack](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Acciones de runbook
Las acciones de runbook inician un runbook en Automatización de Azure.  En orden toouse para este tipo de acción, debe tener hello [solución de automatización](log-analytics-add-solutions.md) instalado y configurado en el área de trabajo OMS.  Puede seleccionar desde los runbooks de hello en la cuenta de automatización de Hola que configuró en hello solución de automatización.

Acciones de runbook requieren propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:---|
| Runbook | Runbook que desea toostart cuando se crea una alerta. |
| Ejecutar en | Especifique **Azure** toorun Hola runbook en la nube de Hola.  Especifique **Hybrid worker** toorun Hola runbook en un agente con [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) instalado.  |

Acciones de runbook iniciar Hola runbook mediante una [webhook](../automation/automation-webhooks.md).  Cuando se crea la regla de alerta de hello, creará automáticamente un webhook nuevo runbook de hello con nombre hello **corrección de alerta de OMS** seguido de un GUID.  

Directamente no se puede rellenar los parámetros de runbook de hello, pero Hola [$WebhookData parámetro](../automation/automation-webhooks.md) incluirá información de Hola de alerta de hello, incluidos los resultados de Hola Hola de búsqueda de registros que lo creó.  Hola runbook necesitará toodefine **$WebhookData** como un parámetro para el mismo tooaccess Hola propiedades de alerta de Hola.  Hello datos de alertas están disponibles en formato de json en una propiedad única denominada **SearchResults** en hello **RequestBody** propiedad de **$WebhookData**.  Esto tendrá con propiedades de hello en hello en la tabla siguiente.

| Nodo | Descripción |
|:--- |:--- |
| id |Ruta de acceso y el GUID del programa Hola a buscan. |
| __metadata |Información sobre Hola alerta incluidos Hola el número de registros y el estado de los resultados de la búsqueda de Hola. |
| value |Entrada separada para cada registro en los resultados de búsqueda de Hola.  detalles de Hola de entrada de hello coincidirá con propiedades de Hola y valores del registro de hello. |

Por ejemplo, hello runbook siguiente podría extraer registros de hello devueltos por la búsqueda de registros de Hola y asignar propiedades diferentes en función de tipo hello de cada registro.  Tenga en cuenta que runbook Hola se inicia mediante la conversión **RequestBody** de json, por lo que TI puede actuar como un objeto en PowerShell.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Pasos siguientes
- Complete un tutorial para [configurar un webhook](log-analytics-alerts-webhooks.md) con una regla de alerta.  
- Obtenga información acerca de cómo toowrite [runbooks en automatización de Azure](https://azure.microsoft.com/documentation/services/automation) problemas tooremediate identificados por las alertas.
