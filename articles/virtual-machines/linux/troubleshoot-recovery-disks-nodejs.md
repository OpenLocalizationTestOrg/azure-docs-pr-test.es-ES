---
title: "aaaUse una solución de problemas de VM con hello Azure CLI 1.0 de Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot VM de Linux que se emite por conexión Hola SO disco tooa recuperación VM mediante Hola 1.0 de CLI de Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>Solucionar problemas de una VM de Linux mediante la asociación de la máquina virtual de recuperación de tooa del disco de hello SO utilizando Hola 1.0 de CLI de Azure
Si la máquina virtual (VM) de Linux se encuentra un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas. Un ejemplo común sería una entrada no válida en `/etc/fstab` que impide Hola VM pueda tooboot correctamente. Este artículo se detallan cómo toouse hello Azure CLI 1.0 tooconnect su virtual rígida tooanother toofix de VM de Linux en disco los errores, a continuación, volver a crea la máquina virtual original.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#recovery-process-overview) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="recovery-process-overview"></a>Introducción al proceso de recuperación
proceso de solución de problemas de Hello es como sigue:

1. Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.
2. Adjuntar y montar tooanother de disco duro virtual de hello VM de Linux para solucionar problemas.
3. Conectar toohello solución de problemas de máquina virtual. Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.
4. Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.
5. Crear una máquina virtual mediante hello: disco duro virtual original.

Asegúrese de que dispone de [Hola 1.0 de CLI de Azure más reciente](../../cli-install-nodejs.md) instalado y registrado en y lo utiliza el modo de administrador de recursos:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros con sus propios valores. Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.


## <a name="determine-boot-issues"></a>Determinación de los problemas de arranque
Examine Hola salida serie toodetermine ¿por qué la máquina virtual no es capaz de tooboot correctamente. Un ejemplo común es una entrada válida en `/etc/fstab`, u Hola subyacente de disco duro virtual que se va a eliminar o mover.

Hello en el ejemplo siguiente se obtiene Hola serie resultado Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

Revise Hola salida serie toodetermine ¿por qué hello VM está fallando tooboot. Si salida serie hello no proporciona ninguna indicación, puede que tenga archivos de registro de tooreview en `/var/log` una vez que tenga Hola virtual disco duro conectado tooa solución de problemas de máquina virtual.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualización de los detalles del disco duro virtual existente
Para poder adjuntar su tooanother de disco duro virtual, necesita tooidentify Hola nombre de disco duro virtual (VHD) de Hola. 

Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

Busque `Vhd URI` en la salida de hello de hello anterior comando. siguiente salida de ejemplo truncados Hello muestra hello `Vhd URI` en la última línea de hello:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>Eliminación de la VM existente
Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure. Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones. Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC). Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual. Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual. concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.

Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio. Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento. Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.

Después de eliminaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` del grupo de recursos de hello denominado `myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual. concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Adjuntar tooanother de disco duro virtual existente
Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas. Adjuntar toothis Hola de disco duro virtual existente toobrowse VM de solución de problemas y editar el contenido del disco de Hola. Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo. Elija o cree otro toouse de máquina virtual para solucionar problemas.

Al adjuntar hello: disco duro virtual existente, especifique el disco de toohello de dirección URL de hello obtenido en hello anterior `azure vm show` comando. Hello en el ejemplo siguiente se asocia un toohello de disco duro virtual existente solución de problemas de máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Montar el disco de datos adjuntos de Hola

> [!NOTE]
> Hello en los ejemplos siguientes detallan los pasos de hello necesarios en una VM Ubuntu. Si usas una distribución de Linux diferentes, por ejemplo, Red Hat Enterprise Linux o SUSE, ubicaciones de archivos de registro de hello y `mount` comandos pueden ser ligeramente diferentes. Consulte la documentación de toohello para su distribución específica para los cambios adecuados de hello en comandos.

1. SSH tooyour de solución de problemas de máquina virtual con las credenciales adecuadas de Hola. Si este disco es Hola primera datos disco conectado tooyour solución de problemas de máquina virtual, es probable que está conectado a disco Hola demasiado`/dev/sdc`. Use `dmseg` tooview discos conectados:

    ```bash
    dmesg | grep SCSI
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    En el anterior ejemplo de Hola, disco de hello SO está en `/dev/sda` y proporcionadas para cada máquina virtual está en el disco temporal hello `/dev/sdb`. Si hubiera varios discos de datos, deben estar en `/dev/sdd`, `/dev/sde`, y así sucesivamente.

2. Cree un directorio toomount el disco duro virtual existente. Hello en el ejemplo siguiente se crea un directorio denominado `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Si tiene varias particiones en el disco duro virtual existente, monte partición Hola necesario. Hello en el ejemplo siguiente se monta primera partición primaria hello en `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Procedimiento recomendado es toomount discos de datos en máquinas virtuales en Azure mediante Hola identificador único universal (UUID) de disco duro virtual de Hola. En este escenario de solución de problemas corto, el montaje Hola disco duro con hello UUID no es necesario. Sin embargo, en condiciones normales, edición `/etc/fstab` discos duros virtuales toomount mediante el nombre de dispositivo en lugar de UUID puede provocar Hola VM toofail tooboot.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Solución de problemas en el disco duro virtual original
Con hello disco duro virtual existente montado, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario. Una vez que se ha solucionado problemas hello, continúe con hello pasos.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmontaje y desconexión del disco duro virtual original
Una vez que se resuelven los errores, desmonta y separar hello: disco duro virtual existente de la máquina virtual para solucionar problemas. No se puede usar el disco duro virtual con cualquier otra máquina virtual hasta que se libera la concesión de hello adjuntar toohello de disco duro virtual de hello VM de solución de problemas.

1. De tooyour de sesión SSH de hello VM de solución de problemas, desmonte hello: disco duro virtual existente. Cambie primero fuera del directorio principal de hello para el punto de montaje:

    ```bash
    cd /
    ```

    Desmonte ahora hello: disco duro virtual existente. Hello en el ejemplo siguiente se desmonta dispositivo hello en `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Ahora separar Hola de disco duro virtual de VM de Hola. Salga de hello SSH sesión tooyour solución de problemas de máquina virtual. Hola CLI de Azure, primer Hola lista adjunta tooyour de discos de datos VM de solución de problemas. el ejemplo siguiente se enumeran Hola discos de datos Hello adjunta toohello máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    Hola Nota `Lun` valor para el disco duro virtual existente. Hello resultado del comando de ejemplo siguiente muestra hello disco virtual conectado en el LUN 0:

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    Desconectar el disco de datos de hello de la máquina virtual con hello aplicable `Lun` valor:

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>Creación de máquina virtual a partir del disco duro original
usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). plantilla JSON real de Hello está en hello siguiente vínculo:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

plantilla de Hello implementa una máquina virtual en una red virtual existente, mediante Hola dirección URL del VHD de hello comando anteriormente. Hello en el ejemplo siguiente se implementa grupo de recursos de toohello Hola plantilla llamado `myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

Hola de respuesta solicita plantilla hello como nombre de máquina virtual (`myDeployedVM` Hola después ejemplo), tipo de sistema operativo (`Linux`) y el tamaño VM (`Standard_DS1_v2`). Hola `osDiskVhdUri` es Hola mismo utiliza anteriormente al adjuntar toohello Hola de disco duro virtual existente VM de solución de problemas. Un ejemplo de salida del comando hello y preguntar si se es como sigue:

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>Rehabilitación de los diagnósticos de arranque

Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente. Hello en el ejemplo siguiente se habilita extensión de diagnóstico de hello en hello máquina virtual denominada `myDeployedVM` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas para conectarse tooyour VM, consulte [solucionar problemas de SSH conexiones tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual de Linux en Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
