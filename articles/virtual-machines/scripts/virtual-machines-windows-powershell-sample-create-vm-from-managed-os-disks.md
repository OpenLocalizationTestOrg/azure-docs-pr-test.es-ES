---
title: "aaaAzure ejemplo de Script de PowerShell: crear una máquina virtual si se adjunta un disco como disco del sistema operativo administrado | Documentos de Microsoft"
description: "Script de Azure PowerShell de Azure de ejemplo: creación de una máquina virtual conectando un disco administrado como disco del SO"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a>Creación de una máquina virtual con un disco del SO administrado mediante PowerShell

Este script crea una máquina virtual conectando un disco administrado como disco del SO. Use este script en los anteriores escenarios:
* Creación de una máquina virtual desde un disco del SO administrado que se copió desde un disco administrado de otra suscripción
* Creación de una máquina virtual desde un disco administrado que se creó a partir de un archivo de disco duro virtual especializado 
* Creación de una máquina virtual desde un disco del SO administrado que se creó a partir de una instantánea 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola comandos tooget administrado disco propiedades siguientes, adjuntar un disco administrado tooa nueva máquina virtual y cree una máquina virtual. Cada elemento de la documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [Get-AzureRmDisk](/powershell/module/azurerm.compute/Get-AzureRmDisk) | Obtiene el objeto de disco basado en nombre de Hola y el grupo de recursos de Hola de un disco. Propiedad de Id. de hello devuelto objeto de disco es tooattach usado Hola disco tooa nueva máquina virtual |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Crea una configuración de máquina virtual. Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas. configuración de Hola se utiliza durante la creación de máquinas virtuales. |
| [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) | Adjunta un disco administrado mediante la propiedad de Id. de hello del disco de hello como sistema operativo disco tooa nueva máquina virtual de |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Crea una dirección IP pública. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Crea una interfaz de red. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Cree una máquina virtual. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Quita un grupo de recursos y todos los recursos incluidos en él. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
