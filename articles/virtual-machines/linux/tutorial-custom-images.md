---
title: "Crear imágenes de máquina virtual personalizadas con la CLI de Azure | Microsoft Docs"
description: "Tutorial: crear una imagen de máquina virtual personalizada mediante la CLI de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d32980f05ad17a76793021d0a5355d597974a4e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-the-cli"></a><span data-ttu-id="82594-103">Crear una imagen personalizada de una máquina virtual de Azure mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="82594-103">Create a custom image of an Azure VM using the CLI</span></span>

<span data-ttu-id="82594-104">Las imágenes personalizadas son como las imágenes de Marketplace, pero las puede crear usted mismo.</span><span class="sxs-lookup"><span data-stu-id="82594-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="82594-105">Las imágenes personalizadas pueden usarse para configuraciones de arranque como la carga previa de aplicaciones, configuraciones de aplicaciones y otras configuraciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="82594-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="82594-106">En este tutorial, creará su propia imagen personalizada de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="82594-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="82594-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="82594-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82594-108">Desaprovisionar y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="82594-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="82594-109">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="82594-109">Create a custom image</span></span>
> * <span data-ttu-id="82594-110">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="82594-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="82594-111">Enumerar todas las imágenes en su suscripción</span><span class="sxs-lookup"><span data-stu-id="82594-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="82594-112">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="82594-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="82594-113">Si decide instalar y usar la CLI localmente, para este tutorial es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="82594-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="82594-114">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="82594-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="82594-115">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="82594-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="82594-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="82594-116">Before you begin</span></span>

<span data-ttu-id="82594-117">Los siguientes pasos explican cómo tomar una máquina virtual existente y convertirla en una imagen personalizada reutilizable que puede usar para crear nuevas instancias de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="82594-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="82594-118">Para completar el ejemplo de este tutorial, debe tener una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="82594-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="82594-119">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="82594-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="82594-120">Al trabajar en el tutorial, reemplace los nombres de grupo de recursos y máquina virtual cuando proceda.</span><span class="sxs-lookup"><span data-stu-id="82594-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="82594-121">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="82594-121">Create a custom image</span></span>

<span data-ttu-id="82594-122">Para crear una imagen de una máquina virtual, debe preparar la máquina virtual, desaprovisionando, desasignando y marcando después la máquina virtual de origen como generalizada.</span><span class="sxs-lookup"><span data-stu-id="82594-122">To create an image of a virtual machine, you need to prepare the VM by deprovisioning, deallocating, and then marking the source VM as generalized.</span></span> <span data-ttu-id="82594-123">Una vez que se ha preparado la máquina virtual, puede crear una imagen.</span><span class="sxs-lookup"><span data-stu-id="82594-123">Once the VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-the-vm"></a><span data-ttu-id="82594-124">Desaprovisionar la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="82594-124">Deprovision the VM</span></span> 

<span data-ttu-id="82594-125">El desaprovisionamiento generaliza la máquina virtual mediante la eliminación de información específica de la máquina.</span><span class="sxs-lookup"><span data-stu-id="82594-125">Deprovisioning generalizes the VM by removing machine-specific information.</span></span> <span data-ttu-id="82594-126">Esta generalización hace posible implementar muchas máquinas virtuales a partir de una sola imagen.</span><span class="sxs-lookup"><span data-stu-id="82594-126">This generalization makes it possible to deploy many VMs from a single image.</span></span> <span data-ttu-id="82594-127">Durante el desaprovisionamiento, el nombre de host se restablece a *localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="82594-127">During deprovisioning, the host name is reset to *localhost.localdomain*.</span></span> <span data-ttu-id="82594-128">También se eliminan las claves de host SSH, las configuraciones de servidor de nombres, la contraseña raíz y las concesiones DHCP almacenadas en caché.</span><span class="sxs-lookup"><span data-stu-id="82594-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="82594-129">Para desaprovisionar la máquina virtual, use el agente de máquina virtual de Azure (waagent).</span><span class="sxs-lookup"><span data-stu-id="82594-129">To deprovision the VM, use the Azure VM agent (waagent).</span></span> <span data-ttu-id="82594-130">El agente de máquina virtual de Azure está instalado en la máquina virtual y administra el aprovisionamiento y la interacción con el controlador de tejido de Azure.</span><span class="sxs-lookup"><span data-stu-id="82594-130">The Azure VM agent is installed on the VM and manages provisioning and interacting with the Azure Fabric Controller.</span></span> <span data-ttu-id="82594-131">Consulte la [Guía de usuario del Agente de Linux de Azure](agent-user-guide.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="82594-131">For more information, see the [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="82594-132">Conéctese a la máquina virtual mediante SSH y ejecute el comando para desaprovisionar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="82594-132">Connect to your VM using SSH and run the command to deprovision the VM.</span></span> <span data-ttu-id="82594-133">Con el argumento `+user` también se elimina la última cuenta de usuario aprovisionada y los datos asociados.</span><span class="sxs-lookup"><span data-stu-id="82594-133">With the `+user` argument, the last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="82594-134">Reemplace la dirección IP de ejemplo con la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="82594-134">Replace the example IP address with the public IP address of your VM.</span></span>

<span data-ttu-id="82594-135">SSH a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="82594-135">SSH to the VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="82594-136">Desaprovisione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="82594-136">Deprovision the VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="82594-137">Cierre la sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="82594-137">Close the SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="82594-138">Desasignar y marcar la máquina virtual como generalizada</span><span class="sxs-lookup"><span data-stu-id="82594-138">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="82594-139">Para crear una imagen, es necesario desasignar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="82594-139">To create an image, the VM needs to be deallocated.</span></span> <span data-ttu-id="82594-140">Desasigne la máquina virtual mediante [az vm deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="82594-140">Deallocate the VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="82594-141">Por último, establezca el estado de la máquina virtual como generalizado con [az vm generalize](/cli//azure/vm#generalize) para que la plataforma Azure lo sepa.</span><span class="sxs-lookup"><span data-stu-id="82594-141">Finally, set the state of the VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so the Azure platform knows the VM has been generalized.</span></span> <span data-ttu-id="82594-142">Solo se puede crear una imagen de una máquina virtual generalizada.</span><span class="sxs-lookup"><span data-stu-id="82594-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-the-image"></a><span data-ttu-id="82594-143">Crear la imagen</span><span class="sxs-lookup"><span data-stu-id="82594-143">Create the image</span></span>

<span data-ttu-id="82594-144">Ahora puede crear una imagen de la máquina virtual con [az image create](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="82594-144">Now you can create an image of the VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="82594-145">En el ejemplo siguiente se crea una imagen denominada *myImage* a partir de la máquina virtual llamada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="82594-145">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="82594-146">Creación de máquinas virtuales a partir de la imagen</span><span class="sxs-lookup"><span data-stu-id="82594-146">Create VMs from the image</span></span>

<span data-ttu-id="82594-147">Ahora que tiene una imagen, puede crear una o varias máquinas virtuales de la imagen mediante [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="82594-147">Now that you have an image, you can create one or more new VMs from the image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="82594-148">En el ejemplo siguiente se crea una máquina virtual denominada *myVMfromImage* a partir de la máquina virtual llamada *myImage*.</span><span class="sxs-lookup"><span data-stu-id="82594-148">The following example creates a VM named *myVMfromImage* from the image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="82594-149">Administración de imágenes</span><span class="sxs-lookup"><span data-stu-id="82594-149">Image management</span></span> 

<span data-ttu-id="82594-150">Estos son algunos ejemplos de tareas de administración de imágenes comunes y cómo realizarlas mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="82594-150">Here are some examples of common image management tasks and how to complete them using the Azure CLI.</span></span>

<span data-ttu-id="82594-151">Una lista de todas las imágenes por nombre en un formato de tabla.</span><span class="sxs-lookup"><span data-stu-id="82594-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="82594-152">Elimine una imagen.</span><span class="sxs-lookup"><span data-stu-id="82594-152">Delete an image.</span></span> <span data-ttu-id="82594-153">Este ejemplo elimina la imagen con el nombre *myOldImage* de *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="82594-153">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="82594-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82594-154">Next steps</span></span>

<span data-ttu-id="82594-155">En este tutorial, ha creado una imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="82594-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="82594-156">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="82594-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82594-157">Desaprovisionar y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="82594-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="82594-158">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="82594-158">Create a custom image</span></span>
> * <span data-ttu-id="82594-159">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="82594-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="82594-160">Enumerar todas las imágenes en su suscripción</span><span class="sxs-lookup"><span data-stu-id="82594-160">List all the images in your subscription</span></span>
> * <span data-ttu-id="82594-161">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="82594-161">Delete an image</span></span>

<span data-ttu-id="82594-162">Avance al siguiente tutorial para obtener información sobre máquinas virtuales de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="82594-162">Advance to the next tutorial to learn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="82594-163">[Creación de máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="82594-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

