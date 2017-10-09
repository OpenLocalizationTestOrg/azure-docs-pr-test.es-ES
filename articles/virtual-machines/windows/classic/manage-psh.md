---
title: "aaaManage las máquinas virtuales mediante el uso de PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de los comandos que puede usar tareas de tooautomate en la administración de las máquinas virtuales."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Administración de las máquinas virtuales con Azure PowerShell
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para los comandos de PowerShell utilizando el modelo de administrador de recursos de hello comunes, consulte [aquí](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Muchas tareas que hacer cada día toomanage las máquinas virtuales pueden automatizarse mediante el uso de cmdlets de PowerShell de Azure. Este artículo proporciona comandos de ejemplo para las tareas más sencillas y tooarticles de vínculos que mostrar los comandos de Hola para tareas más complejas.

> [!NOTE]
> Si no ha instalado y configurado Azure PowerShell aún, si desea obtener instrucciones en el artículo hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>¿Cómo toouse Hola comandos de ejemplo
Necesitará tooreplace parte del texto de Hola Hola comandos con texto que sea adecuada para su entorno. Hola < y > símbolos indican texto necesita tooreplace. Al reemplazar texto hello, quitar símbolos de hello pero deje las comillas de hello en su lugar.

## <a name="get-a-vm"></a>Obtención de una máquina virtual
Es una tarea básica que utilizará a menudo. Usar tooget información acerca de una máquina virtual, realizar tareas en una máquina virtual u obtener toostore de salida en una variable.

tooget información acerca de Hola de máquina virtual, ejecute este comando, reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

Hola toostore de salida en una variable $vm, ejecute:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Inicie sesión en tooa VM basadas en Windows
Ejecute estos comandos:

> [!NOTE]
> Puede obtener la máquina virtual de Hola y el nombre del servicio de nube de pantalla de Hola de hello **Get-AzureVM** comando.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unidad y la carpeta ubicación toostore Hola Descargar archivo RDP, ejemplo: c:\temp >" $localFile = $localPath + "\" + $vmname +".rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-nombre $vmName - LocalPath $localFile-iniciar
> 
> 

## <a name="stop-a-vm"></a>Detención de una máquina virtual
Ejecute este comando:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Usar este hello tookeep de parámetro en caso de que sea de servicio de IP virtual (VIP) de la nube de Hola Hola última VM en ese servicio en la nube. <br><br> Si usas hello StayProvisioned parámetro, se le facturará por hello máquina virtual.
> 
> 

## <a name="start-a-vm"></a>Inicio de una máquina virtual
Ejecute este comando:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Acoplamiento de un disco de datos
Esta tarea requiere unos pocos pasos. En primer lugar, use Hola *** Add-AzureDataDisk *** cmdlet tooadd hello toohello $vm objeto de disco. A continuación, utilice **Update-AzureVM** configuración de cmdlet tooupdate Hola de hello máquina virtual.

También necesitará toodecide si tooattach un disco nuevo o uno que contiene datos. Para un disco nuevo, el comando hello crea el archivo .vhd de hello y lo adjunta.

tooattach un disco nuevo, ejecute este comando:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

tooattach un disco de datos existente, ejecute este comando:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

tooattach los discos de datos de un archivo .vhd existente en el almacenamiento de blobs, ejecute este comando:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Creación de una máquina virtual Windows
una nueva máquina virtual basada en Windows en Azure, use las instrucciones de hello en toocreate [toocreate de usar PowerShell de Azure y preconfigurar máquinas virtuales basadas en Windows](create-powershell.md). Pasos de este tema le guían a través de la creación de hello de un conjunto de comandos que de Azure PowerShell crea una máquina virtual basada en Windows que puede configurar previamente:

* Con pertenencia al dominio de Active Directory;
* Con discos adicionales;
* Como miembro de un conjunto de carga equilibrada;
* Con una dirección IP estática.

