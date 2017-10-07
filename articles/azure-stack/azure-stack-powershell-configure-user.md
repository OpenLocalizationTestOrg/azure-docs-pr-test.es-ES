---
title: entorno de PowerShell del usuario de aaaConfigure Hola pila de Azure | Documentos de Microsoft
description: Configurar el entorno de PowerShell del usuario de hello pila de Azure
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
ms.openlocfilehash: 8e7ccea24a1917d349ab06e0abe29f534b47b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-azure-stack-users-powershell-environment"></a>Configurar el entorno de PowerShell del usuario de hello pila de Azure

Como usuario de Azure Stack, puede configurar el entorno de PowerShell en Azure Stack Development Kit. Después de configurar, puede usar PowerShell recursos de Azure pila toomanage como suscribirse toooffers, crear máquinas virtuales, implementar plantillas del Administrador de recursos de Azure, etcetera. Este tema es toouse ámbito con solo los entornos de usuario hello, si desea tooset PowerShell para entorno de operador de hello en la nube, consulte toohello [configurar el entorno de PowerShell del operador de hello Azure pila](azure-stack-powershell-configure-admin.md) tema. 

## <a name="prerequisites"></a>Requisitos previos 

Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).  
* Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md). 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a>Configurar el entorno de usuario de hello e inicie sesión en tooAzure pila

Según el tipo de saludo de implementación (Azure AD o AD FS), ejecute uno de hello siga tooconfigure script PowerShell para la pila de Azure:

### <a name="azure-active-directory-aad-based-deployments"></a>Implementaciones basadas en Azure Active Directory (AAD)
       
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>Implementaciones basadas en Servicios de federación de Active Directory (AD FS) 
          
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a>Registro de proveedores de recursos

Cuando se trabaja en una suscripción de usuario recién creado que no tiene los recursos que se implementan a través del portal de hello, proveedores de recursos de hello no se registran automáticamente. Se debe registrar explícitamente mediante el uso de hello siguiente secuencia de comandos:

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a>Probar la conectividad de Hola

Ahora que todo lo configure tenemos, vamos a usar PowerShell toocreate recursos dentro de la pila de Azure. Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual. Hola use después el comando toocreate un grupo de recursos denominado "MyResourceGroup":

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Pasos siguientes
* [Desarrollo de plantillas para Azure Stack](azure-stack-develop-templates.md)
* [Implementación de plantillas con PowerShell](azure-stack-deploy-template-powershell.md)
