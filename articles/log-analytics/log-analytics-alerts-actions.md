---
title: "aaaResponses tooalerts en análisis de registros de OMS | Documentos de Microsoft"
description: "Alertas de análisis de registros identificar información importante en el repositorio OMS y se pueden proactivamente avisarle de problemas o invocar acciones tooattempt toocorrect ellos.  Este artículo describe cómo toocreate una regla de alerta y las diferentes acciones de Hola de detalles que pueden tomar."
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
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="b5076-104">Agregue reglas de tooalert de acciones de análisis de registros</span><span class="sxs-lookup"><span data-stu-id="b5076-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="b5076-105">Cuando un [alerta se crea en el análisis de registros](log-analytics-alerts.md), tiene la opción de Hola de [configurar regla de alerta de hello](log-analytics-alerts.md) tooperform una o más acciones.</span><span class="sxs-lookup"><span data-stu-id="b5076-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="b5076-106">Este artículo describe hello las diferentes acciones que están disponibles y los detalles sobre la configuración de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="b5076-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="b5076-107">Acción</span><span class="sxs-lookup"><span data-stu-id="b5076-107">Action</span></span> | <span data-ttu-id="b5076-108">Descripción</span><span class="sxs-lookup"><span data-stu-id="b5076-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="b5076-109">Correo electrónico</span><span class="sxs-lookup"><span data-stu-id="b5076-109">Email</span></span>](#email-actions) | <span data-ttu-id="b5076-110">Enviar un correo electrónico con detalles de Hola de tooone alerta Hola o más destinatarios.</span><span class="sxs-lookup"><span data-stu-id="b5076-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="b5076-111">Webhook</span><span class="sxs-lookup"><span data-stu-id="b5076-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="b5076-112">Invoca un proceso externo a través de una sola solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="b5076-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="b5076-113">Runbook</span><span class="sxs-lookup"><span data-stu-id="b5076-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="b5076-114">Inicia un runbook en Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b5076-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="b5076-115">Acciones de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="b5076-115">Email actions</span></span>
<span data-ttu-id="b5076-116">Acciones de correo electrónico envíen un correo electrónico con los detalles de Hola de tooone alerta Hola o más destinatarios.</span><span class="sxs-lookup"><span data-stu-id="b5076-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="b5076-117">Puede especificar a asunto Hola de correo electrónico de hello, pero su contenido es un formato estándar que se construye mediante el análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="b5076-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="b5076-118">Incluye información de resumen, como nombre de Hola de alerta de hello toodetails de adición de registros de tooten devuelto por la búsqueda de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="b5076-119">También incluye una búsqueda de registros de vínculo tooa de análisis de registros que devolverá el conjunto completo de Hola de registros desde una consulta.</span><span class="sxs-lookup"><span data-stu-id="b5076-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="b5076-120">Hola remitente de correo electrónico de hello es *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="b5076-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="b5076-121">Acciones de correo electrónico requieren propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5076-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="b5076-122">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b5076-122">Property</span></span> | <span data-ttu-id="b5076-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="b5076-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b5076-124">Asunto</span><span class="sxs-lookup"><span data-stu-id="b5076-124">Subject</span></span> |<span data-ttu-id="b5076-125">Asunto de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-125">Subject in hello email.</span></span>  <span data-ttu-id="b5076-126">No se puede modificar el cuerpo de saludo del mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="b5076-127">Recipients</span><span class="sxs-lookup"><span data-stu-id="b5076-127">Recipients</span></span> |<span data-ttu-id="b5076-128">Direcciones de todos los destinatarios de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="b5076-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="b5076-129">Si especifica más de una dirección y, a continuación, direcciones de hello independiente con un punto y coma (;).</span><span class="sxs-lookup"><span data-stu-id="b5076-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="b5076-130">Acciones de webhook</span><span class="sxs-lookup"><span data-stu-id="b5076-130">Webhook actions</span></span>

<span data-ttu-id="b5076-131">Las acciones de Webhook permiten tooinvoke un proceso externo a través de una única solicitud HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="b5076-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="b5076-132">servicio de Hola que se llama debe admitir webhooks y determinar cómo va a utilizar cualquier carga recibe.</span><span class="sxs-lookup"><span data-stu-id="b5076-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="b5076-133">También puede llamar a una API de REST que no admiten específicamente webhooks siempre que sea de solicitud de hello en un formato que Hola que API entiende.</span><span class="sxs-lookup"><span data-stu-id="b5076-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="b5076-134">Ejemplos de uso de un webhook de alerta de tooan de respuesta envían un mensaje [Slack](http://slack.com) o crear un incidente en [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="b5076-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="b5076-135">Está disponible en un tutorial completo de creación de una regla de alerta con una demora de webhook toocall [Webhooks en las alertas de análisis de registros](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b5076-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="b5076-136">Acciones de Webhook requieren propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5076-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="b5076-137">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b5076-137">Property</span></span> | <span data-ttu-id="b5076-138">Descripción</span><span class="sxs-lookup"><span data-stu-id="b5076-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b5076-139">Dirección URL de Webhook</span><span class="sxs-lookup"><span data-stu-id="b5076-139">Webhook URL</span></span> |<span data-ttu-id="b5076-140">dirección URL de Hola de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="b5076-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="b5076-141">Carga de JSON personalizada</span><span class="sxs-lookup"><span data-stu-id="b5076-141">Custom JSON payload</span></span> |<span data-ttu-id="b5076-142">Carga personalizada toosend con hello webhook.</span><span class="sxs-lookup"><span data-stu-id="b5076-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="b5076-143">Consulte a continuación para más información.</span><span class="sxs-lookup"><span data-stu-id="b5076-143">See below for details.</span></span> |


<span data-ttu-id="b5076-144">Webhooks incluir una dirección URL y una carga con el formato JSON que es datos de hello envía toohello de servicio externo.</span><span class="sxs-lookup"><span data-stu-id="b5076-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="b5076-145">De forma predeterminada, carga Hola incluirá los valores de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5076-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="b5076-146">Puede elegir tooreplace esta carga con uno personalizado propio.</span><span class="sxs-lookup"><span data-stu-id="b5076-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="b5076-147">En ese caso se puede utilizar Hola variables de tabla de Hola para cada uno de hello parámetros tooinclude su valor en la carga útil personalizada.</span><span class="sxs-lookup"><span data-stu-id="b5076-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="b5076-148">Parámetro</span><span class="sxs-lookup"><span data-stu-id="b5076-148">Parameter</span></span> | <span data-ttu-id="b5076-149">Variable</span><span class="sxs-lookup"><span data-stu-id="b5076-149">Variable</span></span> | <span data-ttu-id="b5076-150">Descripción</span><span class="sxs-lookup"><span data-stu-id="b5076-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b5076-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="b5076-151">AlertRuleName</span></span> |<span data-ttu-id="b5076-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="b5076-152">#alertrulename</span></span> |<span data-ttu-id="b5076-153">Nombre de regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="b5076-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="b5076-154">AlertThresholdOperator</span></span> |<span data-ttu-id="b5076-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="b5076-155">#thresholdoperator</span></span> |<span data-ttu-id="b5076-156">Operador de umbral para la regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="b5076-157">*Mayor que* o *menor que*.</span><span class="sxs-lookup"><span data-stu-id="b5076-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="b5076-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="b5076-158">AlertThresholdValue</span></span> |<span data-ttu-id="b5076-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="b5076-159">#thresholdvalue</span></span> |<span data-ttu-id="b5076-160">Valor de umbral para la regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="b5076-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="b5076-161">LinkToSearchResults</span></span> |<span data-ttu-id="b5076-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="b5076-162">#linktosearchresults</span></span> |<span data-ttu-id="b5076-163">Vincule la búsqueda de registros de análisis de tooLog que devuelve registros de Hola de consulta de Hola que creó la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="b5076-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="b5076-164">ResultCount</span></span> |<span data-ttu-id="b5076-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="b5076-165">#searchresultcount</span></span> |<span data-ttu-id="b5076-166">Número de registros en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="b5076-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="b5076-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="b5076-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="b5076-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="b5076-169">Hora de finalización de la consulta de hello en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="b5076-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="b5076-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="b5076-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="b5076-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="b5076-171">#searchinterval</span></span> |<span data-ttu-id="b5076-172">Período de tiempo para la regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="b5076-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="b5076-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="b5076-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="b5076-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="b5076-175">Hora de inicio para consulta de hello en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="b5076-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="b5076-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="b5076-176">SearchQuery</span></span> |<span data-ttu-id="b5076-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="b5076-177">#searchquery</span></span> |<span data-ttu-id="b5076-178">Consulta de búsqueda de registro utilizado por la regla de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="b5076-179">SearchResults</span><span class="sxs-lookup"><span data-stu-id="b5076-179">SearchResults</span></span> |<span data-ttu-id="b5076-180">Consulte a continuación</span><span class="sxs-lookup"><span data-stu-id="b5076-180">See below</span></span> |<span data-ttu-id="b5076-181">Registros devueltos por la consulta de hello en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b5076-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="b5076-182">Limitado toohello 5.000 primeros registros.</span><span class="sxs-lookup"><span data-stu-id="b5076-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="b5076-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="b5076-183">WorkspaceID</span></span> |<span data-ttu-id="b5076-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="b5076-184">#workspaceid</span></span> |<span data-ttu-id="b5076-185">Identificador del área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="b5076-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="b5076-186">Por ejemplo, podría especificar Hola después carga personalizada que incluya un parámetro único denominado *texto*.</span><span class="sxs-lookup"><span data-stu-id="b5076-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="b5076-187">servicio de Hola que llama a este webhook podría esperarse este parámetro.</span><span class="sxs-lookup"><span data-stu-id="b5076-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="b5076-188">Esta carga en el ejemplo se resolvería toosomething como Hola siguientes cuando envía toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="b5076-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="b5076-189">resultados de la búsqueda de tooinclude en una carga personalizada, agregue Hola después de línea como una propiedad de nivel superior en la carga de json de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="b5076-190">Por ejemplo, una carga personalizada que incluye solo nombre de la alerta hello y resultados de la búsqueda de hello toocreate, podría utilizar Hola después.</span><span class="sxs-lookup"><span data-stu-id="b5076-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="b5076-191">Puede comenzar con un ejemplo completo de creación de un servicio externo en una regla de alerta con un toostart webhook [crear una acción de alerta webhook en análisis de registros de OMS toosend mensaje tooSlack](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b5076-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="b5076-192">Acciones de runbook</span><span class="sxs-lookup"><span data-stu-id="b5076-192">Runbook actions</span></span>
<span data-ttu-id="b5076-193">Las acciones de runbook inician un runbook en Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="b5076-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="b5076-194">En orden toouse para este tipo de acción, debe tener hello [solución de automatización](log-analytics-add-solutions.md) instalado y configurado en el área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="b5076-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="b5076-195">Puede seleccionar desde los runbooks de hello en la cuenta de automatización de Hola que configuró en hello solución de automatización.</span><span class="sxs-lookup"><span data-stu-id="b5076-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="b5076-196">Acciones de runbook requieren propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5076-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="b5076-197">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b5076-197">Property</span></span> | <span data-ttu-id="b5076-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="b5076-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="b5076-199">Runbook</span><span class="sxs-lookup"><span data-stu-id="b5076-199">Runbook</span></span> | <span data-ttu-id="b5076-200">Runbook que desea toostart cuando se crea una alerta.</span><span class="sxs-lookup"><span data-stu-id="b5076-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="b5076-201">Ejecutar en</span><span class="sxs-lookup"><span data-stu-id="b5076-201">Run on</span></span> | <span data-ttu-id="b5076-202">Especifique **Azure** toorun Hola runbook en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="b5076-203">Especifique **Hybrid worker** toorun Hola runbook en un agente con [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) instalado.</span><span class="sxs-lookup"><span data-stu-id="b5076-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="b5076-204">Acciones de runbook iniciar Hola runbook mediante una [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b5076-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="b5076-205">Cuando se crea la regla de alerta de hello, creará automáticamente un webhook nuevo runbook de hello con nombre hello **corrección de alerta de OMS** seguido de un GUID.</span><span class="sxs-lookup"><span data-stu-id="b5076-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="b5076-206">Directamente no se puede rellenar los parámetros de runbook de hello, pero Hola [$WebhookData parámetro](../automation/automation-webhooks.md) incluirá información de Hola de alerta de hello, incluidos los resultados de Hola Hola de búsqueda de registros que lo creó.</span><span class="sxs-lookup"><span data-stu-id="b5076-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="b5076-207">Hola runbook necesitará toodefine **$WebhookData** como un parámetro para el mismo tooaccess Hola propiedades de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="b5076-208">Hello datos de alertas están disponibles en formato de json en una propiedad única denominada **SearchResults** en hello **RequestBody** propiedad de **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="b5076-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="b5076-209">Esto tendrá con propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="b5076-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="b5076-210">Nodo</span><span class="sxs-lookup"><span data-stu-id="b5076-210">Node</span></span> | <span data-ttu-id="b5076-211">Descripción</span><span class="sxs-lookup"><span data-stu-id="b5076-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b5076-212">id</span><span class="sxs-lookup"><span data-stu-id="b5076-212">id</span></span> |<span data-ttu-id="b5076-213">Ruta de acceso y el GUID del programa Hola a buscan.</span><span class="sxs-lookup"><span data-stu-id="b5076-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="b5076-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="b5076-214">__metadata</span></span> |<span data-ttu-id="b5076-215">Información sobre Hola alerta incluidos Hola el número de registros y el estado de los resultados de la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="b5076-216">value</span><span class="sxs-lookup"><span data-stu-id="b5076-216">value</span></span> |<span data-ttu-id="b5076-217">Entrada separada para cada registro en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5076-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="b5076-218">detalles de Hola de entrada de hello coincidirá con propiedades de Hola y valores del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="b5076-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="b5076-219">Por ejemplo, hello runbook siguiente podría extraer registros de hello devueltos por la búsqueda de registros de Hola y asignar propiedades diferentes en función de tipo hello de cada registro.</span><span class="sxs-lookup"><span data-stu-id="b5076-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="b5076-220">Tenga en cuenta que runbook Hola se inicia mediante la conversión **RequestBody** de json, por lo que TI puede actuar como un objeto en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5076-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="b5076-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5076-221">Next steps</span></span>
- <span data-ttu-id="b5076-222">Complete un tutorial para [configurar un webhook](log-analytics-alerts-webhooks.md) con una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="b5076-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="b5076-223">Obtenga información acerca de cómo toowrite [runbooks en automatización de Azure](https://azure.microsoft.com/documentation/services/automation) problemas tooremediate identificados por las alertas.</span><span class="sxs-lookup"><span data-stu-id="b5076-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>
