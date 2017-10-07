---
title: "imágenes de máquina virtual personalizadas aaaCreate con hello CLI de Azure | Documentos de Microsoft"
description: "Tutorial: crear una imagen de máquina virtual personalizada con hello CLI de Azure."
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
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="7c4f2-103">Crear una imagen personalizada de una máquina virtual de Azure con hello CLI</span><span class="sxs-lookup"><span data-stu-id="7c4f2-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="7c4f2-104">Las imágenes personalizadas son como las imágenes de Marketplace, pero las puede crear usted mismo.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="7c4f2-105">Imágenes personalizadas pueden ser configuraciones toobootstrap usado como carga previa de aplicaciones, configuraciones de aplicaciones y otras configuraciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="7c4f2-106">En este tutorial, creará su propia imagen personalizada de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="7c4f2-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="7c4f2-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c4f2-108">Desaprovisionar y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7c4f2-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="7c4f2-109">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="7c4f2-109">Create a custom image</span></span>
> * <span data-ttu-id="7c4f2-110">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7c4f2-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="7c4f2-111">Una lista de todas las imágenes de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="7c4f2-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="7c4f2-112">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="7c4f2-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7c4f2-113">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7c4f2-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7c4f2-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7c4f2-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="7c4f2-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="7c4f2-116">Before you begin</span></span>

<span data-ttu-id="7c4f2-117">Hola los pasos siguientes detalla cómo tootake una máquina virtual existente y a su vez en un personalizado reutilizable de la imagen que pueden usar toocreate nuevas instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="7c4f2-118">ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="7c4f2-119">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="7c4f2-120">Cuando reemplace trabajar a través de tutorial de hello, grupo de recursos de Hola y VM nombres cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="7c4f2-121">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="7c4f2-121">Create a custom image</span></span>

<span data-ttu-id="7c4f2-122">toocreate una imagen de una máquina virtual, deberá tooprepare Hola VM, desaprovisionamiento, desasignar y, a continuación, marcando una VM como generalizado de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="7c4f2-123">Una vez Hola que se ha preparado la máquina virtual, puede crear una imagen.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="7c4f2-124">Desaprovisionar Hola VM</span><span class="sxs-lookup"><span data-stu-id="7c4f2-124">Deprovision hello VM</span></span> 

<span data-ttu-id="7c4f2-125">Desaprovisionamiento generaliza Hola VM mediante la eliminación de información específica de la máquina.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="7c4f2-126">Esta generalización hace posible toodeploy muchas máquinas virtuales desde una sola imagen.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="7c4f2-127">Durante la cancelación del aprovisionamiento, nombre de host de Hola se restablece demasiado*localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="7c4f2-128">También se eliminan las claves de host SSH, las configuraciones de servidor de nombres, la contraseña raíz y las concesiones DHCP almacenadas en caché.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="7c4f2-129">Hola toodeprovision máquina virtual, use el agente de máquina virtual de Azure de hello (waagent).</span><span class="sxs-lookup"><span data-stu-id="7c4f2-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="7c4f2-130">agente de máquina virtual de Azure de Hola se instala en hello VM y administra el aprovisionamiento e interactuar con hello controlador de tejido de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="7c4f2-131">Para obtener más información, vea hello [manual de usuario del agente Linux de Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="7c4f2-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="7c4f2-132">Conectar tooyour VM mediante SSH y ejecución Hola comando toodeprovision Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="7c4f2-133">Con hello `+user` argumento, la última cuenta de usuario aprovisionado hello y ningún dato asociado también se elimina.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="7c4f2-134">Reemplace la dirección IP de ejemplo de Hola con dirección IP pública de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="7c4f2-135">SSH toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="7c4f2-136">Desaprovisionar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="7c4f2-137">Cerrar sesión de SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="7c4f2-138">Cancelar la asignación y marcar Hola VM como generalizado</span><span class="sxs-lookup"><span data-stu-id="7c4f2-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="7c4f2-139">toocreate una imagen, Hola VM debe toobe desasignado.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="7c4f2-140">Cancela la asignación de hello VM con [cancelar la asignación de máquina virtual az](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7c4f2-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7c4f2-141">Por último, establecer estado de Hola de hello VM tal y como se ha generalizado con [az vm generalizar](/cli//azure/vm#generalize) para que sepa de hello plataforma Windows Azure Hola VM se haya generalizado.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="7c4f2-142">Solo se puede crear una imagen de una máquina virtual generalizada.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="7c4f2-143">Crear imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="7c4f2-143">Create hello image</span></span>

<span data-ttu-id="7c4f2-144">Ahora puede crear una imagen de máquina virtual de hello mediante [crear imagen az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="7c4f2-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="7c4f2-145">Hello en el ejemplo siguiente se crea una imagen denominada *myImage* desde una máquina virtual denominada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="7c4f2-146">Crear máquinas virtuales de la imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="7c4f2-146">Create VMs from hello image</span></span>

<span data-ttu-id="7c4f2-147">Ahora que tiene una imagen, puede crear una o varias nuevas máquinas virtuales de hello imágenes mediante [crear vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7c4f2-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7c4f2-148">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMfromImage* de imagen de hello denominada *myImage*.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="7c4f2-149">Administración de imágenes</span><span class="sxs-lookup"><span data-stu-id="7c4f2-149">Image management</span></span> 

<span data-ttu-id="7c4f2-150">Estos son algunos ejemplos de tareas de administración de imágenes comunes y cómo toocomplete mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="7c4f2-151">Una lista de todas las imágenes por nombre en un formato de tabla.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="7c4f2-152">Elimine una imagen.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-152">Delete an image.</span></span> <span data-ttu-id="7c4f2-153">Este ejemplo elimina Hola imagen denominada *myOldImage* de hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7c4f2-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c4f2-154">Next steps</span></span>

<span data-ttu-id="7c4f2-155">En este tutorial, ha creado una imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="7c4f2-156">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="7c4f2-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c4f2-157">Desaprovisionar y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7c4f2-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="7c4f2-158">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="7c4f2-158">Create a custom image</span></span>
> * <span data-ttu-id="7c4f2-159">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7c4f2-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="7c4f2-160">Una lista de todas las imágenes de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="7c4f2-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="7c4f2-161">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="7c4f2-161">Delete an image</span></span>

<span data-ttu-id="7c4f2-162">Avanzar toohello toolearn de tutorial siguiente sobre máquinas virtuales de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="7c4f2-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="7c4f2-163">[Creación de máquinas virtuales de alta disponibilidad](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="7c4f2-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

