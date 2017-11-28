---
title: "Guía de inicio rápido de instalación y configuración de PowerShell para Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: d0fc07f20937d4867c59930b13f6aed4aa37f98d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="91e9d-103">Póngase a trabajar con PowerShell en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="91e9d-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="91e9d-104">Este artículo es una guía de inicio rápido para instalar y configurar el entorno de Azure Stack con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91e9d-104">This article is a quick start to install and configure Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="91e9d-105">El script proporcionado en este artículo solo viene delimitado por el **operador de Azure Stack**.</span><span class="sxs-lookup"><span data-stu-id="91e9d-105">This script provided in this article is scoped to by the **Azure Stack operator** only.</span></span>

<span data-ttu-id="91e9d-106">Este artículo es una versión comprimida de los pasos descritos en los artículos [Instalación de PowerShell]( azure-stack-powershell-install.md), [Descarga de herramientas]( azure-stack-powershell-download.md) y [Configuración del entorno de PowerShell del operador de Azure Stack]( azure-stack-powershell-configure-admin.md).</span><span class="sxs-lookup"><span data-stu-id="91e9d-106">This article is a condensed version of the steps described in the [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), [Configure the Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="91e9d-107">Mediante el uso de scripts en este tema, puede configurar PowerShell para entornos de Azure Stack que se implementan con Azure Active Directory o con los Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="91e9d-107">By using the scripts in this topic, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services.</span></span>  


## <a name="set-up-powershell-for-aad-based-deployments"></a><span data-ttu-id="91e9d-108">Configuración de PowerShell para las implementaciones basadas en AAD</span><span class="sxs-lookup"><span data-stu-id="91e9d-108">Set up PowerShell for AAD based deployments</span></span>

<span data-ttu-id="91e9d-109">Inicie sesión en Azure Stack Development Kit o en un cliente externo basado en Windows, si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="91e9d-109">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="91e9d-110">Abra una sesión de PowerShell ISE con privilegios elevados y ejecute el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="91e9d-110">Open an elevated PowerShell ISE session and run the following script:</span></span>

```powershell
# Specify Azure Active Directory tenant name
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set the module repository and the execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
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

# Download Azure Stack tools from GitHub and import the connect module
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

# Configure the cloud administrator’s PowerShell environment.
Add-AzureRMEnvironment `
  -Name "AzureStackAdmin" `
  -ArmEndpoint "https://adminmanagement.local.azurestack.external"

Set-AzureRmEnvironment `
  -Name "AzureStackAdmin" `
  -GraphAudience "https://graph.windows.net/"

$TenantID = Get-AzsDirectoryTenantId `
  -AADTenantName $TenantName `
  -EnvironmentName AzureStackAdmin

# Sign-in to the administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="91e9d-111">Configuración de PowerShell para las implementaciones basadas en AD FS</span><span class="sxs-lookup"><span data-stu-id="91e9d-111">Set up PowerShell for AD FS based deployments</span></span> 

<span data-ttu-id="91e9d-112">Inicie sesión en Azure Stack Development Kit o en un cliente externo basado en Windows, si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="91e9d-112">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="91e9d-113">Abra una sesión de PowerShell ISE con privilegios elevados y ejecute el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="91e9d-113">Open an elevated PowerShell ISE session and run the following script:</span></span>

```powershell

# Set the module repository and the execution policy
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
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

# Download Azure Stack tools from GitHub and import the connect module
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

# Configure the cloud administrator’s PowerShell environment.
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

# Sign-in to the administrative portal.
Login-AzureRmAccount `
  -EnvironmentName "AzureStackAdmin" `
  -TenantId $TenantID 

```

## <a name="test-the-connectivity"></a><span data-ttu-id="91e9d-114">Prueba de la conectividad</span><span class="sxs-lookup"><span data-stu-id="91e9d-114">Test the connectivity</span></span>

<span data-ttu-id="91e9d-115">Ahora que ha configurado PowerShell, puede probar la configuración creando un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="91e9d-115">Now that you’ve configured PowerShell, you can test the configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

<span data-ttu-id="91e9d-116">Cuando se crea el grupo de recursos, la salida del cmdlet tiene la propiedad de estado de aprovisionamiento establecida en "Correcto".</span><span class="sxs-lookup"><span data-stu-id="91e9d-116">When the resource group is created, the cmdlet output has the Provisioning state property set to "Succeeded."</span></span>

## <a name="next-steps"></a><span data-ttu-id="91e9d-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91e9d-117">Next steps</span></span>

* [<span data-ttu-id="91e9d-118">Instalación y configuración de la CLI</span><span class="sxs-lookup"><span data-stu-id="91e9d-118">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="91e9d-119">Desarrollo de plantillas</span><span class="sxs-lookup"><span data-stu-id="91e9d-119">Develop templates</span></span>](azure-stack-develop-templates.md)







