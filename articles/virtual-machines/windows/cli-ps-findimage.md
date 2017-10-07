---
title: "imágenes de aaaSelect Windows VM de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure PowerSHell toodetermine Hola publisher, oferta, SKU y versión para imágenes de máquina virtual de Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Cómo imágenes toofind VM de Windows en hello Azure Marketplace con PowerShell de Azure

Este tema describe cómo toouse toofind de PowerShell de Azure VM imágenes en hello Azure Marketplace. Utilice este toospecify una imagen de Marketplace de información cuando se crea una máquina virtual de Windows.

Asegúrese de que instaló y configuró hello más reciente [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Tabla de imágenes de Windows más usadas
| PublisherName | Oferta | SKU |
|:--- |:--- |:--- |:--- |
| Microsoft Windows Server |Windows Server |2016-Datacenter |
| Microsoft Windows Server |Windows Server |2016-Datacenter-Server-Core |
| Microsoft Windows Server |Windows Server |2016-Datacenter-with-Containers |
| Microsoft Windows Server |Windows Server |2016-Nano-Server |
| Microsoft Windows Server |Windows Server |Centro de datos de 2012-R2 |
| Microsoft Windows Server |Windows Server |2008-R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016-WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2-WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Búsqueda de imágenes específicas


Al crear una nueva máquina virtual con el Administrador de recursos de Azure, en algunos casos debe toospecify una imagen con combinación de Hola de hello propiedades de imagen siguientes:

* Publicador
* Oferta
* SKU

Por ejemplo, utilice estos valores con hello [AzureRMVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet de PowerShell, o con una plantilla de grupo de recursos en el que debe especificar el tipo de Hola de toobe de máquina virtual que creó.

Si necesita toodetermine estos valores, puede ejecutar hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), y [AzureRMVMImageSku Get](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets imágenes de hello toonavigate. Determine estos valores:

1. Editores de imagen de Hola de lista.
2. Para un publicador determinado, enumeración de sus ofertas.
3. Para una oferta determinada, enumeración de sus SKU.

En primer lugar, lista publicadores Hola con hello siguientes comandos:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Rellene el nombre del publicador elegido y ejecute hello siguientes comandos:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Rellene el nombre de la oferta elegida y ejecute hello siguientes comandos:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

De salida de hello de hello `Get-AzureRMVMImageSku` comando tiene toda la información de hello necesita imagen de hello toospecify para una nueva máquina virtual.

Hola continuación, muestra un ejemplo completo:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Salida:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Para el publicador de "Microsoft Windows Server" hello:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Salida:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Para la oferta de "Windows Server" hello:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Salida:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

En esta lista, copie Hola elegido el nombre de SKU y tiene toda la información de Hola de hello `Set-AzureRMVMSourceImage` cmdlet de PowerShell o una plantilla de grupo de recursos.

## <a name="next-steps"></a>Pasos siguientes
Ahora puede elegir exactamente Hola imagen desea toouse. toocreate una máquina virtual rápidamente mediante el uso de información de la imagen de hello, que acaba de encontrar, consulte [crear una máquina virtual de Windows con PowerShell](quick-create-powershell.md).
