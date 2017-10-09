---
title: "aaaCalling un Runbook de automatización de Azure desde una alerta de análisis de registro | Documentos de Microsoft"
description: "Este artículo proporciona información general de cómo tooinvoke un runbook de automatización de una alerta de análisis de registros de OMS de Microsoft."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Llamada a un runbook de Azure Automation desde una alerta de Log Analytics de OMS

Cuando se configura una alerta de análisis de registros toocreate se produce un error en un registro de alertas si los resultados coinciden con un criterio determinado, como un aumento de la utilización del procesador o una funcionalidad de toohello críticos del proceso de aplicación concreta de una aplicación empresarial y escribe un evento correspondiente en el registro de eventos de Windows hello, esa alerta puede ejecutar automáticamente un runbook de automatización en un intento de tooauto-corregir el problema de Hola.  

Hay dos toocall opciones un runbook al configurar la alerta de Hola.  Concretamente, puede:

1. Usar un webhook.
   * Esto es Hola la única opción disponible si el área de trabajo OMS no está vinculado tooan cuenta de automatización.
   * Si ya tiene un área de trabajo OMS de automatización de la cuenta vinculada tooan, esta opción está disponible todavía.  

2. Seleccionar un runbook directamente.
   * Esta opción está disponible solo cuando el área de trabajo de hello OMS está vinculado tooan cuenta de automatización.  

## <a name="calling-a-runbook-using-a-webhook"></a>Llamada a un runbook con un webhook

Un webhook permite toostart un runbook determinado en la automatización de Azure a través de una única solicitud HTTP.  Antes de configurar hello [alerta de análisis de registros](../log-analytics/log-analytics-alerts.md#alert-rules) toocall Hola runbook mediante un webhook como una acción de alerta, deberá toofirst crear un webhook de runbook de Hola que se llamará con este método.  Revise y siga los pasos de Hola Hola [crear un webhook](automation-webhooks.md#creating-a-webhook) artículo y recordar la URL del webhook toorecord Hola para que pueda hacer referencia al configurar la regla de alerta de Hola.   

## <a name="calling-a-runbook-directly"></a>Llamada a runbook directamente

Si tienes Hola automatización & oferta Control instalado y configurado en el área de trabajo OMS, al configurar la opción de acciones de hello Runbook de alerta de hello, puede ver todos los runbooks de hello **seleccionar un runbook** lista desplegable y seleccione Hola runbook específico que desee toorun de alerta de toohello de respuesta.  Hola seleccionado runbook puede ejecutarse en un área de trabajo en la nube de Azure de Hola o en un runbook worker híbrido.  Cuando alerta Hola se crea mediante la opción del runbook hello, se creará un webhook de runbook de Hola.  Puede ver hello webhook si va toohello cuenta de automatización y navegue toohello webhook hoja de runbook de hello seleccionado.  Si elimina la alerta de hello, hello webhook no se elimina, pero usuario Hola puede eliminar el webhook Hola manualmente.  No es un problema si no se elimina el webhook hello, es simplemente un elemento huérfano que podría tener toobe elimina en orden toomaintain una cuenta de automatización organizada.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Características de un runbook (para ambas opciones)

Ambos métodos para llamar a Hola runbook de alerta de análisis de registros de hello tienen características de un comportamiento diferente que necesitan toobe entiende antes de configurar las reglas de alertas.  

* Debe tener un parámetro de entrada de runbook denominado **WebhookData** del tipo **Objeto**.  Esto puede ser obligatorio u opcional.  alerta de Hello pasa los resultados de búsqueda de hello toohello runbook con este parámetro de entrada.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  Debe tener el objeto de código tooconvert hello WebhookData tooa PowerShell.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* será una matriz de objetos; cada objeto contiene campos de hello con valores de un resultado de búsqueda

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData incoherencias entre la opción de webhook de Hola y opción de runbook

* Al configurar una alerta toocall un Webhook, escriba una dirección URL del webhook que creó para un runbook y haga clic en hello **Webhook prueba** botón.  Hello WebhookData resultante envía toohello runbook no contiene *. SearchResult* o *. SearchResults*.

*  Si guarda esa alerta cuando alerta Hola desencadena y llama a webhook hello, hello WebhookData envía runbook toohello contiene *. SearchResult*.
* Si crea una alerta y configurar toocall un runbook (que también crea un webhook), cuando Hola desencadenadores alerta envía WebhookData toohello runbook que contiene *. SearchResults*.

Por lo tanto en el ejemplo de código de hello anterior, será necesario tooget *. SearchResult* si alerta Hola llama a un webhook y deberá tooget *. SearchResults* si alerta Hola llama directamente a un runbook.

## <a name="example-walkthrough"></a>Tutorial de ejemplo

Demostraremos cómo funciona mediante el uso de hello después runbook gráfico de ejemplo, que inicia un servicio de Windows.<br><br> ![Runbook gráfico de inicio de servicio de Windows](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Hola runbook tiene un parámetro de entrada de tipo **objeto** que se llama **WebhookData** e incluye datos de webhook Hola pasados de alerta que contiene de hello *. SearchResults*.<br><br> ![Parámetros de entrada de Runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

En este ejemplo, en análisis de registros se crean dos campos personalizados, *SvcDisplayName_CF* y *SvcState_CF*, tooextract Hola mostrar hello y nombre del estado del servicio de servicio de hello (es decir, ejecución o detenido) desde el evento de hello escriben el registro de eventos del sistema de toohello.  A continuación, crearemos una regla de alerta con hello después de consulta de búsqueda: `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` para que se puede detectar cuándo Hola servicio cola de impresión se detiene en el sistema de Windows hello.  Puede ser cualquier servicio en cuestión, pero en este ejemplo hacemos referencia a uno de los servicios preexistente Hola que se incluyen con el sistema operativo Windows hello.  acción de alerta de Hello es tooexecute configurado nuestro runbook utilizado en este ejemplo y ejecutar en hello Hybrid Runbook Worker, cuáles están habilitadas en los sistemas de destino de Hola.   

Hola actividad de runbook código **obtener el nombre de servicio desde LA** convertirá la cadena con formato JSON de hello en un tipo de objeto y el filtro en el elemento de hello *SvcDisplayName_CF* tooextract nombre para mostrar hello de hello Servicio de Windows y pasar a la actividad siguiente hello que comprobará Hola servicio se detiene antes de intentar toorestart lo.  *SvcDisplayName_CF* es un [campo personalizado](../log-analytics/log-analytics-custom-fields.md) creado en el análisis de registros toodemonstrate en este ejemplo.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

Cuando se detiene el servicio de hello, regla de alerta de hello en análisis de registros detectará a una coincidencia y desencadenar runbook Hola y Hola contexto de alerta toohello runbook de envío. Hola runbook llevará a cabo acción tooverify Hola servicio se detiene, y si lo intento toorestart Hola servicio y compruebe si se inició correctamente y da como resultado Hola de salida.     

O bien si no tiene el área de trabajo OMS de automatización de la cuenta vinculada tooyour, configurar la regla de alerta de Hola a un runbook de webhook acción tootrigger Hola y configurar la cadena con formato JSON de hello runbook tooconvert hello y filtro en *. SearchResult* instrucciones Hola se ha mencionado anteriormente.    

## <a name="next-steps"></a>Pasos siguientes

* toolearn más información acerca de las alertas de análisis de registros y toocreate uno, vea [alertas en los análisis de registros](../log-analytics/log-analytics-alerts.md).

* Cómo ver runbooks tootrigger mediante un webhook de toounderstand [webhook de automatización de Azure](automation-webhooks.md).
