---
title: "Uso de Ansible para crear una máquina virtual compleja de Linux en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo usar Ansible para crear un entorno completo de máquina virtual Linux y administrarla en Azure."
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
ms.openlocfilehash: b2fcc288b40c12a9b3f966156ee2eedf4acca313
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="79b2d-103">Creación de un entorno completo de máquina virtual Linux en Azure con Ansible</span><span class="sxs-lookup"><span data-stu-id="79b2d-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="79b2d-104">Ansible permite automatizar la implementación y la configuración de recursos en un entorno.</span><span class="sxs-lookup"><span data-stu-id="79b2d-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="79b2d-105">Puede usar Ansible para administrar máquinas virtuales (VM) en Azure al igual que podría hacerlo con cualquier otro recurso.</span><span class="sxs-lookup"><span data-stu-id="79b2d-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="79b2d-106">En este artículo se muestra cómo crear un entorno completo de Linux y recursos de apoyo con Ansible.</span><span class="sxs-lookup"><span data-stu-id="79b2d-106">This article shows you how to create a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="79b2d-107">También puede obtener información sobre cómo [crear una VM básica con Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="79b2d-107">You can also learn how to [Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="79b2d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="79b2d-108">Prerequisites</span></span>
<span data-ttu-id="79b2d-109">Para administrar recursos de Azure con Ansible, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79b2d-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="79b2d-110">Los módulos de Ansible y SDK de Python de Azure instalados en el sistema de host.</span><span class="sxs-lookup"><span data-stu-id="79b2d-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="79b2d-111">Instale Ansible en [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) y [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).</span><span class="sxs-lookup"><span data-stu-id="79b2d-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="79b2d-112">Las credenciales de Azure y Ansible configurado para usarlas.</span><span class="sxs-lookup"><span data-stu-id="79b2d-112">Azure credentials, and Ansible configured to use them.</span></span>
    - <span data-ttu-id="79b2d-113">[Creación de credenciales de Azure y configuración de Ansible](ansible-install-configure.md#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="79b2d-113">[Create Azure credentials and configure Ansible](ansible-install-configure.md#create-azure-credentials)</span></span>
- <span data-ttu-id="79b2d-114">CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="79b2d-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="79b2d-115">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="79b2d-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="79b2d-116">Si necesita actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="79b2d-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="79b2d-117">También puede usar [Cloud Shell](/azure/cloud-shell/quickstart) desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="79b2d-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="79b2d-118">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="79b2d-118">Create virtual network</span></span>
<span data-ttu-id="79b2d-119">Con la siguiente sección de una guía de Ansible se crea una red virtual llamada *myVnet* en el espacio de direcciones *10.0.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="79b2d-119">The following section in an Ansible playbook creates a virtual network named *myVnet* in the *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="79b2d-120">Para agregar una subred, la siguiente sección crea una subred llamada *mySubnet* en la red virtual *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="79b2d-120">To add a subnet, the following section creates a subnet named *mySubnet* in the *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="79b2d-121">Creación de una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="79b2d-121">Create public IP address</span></span>
<span data-ttu-id="79b2d-122">Para acceder a recursos de Internet, cree una dirección IP pública y asígnela a la VM.</span><span class="sxs-lookup"><span data-stu-id="79b2d-122">To access resources across the Internet, create and assign a public IP address to your VM.</span></span> <span data-ttu-id="79b2d-123">Con la siguiente sección de una guía de Ansible se crea una dirección IP pública llamada *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="79b2d-123">The following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="79b2d-124">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="79b2d-124">Create Network Security Group</span></span>
<span data-ttu-id="79b2d-125">Los grupos de seguridad de red controlan el flujo del tráfico de red entrada y salida de la VM.</span><span class="sxs-lookup"><span data-stu-id="79b2d-125">Network Security Groups control the flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="79b2d-126">Con la siguiente sección de una guía de Ansible se crea un grupo de seguridad de red llamado *myNetworkSecurityGroup* y se define una regla para permitir el tráfico de SSH por el puerto TCP 22:</span><span class="sxs-lookup"><span data-stu-id="79b2d-126">The following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule to allow SSH traffic on TCP port 22:</span></span>

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


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="79b2d-127">Creación de una tarjeta de interfaz de red virtual</span><span class="sxs-lookup"><span data-stu-id="79b2d-127">Create virtual network interface card</span></span>
<span data-ttu-id="79b2d-128">Las tarjetas de interfaz de red (NIC) virtuales conectan la VM a una red virtual determinada, una dirección IP pública y un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="79b2d-128">A virtual network interface card (NIC) connects your VM to a given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="79b2d-129">Con la siguiente sección de una guía de Ansible se crea una NIC virtual llamada *myNIC* que se conecta a los recursos de red virtual que se hayan creado:</span><span class="sxs-lookup"><span data-stu-id="79b2d-129">The following section in an Ansible playbook creates a virtual NIC named *myNIC* connected to the virtual networking resources you have created:</span></span>

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


## <a name="create-virtual-machine"></a><span data-ttu-id="79b2d-130">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="79b2d-130">Create virtual machine</span></span>
<span data-ttu-id="79b2d-131">El último paso es crear una máquina virtual y usar todos los recursos creados.</span><span class="sxs-lookup"><span data-stu-id="79b2d-131">The final step is to create a VM and use all the resources created.</span></span> <span data-ttu-id="79b2d-132">Con la siguiente sección de una guía de Ansible se crea una VM llamada *myVM* y se adjunta la NIC virtual llamada *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="79b2d-132">The following section in an Ansible playbook creates a VM named *myVM* and attaches the virtual NIC named *myNIC*.</span></span> <span data-ttu-id="79b2d-133">Especifique los datos de su propia clave pública en el par *key_data* de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="79b2d-133">Enter your own public key data in the *key_data* pair as follows:</span></span>

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

## <a name="complete-ansible-playbook"></a><span data-ttu-id="79b2d-134">Guía de Ansible completa</span><span class="sxs-lookup"><span data-stu-id="79b2d-134">Complete Ansible playbook</span></span>
<span data-ttu-id="79b2d-135">Para unir todas estas secciones, cree una guía de Ansible llamada *azure_create_complete_vm.yml* y pegue el siguiente contenido:</span><span class="sxs-lookup"><span data-stu-id="79b2d-135">To bring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste the following contents:</span></span>

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

<span data-ttu-id="79b2d-136">Ansible necesita un grupo de recursos en el que implementar todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="79b2d-136">Ansible needs a resource group to deploy all your resources into.</span></span> <span data-ttu-id="79b2d-137">Cree un grupo de recursos con [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="79b2d-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="79b2d-138">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="79b2d-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="79b2d-139">Para crear el entorno de máquina virtual completo con Ansible, ejecute la guía de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="79b2d-139">To create the complete VM environment with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="79b2d-140">El resultado es similar al del siguiente ejemplo, en el que se muestra que la VM se ha creado correctamente:</span><span class="sxs-lookup"><span data-stu-id="79b2d-140">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="79b2d-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79b2d-141">Next steps</span></span>
<span data-ttu-id="79b2d-142">En este ejemplo se crea un entorno de VM completo, incluidos los recursos de red virtual necesarios.</span><span class="sxs-lookup"><span data-stu-id="79b2d-142">This example creates a complete VM environment including the required virtual networking resources.</span></span> <span data-ttu-id="79b2d-143">Para ver un ejemplo más directo de creación de una VM en recursos de red existentes con opciones predeterminadas, consulte [Creación de una VM](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="79b2d-143">For a more direct example to create a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>