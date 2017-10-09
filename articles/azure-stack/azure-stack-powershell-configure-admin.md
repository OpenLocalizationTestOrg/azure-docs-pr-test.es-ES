---
title: entorno de PowerShell del operador de aaaConfigure Hola pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooConfigure Hola entorno de PowerShell del operador de la pila de Azure."
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
ms.openlocfilehash: 1a1e95b95598062f155126b9560934bba4994f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-azure-stack-operators-powershell-environment"></a>Configurar el entorno de PowerShell del operador de hello pila de Azure

Como operador de Azure Stack, puede configurar el entorno de PowerShell en Azure Stack Development Kit. Después de configurar, puede usar recursos de pila de Azure PowerShell toomanage como la creación de ofertas, planes, las cuotas, administrar alertas, etcetera. Este tema es toouse ámbito con el operador de nube Hola entornos únicamente, si desea tooset PowerShell para el entorno de usuario de hello, consultar demasiado[configurar el entorno de PowerShell del usuario de hello Azure pila](azure-stack-powershell-configure-user.md) tema. 

## <a name="prerequisites"></a>Requisitos previos

Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn): 

* Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).  
* Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).  

## <a name="configure-hello-operator-environment-and-sign-in-tooazure-stack"></a>Configurar el entorno de operador de hello e inicie sesión en tooAzure pila

Se basa en el tipo de saludo de implementación (Azure AD o AD FS), ejecute uno de hello siguiendo el entorno de operador de secuencias de comandos tooconfigure Hola pila de Azure con PowerShell:

### <a name="azure-active-directory-aad-based-deployments"></a>Implementaciones basadas en Azure Active Directory (AAD)
       
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackAdmin"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
  ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>Implementaciones basadas en Servicios de federación de Active Directory (AD FS)
         
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackAdmin"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
  ```

## <a name="test-hello-connectivity"></a>Probar la conectividad de Hola

Ahora que todo lo configure tenemos, vamos a usar PowerShell toocreate recursos dentro de la pila de Azure. Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual. Hola use después el comando toocreate un grupo de recursos denominado "MyResourceGroup":

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Pasos siguientes
* [Desarrollo de plantillas para Azure Stack](azure-stack-develop-templates.md)
* [Implementación de plantillas con PowerShell](azure-stack-deploy-template-powershell.md)