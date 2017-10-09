---
title: una VM de Linux mediante Azure CLI 2.0 aaaCopy | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de la máquina virtual Linux de Azure mediante Azure CLI 2.0 y discos administrados."
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
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="0026e-103">Creación de una copia de una máquina virtual Linux mediante la CLI de Azure 2.0 y los discos administrados</span><span class="sxs-lookup"><span data-stu-id="0026e-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="0026e-104">Este artículo muestra cómo toocreate una copia de la máquina virtual (VM de) Azure ejecutando Linux mediante Hola CLI de Azure 2.0 y el modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0026e-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0026e-105">También puede realizar estos pasos con hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0026e-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0026e-106">También puede [cargar y crear una máquina virtual a partir de un VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0026e-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0026e-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0026e-107">Prerequisites</span></span>


-   <span data-ttu-id="0026e-108">Instalar la [CLI de Azure 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="0026e-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="0026e-109">Inicie sesión en tooan Azure cuenta con [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0026e-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="0026e-110">Tener un toouse de máquina virtual de Azure como origen de hello para la copia.</span><span class="sxs-lookup"><span data-stu-id="0026e-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="0026e-111">Paso 1: Detener Hola una VM de origen</span><span class="sxs-lookup"><span data-stu-id="0026e-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="0026e-112">Desasignar una VM de origen Hola utilizando [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="0026e-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="0026e-113">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada **myVM** en grupo de recursos de hello **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="0026e-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="0026e-114">Paso 2: Copiar una VM de origen Hola</span><span class="sxs-lookup"><span data-stu-id="0026e-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="0026e-115">toocopy una máquina virtual, cree una copia del disco de duro virtual subyacente Hola.</span><span class="sxs-lookup"><span data-stu-id="0026e-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="0026e-116">Este proceso crea un disco duro virtual especializado como un disco administrado que contiene Hola misma configuración y la configuración como Hola VM de origen.</span><span class="sxs-lookup"><span data-stu-id="0026e-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="0026e-117">Para más información sobre Azure Managed Disks, consulte [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Introducción a Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="0026e-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="0026e-118">Lista de cada máquina virtual y Hola el nombre de su disco de sistema operativo con [lista de vm az](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="0026e-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="0026e-119">Hello en el ejemplo siguiente se enumera todas las máquinas virtuales en el grupo de recursos denominado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="0026e-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="0026e-120">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0026e-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="0026e-121">Administrar de disco de Hola de copia mediante la creación de un nuevo disco mediante [crear disco az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="0026e-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="0026e-122">Hello en el ejemplo siguiente se crea un disco llamado **myCopiedDisk** desde Hola administrado disco llamado **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="0026e-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="0026e-123">Comprobar los discos de hello administrado ahora en el grupo de recursos mediante el uso de [lista de discos az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="0026e-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="0026e-124">Hello en el ejemplo siguiente se enumera los Hola administrado discos Hola grupo de recursos denominado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="0026e-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="0026e-125">Omitir demasiado["paso 3: configurar una red virtual"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="0026e-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="0026e-126">Paso 3: Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="0026e-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="0026e-127">Hello pasos opcionales siguientes crea una nueva red virtual, la subred, la dirección IP pública y la tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="0026e-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="0026e-128">Si va a copiar una máquina virtual para solucionar problemas con fines o implementaciones adicionales, no conviene toouse una máquina virtual en una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="0026e-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="0026e-129">Si desea toocreate una infraestructura de red virtual para las máquinas virtuales copiadas, siga a continuación Hola pocos pasos.</span><span class="sxs-lookup"><span data-stu-id="0026e-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="0026e-130">Si no desea toocreate una red virtual, omitir demasiado[paso 4: crear una máquina virtual](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="0026e-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="0026e-131">Crear red virtual de hello mediante [crear red virtual de red az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="0026e-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="0026e-132">Hello en el ejemplo siguiente se crea una red virtual denominada **myVnet** y una subred denominada **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="0026e-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="0026e-133">Cree una IP pública mediante [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="0026e-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="0026e-134">Hello en el ejemplo siguiente se crea una IP pública denominada **myPublicIP** con el nombre DNS de Hola de **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="0026e-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="0026e-135">(nombre DNS de hello debe ser único, por lo que proporcione un nombre único.)</span><span class="sxs-lookup"><span data-stu-id="0026e-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="0026e-136">Crear Hola NIC utilizando [crear nic de red az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="0026e-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="0026e-137">Hello en el ejemplo siguiente se crea una NIC denominada **myNic** toothe adjunto que **mySubnet** subred:</span><span class="sxs-lookup"><span data-stu-id="0026e-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="0026e-138">Paso 4: Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0026e-138">Step 4: Create a VM</span></span>

<span data-ttu-id="0026e-139">Ahora puede crear la máquina virtual mediante [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0026e-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="0026e-140">Especificar Hola copia disco administrado toouse como disco de SO hello (--adjuntar-os-disk), como sigue:</span><span class="sxs-lookup"><span data-stu-id="0026e-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="0026e-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0026e-141">Next steps</span></span>

<span data-ttu-id="0026e-142">toolearn cómo toouse CLI de Azure toomanage la nueva máquina virtual, consulte [comandos de CLI de Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="0026e-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
