---
title: aaaUse Ansible toocreate una VM de Linux completo en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Ansible toocreate y administrar un entorno de máquina virtual de Linux completo en Azure"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Creación de un entorno completo de máquina virtual Linux en Azure con Ansible
Ansible permite configurar e implementar de Hola de tooautomate de recursos en su entorno. Puede utilizar Ansible toomanage sus máquinas virtuales (VM) de Azure, Hola igual a como lo haría con cualquier otro recurso. Este artículo muestra cómo toocreate un entorno de Linux completo y compatibilidad con recursos con Ansible. También puede aprender cómo demasiado[crear una máquina virtual básica con Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Requisitos previos
toomanage Azure recursos con Ansible, necesita Hola siguientes:

- Ansible y Hola módulos de Azure Python SDK instalados en el sistema host.
    - Instale Ansible en [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) y [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).
- Las credenciales de Azure y Ansible configurado toouse ellos.
    - [Creación de credenciales de Azure y configuración de Ansible](ansible-install-configure.md#create-azure-credentials).
- CLI de Azure versión 2.0.4 o posterior. Ejecutar `az --version` toofind versión de Hola. 
    - Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). También puede usar [Cloud Shell](/azure/cloud-shell/quickstart) desde el explorador.


## <a name="create-virtual-network"></a>Creación de una red virtual
la sección siguiente en una guía Ansible Hello crea una red virtual con el nombre *myVnet* en hello *10.0.0.0/16* espacio de direcciones:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

Hola pasos de la sección de tooadd una subred, crea una subred denominada *mySubnet* en hello *myVnet* red virtual:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Creación de una dirección IP pública
recursos de tooaccess a través de Internet, Hola crear y asignar una tooyour de dirección IP virtual pública. la sección siguiente en una guía Ansible Hello crea una dirección IP pública denominada *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Creación de un grupo de seguridad de red
Flujo de Hola de tráfico de red dentro y fuera de la máquina virtual de control de grupos de seguridad de red. la sección siguiente en una guía Ansible Hello crea un grupo de seguridad de red con el nombre *myNetworkSecurityGroup* y define un tráfico SSH de tooallow de regla en el puerto TCP 22:

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a>Creación de una tarjeta de interfaz de red virtual
Una tarjeta de interfaz de red virtual (NIC) conecta a su tooa VM dada la red virtual, la dirección IP pública y el grupo de seguridad de red. la sección siguiente en una guía Ansible Hello crea una NIC virtual denominado *myNIC* conectado toohello los recursos de red virtual que ha creado:

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a>Create virtual machine
paso final Hello es toocreate una máquina virtual y usar todos los recursos de hello creados. la sección siguiente en una guía Ansible Hello crea una máquina virtual denominada *myVM* y adjuntará Hola NIC virtual denominado *myNIC*. Escriba sus propios datos de clave públicas en hello *key_data* emparejar como sigue:

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a>Guía de Ansible completa
toobring todas estas secciones juntos, crean una guía de Ansible denominado *azure_create_complete_vm.yml* y pegar Hola siguiente contenido:

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

Ansible necesita un toodeploy de grupo de recursos de todos los recursos en. Cree un grupo de recursos con [az group create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate Hola completo entorno de máquinas virtuales con Ansible, ejecute guía hello como sigue:

```bash
ansible-playbook azure_create_complete_vm.yml
```

salida de Hello tiene un aspecto similar toohello siguiente ejemplo que muestra hello que máquina virtual se creó correctamente:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a>Pasos siguientes
Este ejemplo crea un entorno de VM completo, incluidos los recursos de red virtual de hello necesario. Para un ejemplo más directa toocreate una máquina virtual en los recursos de red existentes con las opciones predeterminadas, vea [crear una máquina virtual](ansible-create-vm.md).
