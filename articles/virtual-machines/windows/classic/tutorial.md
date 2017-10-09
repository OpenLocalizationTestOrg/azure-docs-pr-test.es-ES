---
title: "aaaCreate una máquina virtual en hello portal de Azure | Documentos de Microsoft"
description: "Crear una máquina virtual Windows Hola portal de Azure."
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
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="1bea8-103">Crear una máquina virtual que ejecuta Windows en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1bea8-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1bea8-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1bea8-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="1bea8-105">PowerShell: implementación clásica</span><span class="sxs-lookup"><span data-stu-id="1bea8-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="1bea8-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1bea8-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1bea8-107">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="1bea8-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1bea8-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bea8-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1bea8-109">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo de implementación del Administrador de recursos de hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con hello **portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="1bea8-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="1bea8-110">Este tutorial muestra cómo toocreate una Azure la máquina virtual (VM) ejecuta Windows en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bea8-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="1bea8-111">Vamos a usar una imagen de Windows Server como un ejemplo, pero que es simplemente una de hello muchas imágenes de Azure ofrece.</span><span class="sxs-lookup"><span data-stu-id="1bea8-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="1bea8-112">Tenga en cuenta que las opciones de imagen dependen de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="1bea8-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="1bea8-113">Por ejemplo, imágenes de escritorio de Windows pueden ser suscriptores tooMSDN disponible.</span><span class="sxs-lookup"><span data-stu-id="1bea8-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="1bea8-114">Esta sección muestra cómo hello toouse **panel** en Hola tooselect de portal de Azure y, a continuación, crear la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bea8-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="1bea8-115">También puede crear máquinas virtuales con sus [propias imágenes](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="1bea8-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="1bea8-116">toolearn sobre este y otros métodos, vea [toocreate de distintas formas una máquina virtual Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1bea8-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="1bea8-117"><a id="createvirtualmachine"></a>Crear la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1bea8-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="1bea8-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1bea8-118">Next steps</span></span>
* <span data-ttu-id="1bea8-119">Obtenga información acerca de cómo demasiado[crear una máquina virtual mediante el modelo de implementación del Administrador de recursos de hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1bea8-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="1bea8-120">Inicie sesión en la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="1bea8-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="1bea8-121">Para obtener instrucciones, consulte [inicie sesión en la máquina virtual de tooa ejecuta Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="1bea8-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="1bea8-122">Adjuntar una toostore de datos de disco.</span><span class="sxs-lookup"><span data-stu-id="1bea8-122">Attach a disk toostore data.</span></span> <span data-ttu-id="1bea8-123">Puede acoplar tanto discos vacíos como discos que contienen datos.</span><span class="sxs-lookup"><span data-stu-id="1bea8-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="1bea8-124">Para obtener instrucciones, consulte hello [conectar una máquina de virtual datos disco tooa Windows creada con el modelo de implementación clásica de hello](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1bea8-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
