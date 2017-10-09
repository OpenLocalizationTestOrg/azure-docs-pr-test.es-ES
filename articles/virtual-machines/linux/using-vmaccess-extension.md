---
title: aaaReset acceso tooan VM de Linux de Azure | Documentos de Microsoft
description: "Cómo toomanage a los usuarios acceso de restablecimiento sobre el uso de máquinas virtuales de Linux Hola la VMAccess extensión y Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Administrar usuarios, SSH y comprobación o los discos de reparación sobre el uso de máquinas virtuales de Linux Hola VMAccess extensión con hello 2.0 de CLI de Azure
disco de Hello en la VM de Linux que muestra los errores. Algún modo restablecer la contraseña de la raíz de hello para la VM de Linux o había eliminado accidentalmente su clave privada SSH. Si esto sucede en días de hello del centro de datos de hello, ¿necesita toodrive existe y después abra Hola KVM tooget en consola de servidor de Hola. Considerar Hola extensión VMAccess de Azure como ese conmutador KVM que permite tooaccess Hola consola tooreset acceso tooLinux o realizar tareas de mantenimiento de nivel de disco.

Este artículo muestra cómo toouse Hola toocheck de Azure de la VMAccess extensión o reparar un disco, restablecer el acceso de usuario, administrar cuentas de usuario o restablecer la configuración de SSH de hello en Linux. También puede realizar estos pasos con hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Formas toouse Hola VMAccess extensión
Hay dos formas en que puede utilizar Hola VMAccess extensión en las máquinas virtuales de Linux:

* Utilizar Hola 2.0 de CLI de Azure y los parámetros de hello necesario.
* [Archivos de uso sin formato JSON ese proceso de VMAccess extensión hello](#use-json-files-and-the-vmaccess-extension) y, a continuación, actuar en.

Hola a consecuencia del uso de ejemplos [usuario de vm az](/cli/azure/vm/user) comandos. tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

## <a name="reset-ssh-key"></a>Restablecimiento de la clave SSH
Hello en el ejemplo siguiente se restablece la clave SSH hello para el usuario de hello `azureuser` en hello máquina virtual denominada `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Restablecimiento de contraseña
Hello en el ejemplo siguiente se restablece la Hola contraseña de usuario de hello `azureuser` en hello máquina virtual denominada `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>Reinicio de SSH
Hello en el ejemplo siguiente se reinicia el demonio SSH de Hola y restablece Hola toodefault valores de configuración de SSH en una máquina virtual denominada `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Creación de un usuario
Hello en el ejemplo siguiente se crea un usuario denominado `myNewUser` con una clave SSH para la autenticación en la máquina virtual denominada Hola `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Eliminar un usuario
Hello en el ejemplo siguiente se elimina un usuario denominado `myNewUser` en hello máquina virtual denominada `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>Usar archivos JSON y Hola VMAccess extensión
Hello en los ejemplos siguientes use archivos sin formato de JSON. Use [conjunto de extensión de vm az](/cli/azure/vm/extension#set) toothen llamar a los archivos JSON. Estos archivos JSON también se pueden llamar desde las plantillas de Azure. 

### <a name="reset-user-access"></a>Restablecimiento del acceso de un usuario
Si ha perdido acceso tooroot en la VM de Linux, puede iniciar un tooreset de secuencia de comandos de VMAccess clave SSH o la contraseña de un usuario.

clave pública SSH de tooreset Hola de un usuario, cree un archivo denominado `reset_ssh_key.json` y agregar valores de hello siguiendo el formato. Sustituya los valores propios para hello `username` y `ssh_key` parámetros:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset una contraseña de usuario, cree un archivo denominado `reset_user_password.json` y agregar valores de hello siguiendo el formato. Sustituya los valores propios para hello `username` y `password` parámetros:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>Reinicio de SSH
toorestart Hola demonio de SSH y restablezca los valores de toodefault de configuración de SSH de hello, cree un archivo denominado `reset_sshd.json`. Agregue Hola siguen contenido:

```json
{
  "reset_ssh": true
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Administrar usuarios

toocreate un usuario que utiliza una clave SSH para la autenticación, cree un archivo denominado `create_new_user.json` y agregar valores de hello siguiendo el formato. Sustituya los valores propios para hello `username` y `ssh_key` parámetros:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete un usuario, cree un archivo denominado `delete_user.json` y agregue Hola siguen contenido. Sustituya su propio valor para hello `remove_user` parámetro:

```json
{
  "remove_user":"myNewUser"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Comprobar o reparar el disco de Hola
Uso de VMAccess también puede comprobar y reparar un disco que ha agregado toohello VM de Linux.

toocheck y, a continuación, disco de reparación de hello, cree un archivo denominado `disk_check_repair.json` y agregar valores de hello siguiendo el formato. Sustituya su propio valor para el nombre de Hola de `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Ejecute la secuencia de comandos de hello VMAccess con:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Pasos siguientes
La actualización de Linux utilizando Hola VMAccess extensión de Azure es un método toomake cambia en una VM de Linux de ejecución. También puede usar herramientas como init de la nube y toomodify de plantillas de Azure Resource Manager la VM de Linux en el arranque.

[Características y extensiones de las máquinas virtuales para Linux](extensions-features.md)

[Creación de plantillas de Azure Resource Manager con extensiones de máquina virtual de Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Uso de nube init toocustomize una VM de Linux durante la creación](using-cloud-init.md)

