---
title: "aaaUse Ansible toocreate una VM de Linux básico de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Ansible toocreate y administrar una máquina virtual de Linux básica de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Creación de una máquina virtual básica en Azure con Ansible
Ansible permite configurar e implementar de Hola de tooautomate de recursos en su entorno. Puede utilizar Ansible toomanage sus máquinas virtuales (VM) de Azure, Hola igual a como lo haría con cualquier otro recurso. Este artículo muestra cómo toocreate una máquina virtual básica con Ansible. También puede aprender cómo demasiado[crear un entorno de máquina virtual completando con Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Requisitos previos
toomanage Azure recursos con Ansible, necesita Hola siguientes:

- Ansible y Hola módulos de Azure Python SDK instalados en el sistema host.
    - Instale Ansible en [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) y [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).
- Las credenciales de Azure y Ansible configurado toouse ellos.
    - [Creación de credenciales de Azure y configuración de Ansible](ansible-install-configure.md#create-azure-credentials).
- CLI de Azure versión 2.0.4 o posterior. Ejecutar `az --version` toofind versión de Hola. 
    - Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). También puede usar [Cloud Shell](/azure/cloud-shell/quickstart) desde el explorador.


## <a name="create-supporting-azure-resources"></a>Creación de recursos de Azure de apoyo
En este ejemplo crearemos un runbook que implementa una máquina virtual en una infraestructura existente. En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

Cree una red virtual para la VM con [az network vnet create](/cli/azure/network/vnet#create). Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* y una subred denominada *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Creación y ejecución de guía de Ansible
Crear una guía de Ansible denominado **azure_create_vm.yml** y pegar Hola siguiendo el contenido. En este ejemplo se crea una única VM y se configuran las credenciales de Secure Shell. Escriba sus propios datos de clave públicas en hello *key_data* emparejar como sigue:

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

Hola toocreate VM con Ansible, ejecute guía hello como sigue:

```bash
ansible-playbook azure_create_vm.yml
```

salida de Hello tiene un aspecto similar toohello siguiente ejemplo que muestra hello que máquina virtual se creó correctamente:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Pasos siguientes
En este ejemplo se crea una VM en un grupo de recursos existente con una red virtual ya implementada. Para obtener un ejemplo más detallado sobre cómo toouse Ansible toocreate auxiliares recursos como una red virtual y las reglas del grupo de seguridad de red, consulte [crear un entorno de máquina virtual completando con Ansible](ansible-create-complete-vm.md).
