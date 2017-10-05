---
title: "Eliminación de un clúster de Azure y los recursos que contiene | Microsoft Docs"
description: "Aprenda a eliminar completamente un clúster de Service Fabric, bien mediante la eliminación del grupo de recursos que contiene el clúster o por medio de la eliminación selectiva de recursos."
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
ms.openlocfilehash: 7672aa12421fbe4ad86e7315d6a7a06c2ff5124d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-the-resources-it-uses"></a><span data-ttu-id="e21d8-103">Eliminación de un clúster de Service Fabric en Azure y de los recursos que usa</span><span class="sxs-lookup"><span data-stu-id="e21d8-103">Delete a Service Fabric cluster on Azure and the resources it uses</span></span>
<span data-ttu-id="e21d8-104">Un clúster de Service Fabric está formado por muchos otros recursos de Azure, además del recurso del clúster propiamente dicho.</span><span class="sxs-lookup"><span data-stu-id="e21d8-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="e21d8-105">Así que, para eliminar completamente un clúster de Service Fabric, también debe eliminar todos los recursos que lo componen.</span><span class="sxs-lookup"><span data-stu-id="e21d8-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span>
<span data-ttu-id="e21d8-106">Tiene dos opciones: eliminar el grupo de recursos en el que se encuentra el clúster (lo que elimina el recurso del clúster y todos los demás recursos del grupo) o eliminar específicamente el recurso del clúster y sus recursos asociados (pero ningún otro recurso del grupo).</span><span class="sxs-lookup"><span data-stu-id="e21d8-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="e21d8-107">Con la eliminación del recurso del clúster **no** se eliminan todos los demás recursos de los que consta el clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e21d8-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-the-entire-resource-group-rg-that-the-service-fabric-cluster-is-in"></a><span data-ttu-id="e21d8-108">Eliminación del grupo de recursos completo (RG) en el que se encuentra el clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e21d8-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span></span>
<span data-ttu-id="e21d8-109">Es la forma más sencilla de asegurarse de que elimina todos los recursos asociados al clúster, incluido el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e21d8-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span></span> <span data-ttu-id="e21d8-110">Puede eliminar el grupo de recursos con PowerShell o mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e21d8-110">You can delete the resource group using PowerShell or through the Azure portal.</span></span> <span data-ttu-id="e21d8-111">Si el grupo de recursos tiene recursos que no están relacionados con el clúster de Service fabric, puede eliminar recursos específicos.</span><span class="sxs-lookup"><span data-stu-id="e21d8-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-the-resource-group-using-azure-powershell"></a><span data-ttu-id="e21d8-112">Eliminación del grupo de recursos mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e21d8-112">Delete the resource group using Azure PowerShell</span></span>
<span data-ttu-id="e21d8-113">Otra forma de eliminar el grupo de recursos es ejecutar los siguientes cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e21d8-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e21d8-114">Asegúrese de que tiene instalado en su equipo Azure PowerShell 1.0 o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="e21d8-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="e21d8-115">Si no lo ha hecho antes, siga los pasos que se describen en [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e21d8-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="e21d8-116">Abra una ventana de PowerShell y ejecute los siguientes cmdlets de PS:</span><span class="sxs-lookup"><span data-stu-id="e21d8-116">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="e21d8-117">Si no ha utilizado la opción *-Force* , recibirá un mensaje para confirmar la eliminación.</span><span class="sxs-lookup"><span data-stu-id="e21d8-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span></span> <span data-ttu-id="e21d8-118">Tras la confirmación, el grupo de recursos y todos los recursos que contiene se eliminan.</span><span class="sxs-lookup"><span data-stu-id="e21d8-118">On confirmation the RG and all the resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-the-azure-portal"></a><span data-ttu-id="e21d8-119">Eliminación de un grupo de recursos en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e21d8-119">Delete a resource group in the Azure portal</span></span>
1. <span data-ttu-id="e21d8-120">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e21d8-120">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e21d8-121">Desplácese hasta el clúster de Service Fabric que quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="e21d8-121">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="e21d8-122">Haga clic en el nombre del grupo de recursos en la página de información básica del clúster.</span><span class="sxs-lookup"><span data-stu-id="e21d8-122">Click on the Resource Group name on the cluster essentials page.</span></span>
4. <span data-ttu-id="e21d8-123">Se abre la página **Resource Group Essentials** (Información básica del grupo de recursos).</span><span class="sxs-lookup"><span data-stu-id="e21d8-123">This brings up the **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="e21d8-124">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="e21d8-124">Click **Delete**.</span></span>
6. <span data-ttu-id="e21d8-125">Siga las instrucciones que se indican en esa página para completar la eliminación del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e21d8-125">Follow the instructions on that page to complete the deletion of the resource group.</span></span>

![Eliminación de un grupo de recursos][ResourceGroupDelete]

## <a name="delete-the-cluster-resource-and-the-resources-it-uses-but-not-other-resources-in-the-resource-group"></a><span data-ttu-id="e21d8-127">Eliminación del recurso de clúster y de los recursos que utiliza, pero no de otros recursos del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e21d8-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span></span>
<span data-ttu-id="e21d8-128">Si el grupo de recursos tiene únicamente recursos que están relacionados con el clúster de Service Fabric que quiere eliminar, lo más sencillo es eliminar el grupo de recursos completo.</span><span class="sxs-lookup"><span data-stu-id="e21d8-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span></span> <span data-ttu-id="e21d8-129">Si quiere eliminar de forma selectiva los recursos del grupo uno a uno, siga los pasos que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e21d8-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="e21d8-130">Si ha implementado el clúster mediante el portal o por medio de una de las plantillas de Resource Manager de Service Fabric de la galería de plantillas, entonces todos los recursos del clúster están etiquetados con las dos etiquetas siguientes.</span><span class="sxs-lookup"><span data-stu-id="e21d8-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span></span> <span data-ttu-id="e21d8-131">Puede utilizarlas para decidir qué recursos quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="e21d8-131">You can use them to decide which resources you want to delete.</span></span>

<span data-ttu-id="e21d8-132">***Etiqueta 1:*** Clave = clusterName, valor = 'nombre del clúster'</span><span class="sxs-lookup"><span data-stu-id="e21d8-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span></span>

<span data-ttu-id="e21d8-133">***Etiqueta 2:*** Clave = resourceName, valor = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="e21d8-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-the-azure-portal"></a><span data-ttu-id="e21d8-134">Eliminación de recursos específicos en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e21d8-134">Delete specific resources in the Azure portal</span></span>
1. <span data-ttu-id="e21d8-135">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e21d8-135">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e21d8-136">Desplácese hasta el clúster de Service Fabric que quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="e21d8-136">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="e21d8-137">Vaya a **All settings** (Toda la configuración) en la hoja de información básica.</span><span class="sxs-lookup"><span data-stu-id="e21d8-137">Go to **All settings** on the essentials blade.</span></span>
4. <span data-ttu-id="e21d8-138">Haga clic en **Etiquetas** en **Administración de recursos** en la hoja de configuración.</span><span class="sxs-lookup"><span data-stu-id="e21d8-138">Click on **Tags** under **Resource Management** in the settings blade.</span></span>
5. <span data-ttu-id="e21d8-139">Haga clic en una de las **etiquetas** en la hoja de etiquetas para obtener una lista de todos los recursos con esa etiqueta.</span><span class="sxs-lookup"><span data-stu-id="e21d8-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span></span>
   
    ![Etiquetas del recurso][ResourceTags]
6. <span data-ttu-id="e21d8-141">Cuando tenga la lista de recursos etiquetados, haga clic en cada uno de los recursos y elimínelos.</span><span class="sxs-lookup"><span data-stu-id="e21d8-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span></span>
   
    ![Recursos etiquetados][TaggedResources]

### <a name="delete-the-resources-using-azure-powershell"></a><span data-ttu-id="e21d8-143">Eliminación de los recursos con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e21d8-143">Delete the resources using Azure PowerShell</span></span>
<span data-ttu-id="e21d8-144">Puede eliminar los recursos uno a uno mediante la ejecución de los siguientes cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e21d8-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e21d8-145">Asegúrese de que tiene instalado en su equipo Azure PowerShell 1.0 o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="e21d8-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="e21d8-146">Si no lo ha hecho antes, siga los pasos que se describen en [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e21d8-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="e21d8-147">Abra una ventana de PowerShell y ejecute los siguientes cmdlets de PS:</span><span class="sxs-lookup"><span data-stu-id="e21d8-147">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="e21d8-148">Para cada uno de los recursos que quiere eliminar, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e21d8-148">For each of the resources you want to delete, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of the resource group>" -Force
```

<span data-ttu-id="e21d8-149">Para eliminar el recurso de clúster, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e21d8-149">To delete the cluster resource, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of the resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="e21d8-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e21d8-150">Next steps</span></span>
<span data-ttu-id="e21d8-151">Lea la siguiente información para saber también sobre la actualización de un clúster y los servicios de creación de particiones:</span><span class="sxs-lookup"><span data-stu-id="e21d8-151">Read the following to also learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="e21d8-152">Obtener información sobre actualizaciones de clúster</span><span class="sxs-lookup"><span data-stu-id="e21d8-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="e21d8-153">Obtener información sobre los servicios con estado de creación de particiones para una escala máxima</span><span class="sxs-lookup"><span data-stu-id="e21d8-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
