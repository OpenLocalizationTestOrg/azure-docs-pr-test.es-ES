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
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="8f330-103">Creación de alertas de métricas en Azure Monitor para servicios de Azure: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8f330-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f330-104">Portal</span><span class="sxs-lookup"><span data-stu-id="8f330-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="8f330-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f330-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="8f330-106">CLI</span><span class="sxs-lookup"><span data-stu-id="8f330-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="8f330-107">Información general</span><span class="sxs-lookup"><span data-stu-id="8f330-107">Overview</span></span>
<span data-ttu-id="8f330-108">Este artículo muestra cómo tooset las alertas de métrica Azure utilizando Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f330-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="8f330-109">Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="8f330-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="8f330-110">**Valores de métrica** : hello desencadenadores de alerta cuando el valor Hola de una métrica especificada está fuera de un umbral asignar en cualquier dirección.</span><span class="sxs-lookup"><span data-stu-id="8f330-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="8f330-111">Es decir, desencadena tanto cuando primero se cumple la condición de hello y, a continuación, después cuando la condición que ya no se cumple.</span><span class="sxs-lookup"><span data-stu-id="8f330-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="8f330-112">**Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos.</span><span class="sxs-lookup"><span data-stu-id="8f330-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="8f330-113">más información acerca de las alertas de registro de actividad toolearn [haga clic aquí](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="8f330-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="8f330-114">Puede configurar una métrica toodo alerta hello las siguientes cuando se desencadena:</span><span class="sxs-lookup"><span data-stu-id="8f330-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="8f330-115">enviar el administrador del servicio de toohello de notificaciones de correo electrónico y coadministradores</span><span class="sxs-lookup"><span data-stu-id="8f330-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="8f330-116">enviar correo electrónico mensajes de correo electrónico de tooadditional que especifique.</span><span class="sxs-lookup"><span data-stu-id="8f330-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="8f330-117">Llamar a un webhook.</span><span class="sxs-lookup"><span data-stu-id="8f330-117">call a webhook</span></span>
* <span data-ttu-id="8f330-118">iniciar la ejecución de un runbook de Azure (solo de Hola portal de Azure)</span><span class="sxs-lookup"><span data-stu-id="8f330-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="8f330-119">Puede obtener información sobre las reglas de alerta de métricas y configurarlas mediante:</span><span class="sxs-lookup"><span data-stu-id="8f330-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="8f330-120">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8f330-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="8f330-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f330-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="8f330-122">Interfaz de la línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="8f330-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="8f330-123">API de REST de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="8f330-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="8f330-124">Crear una regla de alerta en una métrica con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8f330-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="8f330-125">Hola [portal](https://portal.azure.com/), busque está interesado en la supervisión de recursos de Hola y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="8f330-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="8f330-126">Seleccione **alertas** o **reglas de alerta** en la sección supervisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f330-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="8f330-127">icono y texto hello pueden variar ligeramente para los distintos recursos.</span><span class="sxs-lookup"><span data-stu-id="8f330-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![Supervisión](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="8f330-129">Seleccione hello **Agregar alerta** comando y rellene los campos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f330-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Agregar alerta](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="8f330-131">Asígnele un **nombre** a la regla de alerta y elija una **descripción**, que también se muestra los correos electrónicos de notificación.</span><span class="sxs-lookup"><span data-stu-id="8f330-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="8f330-132">Seleccione hello **métrica** desea toomonitor y después elija una **condición** y **umbral** valor de métrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f330-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="8f330-133">También elegido hello **período** de tiempo que Hola métrica regla debe cumplirse antes de desencadenadores de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f330-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="8f330-134">Por ejemplo, si usa el período de Hola "PT5M" y busca de la alerta de CPU superior al 80%, alerta de hello desencadena cuando Hola CPU ha estado anterior de forma coherente el 80% durante 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="8f330-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="8f330-135">Una vez que se produce el primer desencadenador que hello, desencadena nuevo cuando Hola CPU permanezca por debajo de 80% durante 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="8f330-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="8f330-136">Hola medida de CPU se produce cada 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="8f330-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="8f330-137">Comprobar **propietarios de correo electrónico...**  si desea que los administradores y coadministradores toobe por correo electrónico cuando Hola alerta se activa.</span><span class="sxs-lookup"><span data-stu-id="8f330-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="8f330-138">Si desea que los mensajes de correo electrónico adicionales tooreceive una notificación cuando hello alerta se desencadena, agregarlos en hello **email(s) Administrador adicional** campo.</span><span class="sxs-lookup"><span data-stu-id="8f330-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="8f330-139">Separe las direcciones de correo electrónico con punto y coma, de la siguiente manera: *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="8f330-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="8f330-140">Colocar en un URI válido en hello **Webhook** campo si desea que se llama cuando Hola alerta se activa.</span><span class="sxs-lookup"><span data-stu-id="8f330-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="8f330-141">Si usas automatización de Azure, puede seleccionar una toobe Runbook ejecutar cuando se desencadene la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f330-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="8f330-142">Seleccione **Aceptar** cuando toocreate done Hola alerta.</span><span class="sxs-lookup"><span data-stu-id="8f330-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="8f330-143">Dentro de unos minutos, alerta de hello está activo y se desencadena como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8f330-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="8f330-144">Administración de las alertas</span><span class="sxs-lookup"><span data-stu-id="8f330-144">Managing your alerts</span></span>
<span data-ttu-id="8f330-145">Una vez que haya creado una alerta, puede seleccionarla y:</span><span class="sxs-lookup"><span data-stu-id="8f330-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="8f330-146">Ver un gráfico que muestra umbral de métrica de Hola y los valores reales de Hola Hola día anterior.</span><span class="sxs-lookup"><span data-stu-id="8f330-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="8f330-147">Editar la alerta o eliminarla.</span><span class="sxs-lookup"><span data-stu-id="8f330-147">Edit or delete it.</span></span>
* <span data-ttu-id="8f330-148">**Deshabilitar** o **habilitar** si desea tootemporarily detener o reanudar la recepción de notificaciones de esa alerta.</span><span class="sxs-lookup"><span data-stu-id="8f330-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f330-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f330-149">Next steps</span></span>
* <span data-ttu-id="8f330-150">[Obtener una visión general de supervisión de Azure](monitoring-overview.md) incluidos Hola los tipos de información que puede recopilar y supervisar.</span><span class="sxs-lookup"><span data-stu-id="8f330-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="8f330-151">Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8f330-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="8f330-152">Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8f330-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="8f330-153">Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="8f330-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="8f330-154">Obtenga [información general sobre los registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) para recopilar métricas detalladas de alta frecuencia sobre el servicio.</span><span class="sxs-lookup"><span data-stu-id="8f330-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="8f330-155">Obtener un [información general de la colección de métricas](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="8f330-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
