---
title: plantillas de Azure Resource Manager aaaUse en pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse plantillas de Azure Resource Manager en recursos de tooprovision de pila de Azure."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="4702a-103">Uso de plantillas de Administrador de recursos de Azure en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4702a-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="4702a-104">Plantillas de administrador de recursos de Azure implementación y aprovisionar todos los recursos de Hola para su aplicación en una única operación coordinada.</span><span class="sxs-lookup"><span data-stu-id="4702a-104">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="4702a-105">También puede volver a implementar plantillas toomake cambios toohello recursos en grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4702a-105">You can also redeploy templates toomake changes toohello resources in hello resource group.</span></span>

<span data-ttu-id="4702a-106">Estas plantillas se pueden implementar con el portal de Microsoft Azure pila hello, PowerShell, línea de comandos de Hola y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4702a-106">These templates can be deployed with hello Microsoft Azure Stack portal, PowerShell, hello command line, and Visual Studio.</span></span>

<span data-ttu-id="4702a-107">Después de plantillas de inicio rápido de Hello está disponible en [GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="4702a-107">hello following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="4702a-108">Implementación de SharePoint (sin alta disponibilidad)</span><span class="sxs-lookup"><span data-stu-id="4702a-108">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="4702a-109">Usar Hola granja de toocreate un servidor de SharePoint 2013 de extensión de DSC de PowerShell que incluye Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4702a-109">Use hello PowerShell DSC extension toocreate a SharePoint 2013 farm that includes hello following resources:</span></span>

* <span data-ttu-id="4702a-110">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="4702a-110">A virtual network</span></span>
* <span data-ttu-id="4702a-111">Tres cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4702a-111">Three storage accounts</span></span>
* <span data-ttu-id="4702a-112">Dos equilibradores de carga externos</span><span class="sxs-lookup"><span data-stu-id="4702a-112">Two external load balancers</span></span>
* <span data-ttu-id="4702a-113">Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio</span><span class="sxs-lookup"><span data-stu-id="4702a-113">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="4702a-114">Una máquina virtual configurada como un servidor independiente de SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="4702a-114">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="4702a-115">Una máquina virtual configurada como una granja de servidores de SharePoint 2013 de la máquina</span><span class="sxs-lookup"><span data-stu-id="4702a-115">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="4702a-116">Implementación de AD (sin alta disponibilidad)</span><span class="sxs-lookup"><span data-stu-id="4702a-116">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="4702a-117">Utilice toocreate de extensión de DSC de PowerShell de hello un servidor de controlador de dominio de AD que incluye Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4702a-117">Use hello PowerShell DSC extension toocreate an AD domain controller server that includes hello following resources:</span></span>

* <span data-ttu-id="4702a-118">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="4702a-118">A virtual network</span></span>
* <span data-ttu-id="4702a-119">Una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4702a-119">One storage account</span></span>
* <span data-ttu-id="4702a-120">Un equilibrador de carga externo</span><span class="sxs-lookup"><span data-stu-id="4702a-120">One external load balancer</span></span>
* <span data-ttu-id="4702a-121">Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio</span><span class="sxs-lookup"><span data-stu-id="4702a-121">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="4702a-122">Implementación de AD/SQL (sin alta disponibilidad)</span><span class="sxs-lookup"><span data-stu-id="4702a-122">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="4702a-123">Usar Hola DSC de PowerShell extensión toocreate un SQL Server 2014 server independiente que incluye Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4702a-123">Use hello PowerShell DSC extension toocreate a SQL Server 2014 stand-alone server that includes hello following resources:</span></span>

* <span data-ttu-id="4702a-124">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="4702a-124">A virtual network</span></span>
* <span data-ttu-id="4702a-125">Dos cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="4702a-125">Two storage accounts</span></span>
* <span data-ttu-id="4702a-126">Un equilibrador de carga externo</span><span class="sxs-lookup"><span data-stu-id="4702a-126">One external load balancer</span></span>
* <span data-ttu-id="4702a-127">Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio</span><span class="sxs-lookup"><span data-stu-id="4702a-127">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="4702a-128">Una máquina virtual configurada como un servidor independiente de SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="4702a-128">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="4702a-129">Extensión DSC de máquina virtual para un servidor de extracción de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="4702a-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="4702a-130">Utilice tooconfigure de extensión de DSC de PowerShell de hello una máquina virtual existente Administrador de configuración Local (LCM) y registrar tooan servidor de extracción de DSC de Azure automatización de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="4702a-130">Use hello PowerShell DSC extension tooconfigure an existing virtual machine Local Configuration Manager (LCM) and register it tooan Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="4702a-131">Creación de una máquina virtual desde una imagen de usuario</span><span class="sxs-lookup"><span data-stu-id="4702a-131">Create a virtual machine from a user image</span></span>
<span data-ttu-id="4702a-132">Cree una máquina virtual desde una imagen de usuario personalizada.</span><span class="sxs-lookup"><span data-stu-id="4702a-132">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="4702a-133">Esta plantilla también implementa una red virtual (con DNS), una dirección IP pública y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="4702a-133">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="4702a-134">VM simple</span><span class="sxs-lookup"><span data-stu-id="4702a-134">Simple VM</span></span>
<span data-ttu-id="4702a-135">Implemente una máquina virtual de Windows que incluya una red virtual (con DNS), una dirección IP pública y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="4702a-135">Deploy a Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="4702a-136">Cancelación de una implementación de la plantilla en ejecución</span><span class="sxs-lookup"><span data-stu-id="4702a-136">Cancel a running template deployment</span></span>
<span data-ttu-id="4702a-137">toocancel una implementación de plantilla de ejecución, utilice hello `Stop-AzureRmResourceGroupDeployment` cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4702a-137">toocancel a running template deployment, use hello `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4702a-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4702a-138">Next steps</span></span>
[<span data-ttu-id="4702a-139">Implementación de plantillas con el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="4702a-139">Deploy templates with hello portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="4702a-140">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4702a-140">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

