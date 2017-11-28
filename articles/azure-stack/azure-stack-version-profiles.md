---
title: "perfiles de la versión de aaaUsing API en la pila de Azure | Documentos de Microsoft"
description: "Aprenda los perfiles de la versión de API en Azure Stack."
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
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: cb54a683054f08fd123bcb6245d88aaa30c29882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a><span data-ttu-id="fd4ec-103">Administre los perfiles de la versión de API en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fd4ec-103">Manage API version profiles in Azure Stack</span></span>

<span data-ttu-id="fd4ec-104">Perfiles de la versión de API proporcionan una manera toomanage diferencias de versión entre Azure y la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-104">API version profiles provide a way toomanage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="fd4ec-105">Un perfil de la versión de la API es un conjunto de módulos de PowerShell AzureRM con versiones específicas de la API.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="fd4ec-106">Cada plataforma de la nube tiene un conjunto de perfiles de versión de API compatibles.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-106">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="fd4ec-107">Por ejemplo, pila de Azure es compatible con una versión de perfil con fecha específico como **2017-03-09-perfil**, Azure es compatible con hello y **más reciente** perfil de la versión de API.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports hello **latest** API version profile.</span></span> <span data-ttu-id="fd4ec-108">Cuando se instala un perfil, hello módulos AzureRM PowerShell correspondientes toohello especificadas perfil están instaladas.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-108">When you install a profile, hello AzureRM PowerShell modules that correspond toohello specified profile are installed.</span></span>

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a><span data-ttu-id="fd4ec-109">Instalar perfiles de la versión de Hola PowerShell los módulos necesarios toouse API</span><span class="sxs-lookup"><span data-stu-id="fd4ec-109">Install hello PowerShell module required toouse API version profiles</span></span>

<span data-ttu-id="fd4ec-110">Hola **AzureRM.Bootstrapper** módulo que está disponible a través de hello Galería de PowerShell proporciona cmdlets de PowerShell que son necesario toowork con perfiles de la versión de API.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-110">hello **AzureRM.Bootstrapper** module that is available through hello PowerShell Gallery provides PowerShell cmdlets that are required toowork with API version profiles.</span></span> <span data-ttu-id="fd4ec-111">Usar hello después de módulo de cmdlets tooinstall Hola AzureRM.Bootstrapper:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-111">Use hello following cmdlet tooinstall hello AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
<span data-ttu-id="fd4ec-112">módulo de Hello AzureRM.Bootstrapper está en vista previa; detalles y las funcionalidades están toochange de asunto.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-112">hello AzureRM.Bootstrapper module is in preview; details and functionality are subject toochange.</span></span> <span data-ttu-id="fd4ec-113">toodownload e instalar Hola versión más reciente de este módulo de hello Galería de PowerShell, ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-113">toodownload and install hello latest version of this module from hello PowerShell Gallery, run hello following cmdlet:</span></span>

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a><span data-ttu-id="fd4ec-114">Instalar un perfil</span><span class="sxs-lookup"><span data-stu-id="fd4ec-114">Install a profile</span></span>

<span data-ttu-id="fd4ec-115">Hola de uso **Install-AzureRmProfile** cmdlet con hello **2017-03-09-perfil** API versión perfil tooinstall hello AzureRM módulos requeridos por la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-115">Use hello **Install-AzureRmProfile** cmdlet with hello **2017-03-09-profile** API version profile tooinstall hello AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="fd4ec-116">Tenga en cuenta que no se instalan módulos de administrador de hello pila de Azure en la nube con este perfil de la versión de API, y deben instalarse por separado según lo especificado en hello paso 3 de hello [instale PowerShell para Azure pila](azure-stack-powershell-install.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-116">Note that hello Azure Stack cloud administrator modules are not installed with this API version profile, and they should be installed separately as specified in hello Step 3 of hello [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="fd4ec-117">Instalar e importar módulos en un perfil</span><span class="sxs-lookup"><span data-stu-id="fd4ec-117">Install and import modules in a profile</span></span>

<span data-ttu-id="fd4ec-118">Hola de uso **AzureRmProfile Use** módulos tooinstall e importación de cmdlets que están asociados a un perfil de la versión de API.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-118">Use hello **Use-AzureRmProfile** cmdlet tooinstall and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="fd4ec-119">Puede importar un solo perfil de la versión de la API en una sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="fd4ec-120">perfil de la versión de tooimport una API diferente, debe abrir una nueva sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-120">tooimport a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="fd4ec-121">Hola siguiente las tareas ejecuta el cmdlet de Hello AzureRMProfile de uso:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-121">hello Use-AzureRMProfile cmdlet runs hello following tasks:</span></span>  
1. <span data-ttu-id="fd4ec-122">Comprueba si el perfil de versión de API especificado de módulos de PowerShell de hello asociados con hello se instala en el ámbito actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-122">Checks if hello PowerShell modules associated with hello specified API version profile are installed in hello current scope.</span></span>  
2. <span data-ttu-id="fd4ec-123">Descarga e instala los módulos de hello si ya no están instalados.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-123">Downloads and installs hello modules if they are not already installed.</span></span>   
3. <span data-ttu-id="fd4ec-124">Importaciones Hola módulos en la sesión actual de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-124">Imports hello modules into hello current PowerShell session.</span></span> 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="fd4ec-125">tooinstall e importación seleccionan AzureRM módulos de un perfil de versión de API, ejecute el cmdlet hello AzureRMProfile de uso con hello **módulo** parámetro:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-125">tooinstall and import selected AzureRM modules from an API version profile, run hello Use-AzureRMProfile cmdlet with hello **Module** parameter:</span></span>

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a><span data-ttu-id="fd4ec-126">Obtener perfiles Hola instalado</span><span class="sxs-lookup"><span data-stu-id="fd4ec-126">Get hello installed profiles</span></span>

<span data-ttu-id="fd4ec-127">Hola de uso **AzureRmProfile Get** lista de cmdlets tooget Hola de perfiles de versión de API disponibles:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-127">Use hello **Get-AzureRmProfile** cmdlet tooget hello list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="fd4ec-128">Administrar perfiles</span><span class="sxs-lookup"><span data-stu-id="fd4ec-128">Update profiles</span></span>

<span data-ttu-id="fd4ec-129">Hola de uso **AzureRmProfile actualización** módulos de cmdlet tooupdate hello en una versión perfil toohello última versión de API de módulos que están disponibles en Hola PSGallery.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-129">Use hello **Update-AzureRmProfile** cmdlet tooupdate hello modules in an API version profile toohello latest version of modules that are available in hello PSGallery.</span></span> <span data-ttu-id="fd4ec-130">Se recomienda tooalways ejecute hello **AzureRmProfile actualización** cmdlet en una nueva tooavoid de sesión de PowerShell entra en conflicto al importar módulos.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-130">It's recommended tooalways run hello **Update-AzureRmProfile** cmdlet in a new PowerShell session tooavoid conflicts when importing modules.</span></span> <span data-ttu-id="fd4ec-131">Hola siguiente las tareas ejecuta el cmdlet de Hello AzureRmProfile de actualización:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-131">hello Update-AzureRmProfile cmdlet runs hello following tasks:</span></span>

1. <span data-ttu-id="fd4ec-132">Comprueba si las últimas versiones de Hola de módulos se instalan en hello dado el perfil de la versión de API para el ámbito actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-132">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="fd4ec-133">Le pide que tooinstall si no están ya instalados.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-133">Prompts you tooinstall if they are not already installed.</span></span>  
3. <span data-ttu-id="fd4ec-134">Instala e importa módulos Hola actualizado en la sesión actual de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-134">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="fd4ec-135">versiones de hello previamente instalado tooremove de módulos de hello antes de actualizar toohello última versión disponible, usar el cmdlet de hello AzureRmProfile actualización junto con hello **- RemovePreviousVersions** parámetro:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-135">tooremove hello previously installed versions of hello modules before updating toohello latest available version, use hello Update-AzureRmProfile cmdlet along with hello **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="fd4ec-136">Este cmdlet ejecuta Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="fd4ec-136">This cmdlet runs hello following tasks:</span></span>  

1. <span data-ttu-id="fd4ec-137">Comprueba si las últimas versiones de Hola de módulos se instalan en hello dado el perfil de la versión de API para el ámbito actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-137">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="fd4ec-138">Quita las versiones anteriores de Hola de módulos de perfil de versión de API actual de Hola y en la sesión actual de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-138">Removes hello older versions of modules from hello current API version profile and in hello current PowerShell session.</span></span>  
4. <span data-ttu-id="fd4ec-139">le versión más reciente de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-139">prompts you tooinstall hello latest version.</span></span>  
5. <span data-ttu-id="fd4ec-140">Instala e importa módulos Hola actualizado en la sesión actual de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-140">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="fd4ec-141">Desinstalar perfiles</span><span class="sxs-lookup"><span data-stu-id="fd4ec-141">Uninstall profiles</span></span>

<span data-ttu-id="fd4ec-142">Hola de uso **AzureRmProfile desinstalar** cmdlet toouninstall Hola especifica el perfil de la versión de API.</span><span class="sxs-lookup"><span data-stu-id="fd4ec-142">Use hello **Uninstall-AzureRmProfile** cmdlet toouninstall hello specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="fd4ec-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fd4ec-143">Next steps</span></span>
* <span data-ttu-id="fd4ec-144">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Instalación de PowerShell para Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="fd4ec-144">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md)</span></span>
* [<span data-ttu-id="fd4ec-145">Configurar el entorno de PowerShell del usuario de hello pila de Azure</span><span class="sxs-lookup"><span data-stu-id="fd4ec-145">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
