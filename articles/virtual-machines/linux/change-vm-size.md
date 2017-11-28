---
title: "Procedimiento para cambiar el tamaño de una máquina virtual Linux con la CLI de Azure 2.0 | Microsoft Docs"
description: "Escalado o reducción en vertical de una máquina virtual de Linux cambiando el tamaño de la VM."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23fc9f7f34732079682857d4ee685fe811751698
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="5858a-103">Cambio de tamaño de una máquina virtual Linux que usa CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5858a-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="5858a-104">Después de aprovisionar una máquina virtual (VM), puede escalarla o reducirla verticalmente cambiando su [tamaño][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="5858a-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="5858a-105">En algunos casos, hay que desasignarla antes.</span><span class="sxs-lookup"><span data-stu-id="5858a-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="5858a-106">Necesita desasignar la VM si el tamaño deseado no se encuentra disponible en el clúster de hardware que hospeda la VM.</span><span class="sxs-lookup"><span data-stu-id="5858a-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="5858a-107">En este artículo se detalla cómo cambiar el tamaño de una máquina virtual Linux con la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="5858a-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="5858a-108">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5858a-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="5858a-109">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5858a-109">Resize a VM</span></span>
<span data-ttu-id="5858a-110">Para cambiar el tamaño de una máquina virtual, necesita tener instalada la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e iniciar sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5858a-110">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="5858a-111">Consulte la lista de tamaños de VM disponibles en el clúster de hardware que hospeda la VM con [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="5858a-111">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="5858a-112">En el ejemplo siguiente se enumeran los tamaños para la VM denominada `myVM` en la región del grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5858a-112">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="5858a-113">Si aparece el tamaño de máquina virtual deseado, cambie el tamaño de la máquina virtual con [az vm resize](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="5858a-113">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="5858a-114">En el ejemplo siguiente se cambia el tamaño de la VM denominada `myVM` por el tamaño `Standard_DS3_v2`:</span><span class="sxs-lookup"><span data-stu-id="5858a-114">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="5858a-115">La VM se reinicia durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="5858a-115">The VM restarts during this process.</span></span> <span data-ttu-id="5858a-116">Tras reiniciar, se reasignan los discos del SO y de datos.</span><span class="sxs-lookup"><span data-stu-id="5858a-116">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="5858a-117">Se pierde todo lo que haya en el disco temporal.</span><span class="sxs-lookup"><span data-stu-id="5858a-117">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="5858a-118">Si no aparece el tamaño de VM deseado, debe desasignar primero la VM con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="5858a-118">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="5858a-119">Este proceso permite cambiar el tamaño de la VM por otro tamaño disponible que la región admite y, a continuación, se inicia.</span><span class="sxs-lookup"><span data-stu-id="5858a-119">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="5858a-120">Los siguientes pasos permiten desasignar, cambiar de tamaño y luego iniciar la VM denominada `myVM` en el grupo de recursos llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5858a-120">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="5858a-121">Al desasignar la máquina virtual, también se liberan todas las direcciones IP dinámicas asignadas a ella.</span><span class="sxs-lookup"><span data-stu-id="5858a-121">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="5858a-122">Esto no afecta a los discos del SO y de datos.</span><span class="sxs-lookup"><span data-stu-id="5858a-122">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5858a-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5858a-123">Next steps</span></span>
<span data-ttu-id="5858a-124">Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="5858a-124">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="5858a-125">Para obtener más información, consulte [Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales][scale-set].</span><span class="sxs-lookup"><span data-stu-id="5858a-125">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
