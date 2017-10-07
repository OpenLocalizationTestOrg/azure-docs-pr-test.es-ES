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
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Creación de alertas de métricas en Azure Monitor para servicios de Azure: PowerShell
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Información general
Este artículo muestra cómo tooset una métrica Azure alertas mediante PowerShell.  

Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.

* **Valores de métrica** : hello desencadenadores de alerta cuando el valor Hola de una métrica especificada está fuera de un umbral asignar en cualquier dirección. Es decir, desencadena tanto cuando primero se cumple la condición de hello y, a continuación, después cuando la condición que ya no se cumple.    
* **Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos. más información acerca de las alertas de registro de actividad toolearn [haga clic aquí](monitoring-activity-log-alerts.md)

Puede configurar una métrica toodo alerta hello las siguientes cuando se desencadena:

* enviar el administrador del servicio de toohello de notificaciones de correo electrónico y coadministradores
* enviar correo electrónico mensajes de correo electrónico de tooadditional que especifique.
* Llamar a un webhook.
* iniciar la ejecución de un runbook de Azure (solo de Hola portal de Azure)

Puede obtener información sobre las reglas de alerta y configurarlas mediante:

* [Portal de Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [Interfaz de la línea de comandos (CLI)](insights-alerts-command-line-interface.md)
* [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Para obtener información adicional, puede escribir siempre ```Get-Help``` y, a continuación, Hola desea obtener ayuda en el comando de PowerShell.

## <a name="create-alert-rules-in-powershell"></a>Creación de reglas de alerta en PowerShell
1. Inicie sesión en tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Obtener una lista de suscripciones de Hola que tiene disponible. Compruebe que está trabajando con suscripción derecho Hola. Si no es así, establezca toohello derecha con valores obtenidos hello en `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. las reglas de toolist existentes en un grupo de recursos, utilice Hola siguiente comando:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate una regla, debe toohave varios fragmentos de información importantes en primer lugar.

  * Hola **Id. de recurso** para el recurso de hello desea tooset una alerta para
  * Hola **definiciones de métrica** disponibles para dicho recurso

     Hola tooget una manera de Id. de recurso es toouse Hola portal de Azure. Suponiendo que ya se ha creado el recurso de hello, selecciónela en el portal de Hola. A continuación, en la hoja de hello siguiente, seleccione *propiedades* en hello *configuración* sección. **Id. de recurso** es un campo en la hoja siguiente Hola. Otra manera es hello toouse [Explorador de recursos de Azure](https://resources.azure.com/).

     Este es un ejemplo de identificador de recursos de una aplicación web:

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Puede usar `Get-AzureRmMetricDefinition` tooview lista de Hola de todas las definiciones métricas para un recurso concreto.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Hello en el ejemplo siguiente se genera una tabla con nombre de métrica de Hola y Hola unidad para esa métrica.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Ejecute Get-MetricDefinitions para obtener una lista completa de las opciones disponibles para Get-AzureRmMetricDefinition.
5. Hola siguiendo el ejemplo se configura una alerta en un recurso de sitio web. desencadenadores de alerta de Hello siempre que sea coherente recibe todo el tráfico de 5 minutos y cuando no recibe ningún tipo de tráfico durante 5 minutos.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate webhook o enviar correo electrónico cuando se desencadena una alerta, en primer lugar crear correo electrónico de Hola o webhook. A continuación, cree inmediatamente regla Hola posteriormente con Hola - etiqueta de acciones y como se muestra en el siguiente ejemplo de Hola. No puede asociar webhooks o correos electrónicos con reglas ya creadas mediante PowerShell.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify que se han creado correctamente las alertas echando un vistazo a reglas individuales Hola.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Elimine las alertas. Estos comandos eliminan reglas de Hola que creó anteriormente en este artículo.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Pasos siguientes
* [Obtener una visión general de supervisión de Azure](monitoring-overview.md) incluidos Hola los tipos de información que puede recopilar y supervisar.
* Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).
* Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).
* Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).
* Obtener un [información general de recopilar registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detallada las métricas de alta frecuencia en su servicio.
* Obtener un [información general de la colección de métricas](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.
