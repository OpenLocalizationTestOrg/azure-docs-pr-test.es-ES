---
title: aaaConfigure PowerShell para su uso con la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure PowerShell para la pila de Azure."
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
ms.date: 07/16/2017
ms.author: sngun
ms.openlocfilehash: bc40869abe453cef4854daaf11605efd94a66c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a><span data-ttu-id="bb9af-103">Configurar PowerShell para su uso con la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="bb9af-103">Configure PowerShell for use with Azure Stack</span></span> 

<span data-ttu-id="bb9af-104">Este artículo describe instancia de hello pasos necesarios tooconnect tooan Kit de desarrollo de pila de Azure mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb9af-104">This article describes hello steps required tooconnect tooan Azure Stack Development Kit instance by using PowerShell.</span></span> <span data-ttu-id="bb9af-105">Después de conectarse, puede tener acceso a portal de hello e implementar recursos a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb9af-105">After you connect, you can access hello portal and deploy resources through PowerShell.</span></span> <span data-ttu-id="bb9af-106">Puede usar los pasos de hello descritos en este artículo del kit de desarrollo de hello, o desde un cliente externo basado en Windows, si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="bb9af-106">You can use hello steps described in this article either from hello development kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="bb9af-107">En este artículo, se detallaron instrucciones tooconfigure PowerShell para la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9af-107">This article has detailed instructions tooconfigure PowerShell for Azure Stack.</span></span> <span data-ttu-id="bb9af-108">Sin embargo, si lo desea tooquickly instalación y configuración de PowerShell, puede usar script de Hola proporcionado en hello [ponerse a trabajar con PowerShell](azure-stack-powershell-configure-quickstart.md) tema.</span><span class="sxs-lookup"><span data-stu-id="bb9af-108">However, if you want tooquickly install and configure PowerShell, you can use hello script provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bb9af-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bb9af-109">Prerequisites</span></span>
* <span data-ttu-id="bb9af-110">Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="bb9af-110">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="bb9af-111">Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="bb9af-111">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="import-hello-connect-powershell-module"></a><span data-ttu-id="bb9af-112">Módulo de importación Hola Connect PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb9af-112">Import hello Connect PowerShell module</span></span>

<span data-ttu-id="bb9af-113">Después de descargar Hola requiere herramientas, desplazarse por las carpetas de toohello descargar e importar hello **conectar** módulo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb9af-113">After you download hello required tools, navigate toohello downloaded folder and import hello **Connect** PowerShell module.</span></span> <span data-ttu-id="bb9af-114">módulo tooimport Hola Connect, ejecute el siguiente comando en una sesión de PowerShell con privilegios elevados de hello:</span><span class="sxs-lookup"><span data-stu-id="bb9af-114">tooimport hello Connect module, run hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a><span data-ttu-id="bb9af-115">Configurar el entorno de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="bb9af-115">Configure hello PowerShell environment</span></span>

<span data-ttu-id="bb9af-116">tooconfigure el entorno de la pila de Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="bb9af-116">tooconfigure your Azure Stack environment, do hello following:</span></span>

1. <span data-ttu-id="bb9af-117">Registrar un entorno de AzureRM destinado a la instancia de la pila de Azure mediante uno de los siguientes cmdlets de hello:</span><span class="sxs-lookup"><span data-stu-id="bb9af-117">Register an AzureRM environment that targets your Azure Stack instance by using one of hello following cmdlets:</span></span>

   * <span data-ttu-id="bb9af-118">**Entorno administrativo en la nube**</span><span class="sxs-lookup"><span data-stu-id="bb9af-118">**Cloud administrative environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * <span data-ttu-id="bb9af-119">**Entorno de usuario**</span><span class="sxs-lookup"><span data-stu-id="bb9af-119">**User environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   <span data-ttu-id="bb9af-120">Después de que ha registrado el entorno de AzureRM hello, puede usar todos los cmdlets de AzureRM hello en su entorno de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9af-120">After you've registered hello AzureRM environment, you can use all hello AzureRM cmdlets in your Azure Stack environment.</span></span> <span data-ttu-id="bb9af-121">se muestra el resultado de Hello del cmdlet anterior Hola Hola siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="bb9af-121">hello output of hello previous cmdlet is shown in hello following screenshot:</span></span>

   ![Obtener detalles del entorno](media/azure-stack-powershell-configure/getenvdetails.png)

2. <span data-ttu-id="bb9af-123">Establezca el valor de GraphEndpointResourceId de hello mediante uno de los siguientes cmdlets de hello:</span><span class="sxs-lookup"><span data-stu-id="bb9af-123">Set hello GraphEndpointResourceId value by using one of hello following cmdlets:</span></span>
   
   * <span data-ttu-id="bb9af-124">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="bb9af-124">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="bb9af-125">Para hello **entorno administrativo en la nube**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-125">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * <span data-ttu-id="bb9af-126">Para hello **entorno del usuario**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-126">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * <span data-ttu-id="bb9af-127">**Servicios de federación de Active Directory**</span><span class="sxs-lookup"><span data-stu-id="bb9af-127">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="bb9af-128">Para hello **entorno administrativo en la nube**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-128">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * <span data-ttu-id="bb9af-129">Para hello **entorno del usuario**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-129">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. <span data-ttu-id="bb9af-130">Obtener valor GUID de Hola Hola inquilino de Active Directory que es usado toodeploy pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9af-130">Get hello GUID value of hello Active Directory tenant that is used toodeploy Azure Stack.</span></span> <span data-ttu-id="bb9af-131">Si su entorno de pila de Azure se implementa mediante el uso de:</span><span class="sxs-lookup"><span data-stu-id="bb9af-131">If your Azure Stack environment is deployed by using:</span></span>  

   * <span data-ttu-id="bb9af-132">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="bb9af-132">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="bb9af-133">Hola tooaccess **entorno administrativo en la nube**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-133">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="bb9af-134">Hola tooaccess **entorno del usuario**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-134">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * <span data-ttu-id="bb9af-135">**Servicios de federación de Active Directory**</span><span class="sxs-lookup"><span data-stu-id="bb9af-135">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="bb9af-136">Hola tooaccess **entorno administrativo en la nube**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-136">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="bb9af-137">Hola tooaccess **entorno del usuario**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-137">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a><span data-ttu-id="bb9af-138">Inicie sesión en tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="bb9af-138">Sign in tooAzure Stack</span></span>

<span data-ttu-id="bb9af-139">Inicie sesión en toohello entorno de pila de Azure mediante uno de hello después de dos cmdlets:</span><span class="sxs-lookup"><span data-stu-id="bb9af-139">Sign in toohello Azure Stack environment by using one of hello following two cmdlets:</span></span>

   * <span data-ttu-id="bb9af-140">toosign en toohello **portal administrativa**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-140">toosign in toohello **administrative portal**, use:</span></span>
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * <span data-ttu-id="bb9af-141">toosign en toohello **portal de usuarios**, use:</span><span class="sxs-lookup"><span data-stu-id="bb9af-141">toosign in toohello **user portal**, use:</span></span>

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a><span data-ttu-id="bb9af-142">Registro de proveedores de recursos</span><span class="sxs-lookup"><span data-stu-id="bb9af-142">Register resource providers</span></span>

<span data-ttu-id="bb9af-143">Después de iniciar sesión en el portal de administrador o usuario toohello, puede emitir las operaciones en proveedores de recursos de hello registrado.</span><span class="sxs-lookup"><span data-stu-id="bb9af-143">After you sign in toohello administrator or user portal, you can issue operations against hello registered resource providers.</span></span> <span data-ttu-id="bb9af-144">De forma predeterminada, se registran todos los proveedores de recursos fundamentales de hello en Hola suscripción predeterminada de proveedor (suscripción del Administrador de la nube de Hola).</span><span class="sxs-lookup"><span data-stu-id="bb9af-144">By default, all hello foundational resource providers are registered in hello Default Provider Subscription (hello cloud administrator's subscription).</span></span>

<span data-ttu-id="bb9af-145">Cuando trabaje en una suscripción de usuario recién creado, que no tiene los recursos que se implementan a través del portal de hello, proveedores de recursos de hello no se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bb9af-145">When you operate on a newly created user subscription, which doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="bb9af-146">Explícitamente, debe registrar proveedores de recursos de Hola mediante Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="bb9af-146">You should explicitly register hello resource providers by using hello following script:</span></span>

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a><span data-ttu-id="bb9af-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb9af-147">Next steps</span></span>
* [<span data-ttu-id="bb9af-148">Desarrollo de plantillas para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bb9af-148">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="bb9af-149">Implementación de plantillas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb9af-149">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
