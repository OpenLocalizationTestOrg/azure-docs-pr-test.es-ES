---
title: "Introducción al agente de máquina Virtual aaaAzure | Documentos de Microsoft"
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
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="ebbda-103">Información general del agente de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="ebbda-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="ebbda-104">Hola agente de máquina Virtual de Microsoft Azure (agente de AM) es un proceso protegido, ligero que administra la interacción de VM con hello controlador de tejido de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbda-104">hello Microsoft Azure Virtual Machine Agent (AM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="ebbda-105">Hola agente de máquina virtual tiene un rol principal en habilitar y ejecutar las extensiones de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbda-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="ebbda-106">Las extensiones de VM habilitan la configuración posterior a la implementación de máquinas virtuales, como la instalación y configuración de software.</span><span class="sxs-lookup"><span data-stu-id="ebbda-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="ebbda-107">Extensiones de máquina virtual también habilitar características de recuperación como restablecer la contraseña administrativa de Hola de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ebbda-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="ebbda-108">Sin Hola agente de máquina virtual de Azure, no se puede ejecutar las extensiones de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ebbda-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="ebbda-109">Este documento describe la instalación, la detección y eliminación de hello agente de máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbda-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="ebbda-110">Instalar agente de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="ebbda-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="ebbda-111">Imagen de la galería de Azure</span><span class="sxs-lookup"><span data-stu-id="ebbda-111">Azure gallery image</span></span>

<span data-ttu-id="ebbda-112">Hello Azure VM Agent está instalado de forma predeterminada en cualquier máquina virtual de Windows implementada a partir de una imagen de la Galería de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbda-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="ebbda-113">Al implementar una imagen de la Galería de Azure de hello Portal, PowerShell, interfaz de línea de comandos o una plantilla de Azure Resource Manager, instalarse hello que también es el agente de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbda-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="ebbda-114">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="ebbda-114">Manual installation</span></span>

<span data-ttu-id="ebbda-115">agente de máquina virtual de Windows Hello puede instalarse manualmente mediante un paquete de Windows installer.</span><span class="sxs-lookup"><span data-stu-id="ebbda-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="ebbda-116">La instalación manual puede ser necesaria cuando se crea una imagen de máquina virtual personalizada que se implementará en Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbda-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="ebbda-117">Hola de toomanually instalar agente de máquina virtual de Windows, descargue el instalador de agente de máquina virtual de Hola desde esta ubicación [descarga del agente de Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="ebbda-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="ebbda-118">Hola agente de máquina virtual se puede instalar haciendo doble clic en el archivo de instalador de windows hello.</span><span class="sxs-lookup"><span data-stu-id="ebbda-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="ebbda-119">Para una instalación desatendida o automatizada de agente de máquina virtual de Hola, ejecute hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="ebbda-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="ebbda-120">Detectar Hola agente de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ebbda-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="ebbda-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebbda-121">PowerShell</span></span>

<span data-ttu-id="ebbda-122">módulo de PowerShell de administrador de recursos de Azure de Hello puede ser usado tooretrieve información acerca de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbda-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="ebbda-123">Ejecuta `Get-AzureRmVM` devuelve una gran cantidad de información incluidas Hola Hola agente de máquina virtual de Azure en el estado de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ebbda-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="ebbda-124">Hola siguiente es un subconjunto de hello `Get-AzureRmVM` salida.</span><span class="sxs-lookup"><span data-stu-id="ebbda-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="ebbda-125">Hola aviso `ProvisionVMAgent` propiedad anidada dentro de `OSProfile`, esta propiedad puede ser usado toodetermine si agente de máquina virtual de Hola se ha implementado toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ebbda-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="ebbda-126">Hola siguiente secuencia de comandos puede ser tooreturn usa una lista concisa de nombres de máquina virtual y el estado de Hola de hello agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ebbda-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="ebbda-127">Detección manual</span><span class="sxs-lookup"><span data-stu-id="ebbda-127">Manual Detection</span></span>

<span data-ttu-id="ebbda-128">Cuando se registran en tooa VM de Windows Azure, el Administrador de tareas puede ser usado tooexamine procesos en ejecución.</span><span class="sxs-lookup"><span data-stu-id="ebbda-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="ebbda-129">toocheck para hello agente de máquina virtual de Azure, abra el Administrador de tareas > haga clic en la ficha de detalles de Hola y busque un nombre de proceso `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="ebbda-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="ebbda-130">presencia de Hola de este proceso indica que Hola VM agent esté instalado.</span><span class="sxs-lookup"><span data-stu-id="ebbda-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="ebbda-131">Actualizar Hola agente de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ebbda-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="ebbda-132">Agente para Windows de Hello Azure VM se actualiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ebbda-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="ebbda-133">Como nuevas máquinas virtuales implementada tooAzure, recibirán el agente de máquina virtual más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebbda-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="ebbda-134">Imágenes de máquina virtual personalizadas deben ser agente tooinclude actualizadas manualmente Hola de nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ebbda-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
