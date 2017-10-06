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
# <a name="manage-azure-cdn-with-powershell"></a>Administración de la red CDN de Azure con PowerShell
PowerShell uno de hello más flexible métodos toomanage proporciona a los perfiles de red CDN de Azure y los puntos de conexión.  Puede usar PowerShell interactivamente o escribiendo scripts tooautomate tareas de administración.  Este tutorial muestra algunas de las tareas más comunes de Hola que puede realizar con PowerShell toomanage sus perfiles de red CDN de Azure y los puntos de conexión.

## <a name="prerequisites"></a>Requisitos previos
toouse PowerShell toomanage sus perfiles de red CDN de Azure y los puntos de conexión, debe tener instalado el módulo de PowerShell de Azure de Hola.  toolearn cómo tooinstall PowerShell de Azure y conectar tooAzure con hello `Login-AzureRmAccount` cmdlet, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

> [!IMPORTANT]
> Debe iniciar sesión con `Login-AzureRmAccount` para poder ejecutar los cmdlets de Azure PowerShell.
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a>Lista de cmdlets de Azure CDN Hola
Puede enumerar todos los cmdlets de Azure CDN Hola con hello `Get-Command` cmdlet.

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

## <a name="getting-help"></a>Ayuda
También puede obtener ayuda con cualquiera de estos cmdlets mediante hello `Get-Help` cmdlet.  `Get-Help` proporciona el uso y la sintaxis y, opcionalmente, muestra ejemplos.

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

## <a name="listing-existing-azure-cdn-profiles"></a>Listado de perfiles existentes de la red CDN de Azure
Hola `Get-AzureRmCdnProfile` cmdlet sin parámetros recupera todos los perfiles de red CDN existentes.

```powershell
Get-AzureRmCdnProfile
```

Este resultado puede ser toocmdlets canalizada para la enumeración.

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

También puede devolver un solo perfil mediante la especificación de grupo de recursos y el nombre de perfil de Hola.

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> Es posible toohave CDN varios perfiles con hello mismo nombre, siempre y cuando están en distintos grupos de recursos.  Si se omite hello `ResourceGroupName` parámetro devuelve todos los perfiles con un nombre coincidente.
> 
> 

## <a name="listing-existing-cdn-endpoints"></a>Listado de los puntos de conexión existentes de la red CDN
`Get-AzureRmCdnEndpoint`puede recuperar un punto de conexión individual o todos los extremos de hello en un perfil.  

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

## <a name="creating-cdn-profiles-and-endpoints"></a>Creación de perfiles y puntos de conexión de red CDN
`New-AzureRmCdnProfile`y `New-AzureRmCdnEndpoint` son perfiles de red CDN toocreate utilizados y puntos de conexión.

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a>Comprobación de la disponibilidad del nombre de un punto de conexión
`Get-AzureRmCdnEndpointNameAvailability` devuelve un objeto que indica si un nombre de punto de conexión está disponible.

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a>Incorporación de un dominio personalizado
`New-AzureRmCdnCustomDomain`Agrega un extremo en la tooan de nombre de dominio personalizado existente.

> [!IMPORTANT]
> Debe configurar Hola CNAME con su proveedor de DNS como se describe en [cómo punto de conexión de red de entrega (CDN) de toomap dominio personalizado tooContent](cdn-map-content-to-custom-domain.md).  Puede probar la asignación de hello antes de modificar el punto de conexión mediante `Test-AzureRmCdnCustomDomain`.
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

## <a name="modifying-an-endpoint"></a>Modificación de un punto de conexión
`Set-AzureRmCdnEndpoint` modifica un punto de conexión ya existente.

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a>Purga o precarga de los recursos de red CDN
`Unpublish-AzureRmCdnEndpointContent` purga los recursos de la caché, mientras que `Publish-AzureRmCdnEndpointContent` precarga los recursos en puntos de conexión compatibles.

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a>Inicio y detención de puntos de conexión de red CDN
`Start-AzureRmCdnEndpoint`y `Stop-AzureRmCdnEndpoint` pueden toostart usado y detener los extremos individuales o grupos de puntos de conexión.

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a>Eliminación de recursos de red CDN
`Remove-AzureRmCdnProfile`y `Remove-AzureRmCdnEndpoint` pueden ser utilizados tooremove perfiles y los puntos de conexión.

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo tooautomate CDN de Azure con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).

toolearn acerca de las características de red CDN, vea [información general de la red CDN](cdn-overview.md).

