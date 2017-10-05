---
title: "Información general del agente de máquina virtual de Azure | Microsoft Docs"
description: "Información general del agente de máquina virtual de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="aa1d4-103">Información general del agente de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="aa1d4-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="aa1d4-104">El agente de máquina virtual de Microsoft Azure (agente VM) es un proceso ligero y seguro que administra la interacción de VM con el controlador de tejido de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="aa1d4-105">El agente de VM tiene un rol principal que consiste en habilitar y ejecutar extensiones de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="aa1d4-106">Las extensiones de VM habilitan la configuración posterior a la implementación de máquinas virtuales, como la instalación y configuración de software.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="aa1d4-107">Las extensiones de máquina virtual también habilitan características de recuperación, como el restablecimiento de la contraseña administrativa de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="aa1d4-108">Sin el agente de VM de Azure, no se pueden ejecutar las extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="aa1d4-109">En este documento se describe la instalación, detección y eliminación del agente de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="aa1d4-110">Instalar el agente de VM</span><span class="sxs-lookup"><span data-stu-id="aa1d4-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="aa1d4-111">Imagen de la galería de Azure</span><span class="sxs-lookup"><span data-stu-id="aa1d4-111">Azure gallery image</span></span>

<span data-ttu-id="aa1d4-112">El agente de VM de Azure se instala de forma predeterminada en cualquier máquina virtual Windows implementada a partir de una imagen de la galería de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="aa1d4-113">Al implementar una imagen de la galería de Azure desde el portal, PowerShell, la interfaz de la línea de comandos o una plantilla de Azure Resource Manager, también se instalará el agente de VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="aa1d4-114">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="aa1d4-114">Manual installation</span></span>

<span data-ttu-id="aa1d4-115">El agente de VM de Windows puede instalarse manualmente mediante un paquete de Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="aa1d4-116">La instalación manual puede ser necesaria cuando se crea una imagen de máquina virtual personalizada que se implementará en Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="aa1d4-117">Para instalar manualmente el agente de VM de Windows, descargue el instalador del agente de VM desde esta ubicación de [descarga del agente de VM de Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="aa1d4-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="aa1d4-118">El agente de VM se puede instalar haciendo doble clic en el archivo de Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="aa1d4-119">Para una instalación automatizada o desatendida del agente de VM, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="aa1d4-120">Detección del agente de VM</span><span class="sxs-lookup"><span data-stu-id="aa1d4-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="aa1d4-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa1d4-121">PowerShell</span></span>

<span data-ttu-id="aa1d4-122">El módulo de PowerShell de Azure Resource Manager puede utilizarse para recuperar información sobre Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="aa1d4-123">La ejecución de `Get-AzureRmVM` devuelve una gran cantidad de información que incluye el estado de aprovisionamiento para el agente de VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="aa1d4-124">Lo siguiente es solo un subconjunto de la salida `Get-AzureRmVM`.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="aa1d4-125">Observe la propiedad `ProvisionVMAgent` anidada dentro de `OSProfile`. Esta propiedad se puede utilizar para determinar si el agente de VM se ha implementado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="aa1d4-126">El siguiente script se puede utilizar para devolver una lista concisa de nombres de máquina virtual y el estado del agente de VM.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="aa1d4-127">Detección manual</span><span class="sxs-lookup"><span data-stu-id="aa1d4-127">Manual Detection</span></span>

<span data-ttu-id="aa1d4-128">Cuando inicia sesión en una VM de Windows Azure, el administrador de tareas se puede usar para examinar los procesos en ejecución.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="aa1d4-129">Para comprobar el agente de VM de Azure, abra el Administrador de tareas > haga clic en la pestaña Detalles y busque un nombre de proceso `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="aa1d4-130">La presencia de este proceso indica que el agente de VM está instalado.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="aa1d4-131">Actualización del agente de VM</span><span class="sxs-lookup"><span data-stu-id="aa1d4-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="aa1d4-132">El agente de VM de Azure para Windows se actualiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="aa1d4-133">A medida que se implementan nuevas máquinas virtuales en Azure, reciben el agente de VM más reciente.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="aa1d4-134">Las imágenes de VM personalizadas se deben actualizar manualmente para que incluya el nuevo agente de VM.</span><span class="sxs-lookup"><span data-stu-id="aa1d4-134">Custom VM images should be manually updated to include the new VM agent.</span></span>