---
title: "acceso de aaaReset sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión | Documentos de Microsoft"
description: "Restablecer el acceso en máquinas virtuales de Linux de Azure con hello VMAccess extensión."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Administrar usuarios, SSH y comprobación o los discos de reparación sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión con hello Azure CLI 1.0
Este artículo muestra cómo toouse hello Azure VMAcesss extensión toocheck o reparar un disco, restablecer el acceso de usuario, administrar cuentas de usuario o restablecer la configuración de SSHD hello en Linux. Hola artículo requiere:

* una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));
* Hola [CLI de Azure](../../cli-install-nodejs.md) inició sesión `azure login`.
* Hola CLI de Azure *debe estar en* modo Azure Resource Manager `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands)– nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="quick-commands"></a>Comandos rápidos
Hay dos maneras toouse VMAccess en las máquinas virtuales de Linux:

* Utilizar hello y hello Azure CLI 1.0 requiere parámetros.
* Con archivos JSON sin formato que procesa VMAccess para luego realizar acciones en ellos.

Para la sección del comando rápido de hello, vamos toouse hello Azure CLI 1.0 `azure vm reset-access` método. Hola siguientes ejemplos de comandos, reemplace los valores de hello que contienen "ejemplo" con valores de hello desde su propio entorno.

## <a name="create-a-resource-group-and-linux-vm"></a>Creación de un grupo de recursos y una VM Linux
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Creación de una máquina virtual Debian
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a>Restablecimiento de la contraseña raíz
contraseña de raíz de Hola tooreset:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>Restablecimiento de la clave SSH
clave SSH tooreset Hola de un usuario no es de raíz:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Creación de un usuario
toocreate un usuario:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Eliminación de un usuario
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>Restablecer SSHD
configuración de tooreset Hola SSHD:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Tutorial detallado
### <a name="vmaccess-defined"></a>VMAccess definido:
disco de Hello en la VM de Linux que muestra los errores. Algún modo restablecer la contraseña de la raíz de hello para la VM de Linux o había eliminado accidentalmente su clave privada SSH. Si esto sucede en días de hello del centro de datos de hello, ¿necesita toodrive existe y después abra Hola KVM tooget en consola de servidor de Hola. Considerar Hola extensión VMAccess de Azure como ese conmutador KVM que permite tooaccess Hola consola tooreset acceso tooLinux o realizar tareas de mantenimiento de nivel de disco.

Para hello detallada tutorial, vamos toouse hello no abreviada de VMAccess, que usa los archivos sin formato de JSON.  Estos archivos JSON de VMAccess también se pueden llamar desde las plantillas de Azure.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Usar disco de Hola de VMAccess toocheck o reparación de una VM de Linux
Uso de VMAccess puede hacer un fsck ejecutar en el disco de hello en la VM de Linux.  También puede hacer una comprobación y reparación de disco con VMAccess.

toocheck y, a continuación, disco de reparación de hello utilizar esta secuencia de comandos de VMAccess:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>Uso de VMAccess tooreset usuario acceso tooLinux
Si ha perdido acceso tooroot en la VM de Linux, puede iniciar una contraseña de la raíz de la secuencia de comandos tooreset VMAccess Hola.

contraseña de la raíz de tooreset hello, use este script VMAccess:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

clave SSH de hello tooreset de un usuario no es de raíz, use este script VMAccess:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Uso de cuentas de usuario de VMAccess toomanage en Linux
VMAccess es un script de Python que puede ser usuarios toomanage usado en la VM de Linux sin inicio de sesión y la cuenta raíz sudo o hello.

toocreate un usuario, use este script VMAccess:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete un usuario, use este script VMAccess:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>Uso de VMAccess tooreset Hola SSHD configuración
Si realiza la configuración de SSHD de máquinas virtuales de Linux de cambios toohello y conexión de SSH Hola cerrar antes de comprobar los cambios de hello, es podrán que no pueda SSH'ing en.  VMAccess puede ser usado tooreset Hola SSHD configuración tooa back-configuración válida conocida sin iniciar sesión mediante SSH.

configuración de tooreset Hola SSHD utilizar esta secuencia de comandos de VMAccess:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Pasos siguientes
La actualización de Linux con extensiones de VMAccess de Azure es un método toomake cambia en una VM de Linux de ejecución.  También puede usar herramientas como init de la nube y toomodify de plantillas de Azure la VM de Linux en el arranque.

[Acerca de las características y extensiones de las máquinas virtuales](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Uso de nube init toocustomize una VM de Linux durante la creación](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

