---
title: "Migración de las alertas de eventos de administración de Azure a Alertas del registro de actividad | Microsoft Docs"
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
ms.openlocfilehash: 08a457029d3721f5c38dbcd2d2aab7d09a241d8f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-azure-alerts-on-management-events-to-activity-log-alerts"></a><span data-ttu-id="6ff19-104">Migración de las alertas de eventos de administración de Azure a Alertas del registro de actividad</span><span class="sxs-lookup"><span data-stu-id="6ff19-104">Migrate Azure alerts on management events to Activity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="6ff19-105">Las Alertas de eventos de administración se desactivarán a partir del 1 de octubre.</span><span class="sxs-lookup"><span data-stu-id="6ff19-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="6ff19-106">Utilice las instrucciones siguientes para determinar si tiene estas alertas y migrarlas en caso afirmativo.</span><span class="sxs-lookup"><span data-stu-id="6ff19-106">Use the directions below to understand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="6ff19-107">Lo que está cambiando</span><span class="sxs-lookup"><span data-stu-id="6ff19-107">What is changing</span></span>

<span data-ttu-id="6ff19-108">Azure Monitor (anteriormente Azure Insights) ofrecía una funcionalidad para crear una alerta desencadenada por eventos de administración y generar notificaciones a direcciones de correo electrónico o a una dirección URL de webhook.</span><span class="sxs-lookup"><span data-stu-id="6ff19-108">Azure Monitor (formerly Azure Insights) offered a capability to create an alert that triggered off of management events and generated notifications to a webhook URL or email addresses.</span></span> <span data-ttu-id="6ff19-109">Es posible que haya creado una de estas alertas de cualquiera de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="6ff19-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="6ff19-110">En Azure Portal para ciertos tipos de recursos, bajo Supervisión -> Alertas -> Agregar alerta, donde "Alerta de" se ha establecido en "Eventos"</span><span class="sxs-lookup"><span data-stu-id="6ff19-110">In the Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set to “Events”</span></span>
* <span data-ttu-id="6ff19-111">Mediante la ejecución del cmdlet de PowerShell Add-AzureRmLogAlertRule</span><span class="sxs-lookup"><span data-stu-id="6ff19-111">By running the Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="6ff19-112">Utilizando directamente [la API de REST alert](http://docs.microsoft.com/rest/api/monitor/alertrules) con odata.type = "ManagementEventRuleCondition" y dataSource.odata.type = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="6ff19-112">By directly using [the alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="6ff19-113">El siguiente script de PowerShell devuelve una lista de todas las alertas de eventos de administración que tiene en su suscripción, así como las condiciones establecidas en cada alerta.</span><span class="sxs-lookup"><span data-stu-id="6ff19-113">The following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as the conditions set on each alert.</span></span>

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

<span data-ttu-id="6ff19-114">Si no tiene alertas de eventos de administración, el cmdlet de PowerShell anterior dará como resultado una serie de mensajes de advertencia como este:</span><span class="sxs-lookup"><span data-stu-id="6ff19-114">If you have no alerts on management events, the PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: The output of this cmdlet will be flattened, i.e. elimination of the properties field, in a future release to improve the user experience.`

<span data-ttu-id="6ff19-115">Estos mensajes de advertencia pueden ignorarse.</span><span class="sxs-lookup"><span data-stu-id="6ff19-115">These warning messages can be ignored.</span></span> <span data-ttu-id="6ff19-116">Si tiene alertas de eventos de administración, la salida de este cmdlet de PowerShell tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="6ff19-116">If you do have alerts on management events, the output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="6ff19-117">Cada alerta está separada por una línea discontinua y los detalles incluyen el identificador de recurso de la alerta y la regla específica que se está supervisando.</span><span class="sxs-lookup"><span data-stu-id="6ff19-117">Each alert is separated by a dashed line and details include the resource ID of the alert and the specific rule being monitored.</span></span>

<span data-ttu-id="6ff19-118">Esta funcionalidad se ha pasado a [Alertas del registro de actividad de Azure Monitor](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6ff19-118">This functionality has been transitioned to [Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="6ff19-119">Estas nuevas alertas permiten establecer una condición en los eventos del registro de actividad y recibir una notificación cuando un nuevo evento coincide con la condición.</span><span class="sxs-lookup"><span data-stu-id="6ff19-119">These new alerts enable you to set a condition on Activity Log events and receive a notification when a new event matches the condition.</span></span> <span data-ttu-id="6ff19-120">También ofrecen varias mejoras sobre las alertas de eventos de administración:</span><span class="sxs-lookup"><span data-stu-id="6ff19-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="6ff19-121">Puede volver a usar el grupo de destinatarios de notificación ("acciones") en muchas alertas mediante los [Grupos de acciones](monitoring-action-groups.md), lo que reduce la complejidad del cambio de quién debe recibir una alerta.</span><span class="sxs-lookup"><span data-stu-id="6ff19-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing the complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="6ff19-122">Puede recibir una notificación directamente en su teléfono mediante SMS con Grupos de acciones.</span><span class="sxs-lookup"><span data-stu-id="6ff19-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="6ff19-123">Puede [Crear alertas del registro de actividad con plantillas de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="6ff19-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="6ff19-124">Puede crear condiciones con mayor flexibilidad y complejidad para satisfacer sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="6ff19-124">You can create conditions with greater flexibility and complexity to meet your specific needs.</span></span>
* <span data-ttu-id="6ff19-125">Las notificaciones se entregan más rápidamente.</span><span class="sxs-lookup"><span data-stu-id="6ff19-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-to-migrate"></a><span data-ttu-id="6ff19-126">Cómo migrar</span><span class="sxs-lookup"><span data-stu-id="6ff19-126">How to migrate</span></span>
 
<span data-ttu-id="6ff19-127">Para crear una nueva alerta del registro de actividad:</span><span class="sxs-lookup"><span data-stu-id="6ff19-127">To create a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="6ff19-128">Siga [nuestra guía sobre cómo crear una alerta en Azure Portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-128">Follow [our guide on how to create an alert in the Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="6ff19-129">Obtenga información acerca de cómo [crear una alerta mediante una plantilla de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-129">Learn how to [create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="6ff19-130">Las alertas de eventos de administración que haya creado previamente no se migrarán automáticamente a las alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="6ff19-130">Alerts on management events that you have previously created will not be automatically migrated to Activity Log Alerts.</span></span> <span data-ttu-id="6ff19-131">Debe utilizar el script de PowerShell anterior para mostrar las alertas de eventos de administración que tiene configuradas y volver a crearlas manualmente como alertas del registro de actividad.</span><span class="sxs-lookup"><span data-stu-id="6ff19-131">You need to use the preceding PowerShell script to list the alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="6ff19-132">Esto debe hacerse antes del 1 de octubre, después del cual las alertas de eventos de administración ya no estará visibles en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff19-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="6ff19-133">Otros tipos de alertas de Azure, incluidas las alertas de métricas de Azure Monitor, las alertas de Application Insights y las alertas de Log Analytics no se ven afectadas por este cambio.</span><span class="sxs-lookup"><span data-stu-id="6ff19-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="6ff19-134">Si tiene alguna pregunta, indíquela en los comentarios a continuación.</span><span class="sxs-lookup"><span data-stu-id="6ff19-134">If you have any questions, post in the comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6ff19-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ff19-135">Next steps</span></span>

* <span data-ttu-id="6ff19-136">Más información sobre el [registro de actividad](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="6ff19-137">Configuración de [alertas del registro de actividad a través de Azure Portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="6ff19-138">Configuración de [alertas del registro de actividad a través de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="6ff19-139">Revisión del [esquema de webhook de alertas del registro de actividad](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-139">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="6ff19-140">Más información sobre las [notificaciones del servicio](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="6ff19-141">Más información sobre los [grupos de acciones](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="6ff19-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
