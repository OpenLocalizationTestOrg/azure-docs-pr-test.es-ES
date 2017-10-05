---
title: "Desconexión de un disco de una máquina virtual Linux en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo desconectar un disco de datos de una máquina virtual de Azure creada mediante la CLI 2.0 o Azure Portal."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 3f29547e1da6028b1e4b91d9e29fd3bcdfe08d50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="4fc32-103">Desconexión de un disco de datos de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="4fc32-103">How to detach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="4fc32-104">Cuando ya no necesite un disco de datos que se encuentra conectado a una máquina virtual, puede desconectarlo fácilmente.</span><span class="sxs-lookup"><span data-stu-id="4fc32-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="4fc32-105">Esto quita el disco de la máquina virtual, pero no lo quita del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4fc32-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="4fc32-106">Si se desconecta un disco, no se elimina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4fc32-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="4fc32-107">Si se ha suscrito a Almacenamiento premium, seguirá acumulando cargos de almacenamiento por el disco.</span><span class="sxs-lookup"><span data-stu-id="4fc32-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="4fc32-108">Para más información, consulte [Precios y facturación](../../storage/common/storage-premium-storage.md#pricing-and-billing)cuando se utiliza Almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="4fc32-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="4fc32-109">Si desea volver a usar los datos existentes en el disco, puede acoplarlo de nuevo a la misma máquina virtual (o a otra).</span><span class="sxs-lookup"><span data-stu-id="4fc32-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="4fc32-110">Desconexión de un disco de datos con la CLI de 2.0</span><span class="sxs-lookup"><span data-stu-id="4fc32-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="4fc32-111">El disco permanece en el almacenamiento pero ya no está acoplado a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fc32-111">The disk remains in storage but is no longer attached to a virtual machine.</span></span>


## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="4fc32-112">Desconexión de un disco de datos mediante el portal</span><span class="sxs-lookup"><span data-stu-id="4fc32-112">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="4fc32-113">En el centro del portal, seleccione **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="4fc32-113">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="4fc32-114">Seleccione la máquina virtual que tiene el disco de datos que quiere desconectar y haga clic en **Detener** para desasignar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fc32-114">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="4fc32-115">En la hoja de la máquina virtual, seleccione **Discos**.</span><span class="sxs-lookup"><span data-stu-id="4fc32-115">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="4fc32-116">En la parte superior de la hoja **Discos**, seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="4fc32-116">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="4fc32-117">En la hoja **Discos**, en el extremo derecho del disco de datos que desea desconectar, haga clic en el botón de desconexión ![imagen del botón de desconexión](./media/detach-disk/detach.png).</span><span class="sxs-lookup"><span data-stu-id="4fc32-117">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="4fc32-118">Después de quitar el disco, haga clic en Guardar en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="4fc32-118">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="4fc32-119">En la hoja de la máquina virtual, haga clic en **Información general** y, luego, haga clic en el botón **Iniciar** de la parte superior de la hoja para reiniciar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fc32-119">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>

<span data-ttu-id="4fc32-120">El disco permanece en el almacenamiento pero ya no está acoplado a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4fc32-120">The disk remains in storage but is no longer attached to a virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="4fc32-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4fc32-121">Next steps</span></span>
<span data-ttu-id="4fc32-122">Si desea reutilizar el disco de datos, basta con que lo [conecte a otra máquina virtual](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fc32-122">If you want to reuse the data disk, you can just [attach it to another VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

