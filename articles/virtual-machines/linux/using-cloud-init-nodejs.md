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
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="2c298-103">Usar en la nube init toocustomize una VM Linux durante la creación con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2c298-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="2c298-104">Este artículo muestra cómo toomake una tooset de secuencia de comandos en la nube init Hola hostname, actualizar los paquetes instalados y administrar cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="2c298-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="2c298-105">secuencias de comandos de Hello init de la nube se llaman durante la creación de VM de Azure CLI Hola.</span><span class="sxs-lookup"><span data-stu-id="2c298-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="2c298-106">Hola artículo requiere:</span><span class="sxs-lookup"><span data-stu-id="2c298-106">hello article requires:</span></span>

* <span data-ttu-id="2c298-107">una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="2c298-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="2c298-108">Hola [CLI de Azure](../../cli-install-nodejs.md) inició sesión `azure login`.</span><span class="sxs-lookup"><span data-stu-id="2c298-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="2c298-109">Hola CLI de Azure *debe estar en* modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="2c298-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2c298-110">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="2c298-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="2c298-111">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="2c298-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="2c298-112">[Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="2c298-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2c298-113">[Azure 2.0 CLI](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="2c298-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="2c298-114">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="2c298-114">Quick Commands</span></span>
<span data-ttu-id="2c298-115">Crear una secuencia de comandos de init.txt en la nube que establece el nombre de host de hello, actualiza todos los paquetes y se agrega un tooLinux de usuario de sudo.</span><span class="sxs-lookup"><span data-stu-id="2c298-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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
<span data-ttu-id="2c298-116">Crear un toolaunch de grupo de recursos de las máquinas virtuales en.</span><span class="sxs-lookup"><span data-stu-id="2c298-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="2c298-117">Crear una VM de Linux con tooconfigure init de la nube durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="2c298-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="2c298-118">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="2c298-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="2c298-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="2c298-119">Introduction</span></span>
<span data-ttu-id="2c298-120">Cuando inicia una nueva VM de Linux, obtiene una VM Linux estándar con nada personalizado o preparada para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="2c298-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="2c298-121">[En la nube init](https://cloudinit.readthedocs.org) es una manera estándar tooinject una secuencia de comandos u opciones de configuración en esa VM de Linux tal y como se está iniciando en hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="2c298-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="2c298-122">En Azure, hay un tres maneras diferentes toomake cambios en una VM Linux cuando se implementa o arrancar.</span><span class="sxs-lookup"><span data-stu-id="2c298-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="2c298-123">Inserte scripts con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="2c298-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="2c298-124">Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c298-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="2c298-125">Una plantilla de Azure con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="2c298-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="2c298-126">Una plantilla de Azure con [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c298-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2c298-127">secuencias de comandos de tooinject en cualquier momento tras el arranque:</span><span class="sxs-lookup"><span data-stu-id="2c298-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="2c298-128">SSH toorun directamente comandos</span><span class="sxs-lookup"><span data-stu-id="2c298-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="2c298-129">Insertar secuencias de comandos mediante hello Azure [VMAccess extensión](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ya sea de manera imperativa o en una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="2c298-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="2c298-130">Herramientas de administración de la configuración, como Ansible, Salt, Chef y Puppet.</span><span class="sxs-lookup"><span data-stu-id="2c298-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="2c298-131">: La extensión VMAccess ejecuta una secuencia de comandos como raíz en hello mismo utilizando SSH puede.</span><span class="sxs-lookup"><span data-stu-id="2c298-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="2c298-132">Sin embargo, utilizando la extensión de máquina virtual de hello habilita varias características que ofrece Azure que puede ser útiles en función de su escenario.</span><span class="sxs-lookup"><span data-stu-id="2c298-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="2c298-133">Disponibilidad de cloud-init en los alias de imagen de creación rápida de VM de Azure:</span><span class="sxs-lookup"><span data-stu-id="2c298-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="2c298-134">Alias</span><span class="sxs-lookup"><span data-stu-id="2c298-134">Alias</span></span> | <span data-ttu-id="2c298-135">Publicador</span><span class="sxs-lookup"><span data-stu-id="2c298-135">Publisher</span></span> | <span data-ttu-id="2c298-136">Oferta</span><span class="sxs-lookup"><span data-stu-id="2c298-136">Offer</span></span> | <span data-ttu-id="2c298-137">SKU</span><span class="sxs-lookup"><span data-stu-id="2c298-137">SKU</span></span> | <span data-ttu-id="2c298-138">Versión</span><span class="sxs-lookup"><span data-stu-id="2c298-138">Version</span></span> | <span data-ttu-id="2c298-139">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="2c298-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="2c298-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="2c298-140">CentOS</span></span> |<span data-ttu-id="2c298-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="2c298-141">OpenLogic</span></span> |<span data-ttu-id="2c298-142">CentOS</span><span class="sxs-lookup"><span data-stu-id="2c298-142">Centos</span></span> |<span data-ttu-id="2c298-143">7,2</span><span class="sxs-lookup"><span data-stu-id="2c298-143">7.2</span></span> |<span data-ttu-id="2c298-144">más reciente</span><span class="sxs-lookup"><span data-stu-id="2c298-144">latest</span></span> |<span data-ttu-id="2c298-145">no</span><span class="sxs-lookup"><span data-stu-id="2c298-145">no</span></span> |
| <span data-ttu-id="2c298-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2c298-146">CoreOS</span></span> |<span data-ttu-id="2c298-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2c298-147">CoreOS</span></span> |<span data-ttu-id="2c298-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2c298-148">CoreOS</span></span> |<span data-ttu-id="2c298-149">Stable</span><span class="sxs-lookup"><span data-stu-id="2c298-149">Stable</span></span> |<span data-ttu-id="2c298-150">más reciente</span><span class="sxs-lookup"><span data-stu-id="2c298-150">latest</span></span> |<span data-ttu-id="2c298-151">yes</span><span class="sxs-lookup"><span data-stu-id="2c298-151">yes</span></span> |
| <span data-ttu-id="2c298-152">Debian</span><span class="sxs-lookup"><span data-stu-id="2c298-152">Debian</span></span> |<span data-ttu-id="2c298-153">credativ</span><span class="sxs-lookup"><span data-stu-id="2c298-153">credativ</span></span> |<span data-ttu-id="2c298-154">Debian</span><span class="sxs-lookup"><span data-stu-id="2c298-154">Debian</span></span> |<span data-ttu-id="2c298-155">8</span><span class="sxs-lookup"><span data-stu-id="2c298-155">8</span></span> |<span data-ttu-id="2c298-156">más reciente</span><span class="sxs-lookup"><span data-stu-id="2c298-156">latest</span></span> |<span data-ttu-id="2c298-157">no</span><span class="sxs-lookup"><span data-stu-id="2c298-157">no</span></span> |
| <span data-ttu-id="2c298-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="2c298-158">openSUSE</span></span> |<span data-ttu-id="2c298-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="2c298-159">SUSE</span></span> |<span data-ttu-id="2c298-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="2c298-160">openSUSE</span></span> |<span data-ttu-id="2c298-161">13.2</span><span class="sxs-lookup"><span data-stu-id="2c298-161">13.2</span></span> |<span data-ttu-id="2c298-162">más reciente</span><span class="sxs-lookup"><span data-stu-id="2c298-162">latest</span></span> |<span data-ttu-id="2c298-163">no</span><span class="sxs-lookup"><span data-stu-id="2c298-163">no</span></span> |
| <span data-ttu-id="2c298-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="2c298-164">RHEL</span></span> |<span data-ttu-id="2c298-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="2c298-165">Redhat</span></span> |<span data-ttu-id="2c298-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="2c298-166">RHEL</span></span> |<span data-ttu-id="2c298-167">7,2</span><span class="sxs-lookup"><span data-stu-id="2c298-167">7.2</span></span> |<span data-ttu-id="2c298-168">más reciente</span><span class="sxs-lookup"><span data-stu-id="2c298-168">latest</span></span> |<span data-ttu-id="2c298-169">no</span><span class="sxs-lookup"><span data-stu-id="2c298-169">no</span></span> |
| <span data-ttu-id="2c298-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="2c298-170">UbuntuLTS</span></span> |<span data-ttu-id="2c298-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="2c298-171">Canonical</span></span> |<span data-ttu-id="2c298-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="2c298-172">UbuntuServer</span></span> |<span data-ttu-id="2c298-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="2c298-173">14.04.4-LTS</span></span> |<span data-ttu-id="2c298-174">más reciente</span><span class="sxs-lookup"><span data-stu-id="2c298-174">latest</span></span> |<span data-ttu-id="2c298-175">yes</span><span class="sxs-lookup"><span data-stu-id="2c298-175">yes</span></span> |

<span data-ttu-id="2c298-176">Microsoft está trabajando con nuestro socios tooget nube-init incluida y estamos trabajando en las imágenes de Hola que proporcionan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2c298-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="2c298-177">Agregar una creación de VM de nube init script toohello con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2c298-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="2c298-178">toolaunch una secuencia de comandos en la nube init al crear una máquina virtual en Azure, especifique el archivo de init de la nube de hello mediante hello Azure CLI `--custom-data` cambiar.</span><span class="sxs-lookup"><span data-stu-id="2c298-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="2c298-179">Crear un toolaunch de grupo de recursos de las máquinas virtuales en.</span><span class="sxs-lookup"><span data-stu-id="2c298-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="2c298-180">Crear una VM de Linux con tooconfigure init de la nube durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="2c298-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="2c298-181">Crear un nombre de host de nube init script tooset Hola de una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="2c298-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="2c298-182">Uno de hello más sencilla y la configuración más importante para las VM de Linux sería el nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c298-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="2c298-183">Podemos establecer esto fácilmente mediante cloud-init con este script.</span><span class="sxs-lookup"><span data-stu-id="2c298-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="2c298-184">Script de cloud-init de ejemplo denominado `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="2c298-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="2c298-185">Durante el inicio de Hola de hello VM, esta secuencia de comandos en la nube init establece Hola hostname demasiado`myservername`.</span><span class="sxs-lookup"><span data-stu-id="2c298-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

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

<span data-ttu-id="2c298-186">Inicio de sesión y comprobar el nombre de host de Hola de hello nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2c298-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="2c298-187">Crear un tooupdate de secuencia de comandos en la nube init Linux</span><span class="sxs-lookup"><span data-stu-id="2c298-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="2c298-188">Para la seguridad, desea que su tooupdate Ubuntu VM en el primer inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2c298-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="2c298-189">Mediante init en la nube que podemos hacer con hello siga script, en función de distribución de Linux de Hola que usa.</span><span class="sxs-lookup"><span data-stu-id="2c298-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="2c298-190">Secuencia de comandos de ejemplo en la nube init `cloud_config_apt_upgrade.txt` para hello Debian familia</span><span class="sxs-lookup"><span data-stu-id="2c298-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="2c298-191">Una vez que ha arrancado Linux, se actualizan todos los paquetes de saludo instalado a través de `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="2c298-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

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

<span data-ttu-id="2c298-192">Inicie sesión y compruebe que todos los paquetes se han actualizado.</span><span class="sxs-lookup"><span data-stu-id="2c298-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="2c298-193">Crear un tooadd de secuencia de comandos en la nube de inicializar un tooLinux de usuario</span><span class="sxs-lookup"><span data-stu-id="2c298-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="2c298-194">Una de las primeras tareas de Hola en cualquier nueva VM de Linux es un usuario para usted mismo o usar tooavoid tooadd `root`.</span><span class="sxs-lookup"><span data-stu-id="2c298-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="2c298-195">Claves de SSH son una práctica recomendada para la seguridad y facilidad de uso y se agregan toohello `~/.ssh/authorized_keys` archivo con este script init de la nube.</span><span class="sxs-lookup"><span data-stu-id="2c298-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="2c298-196">Script de cloud-init de ejemplo `cloud_config_add_users.txt` para la familia Debian</span><span class="sxs-lookup"><span data-stu-id="2c298-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="2c298-197">Una vez que ha arrancado Linux, todos los usuarios de hello enumerado son toohello creado y agregado sudo grupo.</span><span class="sxs-lookup"><span data-stu-id="2c298-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

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

<span data-ttu-id="2c298-198">Inicio de sesión y comprobar el usuario Hola recién creado.</span><span class="sxs-lookup"><span data-stu-id="2c298-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="2c298-199">Salida</span><span class="sxs-lookup"><span data-stu-id="2c298-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="2c298-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c298-200">Next Steps</span></span>
<span data-ttu-id="2c298-201">Init de la nube se está convirtiendo en una toomodify de manera estándar la VM de Linux en el arranque.</span><span class="sxs-lookup"><span data-stu-id="2c298-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="2c298-202">Azure también tiene extensiones de máquina virtual, lo que permitirá toomodify su LinuxVM en el arranque o mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="2c298-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="2c298-203">Por ejemplo, puede usar hello Azure VMAccessExtension tooreset SSH o información de usuario mientras se está ejecutando Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2c298-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="2c298-204">Con init de la nube, necesitará una contraseña de hello tooreset de reinicio.</span><span class="sxs-lookup"><span data-stu-id="2c298-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="2c298-205">Acerca de las características y extensiones de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="2c298-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="2c298-206">Administrar usuarios, SSH y verificación o reparación de discos sobre el uso de máquinas virtuales de Linux de Azure Hola VMAccess extensión</span><span class="sxs-lookup"><span data-stu-id="2c298-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

