---
title: "Uso de cloud-init para personalizar una máquina virtual Linux | Microsoft Docs"
description: "Procedimiento para usar cloud-init con el fin de personalizar una máquina virtual Linux con la CLI de Azure 2.0"
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="37bd5-103">Uso de cloud-init para personalizar una máquina virtual Linux durante la creación</span><span class="sxs-lookup"><span data-stu-id="37bd5-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="37bd5-104">En este artículo se muestra cómo crear un script de cloud-init para establecer el nombre de host, actualizar los paquetes instalados y administrar cuentas de usuario con la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="37bd5-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="37bd5-105">Los scripts de cloud-init se llaman durante la creación de una máquina virtual desde la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="37bd5-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="37bd5-106">Para obtener información más detallada acerca de la instalación de aplicaciones, la escritura de archivos de configuración y la inserción de claves desde Key Vault, consulte [este tutorial](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="37bd5-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="37bd5-107">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="37bd5-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="37bd5-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="37bd5-108">Quick commands</span></span>
<span data-ttu-id="37bd5-109">Cree un script cloud-init.txt que establezca el nombre de host, actualice todos los paquetes y agregue un usuario de sudo a Linux.</span><span class="sxs-lookup"><span data-stu-id="37bd5-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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

<span data-ttu-id="37bd5-110">Cree un grupo de recursos para iniciar máquinas virtuales con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="37bd5-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="37bd5-111">En el ejemplo siguiente se crea el grupo de recursos denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="37bd5-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="37bd5-112">Cree una máquina virtual Linux con [az vm create](/cli/azure/vm#create) mediante cloud-init para configurarla durante el inicio con el parámetro `--custom-data`.</span><span class="sxs-lookup"><span data-stu-id="37bd5-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="37bd5-113">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="37bd5-113">Detailed walkthrough</span></span>
<span data-ttu-id="37bd5-114">Cuando inicia una nueva VM de Linux, obtiene una VM Linux estándar con nada personalizado o preparada para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="37bd5-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="37bd5-115">[Cloud-init](https://cloudinit.readthedocs.org) es una forma estándar de insertar un script u opciones de configuración en esa VM Linux cuando arranca por primera vez.</span><span class="sxs-lookup"><span data-stu-id="37bd5-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="37bd5-116">En Azure hay algunas formas distintas de realizar cambios en una máquina virtual Linux cuando se está implementando o arrancando.</span><span class="sxs-lookup"><span data-stu-id="37bd5-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="37bd5-117">Inserte scripts con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="37bd5-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="37bd5-118">Inserte scripts con la [extensión VMAccess](using-vmaccess-extension.md)de Azure.</span><span class="sxs-lookup"><span data-stu-id="37bd5-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="37bd5-119">Una plantilla de Azure con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="37bd5-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="37bd5-120">Una plantilla de Azure con [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="37bd5-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="37bd5-121">Para insertar scripts en cualquier momento después del arranque:</span><span class="sxs-lookup"><span data-stu-id="37bd5-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="37bd5-122">SSH para ejecutar directamente los comandos.</span><span class="sxs-lookup"><span data-stu-id="37bd5-122">SSH to run commands directly</span></span>
* <span data-ttu-id="37bd5-123">Inserte scripts con la [extensión VMAccess](using-vmaccess-extension.md)de Azure, ya sea de manera imperativa como en una plantilla de Azure.</span><span class="sxs-lookup"><span data-stu-id="37bd5-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="37bd5-124">Herramientas de administración de la configuración, como Ansible, Salt, Chef y Puppet.</span><span class="sxs-lookup"><span data-stu-id="37bd5-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="37bd5-125">La extensión VMAccess ejecuta un script como raíz del mismo modo que podría hacerlo con SSH.</span><span class="sxs-lookup"><span data-stu-id="37bd5-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="37bd5-126">Sin embargo, con la extensión de VM se habilitan varias características que Azure ofrece y que pueden ser útiles según el escenario.</span><span class="sxs-lookup"><span data-stu-id="37bd5-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="37bd5-127">Disponibilidad de cloud-init en los alias de imagen de creación rápida de VM de Azure:</span><span class="sxs-lookup"><span data-stu-id="37bd5-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="37bd5-128">Alias</span><span class="sxs-lookup"><span data-stu-id="37bd5-128">Alias</span></span> | <span data-ttu-id="37bd5-129">Publicador</span><span class="sxs-lookup"><span data-stu-id="37bd5-129">Publisher</span></span> | <span data-ttu-id="37bd5-130">Oferta</span><span class="sxs-lookup"><span data-stu-id="37bd5-130">Offer</span></span> | <span data-ttu-id="37bd5-131">SKU</span><span class="sxs-lookup"><span data-stu-id="37bd5-131">SKU</span></span> | <span data-ttu-id="37bd5-132">Versión</span><span class="sxs-lookup"><span data-stu-id="37bd5-132">Version</span></span> | <span data-ttu-id="37bd5-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="37bd5-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="37bd5-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="37bd5-134">CentOS</span></span> |<span data-ttu-id="37bd5-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="37bd5-135">OpenLogic</span></span> |<span data-ttu-id="37bd5-136">CentOS</span><span class="sxs-lookup"><span data-stu-id="37bd5-136">Centos</span></span> |<span data-ttu-id="37bd5-137">7,2</span><span class="sxs-lookup"><span data-stu-id="37bd5-137">7.2</span></span> |<span data-ttu-id="37bd5-138">más reciente</span><span class="sxs-lookup"><span data-stu-id="37bd5-138">latest</span></span> |<span data-ttu-id="37bd5-139">no</span><span class="sxs-lookup"><span data-stu-id="37bd5-139">no</span></span> |
| <span data-ttu-id="37bd5-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="37bd5-140">CoreOS</span></span> |<span data-ttu-id="37bd5-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="37bd5-141">CoreOS</span></span> |<span data-ttu-id="37bd5-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="37bd5-142">CoreOS</span></span> |<span data-ttu-id="37bd5-143">Stable</span><span class="sxs-lookup"><span data-stu-id="37bd5-143">Stable</span></span> |<span data-ttu-id="37bd5-144">más reciente</span><span class="sxs-lookup"><span data-stu-id="37bd5-144">latest</span></span> |<span data-ttu-id="37bd5-145">yes</span><span class="sxs-lookup"><span data-stu-id="37bd5-145">yes</span></span> |
| <span data-ttu-id="37bd5-146">Debian</span><span class="sxs-lookup"><span data-stu-id="37bd5-146">Debian</span></span> |<span data-ttu-id="37bd5-147">credativ</span><span class="sxs-lookup"><span data-stu-id="37bd5-147">credativ</span></span> |<span data-ttu-id="37bd5-148">Debian</span><span class="sxs-lookup"><span data-stu-id="37bd5-148">Debian</span></span> |<span data-ttu-id="37bd5-149">8</span><span class="sxs-lookup"><span data-stu-id="37bd5-149">8</span></span> |<span data-ttu-id="37bd5-150">más reciente</span><span class="sxs-lookup"><span data-stu-id="37bd5-150">latest</span></span> |<span data-ttu-id="37bd5-151">no</span><span class="sxs-lookup"><span data-stu-id="37bd5-151">no</span></span> |
| <span data-ttu-id="37bd5-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="37bd5-152">openSUSE</span></span> |<span data-ttu-id="37bd5-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="37bd5-153">SUSE</span></span> |<span data-ttu-id="37bd5-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="37bd5-154">openSUSE</span></span> |<span data-ttu-id="37bd5-155">13.2</span><span class="sxs-lookup"><span data-stu-id="37bd5-155">13.2</span></span> |<span data-ttu-id="37bd5-156">más reciente</span><span class="sxs-lookup"><span data-stu-id="37bd5-156">latest</span></span> |<span data-ttu-id="37bd5-157">no</span><span class="sxs-lookup"><span data-stu-id="37bd5-157">no</span></span> |
| <span data-ttu-id="37bd5-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="37bd5-158">RHEL</span></span> |<span data-ttu-id="37bd5-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="37bd5-159">Redhat</span></span> |<span data-ttu-id="37bd5-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="37bd5-160">RHEL</span></span> |<span data-ttu-id="37bd5-161">7,2</span><span class="sxs-lookup"><span data-stu-id="37bd5-161">7.2</span></span> |<span data-ttu-id="37bd5-162">más reciente</span><span class="sxs-lookup"><span data-stu-id="37bd5-162">latest</span></span> |<span data-ttu-id="37bd5-163">no</span><span class="sxs-lookup"><span data-stu-id="37bd5-163">no</span></span> |
| <span data-ttu-id="37bd5-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="37bd5-164">UbuntuLTS</span></span> |<span data-ttu-id="37bd5-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="37bd5-165">Canonical</span></span> |<span data-ttu-id="37bd5-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="37bd5-166">UbuntuServer</span></span> |<span data-ttu-id="37bd5-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="37bd5-167">14.04.4-LTS</span></span> |<span data-ttu-id="37bd5-168">más reciente</span><span class="sxs-lookup"><span data-stu-id="37bd5-168">latest</span></span> |<span data-ttu-id="37bd5-169">yes</span><span class="sxs-lookup"><span data-stu-id="37bd5-169">yes</span></span> |

<span data-ttu-id="37bd5-170">Trabajamos con nuestros asociados para que cloud-init se incluya y funcione en las imágenes que estos proporcionan a Azure.</span><span class="sxs-lookup"><span data-stu-id="37bd5-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="37bd5-171">Incorporación de un script de cloud-init al proceso de creación de máquinas virtuales con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="37bd5-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="37bd5-172">Para iniciar un script de cloud-init al crear una VM en Azure, especifique el archivo de cloud-init mediante el modificador `--custom-data` de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="37bd5-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="37bd5-173">Cree un grupo de recursos para iniciar máquinas virtuales con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="37bd5-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="37bd5-174">En el ejemplo siguiente se crea el grupo de recursos denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="37bd5-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="37bd5-175">Cree una máquina virtual Linux con [az vm create](/cli/azure/vm#create) mediante cloud-init para configurarla durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="37bd5-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="37bd5-176">Creación de un script de cloud-init para establecer el nombre de host de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="37bd5-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="37bd5-177">Una de las configuraciones más sencillas y más importantes para cualquier VM de Linux sería el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="37bd5-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="37bd5-178">Podemos establecer esto fácilmente mediante cloud-init con este script.</span><span class="sxs-lookup"><span data-stu-id="37bd5-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="37bd5-179">Script de cloud-init de ejemplo denominado `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="37bd5-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="37bd5-180">Durante el primer inicio de la máquina virtual, este script de cloud-init establece el nombre de host en *myservername*.</span><span class="sxs-lookup"><span data-stu-id="37bd5-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="37bd5-181">Cree una máquina virtual Linux con [az vm create](/cli/azure/vm#create) mediante cloud-init para configurarla durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="37bd5-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="37bd5-182">Inicie sesión y compruebe el nombre de host de la nueva VM.</span><span class="sxs-lookup"><span data-stu-id="37bd5-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="37bd5-183">Creación de un script de cloud-init</span><span class="sxs-lookup"><span data-stu-id="37bd5-183">Create a cloud-init script</span></span>
<span data-ttu-id="37bd5-184">Por seguridad, desea que la VM de Ubuntu se actualice en el primer arranque.</span><span class="sxs-lookup"><span data-stu-id="37bd5-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="37bd5-185">Mediante cloud-init podemos hacerlo con el siguiente script, dependiendo de la distribución de Linux que se use.</span><span class="sxs-lookup"><span data-stu-id="37bd5-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="37bd5-186">Script de cloud-init de ejemplo `cloud_config_apt_upgrade.txt` para la familia Debian</span><span class="sxs-lookup"><span data-stu-id="37bd5-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="37bd5-187">Después de iniciarse Linux, se actualizan todos los paquetes instalados a través de **apt-get**.</span><span class="sxs-lookup"><span data-stu-id="37bd5-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="37bd5-188">Cree una máquina virtual Linux con [az vm create](/cli/azure/vm#create) mediante cloud-init para configurarla durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="37bd5-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="37bd5-189">Inicie sesión y compruebe que todos los paquetes se han actualizado.</span><span class="sxs-lookup"><span data-stu-id="37bd5-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="37bd5-190">Creación de un script de cloud-init para agregar un usuario a Linux</span><span class="sxs-lookup"><span data-stu-id="37bd5-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="37bd5-191">Una de las primeras tareas en cualquier máquina virtual Linux nueva consiste en agregar un usuario para usted mismo o para evitar el uso de *root*.</span><span class="sxs-lookup"><span data-stu-id="37bd5-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="37bd5-192">Las claves SSH son el procedimiento recomendado para la seguridad y la facilidad de uso; además, se agregan al archivo *~/.ssh/authorized_keys* con este script de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="37bd5-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="37bd5-193">Script de cloud-init de ejemplo `cloud_config_add_users.txt` para la familia Debian</span><span class="sxs-lookup"><span data-stu-id="37bd5-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="37bd5-194">Una vez que se inicia Linux, todos los usuarios de la lista se crean y se agregan al grupo de sudo.</span><span class="sxs-lookup"><span data-stu-id="37bd5-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="37bd5-195">Cree una máquina virtual Linux con [az vm create](/cli/azure/vm#create) mediante cloud-init para configurarla durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="37bd5-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="37bd5-196">Inicie sesión y compruebe el usuario recién creado.</span><span class="sxs-lookup"><span data-stu-id="37bd5-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="37bd5-197">Salida</span><span class="sxs-lookup"><span data-stu-id="37bd5-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="37bd5-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37bd5-198">Next steps</span></span>
<span data-ttu-id="37bd5-199">Cloud-init se convierte en la manera estándar de modificar la VM Linux en el arranque.</span><span class="sxs-lookup"><span data-stu-id="37bd5-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="37bd5-200">Azure también tiene extensiones de VM, que le permiten modificar su VM Linux en el arranque o mientras está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="37bd5-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="37bd5-201">Por ejemplo, puede usar la extensión VMAccessExtension de Azure para restablecer SSH o la información del usuario mientras la VM está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="37bd5-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="37bd5-202">Con cloud-init, necesitaría reiniciar para restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="37bd5-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="37bd5-203">Acerca de las características y extensiones de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="37bd5-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="37bd5-204">Administración de usuarios, SSH y comprobar o reparar discos en máquinas virtuales de Linux de Azure con la extensión VMAccess</span><span class="sxs-lookup"><span data-stu-id="37bd5-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)