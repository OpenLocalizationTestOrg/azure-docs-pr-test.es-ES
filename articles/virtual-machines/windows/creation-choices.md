---
title: aaaDifferent formas toocreate una VM de Windows en Azure | Documentos de Microsoft
description: "Muestra diferentes maneras de hello toocreate una máquina virtual de Windows con el Administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="26479-103">Diferentes maneras toocreate una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="26479-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="26479-104">Azure ofrece toocreate de distintas formas una máquina virtual porque las máquinas virtuales son adecuadas para fines y los distintos usuarios.</span><span class="sxs-lookup"><span data-stu-id="26479-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="26479-105">Esto significa que necesita toomake algunas decisiones sobre la máquina virtual de Hola y cómo toocreate lo.</span><span class="sxs-lookup"><span data-stu-id="26479-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="26479-106">Este artículo proporciona un resumen de estas opciones y vincula tooinstructions.</span><span class="sxs-lookup"><span data-stu-id="26479-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="26479-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="26479-107">Azure portal</span></span>
<span data-ttu-id="26479-108">El uso de hello portal de Azure es un tootry de manera sencilla a una máquina virtual, sobre todo si se está empezando con Azure.</span><span class="sxs-lookup"><span data-stu-id="26479-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="26479-109">Crear una máquina virtual con Windows y portal de Hola</span><span class="sxs-lookup"><span data-stu-id="26479-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="26479-110">Plantilla</span><span class="sxs-lookup"><span data-stu-id="26479-110">Template</span></span>
<span data-ttu-id="26479-111">Las máquinas virtuales requieren una combinación de recursos (por ejemplo, conjuntos de disponibilidad y cuentas de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="26479-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="26479-112">En lugar de implementar y administrar cada recurso por separado, puede crear una plantilla de Azure Resource Manager que implementa y aprovisiona todos los recursos de hello en una única operación coordinada.</span><span class="sxs-lookup"><span data-stu-id="26479-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="26479-113">Creación de una máquina virtual Windows con una plantilla del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="26479-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="26479-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="26479-114">Azure PowerShell</span></span>
<span data-ttu-id="26479-115">Si prefiere trabajar en un shell de comandos, puede usar PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="26479-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="26479-116">Creación de una máquina virtual Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="26479-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="26479-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="26479-117">Visual Studio</span></span>
<span data-ttu-id="26479-118">Usar Visual Studio toobuild, administrar e implementar las máquinas virtuales con hello Azure Tools para Visual Studio y Hola SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="26479-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="26479-119">Herramientas de Azure para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="26479-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

