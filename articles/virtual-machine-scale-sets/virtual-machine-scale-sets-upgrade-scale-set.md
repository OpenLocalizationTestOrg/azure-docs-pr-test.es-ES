---
title: "conjunto de aaaUpgrade una escala de la máquina virtual de Azure | Documentos de Microsoft"
description: "Actualización de un conjunto de escalado de máquinas virtuales de Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="1f366-103">Actualización de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="1f366-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="1f366-104">Este artículo describe cómo puede revertir una escala de máquina virtual de Azure tooan de actualización de sistema operativo establecido sin tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="1f366-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="1f366-105">En este contexto, una actualización del SO implica cambiar versión de Hola o SKU de hello SO u Hola URI de una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="1f366-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="1f366-106">Para actualizar sin tiempos de inactividad, las máquinas virtuales deben actualizarse una a una o en grupos (por ejemplo, un dominio de error a la vez), en lugar de todas a la vez.</span><span class="sxs-lookup"><span data-stu-id="1f366-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="1f366-107">Al hacerlo, todas las máquinas virtuales que no se estén actualizando siguen funcionando.</span><span class="sxs-lookup"><span data-stu-id="1f366-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="1f366-108">tooavoid ambigüedad, vamos a distinguir cuatro tipos de actualización del SO puede tooperform:</span><span class="sxs-lookup"><span data-stu-id="1f366-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="1f366-109">Cambiar la versión de Hola o SKU de una imagen de plataforma.</span><span class="sxs-lookup"><span data-stu-id="1f366-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="1f366-110">Por ejemplo, cambiar Ubuntu versión 14.04.2-LTS desde 14.04.201506100 too14.04.201507060 o el cambio de hello Ubuntu 15.10 ni la última SKU too16.04.0-LTS/latest.</span><span class="sxs-lookup"><span data-stu-id="1f366-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="1f366-111">Este escenario se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1f366-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="1f366-112">Cambiar Hola URI que señala tooa nueva versión de una imagen personalizada que se compiló (**propiedades** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **imagen** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="1f366-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="1f366-113">Este escenario se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1f366-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="1f366-114">Cambiar la referencia a imagen Hola de un conjunto de escala que se creó mediante discos de Azure administrados.</span><span class="sxs-lookup"><span data-stu-id="1f366-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="1f366-115">Aplicación de revisiones Hola OS desde dentro de una máquina virtual (ejemplos de esto son instalar una revisión de seguridad y ejecutar Windows Update).</span><span class="sxs-lookup"><span data-stu-id="1f366-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="1f366-116">Este escenario es posible, pero no se trata en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1f366-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="1f366-117">No hablaremos de los conjuntos de escalado de máquinas virtuales que se implementan como parte de un clúster de [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) .</span><span class="sxs-lookup"><span data-stu-id="1f366-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="1f366-118">Consulte [Aplicación de revisiones del sistema operativo Windows en el clúster de Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) para obtener más información sobre aplicación de revisiones a Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f366-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="1f366-119">Hola básica Hola de secuencia para cambiar la versión de SO o SKU de una imagen de plataforma u Hola URI de una imagen personalizada tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="1f366-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="1f366-120">Obtener el modelo de conjunto de escala de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f366-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="1f366-121">Cambiar la versión de hello, SKU, referencia de la imagen o valor URI en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1f366-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="1f366-122">Actualizar modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="1f366-122">Update hello model.</span></span>
4. <span data-ttu-id="1f366-123">Hacer un *manualUpgrade* llamar en máquinas virtuales de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="1f366-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="1f366-124">Este paso solo es pertinente si *upgradePolicy* se establece demasiado**Manual** en la escala de conjunto.</span><span class="sxs-lookup"><span data-stu-id="1f366-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="1f366-125">Si se establece demasiado**automática**, todas las máquinas virtuales de Hola se actualizan al mismo tiempo, lo que produce el tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="1f366-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="1f366-126">Con esta información en mente, veamos cómo puede actualizar versión Hola de una escala establecida en PowerShell y mediante el uso de hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="1f366-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="1f366-127">Estos ejemplos cubren el caso de hello de una imagen de plataforma, pero en este artículo proporciona información suficiente para tooadapt esta imagen personalizada de proceso tooa.</span><span class="sxs-lookup"><span data-stu-id="1f366-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="1f366-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f366-128">PowerShell</span></span>
<span data-ttu-id="1f366-129">Este ejemplo actualiza un conjunto de escalas de máquina virtual de Windows (creación toohello nueva versión 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="1f366-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="1f366-130">Después de actualizar el modelo de hello, realiza una actualización de una instancia de máquina virtual a la vez.</span><span class="sxs-lookup"><span data-stu-id="1f366-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="1f366-131">Si va a actualizar hello URI para una imagen personalizada en lugar de cambiar una versión de la imagen de plataforma, reemplace Hola "conjunto Hola nueva versión" línea con un comando que se actualizará Hola URI de la imagen de origen.</span><span class="sxs-lookup"><span data-stu-id="1f366-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="1f366-132">Por ejemplo, si se creó el conjunto de escala de hello sin usar discos de Azure administrados, actualización de hello sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="1f366-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="1f366-133">Si una imagen personalizada en función de conjunto de escalas de se creó con discos de Azure administrados, a continuación, la referencia a imagen Hola se actualizaría.</span><span class="sxs-lookup"><span data-stu-id="1f366-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="1f366-134">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1f366-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="1f366-135">Hola API de REST</span><span class="sxs-lookup"><span data-stu-id="1f366-135">hello REST API</span></span>
<span data-ttu-id="1f366-136">Aquí se muestran un par de ejemplos de Python que utilizan hello tooroll de API de REST de Azure espera una actualización de versión de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1f366-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="1f366-137">Ambos utilizan ligero hello [azurerm](https://pypi.python.org/pypi/azurerm) biblioteca de API de REST de Azure contenedor funciones toodo una operación GET en escala de hello establece modelo, seguidas por una operación PUT con un modelo actualizado.</span><span class="sxs-lookup"><span data-stu-id="1f366-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="1f366-138">También examinen en vistas de instancias de máquina virtual tooidentify Hola máquinas virtuales de dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="1f366-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="1f366-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="1f366-139">Vmssupgrade</span></span>
 <span data-ttu-id="1f366-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) es un script de Python que ha usado tooroll espera un tooa de actualización de sistema operativo ejecuta escalas de máquina virtual establece un dominio de actualización a la vez.</span><span class="sxs-lookup"><span data-stu-id="1f366-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Script vmssupgrade para elegir las máquinas virtuales o un dominio de actualización](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="1f366-142">Esta secuencia de comandos le permite elegir tooupdate de máquinas virtuales específicas o especificar un dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="1f366-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="1f366-143">Admite cambiar una versión de la imagen de plataforma u Hola URI de una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="1f366-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="1f366-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="1f366-144">Vmsseditor</span></span>
<span data-ttu-id="1f366-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) es un editor general para conjuntos de escalado de máquinas virtuales que muestra el estado estas en un mapa térmico, donde cada fila representa un dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="1f366-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="1f366-146">Entre otras cosas, puede actualizar el modelo de Hola para un conjunto de escala con una nueva versión, la SKU o el URI de la imagen personalizada y, a continuación, elija tooupgrade de dominios de error.</span><span class="sxs-lookup"><span data-stu-id="1f366-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="1f366-147">Al hacer esto, todas las máquinas virtuales de hello en ese dominio de actualización son toohello actualizado nuevo modelo.</span><span class="sxs-lookup"><span data-stu-id="1f366-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="1f366-148">Como alternativa, puede realizar una actualización gradual basada en el tamaño de lote de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="1f366-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="1f366-149">Hello captura de pantalla siguiente muestra un modelo de una escala establecida para Ubuntu 14.04-2LTS versión 14.04.201507060.</span><span class="sxs-lookup"><span data-stu-id="1f366-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="1f366-150">Muchas más opciones se han agregado toothis herramienta desde que se tomó esta captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="1f366-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Modelo de vmsseditor de conjunto de escalado para Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="1f366-152">Tras hacer clic en **actualizar** y, a continuación, **obtener los detalles de**, tooupdate de inicio de máquinas virtuales en UD 0.</span><span class="sxs-lookup"><span data-stu-id="1f366-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Vmsseditor con la actualización en curso](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

