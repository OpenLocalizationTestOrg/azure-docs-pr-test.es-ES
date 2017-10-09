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
# <a name="configure-hello-azure-stack-operators-powershell-environment"></a><span data-ttu-id="81d8b-103">Configurar el entorno de PowerShell del operador de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="81d8b-103">Configure hello Azure Stack operator's PowerShell environment</span></span>

<span data-ttu-id="81d8b-104">Como operador de Azure Stack, puede configurar el entorno de PowerShell en Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="81d8b-104">As an Azure Stack operator, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="81d8b-105">Después de configurar, puede usar recursos de pila de Azure PowerShell toomanage como la creación de ofertas, planes, las cuotas, administrar alertas, etcetera. Este tema es toouse ámbito con el operador de nube Hola entornos únicamente, si desea tooset PowerShell para el entorno de usuario de hello, consultar demasiado[configurar el entorno de PowerShell del usuario de hello Azure pila](azure-stack-powershell-configure-user.md) tema.</span><span class="sxs-lookup"><span data-stu-id="81d8b-105">After you configure, you can use PowerShell toomanage Azure Stack resources such as creating offers, plans, quotas, managing alerts, etc. This topic is scoped toouse with hello cloud operator environments only, if you want tooset up PowerShell for hello user environment, refer too[Configure hello Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="81d8b-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="81d8b-106">Prerequisites</span></span>

<span data-ttu-id="81d8b-107">Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="81d8b-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span> 

* <span data-ttu-id="81d8b-108">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="81d8b-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="81d8b-109">Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="81d8b-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="configure-hello-operator-environment-and-sign-in-tooazure-stack"></a><span data-ttu-id="81d8b-110">Configurar el entorno de operador de hello e inicie sesión en tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="81d8b-110">Configure hello operator environment and sign in tooAzure Stack</span></span>

<span data-ttu-id="81d8b-111">Se basa en el tipo de saludo de implementación (Azure AD o AD FS), ejecute uno de hello siguiendo el entorno de operador de secuencias de comandos tooconfigure Hola pila de Azure con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="81d8b-111">Based on hello type of deployment (Azure AD or AD FS), run one of hello following script tooconfigure hello Azure Stack operator environment with PowerShell:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="81d8b-112">Implementaciones basadas en Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="81d8b-112">Azure Active Directory (AAD) based deployments</span></span>
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="81d8b-113">Implementaciones basadas en Servicios de federación de Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="81d8b-113">Active Directory Federation Services (AD FS) based deployments</span></span>
         
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

## <a name="test-hello-connectivity"></a><span data-ttu-id="81d8b-114">Probar la conectividad de Hola</span><span class="sxs-lookup"><span data-stu-id="81d8b-114">Test hello connectivity</span></span>

<span data-ttu-id="81d8b-115">Ahora que todo lo configure tenemos, vamos a usar PowerShell toocreate recursos dentro de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="81d8b-115">Now that we've got everything set up, let's use PowerShell toocreate resources within Azure Stack.</span></span> <span data-ttu-id="81d8b-116">Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="81d8b-116">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="81d8b-117">Hola use después el comando toocreate un grupo de recursos denominado "MyResourceGroup":</span><span class="sxs-lookup"><span data-stu-id="81d8b-117">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="81d8b-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81d8b-118">Next steps</span></span>
* [<span data-ttu-id="81d8b-119">Desarrollo de plantillas para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="81d8b-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="81d8b-120">Implementación de plantillas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="81d8b-120">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)