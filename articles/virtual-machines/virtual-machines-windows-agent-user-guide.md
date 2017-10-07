---
title: "Introducción al agente de máquina Virtual aaaAzure | Documentos de Microsoft"
description: "Información general del agente de máquina virtual de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Información general del agente de máquina virtual de Azure

Hola agente de máquina Virtual de Microsoft Azure (agente de VM) es un proceso protegido, ligero que administra la interacción de VM con hello controlador de tejido de Azure. Hola agente de máquina virtual tiene un rol principal en habilitar y ejecutar las extensiones de máquina virtual de Azure. Las extensiones de VM habilitan la configuración posterior a la implementación de máquinas virtuales, como la instalación y configuración de software. Extensiones de máquina virtual también habilitar características de recuperación como restablecer la contraseña administrativa de Hola de una máquina virtual. Sin Hola agente de máquina virtual de Azure, no se puede ejecutar las extensiones de máquina virtual.

Este documento describe la instalación, la detección y eliminación de hello agente de máquina Virtual de Azure.

## <a name="install-hello-vm-agent"></a>Instalar agente de máquina virtual de Hola

### <a name="azure-gallery-image"></a>Imagen de la galería de Azure

Hello Azure VM Agent está instalado de forma predeterminada en cualquier máquina virtual de Windows implementada a partir de una imagen de la Galería de Azure. Al implementar una imagen de la Galería de Azure de hello Portal, PowerShell, interfaz de línea de comandos o una plantilla de Azure Resource Manager, instalarse hello que también es el agente de máquina virtual de Azure. 

### <a name="manual-installation"></a>Instalación manual

agente de máquina virtual de Windows Hello puede instalarse manualmente mediante un paquete de Windows installer. La instalación manual puede ser necesaria cuando se crea una imagen de máquina virtual personalizada que se implementará en Azure. Hola de toomanually instalar agente de máquina virtual de Windows, descargue el instalador de agente de máquina virtual de Hola desde esta ubicación [descarga del agente de Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789). 

Hola agente de máquina virtual se puede instalar haciendo doble clic en el archivo de instalador de windows hello. Para una instalación desatendida o automatizada de agente de máquina virtual de Hola, ejecute hello siguiente comando.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Detectar Hola agente de máquina virtual

### <a name="powershell"></a>PowerShell

módulo de PowerShell de administrador de recursos de Azure de Hello puede ser usado tooretrieve información acerca de máquinas virtuales de Azure. Ejecuta `Get-AzureRmVM` devuelve una gran cantidad de información incluidas Hola Hola agente de máquina virtual de Azure en el estado de aprovisionamiento.

```PowerShell
Get-AzureRmVM
```

Hola siguiente es un subconjunto de hello `Get-AzureRmVM` salida. Hola aviso `ProvisionVMAgent` propiedad anidada dentro de `OSProfile`, esta propiedad puede ser usado toodetermine si agente de máquina virtual de Hola se ha implementado toohello virtual machine.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

Hola siguiente secuencia de comandos puede ser tooreturn usa una lista concisa de nombres de máquina virtual y el estado de Hola de hello agente de máquina virtual.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Detección manual

Cuando se registran en tooa VM de Windows Azure, el Administrador de tareas puede ser usado tooexamine procesos en ejecución. toocheck para hello agente de máquina virtual de Azure, abra el Administrador de tareas > haga clic en la ficha de detalles de Hola y busque un nombre de proceso `WindowsAzureGuestAgent.exe`. presencia de Hola de este proceso indica que Hola VM agent esté instalado.

## <a name="upgrade-hello-vm-agent"></a>Actualizar Hola agente de máquina virtual

Agente para Windows de Hello Azure VM se actualiza automáticamente. Como nuevas máquinas virtuales implementada tooAzure, recibirán el agente de máquina virtual más reciente de Hola. Imágenes de máquina virtual personalizadas deben ser agente tooinclude actualizadas manualmente Hola de nueva máquina virtual.
