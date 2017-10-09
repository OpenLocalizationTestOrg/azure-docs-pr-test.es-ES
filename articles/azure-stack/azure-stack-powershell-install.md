---
title: aaaInstall PowerShell para Azure pila | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall PowerShell para la pila de Azure."
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
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: 60995af2168348638e2513ab941a4125ca5c624a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="c340b-103">Instalación de PowerShell para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c340b-103">Install PowerShell for Azure Stack</span></span>  

<span data-ttu-id="c340b-104">Módulos de PowerShell de Azure compatibles de pila de Azure son necesario toowork con la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c340b-104">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="c340b-105">En esta guía, le guiaremos por hello pasos necesarios tooinstall PowerShell para la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c340b-105">In this guide, we walk you through hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="c340b-106">Puede usar los pasos de hello descritos en este artículo desde Hola Kit de desarrollo de pila de Azure, o desde un cliente externo basado en Windows, si está conectado a través de VPN.</span><span class="sxs-lookup"><span data-stu-id="c340b-106">You can use hello steps described in this article either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="c340b-107">En este artículo, se detallaron instrucciones tooinstall PowerShell para la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c340b-107">This article has detailed instructions tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="c340b-108">Sin embargo, si lo desea tooquickly instalación y configuración de PowerShell, puede usar script de Hola que se proporciona en hello [ponerse a trabajar con PowerShell](azure-stack-powershell-configure-quickstart.md) tema.</span><span class="sxs-lookup"><span data-stu-id="c340b-108">However, if you want tooquickly install and configure PowerShell, you can use hello script that is provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

> [!NOTE]
> <span data-ttu-id="c340b-109">Hola pasos requiere PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="c340b-109">hello following steps require PowerShell 5.0.</span></span> <span data-ttu-id="c340b-110">toocheck su versión, ejecución de comparación e $PSVersionTable.PSVersion Hola "Principal" versión.</span><span class="sxs-lookup"><span data-stu-id="c340b-110">toocheck your version, run $PSVersionTable.PSVersion and compare hello "Major" version.</span></span>

<span data-ttu-id="c340b-111">Comandos de PowerShell para Azure pila se instalan a través de la Galería de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="c340b-111">PowerShell commands for Azure Stack are installed through hello PowerShell gallery.</span></span> <span data-ttu-id="c340b-112">tooregiser Hola PSGallery repositorio, abra una sesión de PowerShell con privilegios elevados desde el kit de desarrollo de Hola o desde un cliente externo basado en Windows, si está conectado a través de VPN y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c340b-112">tooregiser hello PSGallery repository, open an elevated PowerShell session from hello development kit or from a Windows-based external client if you are connected through VPN and run hello following command:</span></span>

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a><span data-ttu-id="c340b-113">Desinstalación de las versiones existentes de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c340b-113">Uninstall existing versions of PowerShell</span></span>

<span data-ttu-id="c340b-114">Antes de instalar la versión requerida de hello, asegúrese de que los desinstale los módulos de PowerShell de Azure existentes.</span><span class="sxs-lookup"><span data-stu-id="c340b-114">Before installing hello required version, make sure that you uninstall any existing Azure PowerShell modules.</span></span> <span data-ttu-id="c340b-115">Puede desinstalarlos mediante uno de hello siguiendo dos métodos:</span><span class="sxs-lookup"><span data-stu-id="c340b-115">You can uninstall them by using one of hello following two methods:</span></span>

* <span data-ttu-id="c340b-116">toouninstall Hola módulos de PowerShell existentes, inicie sesión en el kit de desarrollo de toohello o basados en Windows toohello los clientes externos si tiene previsto tooestablish una conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="c340b-116">toouninstall hello existing PowerShell modules, sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="c340b-117">Cierre todas las sesiones activas de PowerShell de Hola y Hola ejecución siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c340b-117">Close all hello active PowerShell sessions and run hello following command:</span></span> 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* <span data-ttu-id="c340b-118">Inicie sesión en el kit de desarrollo de toohello o basados en Windows toohello los clientes externos si tiene previsto tooestablish una conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="c340b-118">Sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="c340b-119">Eliminar todas las carpetas de Hola que empiezan con "Azure" de hello `C:\Program Files (x86)\WindowsPowerShell\Modules` y `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` carpetas.</span><span class="sxs-lookup"><span data-stu-id="c340b-119">Delete all hello folders that start with "Azure" from hello `C:\Program Files (x86)\WindowsPowerShell\Modules` and `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` folders.</span></span> <span data-ttu-id="c340b-120">Al eliminar estas carpetas, quitan los módulos de PowerShell existentes de Hola "AzureStackAdmin" y ámbitos de usuario "global".</span><span class="sxs-lookup"><span data-stu-id="c340b-120">Deleting these folders removes any existing PowerShell modules from hello "AzureStackAdmin" and "global" user scopes.</span></span> 

<span data-ttu-id="c340b-121">Hello siguientes secciones describen Hola pasos necesarios tooinstall PowerShell para la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="c340b-121">hello following sections describe hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="c340b-122">PowerShell puede instalarse en Azure Stack que opere en un escenario conectado, parcialmente conectado o sin conexión.</span><span class="sxs-lookup"><span data-stu-id="c340b-122">PowerShell can be installed on Azure Stack that is operated in connected, partially connected, or in a disconnected scenario.</span></span> 

## <a name="install-powershell-in-a-connected-scenario"></a><span data-ttu-id="c340b-123">Instalación de PowerShell en un escenario conectado</span><span class="sxs-lookup"><span data-stu-id="c340b-123">Install PowerShell in a connected scenario</span></span> 

<span data-ttu-id="c340b-124">Los módulos AzureRM compatibles con Azure Stack se instalan a través de perfiles de la versión de API.</span><span class="sxs-lookup"><span data-stu-id="c340b-124">Azure Stack compatible AzureRM modules are installed through API version profiles.</span></span> <span data-ttu-id="c340b-125">Pila de Azure requiere hello **2017-03-09-perfil** perfil de versión de API, que está disponible mediante la instalación de módulo de AzureRM.Bootstrapper Hola.</span><span class="sxs-lookup"><span data-stu-id="c340b-125">Azure Stack requires hello **2017-03-09-profile** API version profile, which is available by installing hello AzureRM.Bootstrapper module.</span></span> <span data-ttu-id="c340b-126">toolearn sobre perfiles de la versión de API y cmdlets de hello proporcionada por ellos, consulte toohello [administrar perfiles de la versión de API](azure-stack-version-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="c340b-126">toolearn about API version profiles and hello cmdlets provided by them, refer toohello [manage API version profiles](azure-stack-version-profiles.md).</span></span> <span data-ttu-id="c340b-127">En los módulos de suma toohello AzureRM, también debe instalar los módulos de PowerShell de Azure específica de la pila de Hola.</span><span class="sxs-lookup"><span data-stu-id="c340b-127">In addition toohello AzureRM modules, you should also install hello Azure Stack-specific PowerShell modules.</span></span> <span data-ttu-id="c340b-128">Ejecute hello después tooinstall de secuencia de comandos de PowerShell estos módulos en la estación de trabajo de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="c340b-128">Run hello following PowerShell script tooinstall these modules on your development workstation:</span></span>

  ```powershell
  # Install hello AzureRM.Bootstrapper module. Select Yes when prompted tooinstall NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import hello API Version Profile required by Azure Stack into hello current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.10
  ```

<span data-ttu-id="c340b-129">instalación de hello tooconfirm, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c340b-129">tooconfirm hello installation, run hello following command:</span></span>

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  <span data-ttu-id="c340b-130">Si se realiza correctamente la instalación de hello, hello AzureRM y AzureStack módulos se muestran en la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="c340b-130">If hello installation is successful, hello AzureRM and AzureStack modules are displayed in hello output.</span></span>

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a><span data-ttu-id="c340b-131">Instalación de PowerShell en un escenario sin conexión o parcialmente conectado</span><span class="sxs-lookup"><span data-stu-id="c340b-131">Install PowerShell in a disconnected or in a partially connected scenario</span></span>

<span data-ttu-id="c340b-132">En una situación sin conexión, debe descargar primero máquina tooa de módulos de PowerShell de Hola que tenga conectividad a internet y, a continuación, transferirlos toohello Kit de desarrollo de pila de Azure para la instalación.</span><span class="sxs-lookup"><span data-stu-id="c340b-132">In a disconnected scenario, you must first download hello PowerShell modules tooa machine that has internet connectivity, and then transfer them toohello Azure Stack Development Kit for installation.</span></span>

1. <span data-ttu-id="c340b-133">Inicie sesión en el equipo de tooa donde tiene conectividad a internet y usar hello después hello de la secuencia de comandos toodownload AzureRM y AzureStack paquetes en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="c340b-133">Sign in tooa computer where you have internet connectivity and use hello following script toodownload hello AzureRM, and AzureStack packages onto your local computer:</span></span>

   ```powershell
   $Path = "<Path that is used toosave hello packages>"

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureRM `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureStack `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10 
   ```

2. <span data-ttu-id="c340b-134">Hola copia los paquetes descargados en el dispositivo USB de tooa.</span><span class="sxs-lookup"><span data-stu-id="c340b-134">Copy hello downloaded packages over tooa USB device.</span></span>

3. <span data-ttu-id="c340b-135">Inicie sesión en el kit de desarrollo de toohello y copiar paquetes de saludo de ubicación del tooa Hola para dispositivo USB en el kit de desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c340b-135">Sign in toohello development kit and copy hello packages from hello USB device tooa location on hello development kit.</span></span> 

4. <span data-ttu-id="c340b-136">Ahora debe registrar esta ubicación como repositorio de hello predeterminado e instalar hello AzureRM y AzureStack módulos desde este repositorio:</span><span class="sxs-lookup"><span data-stu-id="c340b-136">Now you must register this location as hello default repository and install hello AzureRM and AzureStack modules from this repository:</span></span>

   ```powershell
   $SourceLocation = "<Location on hello development kit that contains hello PowerShell packages>"
   $RepoName = "MyNuGetSource"

   Register-PSRepository `
     -Name $RepoName `
     -SourceLocation $SourceLocation `
     -InstallationPolicy Trusted

   ```powershell
   Install-Module AzureRM `
     -Repository $RepoName

   Install-Module AzureStack `
     -Repository $RepoName 
   ```

## <a name="next-steps"></a><span data-ttu-id="c340b-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c340b-137">Next steps</span></span>

* [<span data-ttu-id="c340b-138">Descarga de herramientas de Azure Stack desde GitHub</span><span class="sxs-lookup"><span data-stu-id="c340b-138">Download Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)
* [<span data-ttu-id="c340b-139">Configurar el entorno de PowerShell del usuario de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="c340b-139">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
* [<span data-ttu-id="c340b-140">Configurar el entorno de PowerShell del operador de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="c340b-140">Configure hello Azure Stack operator's PowerShell environment</span></span>](azure-stack-powershell-configure-admin.md) 
* [<span data-ttu-id="c340b-141">Administración de perfiles de la versión de API en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c340b-141">Manage API version profiles in Azure Stack</span></span>](azure-stack-version-profiles.md)  
