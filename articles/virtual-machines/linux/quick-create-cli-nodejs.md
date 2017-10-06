---
title: "Creación de una máquina virtual Linux mediante la CLI de Azure 1.0 | Microsoft Docs"
description: "Creación de una máquina virtual Linux en Azure mediante la CLI de Azure 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="717e7-103">Creación de una máquina virtual Linux con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="717e7-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="717e7-104">En este artículo se muestra cómo implementar rápidamente una máquina virtual Linux en Azure mediante el comando `azure vm quick-create` en la interfaz de la línea de comandos (CLI) de Azure.</span><span class="sxs-lookup"><span data-stu-id="717e7-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="717e7-105">El comando `quick-create` implementa una máquina virtual dentro de una infraestructura básica y segura que puede usar para crear un prototipo o hacer una prueba de concepto rápidamente.</span><span class="sxs-lookup"><span data-stu-id="717e7-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="717e7-106">Para crear una máquina virtual mediante la CLI de Azure 2.0, consulte [Creación de una máquina virtual con la CLI de Azure](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="717e7-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="717e7-107">También puede implementar rápidamente una máquina virtual Linux mediante [Azure Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="717e7-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="717e7-108">El artículo requiere un [archivo de clave privada y un archivo de clave pública SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="717e7-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="717e7-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="717e7-109">Quick commands</span></span>

<span data-ttu-id="717e7-110">En el ejemplo siguiente se muestra cómo implementar una máquina virtual CoreOS y asociar su clave de Shell seguro (SSH) (los argumentos pueden ser diferentes):</span><span class="sxs-lookup"><span data-stu-id="717e7-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="717e7-111">Tutorial detallado</span><span class="sxs-lookup"><span data-stu-id="717e7-111">Detailed walkthrough</span></span>

<span data-ttu-id="717e7-112">En el tutorial siguiente, se implementa, paso a paso, una máquina virtual UbuntuLTS, con explicaciones de lo que se hace en cada paso.</span><span class="sxs-lookup"><span data-stu-id="717e7-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="717e7-113">Alias de creación rápida para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="717e7-113">VM quick-create aliases</span></span>

<span data-ttu-id="717e7-114">Una forma rápida de elegir una distribución es usar los alias de la CLI de Azure asignados a las distribuciones de sistemas operativos más comunes.</span><span class="sxs-lookup"><span data-stu-id="717e7-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="717e7-115">En la siguiente tabla se enumeran los alias (desde la versión 0.10 de la CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="717e7-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="717e7-116">Todas las implementaciones que usan `quick-create` utilizan de forma predeterminada las máquinas virtuales que están respaldadas por el almacenamiento en una unidad de estado sólido (SSD), lo que proporciona un aprovisionamiento más rápido y un acceso al disco de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="717e7-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="717e7-117">(Estos alias representan una mínima parte de las distribuciones disponibles en Azure.</span><span class="sxs-lookup"><span data-stu-id="717e7-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="717e7-118">Para encontrar más imágenes en Azure Marketplace, [busque una imagen en PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), búsquela [en la Web](https://azure.microsoft.com/marketplace/virtual-machines/) o [cargue su propia imagen personalizada](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="717e7-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="717e7-119">Alias</span><span class="sxs-lookup"><span data-stu-id="717e7-119">Alias</span></span> | <span data-ttu-id="717e7-120">Publicador</span><span class="sxs-lookup"><span data-stu-id="717e7-120">Publisher</span></span> | <span data-ttu-id="717e7-121">Oferta</span><span class="sxs-lookup"><span data-stu-id="717e7-121">Offer</span></span> | <span data-ttu-id="717e7-122">SKU</span><span class="sxs-lookup"><span data-stu-id="717e7-122">SKU</span></span> | <span data-ttu-id="717e7-123">Versión</span><span class="sxs-lookup"><span data-stu-id="717e7-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="717e7-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="717e7-124">CentOS</span></span> |<span data-ttu-id="717e7-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="717e7-125">OpenLogic</span></span> |<span data-ttu-id="717e7-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="717e7-126">CentOS</span></span> |<span data-ttu-id="717e7-127">7,2</span><span class="sxs-lookup"><span data-stu-id="717e7-127">7.2</span></span> |<span data-ttu-id="717e7-128">más reciente</span><span class="sxs-lookup"><span data-stu-id="717e7-128">latest</span></span> |
| <span data-ttu-id="717e7-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="717e7-129">CoreOS</span></span> |<span data-ttu-id="717e7-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="717e7-130">CoreOS</span></span> |<span data-ttu-id="717e7-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="717e7-131">CoreOS</span></span> |<span data-ttu-id="717e7-132">Stable</span><span class="sxs-lookup"><span data-stu-id="717e7-132">Stable</span></span> |<span data-ttu-id="717e7-133">más reciente</span><span class="sxs-lookup"><span data-stu-id="717e7-133">latest</span></span> |
| <span data-ttu-id="717e7-134">Debian</span><span class="sxs-lookup"><span data-stu-id="717e7-134">Debian</span></span> |<span data-ttu-id="717e7-135">credativ</span><span class="sxs-lookup"><span data-stu-id="717e7-135">credativ</span></span> |<span data-ttu-id="717e7-136">Debian</span><span class="sxs-lookup"><span data-stu-id="717e7-136">Debian</span></span> |<span data-ttu-id="717e7-137">8</span><span class="sxs-lookup"><span data-stu-id="717e7-137">8</span></span> |<span data-ttu-id="717e7-138">más reciente</span><span class="sxs-lookup"><span data-stu-id="717e7-138">latest</span></span> |
| <span data-ttu-id="717e7-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="717e7-139">openSUSE</span></span> |<span data-ttu-id="717e7-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="717e7-140">SUSE</span></span> |<span data-ttu-id="717e7-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="717e7-141">openSUSE</span></span> |<span data-ttu-id="717e7-142">13.2</span><span class="sxs-lookup"><span data-stu-id="717e7-142">13.2</span></span> |<span data-ttu-id="717e7-143">más reciente</span><span class="sxs-lookup"><span data-stu-id="717e7-143">latest</span></span> |
| <span data-ttu-id="717e7-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="717e7-144">RHEL</span></span> |<span data-ttu-id="717e7-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="717e7-145">Red Hat</span></span> |<span data-ttu-id="717e7-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="717e7-146">RHEL</span></span> |<span data-ttu-id="717e7-147">7,2</span><span class="sxs-lookup"><span data-stu-id="717e7-147">7.2</span></span> |<span data-ttu-id="717e7-148">más reciente</span><span class="sxs-lookup"><span data-stu-id="717e7-148">latest</span></span> |
| <span data-ttu-id="717e7-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="717e7-149">UbuntuLTS</span></span> |<span data-ttu-id="717e7-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="717e7-150">Canonical</span></span> |<span data-ttu-id="717e7-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="717e7-151">Ubuntu Server</span></span> |<span data-ttu-id="717e7-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="717e7-152">14.04.4-LTS</span></span> |<span data-ttu-id="717e7-153">más reciente</span><span class="sxs-lookup"><span data-stu-id="717e7-153">latest</span></span> |

<span data-ttu-id="717e7-154">En las siguientes secciones, se usa el alias `UbuntuLTS` de la opción **ImageURN** (`-Q`) para implementar una instancia de Ubuntu 14.04.4 LTS Server.</span><span class="sxs-lookup"><span data-stu-id="717e7-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="717e7-155">En el anterior ejemplo `quick-create` solo se llama a la marca `-M` para identificar la clave pública de SSH que se cargará, al tiempo que se deshabilitan las contraseñas de SSH, por lo que se le solicitan los siguientes argumentos:</span><span class="sxs-lookup"><span data-stu-id="717e7-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="717e7-156">El nombre del grupo de recursos (normalmente cualquier cadena vale para el primer grupo de recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="717e7-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="717e7-157">Nombre de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="717e7-157">VM name</span></span>
* <span data-ttu-id="717e7-158">Ubicación (`westus` o `westeurope` son valores predeterminados adecuados).</span><span class="sxs-lookup"><span data-stu-id="717e7-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="717e7-159">Linux (para informar a Azure qué sistema operativo desea).</span><span class="sxs-lookup"><span data-stu-id="717e7-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="717e7-160">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="717e7-160">username</span></span>

<span data-ttu-id="717e7-161">En el ejemplo siguiente se especifican todos los valores para que no sea necesaria ninguna otra solicitud.</span><span class="sxs-lookup"><span data-stu-id="717e7-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="717e7-162">Siempre que tenga un archivo de clave pública `~/.ssh/id_rsa.pub` con formato ssh-rsa, funciona tal cual:</span><span class="sxs-lookup"><span data-stu-id="717e7-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="717e7-163">La salida debe tener un aspecto similar al siguiente bloque de salida:</span><span class="sxs-lookup"><span data-stu-id="717e7-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="717e7-164">Inicio de sesión en la nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="717e7-164">Log in to the new VM</span></span>
<span data-ttu-id="717e7-165">Inicie sesión en la máquina virtual con la dirección IP pública indicada en la salida.</span><span class="sxs-lookup"><span data-stu-id="717e7-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="717e7-166">También puede utilizar el nombre de dominio completo (FQDN) que aparece:</span><span class="sxs-lookup"><span data-stu-id="717e7-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="717e7-167">El proceso de inicio de sesión debe tener un aspecto similar al siguiente bloque de salida:</span><span class="sxs-lookup"><span data-stu-id="717e7-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="717e7-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="717e7-168">Next steps</span></span>
<span data-ttu-id="717e7-169">El comando `azure vm quick-create` es una forma rápida de implementar una máquina virtual para poder iniciar sesión en un shell de Bash y empezar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="717e7-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="717e7-170">Sin embargo, el uso de `vm quick-create` no ofrece un control amplio ni permite crear un entorno más complejo.</span><span class="sxs-lookup"><span data-stu-id="717e7-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="717e7-171">Para implementar una máquina virtual Linux personalizada para su infraestructura, puede seguir cualquiera de estos artículos.</span><span class="sxs-lookup"><span data-stu-id="717e7-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="717e7-172">Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente</span><span class="sxs-lookup"><span data-stu-id="717e7-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="717e7-173">Creación de una máquina virtual Linux protegida con SSH en Azure mediante plantillas</span><span class="sxs-lookup"><span data-stu-id="717e7-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="717e7-174">También puede [usar el controlador `docker-machine` de Azure con diversos comandos para crear rápidamente una máquina virtual Linux como host de docker](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="717e7-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
