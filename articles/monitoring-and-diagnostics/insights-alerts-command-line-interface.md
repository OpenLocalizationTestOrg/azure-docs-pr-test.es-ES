---
title: aaaCreate alertas para los servicios de Azure - multiplataforma CLI | Documentos de Microsoft
description: "Desencadenador los correos electrónicos, notificaciones, llame a direcciones URL de sitios Web (webhooks), o la automatización cuando se cumplen las condiciones de Hola que especifique."
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
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a>Creación de alertas de métricas en Azure Monitor para los servicios de Azure: CLI multiplataforma
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Información general
Este artículo muestra cómo tooset las alertas de métrica Azure utilizando Hola multiplataforma interfaz de línea de comandos (CLI).

> [!NOTE]
> Monitor de Azure es Hola nuevo nombre lo que se conoce como "Azure Insights" hasta 25 de septiembre de 2016. Sin embargo, los espacios de nombres de hello y, por lo tanto, comandos de hello siguientes sigue sin contengan visión"Hola".
>
>

Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.

* **Valores de métrica** : hello desencadenadores de alerta cuando el valor Hola de una métrica especificada está fuera de un umbral asignar en cualquier dirección. Es decir, desencadena tanto cuando primero se cumple la condición de hello y, a continuación, después cuando la condición que ya no se cumple.    
* **Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos. más información acerca de las alertas de registro de actividad toolearn [haga clic aquí](monitoring-activity-log-alerts.md)

Puede configurar una métrica toodo alerta hello las siguientes cuando se desencadena:

* enviar el administrador del servicio de toohello de notificaciones de correo electrónico y coadministradores
* enviar correo electrónico mensajes de correo electrónico de tooadditional que especifique.
* Llamar a un webhook.
* iniciar la ejecución de un runbook de Azure (solo de Hola portal de Azure en este momento)

Puede obtener información sobre las reglas de alerta de métricas y configurarlas mediante:

* [Portal de Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [Interfaz de la línea de comandos (CLI)](insights-alerts-command-line-interface.md)
* [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Siempre puede recibir ayuda para los comandos escribiendo un comando y poner - ayuda al final de Hola. Por ejemplo:

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a>Crear reglas de alerta mediante Hola CLI
1. Realizar los requisitos previos de Hola y tooAzure de inicio de sesión. Consulte los [ejemplos de CLI de Azure Monitor](insights-cli-samples.md). En resumen, instalar Hola CLI y ejecutar estos comandos. Obtiene se registran en, muestran qué suscripción se está usando y preparación comandos de Azure Monitor toorun.

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. las reglas existentes en un grupo de recursos, toolist usar hello siguiente formulario **lista de reglas de alertas de visión azure** *[opciones] &lt;grupo de recursos&gt;*

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. toocreate una regla, debe toohave varios fragmentos de información importantes en primer lugar.
  * Hola **Id. de recurso** para el recurso de hello desea tooset una alerta para
  * Hola **definiciones de métrica** disponibles para dicho recurso

     Hola tooget una manera de Id. de recurso es toouse Hola portal de Azure. Suponiendo que ya se ha creado el recurso de hello, selecciónela en el portal de Hola. A continuación, en la hoja de hello siguiente, seleccione *propiedades* en hello *configuración* sección. Hola *Id. de recurso* es un campo en la hoja siguiente Hola. Otra manera es hello toouse [Explorador de recursos de Azure](https://resources.azure.com/).

     El siguiente es un ejemplo de identificador de recurso de una aplic. web:

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     una lista de métricas disponibles hello y las unidades de esas métricas para Hola de uso siguiente comando CLI, el ejemplo anterior de recursos Hola tooget:  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     *PT1M* es la granularidad de Hola de medida disponibles de hello (intervalos de 1 minuto). El uso de distintas granularidades le brinda opciones de métricas diferentes.
4. toocreate una regla de alerta basada en la métrica, utilice un comando de hello siguiendo el formato:

    **azure insights alerts rule metric set***[opciones] &lt;nombreRegla&gt;&lt;ubicación&gt;&lt;grupoRecursos&gt;&lt;tamañoVentana&gt;&lt;operador&gt;&lt;umbral&gt;&lt;idRecursoObjetivo&gt;&lt;nombreMétrica&gt;&lt;horaInserciónOperador&gt;*

    Hola siguiendo el ejemplo se configura una alerta en un recurso de sitio web. desencadenadores de alerta de Hello siempre que sea coherente recibe todo el tráfico de 5 minutos y cuando no recibe ningún tipo de tráfico durante 5 minutos.

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. toocreate webhook o enviar correo electrónico cuando se desencadene una alerta de métricas, en primer lugar crear correo electrónico de Hola o webhook. A continuación, crear reglas de hello inmediatamente después. No se puede asociar webhook o correos electrónicos con ya creado reglas con hello CLI.

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. Observe una regla individual para comprobar que las alertas se crearon correctamente.

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. reglas de toodelete, utilice un comando de formulario de hello:

    **insights alerts rule delete** [opciones] &lt;grupoRecursos&gt;&lt;nombreRegla&gt;

    Estos comandos eliminan reglas de Hola que creó anteriormente en este artículo.

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a>Pasos siguientes
* [Obtener una visión general de supervisión de Azure](monitoring-overview.md) incluidos Hola los tipos de información que puede recopilar y supervisar.
* Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).
* Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).
* Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).
* Obtener un [información general de recopilar registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detallada las métricas de alta frecuencia en su servicio.
* Obtener un [información general de la colección de métricas](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.
