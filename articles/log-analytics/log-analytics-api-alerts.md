---
title: "aaaUsing API de REST de alerta de análisis de registros de OMS"
description: "Hola API de REST de alerta de análisis de registros permite toocreate y administrar las alertas en los análisis de registros que forma parte de Operations Management Suite (OMS).  Este artículo proporciona detalles de la API de Hola y varios ejemplos para realizar diferentes operaciones."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Creación y administración de reglas de alerta de Log Analytics con la API de REST
Hola API de REST de alerta de análisis de registros permite toocreate y administrar alertas de Operations Management Suite (OMS).  Este artículo proporciona detalles de la API de Hola y varios ejemplos para realizar diferentes operaciones.

Hola API de REST de búsqueda de análisis de registros es RESTful y son accesibles a través de hello API de REST del Administrador de recursos de Azure. En este documento encontrará ejemplos donde se accede a Hola API desde una línea de comandos de PowerShell con [ARMClient](https://github.com/projectkudu/ARMClient), una herramienta de línea de comandos de código abierto que simplifica la invocación Hola API del Administrador de recursos de Azure. uso de Hola de ARMClient y PowerShell es una de muchas opciones tooaccess Hola API de búsqueda de análisis de registros. Con estas herramientas pueden usar áreas de trabajo de hello API del Administrador de recursos de Azure RESTful toomake llamadas tooOMS y ejecutar comandos de búsqueda dentro de ellos. Hola API darán como resultado tooyou de resultados de búsqueda en formato JSON, permitiéndole toouse resultados de la búsqueda de Hola de muchas formas distintas mediante programación.

## <a name="prerequisites"></a>Requisitos previos
Actualmente, solo se pueden crear alertas con una búsqueda guardada en Log Analytics.  Puede hacer referencia a toohello [API de REST de búsqueda de registros](log-analytics-log-search-api.md) para obtener más información.

## <a name="schedules"></a>Programaciones
Una búsqueda guardada puede tener una o varias programaciones. Hello programación define la frecuencia con hello búsqueda se ejecuta y se identifica el intervalo de tiempo de hello en los criterios que Hola.
Programaciones tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Intervalo |¿Con qué frecuencia hello búsqueda se ejecuta. Se mide en minutos. |
| QueryTimeSpan |intervalo de tiempo de Hello sobre qué Hola se evalúa los criterios. Debe ser igual tooor mayor intervalo. Se mide en minutos. |
| Versión |Hola versión de API que se va a usar.  Actualmente, esto siempre se debe establecer too1. |

Por ejemplo, en una consulta de evento con un valor de Intervalo de 15 minutos y un valor de Timespan de 30 minutos, En este caso, se ejecutaría consulta Hola cada 15 minutos, y se desencadenará una alerta si los criterios de hello sigue tooresolve tootrue durante un período de 30 minutos.

### <a name="retrieving-schedules"></a>Recuperar programaciones
Hola uso obtener método tooretrieve todas las programaciones de una búsqueda guardada.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Hola de uso obtener una programación determinada de una búsqueda guardada de método con un tooretrieve de Id. de programación.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

La siguiente es una respuesta de ejemplo de una programación.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Creación de una programación
Utilice el método de Put de hello con un toocreate de identificador de programación único una nueva programación.  Tenga en cuenta que dos programaciones no se han Hola mismo identificador incluso si están asociados con diferentes búsquedas guardadas.  Cuando se crea una programación en la consola de OMS hello, se crea un GUID para el identificador de programación de Hola.

> [!NOTE]
> nombre de Hola para búsquedas guardadas, las programaciones y acciones creadas con hello API de análisis de registros debe estar en minúsculas.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Edición de una programación
Utilice el método de Put de hello con una programación existente toomodify que la programación de búsqueda de Id. de hello mismo guardado.  cuerpo de saludo de solicitud de hello debe incluir etag Hola de programación de Hola.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Eliminar programaciones
Utilice el método de eliminación de hello con un toodelete de Id. de programación una programación.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Acciones
Una programación puede tener varias acciones. Una acción puede definir uno o más tooperform de procesos, como enviar un correo electrónico o iniciar un runbook, o bien puede definir un umbral que determina si los resultados de saludo de la búsqueda cumplen algunos criterios.  Algunas acciones definirá dos para que se realicen procesos de hello cuando se alcanza el umbral de Hola.

Todas las acciones tienen propiedades de hello en hello en la tabla siguiente.  Los distintos tipos de alertas tienen diferentes propiedades adicionales, descritas aquí.

| Propiedad | Descripción |
|:--- |:--- |
| Tipo |Tipo de acción de Hola.  Actualmente los valores posibles de hello son alerta y Webhook. |
| Nombre |Nombre para mostrar de alerta de Hola. |
| Versión |Hola versión de API que se va a usar.  Actualmente, esto siempre se debe establecer too1. |

### <a name="retrieving-actions"></a>Recuperar acciones
Hola uso obtener método tooretrieve todas las acciones de una programación.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Hola uso obtener método con tooretrieve de Id. de acción de hello una acción concreta para una programación.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Crear o editar acciones
Utilice el método Put de hello con un identificador de acción que es único toohello programación toocreate una nueva acción.  Cuando se crea una acción en la consola de OMS hello, un GUID es para hello Id. de acción.

> [!NOTE]
> nombre de Hola para búsquedas guardadas, las programaciones y acciones creadas con hello API de análisis de registros debe estar en minúsculas.

Utilice el método Put de hello con una Id. de hello mismo guardado buscar toomodify que la programación de acciones existente.  cuerpo de saludo de solicitud de hello debe incluir etag Hola de programación de Hola.

formato de solicitud de Hola para crear una nueva acción varía según el tipo de acción para que estos ejemplos se proporcionan en secciones de hello siguientes.

### <a name="deleting-actions"></a>Eliminar acciones
Utilice el método de eliminación de hello con toodelete de Id. de acción de hello una acción.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Acciones de alerta
Una programación debe tener una acción de alerta única y exclusivamente.  Acciones de alerta tienen una o varias de las secciones de hello en hello en la tabla siguiente.  Cada una de ellas se describe con más detalle abajo.

| Sección | Descripción |
|:--- |:--- |
| Umbral |Criterios cuando se ejecuta la acción de Hola. |
| EmailNotification |Enviar correo electrónico de destinatarios toomultiple. |
| Corrección |Iniciar un runbook en automatización de Azure tooattempt toocorrect había identificado el problema. |

#### <a name="thresholds"></a>Umbrales
Una acción de alerta debe tener un umbral única y exclusivamente.  Cuando los resultados de Hola de una búsqueda guardada coincide con umbral de hello en una acción asociada que la búsqueda, se ejecutan los demás procesos en esa acción.  Una acción también puede contener solo un umbral para que pueda usarse con acciones de otros tipos que no contienen umbrales.

Umbrales tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| operador |Operador de comparación de umbral de Hola. <br> gt = Mayor que <br>  lt = Menor que |
| Valor |Valor de umbral de Hola. |

Por ejemplo, en una consulta de evento con un valor de Intervalo de 15 minutos, un valor de Timespan de 30 minutos y un valor de Threshold mayor que 10, En este caso, se ejecutaría consulta Hola cada 15 minutos, y se desencadenará una alerta si devuelven 10 eventos que se crearon durante un período de 30 minutos.

La siguiente es una respuesta de ejemplo de una acción con un solo umbral.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de umbral para una programación.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Utilice el método de Put de hello con un toomodify de Id. de acción existente una acción de umbral para una programación.  cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Notificación por correo electrónico
Notificaciones de correo electrónico envían correo electrónico tooone o más destinatarios.  Incluyen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Recipients |Lista de direcciones de correo electrónico. |
| Asunto |asunto Hola de correo electrónico de Hola. |
| Datos adjuntos |Actualmente no se admiten datos adjuntos, por lo que siempre aparecerá un valor “None”. |

La siguiente es una respuesta de ejemplo de una acción de notificación de correo con un umbral.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de correo electrónico para una programación.  Hello en el ejemplo siguiente se crea una notificación por correo electrónico con un umbral para que se envía correo de hello cuando los resultados de Hola de hello búsqueda guardada superan el umbral de Hola.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Utilice el método de Put de hello con un toomodify de Id. de acción una acción de correo electrónico existente para una programación.  cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Acciones de corrección
Correcciones de iniciar un runbook en automatización de Azure que intente problema de hello toocorrect identificado por la alerta de Hola.  Debe crear un webhook de runbook de hello utilizado en una acción de corrección y, a continuación, especificar URI Hola Hola WebhookUri propiedad.  Cuando se crea esta acción mediante la consola de OMS de hello, se crea automáticamente un webhook nuevo runbook Hola.

Correcciones incluyen las propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| RunbookName |Nombre de runbook de Hola. Debe coincidir con un runbook publicado en la cuenta de automatización de hello configurado en hello solución de automatización en el área de trabajo OMS. |
| WebhookUri |URI de hello webhook. |
| Expiry |fecha de expiración de Hola y la hora de hello webhook.  Si hello webhook no tiene una expiración, esto puede ser cualquier fecha futura válido. |

La siguiente es una respuesta de ejemplo de una acción de corrección con un umbral.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de corrección para una programación.  Hello en el ejemplo siguiente se crea una solución con un umbral para que hello runbook se inicia cuando los resultados de Hola de hello búsqueda guardada sobrepasan el umbral de Hola.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Utilice el método de Put de hello con un toomodify de Id. de acción existente una acción correctora para una programación.  cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Ejemplo
Aquí te mostramos una toocreate una nueva alerta de correo electrónico de ejemplo completo.  En él, se crea una programación junto con una acción que contiene un umbral y un correo electrónico.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Acciones de webhook
Acciones de Webhook iniciar un proceso mediante una llamada a una dirección URL y, opcionalmente, proporcionar un toobe de carga que envía.  Únicamente son acciones similares de tooRemediation salvo que están concebidos para webhooks que puede invocar procesos distintos de runbooks de automatización de Azure.  También proporcionan opción adicional de Hola de proporcionar un proceso de carga toobe entregado toohello remoto.

Acciones de Webhook no tiene un umbral, pero en su lugar, se deben agregar programación tooa que tiene una acción con un umbral de alerta.  Puede agregar varias acciones de Webhook que todos se ejecutará cuando se cumpla el umbral de Hola.

Acciones de Webhook incluyen las propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| WebhookUri |asunto Hola de correo electrónico de Hola. |
| CustomPayload |Carga personalizada toobe enviado toohello webhook.  formato de Hello dependerá de qué webhook Hola está esperando. |

La siguiente es una respuesta de ejemplo de una acción de webhook y una acción de alerta asociada con un umbral.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Crear o editar una acción de webhook
Utilice el método de Put de hello con un toocreate de Id. de acción única una nueva acción de webhook para una programación.  Hello en el ejemplo siguiente se crea una acción de Webhook y una acción de alerta con un umbral de modo que hello webhook se desencadenará cuando los resultados de Hola de hello búsqueda guardada sobrepasan el umbral de Hola.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Utilice el método de Put de hello con un toomodify de Id. de acción existente una acción de webhook para una programación.  cuerpo de saludo de solicitud de hello debe incluir etag Hola de acción de Hola.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Pasos siguientes
* Hola de uso [búsquedas de registros de API de REST tooperform](log-analytics-log-search-api.md) en análisis de registros.

