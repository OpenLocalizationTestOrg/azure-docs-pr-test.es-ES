---
title: "Escalar automáticamente un servicio en la nube en el portal | Microsoft Docs"
description: "Obtenga información sobre cómo usar el portal para configurar reglas de escalado automático de un rol de trabajo o un rol web de servicio en la nube en Azure."
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
ms.openlocfilehash: e9683d4c5779450fd67fa42ab13095c7f201b4cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a><span data-ttu-id="0f66d-103">Procedimiento para configurar el escalado automático para un servicio en la nube en el Portal</span><span class="sxs-lookup"><span data-stu-id="0f66d-103">How to configure auto scaling for a Cloud Service in the portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f66d-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0f66d-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="0f66d-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="0f66d-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="0f66d-106">Las condiciones se pueden definir para un rol de trabajo de servicio en la nube que desencadene una operación de reducción horizontal y de escalabilidad horizontal.</span><span class="sxs-lookup"><span data-stu-id="0f66d-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="0f66d-107">Las condiciones del rol pueden basarse en la CPU, el disco o la carga de red del rol.</span><span class="sxs-lookup"><span data-stu-id="0f66d-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span></span> <span data-ttu-id="0f66d-108">También puede establecer una condición basada en una cola de mensajes o en la métrica de algún otro recurso de Azure asociado a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="0f66d-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0f66d-109">Este artículo se centra en los roles de trabajo y en los roles web de Servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="0f66d-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="0f66d-110">Al crear una máquina virtual (clásica) directamente, esta se hospeda en un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="0f66d-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="0f66d-111">Puede escalar una máquina virtual estándar asociándola con un [conjunto de disponibilidad](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) y activándola o desactivándola manualmente.</span><span class="sxs-lookup"><span data-stu-id="0f66d-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="0f66d-112">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="0f66d-112">Considerations</span></span>
<span data-ttu-id="0f66d-113">Debe considerar la siguiente información antes de configurar el escalado para su aplicación:</span><span class="sxs-lookup"><span data-stu-id="0f66d-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="0f66d-114">El uso de núcleos afecta el escalado.</span><span class="sxs-lookup"><span data-stu-id="0f66d-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="0f66d-115">Las instancias de rol más grandes usan más núcleos.</span><span class="sxs-lookup"><span data-stu-id="0f66d-115">Larger role instances use more cores.</span></span> <span data-ttu-id="0f66d-116">Solo puede escalar una aplicación dentro del límite de núcleos para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="0f66d-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="0f66d-117">Por ejemplo, supongamos que su suscripción tiene un límite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="0f66d-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="0f66d-118">Si ejecuta una aplicación con dos servicios en la nube de tamaño mediano (un total de 4 núcleos), solo puede escalar verticalmente otras implementaciones del servicio en la nube en su suscripción con los 16 núcleos restantes.</span><span class="sxs-lookup"><span data-stu-id="0f66d-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="0f66d-119">Para obtener más información sobre los tamaños, consulte [Tamaños de los servicios en la nube](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="0f66d-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="0f66d-120">Puede realizar una operación de escalabilidad basada en un umbral de mensajes de cola.</span><span class="sxs-lookup"><span data-stu-id="0f66d-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="0f66d-121">Para obtener más información sobre las colas, consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="0f66d-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="0f66d-122">También puede escalar otros recursos asociados a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="0f66d-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="0f66d-123">Para permitir una alta disponibilidad de la aplicación, debe asegurarse de que se implemente con dos o más instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="0f66d-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="0f66d-124">Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="0f66d-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="0f66d-125">Ubicación de la escala</span><span class="sxs-lookup"><span data-stu-id="0f66d-125">Where scale is located</span></span>
<span data-ttu-id="0f66d-126">Después de seleccionar el servicio en la nube, debe tener visible la hoja del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="0f66d-126">After you select your cloud service, you should have the cloud service blade visible.</span></span>

1. <span data-ttu-id="0f66d-127">En la hoja del servicio en la nube, seleccione el nombre del servicio en la nube en el icono de **Roles e instancias** .</span><span class="sxs-lookup"><span data-stu-id="0f66d-127">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span></span>   
   <span data-ttu-id="0f66d-128">**IMPORTANTE**: No se olvide de hacer clic en el rol del servicio en la nube, no en la instancia de rol que está debajo de dicho rol.</span><span class="sxs-lookup"><span data-stu-id="0f66d-128">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="0f66d-129">Seleccione el icono de **escala** .</span><span class="sxs-lookup"><span data-stu-id="0f66d-129">Select the **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="0f66d-130">Escala automática</span><span class="sxs-lookup"><span data-stu-id="0f66d-130">Automatic scale</span></span>
<span data-ttu-id="0f66d-131">Puede configurar la configuración de escala de un rol con estos dos modos: **Manual** o **Automático**.</span><span class="sxs-lookup"><span data-stu-id="0f66d-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="0f66d-132">Con el modo Manual, como cabe de esperar, establece el número absoluto de instancias.</span><span class="sxs-lookup"><span data-stu-id="0f66d-132">Manual is as you would expect, you set the absolute count of instances.</span></span> <span data-ttu-id="0f66d-133">Sin embargo, con Automático, se pueden establecer reglas que rijan cómo se debe realizar la operación de escala y en qué medida.</span><span class="sxs-lookup"><span data-stu-id="0f66d-133">Automatic however allows you to set rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="0f66d-134">Establezca la opción **Escalar por** para **programar las reglas de rendimiento y programación**.</span><span class="sxs-lookup"><span data-stu-id="0f66d-134">Set the **Scale by** option to **schedule and performance rules**.</span></span>

![Configuración de escala de servicios en la nube con el perfil y la regla](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="0f66d-136">Un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="0f66d-136">An existing profile.</span></span>
2. <span data-ttu-id="0f66d-137">Agregue una regla para el perfil principal.</span><span class="sxs-lookup"><span data-stu-id="0f66d-137">Add a rule for the parent profile.</span></span>
3. <span data-ttu-id="0f66d-138">Agregue otro perfil.</span><span class="sxs-lookup"><span data-stu-id="0f66d-138">Add another profile.</span></span>

<span data-ttu-id="0f66d-139">Seleccione **Agregar perfil**.</span><span class="sxs-lookup"><span data-stu-id="0f66d-139">Select **Add Profile**.</span></span> <span data-ttu-id="0f66d-140">El perfil determina qué modo va a utilizar para realizar la operación de escala: **siempre**, **periodicidad** y **fecha fija**.</span><span class="sxs-lookup"><span data-stu-id="0f66d-140">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="0f66d-141">Después de haber configurado el perfil y ñas reglas, seleccione el icono de **Guardar** situado en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="0f66d-141">After you have configured the profile and rules, select the **Save** icon at the top.</span></span>

#### <a name="profile"></a><span data-ttu-id="0f66d-142">Perfil</span><span class="sxs-lookup"><span data-stu-id="0f66d-142">Profile</span></span>
<span data-ttu-id="0f66d-143">El perfil establece instancias mínimas y máximas para la escala, además de cuándo está activo el intervalo de escala.</span><span class="sxs-lookup"><span data-stu-id="0f66d-143">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="0f66d-144">**Siempre**</span><span class="sxs-lookup"><span data-stu-id="0f66d-144">**Always**</span></span>

    <span data-ttu-id="0f66d-145">Mantenga siempre disponible este rango de instancias.</span><span class="sxs-lookup"><span data-stu-id="0f66d-145">Always keep this range of instances available.</span></span>  

    ![Servicio en la nube en el que siempre se realiza la operación de escala](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="0f66d-147">**Periodicidad**</span><span class="sxs-lookup"><span data-stu-id="0f66d-147">**Recurrence**</span></span>

    <span data-ttu-id="0f66d-148">Elija un conjunto de días de la semana para realizar la escala.</span><span class="sxs-lookup"><span data-stu-id="0f66d-148">Choose a set of days of the week to scale.</span></span>

    ![Escala de servicio en la nube con una programación de periodicidad](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="0f66d-150">**Fecha fija**</span><span class="sxs-lookup"><span data-stu-id="0f66d-150">**Fixed Date**</span></span>

    <span data-ttu-id="0f66d-151">Un intervalo de fechas fijo para escalar el rol.</span><span class="sxs-lookup"><span data-stu-id="0f66d-151">A fixed date range to scale the role.</span></span>

    ![Escala de servicio en la nube con una fecha fija](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="0f66d-153">Después de haber configurado el perfil, seleccione el botón **Aceptar** situado en la parte inferior de la hoja de perfil.</span><span class="sxs-lookup"><span data-stu-id="0f66d-153">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="0f66d-154">Regla</span><span class="sxs-lookup"><span data-stu-id="0f66d-154">Rule</span></span>
<span data-ttu-id="0f66d-155">Las reglas se agregan a un perfil y representan una condición que desencadenará la escala.</span><span class="sxs-lookup"><span data-stu-id="0f66d-155">Rules are added to a profile and represent a condition that triggers the scale.</span></span>

<span data-ttu-id="0f66d-156">El desencadenador de reglas se basa en una métrica del servicio en la nube (uso de CPU o actividad del disco o de la red) a la que puede agregar un valor condicional.</span><span class="sxs-lookup"><span data-stu-id="0f66d-156">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span></span> <span data-ttu-id="0f66d-157">Además, puede basar la acción desencadenadora en una cola de mensajes o en la métrica de algún otro recurso de Azure asociado a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="0f66d-157">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="0f66d-158">Después de haber configurado la regla, seleccione el botón **Aceptar** situado en la parte inferior de la hoja de la regla.</span><span class="sxs-lookup"><span data-stu-id="0f66d-158">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span></span>

## <a name="back-to-manual-scale"></a><span data-ttu-id="0f66d-159">Regreso al paso de escala manual</span><span class="sxs-lookup"><span data-stu-id="0f66d-159">Back to manual scale</span></span>
<span data-ttu-id="0f66d-160">Vaya a la [configuración de escala](#where-scale-is-located) y establezca el valor de la opción **Escalar por** en **un recuento de instancias que especifique manualmente**.</span><span class="sxs-lookup"><span data-stu-id="0f66d-160">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span></span>

![Configuración de escala de servicios en la nube con el perfil y la regla](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="0f66d-162">Con esta configuración se elimina la escala automática del rol y podrá establecer el recuento de instancias directamente.</span><span class="sxs-lookup"><span data-stu-id="0f66d-162">This setting removes automated scaling from the role and then you can set the instance count directly.</span></span>

1. <span data-ttu-id="0f66d-163">La opción de escala (manual o automática).</span><span class="sxs-lookup"><span data-stu-id="0f66d-163">The scale (manual or automated) option.</span></span>
2. <span data-ttu-id="0f66d-164">Un regulador de instancias de rol para definir las instancias en las que se realizará la operación de escala.</span><span class="sxs-lookup"><span data-stu-id="0f66d-164">A role instance slider to set the instances to scale to.</span></span>
3. <span data-ttu-id="0f66d-165">Las instancias del rol en las que se realizar la operación de escala.</span><span class="sxs-lookup"><span data-stu-id="0f66d-165">Instances of the role to scale to.</span></span>

<span data-ttu-id="0f66d-166">Después de configurar la configuración de escala, seleccione el icono de **Guardar** situado en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="0f66d-166">After you have configured the scale settings, select the **Save** icon at the top.</span></span>
