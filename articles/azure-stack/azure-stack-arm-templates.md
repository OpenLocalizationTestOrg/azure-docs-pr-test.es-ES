---
title: Uso de plantillas de Azure Resource Manager en Azure Stack | Microsoft Docs
description: "Obtenga información sobre cómo usar plantillas de Azure Resource Manager en Azure Stack para aprovisionar recursos."
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
ms.openlocfilehash: 228e641afefd16edc7b405a2fc1d60184ce41e96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="003a2-103">Uso de plantillas de Administrador de recursos de Azure en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="003a2-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="003a2-104">Las plantillas de Azure Resource Manager implementan y aprovisionan todos los recursos para su aplicación en una única operación coordinada.</span><span class="sxs-lookup"><span data-stu-id="003a2-104">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="003a2-105">También se pueden reimplementar plantillas para realizar cambios en los recursos del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="003a2-105">You can also redeploy templates to make changes to the resources in the resource group.</span></span>

<span data-ttu-id="003a2-106">Estas plantillas se pueden implementar con el portal de Microsoft Azure Stack, PowerShell, con la línea de comandos y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="003a2-106">These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.</span></span>

<span data-ttu-id="003a2-107">Las plantillas de inicio rápido siguientes están disponibles en [GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="003a2-107">The following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="003a2-108">Implementación de SharePoint (sin alta disponibilidad)</span><span class="sxs-lookup"><span data-stu-id="003a2-108">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="003a2-109">Use la extensión DSC de PowerShell para crear una granja de servidores de SharePoint 2013 que incluya los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="003a2-109">Use the PowerShell DSC extension to create a SharePoint 2013 farm that includes the following resources:</span></span>

* <span data-ttu-id="003a2-110">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="003a2-110">A virtual network</span></span>
* <span data-ttu-id="003a2-111">Tres cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="003a2-111">Three storage accounts</span></span>
* <span data-ttu-id="003a2-112">Dos equilibradores de carga externos</span><span class="sxs-lookup"><span data-stu-id="003a2-112">Two external load balancers</span></span>
* <span data-ttu-id="003a2-113">Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio</span><span class="sxs-lookup"><span data-stu-id="003a2-113">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="003a2-114">Una máquina virtual configurada como un servidor independiente de SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="003a2-114">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="003a2-115">Una máquina virtual configurada como una granja de servidores de SharePoint 2013 de la máquina</span><span class="sxs-lookup"><span data-stu-id="003a2-115">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="003a2-116">Implementación de AD (sin alta disponibilidad)</span><span class="sxs-lookup"><span data-stu-id="003a2-116">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="003a2-117">Use la extensión DSC de PowerShell para crear un servidor de controlador de dominio AD que incluya los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="003a2-117">Use the PowerShell DSC extension to create an AD domain controller server that includes the following resources:</span></span>

* <span data-ttu-id="003a2-118">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="003a2-118">A virtual network</span></span>
* <span data-ttu-id="003a2-119">Una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="003a2-119">One storage account</span></span>
* <span data-ttu-id="003a2-120">Un equilibrador de carga externo</span><span class="sxs-lookup"><span data-stu-id="003a2-120">One external load balancer</span></span>
* <span data-ttu-id="003a2-121">Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio</span><span class="sxs-lookup"><span data-stu-id="003a2-121">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="003a2-122">Implementación de AD/SQL (sin alta disponibilidad)</span><span class="sxs-lookup"><span data-stu-id="003a2-122">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="003a2-123">Use la extensión DSC de PowerShell para crear un servidor independiente de SQL Server 2014 que incluya los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="003a2-123">Use the PowerShell DSC extension to create a SQL Server 2014 stand-alone server that includes the following resources:</span></span>

* <span data-ttu-id="003a2-124">Una red virtual</span><span class="sxs-lookup"><span data-stu-id="003a2-124">A virtual network</span></span>
* <span data-ttu-id="003a2-125">Dos cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="003a2-125">Two storage accounts</span></span>
* <span data-ttu-id="003a2-126">Un equilibrador de carga externo</span><span class="sxs-lookup"><span data-stu-id="003a2-126">One external load balancer</span></span>
* <span data-ttu-id="003a2-127">Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio</span><span class="sxs-lookup"><span data-stu-id="003a2-127">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="003a2-128">Una máquina virtual configurada como un servidor independiente de SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="003a2-128">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="003a2-129">Extensión DSC de máquina virtual para un servidor de extracción de Automatización de Azure</span><span class="sxs-lookup"><span data-stu-id="003a2-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="003a2-130">Utilice la extensión de DSC de PowerShell para configurar Administrador de configuración Local (LCM) de una máquina virtual existente y registrarlo en un servidor de extracción de DSC de la cuenta de Automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="003a2-130">Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="003a2-131">Creación de una máquina virtual desde una imagen de usuario</span><span class="sxs-lookup"><span data-stu-id="003a2-131">Create a virtual machine from a user image</span></span>
<span data-ttu-id="003a2-132">Cree una máquina virtual desde una imagen de usuario personalizada.</span><span class="sxs-lookup"><span data-stu-id="003a2-132">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="003a2-133">Esta plantilla también implementa una red virtual (con DNS), una dirección IP pública y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="003a2-133">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="003a2-134">VM simple</span><span class="sxs-lookup"><span data-stu-id="003a2-134">Simple VM</span></span>
<span data-ttu-id="003a2-135">Implemente una máquina virtual de Windows que incluya una red virtual (con DNS), una dirección IP pública y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="003a2-135">Deploy a Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="003a2-136">Cancelación de una implementación de la plantilla en ejecución</span><span class="sxs-lookup"><span data-stu-id="003a2-136">Cancel a running template deployment</span></span>
<span data-ttu-id="003a2-137">Para cancelar la implementación de una plantilla en ejecución, use el cmdlet `Stop-AzureRmResourceGroupDeployment` de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="003a2-137">To cancel a running template deployment, use the `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="003a2-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="003a2-138">Next steps</span></span>
[<span data-ttu-id="003a2-139">Implementación de plantillas con el portal</span><span class="sxs-lookup"><span data-stu-id="003a2-139">Deploy templates with the portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="003a2-140">Información general sobre Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="003a2-140">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

