---
title: aaaUse toodeploy portal Azure recursos de Azure | Documentos de Microsoft
description: "Usar el portal de Azure y administración de recursos de Azure toodeploy los recursos."
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
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="44197-103">Implementación de recursos con las plantillas de Resource Manager y el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="44197-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44197-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44197-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="44197-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="44197-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="44197-106">Portal</span><span class="sxs-lookup"><span data-stu-id="44197-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="44197-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="44197-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="44197-108">Este tema se muestra cómo hello toouse [portal de Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toodeploy los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="44197-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="44197-109">toolearn acerca de cómo administrar los recursos, consulte [recursos de Azure administrar a través del portal de](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="44197-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="44197-110">Actualmente, no todos los servicios es compatible con el portal de Hola o administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="44197-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="44197-111">Para esos servicios, deberá hello toouse [portal clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="44197-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="44197-112">Para el estado de Hola de cada servicio, consulte [gráfico de disponibilidad de portal de Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="44197-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="44197-113">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="44197-113">Create resource group</span></span>
1. <span data-ttu-id="44197-114">Seleccione un grupo de recursos vacío, toocreate **New** > **administración** > **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="44197-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![crear un grupo de recursos vacío](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="44197-116">Asígnele un nombre y una ubicación y, si es necesario, seleccione una suscripción.</span><span class="sxs-lookup"><span data-stu-id="44197-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="44197-117">Debe tooprovide una ubicación para el grupo de recursos de hello porque el grupo de recursos de hello almacena metadatos acerca de los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="44197-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="44197-118">Por motivos de cumplimiento, puede que desee toospecify donde se almacenan los metadatos.</span><span class="sxs-lookup"><span data-stu-id="44197-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="44197-119">Por lo general, se recomienda especificar una ubicación en la que vayan a residir la mayoría de los recursos.</span><span class="sxs-lookup"><span data-stu-id="44197-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="44197-120">Usar Hola mismo ubicación puede simplificar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="44197-120">Using hello same location can simplify your template.</span></span>
   
    ![establecer valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="44197-122">Implementación de recursos desde Marketplace</span><span class="sxs-lookup"><span data-stu-id="44197-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="44197-123">Después de crear un grupo de recursos, puede implementar tooit de recursos de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="44197-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="44197-124">Hola Marketplace proporciona soluciones predefinidas para los escenarios comunes.</span><span class="sxs-lookup"><span data-stu-id="44197-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="44197-125">toostart una implementación, seleccione **New** y el tipo de saludo de recurso le gustaría toodeploy.</span><span class="sxs-lookup"><span data-stu-id="44197-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="44197-126">A continuación, busque versión concreta de Hola de recursos de hello le gustaría toodeploy.</span><span class="sxs-lookup"><span data-stu-id="44197-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![implementar recursos](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="44197-128">Si no ve la solución concreta Hola le gustaría toodeploy, puede buscar Hola Marketplace para él.</span><span class="sxs-lookup"><span data-stu-id="44197-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![buscar en Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="44197-130">Según el tipo de saludo de recursos seleccionado, tendrá una colección de propiedades relevantes tooset antes de la implementación.</span><span class="sxs-lookup"><span data-stu-id="44197-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="44197-131">Estas opciones no se muestran aquí, dado que varía según el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="44197-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="44197-132">Para todos los tipos, debe seleccionar un grupo de recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="44197-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="44197-133">Hola imagen siguiente se muestra cómo toocreate una aplicación web e implementarlo toohello grupo de recursos que ha creado.</span><span class="sxs-lookup"><span data-stu-id="44197-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![Creación de un grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="44197-135">Como alternativa, puede decidir toocreate un grupo de recursos al implementar los recursos.</span><span class="sxs-lookup"><span data-stu-id="44197-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="44197-136">Seleccione **crear nuevo** y asigne un nombre de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="44197-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![crear nuevo grupo de recursos.](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="44197-138">Comenzará la implementación.</span><span class="sxs-lookup"><span data-stu-id="44197-138">Your deployment begins.</span></span> <span data-ttu-id="44197-139">implementación de Hello podría tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="44197-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="44197-140">Cuando haya terminado la implementación de hello, verá una notificación.</span><span class="sxs-lookup"><span data-stu-id="44197-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![ver notificación](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="44197-142">Después de implementar los recursos, puede agregar el grupo de recursos de más recursos toohello mediante el uso de hello **agregar** comando hoja del grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="44197-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![agregar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="44197-144">Implementación de recursos desde plantilla personalizada</span><span class="sxs-lookup"><span data-stu-id="44197-144">Deploy resources from custom template</span></span>
<span data-ttu-id="44197-145">Si desea tooexecute una implementación pero no usar cualquiera de las plantillas de Hola Hola Marketplace, puede crear una plantilla personalizada que define la infraestructura de Hola para su solución.</span><span class="sxs-lookup"><span data-stu-id="44197-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="44197-146">toolearn acerca de cómo crear plantillas, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="44197-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="44197-147">Seleccione una plantilla personalizada a través del portal de hello, toodeploy **nuevo**y empezar a buscar **implementación de plantilla** hasta que pueda seleccionar opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="44197-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![buscar implementación de plantilla](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="44197-149">Seleccione **implementación de plantilla** de recursos disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="44197-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![seleccionar implementación de plantillas](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="44197-151">Después de iniciar la implementación de la plantilla de hello, abra la plantilla en blanco de Hola que está disponible para personalizar.</span><span class="sxs-lookup"><span data-stu-id="44197-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![crear plantilla](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="44197-153">En el editor de hello, agregar sintaxis de JSON de Hola que define los recursos de Hola que vaya toodeploy.</span><span class="sxs-lookup"><span data-stu-id="44197-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="44197-154">Seleccione **Guardar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="44197-154">Select **Save** when done.</span></span> <span data-ttu-id="44197-155">Para obtener instrucciones sobre cómo escribir sintaxis de JSON de hello, consulte [tutorial de la plantilla de administrador de recursos](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="44197-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![editar plantilla](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="44197-157">O bien, puede seleccionar una plantilla existente de hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="44197-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="44197-158">Estas plantillas se aportan por la Comunidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="44197-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="44197-159">Explican muchos escenarios comunes y alguien puede haber agregado una plantilla que sea similar toowhat está tratando de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="44197-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="44197-160">Puede buscar Hola plantillas toofind algo que coincida con su escenario.</span><span class="sxs-lookup"><span data-stu-id="44197-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![seleccionar plantilla de inicio rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="44197-162">Puede ver la plantilla seleccionada hello en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="44197-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="44197-163">Después de proporcionar Hola todos los otros valores, seleccione **crear** plantilla de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="44197-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![implementar plantilla](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="44197-165">Implementar los recursos de una plantilla guardado tooyour cuenta</span><span class="sxs-lookup"><span data-stu-id="44197-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="44197-166">Hola portal permite toosave una cuenta de Azure tooyour de plantilla y volver a implementarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="44197-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="44197-167">Para obtener más información acerca de cómo trabajar con estos guardar plantillas, [empezar a trabajar con plantillas privadas en el portal de Azure hello](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="44197-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="44197-168">toofind las plantillas de guardado, seleccione **examinar** > **plantillas**.</span><span class="sxs-lookup"><span data-stu-id="44197-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![examinar plantillas](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="44197-170">En lista de Hola de plantillas guardadas tooyour cuenta, seleccione Hola que desea toowork en.</span><span class="sxs-lookup"><span data-stu-id="44197-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![plantillas guardadas](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="44197-172">Seleccione **implementar** tooredeploy Esto guarda la plantilla.</span><span class="sxs-lookup"><span data-stu-id="44197-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![implementar plantilla guardada](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="44197-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44197-174">Next steps</span></span>
* <span data-ttu-id="44197-175">Consulte los registros de auditoría tooview, [auditoría de las operaciones con el Administrador de recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="44197-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="44197-176">errores de implementación de tootroubleshoot, consulte [ver las operaciones de implementación](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="44197-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="44197-177">tooretrieve una plantilla de una implementación o el grupo de recursos, consulte [exportar Azure Resource Manager plantilla de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="44197-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="44197-178">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="44197-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

