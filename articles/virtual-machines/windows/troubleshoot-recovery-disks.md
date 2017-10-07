---
title: "aaaUse una aplicación de Windows, solución de problemas de máquina virtual con PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo emite tootroubleshoot VM de Windows en Azure mediante la conexión de recuperación de tooa de disco de hello SO máquina virtual mediante PowerShell de Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Solucionar problemas de una VM de Windows mediante una asociación recuperación tooa de disco Hola SO máquina virtual mediante PowerShell de Azure
Si la máquina virtual de Windows (VM) en Azure detecta un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas. Un ejemplo común sería una actualización de la aplicación que ha fallado que impide que Hola VM se pueda tooboot correctamente. Este artículo detalles de cómo toouse Azure PowerShell tooconnect su toofix de disco duro virtual tooanother VM de Windows los errores, a continuación, volver a crear la máquina virtual original.


## <a name="recovery-process-overview"></a>Introducción al proceso de recuperación
proceso de solución de problemas de Hello es como sigue:

1. Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.
2. Adjuntar y montar tooanother de disco duro virtual de hello VM de Windows para solucionar problemas.
3. Conectar toohello solución de problemas de máquina virtual. Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.
4. Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.
5. Crear una máquina virtual mediante hello: disco duro virtual original.

Asegúrese de que dispone de [Hola más reciente de PowerShell de Azure](/powershell/azure/overview) instalado y registrado en tooyour suscripción:

```powershell
Login-AzureRMAccount
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros con sus propios valores. Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.


## <a name="determine-boot-issues"></a>Determinación de los problemas de arranque
Puede ver una captura de pantalla de la máquina virtual en Azure toohelp solucionar problemas de arranque. Esta captura de pantalla puede ayudar a identificar por qué se produce un error en una máquina virtual tooboot. Hello en el ejemplo siguiente se obtiene Hola captura de pantalla de máquina virtual de Windows denominada Hola `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Revise toodetermine de captura de pantalla de hello ¿por qué no Hola VM puede tooboot. Tenga en cuenta todos los mensajes de error o códigos de error específicos proporcionados.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualización de los detalles del disco duro virtual existente
Para poder adjuntar su tooanother de disco duro virtual, necesita tooidentify Hola nombre de disco duro virtual (VHD) de Hola.

Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Busque `Vhd URI` en hello `StorageProfile` sección de salida de hello de hello anterior comando. siguiente salida de ejemplo truncados Hello muestra hello `Vhd URI` hacia el final de Hola Hola del bloque de código:

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a>Eliminación de la VM existente
Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure. Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones. Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC). Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual. Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual. concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.

Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio. Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento. Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.

Después de eliminaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` del grupo de recursos de hello denominado `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual. concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Adjuntar tooanother de disco duro virtual existente
Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas. Adjuntar toothis Hola de disco duro virtual existente toobrowse VM de solución de problemas y editar el contenido del disco de Hola. Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo. Elija o cree otro toouse de máquina virtual para solucionar problemas.

Al adjuntar hello: disco duro virtual existente, especifique el disco de toohello de dirección URL de hello obtenido en hello anterior `Get-AzureRmVM` comando. Hello en el ejemplo siguiente se asocia un toohello de disco duro virtual existente solución de problemas de máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Agregar un disco, requiere toospecify Hola un tamaño de disco de Hola. Se adjunta un disco existente, Hola `-DiskSizeInGB` se especifica como `$null`. Este valor garantiza disco de datos de hello está correctamente conectado y sin Hola necesita toodetermine Hola tamaño real del disco de datos.


## <a name="mount-hello-attached-data-disk"></a>Montar el disco de datos adjuntos de Hola

1. RDP tooyour de solución de problemas de máquina virtual con las credenciales adecuadas de Hola. Hello en el ejemplo siguiente se descarga Hola archivo de conexión de RDP para la máquina virtual denominada hello `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`y lo descarga demasiado`C:\Users\ops\Documents`"

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. disco de datos de Hola se detecta automáticamente y se adjunta. Ver lista de hello volúmenes conectados toodetermine Hola letra de unidad como sigue:

    ```powershell
    Get-Disk
    ```

    Después de la salida de ejemplo de Hola muestra el disco duro virtual de hello conectado un disco **2**. (También puede usar `Get-Volume` letra de unidad de hello tooview):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Solución de problemas en el disco duro virtual original
Con hello disco duro virtual existente montado, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario. Una vez que se ha solucionado problemas hello, continúe con hello pasos.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmontaje y desconexión del disco duro virtual original
Una vez que se resuelven los errores, desmonta y separar hello: disco duro virtual existente de la máquina virtual para solucionar problemas. No se puede usar el disco duro virtual con cualquier otra máquina virtual hasta que se libera la concesión de hello adjuntar toohello de disco duro virtual de hello VM de solución de problemas.

1. Desde dentro de la sesión RDP, desmonte el disco de datos de hello en la máquina virtual de recuperación. Se necesita número de disco de Hola de hello anterior `Get-Disk` cmdlet. A continuación, utilice `Set-Disk` tooset disco de hello como sin conexión:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Confirme el disco de hello ahora está establecido como sin conexión mediante `Get-Disk` nuevo. Hello siguiente salida de ejemplo muestra el disco de hello ahora está establecido como sin conexión:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. Salga de la sesión RDP. En la sesión de PowerShell de Azure, quite disco duro virtual de Hola Hola VM de solución de problemas.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Creación de máquina virtual a partir del disco duro original
usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). plantilla JSON real de Hello está en hello siguiente vínculo:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

plantilla de Hello implementa una máquina virtual en una red virtual existente, mediante Hola dirección URL del VHD de hello comando anteriormente. Hello en el ejemplo siguiente se implementa grupo de recursos de toohello Hola plantilla llamado `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

Hola de respuesta solicita plantilla hello como nombre de máquina virtual, el tipo de sistema operativo y el tamaño VM. Hola `osDiskVhdUri` es Hola mismo utiliza anteriormente al adjuntar toohello Hola de disco duro virtual existente VM de solución de problemas.


## <a name="re-enable-boot-diagnostics"></a>Rehabilitación de los diagnósticos de arranque

Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente. Hello en el ejemplo siguiente se habilita extensión de diagnóstico de hello en hello máquina virtual denominada `myVMDeployed` en grupo de recursos de hello llamado `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas para conectarse tooyour VM, consulte [tooan de las conexiones RDP solucionar problemas de máquina virtual de Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para más información sobre el uso de Resource Manager, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
