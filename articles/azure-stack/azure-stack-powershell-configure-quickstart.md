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
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a>Póngase a trabajar con PowerShell en Azure Stack

Este artículo es un tooinstall de inicio rápido y configurar el entorno de la pila de Azure con PowerShell. Este script proporcionado en este artículo es hello de ámbito tooby **operador Azure pila** solo.

En este artículo es una versión comprimida de los pasos de hello descrito en hello [instale PowerShell]( azure-stack-powershell-install.md), [descargar herramientas]( azure-stack-powershell-download.md), [configurar el entorno de PowerShell del operador de hello Azure pila]( azure-stack-powershell-configure-admin.md) artículos. Mediante el uso de secuencias de comandos de hello en este tema, puede configurar PowerShell para entornos de pila de Azure que se implementan con Azure Active Directory o los servicios de federación de Active Directory.  


## <a name="set-up-powershell-for-aad-based-deployments"></a>Configuración de PowerShell para las implementaciones basadas en AAD

Inicie sesión en tooyour Kit de desarrollo de pila de Azure, o un cliente externo basado en Windows si está conectado a través de VPN. Abra una sesión de PowerShell ISE con privilegios elevados y ejecute hello siguiente secuencia de comandos:

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

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a>Configuración de PowerShell para las implementaciones basadas en AD FS 

Inicie sesión en tooyour Kit de desarrollo de pila de Azure, o un cliente externo basado en Windows si está conectado a través de VPN. Abra una sesión de PowerShell ISE con privilegios elevados y ejecute hello siguiente secuencia de comandos:

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

## <a name="test-hello-connectivity"></a>Probar la conectividad de Hola

Ahora que ha configurado PowerShell, puede probar configuración de hello mediante la creación de un grupo de recursos:

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

Cuando se crea el grupo de recursos de hello, salida del cmdlet hello tiene la propiedad de estado de aprovisionamiento de hello establecida demasiado "correcta".

## <a name="next-steps"></a>Pasos siguientes

* [Instalación y configuración de la CLI](azure-stack-connect-cli.md)

* [Desarrollo de plantillas](azure-stack-develop-templates.md)







