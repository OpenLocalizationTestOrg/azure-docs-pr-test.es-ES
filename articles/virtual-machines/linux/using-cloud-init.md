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
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="26704-103">Usar en la nube init toocustomize una VM Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="26704-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="26704-104">Este artículo muestra cómo toomake una tooset de secuencia de comandos en la nube init Hola hostname, actualizar paquetes instalados y administrar cuentas de usuario con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="26704-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="26704-105">secuencias de comandos de Hello init de la nube se llama cuando se crea una máquina virtual (VM) de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="26704-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="26704-106">Para obtener información más detallada acerca de la instalación de aplicaciones, la escritura de archivos de configuración y la inserción de claves desde Key Vault, consulte [este tutorial](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="26704-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="26704-107">También puede realizar estos pasos con hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="26704-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="26704-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="26704-108">Quick commands</span></span>
<span data-ttu-id="26704-109">Crear una secuencia de comandos de init.txt en la nube que establece el nombre de host de hello, actualiza todos los paquetes y se agrega un tooLinux de usuario de sudo.</span><span class="sxs-lookup"><span data-stu-id="26704-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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

<span data-ttu-id="26704-110">Crear un toolaunch de grupo de recursos de las máquinas virtuales en con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="26704-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="26704-111">Hello en el ejemplo siguiente se crea grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="26704-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="26704-112">Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque con hello `--custom-data` parámetro.</span><span class="sxs-lookup"><span data-stu-id="26704-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="26704-113">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="26704-113">Detailed walkthrough</span></span>
<span data-ttu-id="26704-114">Cuando inicia una nueva VM de Linux, obtiene una VM Linux estándar con nada personalizado o preparada para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="26704-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="26704-115">[En la nube init](https://cloudinit.readthedocs.org) es una manera estándar tooinject una secuencia de comandos u opciones de configuración en esa VM de Linux tal y como se está iniciando en hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="26704-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="26704-116">En Azure, hay varias maneras diferentes toomake cambios en una VM Linux cuando se implementa o arrancar.</span><span class="sxs-lookup"><span data-stu-id="26704-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="26704-117">Inserte scripts con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="26704-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="26704-118">Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="26704-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="26704-119">Una plantilla de Azure con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="26704-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="26704-120">Una plantilla de Azure con [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="26704-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="26704-121">secuencias de comandos de tooinject en cualquier momento tras el arranque:</span><span class="sxs-lookup"><span data-stu-id="26704-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="26704-122">SSH toorun directamente comandos</span><span class="sxs-lookup"><span data-stu-id="26704-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="26704-123">Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md), ya sea de manera imperativa o en una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="26704-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="26704-124">Herramientas de administración de la configuración, como Ansible, Salt, Chef y Puppet.</span><span class="sxs-lookup"><span data-stu-id="26704-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="26704-125">La VMAccess extensión ejecuta una secuencia de comandos como raíz en hello mismo utilizando SSH puede.</span><span class="sxs-lookup"><span data-stu-id="26704-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="26704-126">Sin embargo, utilizando la extensión de máquina virtual de hello habilita varias características que ofrece Azure que puede ser útiles en función de su escenario.</span><span class="sxs-lookup"><span data-stu-id="26704-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="26704-127">Disponibilidad de cloud-init en los alias de imagen de creación rápida de VM de Azure:</span><span class="sxs-lookup"><span data-stu-id="26704-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="26704-128">Alias</span><span class="sxs-lookup"><span data-stu-id="26704-128">Alias</span></span> | <span data-ttu-id="26704-129">Publicador</span><span class="sxs-lookup"><span data-stu-id="26704-129">Publisher</span></span> | <span data-ttu-id="26704-130">Oferta</span><span class="sxs-lookup"><span data-stu-id="26704-130">Offer</span></span> | <span data-ttu-id="26704-131">SKU</span><span class="sxs-lookup"><span data-stu-id="26704-131">SKU</span></span> | <span data-ttu-id="26704-132">Versión</span><span class="sxs-lookup"><span data-stu-id="26704-132">Version</span></span> | <span data-ttu-id="26704-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="26704-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="26704-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="26704-134">CentOS</span></span> |<span data-ttu-id="26704-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="26704-135">OpenLogic</span></span> |<span data-ttu-id="26704-136">CentOS</span><span class="sxs-lookup"><span data-stu-id="26704-136">Centos</span></span> |<span data-ttu-id="26704-137">7,2</span><span class="sxs-lookup"><span data-stu-id="26704-137">7.2</span></span> |<span data-ttu-id="26704-138">más reciente</span><span class="sxs-lookup"><span data-stu-id="26704-138">latest</span></span> |<span data-ttu-id="26704-139">no</span><span class="sxs-lookup"><span data-stu-id="26704-139">no</span></span> |
| <span data-ttu-id="26704-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="26704-140">CoreOS</span></span> |<span data-ttu-id="26704-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="26704-141">CoreOS</span></span> |<span data-ttu-id="26704-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="26704-142">CoreOS</span></span> |<span data-ttu-id="26704-143">Stable</span><span class="sxs-lookup"><span data-stu-id="26704-143">Stable</span></span> |<span data-ttu-id="26704-144">más reciente</span><span class="sxs-lookup"><span data-stu-id="26704-144">latest</span></span> |<span data-ttu-id="26704-145">yes</span><span class="sxs-lookup"><span data-stu-id="26704-145">yes</span></span> |
| <span data-ttu-id="26704-146">Debian</span><span class="sxs-lookup"><span data-stu-id="26704-146">Debian</span></span> |<span data-ttu-id="26704-147">credativ</span><span class="sxs-lookup"><span data-stu-id="26704-147">credativ</span></span> |<span data-ttu-id="26704-148">Debian</span><span class="sxs-lookup"><span data-stu-id="26704-148">Debian</span></span> |<span data-ttu-id="26704-149">8</span><span class="sxs-lookup"><span data-stu-id="26704-149">8</span></span> |<span data-ttu-id="26704-150">más reciente</span><span class="sxs-lookup"><span data-stu-id="26704-150">latest</span></span> |<span data-ttu-id="26704-151">no</span><span class="sxs-lookup"><span data-stu-id="26704-151">no</span></span> |
| <span data-ttu-id="26704-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="26704-152">openSUSE</span></span> |<span data-ttu-id="26704-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="26704-153">SUSE</span></span> |<span data-ttu-id="26704-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="26704-154">openSUSE</span></span> |<span data-ttu-id="26704-155">13.2</span><span class="sxs-lookup"><span data-stu-id="26704-155">13.2</span></span> |<span data-ttu-id="26704-156">más reciente</span><span class="sxs-lookup"><span data-stu-id="26704-156">latest</span></span> |<span data-ttu-id="26704-157">no</span><span class="sxs-lookup"><span data-stu-id="26704-157">no</span></span> |
| <span data-ttu-id="26704-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="26704-158">RHEL</span></span> |<span data-ttu-id="26704-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="26704-159">Redhat</span></span> |<span data-ttu-id="26704-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="26704-160">RHEL</span></span> |<span data-ttu-id="26704-161">7,2</span><span class="sxs-lookup"><span data-stu-id="26704-161">7.2</span></span> |<span data-ttu-id="26704-162">más reciente</span><span class="sxs-lookup"><span data-stu-id="26704-162">latest</span></span> |<span data-ttu-id="26704-163">no</span><span class="sxs-lookup"><span data-stu-id="26704-163">no</span></span> |
| <span data-ttu-id="26704-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="26704-164">UbuntuLTS</span></span> |<span data-ttu-id="26704-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="26704-165">Canonical</span></span> |<span data-ttu-id="26704-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="26704-166">UbuntuServer</span></span> |<span data-ttu-id="26704-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="26704-167">14.04.4-LTS</span></span> |<span data-ttu-id="26704-168">más reciente</span><span class="sxs-lookup"><span data-stu-id="26704-168">latest</span></span> |<span data-ttu-id="26704-169">yes</span><span class="sxs-lookup"><span data-stu-id="26704-169">yes</span></span> |

<span data-ttu-id="26704-170">Estamos trabajando con nuestro socios tooget nube-init incluida y estamos trabajando en las imágenes de Hola que proporcionan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="26704-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="26704-171">Agregar una creación de VM de nube init script toohello con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="26704-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="26704-172">toolaunch una secuencia de comandos en la nube init al crear una máquina virtual en Azure, especifique el archivo de init de la nube de hello mediante hello Azure CLI `--custom-data` cambiar.</span><span class="sxs-lookup"><span data-stu-id="26704-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="26704-173">Crear un toolaunch de grupo de recursos de las máquinas virtuales en con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="26704-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="26704-174">Hello en el ejemplo siguiente se crea grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="26704-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="26704-175">Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="26704-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="26704-176">Crear un nombre de host de nube init script tooset Hola de una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="26704-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="26704-177">Uno de hello más sencilla y la configuración más importante para las VM de Linux sería el nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="26704-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="26704-178">Podemos establecer esto fácilmente mediante cloud-init con este script.</span><span class="sxs-lookup"><span data-stu-id="26704-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="26704-179">Script de cloud-init de ejemplo denominado `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="26704-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="26704-180">Durante el inicio de Hola de hello VM, esta secuencia de comandos en la nube init establece Hola hostname demasiado*myservername*.</span><span class="sxs-lookup"><span data-stu-id="26704-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="26704-181">Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="26704-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="26704-182">Inicio de sesión y comprobar el nombre de host de Hola de hello nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26704-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="26704-183">Creación de un script de cloud-init</span><span class="sxs-lookup"><span data-stu-id="26704-183">Create a cloud-init script</span></span>
<span data-ttu-id="26704-184">Para la seguridad, desea que su tooupdate Ubuntu VM en el primer inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="26704-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="26704-185">Mediante init en la nube que podemos hacer con hello siga script, en función de distribución de Linux de Hola que usa.</span><span class="sxs-lookup"><span data-stu-id="26704-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="26704-186">Secuencia de comandos de ejemplo en la nube init `cloud_config_apt_upgrade.txt` para hello Debian familia</span><span class="sxs-lookup"><span data-stu-id="26704-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="26704-187">Una vez que ha arrancado Linux, se actualizan todos los paquetes de saludo instalado a través de **apt get**.</span><span class="sxs-lookup"><span data-stu-id="26704-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="26704-188">Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="26704-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="26704-189">Inicie sesión y compruebe que todos los paquetes se han actualizado.</span><span class="sxs-lookup"><span data-stu-id="26704-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="26704-190">Crear un tooadd de secuencia de comandos en la nube de inicializar un tooLinux de usuario</span><span class="sxs-lookup"><span data-stu-id="26704-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="26704-191">Una de las primeras tareas de Hola en cualquier nueva VM de Linux es un usuario para usted mismo o usar tooavoid tooadd *raíz*.</span><span class="sxs-lookup"><span data-stu-id="26704-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="26704-192">Claves de SSH son una práctica recomendada para la seguridad y facilidad de uso y se agregan toohello *~/.ssh/authorized_keys* archivo con este script init de la nube.</span><span class="sxs-lookup"><span data-stu-id="26704-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="26704-193">Script de cloud-init de ejemplo `cloud_config_add_users.txt` para la familia Debian</span><span class="sxs-lookup"><span data-stu-id="26704-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="26704-194">Una vez que ha arrancado Linux, todos los usuarios de hello enumerado son toohello creado y agregado sudo grupo.</span><span class="sxs-lookup"><span data-stu-id="26704-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="26704-195">Crear una VM de Linux con [crear vm az](/cli/azure/vm#create) con tooconfigure init de la nube durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="26704-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="26704-196">Inicio de sesión y comprobar el usuario Hola recién creado.</span><span class="sxs-lookup"><span data-stu-id="26704-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="26704-197">Salida</span><span class="sxs-lookup"><span data-stu-id="26704-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="26704-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26704-198">Next steps</span></span>
<span data-ttu-id="26704-199">Init de la nube se está convirtiendo en una toomodify de manera estándar la VM de Linux en el arranque.</span><span class="sxs-lookup"><span data-stu-id="26704-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="26704-200">Azure también tiene extensiones de máquina virtual, lo que permitirá toomodify su LinuxVM en el arranque o mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="26704-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="26704-201">Por ejemplo, puede usar hello Azure VMAccessExtension tooreset SSH o información de usuario mientras se está ejecutando Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26704-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="26704-202">Con init de la nube, necesitará una contraseña de hello tooreset de reinicio.</span><span class="sxs-lookup"><span data-stu-id="26704-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="26704-203">Acerca de las características y extensiones de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="26704-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="26704-204">Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión</span><span class="sxs-lookup"><span data-stu-id="26704-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
