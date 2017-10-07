---
title: "aaaUsing init de la nube toocustomize una VM Linux durante la creación de Azure | Documentos de Microsoft"
description: "¿Cómo toouse init de la nube toocustomize una VM de Linux durante la creación con Hola 1.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a>Usar en la nube init toocustomize una VM Linux durante la creación con hello Azure CLI 1.0
Este artículo muestra cómo toomake una tooset de secuencia de comandos en la nube init Hola hostname, actualizar los paquetes instalados y administrar cuentas de usuario.  secuencias de comandos de Hello init de la nube se llaman durante la creación de VM de Azure CLI Hola.  Hola artículo requiere:

* una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));
* Hola [CLI de Azure](../../cli-install-nodejs.md) inició sesión `azure login`.
* Hola CLI de Azure *debe estar en* modo Azure Resource Manager `azure config mode arm`.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="quick-commands"></a>Comandos rápidos
Crear una secuencia de comandos de init.txt en la nube que establece el nombre de host de hello, actualiza todos los paquetes y se agrega un tooLinux de usuario de sudo.

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
Crear un toolaunch de grupo de recursos de las máquinas virtuales en.

```azurecli
azure group create myResourceGroup westus
```

Crear una VM de Linux con tooconfigure init de la nube durante el arranque.

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Tutorial detallado
### <a name="introduction"></a>Introducción
Cuando inicia una nueva VM de Linux, obtiene una VM Linux estándar con nada personalizado o preparada para sus necesidades. [En la nube init](https://cloudinit.readthedocs.org) es una manera estándar tooinject una secuencia de comandos u opciones de configuración en esa VM de Linux tal y como se está iniciando en hello primera vez.

En Azure, hay un tres maneras diferentes toomake cambios en una VM Linux cuando se implementa o arrancar.

* Inserte scripts con cloud-init.
* Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Una plantilla de Azure con cloud-init.
* Una plantilla de Azure con [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

secuencias de comandos de tooinject en cualquier momento tras el arranque:

* SSH toorun directamente comandos
* Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ya sea de manera imperativa o en una plantilla de Azure
* Herramientas de administración de la configuración, como Ansible, Salt, Chef y Puppet.

> [!NOTE]
> : La extensión VMAccess ejecuta una secuencia de comandos como raíz en hello mismo utilizando SSH puede.  Sin embargo, utilizando la extensión de máquina virtual de hello habilita varias características que ofrece Azure que puede ser útiles en función de su escenario.
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Disponibilidad de cloud-init en los alias de imagen de creación rápida de VM de Azure:
| Alias | Publicador | Oferta | SKU | Versión | Cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |CentOS |7,2 |más reciente |no |
| CoreOS |CoreOS |CoreOS |Stable |más reciente |yes |
| Debian |credativ |Debian |8 |más reciente |no |
| openSUSE |SUSE |openSUSE |13.2 |más reciente |no |
| RHEL |Redhat |RHEL |7,2 |más reciente |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |más reciente |yes |

Microsoft está trabajando con nuestro socios tooget nube-init incluida y estamos trabajando en las imágenes de Hola que proporcionan tooAzure.

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Agregar una creación de VM de nube init script toohello con hello CLI de Azure
toolaunch una secuencia de comandos en la nube init al crear una máquina virtual en Azure, especifique el archivo de init de la nube de hello mediante hello Azure CLI `--custom-data` cambiar.

Crear un toolaunch de grupo de recursos de las máquinas virtuales en.

```azurecli
azure group create myResourceGroup westus
```

Crear una VM de Linux con tooconfigure init de la nube durante el arranque.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Crear un nombre de host de nube init script tooset Hola de una VM de Linux
Uno de hello más sencilla y la configuración más importante para las VM de Linux sería el nombre de host de Hola. Podemos establecer esto fácilmente mediante cloud-init con este script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Script de cloud-init de ejemplo denominado `cloud_config_hostname.txt`.
```sh
#cloud-config
hostname: myservername
```

Durante el inicio de Hola de hello VM, esta secuencia de comandos en la nube init establece Hola hostname demasiado`myservername`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

Inicio de sesión y comprobar el nombre de host de Hola de hello nueva máquina virtual.

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a>Crear un tooupdate de secuencia de comandos en la nube init Linux
Para la seguridad, desea que su tooupdate Ubuntu VM en el primer inicio de Hola.  Mediante init en la nube que podemos hacer con hello siga script, en función de distribución de Linux de Hola que usa.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Secuencia de comandos de ejemplo en la nube init `cloud_config_apt_upgrade.txt` para hello Debian familia
```sh
#cloud-config
apt_upgrade: true
```

Una vez que ha arrancado Linux, se actualizan todos los paquetes de saludo instalado a través de `apt-get`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

Inicie sesión y compruebe que todos los paquetes se han actualizado.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a>Crear un tooadd de secuencia de comandos en la nube de inicializar un tooLinux de usuario
Una de las primeras tareas de Hola en cualquier nueva VM de Linux es un usuario para usted mismo o usar tooavoid tooadd `root`. Claves de SSH son una práctica recomendada para la seguridad y facilidad de uso y se agregan toohello `~/.ssh/authorized_keys` archivo con este script init de la nube.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Script de cloud-init de ejemplo `cloud_config_add_users.txt` para la familia Debian
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Una vez que ha arrancado Linux, todos los usuarios de hello enumerado son toohello creado y agregado sudo grupo.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

Inicio de sesión y comprobar el usuario Hola recién creado.

```bash
ssh myVM
cat /etc/group
```

Salida

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Pasos siguientes
Init de la nube se está convirtiendo en una toomodify de manera estándar la VM de Linux en el arranque. Azure también tiene extensiones de máquina virtual, lo que permitirá toomodify su LinuxVM en el arranque o mientras se está ejecutando. Por ejemplo, puede usar hello Azure VMAccessExtension tooreset SSH o información de usuario mientras se está ejecutando Hola máquina virtual. Con init de la nube, necesitará una contraseña de hello tooreset de reinicio.

[Acerca de las características y extensiones de las máquinas virtuales](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

