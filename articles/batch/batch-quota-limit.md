---
title: "Límites y cuotas del servicio para Azure Batch | Microsoft Docs"
description: "Obtenga información sobre las restricciones, los límites y las cuotas de Azure Batch predeterminados y cómo solicitar un aumento de la cuota."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="15547-103">Límites y cuotas del servicio Lote</span><span class="sxs-lookup"><span data-stu-id="15547-103">Batch service quotas and limits</span></span>

<span data-ttu-id="15547-104">Al igual que en otros servicios de Azure, existen límites en determinados recursos asociados con el servicio Lote.</span><span class="sxs-lookup"><span data-stu-id="15547-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="15547-105">Muchos de ellos son cuotas predeterminadas que Azure aplica en el nivel de cuenta o suscripción.</span><span class="sxs-lookup"><span data-stu-id="15547-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="15547-106">En este artículo se describen esos valores predeterminados y cómo solicitar un aumento de la cuota.</span><span class="sxs-lookup"><span data-stu-id="15547-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="15547-107">Tenga presente estas cuotas cuando diseñe y escale las cargas de trabajo de Lote.</span><span class="sxs-lookup"><span data-stu-id="15547-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="15547-108">Por ejemplo, si su grupo no alcanza el número objetivo de nodos de proceso especificado, es posible que se haya alcanzado el límite de cuota de núcleos de la cuenta de Batch o una cuota de núcleos de máquina virtual regionales para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="15547-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="15547-109">Se pueden ejecutar varias cargas de trabajo de Batch en una sola cuenta de Batch, o bien distribuir las cargas de trabajo entre cuentas de Batch que se encuentren en la misma suscripción, pero en diferentes regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="15547-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="15547-110">Si planea ejecutar cargas de trabajo de producción en Lote, es posible que tenga que aumentar el valor predeterminado de una o varias de las cuotas.</span><span class="sxs-lookup"><span data-stu-id="15547-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="15547-111">Si desea aumentar una cuota, puede abrir una [solicitud de soporte técnico al cliente](#increase-a-quota) en línea sin ningún costo.</span><span class="sxs-lookup"><span data-stu-id="15547-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="15547-112">Una cuota es un límite de crédito, no una garantía de capacidad.</span><span class="sxs-lookup"><span data-stu-id="15547-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="15547-113">Si tiene necesidades de capacidad a gran escala, póngase en contacto con el soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="15547-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="15547-114">Cuotas de recursos</span><span class="sxs-lookup"><span data-stu-id="15547-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="15547-115">Cuotas en el modo de suscripción de usuario</span><span class="sxs-lookup"><span data-stu-id="15547-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="15547-116">Para una cuenta de Batch con el modo de asignación de grupo establecido en **suscripción de usuario**, las máquinas virtuales y otros recursos de Batch, como cuentas de almacenamiento, se crean directamente en su suscripción cuando se crea un grupo.</span><span class="sxs-lookup"><span data-stu-id="15547-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="15547-117">La cuota de núcleos de Azure Batch no se aplica a una cuenta creada en este modo.</span><span class="sxs-lookup"><span data-stu-id="15547-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="15547-118">En su lugar, se aplican las cuotas en la suscripción para núcleos de proceso regionales y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="15547-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="15547-119">Aprenda más sobre estas cuotas en [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="15547-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="15547-120">Cuando planee el uso de recursos para una cuenta creada en el modo de suscripción de usuario, tenga en cuenta que los siguientes recursos de Batch (además de núcleos de proceso) son necesarios para cada 40 máquinas virtuales Linux o 20 máquinas virtuales Windows:</span><span class="sxs-lookup"><span data-stu-id="15547-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="15547-121">Recurso</span><span class="sxs-lookup"><span data-stu-id="15547-121">Resource</span></span> | <span data-ttu-id="15547-122">Cuota</span><span class="sxs-lookup"><span data-stu-id="15547-122">Quota</span></span> | <span data-ttu-id="15547-123">Proveedor</span><span class="sxs-lookup"><span data-stu-id="15547-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="15547-124">Una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="15547-124">One storage account</span></span> | <span data-ttu-id="15547-125">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="15547-125">Storage Accounts</span></span> | <span data-ttu-id="15547-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="15547-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="15547-127">Una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="15547-127">One public IP address</span></span> | <span data-ttu-id="15547-128">Direcciones IP públicas</span><span class="sxs-lookup"><span data-stu-id="15547-128">Public IP Addresses</span></span> | <span data-ttu-id="15547-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="15547-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="15547-130">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="15547-130">One virtual network</span></span> | <span data-ttu-id="15547-131">Redes virtuales</span><span class="sxs-lookup"><span data-stu-id="15547-131">Virtual Networks</span></span> | <span data-ttu-id="15547-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="15547-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="15547-133">Un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="15547-133">One network security group</span></span> | <span data-ttu-id="15547-134">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="15547-134">Network Security Groups</span></span> | <span data-ttu-id="15547-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="15547-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="15547-136">Un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="15547-136">One virtual machine scale set</span></span> | <span data-ttu-id="15547-137">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="15547-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="15547-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="15547-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="15547-139">Un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="15547-139">One load balancer</span></span> | <span data-ttu-id="15547-140">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="15547-140">Load Balancers</span></span> | <span data-ttu-id="15547-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="15547-141">Microsoft.Network</span></span> | 

<span data-ttu-id="15547-142">La cuota de núcleos en un nivel regional o por familia de máquinas virtuales se debe establecer en función del tamaño de máquina virtual necesario para el grupo o los grupos de Batch:</span><span class="sxs-lookup"><span data-stu-id="15547-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="15547-143">Cuota</span><span class="sxs-lookup"><span data-stu-id="15547-143">Quota</span></span> | <span data-ttu-id="15547-144">Proveedor</span><span class="sxs-lookup"><span data-stu-id="15547-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="15547-145">N.º total de núcleos regionales</span><span class="sxs-lookup"><span data-stu-id="15547-145">Total Regional Cores</span></span> | <span data-ttu-id="15547-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="15547-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="15547-147">…</span><span class="sxs-lookup"><span data-stu-id="15547-147">…</span></span> <span data-ttu-id="15547-148">Núcleos de familia</span><span class="sxs-lookup"><span data-stu-id="15547-148">Family Cores</span></span> | <span data-ttu-id="15547-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="15547-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="15547-150">Otros límites</span><span class="sxs-lookup"><span data-stu-id="15547-150">Other limits</span></span>
| <span data-ttu-id="15547-151">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="15547-151">**Resource**</span></span> | <span data-ttu-id="15547-152">**Límite máximo**</span><span class="sxs-lookup"><span data-stu-id="15547-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="15547-153">[Tareas simultáneas](batch-parallel-node-tasks.md) por nodo de proceso</span><span class="sxs-lookup"><span data-stu-id="15547-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="15547-154">4 × número de núcleos de nodo</span><span class="sxs-lookup"><span data-stu-id="15547-154">4 x number of node cores</span></span> |
| <span data-ttu-id="15547-155">[Aplicaciones](batch-application-packages.md) por cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="15547-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="15547-156">20 |</span><span class="sxs-lookup"><span data-stu-id="15547-156">20</span></span> |
| <span data-ttu-id="15547-157">Paquetes de aplicación por aplicación</span><span class="sxs-lookup"><span data-stu-id="15547-157">Application packages per application</span></span> |<span data-ttu-id="15547-158">40</span><span class="sxs-lookup"><span data-stu-id="15547-158">40</span></span> |
| <span data-ttu-id="15547-159">Tamaño del paquete de aplicación (cada uno)</span><span class="sxs-lookup"><span data-stu-id="15547-159">Application package size (each)</span></span> |<span data-ttu-id="15547-160">Aprox. 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="15547-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="15547-161">Tamaño máximo de la tarea de inicio</span><span class="sxs-lookup"><span data-stu-id="15547-161">Maximum start task size</span></span> | <span data-ttu-id="15547-162">32 768 caracteres<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="15547-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="15547-163"><sup>1</sup> Límite de Almacenamiento de Azure para el tamaño máximo de blob en bloques</span><span class="sxs-lookup"><span data-stu-id="15547-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="15547-164">
<sup>2</sup> Incluye archivos de recursos y variables de entorno</span><span class="sxs-lookup"><span data-stu-id="15547-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="15547-165">Visualización de las cuotas de Lote</span><span class="sxs-lookup"><span data-stu-id="15547-165">View Batch quotas</span></span>
<span data-ttu-id="15547-166">Vea las cuotas de la cuenta de Batch en [Azure Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="15547-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="15547-167">Seleccione **Cuentas de Batch** en el portal y, luego, seleccione la cuenta de Batch que le interesan.</span><span class="sxs-lookup"><span data-stu-id="15547-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="15547-168">Seleccione **Propiedades** en la hoja del menú de la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="15547-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="15547-169">La hoja Propiedades muestra las **cuotas** que hay aplicadas actualmente en la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="15547-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Cuotas de la cuenta de Lote][account_quotas]

<span data-ttu-id="15547-171">Para una cuenta de Batch creada en el modo de suscripción de usuario, vea las cuotas de suscripción relacionadas en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="15547-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="15547-172">Seleccione **Suscripciones** y la suscripción que usa para la cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="15547-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="15547-173">En la hoja **Suscripción**, seleccione **Uso y cuotas**.</span><span class="sxs-lookup"><span data-stu-id="15547-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="15547-174">Aumento de la cuota</span><span class="sxs-lookup"><span data-stu-id="15547-174">Increase a quota</span></span>
<span data-ttu-id="15547-175">Siga estos pasos para solicitar un aumento de la cuota para la cuenta de Batch o la suscripción con [Azure Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="15547-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="15547-176">El tipo de aumento de cuota depende del modo de asignación de grupo de su cuenta de Batch.</span><span class="sxs-lookup"><span data-stu-id="15547-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="15547-177">Aumento de la cuota de núcleos de Batch</span><span class="sxs-lookup"><span data-stu-id="15547-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="15547-178">Si su cuenta de Batch se creó en el modo de **servicio Batch**, siga estos pasos para solicitar un aumento de la cuota de núcleos de Batch:</span><span class="sxs-lookup"><span data-stu-id="15547-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="15547-179">Seleccione el icono **Ayuda y soporte técnico** en el panel del portal o el signo de interrogación (**?**) en la esquina superior derecha del portal.</span><span class="sxs-lookup"><span data-stu-id="15547-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="15547-180">Seleccione **Nueva solicitud de soporte técnico** > **Básico**.</span><span class="sxs-lookup"><span data-stu-id="15547-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="15547-181">En la hoja **Básico** :</span><span class="sxs-lookup"><span data-stu-id="15547-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="15547-182">a.</span><span class="sxs-lookup"><span data-stu-id="15547-182">a.</span></span> <span data-ttu-id="15547-183">**Tipo de problema** > **Cuota**</span><span class="sxs-lookup"><span data-stu-id="15547-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="15547-184">b.</span><span class="sxs-lookup"><span data-stu-id="15547-184">b.</span></span> <span data-ttu-id="15547-185">Seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="15547-185">Select your subscription.</span></span>
   
    <span data-ttu-id="15547-186">c.</span><span class="sxs-lookup"><span data-stu-id="15547-186">c.</span></span> <span data-ttu-id="15547-187">**Tipo de cuota** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="15547-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="15547-188">d.</span><span class="sxs-lookup"><span data-stu-id="15547-188">d.</span></span> <span data-ttu-id="15547-189">**Plan de soporte técnico** > **Compatibilidad con cuotas (incluida)**</span><span class="sxs-lookup"><span data-stu-id="15547-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="15547-190">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="15547-190">Click **Next**.</span></span>
4. <span data-ttu-id="15547-191">En la hoja **Problema** :</span><span class="sxs-lookup"><span data-stu-id="15547-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="15547-192">a.</span><span class="sxs-lookup"><span data-stu-id="15547-192">a.</span></span> <span data-ttu-id="15547-193">Seleccione una de las opciones en **Gravedad** según su [impacto en el negocio][support_sev].</span><span class="sxs-lookup"><span data-stu-id="15547-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="15547-194">b.</span><span class="sxs-lookup"><span data-stu-id="15547-194">b.</span></span> <span data-ttu-id="15547-195">En **Detalles**, especifique cada cuota que desee cambiar, el nombre de cuenta de Lote y el nuevo límite.</span><span class="sxs-lookup"><span data-stu-id="15547-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="15547-196">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="15547-196">Click **Next**.</span></span>
5. <span data-ttu-id="15547-197">En la hoja **Información de contacto** :</span><span class="sxs-lookup"><span data-stu-id="15547-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="15547-198">a.</span><span class="sxs-lookup"><span data-stu-id="15547-198">a.</span></span> <span data-ttu-id="15547-199">Seleccione un valor en **Método de contacto preferido**.</span><span class="sxs-lookup"><span data-stu-id="15547-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="15547-200">b.</span><span class="sxs-lookup"><span data-stu-id="15547-200">b.</span></span> <span data-ttu-id="15547-201">Compruebe y especifique los detalles de contacto necesarios.</span><span class="sxs-lookup"><span data-stu-id="15547-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="15547-202">Haga clic en **Crear** para enviar la solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="15547-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="15547-203">Una vez que haya enviado la solicitud de soporte técnico, el servicio de soporte técnico de Azure se comunicará con usted.</span><span class="sxs-lookup"><span data-stu-id="15547-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="15547-204">Tenga en cuenta que se puede tardar hasta 2 días laborables en completar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="15547-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="15547-205">Aumento de una cuota de núcleos de suscripción</span><span class="sxs-lookup"><span data-stu-id="15547-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="15547-206">Si su cuenta de Batch se creó en el modo de **suscripción de usuario** y necesita más núcleos regionales o de familia de máquina virtual, solicite un aumento de la cuota en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="15547-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="15547-207">Para ver los pasos, consulte [Solicitudes de aumento de cuota de núcleos de Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="15547-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="15547-208">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="15547-208">Related topics</span></span>
* [<span data-ttu-id="15547-209">Creación de una cuenta de Lote de Azure con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="15547-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="15547-210">Información general de las características de Lote de Azure</span><span class="sxs-lookup"><span data-stu-id="15547-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="15547-211">Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="15547-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
