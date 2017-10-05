---
title: "Ejemplos de inicio rápido de PowerShell de Azure Monitor | Microsoft Docs"
description: "Use PowerShell para acceder a las características de Azure Monitor, como el escalado automático, alertas, webhooks y buscar registros de actividad."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="4f860-104">Ejemplos de inicio rápido de PowerShell de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4f860-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="4f860-105">En este artículo se muestran comandos de PowerShell de ejemplo para ayudarle a acceder a las características de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4f860-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="4f860-106">Azure Monitor permite escalar automáticamente Cloud Services, Virtual Machines y Web Apps para enviar notificaciones de alerta o llamar a direcciones URL web en función de los valores de datos de telemetría configurados.</span><span class="sxs-lookup"><span data-stu-id="4f860-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="4f860-107">Azure Monitor es el nuevo nombre de lo que se conocía como "Azure Insights" hasta el 25 de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="4f860-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="4f860-108">Sin embargo, los espacios de nombres y, por tanto, los siguientes comandos, aún contienen el término "insights".</span><span class="sxs-lookup"><span data-stu-id="4f860-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="4f860-109">Configurar PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f860-109">Set up PowerShell</span></span>
<span data-ttu-id="4f860-110">Si no lo ha hecho ya, configure PowerShell para que se ejecute en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4f860-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="4f860-111">Para más información, consulte el artículo de [instalación y configuración de PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4f860-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="4f860-112">Ejemplos de este artículo</span><span class="sxs-lookup"><span data-stu-id="4f860-112">Examples in this article</span></span>
<span data-ttu-id="4f860-113">Los ejemplos de este artículo muestran cómo puede usar cmdlets de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4f860-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="4f860-114">También puede consultar toda la lista de cmdlets de PowerShell de Azure Monitor en [Azure Monitor Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx) (Cmdlets de Azure Monitor).</span><span class="sxs-lookup"><span data-stu-id="4f860-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="4f860-115">Inicio de sesión y uso de suscripciones</span><span class="sxs-lookup"><span data-stu-id="4f860-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="4f860-116">Primero, inicie sesión en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f860-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="4f860-117">Para ello, es obligatorio iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="4f860-117">This requires you to sign in.</span></span> <span data-ttu-id="4f860-118">Una vez hecho, se muestran el id. predeterminado de la suscripción, el id. de inquilino y la cuenta.</span><span class="sxs-lookup"><span data-stu-id="4f860-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="4f860-119">Todos los cmdlets de Azure funcionan en el contexto de la suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4f860-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="4f860-120">Para ver la lista de suscripciones a las que tiene acceso, use el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="4f860-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="4f860-121">Para cambiar el contexto de trabajo a una suscripción diferente, utilice el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="4f860-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="4f860-122">Recuperación del registro de actividades para una suscripción</span><span class="sxs-lookup"><span data-stu-id="4f860-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="4f860-123">Utilice el cmdlet `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="4f860-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="4f860-124">A continuación se muestran algunos ejemplos comunes.</span><span class="sxs-lookup"><span data-stu-id="4f860-124">The following are some common examples.</span></span>

<span data-ttu-id="4f860-125">Obtención de entradas de registro desde esta fecha y hora hasta la actual:</span><span class="sxs-lookup"><span data-stu-id="4f860-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="4f860-126">Obtención de entradas de registro entre un intervalo de fecha y hora:</span><span class="sxs-lookup"><span data-stu-id="4f860-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="4f860-127">Obtención de entradas de registro de un grupo de recursos específico:</span><span class="sxs-lookup"><span data-stu-id="4f860-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="4f860-128">Obtención de entradas de registro de un proveedor de recursos específico entre un intervalo de fecha y hora:</span><span class="sxs-lookup"><span data-stu-id="4f860-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="4f860-129">Obtener todas las entradas de registro con un llamador concreto:</span><span class="sxs-lookup"><span data-stu-id="4f860-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="4f860-130">El comando siguiente recupera los últimos 1000 eventos desde el registro de actividades:</span><span class="sxs-lookup"><span data-stu-id="4f860-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="4f860-131">`Get-AzureRmLog` es compatible con muchos otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="4f860-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="4f860-132">Consulte la referencia `Get-AzureRmLog` para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4f860-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="4f860-133">`Get-AzureRmLog` solo proporciona 15 días de historial.</span><span class="sxs-lookup"><span data-stu-id="4f860-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="4f860-134">El parámetro **-MaxEvents** permite consultar los últimos eventos N más allá de 15 días.</span><span class="sxs-lookup"><span data-stu-id="4f860-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="4f860-135">Para acceder a eventos de hace más de 15 días, use el SDK o la API de REST (ejemplo de C# usando el SDK).</span><span class="sxs-lookup"><span data-stu-id="4f860-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="4f860-136">Si no incluye **StartTime**, el valor predeterminado será **EndTime** menos una hora.</span><span class="sxs-lookup"><span data-stu-id="4f860-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="4f860-137">Si no incluye **EndTime**, el valor predeterminado será la hora actual.</span><span class="sxs-lookup"><span data-stu-id="4f860-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="4f860-138">Todas las horas se muestran en UTC.</span><span class="sxs-lookup"><span data-stu-id="4f860-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="4f860-139">Recuperación del historial de alertas</span><span class="sxs-lookup"><span data-stu-id="4f860-139">Retrieve alerts history</span></span>
<span data-ttu-id="4f860-140">Para ver todos los eventos de alerta, puede consultar los registros de Azure Resource Manager con los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="4f860-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="4f860-141">Para ver el historial de una regla de alerta específica, puede utilizar el cmdlet `Get-AzureRmAlertHistory`, con lo que se transmitirá el id. de recurso de la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="4f860-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="4f860-142">El cmdlet `Get-AzureRmAlertHistory` admite varios parámetros.</span><span class="sxs-lookup"><span data-stu-id="4f860-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="4f860-143">Puede obtener más información en [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f860-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="4f860-144">Recuperación de información sobre reglas de alerta</span><span class="sxs-lookup"><span data-stu-id="4f860-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="4f860-145">Todos los comandos siguientes se realizan en un grupo de recursos denominado "montest".</span><span class="sxs-lookup"><span data-stu-id="4f860-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="4f860-146">Consulta de todas las propiedades de la regla de alerta:</span><span class="sxs-lookup"><span data-stu-id="4f860-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="4f860-147">Recuperación de todas las alertas de un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="4f860-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="4f860-148">Recuperación de todas las reglas de alerta de un recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="4f860-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="4f860-149">Por ejemplo, todas las reglas de alerta se establecen en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4f860-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="4f860-150">`Get-AzureRmAlertRule` es compatible con otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="4f860-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="4f860-151">Consulte [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4f860-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="4f860-152">Creación de alertas de métrica</span><span class="sxs-lookup"><span data-stu-id="4f860-152">Create metric alerts</span></span>
<span data-ttu-id="4f860-153">Puede usar el cmdlet `Add-AlertRule` para crear, actualizar o deshabilitar una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="4f860-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="4f860-154">Puede crear propiedades de correo electrónico y webhook mediante `New-AzureRmAlertRuleEmail` y `New-AzureRmAlertRuleWebhook` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="4f860-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="4f860-155">En el cmdlet Alert rule, asígnelos como acciones a la propiedad **Actions** de la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="4f860-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="4f860-156">En la tabla siguiente se describen los parámetros y valores utilizados para crear una alerta con una métrica.</span><span class="sxs-lookup"><span data-stu-id="4f860-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="4f860-157">Parámetro</span><span class="sxs-lookup"><span data-stu-id="4f860-157">parameter</span></span> | <span data-ttu-id="4f860-158">value</span><span class="sxs-lookup"><span data-stu-id="4f860-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="4f860-159">Nombre</span><span class="sxs-lookup"><span data-stu-id="4f860-159">Name</span></span> |<span data-ttu-id="4f860-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="4f860-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="4f860-161">Ubicación (Location) de esta regla de alerta</span><span class="sxs-lookup"><span data-stu-id="4f860-161">Location of this alert rule</span></span> |<span data-ttu-id="4f860-162">Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="4f860-162">East US</span></span> |
| <span data-ttu-id="4f860-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4f860-163">ResourceGroup</span></span> |<span data-ttu-id="4f860-164">montest</span><span class="sxs-lookup"><span data-stu-id="4f860-164">montest</span></span> |
| <span data-ttu-id="4f860-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="4f860-165">TargetResourceId</span></span> |<span data-ttu-id="4f860-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="4f860-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="4f860-167">Nombre de la métrica (MetricName) de la alerta que se crea</span><span class="sxs-lookup"><span data-stu-id="4f860-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="4f860-168">\PhysicalDisk (_Total) \Disk escrituras por segundo. Consulte la `Get-MetricDefinitions` acerca de cómo recuperar los nombres exactos de métrica del cmdlet</span><span class="sxs-lookup"><span data-stu-id="4f860-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="4f860-169">operator</span><span class="sxs-lookup"><span data-stu-id="4f860-169">operator</span></span> |<span data-ttu-id="4f860-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="4f860-170">GreaterThan</span></span> |
| <span data-ttu-id="4f860-171">Valor de umbral (número por segundo para esta métrica)</span><span class="sxs-lookup"><span data-stu-id="4f860-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="4f860-172">1</span><span class="sxs-lookup"><span data-stu-id="4f860-172">1</span></span> |
| <span data-ttu-id="4f860-173">WindowSize (formato hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="4f860-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="4f860-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="4f860-174">00:05:00</span></span> |
| <span data-ttu-id="4f860-175">aggregator (estadística de la métrica que, en este caso, usa el recuento medio)</span><span class="sxs-lookup"><span data-stu-id="4f860-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="4f860-176">Media</span><span class="sxs-lookup"><span data-stu-id="4f860-176">Average</span></span> |
| <span data-ttu-id="4f860-177">mensajes de correo electrónico personalizados (matriz de cadenas)</span><span class="sxs-lookup"><span data-stu-id="4f860-177">custom emails (string array)</span></span> |<span data-ttu-id="4f860-178">"foo@example.com","bar@example.com"</span><span class="sxs-lookup"><span data-stu-id="4f860-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="4f860-179">enviar correo electrónico a los propietarios, colaboradores y lectores</span><span class="sxs-lookup"><span data-stu-id="4f860-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="4f860-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="4f860-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="4f860-181">Creación de una acción de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="4f860-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="4f860-182">Crear una acción de Webhook</span><span class="sxs-lookup"><span data-stu-id="4f860-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="4f860-183">Creación de la regla de alerta de la métrica CPU% en una máquina virtual clásica</span><span class="sxs-lookup"><span data-stu-id="4f860-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="4f860-184">Recuperación de la regla de alerta</span><span class="sxs-lookup"><span data-stu-id="4f860-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="4f860-185">El cmdlet Add alert también actualiza la regla si ya existe una para las propiedades determinadas.</span><span class="sxs-lookup"><span data-stu-id="4f860-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="4f860-186">Para deshabilitar una regla de alerta, incluya el parámetro **-DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="4f860-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="4f860-187">Obtención de una lista de métricas disponibles para las alertas</span><span class="sxs-lookup"><span data-stu-id="4f860-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="4f860-188">Puede usar el cmdlet `Get-AzureRmMetricDefinition` para ver la lista de todas las métricas de un recurso específico.</span><span class="sxs-lookup"><span data-stu-id="4f860-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="4f860-189">En el ejemplo siguiente se genera una tabla con el nombre y la unidad de la métrica.</span><span class="sxs-lookup"><span data-stu-id="4f860-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="4f860-190">Hay disponible una lista completa de opciones para `Get-AzureRmMetricDefinition` en [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f860-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="4f860-191">Creación y administración de la configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="4f860-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="4f860-192">Los recursos, como las aplicaciones web, las máquinas virtuales, los servicios en la nube o los conjuntos de escalado de máquinas virtuales, solo pueden tener una configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="4f860-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="4f860-193">Sin embargo, cada configuración de escalado automático puede tener varios perfiles.</span><span class="sxs-lookup"><span data-stu-id="4f860-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="4f860-194">Por ejemplo, uno para un perfil de escalado basado en el rendimiento y otro para uno basado en la programación.</span><span class="sxs-lookup"><span data-stu-id="4f860-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="4f860-195">Cada perfil puede tener varias reglas configuradas.</span><span class="sxs-lookup"><span data-stu-id="4f860-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="4f860-196">Para obtener más información sobre el escalado automático, consulte [Escalado automático de una aplicación](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4f860-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="4f860-197">Estos son los pasos que seguirá:</span><span class="sxs-lookup"><span data-stu-id="4f860-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="4f860-198">Cree reglas.</span><span class="sxs-lookup"><span data-stu-id="4f860-198">Create rule(s).</span></span>
2. <span data-ttu-id="4f860-199">Cree perfiles que asignen las reglas que ha creado anteriormente a los perfiles.</span><span class="sxs-lookup"><span data-stu-id="4f860-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="4f860-200">Opcional: cree notificaciones de escalado automático configurando las propiedades de Webhook y correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="4f860-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="4f860-201">Cree una configuración de escalado automático con un nombre en el recurso de destino mediante la asignación de los perfiles y las notificaciones que creó en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="4f860-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="4f860-202">En los ejemplos siguientes se muestra cómo crear una configuración de escalado automático para un conjunto de escalado de máquinas virtuales de un sistema operativo de Windows mediante la métrica de uso de CPU.</span><span class="sxs-lookup"><span data-stu-id="4f860-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="4f860-203">En primer lugar, cree una regla de escalado horizontal con aumento del recuento de instancias.</span><span class="sxs-lookup"><span data-stu-id="4f860-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="4f860-204">Después, cree una regla de reducción de escalado con una disminución del recuento de instancias.</span><span class="sxs-lookup"><span data-stu-id="4f860-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="4f860-205">Después, cree un perfil para las reglas.</span><span class="sxs-lookup"><span data-stu-id="4f860-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="4f860-206">Cree una propiedad de Webhook.</span><span class="sxs-lookup"><span data-stu-id="4f860-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="4f860-207">Cree la propiedad de notificación para la configuración de escalado automático, incluidas las de correo electrónico y Webhook que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4f860-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="4f860-208">Finalmente, cree la configuración de escalado automático para agregar el perfil que creó antes.</span><span class="sxs-lookup"><span data-stu-id="4f860-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="4f860-209">Para obtener más información sobre cómo administrar la configuración de escalado automático, consulte [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f860-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="4f860-210">Historial de escalado automático</span><span class="sxs-lookup"><span data-stu-id="4f860-210">Autoscale history</span></span>
<span data-ttu-id="4f860-211">En el ejemplo siguiente se muestra cómo puede ver los eventos de alerta y escalado automático recientes.</span><span class="sxs-lookup"><span data-stu-id="4f860-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="4f860-212">Utilice la búsqueda de registros de actividades para ver el historial de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="4f860-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="4f860-213">Puede usar el cmdlet `Get-AzureRmAutoScaleHistory` para recuperar el historial de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="4f860-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="4f860-214">Para obtener más información, consulte [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f860-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="4f860-215">Consulta de los detalles de una configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="4f860-215">View details for an autoscale setting</span></span>
<span data-ttu-id="4f860-216">Puede usar el cmdlet `Get-Autoscalesetting` para recuperar más información sobre la configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="4f860-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="4f860-217">En el ejemplo siguiente se muestra información sobre todas las configuraciones de escalado automático del grupo de recursos "myrg1".</span><span class="sxs-lookup"><span data-stu-id="4f860-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="4f860-218">En el ejemplo siguiente se muestra información sobre todas las configuraciones de escalado automático del grupo de recursos "myrg1" y, en concreto, la configuración de escalado automático con el nombre "MyScaleVMSSSetting".</span><span class="sxs-lookup"><span data-stu-id="4f860-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="4f860-219">Eliminación de una configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="4f860-219">Remove an autoscale setting</span></span>
<span data-ttu-id="4f860-220">Puede usar el cmdlet `Remove-Autoscalesetting` para eliminar una configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="4f860-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="4f860-221">Administración de perfiles de registro para el registro de actividades</span><span class="sxs-lookup"><span data-stu-id="4f860-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="4f860-222">Puede crear un *perfil de registro* y exportar los datos de su registro de actividades a una cuenta de almacenamiento y configurar la retención de datos.</span><span class="sxs-lookup"><span data-stu-id="4f860-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="4f860-223">Si lo desea, también puede transmitir los datos al Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4f860-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="4f860-224">Tenga en cuenta que esta característica se encuentra actualmente en la fase de vista previa y solo puede crear un perfil de registro por suscripción.</span><span class="sxs-lookup"><span data-stu-id="4f860-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="4f860-225">Puede utilizar los siguientes cmdlets con su suscripción actual para crear y administrar perfiles de registro.</span><span class="sxs-lookup"><span data-stu-id="4f860-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="4f860-226">También puede elegir una suscripción específica.</span><span class="sxs-lookup"><span data-stu-id="4f860-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="4f860-227">Aunque PowerShell tiene como valor predeterminado la suscripción actual, puede cambiarla cuando quiera con `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="4f860-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="4f860-228">Puede configurar el registro de actividades para enrutar los datos a cualquier cuenta de almacenamiento o al centro de eventos de dicha suscripción.</span><span class="sxs-lookup"><span data-stu-id="4f860-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="4f860-229">Los datos se escriben como archivos blob en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4f860-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="4f860-230">Obtención de un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="4f860-230">Get a log profile</span></span>
<span data-ttu-id="4f860-231">Para capturar los perfiles de registro existentes, use el cmdlet `Get-AzureRmLogProfile` .</span><span class="sxs-lookup"><span data-stu-id="4f860-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="4f860-232">Adición de un perfil de registro sin retención de datos</span><span class="sxs-lookup"><span data-stu-id="4f860-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="4f860-233">Eliminación de perfil de registro</span><span class="sxs-lookup"><span data-stu-id="4f860-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="4f860-234">Adición de un perfil de registro con retención de datos</span><span class="sxs-lookup"><span data-stu-id="4f860-234">Add a log profile with data retention</span></span>
<span data-ttu-id="4f860-235">Puede especificar la propiedad **-RetentionInDays** con el número de días, como un entero positivo, que se conservarán los datos.</span><span class="sxs-lookup"><span data-stu-id="4f860-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="4f860-236">Adición de un perfil de registro retención y EventHub</span><span class="sxs-lookup"><span data-stu-id="4f860-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="4f860-237">Además de enrutar los datos a la cuenta de almacenamiento, también puede transmitirlos a un Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="4f860-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="4f860-238">Tenga en cuenta que es obligatorio en esta versión de vista previa y configuración de la cuenta de almacenamiento; sin embargo, la configuración del Centro de eventos es opcional.</span><span class="sxs-lookup"><span data-stu-id="4f860-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="4f860-239">Configuración de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4f860-239">Configure diagnostics logs</span></span>
<span data-ttu-id="4f860-240">Muchos servicios de Azure proporcionan otros registros y telemetría que pueden configurarse para guardar los datos en su cuenta de Azure Storage, enviarlos a Event Hubs o enviarlos a un área de trabajo de Log Analytics de OMS.</span><span class="sxs-lookup"><span data-stu-id="4f860-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="4f860-241">Esta operación solo puede realizarse en un nivel de recursos y la cuenta de almacenamiento o el centro de eventos debe encontrarse en la misma región que el recurso de destino donde se ha ajustado la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="4f860-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="4f860-242">Obtención de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4f860-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="4f860-243">Deshabilitación de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4f860-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="4f860-244">Habilitación de la configuración de diagnóstico sin retención</span><span class="sxs-lookup"><span data-stu-id="4f860-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="4f860-245">Habilitación la configuración de diagnóstico con retención</span><span class="sxs-lookup"><span data-stu-id="4f860-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="4f860-246">Habilitación de la configuración de diagnóstico con retención para una categoría de registro específica</span><span class="sxs-lookup"><span data-stu-id="4f860-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="4f860-247">Habilitación de la configuración de diagnóstico para Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4f860-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="4f860-248">Habilitación de la configuración de diagnóstico para OMS</span><span class="sxs-lookup"><span data-stu-id="4f860-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
