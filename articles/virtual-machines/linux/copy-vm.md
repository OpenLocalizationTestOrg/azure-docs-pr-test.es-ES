---
title: "Copia de una máquina virtual Linux mediante la CLI de Azure 2.0 | Microsoft Docs"
description: "Obtenga información sobre cómo crear una copia de la máquina virtual Linux de Azure mediante la CLI de Azure 2.0 y los discos administrados."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: 7983061a933370803669480296d7625106e1360c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="f1ac8-103">Creación de una copia de una máquina virtual Linux mediante la CLI de Azure 2.0 y los discos administrados</span><span class="sxs-lookup"><span data-stu-id="f1ac8-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="f1ac8-104">En este artículo se muestra cómo crear una copia de su máquina virtual de Azure con Linux mediante el modelo de implementación de Azure Resource Manager y la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="f1ac8-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Azure CLI 2.0 and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f1ac8-105">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-105">You can also perform these steps with the [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f1ac8-106">También puede [cargar y crear una máquina virtual a partir de un VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1ac8-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f1ac8-107">Prerequisites</span></span>


-   <span data-ttu-id="f1ac8-108">Instalar la [CLI de Azure 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="f1ac8-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="f1ac8-109">Iniciar sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-109">Sign in to an Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="f1ac8-110">Tener una máquina virtual de Azure como el origen de la copia.</span><span class="sxs-lookup"><span data-stu-id="f1ac8-110">Have an Azure VM to use as the source for your copy.</span></span>

## <a name="step-1-stop-the-source-vm"></a><span data-ttu-id="f1ac8-111">Paso 1: Preparación de la máquina virtual de origen</span><span class="sxs-lookup"><span data-stu-id="f1ac8-111">Step 1: Stop the source VM</span></span>


<span data-ttu-id="f1ac8-112">Desasigne la máquina virtual de origen mediante [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-112">Deallocate the source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="f1ac8-113">En el ejemplo siguiente se desasigna la máquina virtual denominada "**myVM**" en el grupo de recursos **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-113">The following example deallocates the VM named **myVM** in the resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-the-source-vm"></a><span data-ttu-id="f1ac8-114">Paso 2: Copia de la máquina virtual de origen</span><span class="sxs-lookup"><span data-stu-id="f1ac8-114">Step 2: Copy the source VM</span></span>


<span data-ttu-id="f1ac8-115">Para copiar una VM, se crea una copia del disco duro virtual subyacente.</span><span class="sxs-lookup"><span data-stu-id="f1ac8-115">To copy a VM, you create a copy of the underlying virtual hard disk.</span></span> <span data-ttu-id="f1ac8-116">Mediante este proceso, se crea un VHD especializado como disco administrado que contiene la misma configuración que la máquina virtual de origen.</span><span class="sxs-lookup"><span data-stu-id="f1ac8-116">This process creates a specialized VHD as a Managed Disk that contains the same configuration and settings as the source VM.</span></span>

<span data-ttu-id="f1ac8-117">Para más información acerca de Azure Managed Disks, consulte [Introducción a los discos administrados de Azure](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="f1ac8-118">Enumere cada máquina virtual y el nombre de su disco del SO con [az vm list](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-118">List each VM and the name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="f1ac8-119">En el ejemplo siguiente se enumeran todas las VM del grupo de recursos denominado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-119">The following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="f1ac8-120">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-120">The output is similar to the following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="f1ac8-121">Copie el disco mediante la creación de un disco administrado con [az disk create](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-121">Copy the disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="f1ac8-122">En el ejemplo siguiente se crea un disco llamado "**myCopiedDisk**" a partir del disco administrado **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-122">The following example creates a disk named **myCopiedDisk** from the managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="f1ac8-123">Compruebe ahora los discos administrados del grupo de recursos mediante [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-123">Verify the managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="f1ac8-124">En el ejemplo siguiente se enumeran todos los discos administrados del grupo de recursos **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-124">The following example lists the managed disks in the resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="f1ac8-125">Vaya al ["Paso 3: Configuración de una red virtual"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-125">Skip to ["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="f1ac8-126">Paso 3: Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="f1ac8-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="f1ac8-127">Con los siguientes pasos opcionales se crea una nueva red virtual, una subred, una dirección IP pública y una tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-127">The following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="f1ac8-128">Si va a copiar una máquina virtual para solucionar problemas o para realizar implementaciones adicionales, puede que no desee usar una máquina virtual de una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f1ac8-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want to use a VM in an existing virtual network.</span></span>

<span data-ttu-id="f1ac8-129">Si desea crear una infraestructura de red virtual para las máquinas virtuales copiadas, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="f1ac8-129">If you want to create a virtual network infrastructure for your copied VMs, follow the next few steps.</span></span> <span data-ttu-id="f1ac8-130">Si no desea crear una red virtual, vaya a [Paso 4: Creación de una máquina virtual](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-130">If you don't want to create a virtual network, skip to [Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="f1ac8-131">Cree la red virtual mediante [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-131">Create the virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="f1ac8-132">En el ejemplo siguiente se crea una red virtual denominada **myVnet** y una subred **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-132">The following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="f1ac8-133">Cree una IP pública mediante [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="f1ac8-134">En el ejemplo siguiente se crea una IP pública denominada "**myPublicIP**" con el nombre DNS **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="f1ac8-134">The following example creates a public IP named **myPublicIP** with the DNS name of **mypublicdns**.</span></span> <span data-ttu-id="f1ac8-135">(El nombre DNS debe ser único, así que proporcione un nombre único).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-135">(The DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="f1ac8-136">Cree la NIC mediante [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-136">Create the NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="f1ac8-137">En el ejemplo siguiente se crea una NIC **myNic** conectada a la subred **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-137">The following example creates a NIC named **myNic** that's attached to the **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="f1ac8-138">Paso 4: Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f1ac8-138">Step 4: Create a VM</span></span>

<span data-ttu-id="f1ac8-139">Ahora puede crear la máquina virtual mediante [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="f1ac8-140">Especifique el disco administrado copiado que usará como disco del SO (--attach-os-disk), como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f1ac8-140">Specify the copied managed disk to use as the OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="f1ac8-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1ac8-141">Next steps</span></span>

<span data-ttu-id="f1ac8-142">Para aprender a usar la CLI de Azure para administrar la nueva máquina virtual, consulte [Comandos de la CLI de Azure en el modo de Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="f1ac8-142">To learn how to use Azure CLI to manage your new VM, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
