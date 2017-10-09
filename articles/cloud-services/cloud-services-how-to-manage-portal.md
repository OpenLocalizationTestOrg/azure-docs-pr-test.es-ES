---
title: "tareas de administración de servicio de nube aaaCommon | Documentos de Microsoft"
description: "Obtenga información acerca de cómo servicios en la nube toomanage Hola portal de Azure. Estos ejemplos utilizan Hola portal de Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="fd94d-104">Cómo tooManage los servicios de nube</span><span class="sxs-lookup"><span data-stu-id="fd94d-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd94d-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fd94d-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="fd94d-106">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="fd94d-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="fd94d-107">Hola **servicios en la nube (clásico)** área no cliente de hello Azure portal, puede actualizar un rol de servicio o una implementación, promover una implementación de ensayo tooproduction, vincular servicio de recursos tooyour en la nube para que puedan ver recursos de Hola dependencias y la escala Hola recursos juntos y eliminar un servicio de nube o una implementación.</span><span class="sxs-lookup"><span data-stu-id="fd94d-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="fd94d-108">Para obtener más información acerca de cómo tooscale su servicio de nube disponible [aquí](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd94d-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="fd94d-109">Actualización del rol de servicio en la nube o implementación</span><span class="sxs-lookup"><span data-stu-id="fd94d-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="fd94d-110">Si tiene código de la aplicación hello tooupdate para su servicio en la nube, use **actualización** en el módulo de servicio de nube Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="fd94d-111">Puede actualizar un solo rol o todos los roles.</span><span class="sxs-lookup"><span data-stu-id="fd94d-111">You can update a single role or all roles.</span></span> <span data-ttu-id="fd94d-112">tooupdate, puede cargar un nuevo paquete de servicio o un archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="fd94d-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="fd94d-113">Hola [portal de Azure][Azure portal], seleccione servicio de nube de Hola que desee tooupdate.</span><span class="sxs-lookup"><span data-stu-id="fd94d-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="fd94d-114">Este paso abre una hoja de instancia de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="fd94d-115">En la hoja de hello, haga clic en hello **actualización** botón.</span><span class="sxs-lookup"><span data-stu-id="fd94d-115">In hello blade, click hello **Update** button.</span></span>

    ![Botón Actualizar](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="fd94d-117">Implementación de Hola de actualización con un nuevo archivo de paquete de servicio (.cspkg) y el archivo de configuración de servicio (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="fd94d-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![Implementación de actualizaciones](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="fd94d-119">**Si lo desea** actualizar la etiqueta de implementación de Hola y cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="fd94d-120">Si los roles tienen solo una instancia de rol, seleccione hello **implementar aunque uno o varios roles contengan una sola instancia** tooenable Hola actualización tooproceed.</span><span class="sxs-lookup"><span data-stu-id="fd94d-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="fd94d-121">Azure solo puede garantizar un 99,95 % de disponibilidad del servicio durante una actualización del servicio en la nube si cada rol tiene al menos dos instancias de rol (máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="fd94d-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="fd94d-122">Con dos instancias de rol, una máquina virtual procesa las solicitudes de cliente mientras se actualiza Hola otro.</span><span class="sxs-lookup"><span data-stu-id="fd94d-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="fd94d-123">Comprobar **comience** actualización de hello toohave aplicada una vez finalizada la carga de hello del paquete de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="fd94d-124">Haga clic en **Aceptar** toobegin Actualizar servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="fd94d-125">Cómo: intercambiar implementaciones toopromote un tooproduction de implementación de ensayo</span><span class="sxs-lookup"><span data-stu-id="fd94d-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="fd94d-126">Al decidir toodeploy una nueva versión de un servicio de nube, fase y probar la nueva versión en su entorno de ensayo del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="fd94d-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="fd94d-127">Use **intercambiar** tooswitch hello las direcciones URL por qué Hola dos implementaciones se direccionan y promoción un nuevo tooproduction de versión.</span><span class="sxs-lookup"><span data-stu-id="fd94d-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="fd94d-128">Puede intercambiar las implementaciones de hello **servicios en la nube** panel página u Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="fd94d-129">Hola [portal de Azure][Azure portal], seleccione servicio de nube de Hola que desee tooupdate.</span><span class="sxs-lookup"><span data-stu-id="fd94d-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="fd94d-130">Este paso abre una hoja de instancia de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="fd94d-131">En la hoja de hello, haga clic en hello **intercambiar** botón.</span><span class="sxs-lookup"><span data-stu-id="fd94d-131">In hello blade, click hello **Swap** button.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="fd94d-133">Hello siguiente aviso de confirmación se abre.</span><span class="sxs-lookup"><span data-stu-id="fd94d-133">hello following confirmation prompt opens.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="fd94d-135">Después de comprobar la información de implementación de hello, haga clic en **Aceptar** las implementaciones de hello tooswap.</span><span class="sxs-lookup"><span data-stu-id="fd94d-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="fd94d-136">intercambio de implementación de Hello rápidamente sucede porque Hola única que cambia es hello las direcciones IP virtuales (VIP) para las implementaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="fd94d-137">toosave gastos de proceso, puede eliminar Hola implementación de ensayo después de comprobar que la implementación de producción funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="fd94d-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="fd94d-138">Preguntas comunes sobre el intercambio de implementaciones</span><span class="sxs-lookup"><span data-stu-id="fd94d-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="fd94d-139">**¿Cuáles son los requisitos previos de hello para el intercambio de las implementaciones?**</span><span class="sxs-lookup"><span data-stu-id="fd94d-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="fd94d-140">Existen principalmente dos requisitos previos para que el intercambio de implementación se realice de manera correcta:</span><span class="sxs-lookup"><span data-stu-id="fd94d-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="fd94d-141">Si desea que toouse una dirección IP estática para la zona de producción, debe reservar uno para la zona de ensayo.</span><span class="sxs-lookup"><span data-stu-id="fd94d-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="fd94d-142">En caso contrario, se produce un error en el intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="fd94d-143">Todas las instancias de los roles se deben ejecutar para poder realizar intercambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="fd94d-144">Puede comprobar estado de Hola de sus instancias de la hoja de información general de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="fd94d-145">Como alternativa, puede usar hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) comando en Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd94d-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="fd94d-146">Tenga en cuenta que las actualizaciones de SO invitado y la recuperación de las operaciones del servicio también puede producir la implementación intercambia toofail.</span><span class="sxs-lookup"><span data-stu-id="fd94d-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="fd94d-147">Para más información, consulte [Solución de problemas de implementación de servicios en la nube](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="fd94d-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="fd94d-148">**¿Un intercambio conlleva tiempo de inactividad de mi aplicación? ¿Cómo puedo controlarlo?**</span><span class="sxs-lookup"><span data-stu-id="fd94d-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="fd94d-149">Como se describe en la última sección de hello, un intercambio de implementación es suele ser muy rápido porque es un cambio de configuración de equilibrador de carga de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="fd94d-150">Sin embargo, en algunos casos, puede tardar diez o más segundos y dar lugar a errores de conexión transitorios.</span><span class="sxs-lookup"><span data-stu-id="fd94d-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="fd94d-151">los clientes de toolimit impacto tooyour, considere la posibilidad de implementar [lógica de reintento de cliente](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="fd94d-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="fd94d-152">Cómo: vincular un servicio de nube de tooa de recursos</span><span class="sxs-lookup"><span data-stu-id="fd94d-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="fd94d-153">Hola portal de Azure no incluye vínculos a recursos conjuntamente como Hola actual portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="fd94d-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="fd94d-154">En lugar de implementar recursos adicionales toohello mismo grupo de recursos usándola Hola servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fd94d-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="fd94d-155">Eliminación de implementaciones y un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="fd94d-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="fd94d-156">Antes de que pueda eliminar un servicio en la nube, debe eliminar cada implementación existente.</span><span class="sxs-lookup"><span data-stu-id="fd94d-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="fd94d-157">toosave gastos de proceso, puede eliminar Hola implementación de ensayo después de comprobar que la implementación de producción funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="fd94d-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="fd94d-158">Se le facturarán los costos de proceso de las instancias de rol implementadas que se detengan.</span><span class="sxs-lookup"><span data-stu-id="fd94d-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="fd94d-159">Usar hello siguiendo el procedimiento toodelete una implementación o servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fd94d-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="fd94d-160">Hola [portal de Azure][Azure portal], seleccione servicio de nube de Hola que desee toodelete.</span><span class="sxs-lookup"><span data-stu-id="fd94d-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="fd94d-161">Este paso abre una hoja de instancia de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="fd94d-162">En la hoja de hello, haga clic en hello **eliminar** botón.</span><span class="sxs-lookup"><span data-stu-id="fd94d-162">In hello blade, click hello **Delete** button.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="fd94d-164">Puede eliminar el servicio en la nube todo Hola activando **servicio y sus implementaciones de nube** o elija cualquier hello **implementación de producción** o hello **implementación de ensayo**.</span><span class="sxs-lookup"><span data-stu-id="fd94d-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="fd94d-166">Haga clic en hello **eliminar** situado en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="fd94d-167">servicio de nube de hello toodelete, haga clic en **servicio en la nube Delete**.</span><span class="sxs-lookup"><span data-stu-id="fd94d-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="fd94d-168">A continuación, en el mensaje de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="fd94d-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-169">Cuando se elimina un servicio de nube y se configura la supervisión detallada, debe eliminar manualmente los datos de Hola desde su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fd94d-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="fd94d-170">Para obtener información sobre dónde toofind Hola tablas de métricas, vea [esto](cloud-services-how-to-monitor.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="fd94d-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="fd94d-171">Búsqueda de más información acerca de las implementaciones con errores</span><span class="sxs-lookup"><span data-stu-id="fd94d-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="fd94d-172">Hola **Introducción** hoja tiene una barra de estado en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd94d-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="fd94d-173">Al hacer clic en la barra de hello, una nueva hoja se abre y muestra cualquier información de error.</span><span class="sxs-lookup"><span data-stu-id="fd94d-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="fd94d-174">Si la implementación de hello no contiene los errores, hoja de información de hello está en blanco.</span><span class="sxs-lookup"><span data-stu-id="fd94d-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="fd94d-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd94d-176">Next steps</span></span>
* <span data-ttu-id="fd94d-177">[Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd94d-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="fd94d-178">Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd94d-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="fd94d-179">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd94d-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="fd94d-180">Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd94d-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
