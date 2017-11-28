---
title: "ejemplos de inicio rápido de PowerShell de Monitor de aaaAzure. | Microsoft Docs"
description: "Usar PowerShell tooaccess características del Monitor de Azure, como el escalado automático, alertas, webhooks y buscar registros de actividad."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="ac614-104">Ejemplos de inicio rápido de PowerShell de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="ac614-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="ac614-105">Este artículo se demuestra que tome las muestras toohelp de comandos de PowerShell obtener acceso a características del Monitor de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac614-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="ac614-106">Monitor de Azure le permite tooAutoScale servicios en la nube, máquinas virtuales y las aplicaciones Web y toosend notificaciones de alerta o direcciones URL de web de llamada basadas en valores de datos de telemetría configurado.</span><span class="sxs-lookup"><span data-stu-id="ac614-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="ac614-107">Monitor de Azure es Hola nuevo nombre lo que se conoce como "Azure Insights" hasta 25 de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="ac614-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="ac614-108">Sin embargo, hello sigue siendo comandos espacios de nombres de hello y, por tanto, contienen información"Hola".</span><span class="sxs-lookup"><span data-stu-id="ac614-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="ac614-109">Configurar PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac614-109">Set up PowerShell</span></span>
<span data-ttu-id="ac614-110">Si no lo ha hecho ya, configure toorun de PowerShell en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ac614-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="ac614-111">Para obtener más información, consulte [cómo tooInstall y configurar PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac614-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="ac614-112">Ejemplos de este artículo</span><span class="sxs-lookup"><span data-stu-id="ac614-112">Examples in this article</span></span>
<span data-ttu-id="ac614-113">ejemplos de Hello en el artículo Hola muestra cómo puede usar cmdlets de Monitor de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac614-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="ac614-114">También puede revisar la lista completa de Hola de cmdlets de PowerShell de Monitor de Azure en [Cmdlets de Azure Monitor (visión)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac614-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="ac614-115">Inicio de sesión y uso de suscripciones</span><span class="sxs-lookup"><span data-stu-id="ac614-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="ac614-116">En primer lugar, inicie sesión en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac614-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="ac614-117">Para ello, toosign en.</span><span class="sxs-lookup"><span data-stu-id="ac614-117">This requires you toosign in.</span></span> <span data-ttu-id="ac614-118">Una vez hecho, se muestran el id. predeterminado de la suscripción, el id. de inquilino y la cuenta.</span><span class="sxs-lookup"><span data-stu-id="ac614-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="ac614-119">Todos los Hola cmdlets de Azure, trabajar en el contexto de Hola de su suscripción de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ac614-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="ac614-120">lista de hello tooview de suscripciones que tiene acceso, use Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="ac614-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="ac614-121">toochange su trabajo contexto tooa otra suscripción, Hola de uso siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="ac614-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="ac614-122">Recuperación del registro de actividades para una suscripción</span><span class="sxs-lookup"><span data-stu-id="ac614-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="ac614-123">Hola de uso `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac614-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="ac614-124">siguiente Hola es algunos ejemplos comunes.</span><span class="sxs-lookup"><span data-stu-id="ac614-124">hello following are some common examples.</span></span>

<span data-ttu-id="ac614-125">Obtener las entradas del registro de este toopresent de fecha y hora:</span><span class="sxs-lookup"><span data-stu-id="ac614-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="ac614-126">Obtención de entradas de registro entre un intervalo de fecha y hora:</span><span class="sxs-lookup"><span data-stu-id="ac614-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="ac614-127">Obtención de entradas de registro de un grupo de recursos específico:</span><span class="sxs-lookup"><span data-stu-id="ac614-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="ac614-128">Obtención de entradas de registro de un proveedor de recursos específico entre un intervalo de fecha y hora:</span><span class="sxs-lookup"><span data-stu-id="ac614-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="ac614-129">Obtener todas las entradas de registro con un llamador concreto:</span><span class="sxs-lookup"><span data-stu-id="ac614-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="ac614-130">Hola siguiente comando recupera Hola últimos 1000 eventos del registro de actividad de hello:</span><span class="sxs-lookup"><span data-stu-id="ac614-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="ac614-131">`Get-AzureRmLog` es compatible con muchos otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="ac614-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="ac614-132">Vea hello `Get-AzureRmLog` referencia para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ac614-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="ac614-133">`Get-AzureRmLog` solo proporciona 15 días de historial.</span><span class="sxs-lookup"><span data-stu-id="ac614-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="ac614-134">Con hello **MaxEvents -** parámetro permite tooquery Hola últimos N eventos, más allá de 15 días.</span><span class="sxs-lookup"><span data-stu-id="ac614-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="ac614-135">tooaccess eventos anteriores a 15 días, utilice Hola API de REST o SDK (ejemplo de C# con hello SDK).</span><span class="sxs-lookup"><span data-stu-id="ac614-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="ac614-136">Si no incluye **StartTime**, es el valor predeterminado de hello **EndTime** menos una hora.</span><span class="sxs-lookup"><span data-stu-id="ac614-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="ac614-137">Si no incluye **EndTime**, valor predeterminado de hello es la hora actual.</span><span class="sxs-lookup"><span data-stu-id="ac614-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="ac614-138">Todas las horas se muestran en UTC.</span><span class="sxs-lookup"><span data-stu-id="ac614-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="ac614-139">Recuperación del historial de alertas</span><span class="sxs-lookup"><span data-stu-id="ac614-139">Retrieve alerts history</span></span>
<span data-ttu-id="ac614-140">Hola a tooview todos los eventos de alerta, puede consultar los registros de Azure Resource Manager usando hello en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="ac614-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="ac614-141">regla de historial de hello tooview de una alerta específica, puede usar hello `Get-AzureRmAlertHistory` cmdlet, pasando el Id. de recurso de Hola de regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac614-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="ac614-142">Hola `Get-AzureRmAlertHistory` cmdlet admite varios parámetros.</span><span class="sxs-lookup"><span data-stu-id="ac614-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="ac614-143">Puede obtener más información en [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac614-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="ac614-144">Recuperación de información sobre reglas de alerta</span><span class="sxs-lookup"><span data-stu-id="ac614-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="ac614-145">Todos Hola siga los comandos actúan en un grupo de recursos denominado "montest".</span><span class="sxs-lookup"><span data-stu-id="ac614-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="ac614-146">Ver todas las propiedades de Hola de regla de alerta de hello:</span><span class="sxs-lookup"><span data-stu-id="ac614-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="ac614-147">Recuperación de todas las alertas de un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="ac614-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="ac614-148">Recuperación de todas las reglas de alerta de un recurso de destino.</span><span class="sxs-lookup"><span data-stu-id="ac614-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="ac614-149">Por ejemplo, todas las reglas de alerta se establecen en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ac614-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="ac614-150">`Get-AzureRmAlertRule` es compatible con otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="ac614-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="ac614-151">Consulte [Get AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ac614-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="ac614-152">Creación de alertas de métrica</span><span class="sxs-lookup"><span data-stu-id="ac614-152">Create metric alerts</span></span>
<span data-ttu-id="ac614-153">Puede usar hello `Add-AlertRule` toocreate de cmdlet, actualizar o deshabilitar una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="ac614-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="ac614-154">Puede crear propiedades de correo electrónico y webhook mediante `New-AzureRmAlertRuleEmail` y `New-AzureRmAlertRuleWebhook` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ac614-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="ac614-155">En el cmdlet de la regla de alerta de hello, asignar estos como acciones toohello **acciones** propiedad de hello regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="ac614-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="ac614-156">Hello en la tabla siguiente describe los parámetros de Hola y valores usado toocreate una alerta con una métrica.</span><span class="sxs-lookup"><span data-stu-id="ac614-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="ac614-157">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ac614-157">parameter</span></span> | <span data-ttu-id="ac614-158">value</span><span class="sxs-lookup"><span data-stu-id="ac614-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="ac614-159">Nombre</span><span class="sxs-lookup"><span data-stu-id="ac614-159">Name</span></span> |<span data-ttu-id="ac614-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="ac614-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="ac614-161">Ubicación (Location) de esta regla de alerta</span><span class="sxs-lookup"><span data-stu-id="ac614-161">Location of this alert rule</span></span> |<span data-ttu-id="ac614-162">Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="ac614-162">East US</span></span> |
| <span data-ttu-id="ac614-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac614-163">ResourceGroup</span></span> |<span data-ttu-id="ac614-164">montest</span><span class="sxs-lookup"><span data-stu-id="ac614-164">montest</span></span> |
| <span data-ttu-id="ac614-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="ac614-165">TargetResourceId</span></span> |<span data-ttu-id="ac614-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="ac614-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="ac614-167">MetricName de alerta de Hola que se crea</span><span class="sxs-lookup"><span data-stu-id="ac614-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="ac614-168">\PhysicalDisk (_Total) \Disk escrituras por segundo. Vea hello `Get-MetricDefinitions` acerca de cómo tooretrieve Hola nombres de métrica exactos del cmdlet</span><span class="sxs-lookup"><span data-stu-id="ac614-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="ac614-169">operator</span><span class="sxs-lookup"><span data-stu-id="ac614-169">operator</span></span> |<span data-ttu-id="ac614-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="ac614-170">GreaterThan</span></span> |
| <span data-ttu-id="ac614-171">Valor de umbral (número por segundo para esta métrica)</span><span class="sxs-lookup"><span data-stu-id="ac614-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="ac614-172">1</span><span class="sxs-lookup"><span data-stu-id="ac614-172">1</span></span> |
| <span data-ttu-id="ac614-173">WindowSize (formato hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="ac614-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="ac614-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="ac614-174">00:05:00</span></span> |
| <span data-ttu-id="ac614-175">agregador (estadística de métrica de hello, que utiliza el recuento de promedio, en este caso)</span><span class="sxs-lookup"><span data-stu-id="ac614-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="ac614-176">Media</span><span class="sxs-lookup"><span data-stu-id="ac614-176">Average</span></span> |
| <span data-ttu-id="ac614-177">mensajes de correo electrónico personalizados (matriz de cadenas)</span><span class="sxs-lookup"><span data-stu-id="ac614-177">custom emails (string array)</span></span> |<span data-ttu-id="ac614-178">"foo@example.com","bar@example.com"</span><span class="sxs-lookup"><span data-stu-id="ac614-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="ac614-179">enviar correo electrónico tooowners, colaboradores y los lectores</span><span class="sxs-lookup"><span data-stu-id="ac614-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="ac614-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="ac614-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="ac614-181">Creación de una acción de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="ac614-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="ac614-182">Crear una acción de Webhook</span><span class="sxs-lookup"><span data-stu-id="ac614-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="ac614-183">Crear regla de alerta de hello en la métrica de % de CPU de hello en una máquina virtual clásica</span><span class="sxs-lookup"><span data-stu-id="ac614-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="ac614-184">Recuperar la regla de alerta de Hola</span><span class="sxs-lookup"><span data-stu-id="ac614-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="ac614-185">Hola Agregar alerta cmdlet también actualiza la regla de Hola si ya existe una regla de alerta para hello tiene propiedades.</span><span class="sxs-lookup"><span data-stu-id="ac614-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="ac614-186">toodisable una regla de alerta, incluya el parámetro hello **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="ac614-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="ac614-187">Obtención de una lista de métricas disponibles para las alertas</span><span class="sxs-lookup"><span data-stu-id="ac614-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="ac614-188">Puede usar hello `Get-AzureRmMetricDefinition` lista de cmdlets tooview Hola de todas las métricas para un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="ac614-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="ac614-189">Hello en el ejemplo siguiente se genera una tabla con nombre de métrica de Hola y Hola unidad para él.</span><span class="sxs-lookup"><span data-stu-id="ac614-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="ac614-190">Hay disponible una lista completa de opciones para `Get-AzureRmMetricDefinition` en [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac614-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="ac614-191">Creación y administración de la configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="ac614-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="ac614-192">Los recursos, como las aplicaciones web, las máquinas virtuales, los servicios en la nube o los conjuntos de escalado de máquinas virtuales, solo pueden tener una configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="ac614-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="ac614-193">Sin embargo, cada configuración de escalado automático puede tener varios perfiles.</span><span class="sxs-lookup"><span data-stu-id="ac614-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="ac614-194">Por ejemplo, uno para un perfil de escalado basado en el rendimiento y otro para uno basado en la programación.</span><span class="sxs-lookup"><span data-stu-id="ac614-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="ac614-195">Cada perfil puede tener varias reglas configuradas.</span><span class="sxs-lookup"><span data-stu-id="ac614-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="ac614-196">Para obtener más información acerca de escalado automático, consulte [cómo tooAutoscale una aplicación](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ac614-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="ac614-197">Estos son los pasos de Hola que se usará:</span><span class="sxs-lookup"><span data-stu-id="ac614-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="ac614-198">Cree reglas.</span><span class="sxs-lookup"><span data-stu-id="ac614-198">Create rule(s).</span></span>
2. <span data-ttu-id="ac614-199">Crear perfiles de Hola de asignación de reglas que creó previamente toohello perfiles.</span><span class="sxs-lookup"><span data-stu-id="ac614-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="ac614-200">Opcional: cree notificaciones de escalado automático configurando las propiedades de Webhook y correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="ac614-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="ac614-201">Crear una configuración de escalado automático con un nombre de recurso de destino de hello mediante la asignación de perfiles de Hola y notificaciones que creó en los pasos anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac614-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="ac614-202">Hello en los ejemplos siguientes muestran cómo se puede crear una configuración de escalado automático para un conjunto de escala de máquinas virtuales para un sistema operativo de Windows usando la métrica de uso de CPU de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac614-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="ac614-203">En primer lugar, cree una regla tooscale y de salida, con un aumento del número de instancia.</span><span class="sxs-lookup"><span data-stu-id="ac614-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="ac614-204">A continuación, cree una regla tooscale de, con una disminución del recuento de instancia.</span><span class="sxs-lookup"><span data-stu-id="ac614-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="ac614-205">A continuación, cree un perfil para las reglas de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac614-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="ac614-206">Cree una propiedad de Webhook.</span><span class="sxs-lookup"><span data-stu-id="ac614-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="ac614-207">Crear ninguna propiedad de notificación de hello para la configuración de escalado automático de hello, incluido el correo electrónico y Hola webhook que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ac614-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="ac614-208">Finalmente, cree Hola configuración tooadd Hola perfil de escalado automático que haya creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ac614-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="ac614-209">Para obtener más información sobre cómo administrar la configuración de escalado automático, consulte [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac614-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="ac614-210">Historial de escalado automático</span><span class="sxs-lookup"><span data-stu-id="ac614-210">Autoscale history</span></span>
<span data-ttu-id="ac614-211">Hello en el ejemplo siguiente se muestra cómo puede ver eventos recientes de escalado automático y esta alerta.</span><span class="sxs-lookup"><span data-stu-id="ac614-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="ac614-212">Usar historial de hello actividad registro búsqueda tooview Hola escalado automático.</span><span class="sxs-lookup"><span data-stu-id="ac614-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="ac614-213">Puede usar hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve historial de Autoescala.</span><span class="sxs-lookup"><span data-stu-id="ac614-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="ac614-214">Para obtener más información, consulte [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac614-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="ac614-215">Consulta de los detalles de una configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="ac614-215">View details for an autoscale setting</span></span>
<span data-ttu-id="ac614-216">Puede usar hello `Get-Autoscalesetting` tooretrieve de cmdlet para obtener más información acerca de la configuración de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac614-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="ac614-217">Hello en el ejemplo siguiente se muestra información detallada sobre todas las opciones de escalado automático en el grupo de recursos de hello 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="ac614-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="ac614-218">Hello en el ejemplo siguiente se muestra información detallada sobre todas las opciones de escalado automático en el grupo de recursos de hello 'myrg1' y Hola específicamente la configuración de escalado automático con el nombre 'MyScaleVMSSSetting'.</span><span class="sxs-lookup"><span data-stu-id="ac614-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="ac614-219">Eliminación de una configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="ac614-219">Remove an autoscale setting</span></span>
<span data-ttu-id="ac614-220">Puede usar hello `Remove-Autoscalesetting` cmdlet toodelete una configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="ac614-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="ac614-221">Administración de perfiles de registro para el registro de actividades</span><span class="sxs-lookup"><span data-stu-id="ac614-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="ac614-222">Puede crear un *registro perfil* y exportar los datos de la cuenta de almacenamiento de tooa de registro de actividad y pueden configurar la retención de datos para él.</span><span class="sxs-lookup"><span data-stu-id="ac614-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="ac614-223">Si lo desea, también puede transmitir datos de hello tooyour concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="ac614-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="ac614-224">Tenga en cuenta que esta característica se encuentra actualmente en la fase de vista previa y solo puede crear un perfil de registro por suscripción.</span><span class="sxs-lookup"><span data-stu-id="ac614-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="ac614-225">Puede usar hello después cmdlets con los toocreate de suscripción actual y administrar perfiles de registro.</span><span class="sxs-lookup"><span data-stu-id="ac614-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="ac614-226">También puede elegir una suscripción específica.</span><span class="sxs-lookup"><span data-stu-id="ac614-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="ac614-227">Aunque PowerShell tiene como valor predeterminado toohello de suscripción actual, puede cambiar siempre que el uso de `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="ac614-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="ac614-228">Puede configurar la cuenta de almacenamiento de tooany de datos tooroute de registro de actividad o un concentrador de eventos dentro de esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="ac614-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="ac614-229">Los datos se escriben como archivos blob en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ac614-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="ac614-230">Obtención de un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="ac614-230">Get a log profile</span></span>
<span data-ttu-id="ac614-231">toofetch los perfiles de registro existente, use hello `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac614-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="ac614-232">Adición de un perfil de registro sin retención de datos</span><span class="sxs-lookup"><span data-stu-id="ac614-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="ac614-233">Eliminación de perfil de registro</span><span class="sxs-lookup"><span data-stu-id="ac614-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="ac614-234">Adición de un perfil de registro con retención de datos</span><span class="sxs-lookup"><span data-stu-id="ac614-234">Add a log profile with data retention</span></span>
<span data-ttu-id="ac614-235">Puede especificar hello **- RetentionInDays** propiedad con hello número de días, como un entero positivo, donde se conservan los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac614-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="ac614-236">Adición de un perfil de registro retención y EventHub</span><span class="sxs-lookup"><span data-stu-id="ac614-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="ac614-237">En suma toorouting su cuenta de toostorage de datos, también puede transmitirlo tooan concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="ac614-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="ac614-238">Tenga en cuenta que en esta versión preliminar hello y versión de configuración de la cuenta de almacenamiento es obligatorio pero configuración del centro de eventos es opcional.</span><span class="sxs-lookup"><span data-stu-id="ac614-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="ac614-239">Configuración de registros de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ac614-239">Configure diagnostics logs</span></span>
<span data-ttu-id="ac614-240">Muchos servicios de Azure proporcionan tooEvent centros de envío de registros adicionales y telemetría que puede ser datos toosave configurado en la cuenta de almacenamiento de Azure, o envían el área de trabajo de análisis de registros de OMS tooan.</span><span class="sxs-lookup"><span data-stu-id="ac614-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="ac614-241">Esta operación solo puede realizarse en un nivel de recursos y concentrador de evento o la cuenta de almacenamiento Hola debe estar presente en hello misma región como recurso de destino de Hola donde se configura la configuración de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac614-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="ac614-242">Obtención de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ac614-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="ac614-243">Deshabilitación de la configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ac614-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="ac614-244">Habilitación de la configuración de diagnóstico sin retención</span><span class="sxs-lookup"><span data-stu-id="ac614-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="ac614-245">Habilitación la configuración de diagnóstico con retención</span><span class="sxs-lookup"><span data-stu-id="ac614-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="ac614-246">Habilitación de la configuración de diagnóstico con retención para una categoría de registro específica</span><span class="sxs-lookup"><span data-stu-id="ac614-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="ac614-247">Habilitación de la configuración de diagnóstico para Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ac614-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="ac614-248">Habilitación de la configuración de diagnóstico para OMS</span><span class="sxs-lookup"><span data-stu-id="ac614-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
