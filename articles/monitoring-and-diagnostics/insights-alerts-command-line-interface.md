---
title: "Creación de alertas para servicios de Azure - CLI multiplataforma | Microsoft Docs"
description: "Desencadenamiento de correos electrónicos y notificaciones, y llamadas a direcciones URL de sitios web (webhooks) o a la automatización cuando se cumplen las condiciones especificadas."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="6a706-103">Creación de alertas de métricas en Azure Monitor para los servicios de Azure: CLI multiplataforma</span><span class="sxs-lookup"><span data-stu-id="6a706-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a706-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6a706-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="6a706-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a706-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="6a706-106">CLI</span><span class="sxs-lookup"><span data-stu-id="6a706-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="6a706-107">Información general</span><span class="sxs-lookup"><span data-stu-id="6a706-107">Overview</span></span>
<span data-ttu-id="6a706-108">En este artículo se muestra cómo configurar alertas de métricas de Azure con la interfaz de la línea de comandos (CLI) multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="6a706-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="6a706-109">Azure Monitor es el nuevo nombre de lo que se conocía como "Azure Insights" hasta el 25 de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="6a706-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="6a706-110">Sin embargo, los espacios de nombres y, por tanto, los siguientes comandos aún contienen el término "insights".</span><span class="sxs-lookup"><span data-stu-id="6a706-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="6a706-111">Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="6a706-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="6a706-112">**Valores de métrica** : la alerta se desencadena cuando el valor de una métrica específica cruza un umbral asignado en cualquier dirección.</span><span class="sxs-lookup"><span data-stu-id="6a706-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="6a706-113">Es decir, se desencadena tanto la primera vez que se cumple la condición como después, cuando dicha condición ya deja de cumplirse.</span><span class="sxs-lookup"><span data-stu-id="6a706-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="6a706-114">**Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos.</span><span class="sxs-lookup"><span data-stu-id="6a706-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="6a706-115">Para obtener más información sobre las alertas de registro de actividad, [haga clic aquí](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6a706-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="6a706-116">Puede configurar una alerta de métrica para hacer lo siguiente cuando se desencadena:</span><span class="sxs-lookup"><span data-stu-id="6a706-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="6a706-117">Enviar notificaciones de correo electrónico al administrador y los coadministradores del servicio.</span><span class="sxs-lookup"><span data-stu-id="6a706-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="6a706-118">Enviar un correo electrónico a direcciones de correo electrónico adicionales que especifique.</span><span class="sxs-lookup"><span data-stu-id="6a706-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="6a706-119">Llamar a un webhook.</span><span class="sxs-lookup"><span data-stu-id="6a706-119">call a webhook</span></span>
* <span data-ttu-id="6a706-120">Iniciar la ejecución de un runbook de Azure (en este momento, solo desde Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="6a706-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="6a706-121">Puede obtener información sobre las reglas de alerta de métricas y configurarlas mediante:</span><span class="sxs-lookup"><span data-stu-id="6a706-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="6a706-122">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6a706-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="6a706-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a706-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="6a706-124">Interfaz de la línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="6a706-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="6a706-125">API de REST de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="6a706-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="6a706-126">Siempre puede escribir un comando y agregar -help al final para obtener ayuda sobre dicho comando.</span><span class="sxs-lookup"><span data-stu-id="6a706-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="6a706-127">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6a706-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="6a706-128">Creación de reglas de alerta mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="6a706-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="6a706-129">Cumpla los requisitos previos e inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="6a706-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="6a706-130">Consulte los [ejemplos de CLI de Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6a706-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="6a706-131">En pocas palabras, instale la CLI y ejecute estos comandos.</span><span class="sxs-lookup"><span data-stu-id="6a706-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="6a706-132">Con estos comandos, puede iniciar sesión, ver la suscripción que usa y prepararse para ejecutar comandos de Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="6a706-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="6a706-133">Para ver las reglas existentes en un grupo de recursos, use el formato siguiente **azure insights alerts rule list** *[opciones] &lt;grupoRecursos&gt;*</span><span class="sxs-lookup"><span data-stu-id="6a706-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="6a706-134">Para crear una regla, primero debe contar con varios datos importantes.</span><span class="sxs-lookup"><span data-stu-id="6a706-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="6a706-135">El **identificador de recurso** del recursos para el que desea establecer una alerta.</span><span class="sxs-lookup"><span data-stu-id="6a706-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="6a706-136">Las **definiciones de métricas** disponibles para ese recurso.</span><span class="sxs-lookup"><span data-stu-id="6a706-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="6a706-137">Una forma de obtener el identificador de recurso es usar Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6a706-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="6a706-138">Seleccione el recurso en el portal, suponiendo que ya existe.</span><span class="sxs-lookup"><span data-stu-id="6a706-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="6a706-139">En la sección *Configuración* de la hoja siguiente, seleccione *Propiedades*.</span><span class="sxs-lookup"><span data-stu-id="6a706-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="6a706-140">El campo *RESOURCE ID* está en la hoja siguiente.</span><span class="sxs-lookup"><span data-stu-id="6a706-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="6a706-141">Otra forma que puede usar es el [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6a706-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="6a706-142">El siguiente es un ejemplo de identificador de recurso de una aplic. web:</span><span class="sxs-lookup"><span data-stu-id="6a706-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="6a706-143">Para obtener una lista de las métricas disponibles y las unidades de esas métricas para el ejemplo de recurso anterior, use el siguiente comando de CLI:</span><span class="sxs-lookup"><span data-stu-id="6a706-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="6a706-144">*PT1M* es la granularidad de la medida disponible (intervalos de 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="6a706-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="6a706-145">El uso de distintas granularidades le brinda opciones de métricas diferentes.</span><span class="sxs-lookup"><span data-stu-id="6a706-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="6a706-146">Para crear una regla de alerta basada en métricas, use un comando con el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="6a706-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="6a706-147">**azure insights alerts rule metric set** *[opciones] &lt;nombreRegla&gt; &lt;ubicación&gt; &lt;grupoRecursos&gt; &lt;tamañoVentana&gt; &lt;operador&gt; &lt;umbral&gt; &lt;idRecursoObjetivo&gt; &lt;nombreMétrica&gt; &lt;horaInserciónOperador&gt;*</span><span class="sxs-lookup"><span data-stu-id="6a706-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="6a706-148">En el ejemplo siguiente se configura una alerta en un recurso de sitio web.</span><span class="sxs-lookup"><span data-stu-id="6a706-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="6a706-149">La alerta se desencadena cada vez que se recibe constantemente cualquier tráfico durante 5 minutos y nuevamente cuando no se recibe tráfico durante 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="6a706-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="6a706-150">Para crear un webhook o enviar un correo electrónico cuando se active una alerta de métrica, debe crear el correo electrónico o los webhooks.</span><span class="sxs-lookup"><span data-stu-id="6a706-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="6a706-151">Cree la regla inmediatamente después.</span><span class="sxs-lookup"><span data-stu-id="6a706-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="6a706-152">No puede asociar webhooks o correos electrónicos con reglas ya creadas mediante la CLI.</span><span class="sxs-lookup"><span data-stu-id="6a706-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="6a706-153">Observe una regla individual para comprobar que las alertas se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="6a706-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="6a706-154">Para eliminar reglas, use un comando con este formato:</span><span class="sxs-lookup"><span data-stu-id="6a706-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="6a706-155">**insights alerts rule delete** [opciones] &lt;grupoRecursos&gt; &lt;nombreRegla&gt;</span><span class="sxs-lookup"><span data-stu-id="6a706-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="6a706-156">Estos comandos eliminan las reglas que se crearon anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="6a706-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="6a706-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6a706-157">Next steps</span></span>
* <span data-ttu-id="6a706-158">[Obtenga información general sobre la supervisión de Azure](monitoring-overview.md) , incluidos los tipos de información que puede recopilar y supervisar.</span><span class="sxs-lookup"><span data-stu-id="6a706-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="6a706-159">Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6a706-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="6a706-160">Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6a706-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="6a706-161">Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="6a706-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="6a706-162">Obtenga [información general sobre la colección de registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) para recopilar métricas detalladas de alta frecuencia sobre el servicio.</span><span class="sxs-lookup"><span data-stu-id="6a706-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="6a706-163">Obtenga [información general sobre la colección de métricas](insights-how-to-customize-monitoring.md) para garantizar que el servicio está disponible y que responder adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="6a706-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
