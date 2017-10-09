---
title: aaaDetach un disco de datos de una VM Linux - Azure | Documentos de Microsoft
description: "Obtenga información acerca de toodetach un disco de datos de una máquina virtual en Azure con CLI 2.0 o hello portal de Azure."
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
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="5774b-103">Cómo toodetach datos de un disco de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="5774b-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="5774b-104">Cuando ya no necesita un disco de datos que es un equipo virtual tooa conectados, puede separar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="5774b-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="5774b-105">Esto quita el disco de saludo de la máquina virtual de hello, pero no elimina del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5774b-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="5774b-106">Si se desconecta un disco, no se elimina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5774b-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="5774b-107">Si se ha suscrito tooPremium almacenamiento, se le seguirán cargas de almacenamiento tooincur disco Hola.</span><span class="sxs-lookup"><span data-stu-id="5774b-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="5774b-108">Para obtener más información, consulte demasiado[precios y facturación al usar almacenamiento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="5774b-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="5774b-109">Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.</span><span class="sxs-lookup"><span data-stu-id="5774b-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="5774b-110">Desconexión de un disco de datos con la CLI de 2.0</span><span class="sxs-lookup"><span data-stu-id="5774b-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="5774b-111">disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.</span><span class="sxs-lookup"><span data-stu-id="5774b-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="5774b-112">Desconectar un disco de datos mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="5774b-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="5774b-113">En el concentrador de portal de hello, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="5774b-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="5774b-114">Seleccionar máquina virtual de Hola que tiene un disco de datos de Hola que desee toodetach y haga clic en **detener** toodeallocate Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5774b-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="5774b-115">En la hoja de la máquina virtual de hello, seleccione **discos**.</span><span class="sxs-lookup"><span data-stu-id="5774b-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="5774b-116">En parte superior de Hola de hello **discos** hoja, seleccione **editar**.</span><span class="sxs-lookup"><span data-stu-id="5774b-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="5774b-117">Hola **discos** hoja, toohello más a la derecha del disco de datos de Hola que desearía toodetach, haga clic en hello ![imagen del botón separar](./media/detach-disk/detach.png) botón Desasociar.</span><span class="sxs-lookup"><span data-stu-id="5774b-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="5774b-118">Después de que se ha quitado el disco de hello, haga clic en Guardar en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="5774b-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="5774b-119">En la hoja de la máquina virtual de hello, haga clic en **Introducción** y, a continuación, haga clic en hello **iniciar** situado en parte superior de Hola de toorestart Hola VM de hello hoja.</span><span class="sxs-lookup"><span data-stu-id="5774b-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="5774b-120">disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.</span><span class="sxs-lookup"><span data-stu-id="5774b-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="5774b-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5774b-121">Next steps</span></span>
<span data-ttu-id="5774b-122">Si desea que el disco de datos de tooreuse hello, acaba [adjuntar tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5774b-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

