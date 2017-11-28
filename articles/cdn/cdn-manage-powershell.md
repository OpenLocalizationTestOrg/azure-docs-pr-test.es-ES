---
title: aaaManage CDN de Azure con PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toomanage de cmdlets de PowerShell de Azure CDN de Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="4d196-103">Administración de la red CDN de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d196-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="4d196-104">PowerShell uno de hello más flexible métodos toomanage proporciona a los perfiles de red CDN de Azure y los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4d196-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="4d196-105">Puede usar PowerShell interactivamente o escribiendo scripts tooautomate tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="4d196-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="4d196-106">Este tutorial muestra algunas de las tareas más comunes de Hola que puede realizar con PowerShell toomanage sus perfiles de red CDN de Azure y los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4d196-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d196-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4d196-107">Prerequisites</span></span>
<span data-ttu-id="4d196-108">toouse PowerShell toomanage sus perfiles de red CDN de Azure y los puntos de conexión, debe tener instalado el módulo de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d196-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="4d196-109">toolearn cómo tooinstall PowerShell de Azure y conectar tooAzure con hello `Login-AzureRmAccount` cmdlet, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4d196-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d196-110">Debe iniciar sesión con `Login-AzureRmAccount` para poder ejecutar los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d196-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="4d196-111">Lista de cmdlets de Azure CDN Hola</span><span class="sxs-lookup"><span data-stu-id="4d196-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="4d196-112">Puede enumerar todos los cmdlets de Azure CDN Hola con hello `Get-Command` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4d196-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="4d196-113">Ayuda</span><span class="sxs-lookup"><span data-stu-id="4d196-113">Getting help</span></span>
<span data-ttu-id="4d196-114">También puede obtener ayuda con cualquiera de estos cmdlets mediante hello `Get-Help` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4d196-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="4d196-115">`Get-Help` proporciona el uso y la sintaxis y, opcionalmente, muestra ejemplos.</span><span class="sxs-lookup"><span data-stu-id="4d196-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="4d196-116">Listado de perfiles existentes de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="4d196-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="4d196-117">Hola `Get-AzureRmCdnProfile` cmdlet sin parámetros recupera todos los perfiles de red CDN existentes.</span><span class="sxs-lookup"><span data-stu-id="4d196-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="4d196-118">Este resultado puede ser toocmdlets canalizada para la enumeración.</span><span class="sxs-lookup"><span data-stu-id="4d196-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="4d196-119">También puede devolver un solo perfil mediante la especificación de grupo de recursos y el nombre de perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d196-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="4d196-120">Es posible toohave CDN varios perfiles con hello mismo nombre, siempre y cuando están en distintos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="4d196-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="4d196-121">Si se omite hello `ResourceGroupName` parámetro devuelve todos los perfiles con un nombre coincidente.</span><span class="sxs-lookup"><span data-stu-id="4d196-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="4d196-122">Listado de los puntos de conexión existentes de la red CDN</span><span class="sxs-lookup"><span data-stu-id="4d196-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="4d196-123">`Get-AzureRmCdnEndpoint`puede recuperar un punto de conexión individual o todos los extremos de hello en un perfil.</span><span class="sxs-lookup"><span data-stu-id="4d196-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="4d196-124">Creación de perfiles y puntos de conexión de red CDN</span><span class="sxs-lookup"><span data-stu-id="4d196-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="4d196-125">`New-AzureRmCdnProfile`y `New-AzureRmCdnEndpoint` son perfiles de red CDN toocreate utilizados y puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4d196-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="4d196-126">Comprobación de la disponibilidad del nombre de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="4d196-126">Checking endpoint name availability</span></span>
<span data-ttu-id="4d196-127">`Get-AzureRmCdnEndpointNameAvailability` devuelve un objeto que indica si un nombre de punto de conexión está disponible.</span><span class="sxs-lookup"><span data-stu-id="4d196-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="4d196-128">Incorporación de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="4d196-128">Adding a custom domain</span></span>
<span data-ttu-id="4d196-129">`New-AzureRmCdnCustomDomain`Agrega un extremo en la tooan de nombre de dominio personalizado existente.</span><span class="sxs-lookup"><span data-stu-id="4d196-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d196-130">Debe configurar Hola CNAME con su proveedor de DNS como se describe en [cómo punto de conexión de red de entrega (CDN) de toomap dominio personalizado tooContent](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="4d196-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="4d196-131">Puede probar la asignación de hello antes de modificar el punto de conexión mediante `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="4d196-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="4d196-132">Modificación de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="4d196-132">Modifying an endpoint</span></span>
<span data-ttu-id="4d196-133">`Set-AzureRmCdnEndpoint` modifica un punto de conexión ya existente.</span><span class="sxs-lookup"><span data-stu-id="4d196-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="4d196-134">Purga o precarga de los recursos de red CDN</span><span class="sxs-lookup"><span data-stu-id="4d196-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="4d196-135">`Unpublish-AzureRmCdnEndpointContent` purga los recursos de la caché, mientras que `Publish-AzureRmCdnEndpointContent` precarga los recursos en puntos de conexión compatibles.</span><span class="sxs-lookup"><span data-stu-id="4d196-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="4d196-136">Inicio y detención de puntos de conexión de red CDN</span><span class="sxs-lookup"><span data-stu-id="4d196-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="4d196-137">`Start-AzureRmCdnEndpoint`y `Stop-AzureRmCdnEndpoint` pueden toostart usado y detener los extremos individuales o grupos de puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4d196-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="4d196-138">Eliminación de recursos de red CDN</span><span class="sxs-lookup"><span data-stu-id="4d196-138">Deleting CDN resources</span></span>
<span data-ttu-id="4d196-139">`Remove-AzureRmCdnProfile`y `Remove-AzureRmCdnEndpoint` pueden ser utilizados tooremove perfiles y los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="4d196-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="4d196-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d196-140">Next Steps</span></span>
<span data-ttu-id="4d196-141">Obtenga información acerca de cómo tooautomate CDN de Azure con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="4d196-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="4d196-142">toolearn acerca de las características de red CDN, vea [información general de la red CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d196-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

