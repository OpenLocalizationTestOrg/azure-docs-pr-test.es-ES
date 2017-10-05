---
title: "Administración de la red CDN de Azure con PowerShell | Microsoft Docs"
description: Aprenda a usar los cmdlets de Azure PowerShell para administrar la red CDN de Azure.
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
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="f5a8f-103">Administración de la red CDN de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5a8f-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="f5a8f-104">PowerShell proporciona uno de los métodos más flexibles para administrar los perfiles y puntos de conexión de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="f5a8f-105">Puede usar PowerShell interactivamente o mediante la escritura de scripts para automatizar tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="f5a8f-106">Este tutorial muestra algunas de las tareas más comunes que puede realizar con PowerShell para administrar los perfiles y puntos de conexión de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5a8f-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f5a8f-107">Prerequisites</span></span>
<span data-ttu-id="f5a8f-108">Para usar PowerShell para administrar los perfiles y puntos de conexión de la red CDN de Azure debe tener instalado el módulo de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="f5a8f-109">Para obtener información sobre cómo instalar Azure PowerShell y conectarlo a Azure mediante el cmdlet `Login-AzureRmAccount` consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5a8f-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5a8f-110">Debe iniciar sesión con `Login-AzureRmAccount` para poder ejecutar los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="f5a8f-111">Lista de los cmdlets de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="f5a8f-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="f5a8f-112">Puede enumerar todos los cmdlets de la red CDN de Azure mediante el cmdlet `Get-Command` .</span><span class="sxs-lookup"><span data-stu-id="f5a8f-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="f5a8f-113">Ayuda</span><span class="sxs-lookup"><span data-stu-id="f5a8f-113">Getting help</span></span>
<span data-ttu-id="f5a8f-114">Puede obtener ayuda para cualquiera de estos cmdlets mediante el cmdlet `Get-Help` .</span><span class="sxs-lookup"><span data-stu-id="f5a8f-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="f5a8f-115">`Get-Help` proporciona el uso y la sintaxis y, opcionalmente, muestra ejemplos.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="f5a8f-116">Listado de perfiles existentes de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="f5a8f-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="f5a8f-117">El cmdlet `Get-AzureRmCdnProfile` sin parámetros permite recuperar todos los perfiles de red CDN existentes.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="f5a8f-118">Esta salida se puede canalizar a cmdlets para la enumeración.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="f5a8f-119">También puede devolver un solo perfil especificando el grupo de recursos y el nombre del perfil.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="f5a8f-120">Es posible tener varios perfiles de red CDN con el mismo nombre, siempre y cuando estén en distintos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="f5a8f-121">Si se omite el parámetro `ResourceGroupName` se devolverán todos los perfiles con un nombre coincidente.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="f5a8f-122">Listado de los puntos de conexión existentes de la red CDN</span><span class="sxs-lookup"><span data-stu-id="f5a8f-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="f5a8f-123">`Get-AzureRmCdnEndpoint` puede recuperar un punto de conexión individual o todos los puntos de conexión de un perfil.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="f5a8f-124">Creación de perfiles y puntos de conexión de red CDN</span><span class="sxs-lookup"><span data-stu-id="f5a8f-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="f5a8f-125">`New-AzureRmCdnProfile` y `New-AzureRmCdnEndpoint` se utilizan para crear perfiles y puntos de conexión de red CDN.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="f5a8f-126">Comprobación de la disponibilidad del nombre de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="f5a8f-126">Checking endpoint name availability</span></span>
<span data-ttu-id="f5a8f-127">`Get-AzureRmCdnEndpointNameAvailability` devuelve un objeto que indica si un nombre de punto de conexión está disponible.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="f5a8f-128">Incorporación de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="f5a8f-128">Adding a custom domain</span></span>
<span data-ttu-id="f5a8f-129">`New-AzureRmCdnCustomDomain` agrega un nombre de dominio personalizado a un punto de conexión existente.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5a8f-130">Necesita configurar el CNAME con su proveedor de DNS como se describe en [Cómo asignar un dominio personalizado al punto de conexión de la Red de entrega de contenido (CDN)](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="f5a8f-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="f5a8f-131">Puede probar la asignación antes de modificar el punto de conexión mediante `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="f5a8f-132">Modificación de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="f5a8f-132">Modifying an endpoint</span></span>
<span data-ttu-id="f5a8f-133">`Set-AzureRmCdnEndpoint` modifica un punto de conexión ya existente.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="f5a8f-134">Purga o precarga de los recursos de red CDN</span><span class="sxs-lookup"><span data-stu-id="f5a8f-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="f5a8f-135">`Unpublish-AzureRmCdnEndpointContent` purga los recursos de la caché, mientras que `Publish-AzureRmCdnEndpointContent` precarga los recursos en puntos de conexión compatibles.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="f5a8f-136">Inicio y detención de puntos de conexión de red CDN</span><span class="sxs-lookup"><span data-stu-id="f5a8f-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="f5a8f-137">`Start-AzureRmCdnEndpoint` y `Stop-AzureRmCdnEndpoint` se pueden utilizar para iniciar y detener los puntos de conexión individuales o los grupos de estos.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="f5a8f-138">Eliminación de recursos de red CDN</span><span class="sxs-lookup"><span data-stu-id="f5a8f-138">Deleting CDN resources</span></span>
<span data-ttu-id="f5a8f-139">`Remove-AzureRmCdnProfile` y `Remove-AzureRmCdnEndpoint` se pueden utilizar para quitar perfiles y puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="f5a8f-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="f5a8f-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5a8f-140">Next Steps</span></span>
<span data-ttu-id="f5a8f-141">Aprenda a automatizar Azure CDN con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="f5a8f-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="f5a8f-142">Para obtener información sobre las características de la red CDN, vea [Información general de la red CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5a8f-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

