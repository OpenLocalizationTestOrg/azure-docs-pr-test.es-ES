---
title: "Creación de alertas para los servicios de Azure | Microsoft Docs"
description: "Desencadenamiento de correos electrónicos y notificaciones, y llamadas a direcciones URL de sitios web (webhooks) o a la automatización cuando se cumplen las condiciones especificadas."
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
ms.openlocfilehash: 50127242cdf156771d0610e58cf2fc41281adae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="f7d5d-103">Creación de alertas de métricas en Azure Monitor para servicios de Azure: PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7d5d-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7d5d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f7d5d-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="f7d5d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7d5d-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="f7d5d-106">CLI</span><span class="sxs-lookup"><span data-stu-id="f7d5d-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="f7d5d-107">Información general</span><span class="sxs-lookup"><span data-stu-id="f7d5d-107">Overview</span></span>
<span data-ttu-id="f7d5d-108">En este artículo se muestra cómo configurar alertas de métricas de Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-108">This article shows you how to set up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="f7d5d-109">Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="f7d5d-110">**Valores de métrica** : la alerta se desencadena cuando el valor de una métrica específica cruza un umbral asignado en cualquier dirección.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="f7d5d-111">Es decir, se desencadena tanto la primera vez que se cumple la condición como después, cuando dicha condición ya deja de cumplirse.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="f7d5d-112">**Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="f7d5d-113">Para obtener más información sobre las alertas de registro de actividad, [haga clic aquí](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f7d5d-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="f7d5d-114">Puede configurar una alerta de métrica para hacer lo siguiente cuando se desencadena:</span><span class="sxs-lookup"><span data-stu-id="f7d5d-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="f7d5d-115">Enviar notificaciones de correo electrónico al administrador y los coadministradores del servicio.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="f7d5d-116">Enviar un correo electrónico a direcciones de correo electrónico adicionales que especifique.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="f7d5d-117">Llamar a un webhook.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-117">call a webhook</span></span>
* <span data-ttu-id="f7d5d-118">Iniciar la ejecución de un runbook de Azure (solo desde Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="f7d5d-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="f7d5d-119">Puede obtener información sobre las reglas de alerta y configurarlas mediante:</span><span class="sxs-lookup"><span data-stu-id="f7d5d-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="f7d5d-120">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f7d5d-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="f7d5d-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7d5d-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="f7d5d-122">Interfaz de la línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="f7d5d-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="f7d5d-123">API de REST de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f7d5d-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="f7d5d-124">Para información adicional, siempre puede escribir ```Get-Help``` y, luego, el comando de PowerShell sobre el que desea obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="f7d5d-125">Creación de reglas de alerta en PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7d5d-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="f7d5d-126">Inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-126">Log in to Azure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="f7d5d-127">Obtenga una lista de las suscripciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-127">Get a list of the subscriptions you have available.</span></span> <span data-ttu-id="f7d5d-128">Compruebe que trabaja con la suscripción adecuada.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-128">Verify that you are working with the right subscription.</span></span> <span data-ttu-id="f7d5d-129">Si no es así, establezca la suscripción correcta con la salida de `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="f7d5d-130">Para ver las reglas existentes en un grupo de recursos, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="f7d5d-130">To list existing rules on a resource group, use the following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="f7d5d-131">Para crear una regla, primero debe contar con varios datos importantes.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-131">To create a rule, you need to have several important pieces of information first.</span></span>

  * <span data-ttu-id="f7d5d-132">El **identificador de recurso** del recursos para el que desea establecer una alerta.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-132">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="f7d5d-133">Las **definiciones de métricas** disponibles para ese recurso.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-133">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="f7d5d-134">Una forma de obtener el identificador de recurso es usar Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-134">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="f7d5d-135">Seleccione el recurso en el portal, suponiendo que ya existe.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-135">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="f7d5d-136">En la sección *Configuración* de la hoja siguiente, seleccione *Propiedades*.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-136">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="f7d5d-137">El campo **RESOURCE ID** está en la hoja siguiente.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-137">**RESOURCE ID** is a field in the next blade.</span></span> <span data-ttu-id="f7d5d-138">Otra forma que puede usar es el [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f7d5d-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="f7d5d-139">Este es un ejemplo de identificador de recursos de una aplicación web:</span><span class="sxs-lookup"><span data-stu-id="f7d5d-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="f7d5d-140">Puede usar `Get-AzureRmMetricDefinition` para ver la lista de todas las definiciones de métricas de un recurso específico.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="f7d5d-141">En el ejemplo siguiente se genera una tabla con el nombre y la unidad de esa métrica.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-141">The following example generates a table with the metric Name and the Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="f7d5d-142">Ejecute Get-MetricDefinitions para obtener una lista completa de las opciones disponibles para Get-AzureRmMetricDefinition.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="f7d5d-143">En el ejemplo siguiente se configura una alerta en un recurso de sitio web.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-143">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="f7d5d-144">La alerta se desencadena cada vez que se recibe constantemente cualquier tráfico durante 5 minutos y nuevamente cuando no se recibe tráfico durante 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="f7d5d-145">Para crear un webhook o enviar un correo electrónico cuando se desencadene una alerta, debe crear el correo electrónico o los webhooks.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span></span> <span data-ttu-id="f7d5d-146">Cree la regla inmediatamente después con la etiqueta -Actions, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span></span> <span data-ttu-id="f7d5d-147">No puede asociar webhooks o correos electrónicos con reglas ya creadas mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="f7d5d-148">Observe las reglas individuales para comprobar que las alertas se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-148">To verify that your alerts have been created properly by looking at the individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="f7d5d-149">Elimine las alertas.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-149">Delete your alerts.</span></span> <span data-ttu-id="f7d5d-150">Estos comandos eliminan las reglas que se crearon anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-150">These commands delete the rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="f7d5d-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f7d5d-151">Next steps</span></span>
* <span data-ttu-id="f7d5d-152">[Obtenga información general sobre la supervisión de Azure](monitoring-overview.md) , incluidos los tipos de información que puede recopilar y supervisar.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="f7d5d-153">Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f7d5d-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="f7d5d-154">Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f7d5d-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="f7d5d-155">Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="f7d5d-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="f7d5d-156">Obtenga [información general sobre la colección de registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) para recopilar métricas detalladas de alta frecuencia sobre el servicio.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="f7d5d-157">Obtenga [información general sobre la colección de métricas](insights-how-to-customize-monitoring.md) para garantizar que el servicio está disponible y que responder adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="f7d5d-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
