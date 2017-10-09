---
title: "aaaSaved búsquedas y alertas en soluciones de OMS | Documentos de Microsoft"
description: "Soluciones de OMS incluirá, normalmente búsquedas guardadas en los datos de análisis de registros tooanalyze recopilados por solución Hola.  Se puede definir usuario de alertas toonotify Hola o tomar una acción en problema crítico de respuesta tooa automáticamente.  Este artículo describe cómo toodefine análisis de registros guarda las búsquedas y alertas en una plantilla de ARM por lo que pueden incluirse en soluciones de administración."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Adición de análisis de registros guarda tooOMS búsquedas y alertas de solución de administración (versión preliminar)

> [!NOTE]
> La versión de la documentación para crear soluciones de administración de OMS está actualmente en fase preliminar. Cualquier esquema que se describe a continuación es toochange de asunto.   


[Soluciones de administración de OMS](operations-management-suite-solutions.md) incluirá, normalmente [búsquedas guardadas](../log-analytics/log-analytics-log-searches.md) de datos de tooanalyze de análisis de registros recopilados por solución Hola.  También pueden definir [alertas](../log-analytics/log-analytics-alerts.md) toonotify Hola usuario o tomar una acción en problema crítico de respuesta tooa automáticamente.  Este artículo describe cómo toodefine análisis de registros guarda las búsquedas y alertas en un [plantilla de administración de recursos](../resource-manager-template-walkthrough.md) por lo que pueden incluirse en [soluciones de administración de](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Hello ejemplos en este artículo usan parámetros y variables que están bien soluciones toomanagement necesarias o habituales y se describen en [crear soluciones de administración de Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Requisitos previos
En este artículo se da por supuesto que ya está familiarizado con cómo demasiado[crear una solución de administración](operations-management-suite-solutions-creating.md) y la estructura de Hola de un [plantilla de ARM](../resource-group-authoring-templates.md) y el archivo de solución.


## <a name="log-analytics-workspace"></a>Área de trabajo de Log Analytics
Todos los recursos de Log Analytics están contenidos en un [área de trabajo](../log-analytics/log-analytics-manage-access.md).  Como se describe en [OMS área de trabajo y la cuenta de automatización](operations-management-suite-solutions.md#oms-workspace-and-automation-account) área de trabajo de hello no se incluye en la solución de administración de hello, pero debe existir antes de instala la solución de Hola.  Si no está disponible, se producirá un error en la instalación de la solución de Hola.

Hola de área de trabajo de hello llamo en nombre de Hola de cada recurso de análisis de registros.  Esto se hace en soluciones de hello con hello **área de trabajo** parámetro como en el siguiente ejemplo de un recurso de savedsearch de Hola.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Búsquedas guardadas
Incluir [búsquedas guardadas](../log-analytics/log-analytics-log-searches.md) en un solución tooallow usuarios tooquery los datos recopilados por la solución.  Búsquedas guardadas aparecerá en **favoritos** en el portal de OMS de Hola y **búsquedas guardadas** Hola portal de Azure.  También es necesaria una búsqueda guardada para cada alerta.   

[Búsqueda de análisis de registros guardan](../log-analytics/log-analytics-log-searches.md) recursos tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches` y tener Hola siguiendo la estructura.  Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



En hello en la tabla siguiente se describen cada una de las propiedades de Hola de una búsqueda guardada. 

| Propiedad | Descripción |
|:--- |:--- |
| categoría | categoría de Hello para la búsqueda guardada de Hola.  Cualquier búsquedas guardadas en hello a menudo compartirán la misma solución una única categoría por lo que se agrupen en consola Hola. |
| displayname | Nombre toodisplay para hello búsqueda guardada en el portal de Hola. |
| query | Toorun de consulta. |

> [!NOTE]
> Puede que tenga caracteres de escape de toouse en la consulta de hello si incluye caracteres que pudieron interpretarse como JSON.  Por ejemplo, si la consulta era **OperationName:"Microsoft.Compute/virtualMachines/write tipo: AzureActivity"**, deben escribirse en el archivo de solución de hello como **OperationName tipo: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Alertas
Las reglas de alerta que ejecutan una búsqueda guardada a intervalos regulares crean [alertas de Log Analytics](../log-analytics/log-analytics-alerts.md).  Si los resultados de Hola de consulta de hello coinciden con los criterios especificados, se crea un registro de alerta y se ejecutan una o varias acciones.  

Reglas de alerta en una solución de administración se componen de hello después de tres recursos diferentes.

- **Búsqueda guardada.**  Define la búsqueda de registros de Hola que se va a ejecutar.  Varias reglas de alerta pueden compartir una única búsqueda guardada.
- **Programación.**  Define la frecuencia con hello búsqueda de registros se va a ejecutar.  Cada regla de alerta tendrá una única programación.
- **Acción de alerta.**  Cada regla de alerta tendrá un recurso de acción con un tipo de **alerta** que define los detalles de Hola de alerta de hello como criterios de Hola durante un registro de alerta se creará y Hola gravedad de la alerta.  recursos de la acción de Hello, opcionalmente, definirá una respuesta de correo electrónico y el runbook.
- **Acción de webhook (opcional).**  Si la regla de alerta de hello llamará un webhook, entonces requiere un recurso de otra acción con un tipo de **Webhook**.    

Los recursos de búsquedas guardadas se han descrito anteriormente.  Hello otros recursos se describen a continuación.


### <a name="schedule-resource"></a>Recurso de programación

Una búsqueda guardada puede tener una o más programaciones y cada programación representa una regla de alerta independiente. Hello programación definen con qué frecuencia hello búsqueda se ejecuta y Hola intervalo de tiempo sobre qué Hola se recuperan los datos.  Recursos de programación tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` y tener Hola siguiendo la estructura. Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



propiedades de Hola para programar los recursos se describen en hello en la tabla siguiente.

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| enabled       | Sí | Especifica si la alerta de hello está habilitada cuando se crea. |
| interval      | Sí | ¿Con qué frecuencia hello consulta se ejecuta en minutos. |
| queryTimeSpan | Sí | Período de tiempo en minutos en relación con los resultados de tooevaluate. |

recursos de programación de Hello deben depender de hello búsqueda guardada para que se cree antes de programación de Hola.


### <a name="actions"></a>Acciones
Hay dos tipos de recurso de acción especificado por hello **tipo** propiedad.  Una programación requiere uno **alerta** acción que define los detalles de Hola de regla de alerta de Hola y las acciones que se realizan cuando se crea una alerta.  También puede incluir un **Webhook** acción si debe llamarse a un webhook de alerta de Hola.  

Los recursos de acción tienen un tipo de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Acciones de alerta

Cada programación tendrá una acción **Alert**.  Esto define los detalles de Hola de alerta de hello y, opcionalmente, las acciones de notificación y la corrección.  Una notificación envía un correo electrónico tooone o más direcciones.  Una solución, inicia un runbook problema de automatización de Azure tooattempt tooremediate Hola detectado.

Acciones de alerta tienen Hola siguiendo la estructura.  Esto incluye las variables y parámetros comunes para que pueda copiar y pegue este fragmento de código en el archivo de solución y cambiar los nombres de parámetro de Hola. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

propiedades de Hola de recursos de la acción de alerta se describen en hello las tablas siguientes.

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| Tipo | Sí | Tipo de acción de Hola.  Será **Alert** para las acciones de alerta. |
| Nombre | Sí | Nombre para mostrar de alerta de Hola.  Este es el nombre de Hola que se muestra en la consola de hello para la regla de alerta de Hola. |
| Descripción | No | Descripción opcional de alerta de Hola. |
| Severity | Sí | Gravedad de registro y alerta Hola Hola siguientes valores:<br><br> **Critical)** (Crítico)<br>**Warning (ADVERTENCIA)**<br>**Informational** (Informativo) |


##### <a name="threshold"></a>Umbral
Esta sección es obligatoria.  Define propiedades de hello para el umbral de alerta de Hola.

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| Operador | Sí | Operador para la comparación de Hola de hello siguientes valores:<br><br>**gt = mayor que<br>lt = menor que** |
| Valor | Sí | resultados de Hello valor toocompare Hola. |


##### <a name="metricstrigger"></a>MetricsTrigger
Esta sección es opcional.  Inclúyala para una alerta de unidades métricas.

> [!NOTE]
> Las alertas de unidades métricas están actualmente en versión preliminar pública. 

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| TriggerCondition | Sí | Especifica si el umbral de hello es número total de infracciones o infracciones consecutivas de hello después de valores:<br><br>**Total<br>Consecutive** (Total, Consecutivos) |
| Operador | Sí | Operador para la comparación de Hola de hello siguientes valores:<br><br>**gt = mayor que<br>lt = menor que** |
| Valor | Sí | Número de hello horas Hola criterios debe ser alerta de hello tootrigger cumpla. |

##### <a name="throttling"></a>Limitaciones
Esta sección es opcional.  Incluya esta sección si desea que las alertas de toosuppress de hello misma regla para una cantidad de tiempo después de crea una alerta.

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| DurationInMinutes | Sí, si hay una limitación de elementos incluida | Número de alertas de toosuppress de minutos después de que uno de Hola se crea la misma regla de alerta. |

##### <a name="emailnotification"></a>EmailNotification
 Esta sección es opcional incluir si desea Hola tooone de correo electrónico de alerta toosend o más destinatarios.

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| Recipients | Sí | Una lista delimitada por comas de correo electrónico direcciones toosend notificación cuando se crea una alerta como en el siguiente ejemplo de Hola.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Asunto | Sí | Línea de asunto de correo electrónico de Hola. |
| Datos adjuntos | No | Los datos adjuntos no son compatibles actualmente.  Si este elemento está incluido, debe ser **None** (Ninguno). |


##### <a name="remediation"></a>Corrección
Esta sección es opcional incluirlo si desea que un toostart de runbook de alerta de toohello de respuesta. |

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| RunbookName | Sí | Nombre de hello runbook toostart. |
| WebhookUri | Sí | URI del webhook Hola Hola runbook. |
| Expiry | No | Fecha y hora en que Hola corrección expira. |

#### <a name="webhook-actions"></a>Acciones de webhook

Acciones de Webhook iniciar un proceso mediante una llamada a una dirección URL y, opcionalmente, proporcionar un toobe de carga que envía. Únicamente son acciones similares de tooRemediation salvo que están concebidos para webhooks que puede invocar procesos distintos de runbooks de automatización de Azure. También proporcionan opción adicional de Hola de proporcionar un proceso de carga toobe entregado toohello remoto.

Si la alerta llamará un webhook, será necesario un recurso de acción con un tipo de **Webhook** en suma toohello **alerta** recursos de la acción.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

propiedades de Hola de recursos de la acción de Webhook se describen en hello las tablas siguientes.

| Nombre del elemento | Obligatorio | Descripción |
|:--|:--|:--|
| type | Sí | Tipo de acción de Hola.  Será **Webhook** para las acciones de webhook. |
| name | Sí | Nombre para mostrar para la acción de Hola.  Esto no se muestra en la consola de Hola. |
| wehookUri | Sí | URI de hello webhook. |
| customPayload | No | Carga personalizada toobe enviado toohello webhook. formato de Hello dependerá de qué webhook Hola está esperando. |




## <a name="sample"></a>Muestra

Aquí te mostramos un ejemplo de una solución que incluya incluye Hola recursos siguientes:

- Búsqueda guardada
- Schedule
- Acción de alerta
- Acción de webhook

usos de ejemplo de Hola [parámetros de la solución estándar](operations-management-suite-solutions-solution-file.md#parameters) variables que normalmente se utilizarían en una solución como opone toohardcoding valores en las definiciones de recursos de Hola.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Hola siguiente parámetro archivo proporciona valores de ejemplos para esta solución.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Pasos siguientes
* [Agregar vistas](operations-management-suite-solutions-resources-views.md) tooyour solución de administración.
* [Agregar los runbooks de automatización y otros recursos](operations-management-suite-solutions-resources-automation.md) tooyour solución de administración.

