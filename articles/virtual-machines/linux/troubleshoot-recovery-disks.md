---
title: "aaaUse una solución de problemas de VM con hello Azure CLI 2.0 de Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot VM de Linux que se emite por conexión Hola SO disco tooa recuperación VM mediante Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Solucionar problemas de una VM Linux adjuntando Hola SO disco tooa máquina virtual de recuperación con hello 2.0 de CLI de Azure
Si la máquina virtual (VM) de Linux se encuentra un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas. Un ejemplo común sería una entrada no válida en `/etc/fstab` que impide Hola VM pueda tooboot correctamente. Este artículo se detallan cómo toouse Hola CLI de Azure 2.0 tooconnect su virtual rígida tooanother toofix de VM de Linux en disco los errores, a continuación, volver a crea la máquina virtual original. También puede realizar estos pasos con hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="recovery-process-overview"></a>Introducción al proceso de recuperación
proceso de solución de problemas de Hello es como sigue:

1. Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.
2. Adjuntar y montar tooanother de disco duro virtual de hello VM de Linux para solucionar problemas.
3. Conectar toohello solución de problemas de máquina virtual. Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.
4. Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.
5. Crear una máquina virtual mediante hello: disco duro virtual original.

tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros con sus propios valores. Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.


## <a name="determine-boot-issues"></a>Determinación de los problemas de arranque
Examine Hola salida serie toodetermine ¿por qué la máquina virtual no es capaz de tooboot correctamente. Un ejemplo común es una entrada válida en `/etc/fstab`, u Hola subyacente de disco duro virtual que se va a eliminar o mover.

Obtener registros de arranque de hello con [diagnóstico de arranque de vm az get-arranque-log](/cli/azure/vm/boot-diagnostics#get-boot-log). Hello en el ejemplo siguiente se obtiene Hola serie resultado Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

Revise Hola salida serie toodetermine ¿por qué hello VM está fallando tooboot. Si salida serie hello no proporciona ninguna indicación, puede que tenga archivos de registro de tooreview en `/var/log` una vez que tenga Hola virtual disco duro conectado tooa solución de problemas de máquina virtual.


## <a name="view-existing-virtual-hard-disk-details"></a>Visualización de los detalles del disco duro virtual existente
Antes de que puede asociar la máquina virtual de tooanother de disco duro virtual (VHD), debe tooidentify Hola URI de disco del sistema operativo Hola. 

Vea información acerca de la máquina virtual con [az vm show](/cli/azure/vm#show). Hola de uso `--query` el disco toohello OS URI de marca tooextract Hola. Hello en el ejemplo siguiente se obtiene información de disco para la máquina virtual denominada hello `myVM` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

Hola URI es similar demasiado**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.

## <a name="delete-existing-vm"></a>Eliminación de la VM existente
Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure. Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones. Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC). Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual. Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual. concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.

Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio. Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento. Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.

Eliminar Hola VM con [eliminar vm az](/cli/azure/vm#delete). Después de eliminaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` del grupo de recursos de hello denominado `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual. concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Adjuntar tooanother de disco duro virtual existente
Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas. Adjuntar toothis Hola de disco duro virtual existente toobrowse VM de solución de problemas y editar el contenido del disco de Hola. Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo. Elija o cree otro toouse de máquina virtual para solucionar problemas.

Conectar disco duro virtual existente del Hola con [adjuntar az vm no administrada de disco](/cli/azure/vm/unmanaged-disk#attach). Cuando conecte un disco de duro virtual existente hello, especifique disco toohello Hola URI que obtuvo en hello anterior `az vm show` comando. Hello en el ejemplo siguiente se asocia un toohello de disco duro virtual existente solución de problemas de máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
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

2. Ahora separar Hola de disco duro virtual de VM de Hola. Salga de hello SSH sesión tooyour solución de problemas de máquina virtual. Hola lista adjunta datos discos tooyour solución de problemas de máquina virtual con [lista de discos no administrada de vm de az](/cli/azure/vm/unmanaged-disk#list). el ejemplo siguiente se enumeran Hola discos de datos Hello adjunta toohello máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    Anote el nombre de hello para el disco duro virtual existente. Por ejemplo, nombre de Hola de un disco con Hola URI de **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** es **myVHD**. 

    Desconectar el disco de datos de hello de la máquina virtual [separar az vm no administrada de disco](/cli/azure/vm/unmanaged-disk#detach). Hello en el ejemplo siguiente se separa con el nombre de disco de hello `myVHD` de máquina virtual denominada hello `myVMRecovery` en hello `myResourceGroup` grupo de recursos:

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>Creación de máquina virtual a partir del disco duro original
usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). plantilla JSON real de Hello está en hello siguiente vínculo:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

plantilla Hello implementa una máquina virtual mediante Hola URI de VHD de hello comando anteriormente. Implementar la plantilla de hello con [Crear implementación de grupo az](/cli/azure/group/deployment#create). Proporcionar Hola URI tooyour VHD original y, a continuación, especifique Hola SO tipo, tamaño de máquina virtual y nombre de máquina virtual como se indica a continuación:

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>Rehabilitación de los diagnósticos de arranque
Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente. Habilite el diagnóstico de arranque con [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable). Hello en el ejemplo siguiente se habilita extensión de diagnóstico de hello en hello máquina virtual denominada `myDeployedVM` en grupo de recursos de hello llamado `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas para conectarse tooyour VM, consulte [solucionar problemas de SSH conexiones tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual de Linux en Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
