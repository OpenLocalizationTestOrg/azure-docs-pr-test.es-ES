---
title: "aaaGet iniciado con el escalado automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale el recurso de Azure."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="32564-103">Introducción al escalado automático en Azure</span><span class="sxs-lookup"><span data-stu-id="32564-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="32564-104">Este artículo se describe cómo tooset la configuración de escalado automático para el recurso en el portal de Microsoft Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="32564-105">Escalado automático de Monitor de Azure se aplica solo toovirtual conjuntos de escalas de máquina, servicios en la nube, planes de servicio de aplicaciones de Azure y los entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="32564-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="32564-106">Detectar la configuración de escalado automático de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="32564-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="32564-107">Puede detectar todos los recursos de hello para el que es aplicable en el Monitor de Azure de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="32564-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="32564-108">Usar hello siguiendo los pasos para ver un tutorial paso a paso:</span><span class="sxs-lookup"><span data-stu-id="32564-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="32564-109">Abra hello [portal de Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="32564-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="32564-110">Haga clic en el icono de Monitor de Azure de hello en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="32564-111">![Abrir Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="32564-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="32564-112">Haga clic en **escalado automático** tooview todos los recursos de hello para el escalado automático es aplicable, junto con su estado actual de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="32564-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="32564-113">![Detectar el escalado automático en Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="32564-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="32564-114">Puede usar el panel de filtro de Hola en hello tooscope superior hacia abajo tooselect recursos de lista de hello en un grupo de recursos específico, determinados tipos de recursos o un recurso específico.</span><span class="sxs-lookup"><span data-stu-id="32564-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="32564-115">Para cada recurso, encontrará el recuento de instancias actual de Hola y el estado de escalado automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="32564-116">Hola estado de escalado automático puede ser:</span><span class="sxs-lookup"><span data-stu-id="32564-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="32564-117">**No configurado**: aún no se ha habilitado el escalado automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="32564-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="32564-118">**Habilitado**: se ha habilitado el escalado automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="32564-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="32564-119">**Deshabilitado**: se ha deshabilitado el escalado automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="32564-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="32564-120">Creación de la primera configuración de escalado automático</span><span class="sxs-lookup"><span data-stu-id="32564-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="32564-121">Supongamos ahora, vaya a través de un tutorial paso a paso simple toocreate la primera configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="32564-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="32564-122">Abra hello **escalado automático** hoja en el Monitor de Azure y seleccione un recurso que desea tooscale.</span><span class="sxs-lookup"><span data-stu-id="32564-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="32564-123">(hello pasos siguientes utiliza un plan de servicio de aplicaciones asociado a una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="32564-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="32564-124">Puede [crear su primera aplicación web de ASP.NET en Azure en cinco minutos][4]).</span><span class="sxs-lookup"><span data-stu-id="32564-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="32564-125">Tenga en cuenta que el recuento de instancias actual de hello es 1.</span><span class="sxs-lookup"><span data-stu-id="32564-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="32564-126">Haga clic en **Enable autoscale** (Habilitar escalado automático).</span><span class="sxs-lookup"><span data-stu-id="32564-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="32564-127">![Configuración de escalado para la nueva aplicación web][5]</span><span class="sxs-lookup"><span data-stu-id="32564-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="32564-128">Proporcione un nombre para la configuración de escala de hello y, a continuación, haga clic en **agregar una regla de**.</span><span class="sxs-lookup"><span data-stu-id="32564-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="32564-129">Observe las opciones de regla de escala de Hola que abrir un panel de contexto en el lado derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="32564-130">De forma predeterminada, se establece la instancia de recuento en 1 si el porcentaje de CPU del recurso de Hola Hola supera el 70 por ciento de hello opción tooscale.</span><span class="sxs-lookup"><span data-stu-id="32564-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="32564-131">Deje los valores predeterminados y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="32564-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="32564-132">![Crear configuración de escalado para una aplicación web][6]</span><span class="sxs-lookup"><span data-stu-id="32564-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="32564-133">Ahora ha creado su primera regla de escalado.</span><span class="sxs-lookup"><span data-stu-id="32564-133">You've now created your first scale rule.</span></span> <span data-ttu-id="32564-134">Tenga en cuenta que Hola UX recomienda mejores prácticas e indica que "se recomienda toohave al menos una escala en la regla."</span><span class="sxs-lookup"><span data-stu-id="32564-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="32564-135">toodo para:</span><span class="sxs-lookup"><span data-stu-id="32564-135">toodo so:</span></span>
  
    <span data-ttu-id="32564-136">a.</span><span class="sxs-lookup"><span data-stu-id="32564-136">a.</span></span> <span data-ttu-id="32564-137">Haga clic en **Agregar una regla**.</span><span class="sxs-lookup"><span data-stu-id="32564-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="32564-138">b.</span><span class="sxs-lookup"><span data-stu-id="32564-138">b.</span></span> <span data-ttu-id="32564-139">Establecer **operador** demasiado**menor que**.</span><span class="sxs-lookup"><span data-stu-id="32564-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="32564-140">c.</span><span class="sxs-lookup"><span data-stu-id="32564-140">c.</span></span> <span data-ttu-id="32564-141">Establecer **umbral** demasiado**20**.</span><span class="sxs-lookup"><span data-stu-id="32564-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="32564-142">d.</span><span class="sxs-lookup"><span data-stu-id="32564-142">d.</span></span> <span data-ttu-id="32564-143">Establecer **operación** demasiado**disminuir el número por**.</span><span class="sxs-lookup"><span data-stu-id="32564-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="32564-144">Ahora debería tener una configuración de escalado que escale o reduzca horizontalmente en función del uso de CPU.</span><span class="sxs-lookup"><span data-stu-id="32564-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="32564-145">![Escala en función de la CPU][8]</span><span class="sxs-lookup"><span data-stu-id="32564-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="32564-146">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="32564-146">Click **Save**.</span></span>

<span data-ttu-id="32564-147">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="32564-147">Congratulations!</span></span> <span data-ttu-id="32564-148">Ahora que ha creado correctamente su primer tooautoscale de configuración de escala en función de la aplicación web de uso de CPU.</span><span class="sxs-lookup"><span data-stu-id="32564-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="32564-149">Hello mismos pasos son aplicable tooget a trabajar con una escala de máquinas virtuales en la nube o conjunto de rol de servicio.</span><span class="sxs-lookup"><span data-stu-id="32564-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="32564-150">Otras consideraciones</span><span class="sxs-lookup"><span data-stu-id="32564-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="32564-151">Escalación según una programación</span><span class="sxs-lookup"><span data-stu-id="32564-151">Scale based on a schedule</span></span>
<span data-ttu-id="32564-152">Además tooscale en función de la CPU, puede establecer la escala de manera diferente para determinados días de la semana de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="32564-153">Haga clic en **Add a scale condition** (Agregar una condición de escalado).</span><span class="sxs-lookup"><span data-stu-id="32564-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="32564-154">Configurar reglas de hello y modo de escala de hello es igual Hola como condición de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="32564-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="32564-155">Seleccione **repita días específicos** de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="32564-156">Seleccione los días de Hola y tiempo de inicio y fin de Hola para cuándo se debe aplicar la condición de la escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Condición de escalado basada en programación][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="32564-158">Escalado distinto en fechas concretas</span><span class="sxs-lookup"><span data-stu-id="32564-158">Scale differently on specific dates</span></span>
<span data-ttu-id="32564-159">Además tooscale en función de la CPU, puede establecer la escala de manera diferente para las fechas concretas.</span><span class="sxs-lookup"><span data-stu-id="32564-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="32564-160">Haga clic en **Add a scale condition** (Agregar una condición de escalado).</span><span class="sxs-lookup"><span data-stu-id="32564-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="32564-161">Configurar reglas de hello y modo de escala de hello es igual Hola como condición de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="32564-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="32564-162">Seleccione **especificar fechas de inicio y fin** de programación de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="32564-163">Seleccione las fechas de inicio y fin de Hola y la hora de inicio y fin de Hola para cuándo se debe aplicar la condición de la escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Condición de escalado basada en fechas][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="32564-165">Ver el historial de la escala de hello del recurso</span><span class="sxs-lookup"><span data-stu-id="32564-165">View hello scale history of your resource</span></span>
<span data-ttu-id="32564-166">Cada vez que el recurso se escala hacia arriba o hacia abajo, se registra un evento en el registro de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="32564-167">Puede ver historial de la escala de hello del recurso para hello las últimas 24 horas cambiando toohello **historial de ejecución** ficha.</span><span class="sxs-lookup"><span data-stu-id="32564-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![Historial de ejecuciones][11]

<span data-ttu-id="32564-169">Si desea que el historial de escala completa hello tooview (para una copia de seguridad too90 días), seleccione **haga clic aquí toosee detalles más**.</span><span class="sxs-lookup"><span data-stu-id="32564-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="32564-170">Abre el registro de actividad de Hello, con el escalado automático ya seleccionado para el recurso y la categoría.</span><span class="sxs-lookup"><span data-stu-id="32564-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="32564-171">Ver definición de la escala de hello del recurso</span><span class="sxs-lookup"><span data-stu-id="32564-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="32564-172">El escalado automático es un recurso de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="32564-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="32564-173">Puede ver la definición de la escala de hello en JSON cambiando toohello **JSON** ficha.</span><span class="sxs-lookup"><span data-stu-id="32564-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![Definición de escala][12]

<span data-ttu-id="32564-175">Puede realizar cambios en JSON directamente, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="32564-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="32564-176">Estos cambios se reflejarán después de guardarlos.</span><span class="sxs-lookup"><span data-stu-id="32564-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="32564-177">Deshabilitar el escalado automático y escalar manualmente las instancias</span><span class="sxs-lookup"><span data-stu-id="32564-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="32564-178">Puede haber ocasiones cuando desee toodisable la configuración de escala actual y escalar manualmente el recurso.</span><span class="sxs-lookup"><span data-stu-id="32564-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="32564-179">Haga clic en hello **deshabilitar escalado automático** situado en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="32564-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="32564-180">![Deshabilitar escalado automático][13]</span><span class="sxs-lookup"><span data-stu-id="32564-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="32564-181">Esta opción deshabilita su configuración.</span><span class="sxs-lookup"><span data-stu-id="32564-181">This option disables your configuration.</span></span> <span data-ttu-id="32564-182">Sin embargo, puede volver tooit después de habilitar el escalado automático nuevo.</span><span class="sxs-lookup"><span data-stu-id="32564-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="32564-183">Ahora puede establecer el número de Hola de instancias que desee tooscale toomanually.</span><span class="sxs-lookup"><span data-stu-id="32564-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![Definición manual de escalado][14]

<span data-ttu-id="32564-185">Siempre puede volver tooAutoscale haciendo clic en **habilita el escalado automático** y, a continuación, **guardar**.</span><span class="sxs-lookup"><span data-stu-id="32564-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32564-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32564-186">Next steps</span></span>
- [<span data-ttu-id="32564-187">Crear una alerta de registro de actividad toomonitor todas las operaciones de motor de escalado automático en su suscripción</span><span class="sxs-lookup"><span data-stu-id="32564-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="32564-188">Crear una alerta de registro de actividad toomonitor error en todos los operaciones de escala-escalabilidad de escalado automático en su suscripción</span><span class="sxs-lookup"><span data-stu-id="32564-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

