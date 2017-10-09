---
title: aaaCreate una copia de la VM de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de la máquina virtual de Linux de Azure con Hola 1.0 de CLI de Azure en el modelo de implementación del Administrador de recursos de Hola"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="dcf09-103">Crear una copia de una máquina virtual de Linux con Azure con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dcf09-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="dcf09-104">Este artículo muestra cómo toocreate una copia de la máquina virtual de Azure (VM) en ejecución Linux mediante Hola modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="dcf09-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="dcf09-105">En primer lugar debe copiar sobre el sistema operativo de Hola y el nuevo contenedor de datos discos tooa, a continuación, configurar los recursos de red de Hola y crea nueva máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcf09-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="dcf09-106">También puede [cargar y crear una máquina virtual a partir de una imagen de disco personalizada](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dcf09-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="dcf09-107">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="dcf09-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="dcf09-108">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="dcf09-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="dcf09-109">CLI de Azure 1.0 – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="dcf09-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="dcf09-110">[Azure 2.0 CLI](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="dcf09-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dcf09-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="dcf09-111">Before you begin</span></span>
<span data-ttu-id="dcf09-112">Asegúrese de que se cumple Hola siguiendo los requisitos previos antes de comenzar los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="dcf09-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="dcf09-113">Tienes hello [CLI de Azure](../../cli-install-nodejs.md) descargado e instalado en su equipo.</span><span class="sxs-lookup"><span data-stu-id="dcf09-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="dcf09-114">También necesitará cierta información acerca de la máquina virtual Linux de Azure existente:</span><span class="sxs-lookup"><span data-stu-id="dcf09-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="dcf09-115">Información de la máquina virtual de origen</span><span class="sxs-lookup"><span data-stu-id="dcf09-115">Source VM information</span></span> | <span data-ttu-id="dcf09-116">Donde tooget se</span><span class="sxs-lookup"><span data-stu-id="dcf09-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="dcf09-117">Nombre de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dcf09-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="dcf09-118">Nombre del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dcf09-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="dcf09-119">Ubicación</span><span class="sxs-lookup"><span data-stu-id="dcf09-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="dcf09-120">Nombre de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="dcf09-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="dcf09-121">Nombre del contenedor</span><span class="sxs-lookup"><span data-stu-id="dcf09-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="dcf09-122">Nombre del archivo del VHD de la máquina virtual de origen</span><span class="sxs-lookup"><span data-stu-id="dcf09-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="dcf09-123">Necesitará toomake algunas opciones sobre la nueva máquina virtual:   </span><span class="sxs-lookup"><span data-stu-id="dcf09-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="dcf09-124">-Nombre del contenedor    </span><span class="sxs-lookup"><span data-stu-id="dcf09-124">-Container name    </span></span><br> <span data-ttu-id="dcf09-125">-Nombre de la máquina virtual    </span><span class="sxs-lookup"><span data-stu-id="dcf09-125">-VM name    </span></span><br> <span data-ttu-id="dcf09-126">-Tamaño de la máquina virtual    </span><span class="sxs-lookup"><span data-stu-id="dcf09-126">-VM size    </span></span><br> <span data-ttu-id="dcf09-127">-Nombre de red virtual    </span><span class="sxs-lookup"><span data-stu-id="dcf09-127">-vNet name    </span></span><br> <span data-ttu-id="dcf09-128">-Nombre de subred    </span><span class="sxs-lookup"><span data-stu-id="dcf09-128">-SubNet name    </span></span><br> <span data-ttu-id="dcf09-129">-Nombre de IP    </span><span class="sxs-lookup"><span data-stu-id="dcf09-129">-IP Name    </span></span><br> <span data-ttu-id="dcf09-130">-nombre de NIC</span><span class="sxs-lookup"><span data-stu-id="dcf09-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="dcf09-131">Inicio de sesión y establecimiento de la suscripción</span><span class="sxs-lookup"><span data-stu-id="dcf09-131">Login and set your subscription</span></span>
1. <span data-ttu-id="dcf09-132">Inicio de sesión toohello CLI.</span><span class="sxs-lookup"><span data-stu-id="dcf09-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="dcf09-133">Asegúrese de que está en modo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dcf09-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="dcf09-134">Establecer la suscripción correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="dcf09-134">Set hello correct subscription.</span></span> <span data-ttu-id="dcf09-135">Puede usar 'lista de cuentas de azure' toosee todas las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="dcf09-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="dcf09-136">Detener Hola VM</span><span class="sxs-lookup"><span data-stu-id="dcf09-136">Stop hello VM</span></span>
<span data-ttu-id="dcf09-137">Detener y cancelar la asignación de una VM de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="dcf09-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="dcf09-138">Puede usar 'lista de vm de azure' tooget una lista de todas las máquinas virtuales de hello en su suscripción y sus nombres de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dcf09-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="dcf09-139">Copiar Hola VHD</span><span class="sxs-lookup"><span data-stu-id="dcf09-139">Copy hello VHD</span></span>
<span data-ttu-id="dcf09-140">Puede copiar Hola VHD de hello origen almacenamiento toohello destino mediante hello `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="dcf09-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="dcf09-141">En este ejemplo, vamos toocopy Hola VHD toohello misma cuenta de almacenamiento, pero un contenedor diferente.</span><span class="sxs-lookup"><span data-stu-id="dcf09-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="dcf09-142">contenedor de tooanother de disco duro virtual toocopy Hola Hola misma cuenta de almacenamiento, escriba:</span><span class="sxs-lookup"><span data-stu-id="dcf09-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="dcf09-143">Configurar una red virtual de hello para la nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dcf09-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="dcf09-144">Configure una red virtual y una NIC para la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dcf09-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="dcf09-145">Crear nueva máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="dcf09-145">Create hello new VM</span></span>
<span data-ttu-id="dcf09-146">Ahora puede crear una máquina virtual desde el disco virtual cargado [mediante una plantilla de administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) o a través de hello CLI especificando Hola URI tooyour copiados disco escribiendo:</span><span class="sxs-lookup"><span data-stu-id="dcf09-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="dcf09-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dcf09-147">Next steps</span></span>
<span data-ttu-id="dcf09-148">toolearn cómo toouse CLI de Azure toomanage la nueva máquina virtual, consulte [comandos de CLI de Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="dcf09-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

