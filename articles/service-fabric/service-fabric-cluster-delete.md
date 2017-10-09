---
title: "aaaDelete un Azure clúster y sus recursos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo eliminar toocompletely un tejido de servicio de clúster ya sea eliminando grupo de recursos de Hola que contiene el clúster de Hola o eliminando recursos de forma selectiva."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="ac5bf-103">Eliminar un clúster de Service Fabric en los recursos de Azure y hello usa</span><span class="sxs-lookup"><span data-stu-id="ac5bf-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="ac5bf-104">Además propio recurso de clúster toohello, un clúster de Service Fabric se compone de muchos otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="ac5bf-105">Por lo que toocompletely eliminar un clúster de Service Fabric debe toodelete que todos Hola recursos que está formada.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="ac5bf-106">Tienes dos opciones: los grupos de recursos de Hola delete que Hola clúster está en (que elimina los recursos de clúster de Hola y otros recursos en el grupo de recursos de hello) o eliminar específicamente el recurso de clúster de Hola y tiene asociados recursos (pero no para otras recursos de grupo de recursos de hello).</span><span class="sxs-lookup"><span data-stu-id="ac5bf-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="ac5bf-107">Eliminar el recurso de clúster de hello **no** delete todos Hola otros recursos que está formado por el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="ac5bf-108">Eliminar grupo de recursos completo de hello (RG) que Hola a tejido de servicio de clúster se encuentra en</span><span class="sxs-lookup"><span data-stu-id="ac5bf-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="ac5bf-109">Se trata de tooensure Hola de manera más fácil que elimine todos los recursos de hello asociados al clúster, incluido el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="ac5bf-110">Puede eliminar grupo de recursos de hello con PowerShell o a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="ac5bf-111">Si el grupo de recursos tiene recursos que no son tooService relacionados tejido clústeres, puede eliminar recursos específicos.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="ac5bf-112">Eliminar grupo de recursos de hello mediante PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="ac5bf-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="ac5bf-113">También puede eliminar el grupo de recursos de hello ejecutando Hola siguientes cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ac5bf-114">Asegúrese de que tiene instalado en su equipo Azure PowerShell 1.0 o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="ac5bf-115">Si no ha hecho esto antes, siga los pasos de hello descritos en [cómo tooinstall y configurar Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="ac5bf-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="ac5bf-116">Abra una ventana de PowerShell y ejecute hello siguientes cmdlets de PS:</span><span class="sxs-lookup"><span data-stu-id="ac5bf-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="ac5bf-117">Obtendrá una eliminación de hello tooconfirm preguntar si no usas hello *-Force* opción.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="ac5bf-118">En la confirmación Hola RG y se eliminan todos los recursos de hello contiene.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="ac5bf-119">Eliminar un grupo de recursos en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ac5bf-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="ac5bf-120">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac5bf-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ac5bf-121">Navegar por clúster de Service Fabric toohello desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="ac5bf-122">Haga clic en hello nombre del grupo de recursos en página de hello clúster essentials.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="ac5bf-123">Se abrirá hello **Essentials de grupo de recursos** página.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="ac5bf-124">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-124">Click **Delete**.</span></span>
6. <span data-ttu-id="ac5bf-125">Siga las instrucciones de hello en dicha eliminación de página toocomplete Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Eliminación de un grupo de recursos][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="ac5bf-127">Eliminar el recurso de clúster de Hola y recursos de Hola que utiliza, pero no otros recursos en el grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="ac5bf-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="ac5bf-128">Si el grupo de recursos tiene únicamente los recursos que están en clúster de Service Fabric toohello relacionados que desee toodelete, resulta más fácil toodelete Hola todo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="ac5bf-129">Si desea recursos Hola de delete tooselectively uno por uno, en el grupo de recursos que, a continuación, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="ac5bf-130">Si implementa el clúster mediante el portal de Hola o utilizando uno de plantillas de servicio Administrador de recursos de tejido de Hola desde la Galería de plantillas de hello, todos los recursos de Hola Hola de clúster utiliza se etiquetan con hello siguiendo dos etiquetas.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="ac5bf-131">Puede usar toodecide qué recursos desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="ac5bf-132">***Etiqueta n.º 1:*** clave = clusterName, valor = 'nombre de clúster de hello'</span><span class="sxs-lookup"><span data-stu-id="ac5bf-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="ac5bf-133">***Etiqueta 2:*** Clave = resourceName, valor = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="ac5bf-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="ac5bf-134">Eliminar recursos específicos de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ac5bf-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="ac5bf-135">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac5bf-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ac5bf-136">Navegar por clúster de Service Fabric toohello desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="ac5bf-137">Vaya demasiado**toda la configuración de** en la hoja de essentials Hola.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="ac5bf-138">Haga clic en **etiquetas** en **administración de recursos** en la hoja de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="ac5bf-139">Haga clic en uno de hello **etiquetas** en hello etiquetas hoja tooget una lista de todos los recursos de Hola que contienen esa etiqueta.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Etiquetas del recurso][ResourceTags]
6. <span data-ttu-id="ac5bf-141">Una vez que tenga la lista de Hola de recursos etiquetados, haga clic en cada uno de los recursos de Hola y eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Recursos etiquetados][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="ac5bf-143">Eliminar recursos de hello usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac5bf-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="ac5bf-144">Puede eliminar recursos Hola uno por uno, ejecute hello siguientes cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ac5bf-145">Asegúrese de que tiene instalado en su equipo Azure PowerShell 1.0 o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="ac5bf-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="ac5bf-146">Si no ha hecho esto antes, siga los pasos de hello descritos en [cómo tooinstall y configurar Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="ac5bf-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="ac5bf-147">Abra una ventana de PowerShell y ejecute hello siguientes cmdlets de PS:</span><span class="sxs-lookup"><span data-stu-id="ac5bf-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="ac5bf-148">Para cada uno de los recursos de hello desea toodelete, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac5bf-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="ac5bf-149">recurso de clúster en hello toodelete, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac5bf-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="ac5bf-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac5bf-150">Next steps</span></span>
<span data-ttu-id="ac5bf-151">Hola de lectura sigue tooalso Aprenda a actualizar a un clúster y servicios de creación de particiones:</span><span class="sxs-lookup"><span data-stu-id="ac5bf-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="ac5bf-152">Obtener información sobre actualizaciones de clúster</span><span class="sxs-lookup"><span data-stu-id="ac5bf-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="ac5bf-153">Obtener información sobre los servicios con estado de creación de particiones para una escala máxima</span><span class="sxs-lookup"><span data-stu-id="ac5bf-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
