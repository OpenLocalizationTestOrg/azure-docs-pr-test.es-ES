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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="07984-103">Creación de una máquina virtual básica en Azure con Ansible</span><span class="sxs-lookup"><span data-stu-id="07984-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="07984-104">Ansible permite configurar e implementar de Hola de tooautomate de recursos en su entorno.</span><span class="sxs-lookup"><span data-stu-id="07984-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="07984-105">Puede utilizar Ansible toomanage sus máquinas virtuales (VM) de Azure, Hola igual a como lo haría con cualquier otro recurso.</span><span class="sxs-lookup"><span data-stu-id="07984-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="07984-106">Este artículo muestra cómo toocreate una máquina virtual básica con Ansible.</span><span class="sxs-lookup"><span data-stu-id="07984-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="07984-107">También puede aprender cómo demasiado[crear un entorno de máquina virtual completando con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="07984-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="07984-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="07984-108">Prerequisites</span></span>
<span data-ttu-id="07984-109">toomanage Azure recursos con Ansible, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="07984-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="07984-110">Ansible y Hola módulos de Azure Python SDK instalados en el sistema host.</span><span class="sxs-lookup"><span data-stu-id="07984-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="07984-111">Instale Ansible en [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) y [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).</span><span class="sxs-lookup"><span data-stu-id="07984-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="07984-112">Las credenciales de Azure y Ansible configurado toouse ellos.</span><span class="sxs-lookup"><span data-stu-id="07984-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - <span data-ttu-id="07984-113">[Creación de credenciales de Azure y configuración de Ansible](ansible-install-configure.md#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="07984-113">[Create Azure credentials and configure Ansible](ansible-install-configure.md#create-azure-credentials)</span></span>
- <span data-ttu-id="07984-114">CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="07984-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="07984-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="07984-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="07984-116">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="07984-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="07984-117">También puede usar [Cloud Shell](/azure/cloud-shell/quickstart) desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="07984-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="07984-118">Creación de recursos de Azure de apoyo</span><span class="sxs-lookup"><span data-stu-id="07984-118">Create supporting Azure resources</span></span>
<span data-ttu-id="07984-119">En este ejemplo crearemos un runbook que implementa una máquina virtual en una infraestructura existente.</span><span class="sxs-lookup"><span data-stu-id="07984-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="07984-120">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="07984-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="07984-121">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="07984-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="07984-122">Cree una red virtual para la VM con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="07984-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="07984-123">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* y una subred denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="07984-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="07984-124">Creación y ejecución de guía de Ansible</span><span class="sxs-lookup"><span data-stu-id="07984-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="07984-125">Crear una guía de Ansible denominado **azure_create_vm.yml** y pegar Hola siguiendo el contenido.</span><span class="sxs-lookup"><span data-stu-id="07984-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="07984-126">En este ejemplo se crea una única VM y se configuran las credenciales de Secure Shell.</span><span class="sxs-lookup"><span data-stu-id="07984-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="07984-127">Escriba sus propios datos de clave públicas en hello *key_data* emparejar como sigue:</span><span class="sxs-lookup"><span data-stu-id="07984-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

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

<span data-ttu-id="07984-128">Hola toocreate VM con Ansible, ejecute guía hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="07984-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="07984-129">salida de Hello tiene un aspecto similar toohello siguiente ejemplo que muestra hello que máquina virtual se creó correctamente:</span><span class="sxs-lookup"><span data-stu-id="07984-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="07984-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07984-130">Next steps</span></span>
<span data-ttu-id="07984-131">En este ejemplo se crea una VM en un grupo de recursos existente con una red virtual ya implementada.</span><span class="sxs-lookup"><span data-stu-id="07984-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="07984-132">Para obtener un ejemplo más detallado sobre cómo toouse Ansible toocreate auxiliares recursos como una red virtual y las reglas del grupo de seguridad de red, consulte [crear un entorno de máquina virtual completando con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="07984-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
