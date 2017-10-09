---
title: aaaUse toomanage portal Azure recursos de Azure | Documentos de Microsoft
description: "Usar el portal de Azure y administración de recursos de Azure toomanage los recursos. Muestra cómo toowork con recursos de toomonitor de paneles."
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
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="d3b5c-104">Administración de los recursos de Azure a través del Portal</span><span class="sxs-lookup"><span data-stu-id="d3b5c-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3b5c-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b5c-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="d3b5c-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d3b5c-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="d3b5c-107">Portal</span><span class="sxs-lookup"><span data-stu-id="d3b5c-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="d3b5c-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="d3b5c-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="d3b5c-109">Este tema se muestra cómo hello toouse [portal de Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toomanage los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="d3b5c-110">toolearn acerca de cómo implementar los recursos a través del portal de hello, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="d3b5c-111">Actualmente, no todos los servicios es compatible con el portal de Hola o administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="d3b5c-112">Para esos servicios, deberá hello toouse [portal clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="d3b5c-113">Para el estado de Hola de cada servicio, consulte [gráfico de disponibilidad de portal de Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="d3b5c-114">Administración de grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-114">Manage resource groups</span></span>

<span data-ttu-id="d3b5c-115">Un grupo de recursos es un contenedor que almacena los recursos relacionados con una solución de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="d3b5c-116">grupo de recursos de Hello puede incluir todos los recursos de hello para la solución de hello, o sólo aquellos recursos que desea toomanage como un grupo.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="d3b5c-117">Decida cómo desea que los recursos de tooallocate tooresource grupos basan en lo que le resulte hello más conveniente para su organización.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="d3b5c-118">Por lo general, agregar recursos que comparten Hola mismo toohello de ciclo de vida mismo recurso de grupo para fácilmente puede implementar, actualizar y eliminar como un grupo.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="d3b5c-119">grupo de recursos de Hello almacena metadatos acerca de los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="d3b5c-120">Por lo tanto, cuando se especifica una ubicación para el grupo de recursos de hello, está especificando donde se almacenan los metadatos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="d3b5c-121">Por motivos de cumplimiento, puede que necesite tooensure que se almacenan los datos en una región determinada.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="d3b5c-122">toosee todos los grupos de recursos de hello en su suscripción, seleccione **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![buscar grupos de recursos](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="d3b5c-124">Seleccione un grupo de recursos vacío, toocreate **agregar**.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![agregar grupo de recursos](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="d3b5c-126">Proporcione un nombre y ubicación para el nuevo grupo de recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="d3b5c-127">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-127">Select **Create**.</span></span>
   
    ![Creación de un grupo de recursos](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="d3b5c-129">Puede que necesite tooselect **actualizar** grupo de recursos de toosee Hola creado recientemente.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![actualizar grupo de recursos](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="d3b5c-131">toocustomize Hola muestre la información de los grupos de recursos, seleccione **columnas**.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personalizar columnas](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="d3b5c-133">Seleccione Hola columnas tooadd y, a continuación, seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![agregar columnas](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="d3b5c-135">toolearn acerca de cómo implementar recursos tooyour nuevo grupo de recursos, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="d3b5c-136">Para el grupo de recursos de tooa de acceso rápido, puede anclar panel tooyour de hello hoja.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![anclar un grupo de recursos](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="d3b5c-138">panel de Hello muestra el grupo de recursos de Hola y sus recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="d3b5c-139">Puede seleccionar los grupos de recursos de Hola o cualquiera de sus elementos de toohello toonavigate de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![anclar un grupo de recursos](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="d3b5c-141">Etiquetado de recursos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-141">Tag resources</span></span>
<span data-ttu-id="d3b5c-142">Puede aplicar etiquetas tooresource grupos y recursos toologically organizar sus recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="d3b5c-143">Para obtener información sobre cómo trabajar con etiquetas, consulte [mediante etiquetas tooorganize los recursos de Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="d3b5c-144">Supervisión de recursos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-144">Monitor resources</span></span>
<span data-ttu-id="d3b5c-145">Cuando seleccione un recurso, hoja de recursos de hello presenta predeterminado gráficos y tablas para la supervisión de ese tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="d3b5c-146">Seleccione un recurso y observe hello **supervisión** sección.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="d3b5c-147">Incluye gráficos que son el tipo de recurso toohello relevante.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="d3b5c-148">Hello siguiente imagen muestra la Hola predeterminada datos de supervisión de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![mostrar supervisión](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="d3b5c-150">Puede anclar una sección del panel de hello hoja tooyour seleccionando puntos suspensivos de hello (...) por encima de la sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="d3b5c-151">También puede personalizar la sección de Hola Hola tamaño en la hoja de Hola o quitarlo completamente.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="d3b5c-152">Hello siguiente imagen muestra cómo personalizar toopin, o quitar la sección de memoria y CPU Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![anclar sección](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="d3b5c-154">Después de anclar el panel de toohello sección hello, verá Hola resumen en el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="d3b5c-155">Y, si lo selecciona inmediatamente tardarán toomore detalles acerca de los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![ver panel](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="d3b5c-157">toocompletely personalizar datos de Hola para supervisar a través del portal de hello, vaya a Panel de tooyour predeterminado y seleccione **nuevo panel**.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="d3b5c-159">Asigne un nombre a su nuevo panel y arrastre iconos de panel Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="d3b5c-160">Hola mosaicos se filtran por distintas opciones.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-160">hello tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="d3b5c-162">toolearn acerca de cómo trabajar con los paneles, consulte [crear y compartir paneles en el portal de Azure hello](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="d3b5c-163">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-163">Manage resources</span></span>
<span data-ttu-id="d3b5c-164">En la hoja de Hola para un recurso, verá opciones de Hola para administrar recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="d3b5c-165">portal de Hello presenta opciones de administración para ese tipo de recurso determinado.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="d3b5c-166">Vea los comandos de administración de Hola a través de la parte superior de Hola de hoja de recursos de Hola y en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Administración de recursos](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="d3b5c-168">En estas opciones, puede realizar operaciones como iniciar y detener una máquina virtual o volver a configurar las propiedades de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="d3b5c-169">Traslado de recursos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-169">Move resources</span></span>
<span data-ttu-id="d3b5c-170">Si tiene otra suscripción o grupo de recursos de toomove recursos tooanother, consulte [Mover grupo de recursos de toonew de recursos o suscripción](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="d3b5c-171">Bloqueo de recursos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-171">Lock resources</span></span>
<span data-ttu-id="d3b5c-172">Se pueden bloquear una suscripción, el grupo de recursos o el recurso tooprevent otros usuarios de su organización accidentalmente eliminen o modifiquen los recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="d3b5c-173">Para obtener más información, consulte [Bloqueo de recursos con el Administrador de recursos de Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="d3b5c-174">Consulta de sus datos de suscripción y costos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-174">View your subscription and costs</span></span>
<span data-ttu-id="d3b5c-175">Puede ver información acerca de su suscripción y los costos de hello consolidadas para todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="d3b5c-176">Seleccione **suscripciones** y suscripción de Hola que desea toosee.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="d3b5c-177">Solo tendrá una tooselect de suscripción.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-177">You might only have one subscription tooselect.</span></span>

![suscripción](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="d3b5c-179">En la hoja de la suscripción de hello, verá una tasa de avance.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-179">Within hello subscription blade, you see a burn rate.</span></span>

![tasa de evolución](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="d3b5c-181">Y un desglose de costos por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-181">And, a breakdown of costs by resource type.</span></span>

![costo de recursos](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="d3b5c-183">Exportación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="d3b5c-183">Export template</span></span>
<span data-ttu-id="d3b5c-184">Después de configurar el grupo de recursos, puede que desee plantilla de administrador de recursos de tooview Hola Hola para grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="d3b5c-185">Exportar plantilla Hola ofrece dos ventajas:</span><span class="sxs-lookup"><span data-stu-id="d3b5c-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="d3b5c-186">Puede automatizar fácilmente las futuras implementaciones de soluciones de hello como plantilla de hello contiene toda la infraestructura de hello todos los.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="d3b5c-187">Familiarícese con la sintaxis de plantilla examinando Hola JavaScript Object Notation (JSON) que representa la solución.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="d3b5c-188">Para obtener instrucciones detalladas, consulte [Exportación de plantillas de Azure Resource Manager desde recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="d3b5c-189">Eliminación de los recursos o grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="d3b5c-189">Delete resource group or resources</span></span>
<span data-ttu-id="d3b5c-190">Eliminar un grupo de recursos, elimina todos los recursos de hello incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="d3b5c-191">También puede eliminar recursos individuales de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="d3b5c-192">Desea tooexercise cuidado al eliminar un grupo de recursos porque podría haber recursos en otros grupos de recursos que están vinculado tooit.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="d3b5c-193">El Administrador de recursos no se eliminan los recursos vinculados, pero no pueden funcionar correctamente sin recursos Hola esperado.</span><span class="sxs-lookup"><span data-stu-id="d3b5c-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![eliminar grupo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="d3b5c-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3b5c-195">Next steps</span></span>
* <span data-ttu-id="d3b5c-196">registros de actividad de tooview, consulte [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="d3b5c-197">tooview obtener información detallada acerca de una implementación, vea [ver las operaciones de implementación](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="d3b5c-198">toodeploy recursos a través del portal de hello, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="d3b5c-199">toomanage tooresources de acceso, consulte [usar recursos de suscripción de Azure de rol asignaciones toomanage acceso tooyour](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="d3b5c-200">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d3b5c-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

