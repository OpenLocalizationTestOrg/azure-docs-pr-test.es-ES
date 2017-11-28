---
title: "Tareas de administración de servicios en la nube comunes | Microsoft Docs"
description: "Vea cómo administrar servicios en la nube en el Portal de Azure. Estos ejemplos usan el Portal de Azure."
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
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="c9bc7-104">Administración de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="c9bc7-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9bc7-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c9bc7-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="c9bc7-106">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="c9bc7-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="c9bc7-107">En el área **Cloud Services (clásico)** de Azure Portal, puede actualizar un rol de servicio o una implementación, promover una implementación de ensayo en producción, vincular recursos con su servicio en la nube para que pueda ver las dependencias de estos y escalar los recursos juntos, además de eliminar un servicio en la nube o una implementación.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="c9bc7-108">Para obtener más información sobre cómo escalar un servicio en la nube, haga clic [aquí](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="c9bc7-109">Actualización del rol de servicio en la nube o implementación</span><span class="sxs-lookup"><span data-stu-id="c9bc7-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="c9bc7-110">Si necesita actualizar el código de la aplicación para su servicio en la nube, use **Actualizar** en la hoja del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="c9bc7-111">Puede actualizar un solo rol o todos los roles.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-111">You can update a single role or all roles.</span></span> <span data-ttu-id="c9bc7-112">Para ello, puede cargar un nuevo paquete de servicio o un archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="c9bc7-113">En el [portal de Azure][Azure portal], seleccione el servicio en la nube que quiera actualizar.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="c9bc7-114">Tras esta acción, se abrirá la hoja de la instancia del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="c9bc7-115">En la hoja, haga clic en el botón **Actualizar** .</span><span class="sxs-lookup"><span data-stu-id="c9bc7-115">In the blade, click the **Update** button.</span></span>

    ![Botón Actualizar](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="c9bc7-117">Actualice la implementación con un nuevo archivo de paquete de servicio (.cspkg) y un archivo de configuración de servicio (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![Implementación de actualizaciones](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="c9bc7-119">**Opcionalmente** puede actualizar la etiqueta de implementación y la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="c9bc7-120">Si uno de los roles solo tiene una instancia de rol, seleccione **Implementar aunque uno o varios roles contengan una sola instancia** para permitir que la actualización continúe.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="c9bc7-121">Azure solo puede garantizar un 99,95 % de disponibilidad del servicio durante una actualización del servicio en la nube si cada rol tiene al menos dos instancias de rol (máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="c9bc7-122">Con dos instancias de rol, una máquina virtual procesa las solicitudes de cliente mientras la otra se actualiza.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="c9bc7-123">Active **Iniciar implementación** si quiere que la actualización se aplique cuando termine de cargarse el paquete.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="c9bc7-124">Haga clic en **Aceptar** para iniciar la actualización del servicio.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="c9bc7-125">Intercambio de implementaciones para pasar un servicio en la nube de ensayo a producción</span><span class="sxs-lookup"><span data-stu-id="c9bc7-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="c9bc7-126">Cuando decida implementar una nueva versión de un servicio en la nube, puede colocar en etapa y probar la nueva versión en su entorno de ensayo del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="c9bc7-127">Use **Intercambiar** para cambiar las direcciones URL que dirigen a las dos implementaciones y promover una nueva versión a producción.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="c9bc7-128">Puede intercambiar implementaciones desde la página **Servicios en la nube** o el panel.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="c9bc7-129">En el [portal de Azure][Azure portal], seleccione el servicio en la nube que quiera actualizar.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="c9bc7-130">Tras esta acción, se abrirá la hoja de la instancia del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="c9bc7-131">En la hoja, haga clic en el botón **Intercambiar** .</span><span class="sxs-lookup"><span data-stu-id="c9bc7-131">In the blade, click the **Swap** button.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="c9bc7-133">Se abre la siguiente solicitud de confirmación.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-133">The following confirmation prompt opens.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="c9bc7-135">Después de verificar la información de la implementación, haga clic en **Aceptar** para intercambiar las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="c9bc7-136">El intercambio de implementaciones ocurre rápidamente porque lo único que cambia son las direcciones IP virtuales (VIP) de las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="c9bc7-137">Para ahorrar en los costos de proceso, puede eliminar la implementación de ensayo después de comprobar que la implementación de producción funcione según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="c9bc7-138">Preguntas comunes sobre el intercambio de implementaciones</span><span class="sxs-lookup"><span data-stu-id="c9bc7-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="c9bc7-139">**¿Cuáles son los requisitos previos para el intercambio de implementaciones?**</span><span class="sxs-lookup"><span data-stu-id="c9bc7-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="c9bc7-140">Existen principalmente dos requisitos previos para que el intercambio de implementación se realice de manera correcta:</span><span class="sxs-lookup"><span data-stu-id="c9bc7-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="c9bc7-141">Si quiere usar una dirección IP estática para su ranura de producción, debe reservar también una para su ranura de ensayo.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="c9bc7-142">Si no lo hace así, se producirá un error en el intercambio.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="c9bc7-143">Todas las instancias de los roles se deben estar ejecutando para poder realizar el intercambio.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="c9bc7-144">El estado de las instancias se puede comprobar de la hoja de información general de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="c9bc7-145">Como alternativa, puede usar el comando [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="c9bc7-146">Tenga en cuenta que las actualizaciones del SO invitado y las operaciones de recuperación de servicios también pueden provocar errores en los intercambios de implementación.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="c9bc7-147">Para más información, consulte [Solución de problemas de implementación de servicios en la nube](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="c9bc7-148">**¿Un intercambio conlleva tiempo de inactividad de mi aplicación? ¿Cómo puedo controlarlo?**</span><span class="sxs-lookup"><span data-stu-id="c9bc7-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="c9bc7-149">Como se ha descrito en la última sección, un intercambio de implementación suele ser rápido, ya que no es más que un cambio de configuración en Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="c9bc7-150">Sin embargo, en algunos casos, puede tardar diez o más segundos y dar lugar a errores de conexión transitorios.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="c9bc7-151">Para limitar el impacto en los clientes, considere la posibilidad de implementar la [lógica de reintento del cliente](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="c9bc7-152">Vinculación de un recurso a un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="c9bc7-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="c9bc7-153">El Portal de Azure no vincula recursos entre sí como el Portal de Azure clásico actual.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="c9bc7-154">En su lugar, implemente más recursos en el mismo grupo de recursos que está usando el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="c9bc7-155">Eliminación de implementaciones y un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="c9bc7-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="c9bc7-156">Antes de que pueda eliminar un servicio en la nube, debe eliminar cada implementación existente.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="c9bc7-157">Para ahorrar en los costos de proceso, puede eliminar la implementación de ensayo después de comprobar que la implementación de producción funcione según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="c9bc7-158">Se le facturarán los costos de proceso de las instancias de rol implementadas que se detengan.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="c9bc7-159">Use el siguiente procedimiento para eliminar una implementación o su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="c9bc7-160">En el [portal de Azure][Azure portal], seleccione el servicio en la nube que quiera eliminar.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="c9bc7-161">Tras esta acción, se abrirá la hoja de la instancia del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="c9bc7-162">En la hoja, haga clic en el botón **Eliminar** .</span><span class="sxs-lookup"><span data-stu-id="c9bc7-162">In the blade, click the **Delete** button.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="c9bc7-164">Puede eliminar el servicio en la nube completo seleccionando **Servicio en la nube y sus implementaciones** o elija **Implementación de producción** o **Implementación de almacenamiento provisional**.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="c9bc7-166">Haga clic en el botón **Eliminar** situado en la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="c9bc7-167">Para eliminar el servicio en la nube, haga clic en **Eliminar servicio en la nube**.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="c9bc7-168">Luego, haga clic en **Sí**en la solicitud de confirmación.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="c9bc7-169">Cuando se elimina un servicio en la nube y se configura una supervisión detallada, debe eliminar manualmente los datos de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="c9bc7-170">Para obtener información sobre dónde buscar las tablas métricas, consulte [este](cloud-services-how-to-monitor.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="c9bc7-171">Búsqueda de más información acerca de las implementaciones con errores</span><span class="sxs-lookup"><span data-stu-id="c9bc7-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="c9bc7-172">La hoja **Información general** tiene una barra de estado en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="c9bc7-173">Al hacer clic en ella, se abre una nueva hoja que muestra la información de cualquier error.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="c9bc7-174">Si la implementación no contiene errores, la hoja de información está en blanco.</span><span class="sxs-lookup"><span data-stu-id="c9bc7-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Intercambio de servicios en la nube](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="c9bc7-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9bc7-176">Next steps</span></span>
* <span data-ttu-id="c9bc7-177">[Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="c9bc7-178">Obtenga información sobre cómo [implementar un servicio en la nube](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="c9bc7-179">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="c9bc7-180">Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9bc7-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
