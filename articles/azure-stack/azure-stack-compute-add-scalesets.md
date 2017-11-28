---
title: "Proporcionar conjuntos de escalado de máquinas virtuales en Azure Stack"
description: "Obtenga información acerca de cómo un administrador de la nube puede agregar el escalado de máquinas virtuales a la plataforma Marketplace de Azure Stack."
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: c3ce40b182085dbd2fe54d0f6b6cbe704ab28e86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a><span data-ttu-id="960aa-103">Proporcionar conjuntos de escalado de máquinas virtuales en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="960aa-103">Make virtual machine scale sets available in Azure Stack</span></span>
<span data-ttu-id="960aa-104">Los conjuntos de escalado de máquinas virtuales son un recurso de proceso de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="960aa-104">Virtual machine scale sets are an Azure Stack compute resource.</span></span> <span data-ttu-id="960aa-105">Puede utilizarlos para implementar y administrar un conjunto de máquinas virtuales idénticas.</span><span class="sxs-lookup"><span data-stu-id="960aa-105">You can use them to deploy and manage a set of identical virtual machines.</span></span> <span data-ttu-id="960aa-106">Si todas las máquinas virtuales tienen la misma configuración, los conjuntos de escalado no requieren un aprovisionamiento previo de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="960aa-106">With all virtual machines configured the same, scale sets don’t require pre-provisioning of virtual machines.</span></span> <span data-ttu-id="960aa-107">Esto facilita la creación de servicios a gran escala cuyo objetivo son las cargas de trabajo en contenedores, de macroproceso y macrodatos.</span><span class="sxs-lookup"><span data-stu-id="960aa-107">It's easier to build large-scale services that target big compute, big data, and containerized workloads.</span></span>

<span data-ttu-id="960aa-108">Este tema le guía por el proceso de poner a disposición de los usuarios los conjuntos de escalado en la plataforma Marketplace de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="960aa-108">This topic guides you through the process to make scale sets available in the Azure Stack Marketplace.</span></span> <span data-ttu-id="960aa-109">Después de completar este procedimiento, los usuarios pueden agregar conjuntos de escalado de máquinas virtuales a sus suscripciones.</span><span class="sxs-lookup"><span data-stu-id="960aa-109">After you complete this procedure, your users can add virtual machine scale sets to their subscriptions.</span></span>

<span data-ttu-id="960aa-110">Los conjuntos de escalado de máquinas virtuales en Azure Stack son similares a los conjuntos de escalado de máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="960aa-110">Virtual machine scale sets on Azure Stack are like virtual machine scale sets on Azure.</span></span> <span data-ttu-id="960aa-111">Para obtener más información, consulte los siguientes vídeos:</span><span class="sxs-lookup"><span data-stu-id="960aa-111">For more information, see the following videos:</span></span>
* <span data-ttu-id="960aa-112">[Mark Russinovich talks Azure Scale Sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/) (Mark Russinovich habla sobre los conjuntos de escalado de Azure)</span><span class="sxs-lookup"><span data-stu-id="960aa-112">[Mark Russinovich talks Azure scale sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)</span></span>
* [<span data-ttu-id="960aa-113">Virtual Machine Scale Sets with Guy Bowerman</span><span class="sxs-lookup"><span data-stu-id="960aa-113">Virtual Machine Scale Sets with Guy Bowerman</span></span>](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

<span data-ttu-id="960aa-114">En Azure Stack, los conjuntos de escalado de máquinas virtuales no admiten escalado automático.</span><span class="sxs-lookup"><span data-stu-id="960aa-114">On Azure Stack, Virtual Machine Scale Sets do not support auto-scale.</span></span> <span data-ttu-id="960aa-115">Puede agregar más instancias a un conjunto de escalado a través del portal de Azure Stack, las plantillas de Resource Manager o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="960aa-115">You can add more instances to a scale set using the Azure Stack portal, Resource Manager templates, or PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="960aa-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="960aa-116">Prerequisites</span></span>
* <span data-ttu-id="960aa-117">**PowerShell y herramientas**</span><span class="sxs-lookup"><span data-stu-id="960aa-117">**Powershell and tools**</span></span>

   <span data-ttu-id="960aa-118">Instalación y configuración de PowerShell para Azure Stack y las herramientas de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="960aa-118">Install and configured PowerShell for Azure Stack and the Azure Stack tools.</span></span> <span data-ttu-id="960aa-119">Consulte [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md) (Ponerse en marcha con PowerShell en Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="960aa-119">See [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md).</span></span>

   <span data-ttu-id="960aa-120">Después de instalar las herramientas de Azure Stack, asegúrese de importar el siguiente módulo de PowerShell (ruta de acceso relativa a la carpeta .\ComputeAdmin en la carpeta AzureStack-Tools-master):</span><span class="sxs-lookup"><span data-stu-id="960aa-120">After you install the Azure Stack tools, make sure you import the following PowerShell module (path relative to the .\ComputeAdmin folder in the AzureStack-Tools-master folder):</span></span>

        Import-Module .\AzureStack.ComputeAdmin.psm1

* <span data-ttu-id="960aa-121">**Imagen del sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="960aa-121">**Operating system image**</span></span>

   <span data-ttu-id="960aa-122">Si no ha agregado ninguna imagen de sistema operativo a la plataforma Marketplace de Azure Stack, consulte [Add the Windows Server 2016 VM image to the Azure Stack marketplace](azure-stack-add-default-image.md) (Agregar la imagen de VM de Windows Server 2016 a la plataforma Marketplace de Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="960aa-122">If you haven’t added an operating system image to your Azure Stack Marketplace, see [Add the Windows Server 2016 VM image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>

   <span data-ttu-id="960aa-123">Para obtener compatibilidad con Linux, descargue Ubuntu Server 16.04 y agréguelo con ```Add-AzsVMImage``` con los siguientes parámetros: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span><span class="sxs-lookup"><span data-stu-id="960aa-123">For Linux support, download Ubuntu Server 16.04 and add it using ```Add-AzsVMImage``` with the following parameters: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span></span>

## <a name="add-the-virtual-machine-scale-set"></a><span data-ttu-id="960aa-124">Adición del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="960aa-124">Add the virtual machine scale set</span></span>

<span data-ttu-id="960aa-125">Edite el siguiente script de PowerShell para su entorno y, después, ejecútelo para agregar un conjunto de escalado de máquinas virtuales a la plataforma Marketplace de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="960aa-125">Edit the following PowerShell script for your environment and then run it to add a virtual machine scale set to your Azure Stack Marketplace.</span></span> 

<span data-ttu-id="960aa-126">``$User`` es la cuenta que usa para conectar el portal de administración.</span><span class="sxs-lookup"><span data-stu-id="960aa-126">``$User`` is the account you use to connect the administrator portal.</span></span> <span data-ttu-id="960aa-127">Por ejemplo: serviceadmin@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="960aa-127">For example, serviceadmin@contoso.onmicrosoft.com.</span></span>

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

## <a name="remove-a-virtual-machine-scale-set"></a><span data-ttu-id="960aa-128">Eliminación de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="960aa-128">Remove a virtual machine scale set</span></span>

<span data-ttu-id="960aa-129">Para eliminar un elemento de la galería del conjunto de escalado de máquinas virtuales, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="960aa-129">To remove a virtual machine scale set gallery item, run the following PowerShell command:</span></span>

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> <span data-ttu-id="960aa-130">Es posible que el elemento de la galería no se quite de forma inmediata.</span><span class="sxs-lookup"><span data-stu-id="960aa-130">The gallery item may not be removed immediately.</span></span> <span data-ttu-id="960aa-131">Es posible que deba actualizar el portal varias veces para que se quite de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="960aa-131">You may need to refresh the portal several times before it is removed from the Marketplace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="960aa-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="960aa-132">Next steps</span></span>
[<span data-ttu-id="960aa-133">Preguntas frecuentes acerca de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="960aa-133">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

