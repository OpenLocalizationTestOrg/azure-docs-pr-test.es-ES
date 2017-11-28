---
title: "Creación de una máquina virtual en Azure Portal | Microsoft Docs"
description: "Cree una máquina virtual de Windows en el Portal de Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 0981872ff819fdf49a9cc97afce3c212013ce76b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="23af3-103">Creación de una máquina virtual que ejecuta Windows en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="23af3-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23af3-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="23af3-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="23af3-105">PowerShell: implementación clásica</span><span class="sxs-lookup"><span data-stu-id="23af3-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="23af3-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="23af3-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="23af3-107">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="23af3-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="23af3-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="23af3-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="23af3-109">Aprenda a [realizar estos pasos con el modelo de implementación de Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) desde **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="23af3-109">Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.</span></span>

<span data-ttu-id="23af3-110">En este tutorial se muestra cómo crear una máquina virtual de Azure con Windows en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="23af3-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="23af3-111">Vamos a usar una imagen de Windows Server como ejemplo, pero es solo una de las muchas imágenes que Azure ofrece.</span><span class="sxs-lookup"><span data-stu-id="23af3-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="23af3-112">Tenga en cuenta que las opciones de imagen dependen de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="23af3-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="23af3-113">Por ejemplo, las imágenes de escritorio de Windows pueden estar disponibles para los suscriptores de MSDN.</span><span class="sxs-lookup"><span data-stu-id="23af3-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="23af3-114">En esta sección se muestra cómo utilizar el **panel** en Azure Portal para seleccionar y luego crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23af3-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="23af3-115">También puede crear máquinas virtuales con sus [propias imágenes](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="23af3-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="23af3-116">Para obtener más información sobre este y otros métodos, consulte [Diferentes formas de crear una máquina virtual de Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23af3-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="23af3-117"><a id="createvirtualmachine"> </a>Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="23af3-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="23af3-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23af3-118">Next steps</span></span>
* <span data-ttu-id="23af3-119">Aprenda a [crear una máquina virtual mediante el modelo de implementación de Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="23af3-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="23af3-120">Iniciar sesión en la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23af3-120">Log on to the virtual machine.</span></span> <span data-ttu-id="23af3-121">Para obtener instrucciones, consulte el artículo sobre el [inicio de sesión en una máquina virtual que ejecute Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="23af3-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="23af3-122">Acople un disco para almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="23af3-122">Attach a disk to store data.</span></span> <span data-ttu-id="23af3-123">Puede acoplar tanto discos vacíos como discos que contienen datos.</span><span class="sxs-lookup"><span data-stu-id="23af3-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="23af3-124">Para obtener instrucciones, consulte [Conexión de un disco de datos a una máquina virtual Windows creada con el modelo de implementación clásica](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="23af3-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
