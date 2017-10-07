---
title: "aaaGet un identificador de máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Describe cómo tooget y use una única máquina virtual de Azure Linux identificador."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Acceso y uso del identificador único de máquina virtual de Azure
El identificador único de máquina virtual de Azure es un identificador de 128 bits codificado y almacenado en todas las SMBIOS de la máquina virtual IaaS de Azure; actualmente se puede leer mediante comandos BIOS de la plataforma.

El identificador único de máquina virtual de Azure es una propiedad de solo lectura. El identificador único de máquina virtual de Azure no cambiará durante el cierre de reinicio (tanto si se ha planeado como si no), durante el inicio o la detención de la desasignación, durante la recuperación del servicio o la restauración local. Sin embargo, si hello VM es una instantánea y copiado toocreate una nueva instancia, se configura nuevo Id. de máquina virtual de Azure.

> [!NOTE]
> Si tiene máquinas virtuales anteriores crearlas y ejecutan porque esta nueva característica se obtuvo implantada (18 de septiembre de 2014), reinicie la máquina virtual tooautomatically obtener un identificador único Azure.
> 
> 

tooaccess Azure único Id. de máquina virtual desde dentro de hello VM:

## <a name="create-a-vm"></a>Creación de una VM
Para más información, consulte [Creación de una máquina virtual](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="connect-toohello-vm"></a>Conectar toohello VM
Para más información, consulte [SSH desde Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="query-vm-unique-id"></a>Consulta de un identificador único de máquina virtual
Comando (en el ejemplo se emplea **Ubuntu**):

```bash
sudo dmidecode | grep UUID
```

Resultados esperados del ejemplo:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

Pagar tooBig un orden de bits Endian, hello real Id. único de VM en este caso puede ser:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

Id. único de Azure VM puede utilizarse en escenarios diferentes si hello VM se ejecuta en Azure o en local y puede ayudar a los requisitos de seguimiento de licencias, informes o general que puede tener en sus implementaciones de IaaS de Azure. Muchos proveedores independientes de software crear aplicaciones y certificar a ellos en Azure pueden requerir una VM de Azure a lo largo de su ciclo de vida y tootell tooidentify si Hola VM se ejecuta en Azure, local o en otros proveedores de nube. Este identificador de plataforma como puede ayudar a detectar si el software de hello tiene una licencia o ayuda toocorrelate cualquier origen de tooits de datos de máquina virtual como tooassist acerca de cómo configurar las métricas de derecho de hello para la plataforma correcta de Hola y tootrack y correlacionar estas métricas entre otros usos.

