---
title: "Ejemplo de Script de PowerShell - tooVMs de tráfico de equilibrio de carga para lograr alta disponibilidad aaaAzure | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - tooVMs de tráfico de equilibrio de carga para lograr alta disponibilidad"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Cargar tooVMs de tráfico de equilibrio de alta disponibilidad

Este ejemplo de secuencia de comandos crea todo lo necesario toorun varias máquinas virtuales de Windows configurado en una alta disponibilidad y de carga equilibrada de configuración. Después de ejecutar script de Hola, tendrá tres máquinas virtuales, tooan Unidos a un conjunto de disponibilidad de Azure y es accesible a través de un equilibrador de carga de Azure.

Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Crea una configuración de subred. Esta configuración se utiliza con el proceso de creación de red virtual de Hola. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Crea una red virtual y una subred de Azure. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | Crea una dirección IP pública con una dirección IP estática y un nombre DNS asociado. |
| [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)  | Crea una instancia de Azure Load Balancer. |
| [New-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Crea un sondeo de equilibrador de carga. Un sondeo del equilibrador de carga es toomonitor usado en cada máquina virtual en el conjunto de equilibrador de carga de Hola. Si ninguna máquina virtual deja de estar accesible, el tráfico no es toohello enrutado máquina virtual. |
| [New-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Crea una regla de Load Balancer. En este ejemplo, se crea una regla para el puerto 80. Como el tráfico HTTP llega al equilibrador de carga de hello, es tooport enrutado 80 una de las máquinas virtuales de hello en el conjunto de equilibrador de carga de Hola. |
| [New-AzureRmLoadBalancerInboundNatRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | Crea una regla de traducción de direcciones de red (NAT) de Load Balancer.  Las reglas NAT asignan un puerto de puerto de tooa de equilibrador de carga de hello en una máquina virtual. En este ejemplo, se crea una regla NAT para SSH tráfico tooeach VM en el conjunto de equilibrador de carga de Hola.  |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Crea un grupo de seguridad de red (NSG), que es un límite de seguridad entre Hola internet y hello las máquinas virtuales. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Crea un tooallow de regla NSG el tráfico entrante. En este ejemplo, el puerto 22 está abierto al tráfico SSH. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Crea una tarjeta de red virtual y lo adjunta toohello de red virtual, subred y NSG. |
| [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Crea un conjunto de disponibilidad. Conjuntos de disponibilidad de garantizan la disponibilidad de las aplicaciones repartir hello las máquinas virtuales entre recursos físicos de forma que si se produce el error, no se realiza el conjunto completo de Hola. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Crea una configuración de máquina virtual. Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas. configuración de Hola se utiliza durante la creación de máquinas virtuales. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)  | Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG. Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
