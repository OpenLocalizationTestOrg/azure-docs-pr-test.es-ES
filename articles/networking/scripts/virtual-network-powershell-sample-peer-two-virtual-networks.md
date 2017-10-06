---
title: Ejemplo de Script de PowerShell - aaaAzure del mismo nivel dos redes virtuales | Documentos de Microsoft
description: 'Ejemplo de script de Azure PowerShell: emparejar dos redes virtuales'
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a>Conectar dos redes virtuales

Este script crea y se conecta dos redes virtuales en Hola Hola de trhough región misma red de Azure. Después de ejecutar el script de Hola, creará un emparejamiento entre dos redes virtuales.

Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script usa Hola después comandos toocreate un grupo de recursos, la máquina virtual, y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crea un grupo de recursos en el que se almacenan todos los recursos. | 
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| Crea una red virtual y una subred de Azure. |
| [Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | Crea un emparejamiento entre dos redes virtuales.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
