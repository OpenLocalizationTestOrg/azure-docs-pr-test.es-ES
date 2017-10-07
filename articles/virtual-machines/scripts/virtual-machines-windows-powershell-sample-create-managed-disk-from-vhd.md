---
title: "aaaAzure ejemplo de Script de PowerShell: crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en la misma o distintas suscripción | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: crear un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Creación de un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción con PowerShell

Este script crea un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción. Utilice este tooimport script un versión especializada del toocreate de (no generalizado/preparada con Sysprep) VHD toomanaged OS disco una máquina virtual. Además, utilizarlo tooimport un disco de datos de toomanaged de disco duro virtual de datos. 

No debe crear varios discos administrados idénticos desde un archivo VHD en un período de tiempo corto. discos administrados por toocreate desde un archivo de disco duro virtual, se crea la instantánea de blob del archivo de disco duro virtual de hello y, a continuación, resulta discos utilizados toocreate administrado. Instantánea de solo blob puede crearse en un minuto que provoca errores de creación de disco toothrottling due. tooavoid esta limitación, cree un [administrado instantánea del archivo de disco duro virtual de hello](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) y, a continuación, use Hola administrados instantánea toocreate varios discos administrados en poco tiempo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explicación del script

Este script usará los siguientes comandos toocreate un disco administrado desde un disco duro virtual en otra suscripción. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crea la configuración de disco que se usa para la creación del disco. Incluye el tipo de almacenamiento, ubicación, Id. de cuenta de almacenamiento de Hola donde se almacena el VHD primario de hello, URI de VHD de VHD primario de Hola de recurso. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros. |

## <a name="next-steps"></a>Pasos siguientes

[Creación de una máquina virtual conectando un disco administrado como disco del SO](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
