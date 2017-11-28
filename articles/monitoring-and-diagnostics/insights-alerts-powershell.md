---
title: aaaCreate alertas para los servicios de Azure - PowerShell | Documentos de Microsoft
description: "Desencadenador los correos electrónicos, notificaciones, llame a direcciones URL de sitios Web (webhooks), o la automatización cuando se cumplen las condiciones de Hola que especifique."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="e5720-103">Creación de alertas de métricas en Azure Monitor para servicios de Azure: PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5720-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5720-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e5720-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="e5720-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5720-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="e5720-106">CLI</span><span class="sxs-lookup"><span data-stu-id="e5720-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="e5720-107">Información general</span><span class="sxs-lookup"><span data-stu-id="e5720-107">Overview</span></span>
<span data-ttu-id="e5720-108">Este artículo muestra cómo tooset una métrica Azure alertas mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5720-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="e5720-109">Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="e5720-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="e5720-110">**Valores de métrica** : hello desencadenadores de alerta cuando el valor Hola de una métrica especificada está fuera de un umbral asignar en cualquier dirección.</span><span class="sxs-lookup"><span data-stu-id="e5720-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="e5720-111">Es decir, desencadena tanto cuando primero se cumple la condición de hello y, a continuación, después cuando la condición que ya no se cumple.</span><span class="sxs-lookup"><span data-stu-id="e5720-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="e5720-112">**Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos.</span><span class="sxs-lookup"><span data-stu-id="e5720-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="e5720-113">más información acerca de las alertas de registro de actividad toolearn [haga clic aquí](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="e5720-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="e5720-114">Puede configurar una métrica toodo alerta hello las siguientes cuando se desencadena:</span><span class="sxs-lookup"><span data-stu-id="e5720-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="e5720-115">enviar el administrador del servicio de toohello de notificaciones de correo electrónico y coadministradores</span><span class="sxs-lookup"><span data-stu-id="e5720-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="e5720-116">enviar correo electrónico mensajes de correo electrónico de tooadditional que especifique.</span><span class="sxs-lookup"><span data-stu-id="e5720-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="e5720-117">Llamar a un webhook.</span><span class="sxs-lookup"><span data-stu-id="e5720-117">call a webhook</span></span>
* <span data-ttu-id="e5720-118">iniciar la ejecución de un runbook de Azure (solo de Hola portal de Azure)</span><span class="sxs-lookup"><span data-stu-id="e5720-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="e5720-119">Puede obtener información sobre las reglas de alerta y configurarlas mediante:</span><span class="sxs-lookup"><span data-stu-id="e5720-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="e5720-120">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e5720-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="e5720-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5720-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="e5720-122">Interfaz de la línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="e5720-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="e5720-123">API de REST de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="e5720-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="e5720-124">Para obtener información adicional, puede escribir siempre ```Get-Help``` y, a continuación, Hola desea obtener ayuda en el comando de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5720-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="e5720-125">Creación de reglas de alerta en PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5720-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="e5720-126">Inicie sesión en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e5720-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="e5720-127">Obtener una lista de suscripciones de Hola que tiene disponible.</span><span class="sxs-lookup"><span data-stu-id="e5720-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="e5720-128">Compruebe que está trabajando con suscripción derecho Hola.</span><span class="sxs-lookup"><span data-stu-id="e5720-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="e5720-129">Si no es así, establezca toohello derecha con valores obtenidos hello en `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="e5720-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="e5720-130">las reglas de toolist existentes en un grupo de recursos, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e5720-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="e5720-131">toocreate una regla, debe toohave varios fragmentos de información importantes en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="e5720-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="e5720-132">Hola **Id. de recurso** para el recurso de hello desea tooset una alerta para</span><span class="sxs-lookup"><span data-stu-id="e5720-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="e5720-133">Hola **definiciones de métrica** disponibles para dicho recurso</span><span class="sxs-lookup"><span data-stu-id="e5720-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="e5720-134">Hola tooget una manera de Id. de recurso es toouse Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5720-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="e5720-135">Suponiendo que ya se ha creado el recurso de hello, selecciónela en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5720-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="e5720-136">A continuación, en la hoja de hello siguiente, seleccione *propiedades* en hello *configuración* sección.</span><span class="sxs-lookup"><span data-stu-id="e5720-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="e5720-137">**Id. de recurso** es un campo en la hoja siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e5720-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="e5720-138">Otra manera es hello toouse [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5720-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="e5720-139">Este es un ejemplo de identificador de recursos de una aplicación web:</span><span class="sxs-lookup"><span data-stu-id="e5720-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="e5720-140">Puede usar `Get-AzureRmMetricDefinition` tooview lista de Hola de todas las definiciones métricas para un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="e5720-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="e5720-141">Hello en el ejemplo siguiente se genera una tabla con nombre de métrica de Hola y Hola unidad para esa métrica.</span><span class="sxs-lookup"><span data-stu-id="e5720-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="e5720-142">Ejecute Get-MetricDefinitions para obtener una lista completa de las opciones disponibles para Get-AzureRmMetricDefinition.</span><span class="sxs-lookup"><span data-stu-id="e5720-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="e5720-143">Hola siguiendo el ejemplo se configura una alerta en un recurso de sitio web.</span><span class="sxs-lookup"><span data-stu-id="e5720-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="e5720-144">desencadenadores de alerta de Hello siempre que sea coherente recibe todo el tráfico de 5 minutos y cuando no recibe ningún tipo de tráfico durante 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e5720-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="e5720-145">toocreate webhook o enviar correo electrónico cuando se desencadena una alerta, en primer lugar crear correo electrónico de Hola o webhook.</span><span class="sxs-lookup"><span data-stu-id="e5720-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="e5720-146">A continuación, cree inmediatamente regla Hola posteriormente con Hola - etiqueta de acciones y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5720-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="e5720-147">No puede asociar webhooks o correos electrónicos con reglas ya creadas mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5720-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="e5720-148">tooverify que se han creado correctamente las alertas echando un vistazo a reglas individuales Hola.</span><span class="sxs-lookup"><span data-stu-id="e5720-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="e5720-149">Elimine las alertas.</span><span class="sxs-lookup"><span data-stu-id="e5720-149">Delete your alerts.</span></span> <span data-ttu-id="e5720-150">Estos comandos eliminan reglas de Hola que creó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e5720-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="e5720-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5720-151">Next steps</span></span>
* <span data-ttu-id="e5720-152">[Obtener una visión general de supervisión de Azure](monitoring-overview.md) incluidos Hola los tipos de información que puede recopilar y supervisar.</span><span class="sxs-lookup"><span data-stu-id="e5720-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="e5720-153">Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e5720-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="e5720-154">Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e5720-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="e5720-155">Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="e5720-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="e5720-156">Obtener un [información general de recopilar registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detallada las métricas de alta frecuencia en su servicio.</span><span class="sxs-lookup"><span data-stu-id="e5720-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="e5720-157">Obtener un [información general de la colección de métricas](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="e5720-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
