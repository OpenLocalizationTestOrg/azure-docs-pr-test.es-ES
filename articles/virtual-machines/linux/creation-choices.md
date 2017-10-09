---
title: aaaDifferent formas toocreate una VM de Linux en Azure | Microsoft Azure
description: "Obtenga información acerca de maneras diferentes de hello toocreate una máquina virtual de Linux en Azure, incluidos los vínculos tootools y tutoriales para cada método."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="f408a-103">Diferentes maneras toocreate una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="f408a-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="f408a-104">Tiene flexibilidad de hello en Azure toocreate una máquina virtual de Linux (VM) con herramientas y flujos de trabajo tooyou cómodo.</span><span class="sxs-lookup"><span data-stu-id="f408a-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="f408a-105">En este artículo se resume estas diferencias y ejemplos para crear las máquinas virtuales de Linux, incluidas Hola 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f408a-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="f408a-106">También puede ver las opciones de creación incluido hello [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f408a-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="f408a-107">Hola [CLI de Azure 2.0](/cli/azure/install-az-cli2) está disponible en las distintas plataformas a través de un paquete de npm, paquetes suministrados por la distribución o el contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="f408a-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="f408a-108">Instale Hola build más adecuada para su entorno e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="f408a-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="f408a-109">Crear una VM de Linux con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f408a-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="f408a-110">Cree un grupo de recursos con [az group create](/cli/azure/group#create) llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f408a-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="f408a-111">Crear una máquina virtual con [crear vm az](/cli/azure/vm#create) denominado *myVM* utilizando Hola más reciente *UbuntuLTS* de la imagen y generar claves SSH si aún no existen en *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="f408a-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="f408a-112">Creación de una máquina virtual Linux mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="f408a-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="f408a-113">Hello siguiente ejemplo se utiliza [Crear implementación de grupo az](/cli/azure/group/deployment#create) toocreate una máquina virtual desde una plantilla almacenada en GitHub:</span><span class="sxs-lookup"><span data-stu-id="f408a-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="f408a-114">Creación de una máquina virtual Linux y su personalización con cloud-init</span><span class="sxs-lookup"><span data-stu-id="f408a-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="f408a-115">Creación de una aplicación de equilibrio de carga y alta disponibilidad en varias máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="f408a-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="f408a-116">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f408a-116">Azure portal</span></span>
<span data-ttu-id="f408a-117">Hola [portal de Azure](https://portal.azure.com) permite tooquickly crear una máquina virtual porque no hay nada tooinstall en el sistema.</span><span class="sxs-lookup"><span data-stu-id="f408a-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="f408a-118">Use Hola toocreate portal Azure Hola VM:</span><span class="sxs-lookup"><span data-stu-id="f408a-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="f408a-119">Crear una VM de Linux con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f408a-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="f408a-120">Sistema operativo y opciones de imagen</span><span class="sxs-lookup"><span data-stu-id="f408a-120">Operating system and image choices</span></span>
<span data-ttu-id="f408a-121">Al crear una máquina virtual, puede elegir una imagen basada en hello desea toorun de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f408a-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="f408a-122">Azure y sus socios ofrecen muchas imágenes, algunas de las cuales incluyen aplicaciones y herramientas preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="f408a-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="f408a-123">O bien, cargue uno de sus propias imágenes (consulte [Hola después de la sección](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="f408a-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="f408a-124">Imágenes de Azure</span><span class="sxs-lookup"><span data-stu-id="f408a-124">Azure images</span></span>
<span data-ttu-id="f408a-125">Hola de uso [imagen de máquina virtual az](/cli/azure/vm/image) comandos toosee lo que está disponible por publicador, versión de distribución y las compilaciones.</span><span class="sxs-lookup"><span data-stu-id="f408a-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="f408a-126">Lista de publicadores disponibles:</span><span class="sxs-lookup"><span data-stu-id="f408a-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="f408a-127">Lista de productos disponibles (ofertas) de un publicador determinado:</span><span class="sxs-lookup"><span data-stu-id="f408a-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="f408a-128">Lista de SKU disponibles (versiones de distribución) de una oferta determinada:</span><span class="sxs-lookup"><span data-stu-id="f408a-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="f408a-129">Lista de todas las imágenes disponibles para una versión determinada:</span><span class="sxs-lookup"><span data-stu-id="f408a-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="f408a-130">Para obtener más ejemplos sobre cómo examinar y utilizar imágenes disponibles, vea [navegue y seleccione las imágenes de máquina virtual de Azure con hello Azure CLI](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="f408a-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="f408a-131">Hola [crear vm az](/cli/azure/vm#create) comando tiene el alias que se puede utilizar acceso tooquickly Hola distribuciones más comunes y sus versiones más recientes.</span><span class="sxs-lookup"><span data-stu-id="f408a-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="f408a-132">Uso de alias suele ser más rápido que especifica el publicador de hello, oferta, SKU y versión cada vez que cree una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="f408a-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="f408a-133">Alias</span><span class="sxs-lookup"><span data-stu-id="f408a-133">Alias</span></span> | <span data-ttu-id="f408a-134">Publicador</span><span class="sxs-lookup"><span data-stu-id="f408a-134">Publisher</span></span> | <span data-ttu-id="f408a-135">Oferta</span><span class="sxs-lookup"><span data-stu-id="f408a-135">Offer</span></span> | <span data-ttu-id="f408a-136">SKU</span><span class="sxs-lookup"><span data-stu-id="f408a-136">SKU</span></span> | <span data-ttu-id="f408a-137">Versión</span><span class="sxs-lookup"><span data-stu-id="f408a-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="f408a-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="f408a-138">CentOS</span></span> |<span data-ttu-id="f408a-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="f408a-139">OpenLogic</span></span> |<span data-ttu-id="f408a-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="f408a-140">Centos</span></span> |<span data-ttu-id="f408a-141">7,2</span><span class="sxs-lookup"><span data-stu-id="f408a-141">7.2</span></span> |<span data-ttu-id="f408a-142">más reciente</span><span class="sxs-lookup"><span data-stu-id="f408a-142">latest</span></span> |
| <span data-ttu-id="f408a-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f408a-143">CoreOS</span></span> |<span data-ttu-id="f408a-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f408a-144">CoreOS</span></span> |<span data-ttu-id="f408a-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f408a-145">CoreOS</span></span> |<span data-ttu-id="f408a-146">Stable</span><span class="sxs-lookup"><span data-stu-id="f408a-146">Stable</span></span> |<span data-ttu-id="f408a-147">más reciente</span><span class="sxs-lookup"><span data-stu-id="f408a-147">latest</span></span> |
| <span data-ttu-id="f408a-148">Debian</span><span class="sxs-lookup"><span data-stu-id="f408a-148">Debian</span></span> |<span data-ttu-id="f408a-149">credativ</span><span class="sxs-lookup"><span data-stu-id="f408a-149">credativ</span></span> |<span data-ttu-id="f408a-150">Debian</span><span class="sxs-lookup"><span data-stu-id="f408a-150">Debian</span></span> |<span data-ttu-id="f408a-151">8</span><span class="sxs-lookup"><span data-stu-id="f408a-151">8</span></span> |<span data-ttu-id="f408a-152">más reciente</span><span class="sxs-lookup"><span data-stu-id="f408a-152">latest</span></span> |
| <span data-ttu-id="f408a-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f408a-153">openSUSE</span></span> |<span data-ttu-id="f408a-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="f408a-154">SUSE</span></span> |<span data-ttu-id="f408a-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f408a-155">openSUSE</span></span> |<span data-ttu-id="f408a-156">13.2</span><span class="sxs-lookup"><span data-stu-id="f408a-156">13.2</span></span> |<span data-ttu-id="f408a-157">más reciente</span><span class="sxs-lookup"><span data-stu-id="f408a-157">latest</span></span> |
| <span data-ttu-id="f408a-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="f408a-158">RHEL</span></span> |<span data-ttu-id="f408a-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="f408a-159">Redhat</span></span> |<span data-ttu-id="f408a-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="f408a-160">RHEL</span></span> |<span data-ttu-id="f408a-161">7,2</span><span class="sxs-lookup"><span data-stu-id="f408a-161">7.2</span></span> |<span data-ttu-id="f408a-162">más reciente</span><span class="sxs-lookup"><span data-stu-id="f408a-162">latest</span></span> |
| <span data-ttu-id="f408a-163">SLES</span><span class="sxs-lookup"><span data-stu-id="f408a-163">SLES</span></span> |<span data-ttu-id="f408a-164">SLES</span><span class="sxs-lookup"><span data-stu-id="f408a-164">SLES</span></span> |<span data-ttu-id="f408a-165">SLES</span><span class="sxs-lookup"><span data-stu-id="f408a-165">SLES</span></span> |<span data-ttu-id="f408a-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="f408a-166">12-SP1</span></span> |<span data-ttu-id="f408a-167">más reciente</span><span class="sxs-lookup"><span data-stu-id="f408a-167">latest</span></span> |
| <span data-ttu-id="f408a-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="f408a-168">UbuntuLTS</span></span> |<span data-ttu-id="f408a-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="f408a-169">Canonical</span></span> |<span data-ttu-id="f408a-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f408a-170">UbuntuServer</span></span> |<span data-ttu-id="f408a-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="f408a-171">14.04.4-LTS</span></span> |<span data-ttu-id="f408a-172">más reciente</span><span class="sxs-lookup"><span data-stu-id="f408a-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="f408a-173">Uso de su propia imagen</span><span class="sxs-lookup"><span data-stu-id="f408a-173">Use your own image</span></span>
<span data-ttu-id="f408a-174">Si necesita realizar cambios personalizados específicos, use una imagen basada en una máquina virtual de Azure existente; para ello, capture esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f408a-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="f408a-175">También puede cargar una imagen creada de forma local.</span><span class="sxs-lookup"><span data-stu-id="f408a-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="f408a-176">Para obtener más información sobre las distribuciones compatibles y cómo toouse sus propias imágenes, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="f408a-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="f408a-177">Distribuciones aprobadas por Azure</span><span class="sxs-lookup"><span data-stu-id="f408a-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="f408a-178">Información para las distribuciones no aprobadas</span><span class="sxs-lookup"><span data-stu-id="f408a-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="f408a-179">[¿Cómo toocreate una imagen de una máquina virtual de Azure existente](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="f408a-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="f408a-180">Inicio rápido de comandos de ejemplo toocreate una imagen de una máquina virtual de Azure existente:</span><span class="sxs-lookup"><span data-stu-id="f408a-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="f408a-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f408a-181">Next steps</span></span>
* <span data-ttu-id="f408a-182">Crear una VM de Linux con hello [CLI](quick-create-cli.md), de hello [portal](quick-create-portal.md), o mediante un [plantilla de Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f408a-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="f408a-183">Después de crear una máquina virtual Linux, [aprenda sobre los discos y el almacenamiento de Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="f408a-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="f408a-184">Los pasos demasiado rápido[restablecer una contraseña o claves SSH y administrar los usuarios](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f408a-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
