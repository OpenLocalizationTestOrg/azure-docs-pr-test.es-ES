---
title: "conjuntos de escalas de máquina virtual de aaaMake disponibles en la pila de Azure"
description: "Obtenga información acerca de cómo un administrador de la nube puede agregar toohello de escala de máquina virtual Azure Marketplace de pila"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a><span data-ttu-id="afc6d-103">Proporcionar conjuntos de escalado de máquinas virtuales en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="afc6d-103">Make virtual machine scale sets available in Azure Stack</span></span>
<span data-ttu-id="afc6d-104">Los conjuntos de escalado de máquinas virtuales son un recurso de proceso de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="afc6d-104">Virtual machine scale sets are an Azure Stack compute resource.</span></span> <span data-ttu-id="afc6d-105">Puede usar toodeploy y administrar un conjunto de máquinas virtuales idénticos.</span><span class="sxs-lookup"><span data-stu-id="afc6d-105">You can use them toodeploy and manage a set of identical virtual machines.</span></span> <span data-ttu-id="afc6d-106">Con todas las máquinas virtuales configuradas Hola igual, no requieren conjuntos de escalas previamente el aprovisionamiento de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="afc6d-106">With all virtual machines configured hello same, scale sets don’t require pre-provisioning of virtual machines.</span></span> <span data-ttu-id="afc6d-107">Es más fácil de servicios a gran escala toobuild que tienen como destino de proceso intensivo, grandes cantidades de datos y las cargas de trabajo en contenedores.</span><span class="sxs-lookup"><span data-stu-id="afc6d-107">It's easier toobuild large-scale services that target big compute, big data, and containerized workloads.</span></span>

<span data-ttu-id="afc6d-108">En este tema le guía a través de conjuntos de escalas de hello proceso toomake disponibles en hello Azure Marketplace de pila.</span><span class="sxs-lookup"><span data-stu-id="afc6d-108">This topic guides you through hello process toomake scale sets available in hello Azure Stack Marketplace.</span></span> <span data-ttu-id="afc6d-109">Después de completar este procedimiento, los usuarios pueden agregar a escala de máquinas virtuales establece tootheir suscripciones.</span><span class="sxs-lookup"><span data-stu-id="afc6d-109">After you complete this procedure, your users can add virtual machine scale sets tootheir subscriptions.</span></span>

<span data-ttu-id="afc6d-110">Los conjuntos de escalado de máquinas virtuales en Azure Stack son similares a los conjuntos de escalado de máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="afc6d-110">Virtual machine scale sets on Azure Stack are like virtual machine scale sets on Azure.</span></span> <span data-ttu-id="afc6d-111">Para obtener más información, vea Hola siguientes vídeos:</span><span class="sxs-lookup"><span data-stu-id="afc6d-111">For more information, see hello following videos:</span></span>
* <span data-ttu-id="afc6d-112">[Mark Russinovich talks Azure Scale Sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/) (Mark Russinovich habla sobre los conjuntos de escalado de Azure)</span><span class="sxs-lookup"><span data-stu-id="afc6d-112">[Mark Russinovich talks Azure scale sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)</span></span>
* [<span data-ttu-id="afc6d-113">Virtual Machine Scale Sets with Guy Bowerman</span><span class="sxs-lookup"><span data-stu-id="afc6d-113">Virtual Machine Scale Sets with Guy Bowerman</span></span>](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

<span data-ttu-id="afc6d-114">En Azure Stack, los conjuntos de escalado de máquinas virtuales no admiten escalado automático.</span><span class="sxs-lookup"><span data-stu-id="afc6d-114">On Azure Stack, Virtual Machine Scale Sets do not support auto-scale.</span></span> <span data-ttu-id="afc6d-115">Puede agregar más escala tooa de instancias establecido mediante el portal de Azure pila hello, plantillas de administrador de recursos o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afc6d-115">You can add more instances tooa scale set using hello Azure Stack portal, Resource Manager templates, or PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afc6d-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="afc6d-116">Prerequisites</span></span>
* <span data-ttu-id="afc6d-117">**PowerShell y herramientas**</span><span class="sxs-lookup"><span data-stu-id="afc6d-117">**Powershell and tools**</span></span>

   <span data-ttu-id="afc6d-118">Instalar y PowerShell configurada para la pila de Azure y las herramientas de la pila de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="afc6d-118">Install and configured PowerShell for Azure Stack and hello Azure Stack tools.</span></span> <span data-ttu-id="afc6d-119">Consulte [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md) (Ponerse en marcha con PowerShell en Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="afc6d-119">See [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md).</span></span>

   <span data-ttu-id="afc6d-120">Después de instalar las herramientas de la pila de Azure de hello, asegúrese de que importar Hola después de módulo de PowerShell (ruta de acceso relativa toohello. \ComputeAdmin carpeta de hello AzureStack-herramientas-master):</span><span class="sxs-lookup"><span data-stu-id="afc6d-120">After you install hello Azure Stack tools, make sure you import hello following PowerShell module (path relative toohello .\ComputeAdmin folder in hello AzureStack-Tools-master folder):</span></span>

        Import-Module .\AzureStack.ComputeAdmin.psm1

* <span data-ttu-id="afc6d-121">**Imagen del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="afc6d-121">**Operating system image**</span></span>

   <span data-ttu-id="afc6d-122">Si no ha agregado un tooyour de imagen de sistema operativo Azure Marketplace de pila, vea [marketplace de pila de Azure de agregar Hola VM de Windows Server 2016 imagen toohello](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="afc6d-122">If you haven’t added an operating system image tooyour Azure Stack Marketplace, see [Add hello Windows Server 2016 VM image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>

   <span data-ttu-id="afc6d-123">Para compatibilidad con Linux, descargar Ubuntu Server 16.04 y agregarlo mediante ```Add-AzsVMImage``` con hello parámetros siguientes: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span><span class="sxs-lookup"><span data-stu-id="afc6d-123">For Linux support, download Ubuntu Server 16.04 and add it using ```Add-AzsVMImage``` with hello following parameters: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span></span>

## <a name="add-hello-virtual-machine-scale-set"></a><span data-ttu-id="afc6d-124">Agregar conjunto de escalas de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="afc6d-124">Add hello virtual machine scale set</span></span>

<span data-ttu-id="afc6d-125">Editar Hola PowerShell siguiente para su entorno de script y vuelva a ejecutarlo tooadd un tooyour de conjunto de escala de máquina virtual Azure Marketplace de pila.</span><span class="sxs-lookup"><span data-stu-id="afc6d-125">Edit hello following PowerShell script for your environment and then run it tooadd a virtual machine scale set tooyour Azure Stack Marketplace.</span></span> 

<span data-ttu-id="afc6d-126">``$User``es la cuenta de hello que usar portal del administrador tooconnect Hola.</span><span class="sxs-lookup"><span data-stu-id="afc6d-126">``$User`` is hello account you use tooconnect hello administrator portal.</span></span> <span data-ttu-id="afc6d-127">Por ejemplo: serviceadmin@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="afc6d-127">For example, serviceadmin@contoso.onmicrosoft.com.</span></span>

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a><span data-ttu-id="afc6d-128">Eliminación de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="afc6d-128">Remove a virtual machine scale set</span></span>

<span data-ttu-id="afc6d-129">tooremove un elemento de galería de conjunto de escala máquina virtual, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="afc6d-129">tooremove a virtual machine scale set gallery item, run hello following PowerShell command:</span></span>

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> <span data-ttu-id="afc6d-130">elemento de la Galería de Hello no se quitará de forma inmediata.</span><span class="sxs-lookup"><span data-stu-id="afc6d-130">hello gallery item may not be removed immediately.</span></span> <span data-ttu-id="afc6d-131">Puede que tenga la forma en portal de hello toorefresh varias veces antes de quitarlo de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="afc6d-131">You may need toorefresh hello portal several times before it is removed from hello Marketplace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="afc6d-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="afc6d-132">Next steps</span></span>
[<span data-ttu-id="afc6d-133">Preguntas frecuentes acerca de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="afc6d-133">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

