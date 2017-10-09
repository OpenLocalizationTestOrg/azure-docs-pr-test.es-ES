---
title: "aplicación administrada de aaaConsume un Azure | Documentos de Microsoft"
description: "Describe cómo crear una aplicación administrada de Azure a partir de archivos publicados."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="a4b68-103">Uso de una aplicación administrada interna</span><span class="sxs-lookup"><span data-stu-id="a4b68-103">Consume an internal managed application</span></span>

<span data-ttu-id="a4b68-104">Puede usar [aplicaciones administradas](managed-application-overview.md) de Azure que están diseñadas para los miembros de su organización.</span><span class="sxs-lookup"><span data-stu-id="a4b68-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="a4b68-105">Por ejemplo, puede seleccionar aplicaciones administradas desde el departamento de TI que garantizan el cumplimiento normativo de los estándares de la organización.</span><span class="sxs-lookup"><span data-stu-id="a4b68-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="a4b68-106">Estas aplicaciones administradas están disponibles a través de hello catálogo de servicios, no hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a4b68-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="a4b68-107">Antes de continuar con este artículo, debe tener una aplicación administrada disponible en el catálogo de servicios de Hola para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="a4b68-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="a4b68-108">Si nadie de la organización ha creado todavía una aplicación administrada, consulte [Publicación de una aplicación administrada para uso interno](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a4b68-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="a4b68-109">Actualmente, se puede utilizar la CLI de Azure o hello tooconsume portal Azure una aplicación administrada.</span><span class="sxs-lookup"><span data-stu-id="a4b68-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="a4b68-110">Crear aplicación hello administrado mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="a4b68-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="a4b68-111">toodeploy una aplicación administrada a través del portal de hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a4b68-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="a4b68-112">Vaya toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b68-112">Go toohello Azure portal.</span></span> <span data-ttu-id="a4b68-113">Búsqueda de una **aplicación administrada del catálogo de servicios**.</span><span class="sxs-lookup"><span data-stu-id="a4b68-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Aplicación administrada del catálogo de servicios](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="a4b68-115">Hola seleccione administra aplicación desea toocreate de lista de Hola de las soluciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="a4b68-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="a4b68-116">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a4b68-116">Select **Create**.</span></span>

   ![Selección de aplicaciones administradas](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="a4b68-118">Proporcionar valores para parámetros de Hola que sean necesarios tooprovision Hola recursos.</span><span class="sxs-lookup"><span data-stu-id="a4b68-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="a4b68-119">Seleccione **Centro occidental de EE. UU.** como ubicación.</span><span class="sxs-lookup"><span data-stu-id="a4b68-119">Select **West Central US** for location.</span></span> <span data-ttu-id="a4b68-120">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a4b68-120">Select **OK**.</span></span>

   ![Parámetros de aplicaciones administradas](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="a4b68-122">plantilla de Hola valida valores de hello que proporcionó.</span><span class="sxs-lookup"><span data-stu-id="a4b68-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="a4b68-123">Si la validación es correcta, seleccione **Aceptar** implementación de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="a4b68-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Validación de aplicaciones administradas](./media/managed-application-consumption/validation.png)

<span data-ttu-id="a4b68-125">Una vez finalizada la implementación de hello, los recursos adecuados de hello definidos en la plantilla de Hola se aprovisionan en grupo de recursos administrados de hello proporcionada.</span><span class="sxs-lookup"><span data-stu-id="a4b68-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="a4b68-126">Crear aplicación hello administrado mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a4b68-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="a4b68-127">Hay dos toocreate formas una aplicación administrada mediante Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="a4b68-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="a4b68-128">Use el comando de hello para la creación de aplicaciones administradas.</span><span class="sxs-lookup"><span data-stu-id="a4b68-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="a4b68-129">Use el comando de implementación de plantilla Normal Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="a4b68-130">Use el comando de implementación de plantilla Hola</span><span class="sxs-lookup"><span data-stu-id="a4b68-130">Use hello template deployment command</span></span>

<span data-ttu-id="a4b68-131">Implementar archivo applianceMainTemplate.json Hola Hola proveedor creado.</span><span class="sxs-lookup"><span data-stu-id="a4b68-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="a4b68-132">Después, cree dos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4b68-132">Then create two resource groups.</span></span> <span data-ttu-id="a4b68-133">Hello primer grupo de recursos es donde hello recursos de la aplicación administrada que se crea: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="a4b68-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="a4b68-134">segundo grupo de recursos de Hello contiene todos los recursos de hello definidos en mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a4b68-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="a4b68-135">Hola ISV administra este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4b68-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="a4b68-136">Use `westcentralus` como ubicación de Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4b68-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="a4b68-137">toodeploy applianceMainTemplate.json en mainResourceGroup, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a4b68-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="a4b68-138">Después de hello anterior se ejecuta de la plantilla, le pedirá Hola valores de parámetros de Hola que se definen en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="a4b68-139">Además toohello parámetros que necesitan recursos tooprovision en una plantilla, es necesario que dos valores de parámetro de clave:</span><span class="sxs-lookup"><span data-stu-id="a4b68-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="a4b68-140">**managedResourceGroupId**: Hola identificador hello de recursos de grupo contenedor Hola recursos definidos en applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a4b68-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="a4b68-141">Id. de Hello tiene el formato de hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="a4b68-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="a4b68-142">En el anterior ejemplo de Hola, lo del Id. de Hola de `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="a4b68-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="a4b68-143">**applianceDefinitionId**: Id. de Hola de hello administra recursos de la definición de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a4b68-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="a4b68-144">Este valor se proporciona por hello ISV.</span><span class="sxs-lookup"><span data-stu-id="a4b68-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="a4b68-145">publicador de Hello debe conceder el grupo de recursos de toohello de acceso que contiene la definición de la aplicación hello administrado.</span><span class="sxs-lookup"><span data-stu-id="a4b68-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="a4b68-146">se crea el recurso de la definición de Hello en la suscripción del publicador de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="a4b68-147">Por lo tanto, un usuario, el grupo de usuarios o la aplicación en el inquilino de cliente hello necesita acceso de lectura toothis recursos.</span><span class="sxs-lookup"><span data-stu-id="a4b68-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="a4b68-148">Cuando finaliza correctamente la implementación de hello, vea Hola administrado aplicación se crea en mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="a4b68-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="a4b68-149">se crea el recurso de storageAccount de Hello en managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="a4b68-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="a4b68-150">Hola use create, comando</span><span class="sxs-lookup"><span data-stu-id="a4b68-150">Use hello create command</span></span>

<span data-ttu-id="a4b68-151">Puede usar hello `az managedapp create` comando toocreate una aplicación administrada de hello administra la definición de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a4b68-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="a4b68-152">**Id. de definición de dispositivo**: definición de aplicación creado en hello anterior paso administrada por Id. de recurso de Hola de hello.</span><span class="sxs-lookup"><span data-stu-id="a4b68-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="a4b68-153">tooobtain este identificador, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a4b68-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="a4b68-154">Este comando devuelve la definición de la aplicación hello administrado.</span><span class="sxs-lookup"><span data-stu-id="a4b68-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="a4b68-155">Se necesita el valor de Hola de propiedad de Id. de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="a4b68-156">**Identificador administrado rg**: nombre de Hola Hola de recursos de grupo contenedor Hola recursos definidos en applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a4b68-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="a4b68-157">Este grupo de recursos es el grupo de recursos administrados de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="a4b68-158">Está administrado por el publicador de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-158">It's managed by hello publisher.</span></span> <span data-ttu-id="a4b68-159">Si no existe, se crea.</span><span class="sxs-lookup"><span data-stu-id="a4b68-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="a4b68-160">**grupo de recursos**: se crea el grupo de recursos de Hola donde hello administra el recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a4b68-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="a4b68-161">Hola Microsoft.Solutions/appliance recursos vive en este grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4b68-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="a4b68-162">**parámetros**: Hola parámetros que son necesarios para los recursos de hello definidos en applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="a4b68-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a4b68-163">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="a4b68-163">Known issues</span></span>

<span data-ttu-id="a4b68-164">Esta versión de vista previa incluye Hola problemas siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4b68-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="a4b68-165">Aparece un error de servidor interno 500 durante la creación de hello de aplicación hello administrado.</span><span class="sxs-lookup"><span data-stu-id="a4b68-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="a4b68-166">Si experimenta este problema, es probable que toobe intermitente.</span><span class="sxs-lookup"><span data-stu-id="a4b68-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="a4b68-167">Vuelva a intentar la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-167">Retry hello operation.</span></span>
* <span data-ttu-id="a4b68-168">Se necesita un nuevo grupo de recursos para el grupo de recursos administrados de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="a4b68-169">Si utiliza un grupo de recursos existente, se produce un error en la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4b68-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="a4b68-170">Hello grupo de recursos que contiene el recurso de hello Microsoft.Solutions/appliances debe crearse en hello **westcentralus** ubicación.</span><span class="sxs-lookup"><span data-stu-id="a4b68-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4b68-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4b68-171">Next steps</span></span>

* <span data-ttu-id="a4b68-172">Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4b68-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a4b68-173">Para información sobre cómo publicar una aplicación administrada del catálogo de servicios, consulte [Creación y publicación de una aplicación administrada del catálogo de servicios](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a4b68-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="a4b68-174">Para obtener información acerca de la publicación de aplicaciones administradas de toohello Azure Marketplace, vea [Azure administra las aplicaciones de hello Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="a4b68-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="a4b68-175">Para obtener información acerca de cómo consumir una aplicación administrada de hello Marketplace, vea [Azure consumir las aplicaciones en hello Marketplace administradas](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="a4b68-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
