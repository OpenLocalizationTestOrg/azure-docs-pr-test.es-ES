---
title: "aaaDetach un disco de datos de una máquina virtual de Windows - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de un disco de datos de una máquina virtual en Azure mediante el modelo de implementación del Administrador de recursos de hello toodetach."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="cfa60-103">Cómo toodetach datos de un disco de una máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="cfa60-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="cfa60-104">Cuando ya no necesita un disco de datos que es un equipo virtual tooa conectados, puede separar fácilmente.</span><span class="sxs-lookup"><span data-stu-id="cfa60-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="cfa60-105">Esto quita el disco de saludo de la máquina virtual de hello, pero no elimina del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cfa60-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="cfa60-106">Si se desconecta un disco, no se elimina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cfa60-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="cfa60-107">Si se ha suscrito tooPremium almacenamiento, se le seguirán cargas de almacenamiento tooincur disco Hola.</span><span class="sxs-lookup"><span data-stu-id="cfa60-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="cfa60-108">Para obtener más información, consulte demasiado[precios y facturación al usar almacenamiento Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="cfa60-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="cfa60-109">Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.</span><span class="sxs-lookup"><span data-stu-id="cfa60-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="cfa60-110">Desconectar un disco de datos mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="cfa60-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="cfa60-111">En el concentrador de portal de hello, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="cfa60-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="cfa60-112">Seleccionar máquina virtual de Hola que tiene un disco de datos de Hola que desee toodetach y haga clic en **detener** toodeallocate Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfa60-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="cfa60-113">En la hoja de la máquina virtual de hello, seleccione **discos**.</span><span class="sxs-lookup"><span data-stu-id="cfa60-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="cfa60-114">En parte superior de Hola de hello **discos** hoja, seleccione **editar**.</span><span class="sxs-lookup"><span data-stu-id="cfa60-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="cfa60-115">Hola **discos** hoja, toohello más a la derecha del disco de datos de Hola que desearía toodetach, haga clic en hello ![imagen del botón separar](./media/detach-disk/detach.png) botón Desasociar.</span><span class="sxs-lookup"><span data-stu-id="cfa60-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="cfa60-116">Después de que se ha quitado el disco de hello, haga clic en Guardar en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfa60-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="cfa60-117">En la hoja de la máquina virtual de hello, haga clic en **Introducción** y, a continuación, haga clic en hello **iniciar** situado en parte superior de Hola de toorestart Hola VM de hello hoja.</span><span class="sxs-lookup"><span data-stu-id="cfa60-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="cfa60-118">disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.</span><span class="sxs-lookup"><span data-stu-id="cfa60-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="cfa60-119">Desconexión de un disco de datos con PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfa60-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="cfa60-120">En este ejemplo, Hola el primer comando obtiene Hola máquina virtual denominada **MyVM07** en hello **RG11** grupo de recursos mediante el cmdlet Get-AzureRmVM Hola.</span><span class="sxs-lookup"><span data-stu-id="cfa60-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="cfa60-121">Hola comando almacenes Hola máquina virtual en hello **$VirtualMachine** variable.</span><span class="sxs-lookup"><span data-stu-id="cfa60-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="cfa60-122">Hola segundo comando quita Hola datos de un disco con el nombre de la máquina virtual de hello DataDisk3.</span><span class="sxs-lookup"><span data-stu-id="cfa60-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="cfa60-123">comando final Hola actualiza estado de Hola de proceso de hello toocomplete Hola de máquina virtual de la eliminación de disco de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfa60-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="cfa60-124">Para obtener más información, consulte [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="cfa60-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfa60-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cfa60-125">Next steps</span></span>
<span data-ttu-id="cfa60-126">Si desea que el disco de datos de tooreuse hello, acaba [adjuntar tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="cfa60-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

