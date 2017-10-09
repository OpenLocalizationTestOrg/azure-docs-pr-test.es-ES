---
title: "Ejemplos de PowerShell de la máquina Virtual aaaAzure | Documentos de Microsoft"
description: "Ejemplos de PowerShell de máquina virtual de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Ejemplos de PowerShell de máquina virtual de Azure

Hello siguiente tabla incluye ejemplos de secuencias de comandos de tooPowerShell de vínculos que crear y administración máquinas virtuales de Windows.

| | |
|---|---|
|**Creación de máquinas virtuales**||
| [Creación una máquina virtual completamente configurada](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea un grupo de recursos, una máquina virtual y todos los recursos relacionados.|
| [Creación de máquinas virtuales de alta disponibilidad](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea varias máquinas virtuales de alta disponibilidad y una configuración de equilibrio de carga.|
| [Creación de una máquina virtual y ejecución de un script de configuración](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una máquina virtual y usa tooinstall de extensión de Script personalizado de Azure de hello IIS. |
| [Creación de una máquina virtual y ejecución de una configuración de DSC](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una máquina virtual y usa tooinstall de extensión de configuración de estado deseado (DSC) de Azure de hello IIS. |
| [Carga de un disco duro virtual y creación de máquinas virtuales](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods un disco duro virtual local tooAzure de archivos, crea y la imagen de disco duro virtual de hello y, a continuación, crea una máquina virtual desde esa imagen. |
| [Creación de una máquina virtual desde un disco del SO administrado](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una máquina virtual conectando un disco administrado como disco del SO. |
| [Creación de una VM a partir de una instantánea](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una máquina virtual desde una instantánea creando primero un disco administrado de instantánea y, a continuación, adjuntar Hola nuevo administrado disco como disco del sistema operativo. |
|**Administrar el almacenamiento**||
| [Creación de un disco administrado desde un disco duro virtual en la misma u otra suscripción](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea un disco administrado a partir de un disco duro virtual especializado como un disco del sistema operativo, o a partir de un disco duro virtual de datos como un disco de datos en la misma u otra suscripción.  |
| [Creación de un disco administrado a partir de una instantánea](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea un disco administrado a partir de una instantánea. |
| [Copiar disco administrado toosame u otra suscripción](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Copias administrados disco toosame u otra suscripción pero en Hola misma región como elemento primario de hello administrados disco. 
| [Exportar una instantánea como cuenta de almacenamiento de disco duro virtual tooa](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Exporta una instantánea administrada como cuenta de almacenamiento de disco duro virtual tooa en otra región. |
| [Creación de una instantánea a partir de un disco duro virtual](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea instantáneas de un disco duro virtual toocreate varios discos administrados idénticos de instantánea en poco tiempo.  |
| [Copia instantánea toosame u otra suscripción](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Copias instantáneas toosame u otra suscripción pero en Hola misma región que la instantánea primaria de Hola. |
|**Protección de las máquinas virtuales**||
| [Cifrado de una máquina virtual y discos de datos](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Crea una instancia de Azure Key Vault, una clave de cifrado y una entidad de servicio, y luego cifra una máquina virtual. |
|**Supervisión de máquinas virtuales**||
| [Supervisión de una máquina virtual con Operations Management Suite](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crea una máquina virtual, instala al agente de Operations Management Suite de Hola e inscribe Hola máquina virtual en un área de trabajo de OMS.  |
| | |

