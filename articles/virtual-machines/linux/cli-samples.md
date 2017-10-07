---
title: Ejemplos de CLI aaaAzure | Documentos de Microsoft
description: Ejemplos de la CLI de Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>Ejemplos de la CLI de Azure para máquinas virtuales Linux

Hello tabla siguiente incluye vínculos toobash scripts creados con hello CLI de Azure.

| | |
|---|---|
|**Creación de máquinas virtuales**||
| [Creación de una máquina virtual](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una máquina virtual Linux con una configuración mínima. |
| [Creación una máquina virtual completamente configurada](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un grupo de recursos, una máquina virtual y todos los recursos relacionados.|
| [Creación de máquinas virtuales de alta disponibilidad](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | Crea varias máquinas virtuales de alta disponibilidad y una configuración de equilibrio de carga. |
| [Creación de una máquina virtual con Docker habilitado](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una máquina virtual, la configura como un host Docker y ejecuta un contenedor NGINX. |
| [Creación de una máquina virtual y ejecución de un script de configuración](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una máquina virtual y usa la extensión tooinstall NGINX de hello Script personalizado de Azure. |
| [Creación de una máquina virtual con WordPress instalado](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una máquina virtual y usa tooinstall de extensión de Script personalizado de Azure de hello WordPress. |
| [Creación de una máquina virtual desde un disco del SO administrado](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | Crea una máquina virtual conectando un disco administrado como disco del SO. |
| [Creación de una VM a partir de una instantánea](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Crea una máquina virtual desde una instantánea creando primero un disco administrado de instantánea y, a continuación, adjuntar Hola nuevo administrado disco como disco del sistema operativo. |
|**Administrar el almacenamiento**||
| [Crear disco administrado desde un disco duro virtual](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | Crea un disco administrado desde un disco duro virtual especializado como un disco del sistema operativo, o desde un disco duro virtual de datos como un disco de datos.  |
| [Crear un disco administrado a partir de una instantánea](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Crea un disco administrado a partir de una instantánea. |
| [Copiar disco administrado toosame u otra suscripción](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Copias administrados disco toosame u otra suscripción pero en Hola misma región como elemento primario de hello administrados disco. 
| [Exportar una instantánea como cuenta de almacenamiento de disco duro virtual tooa](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | Exporta una instantánea administrada como cuenta de almacenamiento de disco duro virtual tooa en otra región. |
| [Copia instantánea toosame u otra suscripción](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Copias instantáneas toosame u otra suscripción pero en Hola misma región que la instantánea primaria de Hola. |
|**Máquinas virtuales de red**||
| [Protección del tráfico de red entre máquinas virtuales](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | Crea dos máquinas virtuales, todos los recursos relacionados y grupos de seguridad de red internos y externos (NSG). |
|**Protección de máquinas virtuales**||
| [Cifrado de una máquina virtual y discos de datos](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una instancia de Azure Key Vault, una clave de cifrado y una entidad de servicio, y luego cifra una máquina virtual. |
|**Supervisión de máquinas virtuales**||
| [Supervisión de una máquina virtual con Operations Management Suite](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una máquina virtual, instala al agente de Operations Management Suite de Hola e inscribe Hola máquina virtual en un área de trabajo de OMS.  |
|**Solución de problemas de máquinas virtuales**||
| [Solución de problemas de un disco de sistema operativo de máquina virtual](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | Monta el disco del sistema operativo de Hola a partir de una máquina virtual como un disco de datos en una segunda máquina virtual. |
| | |
