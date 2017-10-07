---
title: "aaaResize una VM de Windows en el modelo de implementación clásica de hello - Azure | Documentos de Microsoft"
description: "Cambiar el tamaño de una máquina virtual de Windows creada en el modelo de implementación clásica de hello, uso de Powershell de Azure."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="76043-103">Cambiar el tamaño de una VM de Windows creados en el modelo de implementación clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="76043-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="76043-104">Este artículo muestra cómo tooresize una VM de Windows, creado en el modelo de implementación clásica de hello mediante Powershell de Azure.</span><span class="sxs-lookup"><span data-stu-id="76043-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="76043-105">Al considerar Hola capacidad tooresize una máquina virtual, hay dos conceptos que controlan el intervalo de Hola de máquina virtual de los tamaños disponibles tooresize Hola.</span><span class="sxs-lookup"><span data-stu-id="76043-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="76043-106">concepto primera Hello es región hello en el que se implementa la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76043-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="76043-107">lista de Hola de tamaños de máquina virtual disponibles en la región está en la ficha de servicios de Hola de página web de hello regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="76043-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="76043-108">concepto de segundo de Hello es hardware físico Hola hospeda actualmente la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76043-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="76043-109">servidores físicos Hola hospeda máquinas virtuales se agrupan en clústeres de hardware físico comunes.</span><span class="sxs-lookup"><span data-stu-id="76043-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="76043-110">método Hello del cambio de tamaño de máquina virtual es diferente en función de si hello deseado nuevo tamaño VM admite clústeres de hardware de hello hospedando Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76043-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="76043-111">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="76043-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="76043-112">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="76043-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="76043-113">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="76043-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="76043-114">También puede [cambiar el tamaño de una máquina virtual que creó en el modelo de implementación del Administrador de recursos de hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="76043-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="76043-115">Adición de la cuenta</span><span class="sxs-lookup"><span data-stu-id="76043-115">Add your account</span></span>
<span data-ttu-id="76043-116">Debe configurar Azure PowerShell toowork con recursos de Azure clásicos.</span><span class="sxs-lookup"><span data-stu-id="76043-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="76043-117">Siga los pasos de hello debajo de PowerShell de Azure tooconfigure toomanage los recursos clásicos.</span><span class="sxs-lookup"><span data-stu-id="76043-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="76043-118">En el símbolo del sistema de PowerShell hello, escriba `Add-AzureAccount` y haga clic en **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="76043-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="76043-119">Escriba Hola dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="76043-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="76043-120">Escribir contraseña de Hola para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="76043-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="76043-121">Haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="76043-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="76043-122">Cambiar el tamaño en hello mismo clúster de hardware</span><span class="sxs-lookup"><span data-stu-id="76043-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="76043-123">tooresize un tamaño de tooa de memoria virtual disponible en el clúster de hardware de hello hospedaje Hola de máquina virtual, realice Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="76043-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="76043-124">Ejecute hello siguiente comando de PowerShell Hola de tamaños de máquinas virtuales de hello toolist disponibles en el clúster de hardware de hello hospedaje de servicio de nube de Hola que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="76043-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="76043-125">Ejecute hello después comandos tooresize Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76043-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="76043-126">Cambio de tamaño en un nuevo clúster de hardware</span><span class="sxs-lookup"><span data-stu-id="76043-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="76043-127">tooresize tooa tamaño no está disponible en el clúster de hardware de hello, que hospeda Hola VM, hello todas las máquinas virtuales en el servicio de nube de Hola y servicio en la nube deben volver a crearse.</span><span class="sxs-lookup"><span data-stu-id="76043-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="76043-128">Cada servicio en la nube se hospeda en un clúster de hardware único para que todas las máquinas virtuales en el servicio de nube de hello deben tener un tamaño que se admite en un clúster de hardware.</span><span class="sxs-lookup"><span data-stu-id="76043-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="76043-129">Hello pasos siguientes describen cómo tooresize una máquina virtual, eliminar y volver a crear a continuación, Hola nube servicio.</span><span class="sxs-lookup"><span data-stu-id="76043-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="76043-130">Ejecute hello después PowerShell comando toolist Hola tamaños de máquina virtual disponibles en la región de Hola.</span><span class="sxs-lookup"><span data-stu-id="76043-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="76043-131">Tome nota de todos los valores de configuración para cada máquina virtual Hola del servicio en nube que contiene Hola VM toobe cambia de tamaño.</span><span class="sxs-lookup"><span data-stu-id="76043-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="76043-132">Eliminar todas las máquinas virtuales en el servicio de nube de hello seleccionar discos de hello opción tooretain Hola para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76043-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="76043-133">Vuelva a crear Hola VM toobe cambiar de tamaño mediante el tamaño de la máquina virtual de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="76043-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="76043-134">Volver a crear todas las demás máquinas virtuales que estaban en el servicio de nube de hello con un tamaño de memoria virtual disponible en el clúster de hardware de hello hospedando, entonces, servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="76043-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="76043-135">[Aquí](https://github.com/Azure/azure-vm-scripts) puede encontrar un script de ejemplo para eliminar y volver a crear un servicio en la nube con un nuevo tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76043-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="76043-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76043-136">Next steps</span></span>
* <span data-ttu-id="76043-137">[Cambiar el tamaño de una máquina virtual que creó en el modelo de implementación del Administrador de recursos de hello](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="76043-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

