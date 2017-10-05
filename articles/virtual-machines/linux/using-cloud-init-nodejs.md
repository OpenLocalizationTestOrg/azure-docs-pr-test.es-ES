---
title: "Uso de cloud-init para personalizar una máquina virtual Linux durante su creación en Azure | Microsoft Docs"
description: "Procedimiento para usar cloud-init con el fin de personalizar una máquina virtual Linux con la CLI de Azure 1.0"
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
ms.openlocfilehash: 0b6150bca333188666935b3c9aa02c4b33690db9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="24d03-103">Uso de cloud-init para personalizar una máquina virtual Linux con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="24d03-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="24d03-104">Este artículo muestra cómo crear un script de cloud-init para establecer el nombre de host, actualizar los paquetes instalados y administrar cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="24d03-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="24d03-105">Los scripts de cloud-init se llaman durante la creación de la VM desde la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="24d03-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="24d03-106">Este artículo requiere:</span><span class="sxs-lookup"><span data-stu-id="24d03-106">The article requires:</span></span>

* <span data-ttu-id="24d03-107">una cuenta de Azure ([obtenga aquí una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="24d03-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="24d03-108">la [CLI de Azure](../../cli-install-nodejs.md) en la que se inició sesión con `azure login`;</span><span class="sxs-lookup"><span data-stu-id="24d03-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="24d03-109">la CLI de Azure *debe estar en* el modo Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="24d03-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="24d03-110">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="24d03-110">CLI versions to complete the task</span></span>
<span data-ttu-id="24d03-111">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="24d03-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="24d03-112">[CLI de Azure 1.0](#quick-commands): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="24d03-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="24d03-113">[CLI de Azure 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): la CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="24d03-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="24d03-114">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="24d03-114">Quick Commands</span></span>
<span data-ttu-id="24d03-115">Cree un script cloud-init.txt que establezca el nombre de host, actualice todos los paquetes y agregue un usuario de sudo a Linux.</span><span class="sxs-lookup"><span data-stu-id="24d03-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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
<span data-ttu-id="24d03-116">Cree un grupo de recursos en el que se inicien las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="24d03-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="24d03-117">Cree una VM Linux con cloud-init para configurarla durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="24d03-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="24d03-118">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="24d03-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="24d03-119">Introducción</span><span class="sxs-lookup"><span data-stu-id="24d03-119">Introduction</span></span>
<span data-ttu-id="24d03-120">Cuando inicia una nueva VM de Linux, obtiene una VM Linux estándar con nada personalizado o preparada para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="24d03-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="24d03-121">[Cloud-init](https://cloudinit.readthedocs.org) es una forma estándar de insertar un script u opciones de configuración en esa VM Linux cuando arranca por primera vez.</span><span class="sxs-lookup"><span data-stu-id="24d03-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="24d03-122">En Azure hay tres formas distintas de realizar cambios en una VM Linux cuando se está implementando o arrancando.</span><span class="sxs-lookup"><span data-stu-id="24d03-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="24d03-123">Inserte scripts con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="24d03-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="24d03-124">Inserte scripts con la [extensión VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)de Azure.</span><span class="sxs-lookup"><span data-stu-id="24d03-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="24d03-125">Una plantilla de Azure con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="24d03-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="24d03-126">Una plantilla de Azure con [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24d03-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="24d03-127">Para insertar scripts en cualquier momento después del arranque:</span><span class="sxs-lookup"><span data-stu-id="24d03-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="24d03-128">SSH para ejecutar directamente los comandos.</span><span class="sxs-lookup"><span data-stu-id="24d03-128">SSH to run commands directly</span></span>
* <span data-ttu-id="24d03-129">Inserte scripts con la [extensión VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)de Azure, ya sea de manera imperativa como en una plantilla de Azure.</span><span class="sxs-lookup"><span data-stu-id="24d03-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="24d03-130">Herramientas de administración de la configuración, como Ansible, Salt, Chef y Puppet.</span><span class="sxs-lookup"><span data-stu-id="24d03-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="24d03-131">La extensión VMAccess ejecuta un script como raíz del mismo modo que podría hacerlo con SSH.</span><span class="sxs-lookup"><span data-stu-id="24d03-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="24d03-132">Sin embargo, con la extensión de VM se habilitan varias características que Azure ofrece y que pueden ser útiles según el escenario.</span><span class="sxs-lookup"><span data-stu-id="24d03-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="24d03-133">Disponibilidad de cloud-init en los alias de imagen de creación rápida de VM de Azure:</span><span class="sxs-lookup"><span data-stu-id="24d03-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="24d03-134">Alias</span><span class="sxs-lookup"><span data-stu-id="24d03-134">Alias</span></span> | <span data-ttu-id="24d03-135">Publicador</span><span class="sxs-lookup"><span data-stu-id="24d03-135">Publisher</span></span> | <span data-ttu-id="24d03-136">Oferta</span><span class="sxs-lookup"><span data-stu-id="24d03-136">Offer</span></span> | <span data-ttu-id="24d03-137">SKU</span><span class="sxs-lookup"><span data-stu-id="24d03-137">SKU</span></span> | <span data-ttu-id="24d03-138">Versión</span><span class="sxs-lookup"><span data-stu-id="24d03-138">Version</span></span> | <span data-ttu-id="24d03-139">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="24d03-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="24d03-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="24d03-140">CentOS</span></span> |<span data-ttu-id="24d03-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="24d03-141">OpenLogic</span></span> |<span data-ttu-id="24d03-142">CentOS</span><span class="sxs-lookup"><span data-stu-id="24d03-142">Centos</span></span> |<span data-ttu-id="24d03-143">7,2</span><span class="sxs-lookup"><span data-stu-id="24d03-143">7.2</span></span> |<span data-ttu-id="24d03-144">más reciente</span><span class="sxs-lookup"><span data-stu-id="24d03-144">latest</span></span> |<span data-ttu-id="24d03-145">no</span><span class="sxs-lookup"><span data-stu-id="24d03-145">no</span></span> |
| <span data-ttu-id="24d03-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="24d03-146">CoreOS</span></span> |<span data-ttu-id="24d03-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="24d03-147">CoreOS</span></span> |<span data-ttu-id="24d03-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="24d03-148">CoreOS</span></span> |<span data-ttu-id="24d03-149">Stable</span><span class="sxs-lookup"><span data-stu-id="24d03-149">Stable</span></span> |<span data-ttu-id="24d03-150">más reciente</span><span class="sxs-lookup"><span data-stu-id="24d03-150">latest</span></span> |<span data-ttu-id="24d03-151">yes</span><span class="sxs-lookup"><span data-stu-id="24d03-151">yes</span></span> |
| <span data-ttu-id="24d03-152">Debian</span><span class="sxs-lookup"><span data-stu-id="24d03-152">Debian</span></span> |<span data-ttu-id="24d03-153">credativ</span><span class="sxs-lookup"><span data-stu-id="24d03-153">credativ</span></span> |<span data-ttu-id="24d03-154">Debian</span><span class="sxs-lookup"><span data-stu-id="24d03-154">Debian</span></span> |<span data-ttu-id="24d03-155">8</span><span class="sxs-lookup"><span data-stu-id="24d03-155">8</span></span> |<span data-ttu-id="24d03-156">más reciente</span><span class="sxs-lookup"><span data-stu-id="24d03-156">latest</span></span> |<span data-ttu-id="24d03-157">no</span><span class="sxs-lookup"><span data-stu-id="24d03-157">no</span></span> |
| <span data-ttu-id="24d03-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="24d03-158">openSUSE</span></span> |<span data-ttu-id="24d03-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="24d03-159">SUSE</span></span> |<span data-ttu-id="24d03-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="24d03-160">openSUSE</span></span> |<span data-ttu-id="24d03-161">13.2</span><span class="sxs-lookup"><span data-stu-id="24d03-161">13.2</span></span> |<span data-ttu-id="24d03-162">más reciente</span><span class="sxs-lookup"><span data-stu-id="24d03-162">latest</span></span> |<span data-ttu-id="24d03-163">no</span><span class="sxs-lookup"><span data-stu-id="24d03-163">no</span></span> |
| <span data-ttu-id="24d03-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="24d03-164">RHEL</span></span> |<span data-ttu-id="24d03-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="24d03-165">Redhat</span></span> |<span data-ttu-id="24d03-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="24d03-166">RHEL</span></span> |<span data-ttu-id="24d03-167">7,2</span><span class="sxs-lookup"><span data-stu-id="24d03-167">7.2</span></span> |<span data-ttu-id="24d03-168">más reciente</span><span class="sxs-lookup"><span data-stu-id="24d03-168">latest</span></span> |<span data-ttu-id="24d03-169">no</span><span class="sxs-lookup"><span data-stu-id="24d03-169">no</span></span> |
| <span data-ttu-id="24d03-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="24d03-170">UbuntuLTS</span></span> |<span data-ttu-id="24d03-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="24d03-171">Canonical</span></span> |<span data-ttu-id="24d03-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="24d03-172">UbuntuServer</span></span> |<span data-ttu-id="24d03-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="24d03-173">14.04.4-LTS</span></span> |<span data-ttu-id="24d03-174">más reciente</span><span class="sxs-lookup"><span data-stu-id="24d03-174">latest</span></span> |<span data-ttu-id="24d03-175">yes</span><span class="sxs-lookup"><span data-stu-id="24d03-175">yes</span></span> |

<span data-ttu-id="24d03-176">Microsoft trabaja con nuestros asociados para que cloud-init se incluya y funcione en las imágenes que proporcionan a Azure.</span><span class="sxs-lookup"><span data-stu-id="24d03-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="24d03-177">Incorporación de un script de cloud-init a la creación de VM con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="24d03-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="24d03-178">Para iniciar un script de cloud-init al crear una VM en Azure, especifique el archivo de cloud-init mediante el modificador `--custom-data` de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="24d03-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="24d03-179">Cree un grupo de recursos en el que se inicien las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="24d03-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="24d03-180">Cree una VM Linux con cloud-init para configurarla durante el arranque.</span><span class="sxs-lookup"><span data-stu-id="24d03-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

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

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="24d03-181">Creación de un script de cloud-init para establecer el nombre de host de una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="24d03-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="24d03-182">Una de las configuraciones más sencillas y más importantes para cualquier VM de Linux sería el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="24d03-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="24d03-183">Podemos establecer esto fácilmente mediante cloud-init con este script.</span><span class="sxs-lookup"><span data-stu-id="24d03-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="24d03-184">Script de cloud-init de ejemplo denominado `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="24d03-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="24d03-185">Durante el primer inicio de la VM, este script de cloud-init establece el nombre de host en `myservername`.</span><span class="sxs-lookup"><span data-stu-id="24d03-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

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

<span data-ttu-id="24d03-186">Inicie sesión y compruebe el nombre de host de la nueva VM.</span><span class="sxs-lookup"><span data-stu-id="24d03-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="24d03-187">Creación de un script de cloud-init para actualizar Linux</span><span class="sxs-lookup"><span data-stu-id="24d03-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="24d03-188">Por seguridad, desea que la VM de Ubuntu se actualice en el primer arranque.</span><span class="sxs-lookup"><span data-stu-id="24d03-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="24d03-189">Mediante cloud-init podemos hacerlo con el siguiente script, dependiendo de la distribución de Linux que se use.</span><span class="sxs-lookup"><span data-stu-id="24d03-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="24d03-190">Script de cloud-init de ejemplo `cloud_config_apt_upgrade.txt` para la familia Debian</span><span class="sxs-lookup"><span data-stu-id="24d03-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="24d03-191">Después de iniciarse Linux, se actualizan todos los paquetes instalados a través de `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="24d03-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

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

<span data-ttu-id="24d03-192">Inicie sesión y compruebe que todos los paquetes se han actualizado.</span><span class="sxs-lookup"><span data-stu-id="24d03-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="24d03-193">Creación de un script de cloud-init para agregar un usuario a Linux</span><span class="sxs-lookup"><span data-stu-id="24d03-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="24d03-194">Una de las primeras tareas en cualquier VM Linux nueva es agregar un usuario para usted mismo o para evitar el uso de `root`.</span><span class="sxs-lookup"><span data-stu-id="24d03-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="24d03-195">Las claves SSH son el procedimiento recomendado para la seguridad y la facilidad de uso; además, se agregan al archivo `~/.ssh/authorized_keys` con este script de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="24d03-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="24d03-196">Script de cloud-init de ejemplo `cloud_config_add_users.txt` para la familia Debian</span><span class="sxs-lookup"><span data-stu-id="24d03-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="24d03-197">Una vez que se inicia Linux, todos los usuarios de la lista se crean y se agregan al grupo de sudo.</span><span class="sxs-lookup"><span data-stu-id="24d03-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

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

<span data-ttu-id="24d03-198">Inicie sesión y compruebe el usuario recién creado.</span><span class="sxs-lookup"><span data-stu-id="24d03-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="24d03-199">Salida</span><span class="sxs-lookup"><span data-stu-id="24d03-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="24d03-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24d03-200">Next Steps</span></span>
<span data-ttu-id="24d03-201">Cloud-init se convierte en la manera estándar de modificar la VM Linux en el arranque.</span><span class="sxs-lookup"><span data-stu-id="24d03-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="24d03-202">Azure también tiene extensiones de VM, que le permiten modificar su VM Linux en el arranque o mientras está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="24d03-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="24d03-203">Por ejemplo, puede usar la extensión VMAccessExtension de Azure para restablecer SSH o la información del usuario mientras la VM está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="24d03-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="24d03-204">Con cloud-init, necesitaría reiniciar para restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="24d03-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="24d03-205">Acerca de las características y extensiones de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="24d03-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="24d03-206">Administración de usuarios, SSH y comprobar o reparar discos en máquinas virtuales de Linux de Azure con la extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="24d03-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

