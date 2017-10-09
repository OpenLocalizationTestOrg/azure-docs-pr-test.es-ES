---
title: "aaaInstall y configurar PowerShell para inicio rápido de la pila de Azure | Documentos de Microsoft"
description: Aprenda a instalar y configurar PowerShell para Azure Stack.
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
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: bb0bed983a09e32dbaaa39159b1d6d8bae7ea690
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="8bec3-103">Póngase a trabajar con PowerShell en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8bec3-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="8bec3-104">Este artículo es un tooinstall de inicio rápido y configurar el entorno de la pila de Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bec3-104">This article is a quick start tooinstall and configure Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="8bec3-105">Este script proporcionado en este artículo es hello de ámbito tooby **operador Azure pila** solo.</span><span class="sxs-lookup"><span data-stu-id="8bec3-105">This script provided in this article is scoped tooby hello **Azure Stack operator** only.</span></span>

<span data-ttu-id="8bec3-106">En este artículo es una versión comprimida de los pasos de hello descrito en hello [instale PowerShell]( azure-stack-powershell-install.md), [descargar herramientas]( azure-stack-powershell-download.md), [configurar el entorno de PowerShell del operador de hello Azure pila]( azure-stack-powershell-configure-admin.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="8bec3-106">This article is a condensed version of hello steps described in hello [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), [Configure hello Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="8bec3-107">Mediante el uso de secuencias de comandos de hello en este tema, puede configurar PowerShell para entornos de pila de Azure que se implementan con Azure Active Directory o los servicios de federación de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8bec3-107">By using hello scripts in this topic, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services.</span></span>  


## <a name="set-up-powershell-for-aad-based-deployments"></a><span data-ttu-id="8bec3-108">Configuración de PowerShell para las implementaciones basadas en AAD</span><span class="sxs-lookup"><span data-stu-id="8bec3-108">Set up PowerShell for AAD based deployments</span></span>

<span data-ttu-id="8bec3-109">Inicie sesión en tooyour Kit de desarrollo de pila de Azure, o un cliente externo basado en Windows si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="8bec3-109">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="8bec3-110">Abra una sesión de PowerShell ISE con privilegios elevados y ejecute hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="8bec3-110">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell
# Specify Azure Active Directory tenant name
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import hello connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure hello cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $TenantName `
  -EnvironmentName AzureStackAdmin

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="8bec3-111">Configuración de PowerShell para las implementaciones basadas en AD FS</span><span class="sxs-lookup"><span data-stu-id="8bec3-111">Set up PowerShell for AD FS based deployments</span></span> 

<span data-ttu-id="8bec3-112">Inicie sesión en tooyour Kit de desarrollo de pila de Azure, o un cliente externo basado en Windows si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="8bec3-112">Sign in tooyour Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="8bec3-113">Abra una sesión de PowerShell ISE con privilegios elevados y ejecute hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="8bec3-113">Open an elevated PowerShell ISE session and run hello following script:</span></span>

```powershell

# Set hello module repository and hello execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. toouninstall, close all hello active PowerShell sessions and run hello following command:
Get-Module -ListAvailable | `
  where-Object {$_.Name -like “Azure*”} | `
  Uninstall-Module

# Install PowerShell for Azure Stack
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.10 `
  -Force 

# Download Azure Stack tools from GitHub and import hello connect module
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module `
  .\Connect\AzureStack.Connect.psm1

# Configure hello cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.local.azurestack.external/" `
  -EnableAdfsAuthentication:$true

$TenantID = Get-AzsDirectoryTenantId `
  -ADFS `
  -EnvironmentName "AzureStackAdmin"

# Sign-in toohello administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="test-hello-connectivity"></a><span data-ttu-id="8bec3-114">Probar la conectividad de Hola</span><span class="sxs-lookup"><span data-stu-id="8bec3-114">Test hello connectivity</span></span>

<span data-ttu-id="8bec3-115">Ahora que ha configurado PowerShell, puede probar configuración de hello mediante la creación de un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="8bec3-115">Now that you’ve configured PowerShell, you can test hello configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

<span data-ttu-id="8bec3-116">Cuando se crea el grupo de recursos de hello, salida del cmdlet hello tiene la propiedad de estado de aprovisionamiento de hello establecida demasiado "correcta".</span><span class="sxs-lookup"><span data-stu-id="8bec3-116">When hello resource group is created, hello cmdlet output has hello Provisioning state property set too"Succeeded."</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bec3-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8bec3-117">Next steps</span></span>

* [<span data-ttu-id="8bec3-118">Instalación y configuración de la CLI</span><span class="sxs-lookup"><span data-stu-id="8bec3-118">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="8bec3-119">Desarrollo de plantillas</span><span class="sxs-lookup"><span data-stu-id="8bec3-119">Develop templates</span></span>](azure-stack-develop-templates.md)







