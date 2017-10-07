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
# <a name="configure-hello-azure-stack-users-powershell-environment"></a><span data-ttu-id="df7e6-103">Configurar el entorno de PowerShell del usuario de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="df7e6-103">Configure hello Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="df7e6-104">Como usuario de Azure Stack, puede configurar el entorno de PowerShell en Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="df7e6-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="df7e6-105">Después de configurar, puede usar PowerShell recursos de Azure pila toomanage como suscribirse toooffers, crear máquinas virtuales, implementar plantillas del Administrador de recursos de Azure, etcetera. Este tema es toouse ámbito con solo los entornos de usuario hello, si desea tooset PowerShell para entorno de operador de hello en la nube, consulte toohello [configurar el entorno de PowerShell del operador de hello Azure pila](azure-stack-powershell-configure-admin.md) tema.</span><span class="sxs-lookup"><span data-stu-id="df7e6-105">After you configure, you can use PowerShell toomanage Azure Stack resources such as subscribe toooffers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped toouse with hello user environments only, if you want tooset up PowerShell for hello cloud operator environment, refer toohello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="df7e6-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="df7e6-106">Prerequisites</span></span> 

<span data-ttu-id="df7e6-107">Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="df7e6-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="df7e6-108">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="df7e6-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="df7e6-109">Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="df7e6-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a><span data-ttu-id="df7e6-110">Configurar el entorno de usuario de hello e inicie sesión en tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="df7e6-110">Configure hello user environment and sign in tooAzure Stack</span></span>

<span data-ttu-id="df7e6-111">Según el tipo de saludo de implementación (Azure AD o AD FS), ejecute uno de hello siga tooconfigure script PowerShell para la pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="df7e6-111">Based on hello type of deployment (Azure AD or AD FS), run one of hello following script tooconfigure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="df7e6-112">Implementaciones basadas en Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="df7e6-112">Azure Active Directory (AAD) based deployments</span></span>
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="df7e6-113">Implementaciones basadas en Servicios de federación de Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="df7e6-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
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

## <a name="register-resource-providers"></a><span data-ttu-id="df7e6-114">Registro de proveedores de recursos</span><span class="sxs-lookup"><span data-stu-id="df7e6-114">Register resource providers</span></span>

<span data-ttu-id="df7e6-115">Cuando se trabaja en una suscripción de usuario recién creado que no tiene los recursos que se implementan a través del portal de hello, proveedores de recursos de hello no se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="df7e6-115">When operating on a newly created user subscription that doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="df7e6-116">Se debe registrar explícitamente mediante el uso de hello siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="df7e6-116">You should explicitly register them by using hello following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a><span data-ttu-id="df7e6-117">Probar la conectividad de Hola</span><span class="sxs-lookup"><span data-stu-id="df7e6-117">Test hello connectivity</span></span>

<span data-ttu-id="df7e6-118">Ahora que todo lo configure tenemos, vamos a usar PowerShell toocreate recursos dentro de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="df7e6-118">Now that we've got everything set up, let's use PowerShell toocreate resources within Azure Stack.</span></span> <span data-ttu-id="df7e6-119">Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="df7e6-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="df7e6-120">Hola use después el comando toocreate un grupo de recursos denominado "MyResourceGroup":</span><span class="sxs-lookup"><span data-stu-id="df7e6-120">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="df7e6-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df7e6-121">Next steps</span></span>
* [<span data-ttu-id="df7e6-122">Desarrollo de plantillas para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="df7e6-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="df7e6-123">Implementación de plantillas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="df7e6-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
