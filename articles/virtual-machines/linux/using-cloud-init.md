---
title: aaaUse init de la nube toocustomize una VM de Linux | Documentos de Microsoft
description: "¿Cómo toouse init de la nube toocustomize una VM de Linux durante la creación con Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>Usar en la nube init toocustomize una VM Linux durante la creación
Este artículo muestra cómo toomake una tooset de secuencia de comandos en la nube init Hola hostname, actualizar paquetes instalados y administrar cuentas de usuario con hello 2.0 de CLI de Azure. secuencias de comandos de Hello init de la nube se llama cuando se crea una máquina virtual (VM) de CLI de Azure. Para obtener información más detallada acerca de la instalación de aplicaciones, la escritura de archivos de configuración y la inserción de claves desde Key Vault, consulte [este tutorial](tutorial-automate-vm-deployment.md). También puede realizar estos pasos con hello [Azure CLI 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Comandos rápidos
Crear una secuencia de comandos de init.txt en la nube que establece el nombre de host de hello, actualiza todos los paquetes y se agrega un tooLinux de usuario de sudo.

```yaml
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

Crear un toolaunch de grupo de recursos de las máquinas virtuales en con [crear grupo az](/cli/azure/group#create). Hello en el ejemplo siguiente se crea grupo de recursos de hello llamado *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque con hello `--custom-data` parámetro.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Tutorial detallado
Cuando inicia una nueva VM de Linux, obtiene una VM Linux estándar con nada personalizado o preparada para sus necesidades. [En la nube init](https://cloudinit.readthedocs.org) es una manera estándar tooinject una secuencia de comandos u opciones de configuración en esa VM de Linux tal y como se está iniciando en hello primera vez.

En Azure, hay varias maneras diferentes toomake cambios en una VM Linux cuando se implementa o arrancar.

* Inserte scripts con cloud-init.
* Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md).
* Una plantilla de Azure con cloud-init.
* Una plantilla de Azure con [CustomScriptExtention](extensions-customscript.md).

secuencias de comandos de tooinject en cualquier momento tras el arranque:

* SSH toorun directamente comandos
* Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md), ya sea de manera imperativa o en una plantilla de Azure
* Herramientas de administración de la configuración, como Ansible, Salt, Chef y Puppet.

> [!NOTE]
> La VMAccess extensión ejecuta una secuencia de comandos como raíz en hello mismo utilizando SSH puede. Sin embargo, utilizando la extensión de máquina virtual de hello habilita varias características que ofrece Azure que puede ser útiles en función de su escenario.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Disponibilidad de cloud-init en los alias de imagen de creación rápida de VM de Azure:
| Alias | Publicador | Oferta | SKU | Versión | Cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |CentOS |7,2 |más reciente |no |
| CoreOS |CoreOS |CoreOS |Stable |más reciente |yes |
| Debian |credativ |Debian |8 |más reciente |no |
| openSUSE |SUSE |openSUSE |13.2 |más reciente |no |
| RHEL |Redhat |RHEL |7,2 |más reciente |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |más reciente |yes |

Estamos trabajando con nuestro socios tooget nube-init incluida y estamos trabajando en las imágenes de Hola que proporcionan tooAzure.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Agregar una creación de VM de nube init script toohello con hello CLI de Azure
toolaunch una secuencia de comandos en la nube init al crear una máquina virtual en Azure, especifique el archivo de init de la nube de hello mediante hello Azure CLI `--custom-data` cambiar.

Crear un toolaunch de grupo de recursos de las máquinas virtuales en con [crear grupo az](/cli/azure/group#create). Hello en el ejemplo siguiente se crea grupo de recursos de hello llamado *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Crear un nombre de host de nube init script tooset Hola de una VM de Linux
Uno de hello más sencilla y la configuración más importante para las VM de Linux sería el nombre de host de Hola. Podemos establecer esto fácilmente mediante cloud-init con este script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Script de cloud-init de ejemplo denominado `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Durante el inicio de Hola de hello VM, esta secuencia de comandos en la nube init establece Hola hostname demasiado*myservername*. Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Inicio de sesión y comprobar el nombre de host de Hola de hello nueva máquina virtual.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Creación de un script de cloud-init
Para la seguridad, desea que su tooupdate Ubuntu VM en el primer inicio de Hola. Mediante init en la nube que podemos hacer con hello siga script, en función de distribución de Linux de Hola que usa.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Secuencia de comandos de ejemplo en la nube init `cloud_config_apt_upgrade.txt` para hello Debian familia
```yaml
#cloud-config
apt_upgrade: true
```

Una vez que ha arrancado Linux, se actualizan todos los paquetes de saludo instalado a través de **apt get**. Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>Crear un tooadd de secuencia de comandos en la nube de inicializar un tooLinux de usuario
Una de las primeras tareas de Hola en cualquier nueva VM de Linux es un usuario para usted mismo o usar tooavoid tooadd *raíz*. Claves de SSH son una práctica recomendada para la seguridad y facilidad de uso y se agregan toohello *~/.ssh/authorized_keys* archivo con este script init de la nube.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Script de cloud-init de ejemplo `cloud_config_add_users.txt` para la familia Debian
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Una vez que ha arrancado Linux, todos los usuarios de hello enumerado son toohello creado y agregado sudo grupo. Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
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

[Acerca de las características y extensiones de las máquinas virtuales](extensions-features.md)

[Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión](using-vmaccess-extension.md)
