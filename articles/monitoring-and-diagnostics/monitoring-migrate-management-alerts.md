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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="86462-104">Migrar alertas de alertas de registro de tooActivity de eventos de administración de Azure</span><span class="sxs-lookup"><span data-stu-id="86462-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="86462-105">Las Alertas de eventos de administración se desactivarán a partir del 1 de octubre.</span><span class="sxs-lookup"><span data-stu-id="86462-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="86462-106">Utilice las directrices de hello debajo toounderstand si tiene estas alertas y migrarlos si es así.</span><span class="sxs-lookup"><span data-stu-id="86462-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="86462-107">Lo que está cambiando</span><span class="sxs-lookup"><span data-stu-id="86462-107">What is changing</span></span>

<span data-ttu-id="86462-108">Monitor de Azure (anteriormente Azure Insights) que ofrece una capacidad toocreate una alerta que se desencadena en los eventos de administración y direcciones de correo electrónico o dirección URL de la webhook del tooa las notificaciones generadas.</span><span class="sxs-lookup"><span data-stu-id="86462-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="86462-109">Es posible que haya creado una de estas alertas de cualquiera de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="86462-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="86462-110">Hola portal de Azure para ciertos tipos de recursos, en supervisión -> -> Agregar alerta, donde "Alerta de" se establece demasiado alertas "Eventos"</span><span class="sxs-lookup"><span data-stu-id="86462-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="86462-111">Mediante el cmdlet de PowerShell Add-AzureRmLogAlertRule ejecución Hola</span><span class="sxs-lookup"><span data-stu-id="86462-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="86462-112">Directamente utilizando [Hola API de REST de alerta](http://docs.microsoft.com/rest/api/monitor/alertrules) con odata.type = "ManagementEventRuleCondition" y dataSource.odata.type = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="86462-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="86462-113">Hello siguiente script de PowerShell devuelve una lista de todas las alertas de eventos de administración que tiene en su suscripción, así como las condiciones de Hola que se establecen en cada alerta.</span><span class="sxs-lookup"><span data-stu-id="86462-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="86462-114">Si no tiene alertas de eventos de administración, el cmdlet de PowerShell de hello anterior dará como resultado una serie de mensajes de advertencia como este:</span><span class="sxs-lookup"><span data-stu-id="86462-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="86462-115">Estos mensajes de advertencia pueden ignorarse.</span><span class="sxs-lookup"><span data-stu-id="86462-115">These warning messages can be ignored.</span></span> <span data-ttu-id="86462-116">Si tiene alertas de eventos de administración, la salida de hello de este cmdlet de PowerShell tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="86462-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="86462-117">Cada alerta está separado por una línea discontinua e incluye el Id. de recurso de Hola de alerta de Hola y regla concreta de Hola que se está supervisando.</span><span class="sxs-lookup"><span data-stu-id="86462-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="86462-118">Esta funcionalidad se ha pasado demasiado[alertas de registro de actividad de Azure Monitor](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="86462-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="86462-119">Estas nuevas alertas permiten tooset una condición en los eventos de registro de actividad y reciban una notificación cuando un nuevo evento cumple la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="86462-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="86462-120">También ofrecen varias mejoras sobre las alertas de eventos de administración:</span><span class="sxs-lookup"><span data-stu-id="86462-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="86462-121">Puede volver a usar el grupo de destinatarios de notificación ("acciones") a través de muchas alertas mediante [grupos de acciones](monitoring-action-groups.md), reduciendo la complejidad de hello del cambio de quién debe recibir una alerta.</span><span class="sxs-lookup"><span data-stu-id="86462-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="86462-122">Puede recibir una notificación directamente en su teléfono mediante SMS con Grupos de acciones.</span><span class="sxs-lookup"><span data-stu-id="86462-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="86462-123">Puede [Crear alertas del registro de actividad con plantillas de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="86462-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="86462-124">Puede crear condiciones con mayor toomeet flexibilidad y la complejidad de sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="86462-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="86462-125">Las notificaciones se entregan más rápidamente.</span><span class="sxs-lookup"><span data-stu-id="86462-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="86462-126">Cómo toomigrate</span><span class="sxs-lookup"><span data-stu-id="86462-126">How toomigrate</span></span>
 
<span data-ttu-id="86462-127">toocreate una nueva alerta de registro de actividad, puede:</span><span class="sxs-lookup"><span data-stu-id="86462-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="86462-128">Siga [nuestra guía sobre cómo toocreate una alerta en Hola portal de Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="86462-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="86462-129">Obtenga información acerca de cómo demasiado[crear una alerta mediante una plantilla de administrador de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="86462-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="86462-130">Alertas de eventos de administración que haya creado previamente no estará automáticamente migrado tooActivity registro de alertas.</span><span class="sxs-lookup"><span data-stu-id="86462-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="86462-131">Necesita hello toouse anterior a alertas de Hola de toolist de secuencia de comandos de PowerShell en eventos de administración que está configurando y manualmente volver a crearlos como alertas de registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="86462-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="86462-132">Esto debe hacerse antes del 1 de octubre, después del cual las alertas de eventos de administración ya no estará visibles en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="86462-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="86462-133">Otros tipos de alertas de Azure, incluidas las alertas de métricas de Azure Monitor, las alertas de Application Insights y las alertas de Log Analytics no se ven afectadas por este cambio.</span><span class="sxs-lookup"><span data-stu-id="86462-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="86462-134">Si tiene alguna pregunta, publique en comentarios de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="86462-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="86462-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86462-135">Next steps</span></span>

* <span data-ttu-id="86462-136">Más información sobre el [registro de actividad](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="86462-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="86462-137">Configuración de [alertas del registro de actividad a través de Azure Portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="86462-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="86462-138">Configuración de [alertas del registro de actividad a través de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="86462-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="86462-139">Hola de revisión [esquema de webhook alerta de registro de actividad](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="86462-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="86462-140">Más información sobre las [notificaciones del servicio](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="86462-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="86462-141">Más información sobre los [grupos de acciones](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="86462-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
