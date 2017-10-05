---
title: "Escalado automático de un servicio en la nube en el portal clásico | Microsoft Docs"
description: "(clásico) Obtenga información sobre cómo usar el portal clásico para configurar reglas de escalado automático de un rol de trabajo o un rol web de servicio en la nube en Azure."
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
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="e4683-103">Configuración del escalado automático para un servicio en la nube en el portal clásico</span><span class="sxs-lookup"><span data-stu-id="e4683-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4683-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e4683-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="e4683-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e4683-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="e4683-106">En la página Escala del portal de Azure clásico, puede definir la configuración del escalado automático para el rol web o el rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e4683-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="e4683-107">También puede configurar el escalado manual en lugar del escalado automático basado en reglas.</span><span class="sxs-lookup"><span data-stu-id="e4683-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="e4683-108">Este artículo se centra en los roles de trabajo y en los roles web de Servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="e4683-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="e4683-109">Al crear una máquina virtual (clásica) directamente, esta se hospeda en un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="e4683-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="e4683-110">Parte de esta información se aplica a estos tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e4683-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="e4683-111">Escalar un conjunto de disponibilidad de máquinas virtuales consiste simplemente en encenderlas y apagarlas basándose en las reglas de escalado que configure.</span><span class="sxs-lookup"><span data-stu-id="e4683-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="e4683-112">Para más información sobre las máquinas virtuales y los conjuntos de disponibilidad, consulte [Administración de la disponibilidad de las máquinas virtuales](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e4683-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="e4683-113">Debe considerar la siguiente información antes de configurar el escalado para su aplicación:</span><span class="sxs-lookup"><span data-stu-id="e4683-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="e4683-114">El uso de núcleos afecta el escalado.</span><span class="sxs-lookup"><span data-stu-id="e4683-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="e4683-115">Las instancias de rol más grandes usan más núcleos.</span><span class="sxs-lookup"><span data-stu-id="e4683-115">Larger role instances use more cores.</span></span> <span data-ttu-id="e4683-116">Solo puede escalar una aplicación dentro del límite de núcleos para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="e4683-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="e4683-117">Por ejemplo, supongamos que su suscripción tiene un límite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="e4683-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="e4683-118">Si ejecuta una aplicación con dos servicios en la nube de tamaño mediano (un total de 4 núcleos), solo puede escalar verticalmente otras implementaciones del servicio en la nube en su suscripción con los 16 núcleos restantes.</span><span class="sxs-lookup"><span data-stu-id="e4683-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="e4683-119">Para obtener más información sobre los tamaños, consulte [Tamaños de los servicios en la nube](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="e4683-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="e4683-120">Debe crear una cola y asociarla con un rol para poder escalar una aplicación según el umbral de un mensaje.</span><span class="sxs-lookup"><span data-stu-id="e4683-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="e4683-121">Para obtener más información, consulte [Uso del servicio de almacenamiento de colas](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="e4683-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="e4683-122">Puede escalar los recursos que están vinculados con su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="e4683-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="e4683-123">Para obtener más información acerca de los recursos de vinculación, consulte [Vinculación de un recurso a un servicio en la nube](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="e4683-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="e4683-124">Para permitir una alta disponibilidad de la aplicación, debe asegurarse de que se implemente con dos o más instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="e4683-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="e4683-125">Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="e4683-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="e4683-126">Programar escalado</span><span class="sxs-lookup"><span data-stu-id="e4683-126">Schedule scaling</span></span>
<span data-ttu-id="e4683-127">De forma predeterminada, todos los roles no siguen una programación específica.</span><span class="sxs-lookup"><span data-stu-id="e4683-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="e4683-128">Por lo tanto, cualquier configuración modificada se aplica a cualquier hora y día durante todo el año.</span><span class="sxs-lookup"><span data-stu-id="e4683-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="e4683-129">Si quiere, puede configurar el escalado automático o manual para uno de los modos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e4683-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="e4683-130">Días laborables</span><span class="sxs-lookup"><span data-stu-id="e4683-130">Weekdays</span></span>
* <span data-ttu-id="e4683-131">Fines de semana</span><span class="sxs-lookup"><span data-stu-id="e4683-131">Weekends</span></span>
* <span data-ttu-id="e4683-132">Noches entre semana</span><span class="sxs-lookup"><span data-stu-id="e4683-132">Week nights</span></span>
* <span data-ttu-id="e4683-133">Mañanas entre semana</span><span class="sxs-lookup"><span data-stu-id="e4683-133">Week mornings</span></span>
* <span data-ttu-id="e4683-134">Fechas específicas</span><span class="sxs-lookup"><span data-stu-id="e4683-134">Specific dates</span></span>
* <span data-ttu-id="e4683-135">Intervalos de fechas específicas</span><span class="sxs-lookup"><span data-stu-id="e4683-135">Specific date ranges</span></span>

<span data-ttu-id="e4683-136">La opción de programación se configura en el [Portal de Azure clásico](https://manage.windowsazure.com/) en la página</span><span class="sxs-lookup"><span data-stu-id="e4683-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="e4683-137">**Cloud Services** > **\[Su servicio en la nube\]** > **Escala** > **\[Producción y almacenamiento provisional\]**.</span><span class="sxs-lookup"><span data-stu-id="e4683-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="e4683-138">Haga clic en el botón **Configurar horas de programación** para cada rol que quiera cambiar.</span><span class="sxs-lookup"><span data-stu-id="e4683-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![Escalado automático en un servicio en la nube basado en una programación][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="e4683-140">Escala manual</span><span class="sxs-lookup"><span data-stu-id="e4683-140">Manual scale</span></span>
<span data-ttu-id="e4683-141">En la página **Escala** , puede aumentar o disminuir manualmente la cantidad de instancias en ejecución en un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="e4683-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="e4683-142">Esta opción se configura para cada programación que haya creado o para todas si no ha creado una programación.</span><span class="sxs-lookup"><span data-stu-id="e4683-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="e4683-143">En el [Portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **Servicios en la nube**y, a continuación, haga clic en el nombre del servicio en la nube para abrir el panel.</span><span class="sxs-lookup"><span data-stu-id="e4683-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e4683-144">Si no ve el servicio en la nube, debe cambiar de **Producción** a **Almacenamiento provisional** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="e4683-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="e4683-145">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="e4683-145">Click **Scale**.</span></span>
3. <span data-ttu-id="e4683-146">Seleccione la programación en la que quiere cambiar las opciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="e4683-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="e4683-147">*No hay horas programadas* es el valor predeterminado si no dispone de ninguna programación definida.</span><span class="sxs-lookup"><span data-stu-id="e4683-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="e4683-148">Busque la sección **Escalar por métrica** y seleccione **NINGUNA**.</span><span class="sxs-lookup"><span data-stu-id="e4683-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="e4683-149">Esta es la configuración predeterminada de todos los roles.</span><span class="sxs-lookup"><span data-stu-id="e4683-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="e4683-150">Cada rol en el servicio en la nube tiene un control deslizante para cambiar la cantidad de instancias que se van a usar.</span><span class="sxs-lookup"><span data-stu-id="e4683-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![Escalar manualmente un rol de servicio en la nube][manual_scale]
   
    <span data-ttu-id="e4683-152">Si necesita más instancias, debe cambiar el [tamaño de la máquina virtual del servicio en la nube](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="e4683-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="e4683-153">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e4683-153">Click **Save**.</span></span>  
   <span data-ttu-id="e4683-154">Las instancias de rol se agregan o quitan según las selecciones realizadas.</span><span class="sxs-lookup"><span data-stu-id="e4683-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="e4683-155">Siempre que vea ![][tip_icon], mueva el mouse y podrá obtener ayuda acerca de lo que realiza una configuración específica.</span><span class="sxs-lookup"><span data-stu-id="e4683-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="e4683-156">Escala automática: CPU</span><span class="sxs-lookup"><span data-stu-id="e4683-156">Automatic scale - CPU</span></span>
<span data-ttu-id="e4683-157">Este modo escala si el porcentaje medio de uso de la CPU está por encima o por debajo de los umbrales especificados.</span><span class="sxs-lookup"><span data-stu-id="e4683-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="e4683-158">Las instancias de rol se crean o eliminan cuando esto ocurre.</span><span class="sxs-lookup"><span data-stu-id="e4683-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="e4683-159">En el [Portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **Servicios en la nube**y, a continuación, haga clic en el nombre del servicio en la nube para abrir el panel.</span><span class="sxs-lookup"><span data-stu-id="e4683-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e4683-160">Si no ve el servicio en la nube, debe cambiar de **Producción** a **Almacenamiento provisional** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="e4683-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="e4683-161">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="e4683-161">Click **Scale**.</span></span>
3. <span data-ttu-id="e4683-162">Seleccione la programación en la que quiere cambiar las opciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="e4683-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="e4683-163">*No hay horas programadas* es el valor predeterminado si no dispone de ninguna programación definida.</span><span class="sxs-lookup"><span data-stu-id="e4683-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="e4683-164">Busque la sección **Escalar por métrica** y seleccione **CPU**.</span><span class="sxs-lookup"><span data-stu-id="e4683-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="e4683-165">Ahora puede configurar un intervalo máximo y mínimo de instancias de rol, el uso de la CPU de destino (para desencadenar una escalada vertical) y el número de instancias para escalar y reducir verticalmente.</span><span class="sxs-lookup"><span data-stu-id="e4683-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![Escalar un rol de servicio en la nube con la carga de la CPU][cpu_scale]

> [!TIP]
> <span data-ttu-id="e4683-167">Siempre que vea ![][tip_icon], mueva el mouse y podrá obtener ayuda acerca de lo que realiza una configuración específica.</span><span class="sxs-lookup"><span data-stu-id="e4683-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="e4683-168">Escala automática: Cola</span><span class="sxs-lookup"><span data-stu-id="e4683-168">Automatic scale - Queue</span></span>
<span data-ttu-id="e4683-169">Este modo escala automáticamente si el número de mensajes en una cola está por encima o por debajo de un umbral especificado.</span><span class="sxs-lookup"><span data-stu-id="e4683-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="e4683-170">Las instancias de rol se crean o eliminan cuando esto ocurre.</span><span class="sxs-lookup"><span data-stu-id="e4683-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="e4683-171">En el [Portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **Servicios en la nube**y, a continuación, haga clic en el nombre del servicio en la nube para abrir el panel.</span><span class="sxs-lookup"><span data-stu-id="e4683-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e4683-172">Si no ve el servicio en la nube, debe cambiar de **Producción** a **Almacenamiento provisional** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="e4683-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="e4683-173">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="e4683-173">Click **Scale**.</span></span>
3. <span data-ttu-id="e4683-174">Busque la sección **Escalar por métrica** y seleccione **COLA**.</span><span class="sxs-lookup"><span data-stu-id="e4683-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="e4683-175">Ahora puede configurar un intervalo máximo y mínimo de instancias de rol, la cola y el número de mensajes de cola para procesar por cada instancia, y el número de instancias para escalar y reducir verticalmente.</span><span class="sxs-lookup"><span data-stu-id="e4683-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![Escalar un rol de servicio en la nube con una cola de mensajes][queue_scale]

> [!TIP]
> <span data-ttu-id="e4683-177">Siempre que vea ![][tip_icon], mueva el mouse y podrá obtener ayuda acerca de lo que realiza una configuración específica.</span><span class="sxs-lookup"><span data-stu-id="e4683-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="e4683-178">Escalado de recursos vinculados</span><span class="sxs-lookup"><span data-stu-id="e4683-178">Scale linked resources</span></span>
<span data-ttu-id="e4683-179">A menudo, cuando se escala un rol, es beneficioso también escalar la base de datos que la aplicación está usando.</span><span class="sxs-lookup"><span data-stu-id="e4683-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="e4683-180">Si vincula la base de datos al servicio en la nube, puede acceder a la configuración de escalado de ese recurso haciendo clic en el vínculo apropiado.</span><span class="sxs-lookup"><span data-stu-id="e4683-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="e4683-181">En el [Portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **Servicios en la nube**y, a continuación, haga clic en el nombre del servicio en la nube para abrir el panel.</span><span class="sxs-lookup"><span data-stu-id="e4683-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e4683-182">Si no ve el servicio en la nube, debe cambiar de **Producción** a **Almacenamiento provisional** o viceversa.</span><span class="sxs-lookup"><span data-stu-id="e4683-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="e4683-183">Haga clic en **Escalar**.</span><span class="sxs-lookup"><span data-stu-id="e4683-183">Click **Scale**.</span></span>
3. <span data-ttu-id="e4683-184">Busque la sección **recursos vinculados** y haga clic en **Administrar el escalado de esta base de datos**.</span><span class="sxs-lookup"><span data-stu-id="e4683-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4683-185">Si no ve la sección **recursos vinculados** , probablemente no tenga ningún recurso vinculado.</span><span class="sxs-lookup"><span data-stu-id="e4683-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
