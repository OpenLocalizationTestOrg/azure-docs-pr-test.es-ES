---
title: Ejemplos de la CLI de Azure para Windows | Microsoft Docs
description: Ejemplos de la CLI de Azure para Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f4b2e8a5583855df7472af3fbef01ac641caf6bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a><span data-ttu-id="3912b-103">Ejemplos de la CLI de Azure para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="3912b-103">Azure CLI Samples for Windows virtual machines</span></span>

<span data-ttu-id="3912b-104">En la tabla siguiente se incluyen vínculos a scripts de Bash creados con la CLI de Azure que implementan máquinas virtuales Windows.</span><span class="sxs-lookup"><span data-stu-id="3912b-104">The following table includes links to bash scripts built using the Azure CLI that deploy Windows virtual machines.</span></span>

| | |
|---|---|
|<span data-ttu-id="3912b-105">**Creación de máquinas virtuales**</span><span class="sxs-lookup"><span data-stu-id="3912b-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="3912b-106">Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3912b-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-107">Crea una máquina virtual Windows con una configuración mínima.</span><span class="sxs-lookup"><span data-stu-id="3912b-107">Creates a Windows virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="3912b-108">Creación una máquina virtual completamente configurada</span><span class="sxs-lookup"><span data-stu-id="3912b-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-109">Crea un grupo de recursos, una máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="3912b-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="3912b-110">Creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3912b-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-111">Crea varias máquinas virtuales de alta disponibilidad y una configuración de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="3912b-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="3912b-112">Creación de una máquina virtual y ejecución de un script de configuración</span><span class="sxs-lookup"><span data-stu-id="3912b-112">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-113">Crea una máquina virtual y usa la extensión de script personalizado de Azure para instalar IIS.</span><span class="sxs-lookup"><span data-stu-id="3912b-113">Creates a virtual machine and uses the Azure Custom Script extension to install IIS.</span></span> |
| [<span data-ttu-id="3912b-114">Creación de una máquina virtual y ejecución de una configuración de DSC</span><span class="sxs-lookup"><span data-stu-id="3912b-114">Create a VM and run DSC configuration</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-115">Crea una máquina virtual y usa la extensión de configuración de estado deseado (DSC) de Azure para instalar IIS.</span><span class="sxs-lookup"><span data-stu-id="3912b-115">Creates a virtual machine and uses the Azure Desired State Configuration (DSC) extension to install IIS.</span></span> |
|<span data-ttu-id="3912b-116">**Máquinas virtuales de red**</span><span class="sxs-lookup"><span data-stu-id="3912b-116">**Network virtual machines**</span></span>||
| [<span data-ttu-id="3912b-117">Protección del tráfico de red entre máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="3912b-117">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-118">Crea dos máquinas virtuales, todos los recursos relacionados y grupos de seguridad de red internos y externos (NSG).</span><span class="sxs-lookup"><span data-stu-id="3912b-118">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="3912b-119">**Protección de máquinas virtuales**</span><span class="sxs-lookup"><span data-stu-id="3912b-119">**Secure virtual machines**</span></span>||
| [<span data-ttu-id="3912b-120">Cifrado de una máquina virtual y discos de datos</span><span class="sxs-lookup"><span data-stu-id="3912b-120">Encrypt a VM and data disks</span></span>](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-121">Crea una instancia de Azure Key Vault, una clave de cifrado y una entidad de servicio, y luego cifra una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3912b-121">Creates an Azure Key Vault, encryption key, and service principal, then encrypts a VM.</span></span> |
|<span data-ttu-id="3912b-122">**Supervisión de máquinas virtuales**</span><span class="sxs-lookup"><span data-stu-id="3912b-122">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="3912b-123">Supervisión de una máquina virtual con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="3912b-123">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="3912b-124">Crea una máquina virtual, instala el agente de Operations Management Suite e inscribe la máquina virtual en un área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="3912b-124">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
| | |
