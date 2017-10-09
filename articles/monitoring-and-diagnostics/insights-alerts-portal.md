---
title: 'aaaCreate alertas para los servicios de Azure: portal de Azure | Documentos de Microsoft'
description: "Desencadenador los correos electrónicos, notificaciones, llame a direcciones URL de sitios Web (webhooks), o la automatización cuando se cumplen las condiciones de Hola que especifique."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>Creación de alertas de métricas en Azure Monitor para servicios de Azure: Azure Portal
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Información general
Este artículo muestra cómo tooset las alertas de métrica Azure utilizando Hola portal de Azure.   

Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.

* **Valores de métrica** : hello desencadenadores de alerta cuando el valor Hola de una métrica especificada está fuera de un umbral asignar en cualquier dirección. Es decir, desencadena tanto cuando primero se cumple la condición de hello y, a continuación, después cuando la condición que ya no se cumple.    
* **Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos. más información acerca de las alertas de registro de actividad toolearn [haga clic aquí](monitoring-activity-log-alerts.md)

Puede configurar una métrica toodo alerta hello las siguientes cuando se desencadena:

* enviar el administrador del servicio de toohello de notificaciones de correo electrónico y coadministradores
* enviar correo electrónico mensajes de correo electrónico de tooadditional que especifique.
* Llamar a un webhook.
* iniciar la ejecución de un runbook de Azure (solo de Hola portal de Azure)

Puede obtener información sobre las reglas de alerta de métricas y configurarlas mediante:

* [Portal de Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [Interfaz de la línea de comandos (CLI)](insights-alerts-command-line-interface.md)
* [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Crear una regla de alerta en una métrica con hello portal de Azure
1. Hola [portal](https://portal.azure.com/), busque está interesado en la supervisión de recursos de Hola y selecciónelo.

2. Seleccione **alertas** o **reglas de alerta** en la sección supervisión de Hola. icono y texto hello pueden variar ligeramente para los distintos recursos.  

    ![Supervisión](./media/insights-alerts-portal/AlertRulesButton.png)

3. Seleccione hello **Agregar alerta** comando y rellene los campos de Hola.

    ![Agregar alerta](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. Asígnele un **nombre** a la regla de alerta y elija una **descripción**, que también se muestra los correos electrónicos de notificación.

5. Seleccione hello **métrica** desea toomonitor y después elija una **condición** y **umbral** valor de métrica de Hola. También elegido hello **período** de tiempo que Hola métrica regla debe cumplirse antes de desencadenadores de alerta de Hola. Por ejemplo, si usa el período de Hola "PT5M" y busca de la alerta de CPU superior al 80%, alerta de hello desencadena cuando Hola CPU ha estado anterior de forma coherente el 80% durante 5 minutos. Una vez que se produce el primer desencadenador que hello, desencadena nuevo cuando Hola CPU permanezca por debajo de 80% durante 5 minutos. Hola medida de CPU se produce cada 1 minuto.   

6. Comprobar **propietarios de correo electrónico...**  si desea que los administradores y coadministradores toobe por correo electrónico cuando Hola alerta se activa.

7. Si desea que los mensajes de correo electrónico adicionales tooreceive una notificación cuando hello alerta se desencadena, agregarlos en hello **email(s) Administrador adicional** campo. Separe las direcciones de correo electrónico con punto y coma, de la siguiente manera: *email@contoso.com;email2@contoso.com*

8. Colocar en un URI válido en hello **Webhook** campo si desea que se llama cuando Hola alerta se activa.

9. Si usas automatización de Azure, puede seleccionar una toobe Runbook ejecutar cuando se desencadene la alerta de Hola.

10. Seleccione **Aceptar** cuando toocreate done Hola alerta.   

Dentro de unos minutos, alerta de hello está activo y se desencadena como se describió anteriormente.

## <a name="managing-your-alerts"></a>Administración de las alertas
Una vez que haya creado una alerta, puede seleccionarla y:

* Ver un gráfico que muestra umbral de métrica de Hola y los valores reales de Hola Hola día anterior.
* Editar la alerta o eliminarla.
* **Deshabilitar** o **habilitar** si desea tootemporarily detener o reanudar la recepción de notificaciones de esa alerta.

## <a name="next-steps"></a>Pasos siguientes
* [Obtener una visión general de supervisión de Azure](monitoring-overview.md) incluidos Hola los tipos de información que puede recopilar y supervisar.
* Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).
* Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).
* Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).
* Obtenga [información general sobre los registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) para recopilar métricas detalladas de alta frecuencia sobre el servicio.
* Obtener un [información general de la colección de métricas](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.
