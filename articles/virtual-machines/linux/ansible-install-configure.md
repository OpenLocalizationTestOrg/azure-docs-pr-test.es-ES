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
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Instalar y configurar máquinas virtuales de Ansible toomanage en Azure
Este artículo detalla cómo tooinstall Ansible y módulos de Azure SDK de Python necesarios para algunos de Hola distribuciones de Linux más comunes. Puede instalar Ansible en otras distribuciones ajustando Hola instalado paquetes toofit su plataforma concreta. toocreate Azure recursos de forma segura, también aprenderá cómo toocreate y definir credenciales para Ansible toouse. 

Para obtener más opciones de instalación y los pasos para plataformas adicionales, vea hello [Guía de instalación de Ansible](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Instalación de Ansible
En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupAnsible* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Ahora cree una máquina virtual e instale Ansible para uno de hello siguientes distribuciones:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Cree la máquina virtual con [az vm create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM con Hola `publicIpAddress` anotó en hello operación de creación de la salida de hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

En la máquina virtual, instalar paquetes de hello necesario para módulos de Azure SDK de Python de Hola y Ansible como se indica a continuación:

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

Ahora pasamos demasiado[las credenciales de Azure crear](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Cree la máquina virtual con [az vm create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM con Hola `publicIpAddress` anotó en hello operación de creación de la salida de hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

En la máquina virtual, instalar paquetes de hello necesario para módulos de Azure SDK de Python de Hola y Ansible como se indica a continuación:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Ahora pasamos demasiado[las credenciales de Azure crear](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
Cree la máquina virtual con [az vm create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM con Hola `publicIpAddress` anotó en hello operación de creación de la salida de hello VM:

```bash
ssh azureuser@<publicIpAddress>
```

En la máquina virtual, instalar paquetes de hello necesario para módulos de Azure SDK de Python de Hola y Ansible como se indica a continuación:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Ahora pasamos demasiado[las credenciales de Azure crear](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Creación de credenciales de Azure
Ansible se comunica con Azure mediante un nombre de usuario y una contraseña, o a través de una entidad de servicio. Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como Ansible. Controlar y definir permisos de hello como entidad de servicio de hello toowhat operaciones puede llevar a cabo en Azure. tooimprove seguridad a través de la que se proporcionen un nombre de usuario y una contraseña, este ejemplo crea un servicio básico principal.

Crear un servicio principal con [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) y las credenciales de Hola de salida que necesita Ansible:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Un ejemplo de salida de hello de hello anterior comandos es la siguiente:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure, también deberá tooobtain Id. de la suscripción de Azure con [mostrar de la cuenta de az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Utilice la salida de hello de estos dos comandos en el paso siguiente Hola.


## <a name="create-ansible-credentials-file"></a>Creación de un archivo de credenciales de Ansible
tooprovide credenciales tooAnsible, definir variables de entorno o crear un archivo de credenciales locales. Para obtener más información acerca de cómo toodefine Ansible credenciales, vea [tooAzure proporcionar credenciales módulos](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Para entornos de desarrollo, cree un archivo *credentials* para Ansible en la VM de host de la siguiente forma:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Hola *credenciales* propio archivo combina Id. de suscripción de hello con salida de hello de creación de una entidad de servicio. Salida de hello anterior [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) comando es Hola mismo ordenar según sea necesario para *client_id*, *secreto*, y *inquilino* . Hola después ejemplo *credenciales* archivo muestra estos valores que coinciden con salida de hello anterior. Escriba sus propios valores, como se indica a continuación:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Uso de variables de entorno de Ansible
Si va toouse herramientas como Ansible torre o Jenkins, puede definir variables de entorno como se indica a continuación. Estas variables combinan Hola Id. de suscripción con el resultado de hello de creación de un servicio principal. Salida de hello anterior [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) comando es Hola mismo ordenar según sea necesario para *AZURE_CLIENT_ID*, *AZURE_SECRET*, y *AZURE_ INQUILINO*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Pasos siguientes
Ahora tiene Ansible y Hola necesario módulos de Azure Python SDK instalados y las credenciales definidas para Ansible toouse. Obtenga información acerca de cómo demasiado[crear una máquina virtual con Ansible](ansible-create-vm.md). También puede aprender cómo demasiado[crear una VM de Azure completo y compatibilidad con recursos con Ansible](ansible-create-complete-vm.md).
