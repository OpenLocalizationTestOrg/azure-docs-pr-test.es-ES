---
title: "ejemplo de script de PowerShell aaaAzure - enrutar el tráfico a través de un dispositivo virtual de red | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: redirigir el tráfico a través de una aplicación virtual de red de firewall."
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Redirigir el tráfico a través de una aplicación virtual de red

Este ejemplo de script crea una red virtual con subredes de front-end y back-end. También se crea una máquina virtual con la dirección IP que reenvía el tráfico de tooroute habilitado entre dos subredes de Hola. Después de ejecutar el script de Hola puede implementar software de red, como una aplicación de firewall, toohello máquina virtual.

Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, redes virtuales y grupos de seguridad de red. Cada comando de la tabla de hello vincula documentación específica del toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Crea una subred de front-end y una red virtual de Azure. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Crea subredes de back-end y de red perimetral. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Crea una interfaz de red virtual y habilita el reenvío IP para ella. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Crea un grupo de seguridad de red (NSG). |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Crea reglas NSG que permiten a los puertos HTTP y HTTPS entrantes toohello máquina virtual. |
| [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| Asocia Hola NSG y toosubnets de tablas de ruta. |
| [New-AzureRmRouteTable](/powershell/module/azurerm.network/new-azurermroutetable)| Crea una tabla de rutas para todas las rutas. |
| [New-AzureRMRouteConfig](/powershell/module/azurerm.network/new-azurermrouteconfig)| Crea rutas tooroute tráfico entre subredes y Hola Internet a través de hello máquina virtual. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Crea una máquina virtual y conecta Hola NIC tooit. Este comando también especifica toouse de imagen de máquina virtual de Hola y credenciales administrativas. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | Elimina un grupo de recursos y todos los recursos que contiene. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
