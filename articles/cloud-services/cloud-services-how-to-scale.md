---
title: "aaaAuto escalar un servicio de nube en el portal clásico de hello | Documentos de Microsoft"
description: "(clásico) Obtenga información acerca de cómo toouse Hola tooconfigure portal clásico reglas de escalado automático para un rol web de servicio de nube o el rol de trabajo en Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="bd29c-103">Cómo tooconfigure Autoescala para un servicio de nube en el portal clásico de Hola</span><span class="sxs-lookup"><span data-stu-id="bd29c-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd29c-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bd29c-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="bd29c-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="bd29c-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="bd29c-106">En página de escala de Hola de hello portal de Azure clásico, puede configurar la configuración de escalado automático para el rol web o el rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bd29c-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="bd29c-107">También puede configurar el escalado manual en lugar del escalado automático basado en reglas.</span><span class="sxs-lookup"><span data-stu-id="bd29c-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="bd29c-108">Este artículo se centra en los roles de trabajo y en los roles web de Servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bd29c-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="bd29c-109">Al crear una máquina virtual (clásica) directamente, esta se hospeda en un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bd29c-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="bd29c-110">Parte de esta información se aplica tipos de toothese de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd29c-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="bd29c-111">Ajuste de escala en un conjunto de disponibilidad de máquinas virtuales es simplemente va a cerrar ellos activar y desactivar en función de las reglas de la escala de Hola que configure.</span><span class="sxs-lookup"><span data-stu-id="bd29c-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="bd29c-112">Para obtener más información sobre máquinas virtuales y los conjuntos de disponibilidad, consulte [administrar Hola disponibilidad de máquinas virtuales](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bd29c-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="bd29c-113">Debe considerar Hola siguiente información antes de configurar el escalado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="bd29c-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="bd29c-114">El uso de núcleos afecta el escalado.</span><span class="sxs-lookup"><span data-stu-id="bd29c-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="bd29c-115">Las instancias de rol más grandes usan más núcleos.</span><span class="sxs-lookup"><span data-stu-id="bd29c-115">Larger role instances use more cores.</span></span> <span data-ttu-id="bd29c-116">Puede escalar una aplicación solo en el límite de Hola de núcleos de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="bd29c-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="bd29c-117">Por ejemplo, supongamos que su suscripción tiene un límite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="bd29c-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="bd29c-118">Si ejecuta una aplicación con dos servicios en la nube de tamaño mediano (un total de 4 núcleos), solo puede aumentar otras implementaciones de servicio de nube en su suscripción por restantes 16 núcleos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd29c-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="bd29c-119">Para obtener más información sobre los tamaños, consulte [Tamaños de los servicios en la nube](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="bd29c-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="bd29c-120">Debe crear una cola y asociarla con un rol para poder escalar una aplicación según el umbral de un mensaje.</span><span class="sxs-lookup"><span data-stu-id="bd29c-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="bd29c-121">Para obtener más información, consulte [cómo toouse Hola servicio de almacenamiento cola](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="bd29c-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="bd29c-122">Puede escalar los recursos que están vinculado tooyour servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bd29c-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="bd29c-123">Para obtener más información acerca de la vinculación de recursos, consulte [Cómo: vincular un servicio de nube de recursos tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="bd29c-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="bd29c-124">tooenable alta disponibilidad de la aplicación, debe asegurarse de que se implementa con dos o más instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="bd29c-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="bd29c-125">Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="bd29c-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="bd29c-126">Programar escalado</span><span class="sxs-lookup"><span data-stu-id="bd29c-126">Schedule scaling</span></span>
<span data-ttu-id="bd29c-127">De forma predeterminada, todos los roles no siguen una programación específica.</span><span class="sxs-lookup"><span data-stu-id="bd29c-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="bd29c-128">Por lo tanto, de aplicarse cualquier configuración cambiado tooall veces y todos los días a lo largo del año de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd29c-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="bd29c-129">Si lo desea, puede configurar el ajuste de escala manual o automática para uno de los siguientes modos de hello:</span><span class="sxs-lookup"><span data-stu-id="bd29c-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="bd29c-130">Días laborables</span><span class="sxs-lookup"><span data-stu-id="bd29c-130">Weekdays</span></span>
* <span data-ttu-id="bd29c-131">Fines de semana</span><span class="sxs-lookup"><span data-stu-id="bd29c-131">Weekends</span></span>
* <span data-ttu-id="bd29c-132">Noches entre semana</span><span class="sxs-lookup"><span data-stu-id="bd29c-132">Week nights</span></span>
* <span data-ttu-id="bd29c-133">Mañanas entre semana</span><span class="sxs-lookup"><span data-stu-id="bd29c-133">Week mornings</span></span>
* <span data-ttu-id="bd29c-134">Fechas específicas</span><span class="sxs-lookup"><span data-stu-id="bd29c-134">Specific dates</span></span>
* <span data-ttu-id="bd29c-135">Intervalos de fechas específicas</span><span class="sxs-lookup"><span data-stu-id="bd29c-135">Specific date ranges</span></span>

<span data-ttu-id="bd29c-136">Hello programación se establece en hello [portal de Azure clásico](https://manage.windowsazure.com/) en hello</span><span class="sxs-lookup"><span data-stu-id="bd29c-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="bd29c-137">**Cloud Services** > **\[Su servicio en la nube\]** > **Escala** > **\[Producción y almacenamiento provisional\]**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="bd29c-138">Haga clic en hello **configurar horas de programación** botón para cada rol que desee toochange.</span><span class="sxs-lookup"><span data-stu-id="bd29c-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Escalado automático en un servicio en la nube basado en una programación][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="bd29c-140">Escala manual</span><span class="sxs-lookup"><span data-stu-id="bd29c-140">Manual scale</span></span>
<span data-ttu-id="bd29c-141">En hello **escala** página, puede manualmente aumentar o reducir el número de Hola de instancias en ejecución en un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="bd29c-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="bd29c-142">Esta opción se configura para cada programación que haya creado o un tiempo de tooall si no ha creado una programación.</span><span class="sxs-lookup"><span data-stu-id="bd29c-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="bd29c-143">Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.</span><span class="sxs-lookup"><span data-stu-id="bd29c-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bd29c-144">Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="bd29c-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="bd29c-145">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-145">Click **Scale**.</span></span>
3. <span data-ttu-id="bd29c-146">Seleccione la programación de hello desea toochange opciones para de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd29c-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="bd29c-147">*Ya no las horas programadas* es predeterminado de hello si no tienes ninguna programación definida.</span><span class="sxs-lookup"><span data-stu-id="bd29c-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="bd29c-148">Buscar hello **escalar por métrica** sección y seleccione **NONE**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="bd29c-149">Este valor es el predeterminado de Hola para todos los roles.</span><span class="sxs-lookup"><span data-stu-id="bd29c-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="bd29c-150">Cada función hello del servicio en nube tiene un control deslizante para cambiar el número de Hola de toouse de instancias.</span><span class="sxs-lookup"><span data-stu-id="bd29c-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Escalar manualmente un rol de servicio en la nube][manual_scale]
   
    <span data-ttu-id="bd29c-152">Si tiene varias instancias, puede que tenga hello toochange [tamaño de máquina virtual de servicio de nube](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="bd29c-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="bd29c-153">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-153">Click **Save**.</span></span>  
   <span data-ttu-id="bd29c-154">Las instancias de rol se agregan o quitan según las selecciones realizadas.</span><span class="sxs-lookup"><span data-stu-id="bd29c-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="bd29c-155">Siempre que vea ![][tip_icon] mover su tooit de mouse (ratón) y también puede obtener ayuda acerca de una configuración específica de qué hace.</span><span class="sxs-lookup"><span data-stu-id="bd29c-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="bd29c-156">Escala automática: CPU</span><span class="sxs-lookup"><span data-stu-id="bd29c-156">Automatic scale - CPU</span></span>
<span data-ttu-id="bd29c-157">Este modo de escala si deja de porcentaje medio de hello del uso de CPU por encima o por debajo de los umbrales especificados.</span><span class="sxs-lookup"><span data-stu-id="bd29c-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="bd29c-158">Las instancias de rol se crean o eliminan cuando esto ocurre.</span><span class="sxs-lookup"><span data-stu-id="bd29c-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="bd29c-159">Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.</span><span class="sxs-lookup"><span data-stu-id="bd29c-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bd29c-160">Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="bd29c-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="bd29c-161">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-161">Click **Scale**.</span></span>
3. <span data-ttu-id="bd29c-162">Seleccione la programación de hello desea toochange opciones para de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd29c-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="bd29c-163">*Ya no las horas programadas* es predeterminado de hello si no tienes ninguna programación definida.</span><span class="sxs-lookup"><span data-stu-id="bd29c-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="bd29c-164">Buscar hello **escalar por métrica** sección y seleccione **CPU**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="bd29c-165">Ahora puede configurar un intervalo mínimo y máximo de instancias de roles, el uso de CPU de destino de hello (tootrigger una ampliación vertical) y cuántas instancias tooscale hacia arriba y hacia abajo por.</span><span class="sxs-lookup"><span data-stu-id="bd29c-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Escalar un rol de servicio en la nube con la carga de la CPU][cpu_scale]

> [!TIP]
> <span data-ttu-id="bd29c-167">Siempre que vea ![][tip_icon] mover su tooit de mouse (ratón) y también puede obtener ayuda acerca de una configuración específica de qué hace.</span><span class="sxs-lookup"><span data-stu-id="bd29c-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="bd29c-168">Escala automática: Cola</span><span class="sxs-lookup"><span data-stu-id="bd29c-168">Automatic scale - Queue</span></span>
<span data-ttu-id="bd29c-169">Este modo se escala automáticamente si número Hola de mensajes en una cola pasa por encima o por debajo del umbral especificado.</span><span class="sxs-lookup"><span data-stu-id="bd29c-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="bd29c-170">Las instancias de rol se crean o eliminan cuando esto ocurre.</span><span class="sxs-lookup"><span data-stu-id="bd29c-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="bd29c-171">Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.</span><span class="sxs-lookup"><span data-stu-id="bd29c-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bd29c-172">Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="bd29c-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="bd29c-173">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-173">Click **Scale**.</span></span>
3. <span data-ttu-id="bd29c-174">Buscar hello **escalar por métrica** sección y seleccione **cola**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="bd29c-175">Ahora puede configurar un intervalo mínimo y máximo de instancias de roles, cola de Hola y el número de cola mensajes tooprocess para cada instancia y cuántos tooscale de instancias avanzar y retroceder por.</span><span class="sxs-lookup"><span data-stu-id="bd29c-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![Escalar un rol de servicio en la nube con una cola de mensajes][queue_scale]

> [!TIP]
> <span data-ttu-id="bd29c-177">Siempre que vea ![][tip_icon] mover su tooit de mouse (ratón) y también puede obtener ayuda acerca de una configuración específica de qué hace.</span><span class="sxs-lookup"><span data-stu-id="bd29c-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="bd29c-178">Escalado de recursos vinculados</span><span class="sxs-lookup"><span data-stu-id="bd29c-178">Scale linked resources</span></span>
<span data-ttu-id="bd29c-179">A menudo, cuando escalar un rol, es la base de datos de Hola de tooscale beneficioso aplicación hello usa también.</span><span class="sxs-lookup"><span data-stu-id="bd29c-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="bd29c-180">Si vincula el servicio en la nube toohello Hola base de datos, puede tener acceso a Hola ajuste de escala en configuración para ese recurso haciendo clic en el vínculo apropiado de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd29c-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="bd29c-181">Hola [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **servicios en la nube**y, a continuación, haga clic en nombre de Hola Hola nube tooopen Hola de panel de servicio.</span><span class="sxs-lookup"><span data-stu-id="bd29c-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bd29c-182">Si no ve el servicio en la nube, puede que necesite toochange de **producción** demasiado**ensayo** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="bd29c-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="bd29c-183">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-183">Click **Scale**.</span></span>
3. <span data-ttu-id="bd29c-184">Buscar hello **recursos vinculados** sección y haga clic en **administrar el escalado de esta base de datos**.</span><span class="sxs-lookup"><span data-stu-id="bd29c-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bd29c-185">Si no ve la sección **recursos vinculados** , probablemente no tenga ningún recurso vinculado.</span><span class="sxs-lookup"><span data-stu-id="bd29c-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
