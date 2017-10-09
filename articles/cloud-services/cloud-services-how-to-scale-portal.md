---
title: aaaAuto escalar un servicio de nube en el portal de hello | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola portal tooconfigure reglas de escalado automático para un rol web de servicio de nube o el rol de trabajo en Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="307af-103">Cómo tooconfigure Autoescala para un servicio de nube en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="307af-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="307af-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="307af-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="307af-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="307af-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="307af-106">Las condiciones se pueden definir para un rol de trabajo de servicio en la nube que desencadene una operación de reducción horizontal y de escalabilidad horizontal.</span><span class="sxs-lookup"><span data-stu-id="307af-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="307af-107">condiciones de Hello para el rol de hello pueden basarse en hello CPU, disco o de carga de red del rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="307af-108">También puede establecer una condición basada en una métrica de Hola o de cola de mensajes de algún otro recurso de Azure asociado a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="307af-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="307af-109">Este artículo se centra en los roles de trabajo y en los roles web de Servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="307af-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="307af-110">Al crear una máquina virtual (clásica) directamente, esta se hospeda en un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="307af-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="307af-111">Puede escalar una máquina virtual estándar asociándola con un [conjunto de disponibilidad](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) y activándola o desactivándola manualmente.</span><span class="sxs-lookup"><span data-stu-id="307af-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="307af-112">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="307af-112">Considerations</span></span>
<span data-ttu-id="307af-113">Debe considerar Hola siguiente información antes de configurar el escalado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="307af-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="307af-114">El uso de núcleos afecta el escalado.</span><span class="sxs-lookup"><span data-stu-id="307af-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="307af-115">Las instancias de rol más grandes usan más núcleos.</span><span class="sxs-lookup"><span data-stu-id="307af-115">Larger role instances use more cores.</span></span> <span data-ttu-id="307af-116">Puede escalar una aplicación solo en el límite de Hola de núcleos de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="307af-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="307af-117">Por ejemplo, supongamos que su suscripción tiene un límite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="307af-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="307af-118">Si ejecuta una aplicación con dos servicios en la nube de tamaño mediano (un total de 4 núcleos), solo puede aumentar otras implementaciones de servicio de nube en su suscripción por restantes 16 núcleos de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="307af-119">Para obtener más información sobre los tamaños, consulte [Tamaños de los servicios en la nube](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="307af-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="307af-120">Puede realizar una operación de escalabilidad basada en un umbral de mensajes de cola.</span><span class="sxs-lookup"><span data-stu-id="307af-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="307af-121">Para obtener más información acerca de cómo toouse colas, consulte [cómo toouse Hola servicio de almacenamiento cola](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="307af-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="307af-122">También puede escalar otros recursos asociados a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="307af-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="307af-123">tooenable alta disponibilidad de la aplicación, debe asegurarse de que se implementa con dos o más instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="307af-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="307af-124">Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="307af-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="307af-125">Ubicación de la escala</span><span class="sxs-lookup"><span data-stu-id="307af-125">Where scale is located</span></span>
<span data-ttu-id="307af-126">Después de seleccionar el servicio en la nube, debe tener la hoja de servicio de nube de hello visible.</span><span class="sxs-lookup"><span data-stu-id="307af-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="307af-127">En la hoja de servicio de nube de hello en hello **Roles e instancias** icono, el nombre de hello seleccione del servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="307af-128">**IMPORTANTE**: hacer seguro en la nube tooclick Hola rol de servicio y no Hola instancia de rol que está por debajo de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="307af-129">Seleccione hello **escala** icono.</span><span class="sxs-lookup"><span data-stu-id="307af-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="307af-130">Escala automática</span><span class="sxs-lookup"><span data-stu-id="307af-130">Automatic scale</span></span>
<span data-ttu-id="307af-131">Puede configurar la configuración de escala de un rol con estos dos modos: **Manual** o **Automático**.</span><span class="sxs-lookup"><span data-stu-id="307af-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="307af-132">Manual es el método tal como se esperaría, Establece Hola absoluta recuento de instancias.</span><span class="sxs-lookup"><span data-stu-id="307af-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="307af-133">Sin embargo, automático permite tooset reglas que rigen cómo y en qué cantidad se adaptarán.</span><span class="sxs-lookup"><span data-stu-id="307af-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="307af-134">Conjunto hello **escalar** opción demasiado**reglas de programación y rendimiento**.</span><span class="sxs-lookup"><span data-stu-id="307af-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Configuración de escala de servicios en la nube con el perfil y la regla](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="307af-136">Un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="307af-136">An existing profile.</span></span>
2. <span data-ttu-id="307af-137">Agregar una regla para el perfil de hello primario.</span><span class="sxs-lookup"><span data-stu-id="307af-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="307af-138">Agregue otro perfil.</span><span class="sxs-lookup"><span data-stu-id="307af-138">Add another profile.</span></span>

<span data-ttu-id="307af-139">Seleccione **Agregar perfil**.</span><span class="sxs-lookup"><span data-stu-id="307af-139">Select **Add Profile**.</span></span> <span data-ttu-id="307af-140">perfil Hello determina qué modo desea toouse para la escala de hello: **siempre**, **periodicidad**, **fecha fija**.</span><span class="sxs-lookup"><span data-stu-id="307af-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="307af-141">Después de haber configurado el perfil de Hola y reglas, seleccione hello **guardar** situado en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="307af-142">Perfil</span><span class="sxs-lookup"><span data-stu-id="307af-142">Profile</span></span>
<span data-ttu-id="307af-143">mínimo de conjuntos de perfiles de Hola y escala el número máximo de instancias para hello y también cuando este intervalo de escala está activo.</span><span class="sxs-lookup"><span data-stu-id="307af-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="307af-144">**Siempre**</span><span class="sxs-lookup"><span data-stu-id="307af-144">**Always**</span></span>

    <span data-ttu-id="307af-145">Mantenga siempre disponible este rango de instancias.</span><span class="sxs-lookup"><span data-stu-id="307af-145">Always keep this range of instances available.</span></span>  

    ![Servicio en la nube en el que siempre se realiza la operación de escala](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="307af-147">**Periodicidad**</span><span class="sxs-lookup"><span data-stu-id="307af-147">**Recurrence**</span></span>

    <span data-ttu-id="307af-148">Elija un conjunto de días de hello semana tooscale.</span><span class="sxs-lookup"><span data-stu-id="307af-148">Choose a set of days of hello week tooscale.</span></span>

    ![Escala de servicio en la nube con una programación de periodicidad](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="307af-150">**Fecha fija**</span><span class="sxs-lookup"><span data-stu-id="307af-150">**Fixed Date**</span></span>

    <span data-ttu-id="307af-151">Un rol de hello tooscale del intervalo de fecha fija.</span><span class="sxs-lookup"><span data-stu-id="307af-151">A fixed date range tooscale hello role.</span></span>

    ![Escala de servicio en la nube con una fecha fija](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="307af-153">Después de haber configurado el perfil de hello, seleccione hello **Aceptar** situado en parte inferior de Hola de hoja de perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="307af-154">Regla</span><span class="sxs-lookup"><span data-stu-id="307af-154">Rule</span></span>
<span data-ttu-id="307af-155">Las reglas se agregan tooa perfil y representan una condición que desencadena la escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="307af-156">desencadenador de la regla de Hola se basa en una métrica de servicio en la nube hello (uso de CPU, la actividad del disco o actividad de red) toowhich puede agregar un valor condicional.</span><span class="sxs-lookup"><span data-stu-id="307af-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="307af-157">Además puede tener el desencadenamiento de hello basándose en una métrica de Hola o de cola de mensajes de algún otro recurso de Azure asociado a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="307af-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="307af-158">Después de haber configurado la regla de hello, seleccione hello **Aceptar** situado en parte inferior de Hola de hoja de la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="307af-159">Escala de toomanual atrás</span><span class="sxs-lookup"><span data-stu-id="307af-159">Back toomanual scale</span></span>
<span data-ttu-id="307af-160">Navegue toohello [configuración de la escala](#where-scale-is-located) conjunto hello y **escalar** opción demasiado**un recuento de instancias que especifique manualmente**.</span><span class="sxs-lookup"><span data-stu-id="307af-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Configuración de escala de servicios en la nube con el perfil y la regla](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="307af-162">Esta opción quita escalado automatizadas de rol de hello y, a continuación, puede establecer recuento de instancias de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="307af-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="307af-163">opción de escala (manuales o automatizadas) Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="307af-164">Un Hola de tooset del control deslizante de instancia de rol tooscale para las instancias.</span><span class="sxs-lookup"><span data-stu-id="307af-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="307af-165">Instancias de hello rol tooscale a.</span><span class="sxs-lookup"><span data-stu-id="307af-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="307af-166">Después de configurar la configuración de escalado hello, seleccione hello **guardar** situado en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="307af-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
