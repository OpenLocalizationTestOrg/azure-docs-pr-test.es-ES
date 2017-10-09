---
title: "ejemplo de acción de alerta de aaaWebhook en análisis de registros de OMS | Documentos de Microsoft"
description: "Uno se puede ejecutar en tooa de respuesta es alerta de análisis de registros de acciones de hello un * webhook *, lo que permite tooinvoke un proceso externo a través de una única solicitud HTTP. En este artículo, le guiaremos por un ejemplo en el que se creará una acción de webhook en una alerta de Log Analytics con Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="3a79e-104">Crear una acción de alerta webhook en análisis de registros de OMS toosend mensaje tooSlack</span><span class="sxs-lookup"><span data-stu-id="3a79e-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="3a79e-105">Uno de acciones de hello puede ejecutar en respuesta tooa [alerta de análisis de registros](log-analytics-alerts.md) es un *webhook*, lo cual permite hacer tooinvoke un proceso externo a través de una única solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a79e-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="3a79e-106">En [Alerts in Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="3a79e-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="3a79e-107">En este artículo, le guiaremos por un ejemplo en el que se creará una acción de webhook en una alerta de Log Analytics con Slack, que es un servicio de mensajería.</span><span class="sxs-lookup"><span data-stu-id="3a79e-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="3a79e-108">Debe tener una cuenta de Slack toocomplete en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3a79e-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="3a79e-109">Puede registrarse para obtener una cuenta gratuita en [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="3a79e-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="3a79e-110">Paso 1: habilitar webhooks en Slack</span><span class="sxs-lookup"><span data-stu-id="3a79e-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="3a79e-111">Inicie sesión en tooSlack en [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="3a79e-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="3a79e-112">Seleccione un canal en hello **canales** sección en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a79e-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="3a79e-113">Éste es el canal de hello ese mensaje Hola se enviarán a.</span><span class="sxs-lookup"><span data-stu-id="3a79e-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="3a79e-114">Puede seleccionar uno de los canales de hello predeterminado como **general** o **aleatorio**.</span><span class="sxs-lookup"><span data-stu-id="3a79e-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="3a79e-115">En un escenario de producción, probablemente crearía un canal especial, como **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="3a79e-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Canales de Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="3a79e-117">Haga clic en **agregar una aplicación o integración personalizados** tooopen Hola directorio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a79e-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="3a79e-118">Tipo de *webhooks* en el cuadro de búsqueda de hello y, a continuación, seleccione **WebHooks entrante**.</span><span class="sxs-lookup"><span data-stu-id="3a79e-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Canales de Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="3a79e-120">Haga clic en **instalar** siguiente nombre de equipo de tooyour.</span><span class="sxs-lookup"><span data-stu-id="3a79e-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="3a79e-121">Haga clic en **Add Configuration**(Agregar configuración).</span><span class="sxs-lookup"><span data-stu-id="3a79e-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="3a79e-122">Canal de Hola Hola SELECT que va a toouse para este ejemplo y, a continuación, haga clic en **WebHooks entrante agregar integración**.</span><span class="sxs-lookup"><span data-stu-id="3a79e-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="3a79e-123">Hola copia **URL del Webhook**.</span><span class="sxs-lookup"><span data-stu-id="3a79e-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="3a79e-124">Se pegará esto en configuración de alertas de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a79e-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Canales de Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="3a79e-126">Paso 2: crear una regla de alerta en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3a79e-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="3a79e-127">[Crear una regla de alerta](log-analytics-alerts.md) con hello después de la configuración.</span><span class="sxs-lookup"><span data-stu-id="3a79e-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="3a79e-128">Consulta: ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="3a79e-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="3a79e-129">Buscar esta alerta cada: 5 minutos</span><span class="sxs-lookup"><span data-stu-id="3a79e-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="3a79e-130">número de Hola de resultados es: mayor que 10</span><span class="sxs-lookup"><span data-stu-id="3a79e-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="3a79e-131">Durante este periodo de tiempo: 60 minutos</span><span class="sxs-lookup"><span data-stu-id="3a79e-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="3a79e-132">Seleccione **Sí** para **Webhook** y **n** para Hola otras acciones.</span><span class="sxs-lookup"><span data-stu-id="3a79e-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="3a79e-133">Hola pegar dirección URL de la demora en hello **URL del Webhook** campo.</span><span class="sxs-lookup"><span data-stu-id="3a79e-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="3a79e-134">Seleccione la opción de hello demasiado**incluyen una carga útil JSON personalizada**.</span><span class="sxs-lookup"><span data-stu-id="3a79e-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="3a79e-135">Slack espera una carga con formato JSON y con un parámetro denominado *text*,</span><span class="sxs-lookup"><span data-stu-id="3a79e-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="3a79e-136">Esto es texto hello que se mostrará en el mensaje de bienvenida que crea.</span><span class="sxs-lookup"><span data-stu-id="3a79e-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="3a79e-137">Puede usar uno o varios de los parámetros de alerta de hello mediante hello  *#*  de símbolos, como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a79e-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![carga JSON de ejemplo](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="3a79e-139">Haga clic en **guardar** regla de alerta de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="3a79e-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="3a79e-140">Esperar un tiempo suficiente para una alerta toobe creado y, a continuación, busque demora un mensaje que será similar siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="3a79e-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![webhook de ejemplo en Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="3a79e-142">Carga de webhook avanzada para Slack</span><span class="sxs-lookup"><span data-stu-id="3a79e-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="3a79e-143">Los mensajes entrantes se pueden personalizar completamente con Slack.</span><span class="sxs-lookup"><span data-stu-id="3a79e-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="3a79e-144">Para obtener más información, consulte [Webhooks entrante](https://api.slack.com/incoming-webhooks) en el sitio Web de demora de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a79e-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="3a79e-145">Aquí te mostramos un toocreate de carga un mensaje con formato enriquecido más compleja:</span><span class="sxs-lookup"><span data-stu-id="3a79e-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="3a79e-146">Esto generaría un mensaje en demora siguiente toohello similar.</span><span class="sxs-lookup"><span data-stu-id="3a79e-146">This would generate a message in Slack similar toohello following.</span></span>

![mensaje de ejemplo en Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="3a79e-148">Resumen</span><span class="sxs-lookup"><span data-stu-id="3a79e-148">Summary</span></span>
<span data-ttu-id="3a79e-149">Con esta regla de alerta en su lugar, tendría un mensaje enviado tooSlack cada vez que se cumplen los criterios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a79e-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="3a79e-150">Esto es sólo un ejemplo de una acción que se puede crear en la alerta de tooan de respuesta.</span><span class="sxs-lookup"><span data-stu-id="3a79e-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="3a79e-151">Podría crear una acción de webhook que llama a otro servicio externo, un toostart de acción de runbook un runbook en automatización de Azure o un toosend de acción de correo electrónico un tooyourself de correo electrónico o de otros destinatarios.</span><span class="sxs-lookup"><span data-stu-id="3a79e-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="3a79e-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3a79e-152">Next Steps</span></span>
* <span data-ttu-id="3a79e-153">Conozca otras [acciones de alerta en Log Analytics](log-analytics-alerts-actions.md), incluidas otras acciones.</span><span class="sxs-lookup"><span data-stu-id="3a79e-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


