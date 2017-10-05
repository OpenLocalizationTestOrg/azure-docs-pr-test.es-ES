---
title: Respuesta a las alertas en OMS Log Analytics | Microsoft Docs
description: "Las alertas de Log Analytics identifican información importante en el repositorio de OMS y pueden avisarle proactivamente de problemas o invocar acciones para intentar corregirlos.  En este artículo se describe cómo crear una regla de alerta y los detalles de las distintas acciones que pueden realizar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a><span data-ttu-id="dd20b-104">Adición de acciones a reglas de alerta en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="dd20b-104">Add actions to alert rules in Log Analytics</span></span>
<span data-ttu-id="dd20b-105">Cuando se [crea una alerta en Log Analytics](log-analytics-alerts.md), tiene la opción de [configurar la regla de alerta](log-analytics-alerts.md) para realizar una o varias acciones.</span><span class="sxs-lookup"><span data-stu-id="dd20b-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have the option of [configuring the alert rule](log-analytics-alerts.md) to perform one or more actions.</span></span>  <span data-ttu-id="dd20b-106">En este artículo se describen las diferentes acciones que están disponibles y los detalles sobre la configuración de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="dd20b-106">This article describes the different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="dd20b-107">Acción</span><span class="sxs-lookup"><span data-stu-id="dd20b-107">Action</span></span> | <span data-ttu-id="dd20b-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="dd20b-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="dd20b-109">Correo electrónico</span><span class="sxs-lookup"><span data-stu-id="dd20b-109">Email</span></span>](#email-actions) | <span data-ttu-id="dd20b-110">Envía un correo electrónico con los detalles de la alerta a uno o varios destinatarios.</span><span class="sxs-lookup"><span data-stu-id="dd20b-110">Send an e-mail with the details of the alert to one or more recipients.</span></span> |
| [<span data-ttu-id="dd20b-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="dd20b-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="dd20b-112">Invoca un proceso externo a través de una sola solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="dd20b-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="dd20b-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="dd20b-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="dd20b-114">Inicia un runbook en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="dd20b-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="dd20b-115">Acciones de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="dd20b-115">Email actions</span></span>
<span data-ttu-id="dd20b-116">Las acciones de correo electrónico envían un correo electrónico con los detalles de la alerta a uno o varios destinatarios.</span><span class="sxs-lookup"><span data-stu-id="dd20b-116">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>  <span data-ttu-id="dd20b-117">Puede especificar el asunto del mensaje de correo, pero su contenido es un formato estándar construido por Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dd20b-117">You can specify the subject of the mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="dd20b-118">En él se incluye información de resumen, como el nombre de la alerta, además de los detalles de hasta diez registros devueltos por la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="dd20b-118">It includes summary information such as the name of the alert in addition to details of up to ten records returned by the log search.</span></span>  <span data-ttu-id="dd20b-119">También se incluye un vínculo a una búsqueda de registros de Log Analytics que devolverá todo el conjunto de registros de esa consulta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-119">It also includes a link to a log search in Log Analytics that will return the entire set of records from that query.</span></span>   <span data-ttu-id="dd20b-120">El remitente del mensaje de correo es el *equipo de Microsoft Operations Management Suite&lt;noreply@oms.microsoft.com&gt;*.</span><span class="sxs-lookup"><span data-stu-id="dd20b-120">The sender of the mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="dd20b-121">Las acciones de correo electrónico requieren las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="dd20b-121">Email actions require the properties in the following table.</span></span>

| <span data-ttu-id="dd20b-122">Propiedad</span><span class="sxs-lookup"><span data-stu-id="dd20b-122">Property</span></span> | <span data-ttu-id="dd20b-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="dd20b-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dd20b-124">Asunto</span><span class="sxs-lookup"><span data-stu-id="dd20b-124">Subject</span></span> |<span data-ttu-id="dd20b-125">El asunto del correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="dd20b-125">Subject in the email.</span></span>  <span data-ttu-id="dd20b-126">No se puede modificar el cuerpo del mensaje de correo.</span><span class="sxs-lookup"><span data-stu-id="dd20b-126">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="dd20b-127">Recipients</span><span class="sxs-lookup"><span data-stu-id="dd20b-127">Recipients</span></span> |<span data-ttu-id="dd20b-128">Direcciones de todos los destinatarios de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="dd20b-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="dd20b-129">Si especifica más de una dirección, separe las direcciones con un punto y coma (;).</span><span class="sxs-lookup"><span data-stu-id="dd20b-129">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="dd20b-130">Acciones de webhook</span><span class="sxs-lookup"><span data-stu-id="dd20b-130">Webhook actions</span></span>

<span data-ttu-id="dd20b-131">Las acciones de Webhook permiten invocar un proceso externo a través de una sola solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="dd20b-131">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="dd20b-132">El servicio que se llama debe admitir webhooks y determinar cómo utilizará toda la carga que reciba.</span><span class="sxs-lookup"><span data-stu-id="dd20b-132">The service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="dd20b-133">También puede llamar a una API de REST que no admita específicamente webhooks mientras la solicitud esté en un formato que entienda la API.</span><span class="sxs-lookup"><span data-stu-id="dd20b-133">You could also call a REST API that doesn't specifically support webhooks as long as the request is in a format that the API understands.</span></span>  <span data-ttu-id="dd20b-134">Ejemplos de uso de un webhook en respuesta a una alerta donde se envía un mensaje en [Slack](http://slack.com) o se crea un incidente en [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="dd20b-134">Examples of using a webhook in response to an alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="dd20b-135">Puede encontrar un tutorial completo sobre la creación de una regla de alerta con un webhook para llamar a Slack en [Webhooks en alertas de Log Analytics](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="dd20b-135">A complete walkthrough of creating an alert rule with a webhook to call Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="dd20b-136">Las acciones de webhook requieren las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="dd20b-136">Webhook actions require the properties in the following table.</span></span>

| <span data-ttu-id="dd20b-137">Propiedad</span><span class="sxs-lookup"><span data-stu-id="dd20b-137">Property</span></span> | <span data-ttu-id="dd20b-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="dd20b-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dd20b-139">Dirección URL de Webhook</span><span class="sxs-lookup"><span data-stu-id="dd20b-139">Webhook URL</span></span> |<span data-ttu-id="dd20b-140">La dirección URL del webhook.</span><span class="sxs-lookup"><span data-stu-id="dd20b-140">The URL of the webhook.</span></span> |
| <span data-ttu-id="dd20b-141">Carga de JSON personalizada</span><span class="sxs-lookup"><span data-stu-id="dd20b-141">Custom JSON payload</span></span> |<span data-ttu-id="dd20b-142">Carga personalizada para enviar con el webhook.</span><span class="sxs-lookup"><span data-stu-id="dd20b-142">Custom payload to send with the webhook.</span></span>  <span data-ttu-id="dd20b-143">Consulte a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="dd20b-143">See below for details.</span></span> |


<span data-ttu-id="dd20b-144">Los webhooks incluyen una dirección URL y una carga en formato JSON que son los datos enviados al servicio externo.</span><span class="sxs-lookup"><span data-stu-id="dd20b-144">Webhooks include a URL and a payload formatted in JSON that is the data sent to the external service.</span></span>  <span data-ttu-id="dd20b-145">De forma predeterminada, la carga incluirá los valores en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="dd20b-145">By default, the payload will include the values in the following table.</span></span>  <span data-ttu-id="dd20b-146">Puede optar por reemplazar esta carga con una personalizada de su propiedad.</span><span class="sxs-lookup"><span data-stu-id="dd20b-146">You can choose to replace this payload with a custom one of your own.</span></span>  <span data-ttu-id="dd20b-147">En ese caso, puede utilizar las variables de la tabla para cada uno de los parámetros para incluir su valor en la carga personalizada.</span><span class="sxs-lookup"><span data-stu-id="dd20b-147">In that case you can use the variables in the table for each of the parameters to include their value in your custom payload.</span></span>

| <span data-ttu-id="dd20b-148">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dd20b-148">Parameter</span></span> | <span data-ttu-id="dd20b-149">Variable</span><span class="sxs-lookup"><span data-stu-id="dd20b-149">Variable</span></span> | <span data-ttu-id="dd20b-150">Descripción</span><span class="sxs-lookup"><span data-stu-id="dd20b-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="dd20b-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="dd20b-151">AlertRuleName</span></span> |<span data-ttu-id="dd20b-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="dd20b-152">#alertrulename</span></span> |<span data-ttu-id="dd20b-153">Nombre de la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-153">Name of the alert rule.</span></span> |
| <span data-ttu-id="dd20b-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="dd20b-154">AlertThresholdOperator</span></span> |<span data-ttu-id="dd20b-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="dd20b-155">#thresholdoperator</span></span> |<span data-ttu-id="dd20b-156">Operador de umbral para la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-156">Threshold operator for the alert rule.</span></span>  <span data-ttu-id="dd20b-157">*Mayor que* o *menor que*.</span><span class="sxs-lookup"><span data-stu-id="dd20b-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="dd20b-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="dd20b-158">AlertThresholdValue</span></span> |<span data-ttu-id="dd20b-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="dd20b-159">#thresholdvalue</span></span> |<span data-ttu-id="dd20b-160">Valor de umbral para la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-160">Threshold value for the alert rule.</span></span> |
| <span data-ttu-id="dd20b-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="dd20b-161">LinkToSearchResults</span></span> |<span data-ttu-id="dd20b-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="dd20b-162">#linktosearchresults</span></span> |<span data-ttu-id="dd20b-163">Vincular a la búsqueda de registros de Log Analytics que devuelve los registros de la consulta que creó la alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-163">Link to Log Analytics log search that returns the records from the query that created the alert.</span></span> |
| <span data-ttu-id="dd20b-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="dd20b-164">ResultCount</span></span> |<span data-ttu-id="dd20b-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="dd20b-165">#searchresultcount</span></span> |<span data-ttu-id="dd20b-166">Número de registros en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="dd20b-166">Number of records in the search results.</span></span> |
| <span data-ttu-id="dd20b-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="dd20b-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="dd20b-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="dd20b-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="dd20b-169">Hora de finalización de la consulta en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="dd20b-169">End time for the query in UTC format.</span></span> |
| <span data-ttu-id="dd20b-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="dd20b-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="dd20b-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="dd20b-171">#searchinterval</span></span> |<span data-ttu-id="dd20b-172">Período de tiempo para la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-172">Time window for the alert rule.</span></span> |
| <span data-ttu-id="dd20b-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="dd20b-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="dd20b-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="dd20b-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="dd20b-175">Hora de inicio para la consulta en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="dd20b-175">Start time for the query in UTC format.</span></span> |
| <span data-ttu-id="dd20b-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="dd20b-176">SearchQuery</span></span> |<span data-ttu-id="dd20b-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="dd20b-177">#searchquery</span></span> |<span data-ttu-id="dd20b-178">Consulta de búsqueda de registros utilizada por la regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-178">Log search query used by the alert rule.</span></span> |
| <span data-ttu-id="dd20b-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="dd20b-179">SearchResults</span></span> |<span data-ttu-id="dd20b-180">Consulte a continuación</span><span class="sxs-lookup"><span data-stu-id="dd20b-180">See below</span></span> |<span data-ttu-id="dd20b-181">Registros devueltos por la consulta en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="dd20b-181">Records returned by the query in JSON format.</span></span>  <span data-ttu-id="dd20b-182">Limitado a los primeros 5000 registros.</span><span class="sxs-lookup"><span data-stu-id="dd20b-182">Limited to the first 5,000 records.</span></span> |
| <span data-ttu-id="dd20b-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="dd20b-183">WorkspaceID</span></span> |<span data-ttu-id="dd20b-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="dd20b-184">#workspaceid</span></span> |<span data-ttu-id="dd20b-185">Identificador del área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="dd20b-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="dd20b-186">Por ejemplo, podría especificar la siguiente carga personalizada que incluye un único parámetro denominado *text*.</span><span class="sxs-lookup"><span data-stu-id="dd20b-186">For example, you might specify the following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="dd20b-187">El servicio al que llama este webhook estaría esperando este parámetro.</span><span class="sxs-lookup"><span data-stu-id="dd20b-187">The service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="dd20b-188">Esta carga de ejemplo se resolvería en algo similar a lo siguiente al enviarse al webhook.</span><span class="sxs-lookup"><span data-stu-id="dd20b-188">This example payload would resolve to something like the following when sent to the webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="dd20b-189">Para incluir resultados de búsqueda en una carga personalizada, agregue la siguiente línea como una propiedad de nivel superior en la carga de json.</span><span class="sxs-lookup"><span data-stu-id="dd20b-189">To include search results in a custom payload, add the following line as a top level property in the json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="dd20b-190">Por ejemplo, para crear una carga personalizada que incluya solo el nombre de la alerta y los resultados de la búsqueda, puede utilizar lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="dd20b-190">For example, to create a custom payload that includes just the alert name and the search results, you could use the following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="dd20b-191">Puede recorrer un ejemplo completo de creación de una regla de alerta con un webhook para iniciar un servicio externo en [Webhooks en alertas de Log Analytics](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="dd20b-191">You can walk through a complete example of creating an alert rule with a webhook to start an external service at [Create an alert webhook action in OMS Log Analytics to send message to Slack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="dd20b-192">Acciones de runbook</span><span class="sxs-lookup"><span data-stu-id="dd20b-192">Runbook actions</span></span>
<span data-ttu-id="dd20b-193">Las acciones de runbook inician un runbook en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd20b-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="dd20b-194">Para usar este tipo de acción, debe tener la [solución de Automatización](log-analytics-add-solutions.md) instalada y configurada en el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="dd20b-194">In order to use this type of action, you must have the [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="dd20b-195">Puede seleccionar entre los runbooks de la cuenta de automatización que configuró en la solución de Automatización.</span><span class="sxs-lookup"><span data-stu-id="dd20b-195">You can select from the runbooks in the automation account that you configured in the Automation solution.</span></span>

<span data-ttu-id="dd20b-196">Las acciones de runbook requieren las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="dd20b-196">Runbook actions require the properties in the following table.</span></span>

| <span data-ttu-id="dd20b-197">Propiedad</span><span class="sxs-lookup"><span data-stu-id="dd20b-197">Property</span></span> | <span data-ttu-id="dd20b-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="dd20b-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="dd20b-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="dd20b-199">Runbook</span></span> | <span data-ttu-id="dd20b-200">El runbook que desea iniciar cuando se crea una alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-200">Runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="dd20b-201">Ejecutar en</span><span class="sxs-lookup"><span data-stu-id="dd20b-201">Run on</span></span> | <span data-ttu-id="dd20b-202">Especifique **Azure** para ejecutar el runbook en la nube.</span><span class="sxs-lookup"><span data-stu-id="dd20b-202">Specify **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="dd20b-203">Especifique **Hybrid Worker** para ejecutar el runbook en un agente con [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) instalado.</span><span class="sxs-lookup"><span data-stu-id="dd20b-203">Specify **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="dd20b-204">Las acciones de runbook inician el runbook mediante un [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="dd20b-204">Runbook actions start the runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="dd20b-205">Al crear la regla de alerta, se creará automáticamente un nuevo webhook para el runbook con el nombre **OMS Alert Remediation** seguido de un GUID.</span><span class="sxs-lookup"><span data-stu-id="dd20b-205">When you create the alert rule, it will automatically create a new webhook for the runbook with the name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="dd20b-206">No se pueden llenar directamente los parámetros del runbook, pero el [parámetro $WebhookData](../automation/automation-webhooks.md) incluirá los detalles de la alerta, como los resultados de la búsqueda de registros que lo crearan.</span><span class="sxs-lookup"><span data-stu-id="dd20b-206">You cannot directly populate any parameters of the runbook, but the [$WebhookData parameter](../automation/automation-webhooks.md) will include the details of the alert, including the results of the log search that created it.</span></span>  <span data-ttu-id="dd20b-207">El runbook tendrá que definir **$WebhookData** como parámetro para tener acceso a las propiedades de la alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-207">The runbook will need to define **$WebhookData** as a parameter for it to access the properties of the alert.</span></span>  <span data-ttu-id="dd20b-208">Los datos de la alerta están disponibles en formato json en una sola propiedad denominada **SearchResults** de la propiedad **RequestBody** de **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="dd20b-208">The alert data is available in json format in a single property called **SearchResults** in the **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="dd20b-209">Esta tendrá las propiedades de la siguiente tabla.</span><span class="sxs-lookup"><span data-stu-id="dd20b-209">This will have with the properties in the following table.</span></span>

| <span data-ttu-id="dd20b-210">Nodo</span><span class="sxs-lookup"><span data-stu-id="dd20b-210">Node</span></span> | <span data-ttu-id="dd20b-211">Descripción</span><span class="sxs-lookup"><span data-stu-id="dd20b-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dd20b-212">id</span><span class="sxs-lookup"><span data-stu-id="dd20b-212">id</span></span> |<span data-ttu-id="dd20b-213">Ruta de acceso y el GUID de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="dd20b-213">Path and GUID of the search.</span></span> |
| <span data-ttu-id="dd20b-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="dd20b-214">__metadata</span></span> |<span data-ttu-id="dd20b-215">Información sobre la alerta, como el número de registros y el estado de los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="dd20b-215">Information about the alert including the number of records and status of the search results.</span></span> |
| <span data-ttu-id="dd20b-216">value</span><span class="sxs-lookup"><span data-stu-id="dd20b-216">value</span></span> |<span data-ttu-id="dd20b-217">Entrada independiente para cada registro en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="dd20b-217">Separate entry for each record in the search results.</span></span>  <span data-ttu-id="dd20b-218">Los detalles de la entrada coincidirán con las propiedades y los valores del registro.</span><span class="sxs-lookup"><span data-stu-id="dd20b-218">The details of the entry will match the properties and values of the record.</span></span> |

<span data-ttu-id="dd20b-219">Por ejemplo, el siguiente runbook podría extraer los registros devueltos por la búsqueda de registros y asignar propiedades diferentes según el tipo de cada registro.</span><span class="sxs-lookup"><span data-stu-id="dd20b-219">For example, the following runbook would extract the records returned by the log search  and assign different properties based on the type of each record.</span></span>  <span data-ttu-id="dd20b-220">Tenga en cuenta que el runbook se inicia mediante la conversión de **RequestBody** de json, por lo que puede actuar como un objeto de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd20b-220">Note that the runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="dd20b-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd20b-221">Next steps</span></span>
- <span data-ttu-id="dd20b-222">Complete un tutorial para [configurar un webhook](log-analytics-alerts-webhooks.md) con una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="dd20b-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="dd20b-223">Aprenda a escribir [runbooks en Automatización de Azure](https://azure.microsoft.com/documentation/services/automation) para solucionar los problemas identificados por las alertas.</span><span class="sxs-lookup"><span data-stu-id="dd20b-223">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>