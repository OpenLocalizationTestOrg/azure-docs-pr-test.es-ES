---
title: aaaHow tooresize una VM de Linux con hello 2.0 de CLI de Azure | Documentos de Microsoft
description: "¿Cómo tooscale seguridad o reduzca verticalmente una máquina virtual de Linux, cambiando Hola tamaño de máquina virtual."
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
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="0487e-103">Cambio de tamaño de una máquina virtual Linux que usa CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0487e-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="0487e-104">Después de aprovisionar una máquina virtual (VM), puede escalar Hola VM hacia arriba o hacia abajo cambiando hello [tamaño de máquina virtual][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="0487e-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="0487e-105">En algunos casos, debe desasignar Hola VM en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="0487e-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="0487e-106">Necesitará toodeallocate Hola VM si Hola deseado tamaño no está disponible en el clúster de hardware de Hola que hospeda Hola VM.</span><span class="sxs-lookup"><span data-stu-id="0487e-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="0487e-107">Este artículo detalla cómo tooresize una VM de Linux con Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="0487e-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="0487e-108">También puede realizar estos pasos con hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0487e-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="0487e-109">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0487e-109">Resize a VM</span></span>
<span data-ttu-id="0487e-110">tooresize una máquina virtual, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0487e-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="0487e-111">Cambia el tamaño de lista de Hola de vista de la máquina virtual disponible en clúster de hardware de Hola donde se hospeda Hola VM con [lista de vm az-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="0487e-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="0487e-112">Hello en el ejemplo siguiente se enumera los tamaños de máquina virtual para la máquina virtual denominada hello `myVM` en grupo de recursos de hello `myResourceGroup` región:</span><span class="sxs-lookup"><span data-stu-id="0487e-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="0487e-113">Si Hola deseado se muestra el tamaño de máquina virtual, cambiar el tamaño de Hola VM con [cambiar el tamaño de vm az](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="0487e-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="0487e-114">Hola después cambia de tamaño de ejemplo Hola máquina virtual denominada `myVM` toohello `Standard_DS3_v2` tamaño:</span><span class="sxs-lookup"><span data-stu-id="0487e-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="0487e-115">Hola VM se reiniciará durante este proceso.</span><span class="sxs-lookup"><span data-stu-id="0487e-115">hello VM restarts during this process.</span></span> <span data-ttu-id="0487e-116">Después del reinicio de hello, se reasignan los discos de datos y el sistema operativo existente.</span><span class="sxs-lookup"><span data-stu-id="0487e-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="0487e-117">Cualquier cosa en disco temporal de Hola se pierde.</span><span class="sxs-lookup"><span data-stu-id="0487e-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="0487e-118">Si Hola deseado no se muestra el tamaño de máquina virtual, deberá toofirst desasignar Hola VM con [az vm desasignar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="0487e-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="0487e-119">Este proceso permite Hola VM toothen tooany cuyo tamaño ha cambiado tamaño disponible que Hola admite la región y, a continuación, se inicia.</span><span class="sxs-lookup"><span data-stu-id="0487e-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="0487e-120">Hello pasos siguientes desasignar, cambiar el tamaño e inicie Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="0487e-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="0487e-121">Hola desasignar VM también libera todas las direcciones IP dinámicas asignadas toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0487e-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="0487e-122">Hola OS y discos de datos no se ven afectados.</span><span class="sxs-lookup"><span data-stu-id="0487e-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0487e-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0487e-123">Next steps</span></span>
<span data-ttu-id="0487e-124">Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente. Para obtener más información, consulte [Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales][scale-set].</span><span class="sxs-lookup"><span data-stu-id="0487e-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
