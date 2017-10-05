---
title: Uso de Azure Portal para administrar los recursos de Azure | Microsoft Docs
description: "Uso del Portal de Azure y de Azure Resource Manager para implementar los recursos. Muestra cómo trabajar con paneles para supervisar recursos."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 7a94fd5065de93384460e851627a9813d439956b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="dd619-104">Administración de los recursos de Azure a través del Portal</span><span class="sxs-lookup"><span data-stu-id="dd619-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd619-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd619-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="dd619-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dd619-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="dd619-107">Portal</span><span class="sxs-lookup"><span data-stu-id="dd619-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="dd619-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="dd619-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="dd619-109">En este tema se muestra cómo utilizar el [Azure Portal](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) para administrar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd619-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="dd619-110">Para aprender sobre la implementación de recursos a través del Portal, consulte [Implementación de recursos con las plantillas de Resource Manager y el Portal de Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="dd619-111">Actualmente, no todos los servicios son compatibles con el portal o con el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="dd619-112">Para esos servicios, deberá usar el [portal clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="dd619-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="dd619-113">Para más información sobre el estado de cada servicio, consulte [Tabla de disponibilidad de los portales de Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="dd619-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="dd619-114">Administración de grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="dd619-114">Manage resource groups</span></span>

<span data-ttu-id="dd619-115">Un grupo de recursos es un contenedor que almacena los recursos relacionados con una solución de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd619-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="dd619-116">El grupo de recursos puede incluir todos los recursos de la solución o solo aquellos que se desean administrar como grupo.</span><span class="sxs-lookup"><span data-stu-id="dd619-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="dd619-117">Para decidir cómo asignar los recursos a los grupos de recursos, tenga en cuenta lo que más conviene a su organización.</span><span class="sxs-lookup"><span data-stu-id="dd619-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="dd619-118">Por lo general, se recomienda agregar recursos que compartan el mismo ciclo de vida al mismo grupo de recursos para que los pueda implementar, actualizar y eliminar con facilidad como un grupo.</span><span class="sxs-lookup"><span data-stu-id="dd619-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="dd619-119">Los grupos de recursos almacenan metadatos acerca de los recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="dd619-120">Por consiguiente, al especificar la ubicación del grupo de recursos, se especifica el lugar en que se almacenan dichos metadatos.</span><span class="sxs-lookup"><span data-stu-id="dd619-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="dd619-121">Por motivos de compatibilidad, es posible que sea preciso asegurarse de que los datos se almacenan en una región concreta.</span><span class="sxs-lookup"><span data-stu-id="dd619-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="dd619-122">Para ver todos los grupos de recursos de su suscripción, seleccione **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="dd619-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![buscar grupos de recursos](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="dd619-124">Seleccione **Agregar**para crear un grupo de recursos vacío.</span><span class="sxs-lookup"><span data-stu-id="dd619-124">To create an empty resource group, select **Add**.</span></span>
   
    ![agregar grupo de recursos](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="dd619-126">Proporcione un nombre y una ubicación para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="dd619-127">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dd619-127">Select **Create**.</span></span>
   
    ![crear grupo de recursos](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="dd619-129">Debe seleccionar **Actualizar** para ver el grupo de recursos creado recientemente.</span><span class="sxs-lookup"><span data-stu-id="dd619-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![actualizar grupo de recursos](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="dd619-131">Para personalizar la información que se muestra para los grupos de recursos, seleccione **Columnas**.</span><span class="sxs-lookup"><span data-stu-id="dd619-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personalizar columnas](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="dd619-133">Seleccione las columnas que desea agregar y, después, seleccione **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="dd619-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![agregar columnas](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="dd619-135">Si quiere aprender cómo implementar recursos en su nuevo grupo de recursos, consulte [Implementación de recursos con las plantillas de Resource Manager y el Portal de Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="dd619-136">Para obtener un acceso rápido al grupo de recursos, puede anclar la hoja en el panel.</span><span class="sxs-lookup"><span data-stu-id="dd619-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![anclar un grupo de recursos](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="dd619-138">El panel muestra el grupo de recursos y sus recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="dd619-139">Puede seleccionar los grupos de recursos o cualquiera de sus recursos para navegar hasta el elemento.</span><span class="sxs-lookup"><span data-stu-id="dd619-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![anclar un grupo de recursos](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="dd619-141">Etiquetado de recursos</span><span class="sxs-lookup"><span data-stu-id="dd619-141">Tag resources</span></span>
<span data-ttu-id="dd619-142">Puede aplicar etiquetas a los recursos y grupos de recursos para organizar de manera lógica los recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="dd619-143">Para más información sobre cómo trabajar con etiquetas, consulte [Uso de etiquetas para organizar los recursos de Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="dd619-144">Supervisión de recursos</span><span class="sxs-lookup"><span data-stu-id="dd619-144">Monitor resources</span></span>
<span data-ttu-id="dd619-145">Cuando se selecciona un recurso, la hoja del recurso presenta los gráficos y las tablas predeterminados para supervisar ese tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="dd619-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="dd619-146">Seleccione un recurso y observe la sección **Supervisión** .</span><span class="sxs-lookup"><span data-stu-id="dd619-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="dd619-147">Incluye gráficos que son pertinentes para el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="dd619-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="dd619-148">En la imagen siguiente se muestran los datos de supervisión predeterminados para una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dd619-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![mostrar supervisión](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="dd619-150">Para anclar una sección de la hoja al panel, seleccione el botón de puntos suspensivos (...) que se encuentra encima de la sección.</span><span class="sxs-lookup"><span data-stu-id="dd619-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="dd619-151">Asimismo puede personalizar el tamaño de la sección en la hoja o quitarlo.</span><span class="sxs-lookup"><span data-stu-id="dd619-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="dd619-152">La siguiente imagen muestra cómo anclar, personalizar o quitar la sección CPU y memoria.</span><span class="sxs-lookup"><span data-stu-id="dd619-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![anclar sección](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="dd619-154">Después de anclar la sección en el panel, verá el resumen en el panel.</span><span class="sxs-lookup"><span data-stu-id="dd619-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="dd619-155">Y, si lo selecciona inmediatamente, obtendrá más detalles de los datos.</span><span class="sxs-lookup"><span data-stu-id="dd619-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![ver panel](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="dd619-157">Para personalizar completamente los datos que supervisa mediante el portal, vaya al panel predeterminado y seleccione **Nuevo panel**.</span><span class="sxs-lookup"><span data-stu-id="dd619-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="dd619-159">Asigne un nombre al nuevo panel y arrastre hasta ahí los iconos.</span><span class="sxs-lookup"><span data-stu-id="dd619-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="dd619-160">Los iconos se filtran por distintas opciones.</span><span class="sxs-lookup"><span data-stu-id="dd619-160">The tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="dd619-162">Para aprender a trabajar con paneles, vea el vídeo [Creación y uso compartido de paneles en Azure Portal](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="dd619-163">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="dd619-163">Manage resources</span></span>
<span data-ttu-id="dd619-164">En la hoja de un recurso, verá las opciones para administrar el recurso.</span><span class="sxs-lookup"><span data-stu-id="dd619-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="dd619-165">El portal presenta opciones de administración para ese tipo de recurso en particular.</span><span class="sxs-lookup"><span data-stu-id="dd619-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="dd619-166">Verá los comandos de administración en la parte superior de la hoja de recursos y en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="dd619-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![Administración de recursos](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="dd619-168">Desde estas opciones, puede realizar operaciones como iniciar y detener una máquina virtual o volver a configurar las propiedades de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dd619-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="dd619-169">Traslado de recursos</span><span class="sxs-lookup"><span data-stu-id="dd619-169">Move resources</span></span>
<span data-ttu-id="dd619-170">Si necesita trasladar un recurso a otro grupo de recursos u otra suscripción, consulte [Traslado de los recursos a un nuevo grupo de recursos o a una nueva suscripción](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="dd619-171">Bloqueo de recursos</span><span class="sxs-lookup"><span data-stu-id="dd619-171">Lock resources</span></span>
<span data-ttu-id="dd619-172">Puede bloquear una suscripción, un grupo de recursos o un recurso para impedir que otros usuarios de su organización eliminen o modifiquen por error recursos esenciales.</span><span class="sxs-lookup"><span data-stu-id="dd619-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="dd619-173">Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="dd619-174">Consulta de sus datos de suscripción y costos</span><span class="sxs-lookup"><span data-stu-id="dd619-174">View your subscription and costs</span></span>
<span data-ttu-id="dd619-175">Puede ver información acerca de la suscripción y los costos acumulados de todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="dd619-176">Seleccione **Suscripciones** y la suscripción que quiere ver.</span><span class="sxs-lookup"><span data-stu-id="dd619-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="dd619-177">Es posible que solo tenga una suscripción para seleccionar.</span><span class="sxs-lookup"><span data-stu-id="dd619-177">You might only have one subscription to select.</span></span>

![suscripción](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="dd619-179">En la hoja de suscripciones, verá una tasa de evolución.</span><span class="sxs-lookup"><span data-stu-id="dd619-179">Within the subscription blade, you see a burn rate.</span></span>

![tasa de evolución](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="dd619-181">Y un desglose de costos por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="dd619-181">And, a breakdown of costs by resource type.</span></span>

![costo de recursos](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="dd619-183">Exportación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="dd619-183">Export template</span></span>
<span data-ttu-id="dd619-184">Después de configurar el grupo de recursos, quizás quiera ver la plantilla de Resource Manager para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="dd619-185">Exportar la plantilla ofrece dos ventajas:</span><span class="sxs-lookup"><span data-stu-id="dd619-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="dd619-186">Puede automatizar fácilmente las futuras implementaciones de la solución porque la plantilla contiene la infraestructura completa.</span><span class="sxs-lookup"><span data-stu-id="dd619-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="dd619-187">Para familiarizarse con la sintaxis de la plantilla, consulte la notación de objetos JavaScript (JSON) que representa la solución.</span><span class="sxs-lookup"><span data-stu-id="dd619-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="dd619-188">Para obtener instrucciones detalladas, consulte [Exportación de plantillas de Azure Resource Manager desde recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="dd619-189">Eliminación de los recursos o grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="dd619-189">Delete resource group or resources</span></span>
<span data-ttu-id="dd619-190">Al eliminar un grupo de recursos se eliminan todos los recursos contenidos en el mismo.</span><span class="sxs-lookup"><span data-stu-id="dd619-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="dd619-191">También puede eliminar recursos individuales de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="dd619-192">Debe prestar atención cuando elimine un grupo de recursos porque podría haber recursos vinculados a él en otros grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd619-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="dd619-193">Resource Manager no elimina los recursos vinculados, pero podrían no funcionar correctamente sin los recursos esperados.</span><span class="sxs-lookup"><span data-stu-id="dd619-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![eliminar grupo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="dd619-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd619-195">Next steps</span></span>
* <span data-ttu-id="dd619-196">Para ver los registros de auditoría, consulte el artículo sobre [operaciones de auditoría con Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="dd619-197">Para ver detalles acerca de una implementación, consulte [View deployment operations](resource-manager-deployment-operations.md) (Ver operaciones de implementación).</span><span class="sxs-lookup"><span data-stu-id="dd619-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="dd619-198">Para implementar recursos mediante el Portal, consulte [Implementación de recursos con las plantillas de Resource Manager y el Portal de Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="dd619-199">Para administrar el acceso a los recursos, consulte [Uso de asignaciones de roles para administrar el acceso a los recursos de la suscripción de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="dd619-200">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="dd619-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

