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
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="6d3dd-103">Creación de alertas de métricas en Azure Monitor para los servicios de Azure: CLI multiplataforma</span><span class="sxs-lookup"><span data-stu-id="6d3dd-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d3dd-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6d3dd-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="6d3dd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d3dd-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="6d3dd-106">CLI</span><span class="sxs-lookup"><span data-stu-id="6d3dd-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="6d3dd-107">Información general</span><span class="sxs-lookup"><span data-stu-id="6d3dd-107">Overview</span></span>
<span data-ttu-id="6d3dd-108">Este artículo muestra cómo tooset las alertas de métrica Azure utilizando Hola multiplataforma interfaz de línea de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="6d3dd-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="6d3dd-109">Monitor de Azure es Hola nuevo nombre lo que se conoce como "Azure Insights" hasta 25 de septiembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="6d3dd-110">Sin embargo, los espacios de nombres de hello y, por lo tanto, comandos de hello siguientes sigue sin contengan visión"Hola".</span><span class="sxs-lookup"><span data-stu-id="6d3dd-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="6d3dd-111">Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="6d3dd-112">**Valores de métrica** : hello desencadenadores de alerta cuando el valor Hola de una métrica especificada está fuera de un umbral asignar en cualquier dirección.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="6d3dd-113">Es decir, desencadena tanto cuando primero se cumple la condición de hello y, a continuación, después cuando la condición que ya no se cumple.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="6d3dd-114">**Eventos de registro de actividades**: una alerta puede desencadenarse con *cada* evento o solo cuando se producen ciertos eventos concretos.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="6d3dd-115">más información acerca de las alertas de registro de actividad toolearn [haga clic aquí](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6d3dd-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="6d3dd-116">Puede configurar una métrica toodo alerta hello las siguientes cuando se desencadena:</span><span class="sxs-lookup"><span data-stu-id="6d3dd-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="6d3dd-117">enviar el administrador del servicio de toohello de notificaciones de correo electrónico y coadministradores</span><span class="sxs-lookup"><span data-stu-id="6d3dd-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="6d3dd-118">enviar correo electrónico mensajes de correo electrónico de tooadditional que especifique.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="6d3dd-119">Llamar a un webhook.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-119">call a webhook</span></span>
* <span data-ttu-id="6d3dd-120">iniciar la ejecución de un runbook de Azure (solo de Hola portal de Azure en este momento)</span><span class="sxs-lookup"><span data-stu-id="6d3dd-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="6d3dd-121">Puede obtener información sobre las reglas de alerta de métricas y configurarlas mediante:</span><span class="sxs-lookup"><span data-stu-id="6d3dd-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="6d3dd-122">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6d3dd-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="6d3dd-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d3dd-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="6d3dd-124">Interfaz de la línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="6d3dd-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="6d3dd-125">API de REST de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="6d3dd-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="6d3dd-126">Siempre puede recibir ayuda para los comandos escribiendo un comando y poner - ayuda al final de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="6d3dd-127">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d3dd-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="6d3dd-128">Crear reglas de alerta mediante Hola CLI</span><span class="sxs-lookup"><span data-stu-id="6d3dd-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="6d3dd-129">Realizar los requisitos previos de Hola y tooAzure de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="6d3dd-130">Consulte los [ejemplos de CLI de Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6d3dd-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="6d3dd-131">En resumen, instalar Hola CLI y ejecutar estos comandos.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="6d3dd-132">Obtiene se registran en, muestran qué suscripción se está usando y preparación comandos de Azure Monitor toorun.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="6d3dd-133">las reglas existentes en un grupo de recursos, toolist usar hello siguiente formulario **lista de reglas de alertas de visión azure** *[opciones] &lt;grupo de recursos&gt;*</span><span class="sxs-lookup"><span data-stu-id="6d3dd-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="6d3dd-134">toocreate una regla, debe toohave varios fragmentos de información importantes en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="6d3dd-135">Hola **Id. de recurso** para el recurso de hello desea tooset una alerta para</span><span class="sxs-lookup"><span data-stu-id="6d3dd-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="6d3dd-136">Hola **definiciones de métrica** disponibles para dicho recurso</span><span class="sxs-lookup"><span data-stu-id="6d3dd-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="6d3dd-137">Hola tooget una manera de Id. de recurso es toouse Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="6d3dd-138">Suponiendo que ya se ha creado el recurso de hello, selecciónela en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="6d3dd-139">A continuación, en la hoja de hello siguiente, seleccione *propiedades* en hello *configuración* sección.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="6d3dd-140">Hola *Id. de recurso* es un campo en la hoja siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="6d3dd-141">Otra manera es hello toouse [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6d3dd-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="6d3dd-142">El siguiente es un ejemplo de identificador de recurso de una aplic. web:</span><span class="sxs-lookup"><span data-stu-id="6d3dd-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="6d3dd-143">una lista de métricas disponibles hello y las unidades de esas métricas para Hola de uso siguiente comando CLI, el ejemplo anterior de recursos Hola tooget:</span><span class="sxs-lookup"><span data-stu-id="6d3dd-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="6d3dd-144">*PT1M* es la granularidad de Hola de medida disponibles de hello (intervalos de 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="6d3dd-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="6d3dd-145">El uso de distintas granularidades le brinda opciones de métricas diferentes.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="6d3dd-146">toocreate una regla de alerta basada en la métrica, utilice un comando de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="6d3dd-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="6d3dd-147">**azure insights alerts rule metric set***[opciones] &lt;nombreRegla&gt;&lt;ubicación&gt;&lt;grupoRecursos&gt;&lt;tamañoVentana&gt;&lt;operador&gt;&lt;umbral&gt;&lt;idRecursoObjetivo&gt;&lt;nombreMétrica&gt;&lt;horaInserciónOperador&gt;*</span><span class="sxs-lookup"><span data-stu-id="6d3dd-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="6d3dd-148">Hola siguiendo el ejemplo se configura una alerta en un recurso de sitio web.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="6d3dd-149">desencadenadores de alerta de Hello siempre que sea coherente recibe todo el tráfico de 5 minutos y cuando no recibe ningún tipo de tráfico durante 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="6d3dd-150">toocreate webhook o enviar correo electrónico cuando se desencadene una alerta de métricas, en primer lugar crear correo electrónico de Hola o webhook.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="6d3dd-151">A continuación, crear reglas de hello inmediatamente después.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="6d3dd-152">No se puede asociar webhook o correos electrónicos con ya creado reglas con hello CLI.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="6d3dd-153">Observe una regla individual para comprobar que las alertas se crearon correctamente.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="6d3dd-154">reglas de toodelete, utilice un comando de formulario de hello:</span><span class="sxs-lookup"><span data-stu-id="6d3dd-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="6d3dd-155">**insights alerts rule delete** [opciones] &lt;grupoRecursos&gt;&lt;nombreRegla&gt;</span><span class="sxs-lookup"><span data-stu-id="6d3dd-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="6d3dd-156">Estos comandos eliminan reglas de Hola que creó anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="6d3dd-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d3dd-157">Next steps</span></span>
* <span data-ttu-id="6d3dd-158">[Obtener una visión general de supervisión de Azure](monitoring-overview.md) incluidos Hola los tipos de información que puede recopilar y supervisar.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="6d3dd-159">Obtenga más información sobre cómo [configurar webhooks en las alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6d3dd-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="6d3dd-160">Obtenga más información sobre la [configuración de alertas sobre los eventos de registro de actividad](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6d3dd-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="6d3dd-161">Obtenga más información sobre los [runbooks de Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="6d3dd-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="6d3dd-162">Obtener un [información general de recopilar registros de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detallada las métricas de alta frecuencia en su servicio.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="6d3dd-163">Obtener un [información general de la colección de métricas](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="6d3dd-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
