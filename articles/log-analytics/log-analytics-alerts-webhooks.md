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
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Crear una acción de alerta webhook en análisis de registros de OMS toosend mensaje tooSlack
Uno de acciones de hello puede ejecutar en respuesta tooa [alerta de análisis de registros](log-analytics-alerts.md) es un *webhook*, lo cual permite hacer tooinvoke un proceso externo a través de una única solicitud HTTP.  En [Alerts in Log Analytics](log-analytics-alerts.md)

En este artículo, le guiaremos por un ejemplo en el que se creará una acción de webhook en una alerta de Log Analytics con Slack, que es un servicio de mensajería.

> [!NOTE]
> Debe tener una cuenta de Slack toocomplete en este ejemplo.  Puede registrarse para obtener una cuenta gratuita en [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Paso 1: habilitar webhooks en Slack
1. Inicie sesión en tooSlack en [slack.com](http://slack.com).
2. Seleccione un canal en hello **canales** sección en el panel izquierdo de Hola.  Éste es el canal de hello ese mensaje Hola se enviarán a.  Puede seleccionar uno de los canales de hello predeterminado como **general** o **aleatorio**.  En un escenario de producción, probablemente crearía un canal especial, como **criticalservicealerts**. <br>
   
   ![Canales de Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Haga clic en **agregar una aplicación o integración personalizados** tooopen Hola directorio de aplicación.
4. Tipo de *webhooks* en el cuadro de búsqueda de hello y, a continuación, seleccione **WebHooks entrante**. <br>
   
   ![Canales de Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Haga clic en **instalar** siguiente nombre de equipo de tooyour.
6. Haga clic en **Add Configuration**(Agregar configuración).
7. Canal de Hola Hola SELECT que va a toouse para este ejemplo y, a continuación, haga clic en **WebHooks entrante agregar integración**.  
8. Hola copia **URL del Webhook**.  Se pegará esto en configuración de alertas de Hola. <br>
   
    ![Canales de Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Paso 2: crear una regla de alerta en Log Analytics
1. [Crear una regla de alerta](log-analytics-alerts.md) con hello después de la configuración.
   * Consulta: ```    Type=Event EventLevelName=error ```
   * Buscar esta alerta cada: 5 minutos
   * número de Hola de resultados es: mayor que 10
   * Durante este periodo de tiempo: 60 minutos
   * Seleccione **Sí** para **Webhook** y **n** para Hola otras acciones.
2. Hola pegar dirección URL de la demora en hello **URL del Webhook** campo.
3. Seleccione la opción de hello demasiado**incluyen una carga útil JSON personalizada**.
4. Slack espera una carga con formato JSON y con un parámetro denominado *text*,  Esto es texto hello que se mostrará en el mensaje de bienvenida que crea.  Puede usar uno o varios de los parámetros de alerta de hello mediante hello  *#*  de símbolos, como en el siguiente ejemplo de Hola.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![carga JSON de ejemplo](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Haga clic en **guardar** regla de alerta de toosave Hola.
6. Esperar un tiempo suficiente para una alerta toobe creado y, a continuación, busque demora un mensaje que será similar siguiente toohello.
   
   ![webhook de ejemplo en Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Carga de webhook avanzada para Slack
Los mensajes entrantes se pueden personalizar completamente con Slack. Para obtener más información, consulte [Webhooks entrante](https://api.slack.com/incoming-webhooks) en el sitio Web de demora de Hola. Aquí te mostramos un toocreate de carga un mensaje con formato enriquecido más compleja:

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


Esto generaría un mensaje en demora siguiente toohello similar.

![mensaje de ejemplo en Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Resumen
Con esta regla de alerta en su lugar, tendría un mensaje enviado tooSlack cada vez que se cumplen los criterios de Hola.  

Esto es sólo un ejemplo de una acción que se puede crear en la alerta de tooan de respuesta.  Podría crear una acción de webhook que llama a otro servicio externo, un toostart de acción de runbook un runbook en automatización de Azure o un toosend de acción de correo electrónico un tooyourself de correo electrónico o de otros destinatarios.   

## <a name="next-steps"></a>Pasos siguientes
* Conozca otras [acciones de alerta en Log Analytics](log-analytics-alerts-actions.md), incluidas otras acciones.


