---
title: "Configuración del entorno de PowerShell del usuario de Azure Stack | Microsoft Docs"
description: "Configuración del entorno de PowerShell del usuario de Azure Stack"
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
ms.openlocfilehash: dabbd83fb35397f2cf90fac5957d299f0c5d446e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-the-azure-stack-users-powershell-environment"></a><span data-ttu-id="29fab-103">Configuración del entorno de PowerShell del usuario de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="29fab-103">Configure the Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="29fab-104">Como usuario de Azure Stack, puede configurar el entorno de PowerShell en Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="29fab-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="29fab-105">Tras la configuración, puede usar PowerShell para administrar los recursos de Azure Stack como la suscripción a ofertas, la creación de máquinas virtuales, la implementación de plantillas de Azure Resource Manager, etcétera. Este tema está pensado para delimitarse únicamente a entornos de usuario, si desea configurar PowerShell para el entorno de operadores en la nube, consulte el tema [Configuración del entorno de PowerShell del operador de Azure Stack](azure-stack-powershell-configure-admin.md).</span><span class="sxs-lookup"><span data-stu-id="29fab-105">After you configure, you can use PowerShell to manage Azure Stack resources such as subscribe to offers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped to use with the user environments only, if you want to set up PowerShell for the cloud operator environment, refer to the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="29fab-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29fab-106">Prerequisites</span></span> 

<span data-ttu-id="29fab-107">Implemente los siguientes requisitos previos desde el [kit de desarrollo](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) o desde un cliente externo basado en Windows, si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="29fab-107">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="29fab-108">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="29fab-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="29fab-109">Descargue las [herramientas necesarias para trabajar con Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="29fab-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-the-user-environment-and-sign-in-to-azure-stack"></a><span data-ttu-id="29fab-110">Configuración del entorno de usuario e inicio de sesión en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="29fab-110">Configure the user environment and sign in to Azure Stack</span></span>

<span data-ttu-id="29fab-111">Según el tipo de implementación (Azure AD o AD FS), ejecute uno de los scripts siguientes a fin de configurar PowerShell para Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="29fab-111">Based on the type of deployment (Azure AD or AD FS), run one of the following script to configure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="29fab-112">Implementaciones basadas en Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="29fab-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get the Active Directory tenantId that is used to deploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="29fab-113">Implementaciones basadas en Servicios de federación de Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="29fab-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get the Active Directory tenantId that is used to deploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="29fab-114">Registro de proveedores de recursos</span><span class="sxs-lookup"><span data-stu-id="29fab-114">Register resource providers</span></span>

<span data-ttu-id="29fab-115">Cuando se trabaja en una suscripción de usuario recién creada que no tiene recursos implementados a través del portal, los proveedores de recursos no se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="29fab-115">When operating on a newly created user subscription that doesn’t have any resources deployed through the portal, the resource providers aren't automatically registered.</span></span> <span data-ttu-id="29fab-116">Se deben registrar de modo explícito mediante el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="29fab-116">You should explicitly register them by using the following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-the-connectivity"></a><span data-ttu-id="29fab-117">Prueba de la conectividad</span><span class="sxs-lookup"><span data-stu-id="29fab-117">Test the connectivity</span></span>

<span data-ttu-id="29fab-118">Ahora que todo está configurado, vamos a usar PowerShell para crear recursos en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="29fab-118">Now that we've got everything set up, let's use PowerShell to create resources within Azure Stack.</span></span> <span data-ttu-id="29fab-119">Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="29fab-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="29fab-120">Use el comando siguiente para crear un grupo de recursos denominado "MyResourceGroup":</span><span class="sxs-lookup"><span data-stu-id="29fab-120">Use the following command to create a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="29fab-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29fab-121">Next steps</span></span>
* [<span data-ttu-id="29fab-122">Desarrollo de plantillas para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="29fab-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="29fab-123">Implementación de plantillas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="29fab-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
