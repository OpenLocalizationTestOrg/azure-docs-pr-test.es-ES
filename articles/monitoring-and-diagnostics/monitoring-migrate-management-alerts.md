---
title: "aaaMigrate las alertas de Azure en tooActivity alertas de registro de eventos de administración | Documentos de Microsoft"
description: "Las Alertas de eventos de administración se retirarán el 1 de octubre. Preparar la migración de las alertas existentes."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Migrar alertas de alertas de registro de tooActivity de eventos de administración de Azure


> [!WARNING]
> Las Alertas de eventos de administración se desactivarán a partir del 1 de octubre. Utilice las directrices de hello debajo toounderstand si tiene estas alertas y migrarlos si es así.
>
> 

## <a name="what-is-changing"></a>Lo que está cambiando

Monitor de Azure (anteriormente Azure Insights) que ofrece una capacidad toocreate una alerta que se desencadena en los eventos de administración y direcciones de correo electrónico o dirección URL de la webhook del tooa las notificaciones generadas. Es posible que haya creado una de estas alertas de cualquiera de las siguientes maneras:
* Hola portal de Azure para ciertos tipos de recursos, en supervisión -> -> Agregar alerta, donde "Alerta de" se establece demasiado alertas "Eventos"
* Mediante el cmdlet de PowerShell Add-AzureRmLogAlertRule ejecución Hola
* Directamente utilizando [Hola API de REST de alerta](http://docs.microsoft.com/rest/api/monitor/alertrules) con odata.type = "ManagementEventRuleCondition" y dataSource.odata.type = "RuleManagementEventDataSource"
 
Hello siguiente script de PowerShell devuelve una lista de todas las alertas de eventos de administración que tiene en su suscripción, así como las condiciones de Hola que se establecen en cada alerta.

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

Si no tiene alertas de eventos de administración, el cmdlet de PowerShell de hello anterior dará como resultado una serie de mensajes de advertencia como este:

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Estos mensajes de advertencia pueden ignorarse. Si tiene alertas de eventos de administración, la salida de hello de este cmdlet de PowerShell tendrá un aspecto similar al siguiente:

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

Cada alerta está separado por una línea discontinua e incluye el Id. de recurso de Hola de alerta de Hola y regla concreta de Hola que se está supervisando.

Esta funcionalidad se ha pasado demasiado[alertas de registro de actividad de Azure Monitor](monitoring-activity-log-alerts.md). Estas nuevas alertas permiten tooset una condición en los eventos de registro de actividad y reciban una notificación cuando un nuevo evento cumple la condición de Hola. También ofrecen varias mejoras sobre las alertas de eventos de administración:
* Puede volver a usar el grupo de destinatarios de notificación ("acciones") a través de muchas alertas mediante [grupos de acciones](monitoring-action-groups.md), reduciendo la complejidad de hello del cambio de quién debe recibir una alerta.
* Puede recibir una notificación directamente en su teléfono mediante SMS con Grupos de acciones.
* Puede [Crear alertas del registro de actividad con plantillas de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* Puede crear condiciones con mayor toomeet flexibilidad y la complejidad de sus necesidades específicas.
* Las notificaciones se entregan más rápidamente.
 
## <a name="how-toomigrate"></a>Cómo toomigrate
 
toocreate una nueva alerta de registro de actividad, puede:
* Siga [nuestra guía sobre cómo toocreate una alerta en Hola portal de Azure](monitoring-activity-log-alerts.md)
* Obtenga información acerca de cómo demasiado[crear una alerta mediante una plantilla de administrador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Alertas de eventos de administración que haya creado previamente no estará automáticamente migrado tooActivity registro de alertas. Necesita hello toouse anterior a alertas de Hola de toolist de secuencia de comandos de PowerShell en eventos de administración que está configurando y manualmente volver a crearlos como alertas de registro de actividad. Esto debe hacerse antes del 1 de octubre, después del cual las alertas de eventos de administración ya no estará visibles en la suscripción de Azure. Otros tipos de alertas de Azure, incluidas las alertas de métricas de Azure Monitor, las alertas de Application Insights y las alertas de Log Analytics no se ven afectadas por este cambio. Si tiene alguna pregunta, publique en comentarios de Hola a continuación.


## <a name="next-steps"></a>Pasos siguientes

* Más información sobre el [registro de actividad](monitoring-overview-activity-logs.md)
* Configuración de [alertas del registro de actividad a través de Azure Portal](monitoring-activity-log-alerts.md)
* Configuración de [alertas del registro de actividad a través de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Hola de revisión [esquema de webhook alerta de registro de actividad](monitoring-activity-log-alerts-webhook.md)
* Más información sobre las [notificaciones del servicio](monitoring-service-notifications.md)
* Más información sobre los [grupos de acciones](monitoring-action-groups.md)
