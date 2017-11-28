---
title: Uso de Azure Portal para implementar los recursos de Azure | Microsoft Docs
description: Utilice el Portal de Azure y Azure Resource Manager para implementar los recursos.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="74f2b-103">Implementación de recursos con las plantillas de Resource Manager y el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="74f2b-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74f2b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="74f2b-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="74f2b-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="74f2b-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="74f2b-106">Portal</span><span class="sxs-lookup"><span data-stu-id="74f2b-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="74f2b-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="74f2b-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="74f2b-108">En este tema se muestra cómo utilizar [Azure Portal](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) para implementar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="74f2b-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="74f2b-109">Para obtener más información sobre cómo administrar los recursos, consulte [Administración de los recursos de Azure a través del Portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="74f2b-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="74f2b-110">Actualmente, no todos los servicios son compatibles con el portal o con el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="74f2b-111">Para esos servicios, deberá usar el [portal clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="74f2b-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="74f2b-112">Para obtener más información sobre el estado de cada servicio, consulte [Tabla de disponibilidad de los portales de Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="74f2b-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="74f2b-113">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="74f2b-113">Create resource group</span></span>
1. <span data-ttu-id="74f2b-114">Para crear un grupo de recursos vacío, seleccione **Nuevo** > **Administración** > **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="74f2b-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![crear un grupo de recursos vacío](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="74f2b-116">Asígnele un nombre y una ubicación y, si es necesario, seleccione una suscripción.</span><span class="sxs-lookup"><span data-stu-id="74f2b-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="74f2b-117">Debe proporcionar una ubicación para el grupo de recursos porque este almacena metadatos sobre los recursos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="74f2b-118">Por motivos de cumplimiento, debería especificar dónde se almacenan esos metadatos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="74f2b-119">Por lo general, se recomienda especificar una ubicación en la que vayan a residir la mayoría de los recursos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="74f2b-120">Si usa la misma ubicación, puede simplificar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="74f2b-120">Using the same location can simplify your template.</span></span>
   
    ![establecer valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="74f2b-122">Implementación de recursos desde Marketplace</span><span class="sxs-lookup"><span data-stu-id="74f2b-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="74f2b-123">Una vez creado el grupo de recursos, puede implementar recursos en él desde Marketplace.</span><span class="sxs-lookup"><span data-stu-id="74f2b-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="74f2b-124">Marketplace proporciona soluciones predefinidas para escenarios habituales.</span><span class="sxs-lookup"><span data-stu-id="74f2b-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="74f2b-125">Para iniciar la implementación, seleccione **Nuevo** y el tipo de recurso que quiere implementar.</span><span class="sxs-lookup"><span data-stu-id="74f2b-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="74f2b-126">A continuación, busque la versión concreta del recurso que le gustaría implementar.</span><span class="sxs-lookup"><span data-stu-id="74f2b-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![implementar recursos](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="74f2b-128">Si no ve la solución específica que gustaría implementar, búsquela en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="74f2b-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![buscar en Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="74f2b-130">Según el tipo del recurso seleccionado, tiene una colección de propiedades pertinentes que debe establecer antes de la implementación.</span><span class="sxs-lookup"><span data-stu-id="74f2b-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="74f2b-131">Estas opciones no se muestran aquí, dado que varía según el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="74f2b-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="74f2b-132">Para todos los tipos, debe seleccionar un grupo de recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="74f2b-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="74f2b-133">En la imagen siguiente se muestra cómo crear una aplicación web e implementarla en el grupo de recursos que ha creado.</span><span class="sxs-lookup"><span data-stu-id="74f2b-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![Creación de un grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="74f2b-135">Como alternativa, puede decidir crear un nuevo grupo de recursos al implementar estos últimos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="74f2b-136">Seleccione **Crear nuevo** y asígnele un nombre al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![crear nuevo grupo de recursos.](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="74f2b-138">Comenzará la implementación.</span><span class="sxs-lookup"><span data-stu-id="74f2b-138">Your deployment begins.</span></span> <span data-ttu-id="74f2b-139">Esta puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="74f2b-140">Cuando haya terminado la implementación, verá una notificación.</span><span class="sxs-lookup"><span data-stu-id="74f2b-140">When the deployment has finished, you see a notification.</span></span>
   
    ![ver notificación](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="74f2b-142">Después de implementar los recursos, puede agregar más recursos al grupo de recursos mediante el comando **Agregar** de la hoja del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="74f2b-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![agregar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="74f2b-144">Implementación de recursos desde plantilla personalizada</span><span class="sxs-lookup"><span data-stu-id="74f2b-144">Deploy resources from custom template</span></span>
<span data-ttu-id="74f2b-145">Si desea ejecutar una implementación sin usar las plantillas de Marketplace, puede crear una plantilla personalizada que defina la infraestructura para la solución.</span><span class="sxs-lookup"><span data-stu-id="74f2b-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="74f2b-146">Para obtener más información sobre la creación de plantillas, vea [Creación de plantillas del Administrador de recursos de Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="74f2b-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="74f2b-147">Para implementar una plantilla personalizada a través del portal, seleccione **Nuevo** y busque **Implementación de plantillas** hasta que pueda seleccionarla entre las opciones.</span><span class="sxs-lookup"><span data-stu-id="74f2b-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![buscar implementación de plantilla](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="74f2b-149">Seleccione **Implementación de plantillas** en los recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="74f2b-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![seleccionar implementación de plantillas](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="74f2b-151">Después de iniciar la implementación de la plantilla, abra la plantilla en blanco que está disponible para la personalización.</span><span class="sxs-lookup"><span data-stu-id="74f2b-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![crear plantilla](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="74f2b-153">En el editor, agregue la sintaxis JSON que define los recursos que desea implementar.</span><span class="sxs-lookup"><span data-stu-id="74f2b-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="74f2b-154">Seleccione **Guardar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="74f2b-154">Select **Save** when done.</span></span> <span data-ttu-id="74f2b-155">Para obtener instrucciones sobre cómo escribir la sintaxis JSON, consulte el [Tutorial de la plantilla de Resource Manager](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="74f2b-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![editar plantilla](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="74f2b-157">O bien puede seleccionar una plantilla existente en [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="74f2b-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="74f2b-158">Estas plantillas son aportaciones de la comunidad.</span><span class="sxs-lookup"><span data-stu-id="74f2b-158">These templates are contributed by the community.</span></span> <span data-ttu-id="74f2b-159">Abarcan muchos escenarios comunes y puede que alguien haya agregado una plantilla que sea similar a lo que desea implementar.</span><span class="sxs-lookup"><span data-stu-id="74f2b-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="74f2b-160">Puede buscar las plantillas para encontrar alguna que coincida con su escenario.</span><span class="sxs-lookup"><span data-stu-id="74f2b-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![seleccionar plantilla de inicio rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="74f2b-162">Puede ver la plantilla seleccionada en el editor.</span><span class="sxs-lookup"><span data-stu-id="74f2b-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="74f2b-163">Después de proporcionar todos los demás valores, seleccione **Crear** para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="74f2b-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![implementar plantilla](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="74f2b-165">Implementación de los recursos desde una plantilla guardada en la cuenta</span><span class="sxs-lookup"><span data-stu-id="74f2b-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="74f2b-166">El portal permite guardar una plantilla en su cuenta de Azure y volver a implementarla más adelante.</span><span class="sxs-lookup"><span data-stu-id="74f2b-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="74f2b-167">Para obtener más información sobre cómo trabajar con estas plantillas guardadas, consulte [Introducción a las plantillas privadas del Portal de Azure](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="74f2b-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="74f2b-168">Para buscar las plantillas guardadas, seleccione **Examinar** > **Plantillas**.</span><span class="sxs-lookup"><span data-stu-id="74f2b-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![examinar plantillas](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="74f2b-170">En la lista de plantillas guardadas en su cuenta, seleccione aquella en la que desea trabajar.</span><span class="sxs-lookup"><span data-stu-id="74f2b-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![plantillas guardadas](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="74f2b-172">Seleccione **Implementar** para volver a implementar esta plantilla guardada.</span><span class="sxs-lookup"><span data-stu-id="74f2b-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![implementar plantilla guardada](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="74f2b-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74f2b-174">Next steps</span></span>
* <span data-ttu-id="74f2b-175">Para ver los registros de auditoría, consulte [Operaciones de auditoría con Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="74f2b-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="74f2b-176">Para solucionar errores de implementación, vea [View deployment operations](resource-manager-deployment-operations.md) (Ver operaciones de implementación).</span><span class="sxs-lookup"><span data-stu-id="74f2b-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="74f2b-177">Para recuperar una plantilla de una implementación o un grupo de recursos, consulte [Exportación de plantillas de Azure Resource Manager desde recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="74f2b-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="74f2b-178">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="74f2b-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

