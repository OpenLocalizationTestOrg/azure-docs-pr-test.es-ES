---
title: "aaaInstall y configurar Ansible para su uso con máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall y configurar Ansible para administrar recursos de Azure en Ubuntu, CentOS y SLES"
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
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="fc52f-103">Instalar y configurar máquinas virtuales de Ansible toomanage en Azure</span><span class="sxs-lookup"><span data-stu-id="fc52f-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="fc52f-104">Este artículo detalla cómo tooinstall Ansible y módulos de Azure SDK de Python necesarios para algunos de Hola distribuciones de Linux más comunes.</span><span class="sxs-lookup"><span data-stu-id="fc52f-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="fc52f-105">Puede instalar Ansible en otras distribuciones ajustando Hola instalado paquetes toofit su plataforma concreta.</span><span class="sxs-lookup"><span data-stu-id="fc52f-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="fc52f-106">toocreate Azure recursos de forma segura, también aprenderá cómo toocreate y definir credenciales para Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="fc52f-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="fc52f-107">Para obtener más opciones de instalación y los pasos para plataformas adicionales, vea hello [Guía de instalación de Ansible](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="fc52f-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="fc52f-108">Instalación de Ansible</span><span class="sxs-lookup"><span data-stu-id="fc52f-108">Install Ansible</span></span>
<span data-ttu-id="fc52f-109">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fc52f-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fc52f-110">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAnsible* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="fc52f-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="fc52f-111">Ahora cree una máquina virtual e instale Ansible para uno de hello siguientes distribuciones:</span><span class="sxs-lookup"><span data-stu-id="fc52f-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="fc52f-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="fc52f-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="fc52f-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="fc52f-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="fc52f-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="fc52f-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="fc52f-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="fc52f-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="fc52f-116">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fc52f-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fc52f-117">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="fc52f-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fc52f-118">SSH tooyour VM con Hola `publicIpAddress` anotó en hello operación de creación de la salida de hello VM:</span><span class="sxs-lookup"><span data-stu-id="fc52f-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="fc52f-119">En la máquina virtual, instalar paquetes de hello necesario para módulos de Azure SDK de Python de Hola y Ansible como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fc52f-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="fc52f-120">Ahora pasamos demasiado[las credenciales de Azure crear](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="fc52f-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="fc52f-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="fc52f-121">CentOS 7.3</span></span>
<span data-ttu-id="fc52f-122">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fc52f-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fc52f-123">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="fc52f-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fc52f-124">SSH tooyour VM con Hola `publicIpAddress` anotó en hello operación de creación de la salida de hello VM:</span><span class="sxs-lookup"><span data-stu-id="fc52f-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="fc52f-125">En la máquina virtual, instalar paquetes de hello necesario para módulos de Azure SDK de Python de Hola y Ansible como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fc52f-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="fc52f-126">Ahora pasamos demasiado[las credenciales de Azure crear](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="fc52f-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="fc52f-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="fc52f-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="fc52f-128">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fc52f-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fc52f-129">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="fc52f-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fc52f-130">SSH tooyour VM con Hola `publicIpAddress` anotó en hello operación de creación de la salida de hello VM:</span><span class="sxs-lookup"><span data-stu-id="fc52f-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="fc52f-131">En la máquina virtual, instalar paquetes de hello necesario para módulos de Azure SDK de Python de Hola y Ansible como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fc52f-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="fc52f-132">Ahora pasamos demasiado[las credenciales de Azure crear](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="fc52f-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="fc52f-133">Creación de credenciales de Azure</span><span class="sxs-lookup"><span data-stu-id="fc52f-133">Create Azure credentials</span></span>
<span data-ttu-id="fc52f-134">Ansible se comunica con Azure mediante un nombre de usuario y una contraseña, o a través de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="fc52f-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="fc52f-135">Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como Ansible.</span><span class="sxs-lookup"><span data-stu-id="fc52f-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="fc52f-136">Controlar y definir permisos de hello como entidad de servicio de hello toowhat operaciones puede llevar a cabo en Azure.</span><span class="sxs-lookup"><span data-stu-id="fc52f-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="fc52f-137">tooimprove seguridad a través de la que se proporcionen un nombre de usuario y una contraseña, este ejemplo crea un servicio básico principal.</span><span class="sxs-lookup"><span data-stu-id="fc52f-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="fc52f-138">Crear un servicio principal con [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) y las credenciales de Hola de salida que necesita Ansible:</span><span class="sxs-lookup"><span data-stu-id="fc52f-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="fc52f-139">Un ejemplo de salida de hello de hello anterior comandos es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="fc52f-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="fc52f-140">tooauthenticate tooAzure, también deberá tooobtain Id. de la suscripción de Azure con [mostrar de la cuenta de az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="fc52f-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="fc52f-141">Utilice la salida de hello de estos dos comandos en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="fc52f-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="fc52f-142">Creación de un archivo de credenciales de Ansible</span><span class="sxs-lookup"><span data-stu-id="fc52f-142">Create Ansible credentials file</span></span>
<span data-ttu-id="fc52f-143">tooprovide credenciales tooAnsible, definir variables de entorno o crear un archivo de credenciales locales.</span><span class="sxs-lookup"><span data-stu-id="fc52f-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="fc52f-144">Para obtener más información acerca de cómo toodefine Ansible credenciales, vea [tooAzure proporcionar credenciales módulos](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="fc52f-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="fc52f-145">Para entornos de desarrollo, cree un archivo *credentials* para Ansible en la VM de host de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="fc52f-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="fc52f-146">Hola *credenciales* propio archivo combina Id. de suscripción de hello con salida de hello de creación de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="fc52f-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="fc52f-147">Salida de hello anterior [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) comando es Hola mismo ordenar según sea necesario para *client_id*, *secreto*, y *inquilino* .</span><span class="sxs-lookup"><span data-stu-id="fc52f-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="fc52f-148">Hola después ejemplo *credenciales* archivo muestra estos valores que coinciden con salida de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="fc52f-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="fc52f-149">Escriba sus propios valores, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fc52f-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="fc52f-150">Uso de variables de entorno de Ansible</span><span class="sxs-lookup"><span data-stu-id="fc52f-150">Use Ansible environment variables</span></span>
<span data-ttu-id="fc52f-151">Si va toouse herramientas como Ansible torre o Jenkins, puede definir variables de entorno como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="fc52f-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="fc52f-152">Estas variables combinan Hola Id. de suscripción con el resultado de hello de creación de un servicio principal.</span><span class="sxs-lookup"><span data-stu-id="fc52f-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="fc52f-153">Salida de hello anterior [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) comando es Hola mismo ordenar según sea necesario para *AZURE_CLIENT_ID*, *AZURE_SECRET*, y *AZURE_ INQUILINO*.</span><span class="sxs-lookup"><span data-stu-id="fc52f-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="fc52f-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc52f-154">Next steps</span></span>
<span data-ttu-id="fc52f-155">Ahora tiene Ansible y Hola necesario módulos de Azure Python SDK instalados y las credenciales definidas para Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="fc52f-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="fc52f-156">Obtenga información acerca de cómo demasiado[crear una máquina virtual con Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="fc52f-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="fc52f-157">También puede aprender cómo demasiado[crear una VM de Azure completo y compatibilidad con recursos con Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="fc52f-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
