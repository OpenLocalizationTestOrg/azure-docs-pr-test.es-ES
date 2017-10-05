---
title: Descarga de herramientas de Azure Stack desde GitHub | Microsoft Docs
description: Aprenda a descargar las herramientas necesarias para trabajar con Azure Stack.
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 589d2ea1ffed9f8ac82793132d9c91efcc60a5fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="b8ff3-103">Descarga de herramientas de Azure Stack desde GitHub</span><span class="sxs-lookup"><span data-stu-id="b8ff3-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="b8ff3-104">AzureStack-Tools es un repositorio de GitHub que hospeda módulos de PowerShell que puede usar para administrar e implementar recursos en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use to manage and deploy resources to Azure Stack.</span></span> <span data-ttu-id="b8ff3-105">Puede descargar y usar estos módulos de PowerShell para Azure Stack Development Kit, o para un cliente externo basado en Windows, si va a establecer la conectividad VPN.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-105">You can download and use these PowerShell modules to the Azure Stack Development Kit, or to a windows-based external client if you are planning to establish VPN connectivity.</span></span> <span data-ttu-id="b8ff3-106">Para obtener estas herramientas, clone el repositorio de GitHub o descargue la carpeta AzureStack-Tools.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-106">To obtain these tools, clone the GitHub repository or download the AzureStack-Tools folder.</span></span> 

<span data-ttu-id="b8ff3-107">Para clonar el repositorio, descargue [Git](https://git-scm.com/download/win) para Windows, abra una ventana del símbolo del sistema y ejecute el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="b8ff3-107">To clone the repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run the following script:</span></span>

```PowerShell
# Change directory to the root directory 
cd \

# clone the repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change to the tools directory
cd AzureStack-Tools
```

<span data-ttu-id="b8ff3-108">Para descargar la carpeta de herramientas, ejecute el script siguiente:</span><span class="sxs-lookup"><span data-stu-id="b8ff3-108">To download the tools folder, run the following script:</span></span>

```PowerShell
# Change directory to the root directory 
cd \

# Download the tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-the-modules"></a><span data-ttu-id="b8ff3-109">Funcionalidades proporcionadas por los módulos</span><span class="sxs-lookup"><span data-stu-id="b8ff3-109">Functionalities provided by the modules</span></span>

<span data-ttu-id="b8ff3-110">El repositorio AzureStack-Tools contiene los módulos de PowerShell que admiten las siguientes funcionalidades para Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="b8ff3-110">The AzureStack-Tools repository contains PowerShell modules that support the following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="b8ff3-111">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="b8ff3-111">Functionality</span></span> | <span data-ttu-id="b8ff3-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="b8ff3-112">Description</span></span> | <span data-ttu-id="b8ff3-113">¿Quién puede usar este módulo?</span><span class="sxs-lookup"><span data-stu-id="b8ff3-113">who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="b8ff3-114">Funcionalidades en la nube</span><span class="sxs-lookup"><span data-stu-id="b8ff3-114">Cloud capabilities</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="b8ff3-115">Utilice este módulo para obtener las funcionalidades en la nube de una nube.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-115">Use this module to get the cloud capabilities of a cloud.</span></span> <span data-ttu-id="b8ff3-116">Por ejemplo, con este módulo, puede obtener funcionalidades en la nube como la versión de API, los recursos de Azure Resource Manager, las extensiones de VM, etc. para las nubes de Azure Stack y Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-116">For example, you can get the cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span></span> | <span data-ttu-id="b8ff3-117">Los administradores de nube y los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-117">Cloud administrators and users.</span></span> |
| [<span data-ttu-id="b8ff3-118">Administración de procesos de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8ff3-118">Azure Stack compute administration</span></span>](azure-stack-add-vm-image.md) | <span data-ttu-id="b8ff3-119">Utilice este módulo para agregar o quitar una imagen de máquina virtual desde el marketplace de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-119">Use this module to add or remove a VM image from the Azure Stack marketplace.</span></span> | <span data-ttu-id="b8ff3-120">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-120">Cloud administrators.</span></span> |
| [<span data-ttu-id="b8ff3-121">Administración de la infraestructura de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8ff3-121">Azure Stack Infrastructure administration</span></span>](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | <span data-ttu-id="b8ff3-122">Utilice este módulo para administrar las actualizaciones, las alertas, las máquinas virtuales de infraestructura de Azure Stack, etcétera.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-122">Use this module to manage Azure Stack infrastructure VMs, alerts, updates etc.</span></span> |  <span data-ttu-id="b8ff3-123">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-123">Cloud administrators.</span></span>|
| [<span data-ttu-id="b8ff3-124">Directiva de Resource Manager para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8ff3-124">Resource Manager policy for Azure Stack</span></span>](azure-stack-policy-module.md) | <span data-ttu-id="b8ff3-125">Utilice este módulo para configurar una suscripción de Azure o un grupo de recursos de Azure con la misma disponibilidad de servicios y control de versiones que Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-125">Use this module to configure an Azure subscription or an Azure resource group with the same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="b8ff3-126">Los usuarios y administradores de nube</span><span class="sxs-lookup"><span data-stu-id="b8ff3-126">Cloud administrators and users</span></span> |
| [<span data-ttu-id="b8ff3-127">Registro con Azure</span><span class="sxs-lookup"><span data-stu-id="b8ff3-127">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="b8ff3-128">Utilice este módulo para registrar la instancia de Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-128">Use this module to register your development kit instance with Azure.</span></span> <span data-ttu-id="b8ff3-129">Después del registro, puede descargar los elementos de marketplace de Azure y usarlos en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-129">After registering, you can download the marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="b8ff3-130">Administradores de nube</span><span class="sxs-lookup"><span data-stu-id="b8ff3-130">Cloud administrators</span></span> |
| [<span data-ttu-id="b8ff3-131">Implementación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8ff3-131">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="b8ff3-132">Utilice este módulo para preparar el equipo host de Azure Stack para implementar y volver a implementar con la imagen de disco duro virtual (VHD) de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-132">Use this module to prepare the Azure Stack host computer to deploy and redeploy by using the Azure Stack Virtual Hard Disk(VHD) image.</span></span> | <span data-ttu-id="b8ff3-133">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-133">Cloud administrators.</span></span> |
| [<span data-ttu-id="b8ff3-134">Conexión a Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8ff3-134">Connecting to Azure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="b8ff3-135">Utilice este módulo para conectarse a una instancia de Azure Stack a través de PowerShell y configurar la conectividad VPN a Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-135">Use this module to connect to an Azure Stack instance through PowerShell and to configure VPN connectivity to Azure Stack.</span></span> | <span data-ttu-id="b8ff3-136">Los usuarios y administradores de nube</span><span class="sxs-lookup"><span data-stu-id="b8ff3-136">Cloud administrators and users</span></span> |
| [<span data-ttu-id="b8ff3-137">Administración de servicios de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8ff3-137">Azure Stack service administration</span></span>](azure-stack-create-offer.md) | <span data-ttu-id="b8ff3-138">Administradores de pila Azure pueden usar este módulo para crear una oferta de inquilino de forma predeterminada con una cuota de ilimitado a través de servicios de proceso, almacenamiento, red y el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-138">Azure Stack administrators can use this module to create a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span></span>   | <span data-ttu-id="b8ff3-139">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-139">Cloud administrators.</span></span>|
| [<span data-ttu-id="b8ff3-140">Validador de plantilla</span><span class="sxs-lookup"><span data-stu-id="b8ff3-140">Template validator</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="b8ff3-141">Utilice este módulo para comprobar si una plantilla nueva o existente puede implementarse en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b8ff3-141">Use this module to verify if an existing or a new template can be deployed to Azure Stack.</span></span> | <span data-ttu-id="b8ff3-142">Los usuarios y administradores de nube</span><span class="sxs-lookup"><span data-stu-id="b8ff3-142">Cloud administrators and users</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b8ff3-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8ff3-143">Next steps</span></span>
* [<span data-ttu-id="b8ff3-144">Configuración del entorno de PowerShell del usuario de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b8ff3-144">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)   
* [<span data-ttu-id="b8ff3-145">Conexión a Azure Stack Development Kit a través de una VPN</span><span class="sxs-lookup"><span data-stu-id="b8ff3-145">Connect to Azure Stack Development Kit over a VPN</span></span>](azure-stack-connect-azure-stack.md)  
