---
title: "aaaService las cuotas y límites de lote de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de las cuotas de lote de Azure de forma predeterminada, los límites y restricciones, y cómo aumenta la cuota de toorequest"
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
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="b7664-103">Límites y cuotas del servicio Lote</span><span class="sxs-lookup"><span data-stu-id="b7664-103">Batch service quotas and limits</span></span>

<span data-ttu-id="b7664-104">Como con otros servicios de Azure, hay límites en determinados recursos asociados con hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="b7664-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="b7664-105">Muchos de estos límites son cuotas predeterminado que se aplican por Azure en el nivel de cuenta o suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7664-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="b7664-106">En este artículo se describen esos valores predeterminados y cómo solicitar un aumento de la cuota.</span><span class="sxs-lookup"><span data-stu-id="b7664-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="b7664-107">Tenga presente estas cuotas cuando diseñe y escale las cargas de trabajo de Lote.</span><span class="sxs-lookup"><span data-stu-id="b7664-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="b7664-108">Por ejemplo, si el grupo no alcance el número de destino de Hola de nodos de proceso que ha especificado, podría ha alcanzado el límite de cuota de núcleos de Hola para su cuenta de lote o una cuota de núcleos VM regional de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="b7664-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="b7664-109">Puede ejecutar varias cargas de trabajo por lotes en una sola cuenta de lote, o distribuir las cargas de trabajo entre las cuentas de lote que se encuentran en hello misma suscripción, pero en diferentes regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7664-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="b7664-110">Si tiene previsto cargas de trabajo de producción de toorun en lote, deberá tooincrease una o varias de las cuotas de Hola por encima del valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7664-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="b7664-111">Si desea tooraise una cuota, puede abrir en línea [solicitud de soporte técnico al cliente](#increase-a-quota) sin cargo.</span><span class="sxs-lookup"><span data-stu-id="b7664-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="b7664-112">Una cuota es un límite de crédito, no una garantía de capacidad.</span><span class="sxs-lookup"><span data-stu-id="b7664-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="b7664-113">Si tiene necesidades de capacidad a gran escala, póngase en contacto con el soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7664-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="b7664-114">Cuotas de recursos</span><span class="sxs-lookup"><span data-stu-id="b7664-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="b7664-115">Cuotas en el modo de suscripción de usuario</span><span class="sxs-lookup"><span data-stu-id="b7664-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="b7664-116">Para una cuenta de lote con el modo de asignación de grupo establecido demasiado**suscripción usuario**, las máquinas virtuales y otros recursos, como las cuentas de almacenamiento por lotes, se crean directamente en su suscripción cuando se crea un grupo.</span><span class="sxs-lookup"><span data-stu-id="b7664-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="b7664-117">cuota de núcleos de Hello Azure Batch no aplica a cuenta de tooan creada en este modo.</span><span class="sxs-lookup"><span data-stu-id="b7664-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="b7664-118">En su lugar, se aplican las cuotas de hello en la suscripción de núcleos de proceso regionales y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="b7664-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="b7664-119">Aprenda más sobre estas cuotas en [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="b7664-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="b7664-120">Al planear el uso de recursos para una cuenta creada en el modo de suscripción de usuario, Hola nota después de recursos de proceso por lotes (de núcleos de suma toocompute) son necesarias para cada 40 máquinas virtuales de Linux o 20 máquinas virtuales de Windows:</span><span class="sxs-lookup"><span data-stu-id="b7664-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="b7664-121">Recurso</span><span class="sxs-lookup"><span data-stu-id="b7664-121">Resource</span></span> | <span data-ttu-id="b7664-122">Cuota</span><span class="sxs-lookup"><span data-stu-id="b7664-122">Quota</span></span> | <span data-ttu-id="b7664-123">Proveedor</span><span class="sxs-lookup"><span data-stu-id="b7664-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="b7664-124">Una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b7664-124">One storage account</span></span> | <span data-ttu-id="b7664-125">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b7664-125">Storage Accounts</span></span> | <span data-ttu-id="b7664-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="b7664-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="b7664-127">Una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="b7664-127">One public IP address</span></span> | <span data-ttu-id="b7664-128">Direcciones IP públicas</span><span class="sxs-lookup"><span data-stu-id="b7664-128">Public IP Addresses</span></span> | <span data-ttu-id="b7664-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="b7664-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="b7664-130">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="b7664-130">One virtual network</span></span> | <span data-ttu-id="b7664-131">Redes virtuales</span><span class="sxs-lookup"><span data-stu-id="b7664-131">Virtual Networks</span></span> | <span data-ttu-id="b7664-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="b7664-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="b7664-133">Un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="b7664-133">One network security group</span></span> | <span data-ttu-id="b7664-134">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="b7664-134">Network Security Groups</span></span> | <span data-ttu-id="b7664-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="b7664-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="b7664-136">Un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="b7664-136">One virtual machine scale set</span></span> | <span data-ttu-id="b7664-137">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b7664-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="b7664-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="b7664-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="b7664-139">Un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="b7664-139">One load balancer</span></span> | <span data-ttu-id="b7664-140">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="b7664-140">Load Balancers</span></span> | <span data-ttu-id="b7664-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="b7664-141">Microsoft.Network</span></span> | 

<span data-ttu-id="b7664-142">cuota de núcleos de Hola a nivel regional o por familia de máquina virtual debe ser correspondiente toohello VM tamaño del espacio necesario para el grupo de proceso por lotes o grupos:</span><span class="sxs-lookup"><span data-stu-id="b7664-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="b7664-143">Quota</span><span class="sxs-lookup"><span data-stu-id="b7664-143">Quota</span></span> | <span data-ttu-id="b7664-144">Proveedor</span><span class="sxs-lookup"><span data-stu-id="b7664-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="b7664-145">N.º total de núcleos regionales</span><span class="sxs-lookup"><span data-stu-id="b7664-145">Total Regional Cores</span></span> | <span data-ttu-id="b7664-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="b7664-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="b7664-147">…</span><span class="sxs-lookup"><span data-stu-id="b7664-147">…</span></span> <span data-ttu-id="b7664-148">Núcleos de familia</span><span class="sxs-lookup"><span data-stu-id="b7664-148">Family Cores</span></span> | <span data-ttu-id="b7664-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="b7664-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="b7664-150">Otros límites</span><span class="sxs-lookup"><span data-stu-id="b7664-150">Other limits</span></span>
| <span data-ttu-id="b7664-151">**Recurso**</span><span class="sxs-lookup"><span data-stu-id="b7664-151">**Resource**</span></span> | <span data-ttu-id="b7664-152">**Límite máximo**</span><span class="sxs-lookup"><span data-stu-id="b7664-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="b7664-153">[Tareas simultáneas](batch-parallel-node-tasks.md) por nodo de proceso</span><span class="sxs-lookup"><span data-stu-id="b7664-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="b7664-154">4 × número de núcleos de nodo</span><span class="sxs-lookup"><span data-stu-id="b7664-154">4 x number of node cores</span></span> |
| <span data-ttu-id="b7664-155">[Aplicaciones](batch-application-packages.md) por cuenta de Lote</span><span class="sxs-lookup"><span data-stu-id="b7664-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="b7664-156">20 |</span><span class="sxs-lookup"><span data-stu-id="b7664-156">20</span></span> |
| <span data-ttu-id="b7664-157">Paquetes de aplicación por aplicación</span><span class="sxs-lookup"><span data-stu-id="b7664-157">Application packages per application</span></span> |<span data-ttu-id="b7664-158">40</span><span class="sxs-lookup"><span data-stu-id="b7664-158">40</span></span> |
| <span data-ttu-id="b7664-159">Tamaño del paquete de aplicación (cada uno)</span><span class="sxs-lookup"><span data-stu-id="b7664-159">Application package size (each)</span></span> |<span data-ttu-id="b7664-160">Aprox. 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7664-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="b7664-161">Tamaño máximo de la tarea de inicio</span><span class="sxs-lookup"><span data-stu-id="b7664-161">Maximum start task size</span></span> | <span data-ttu-id="b7664-162">32 768 caracteres<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b7664-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="b7664-163"><sup>1</sup> Límite de Almacenamiento de Azure para el tamaño máximo de blob en bloques</span><span class="sxs-lookup"><span data-stu-id="b7664-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="b7664-164">
<sup>2</sup> Incluye archivos de recursos y variables de entorno</span><span class="sxs-lookup"><span data-stu-id="b7664-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="b7664-165">Visualización de las cuotas de Lote</span><span class="sxs-lookup"><span data-stu-id="b7664-165">View Batch quotas</span></span>
<span data-ttu-id="b7664-166">Ver las cuotas de la cuenta de lote en hello [portal de Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="b7664-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="b7664-167">Seleccione **por lotes cuentas** en el portal de hello, a continuación, seleccione cuenta de lote de Hola que le interesa.</span><span class="sxs-lookup"><span data-stu-id="b7664-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="b7664-168">Seleccione **propiedades** en la hoja de menú de la cuenta de hello por lotes.</span><span class="sxs-lookup"><span data-stu-id="b7664-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="b7664-169">hoja de propiedades de Hello muestra hello **cuotas** aplicados actualmente toohello cuenta de lote</span><span class="sxs-lookup"><span data-stu-id="b7664-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Cuotas de la cuenta de Lote][account_quotas]

<span data-ttu-id="b7664-171">Una cuenta de lote que se crea en modo de suscripción de usuario, Hola vista relacionado con las cuotas de suscripción en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7664-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="b7664-172">Seleccione **suscripciones**y seleccione la suscripción de Hola que estás usando para hello cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="b7664-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="b7664-173">En hello **suscripción** hoja, seleccione **uso + cuotas**.</span><span class="sxs-lookup"><span data-stu-id="b7664-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="b7664-174">Aumento de la cuota</span><span class="sxs-lookup"><span data-stu-id="b7664-174">Increase a quota</span></span>
<span data-ttu-id="b7664-175">Siga estos toorequest pasos aumentar una cuota para su cuenta de lote o en la suscripción con hello [portal de Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="b7664-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="b7664-176">tipo de Hola de aumento de la cuota depende de modo de asignación de grupo de Hola de su cuenta de lote.</span><span class="sxs-lookup"><span data-stu-id="b7664-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="b7664-177">Aumento de la cuota de núcleos de Batch</span><span class="sxs-lookup"><span data-stu-id="b7664-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="b7664-178">Si se creó su cuenta de lote en **por lotes servicio** modo, siga estas toorequest pasos aumento de la cuota de núcleos de proceso por lotes:</span><span class="sxs-lookup"><span data-stu-id="b7664-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="b7664-179">Seleccione hello **ayuda y soporte técnico** icono en el panel del portal u Hola signo de interrogación (**?**) en la esquina superior derecha de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7664-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="b7664-180">Seleccione **Nueva solicitud de soporte técnico** > **Básico**.</span><span class="sxs-lookup"><span data-stu-id="b7664-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="b7664-181">En hello **Fundamentos** hoja:</span><span class="sxs-lookup"><span data-stu-id="b7664-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="b7664-182">a.</span><span class="sxs-lookup"><span data-stu-id="b7664-182">a.</span></span> <span data-ttu-id="b7664-183">**Tipo de problema** > **Cuota**</span><span class="sxs-lookup"><span data-stu-id="b7664-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="b7664-184">b.</span><span class="sxs-lookup"><span data-stu-id="b7664-184">b.</span></span> <span data-ttu-id="b7664-185">Seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="b7664-185">Select your subscription.</span></span>
   
    <span data-ttu-id="b7664-186">c.</span><span class="sxs-lookup"><span data-stu-id="b7664-186">c.</span></span> <span data-ttu-id="b7664-187">**Tipo de cuota** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="b7664-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="b7664-188">d.</span><span class="sxs-lookup"><span data-stu-id="b7664-188">d.</span></span> <span data-ttu-id="b7664-189">**Plan de soporte técnico** > **Compatibilidad con cuotas (incluida)**</span><span class="sxs-lookup"><span data-stu-id="b7664-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="b7664-190">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b7664-190">Click **Next**.</span></span>
4. <span data-ttu-id="b7664-191">En hello **problema** hoja:</span><span class="sxs-lookup"><span data-stu-id="b7664-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="b7664-192">a.</span><span class="sxs-lookup"><span data-stu-id="b7664-192">a.</span></span> <span data-ttu-id="b7664-193">Seleccione un **gravedad** según tooyour [impacto para la empresa][support_sev].</span><span class="sxs-lookup"><span data-stu-id="b7664-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="b7664-194">b.</span><span class="sxs-lookup"><span data-stu-id="b7664-194">b.</span></span> <span data-ttu-id="b7664-195">En **detalles**, especifique cada cuota que desea toochange, nombre de cuenta de lote de Hola y límite nuevo Hola.</span><span class="sxs-lookup"><span data-stu-id="b7664-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="b7664-196">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b7664-196">Click **Next**.</span></span>
5. <span data-ttu-id="b7664-197">En hello **información de contacto** hoja:</span><span class="sxs-lookup"><span data-stu-id="b7664-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="b7664-198">a.</span><span class="sxs-lookup"><span data-stu-id="b7664-198">a.</span></span> <span data-ttu-id="b7664-199">Seleccione un valor en **Método de contacto preferido**.</span><span class="sxs-lookup"><span data-stu-id="b7664-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="b7664-200">b.</span><span class="sxs-lookup"><span data-stu-id="b7664-200">b.</span></span> <span data-ttu-id="b7664-201">Compruebe y escriba los detalles de contacto de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="b7664-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="b7664-202">Haga clic en **crear** solicitud de soporte técnico de toosubmit Hola.</span><span class="sxs-lookup"><span data-stu-id="b7664-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="b7664-203">Una vez que haya enviado la solicitud de soporte técnico, el servicio de soporte técnico de Azure se comunicará con usted.</span><span class="sxs-lookup"><span data-stu-id="b7664-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="b7664-204">Tenga en cuenta que la finalización de la solicitud de Hola puede tardar hasta días laborables de too2.</span><span class="sxs-lookup"><span data-stu-id="b7664-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="b7664-205">Aumento de una cuota de núcleos de suscripción</span><span class="sxs-lookup"><span data-stu-id="b7664-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="b7664-206">Si su cuenta de Batch se creó en el modo de **suscripción de usuario** y necesita más núcleos regionales o de familia de máquina virtual, solicite un aumento de la cuota en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="b7664-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="b7664-207">Para ver los pasos, consulte [Solicitudes de aumento de cuota de núcleos de Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="b7664-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="b7664-208">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="b7664-208">Related topics</span></span>
* [<span data-ttu-id="b7664-209">Crear una cuenta de Azure Batch mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b7664-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="b7664-210">Información general de las características de Lote de Azure</span><span class="sxs-lookup"><span data-stu-id="b7664-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="b7664-211">Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b7664-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
