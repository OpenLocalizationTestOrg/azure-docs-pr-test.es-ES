---
title: aaaDownload pila de Azure tools desde GitHub | Documentos de Microsoft
description: "Obtenga información acerca de cómo las herramientas de toodownload necesario toowork con la pila de Azure."
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
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="34b9b-103">Descarga de herramientas de Azure Stack desde GitHub</span><span class="sxs-lookup"><span data-stu-id="34b9b-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="34b9b-104">Herramientas de AzureStack es un repositorio de GitHub que hospeda módulos de PowerShell que puede usar toomanage e implementar recursos tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="34b9b-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use toomanage and deploy resources tooAzure Stack.</span></span> <span data-ttu-id="34b9b-105">Puede descargar y usar a estos módulos toohello Kit de desarrollo de pila de Azure o tooa basados en windows externo cliente de PowerShell si tiene previsto tooestablish conectividad VPN.</span><span class="sxs-lookup"><span data-stu-id="34b9b-105">You can download and use these PowerShell modules toohello Azure Stack Development Kit, or tooa windows-based external client if you are planning tooestablish VPN connectivity.</span></span> <span data-ttu-id="34b9b-106">tooobtain estas herramientas, clonar el repositorio de GitHub de Hola o hello AzureStack herramientas carpeta de descarga.</span><span class="sxs-lookup"><span data-stu-id="34b9b-106">tooobtain these tools, clone hello GitHub repository or download hello AzureStack-Tools folder.</span></span> 

<span data-ttu-id="34b9b-107">repositorio de hello tooclone, descargue [Git](https://git-scm.com/download/win) para Windows, abra una ventana del símbolo del sistema y ejecute la siguiente secuencia de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="34b9b-107">tooclone hello repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

<span data-ttu-id="34b9b-108">carpeta de herramientas en hello toodownload, ejecute la siguiente secuencia de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="34b9b-108">toodownload hello tools folder, run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a><span data-ttu-id="34b9b-109">Funcionalidades proporcionadas por módulos de Hola</span><span class="sxs-lookup"><span data-stu-id="34b9b-109">Functionalities provided by hello modules</span></span>

<span data-ttu-id="34b9b-110">repositorio de Hello AzureStack-Tools contiene los módulos de PowerShell que admiten Hola siga funcionalidades para la pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="34b9b-110">hello AzureStack-Tools repository contains PowerShell modules that support hello following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="34b9b-111">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="34b9b-111">Functionality</span></span> | <span data-ttu-id="34b9b-112">Descripción</span><span class="sxs-lookup"><span data-stu-id="34b9b-112">Description</span></span> | <span data-ttu-id="34b9b-113">¿Quién puede usar este módulo?</span><span class="sxs-lookup"><span data-stu-id="34b9b-113">who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="34b9b-114">Funcionalidades en la nube</span><span class="sxs-lookup"><span data-stu-id="34b9b-114">Cloud capabilities</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="34b9b-115">Utilice este capacidades de módulo tooget hello en la nube de una nube.</span><span class="sxs-lookup"><span data-stu-id="34b9b-115">Use this module tooget hello cloud capabilities of a cloud.</span></span> <span data-ttu-id="34b9b-116">Por ejemplo, puede obtener capacidades de la nube de hello como versión de API, los recursos de Azure Resource Manager, etc. de extensiones de máquina virtual para la pila de Azure y Azure nubes mediante este módulo.</span><span class="sxs-lookup"><span data-stu-id="34b9b-116">For example, you can get hello cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span></span> | <span data-ttu-id="34b9b-117">Usuarios y administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="34b9b-117">Cloud administrators and users.</span></span> |
| [<span data-ttu-id="34b9b-118">Administración de procesos de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34b9b-118">Azure Stack compute administration</span></span>](azure-stack-add-vm-image.md) | <span data-ttu-id="34b9b-119">Use este módulo tooadd o quitar una imagen de VM de marketplace de Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="34b9b-119">Use this module tooadd or remove a VM image from hello Azure Stack marketplace.</span></span> | <span data-ttu-id="34b9b-120">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="34b9b-120">Cloud administrators.</span></span> |
| [<span data-ttu-id="34b9b-121">Administración de la infraestructura de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34b9b-121">Azure Stack Infrastructure administration</span></span>](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | <span data-ttu-id="34b9b-122">Use esta infraestructura de Azure pila módulo toomanage máquinas virtuales, alertas, actualizaciones etcetera.</span><span class="sxs-lookup"><span data-stu-id="34b9b-122">Use this module toomanage Azure Stack infrastructure VMs, alerts, updates etc.</span></span> |  <span data-ttu-id="34b9b-123">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="34b9b-123">Cloud administrators.</span></span>|
| [<span data-ttu-id="34b9b-124">Directiva de Resource Manager para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34b9b-124">Resource Manager policy for Azure Stack</span></span>](azure-stack-policy-module.md) | <span data-ttu-id="34b9b-125">Utilice este tooconfigure módulo una suscripción de Azure o grupo de un recurso de Azure con hello mismo control de versiones y el servicio de disponibilidad como la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="34b9b-125">Use this module tooconfigure an Azure subscription or an Azure resource group with hello same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="34b9b-126">Usuarios y administradores de la nube</span><span class="sxs-lookup"><span data-stu-id="34b9b-126">Cloud administrators and users</span></span> |
| [<span data-ttu-id="34b9b-127">Registro con Azure</span><span class="sxs-lookup"><span data-stu-id="34b9b-127">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="34b9b-128">Utilice este módulo tooregister la instancia del kit de desarrollo con Azure.</span><span class="sxs-lookup"><span data-stu-id="34b9b-128">Use this module tooregister your development kit instance with Azure.</span></span> <span data-ttu-id="34b9b-129">Después de registrar, puede descargar los elementos de marketplace de Hola de Azure y usarlos en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="34b9b-129">After registering, you can download hello marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="34b9b-130">Administradores de nube</span><span class="sxs-lookup"><span data-stu-id="34b9b-130">Cloud administrators</span></span> |
| [<span data-ttu-id="34b9b-131">Implementación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34b9b-131">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="34b9b-132">Utilice este toodeploy del equipo de host de módulo tooprepare hello Azure pila y volver a implementar mediante hello Disk(VHD) de disco duro Virtual de Azure pila imagen.</span><span class="sxs-lookup"><span data-stu-id="34b9b-132">Use this module tooprepare hello Azure Stack host computer toodeploy and redeploy by using hello Azure Stack Virtual Hard Disk(VHD) image.</span></span> | <span data-ttu-id="34b9b-133">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="34b9b-133">Cloud administrators.</span></span> |
| [<span data-ttu-id="34b9b-134">Pila de conexión tooAzure</span><span class="sxs-lookup"><span data-stu-id="34b9b-134">Connecting tooAzure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="34b9b-135">Utilice esta instancia de Azure pila módulo tooconnect tooan a través de PowerShell y tooconfigure tooAzure de conectividad VPN pila.</span><span class="sxs-lookup"><span data-stu-id="34b9b-135">Use this module tooconnect tooan Azure Stack instance through PowerShell and tooconfigure VPN connectivity tooAzure Stack.</span></span> | <span data-ttu-id="34b9b-136">Usuarios y administradores de la nube</span><span class="sxs-lookup"><span data-stu-id="34b9b-136">Cloud administrators and users</span></span> |
| [<span data-ttu-id="34b9b-137">Administración de servicios de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34b9b-137">Azure Stack service administration</span></span>](azure-stack-create-offer.md) | <span data-ttu-id="34b9b-138">Azure administradores de pila pueden usar este toocreate módulo ofrecen un inquilino de forma predeterminada con una cuota de ilimitado a través de servicios de proceso, almacenamiento, red y el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="34b9b-138">Azure Stack administrators can use this module toocreate a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span></span>   | <span data-ttu-id="34b9b-139">Administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="34b9b-139">Cloud administrators.</span></span>|
| [<span data-ttu-id="34b9b-140">Validador de plantilla</span><span class="sxs-lookup"><span data-stu-id="34b9b-140">Template validator</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="34b9b-141">Use este módulo tooverify si una plantilla nueva o existente puede ser implementado tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="34b9b-141">Use this module tooverify if an existing or a new template can be deployed tooAzure Stack.</span></span> | <span data-ttu-id="34b9b-142">Usuarios y administradores de la nube</span><span class="sxs-lookup"><span data-stu-id="34b9b-142">Cloud administrators and users</span></span> |


## <a name="next-steps"></a><span data-ttu-id="34b9b-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34b9b-143">Next steps</span></span>
* [<span data-ttu-id="34b9b-144">Configurar el entorno de PowerShell del usuario de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="34b9b-144">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)   
* [<span data-ttu-id="34b9b-145">Conectar tooAzure Kit de desarrollo de pila a través de una VPN</span><span class="sxs-lookup"><span data-stu-id="34b9b-145">Connect tooAzure Stack Development Kit over a VPN</span></span>](azure-stack-connect-azure-stack.md)  
