---
title: "Diferentes formas de crear una máquina virtual Linux en Azure | Microsoft Azure"
description: "Conozca las distintas formas de crear una máquina virtual Linux en Azure, y obtenga vínculos a herramientas y tutoriales para cada método."
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
ms.openlocfilehash: b2f93579eb1c7a69d0dbd1b0ef112aed9b2168c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-linux-vm"></a><span data-ttu-id="5cdcb-103">Diferentes formas de crear una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="5cdcb-103">Different ways to create a Linux VM</span></span>
<span data-ttu-id="5cdcb-104">En Azure, tiene la flexibilidad crear una máquina virtual Linux con las herramientas y los flujos de trabajo que le resulten cómodos.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="5cdcb-105">En este artículo se resumen estas diferencias y se ofrecen ejemplos para crear máquinas virtuales Linux, que incluyen la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span></span> <span data-ttu-id="5cdcb-106">También puede ver las opciones de creación que se incluye en la [CLI de Azure 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5cdcb-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="5cdcb-107">La [CLI de Azure 2.0](/cli/azure/install-az-cli2) se puede usar en distintas plataformas mediante un paquete de npm, paquetes proporcionados por la distribución o un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="5cdcb-108">Instale la compilación más apropiada para su entorno e inicie sesión en una cuenta de Azure mediante [az login](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="5cdcb-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="5cdcb-109">Creación de una máquina virtual Linux con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="5cdcb-109">Create a Linux VM with the Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="5cdcb-110">Cree un grupo de recursos con [az group create](/cli/azure/group#create) llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="5cdcb-111">Cree una máquina virtual con [az vm create](/cli/azure/vm#create) llamada *myVM* mediante la imagen más reciente de *UbuntuLTS* y genere claves SSH si no existen en *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using the latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="5cdcb-112">Creación de una máquina virtual Linux mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="5cdcb-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="5cdcb-113">En el ejemplo siguiente se usa [az group deployment create](/cli/azure/group/deployment#create) para crear una máquina virtual mediante una plantilla almacenada en GitHub:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-113">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="5cdcb-114">Creación de una máquina virtual Linux y su personalización con cloud-init</span><span class="sxs-lookup"><span data-stu-id="5cdcb-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="5cdcb-115">Creación de una aplicación de equilibrio de carga y alta disponibilidad en varias máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="5cdcb-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="5cdcb-116">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5cdcb-116">Azure portal</span></span>
<span data-ttu-id="5cdcb-117">[Azure Portal](https://portal.azure.com) le permite crear rápidamente una máquina virtual porque no hay nada que instalar en el sistema.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-117">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="5cdcb-118">Use el Portal de Azure para crear la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-118">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="5cdcb-119">Creación de una máquina virtual Linux en Azure mediante el Portal</span><span class="sxs-lookup"><span data-stu-id="5cdcb-119">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="5cdcb-120">Sistema operativo y opciones de imagen</span><span class="sxs-lookup"><span data-stu-id="5cdcb-120">Operating system and image choices</span></span>
<span data-ttu-id="5cdcb-121">Al crear una máquina virtual, elija una imagen basada en el sistema operativo que desee ejecutar.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-121">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="5cdcb-122">Azure y sus socios ofrecen muchas imágenes, algunas de las cuales incluyen aplicaciones y herramientas preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="5cdcb-123">O bien, cargue una de sus propias imágenes (consulte [la siguiente sección](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="5cdcb-123">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="5cdcb-124">Imágenes de Azure</span><span class="sxs-lookup"><span data-stu-id="5cdcb-124">Azure images</span></span>
<span data-ttu-id="5cdcb-125">Los comandos de [az vm image](/cli/azure/vm/image) se usan para ver lo que hay disponible por publicador, versión de distribución y compilaciones.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-125">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="5cdcb-126">Lista de publicadores disponibles:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="5cdcb-127">Lista de productos disponibles (ofertas) de un publicador determinado:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="5cdcb-128">Lista de SKU disponibles (versiones de distribución) de una oferta determinada:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="5cdcb-129">Lista de todas las imágenes disponibles para una versión determinada:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="5cdcb-130">Consulte [Selección de imágenes de máquinas virtuales con la CLI de Azure](cli-ps-findimage.md)para ver ejemplos sobre cómo buscar y usar las imágenes disponibles.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="5cdcb-131">El comando [az vm create](/cli/azure/vm#create) tiene alias que se pueden usar para acceder rápidamente a las distribuciones más comunes y a sus versiones más recientes.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-131">The [az vm create](/cli/azure/vm#create) command has aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="5cdcb-132">Usar alias es más fácil que tener que especificar el publicador, la oferta, el SKU y la versión cada vez que cree una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-132">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="5cdcb-133">Alias</span><span class="sxs-lookup"><span data-stu-id="5cdcb-133">Alias</span></span> | <span data-ttu-id="5cdcb-134">Publicador</span><span class="sxs-lookup"><span data-stu-id="5cdcb-134">Publisher</span></span> | <span data-ttu-id="5cdcb-135">Oferta</span><span class="sxs-lookup"><span data-stu-id="5cdcb-135">Offer</span></span> | <span data-ttu-id="5cdcb-136">SKU</span><span class="sxs-lookup"><span data-stu-id="5cdcb-136">SKU</span></span> | <span data-ttu-id="5cdcb-137">Versión</span><span class="sxs-lookup"><span data-stu-id="5cdcb-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="5cdcb-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="5cdcb-138">CentOS</span></span> |<span data-ttu-id="5cdcb-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="5cdcb-139">OpenLogic</span></span> |<span data-ttu-id="5cdcb-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="5cdcb-140">Centos</span></span> |<span data-ttu-id="5cdcb-141">7,2</span><span class="sxs-lookup"><span data-stu-id="5cdcb-141">7.2</span></span> |<span data-ttu-id="5cdcb-142">más reciente</span><span class="sxs-lookup"><span data-stu-id="5cdcb-142">latest</span></span> |
| <span data-ttu-id="5cdcb-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5cdcb-143">CoreOS</span></span> |<span data-ttu-id="5cdcb-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5cdcb-144">CoreOS</span></span> |<span data-ttu-id="5cdcb-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="5cdcb-145">CoreOS</span></span> |<span data-ttu-id="5cdcb-146">Stable</span><span class="sxs-lookup"><span data-stu-id="5cdcb-146">Stable</span></span> |<span data-ttu-id="5cdcb-147">más reciente</span><span class="sxs-lookup"><span data-stu-id="5cdcb-147">latest</span></span> |
| <span data-ttu-id="5cdcb-148">Debian</span><span class="sxs-lookup"><span data-stu-id="5cdcb-148">Debian</span></span> |<span data-ttu-id="5cdcb-149">credativ</span><span class="sxs-lookup"><span data-stu-id="5cdcb-149">credativ</span></span> |<span data-ttu-id="5cdcb-150">Debian</span><span class="sxs-lookup"><span data-stu-id="5cdcb-150">Debian</span></span> |<span data-ttu-id="5cdcb-151">8</span><span class="sxs-lookup"><span data-stu-id="5cdcb-151">8</span></span> |<span data-ttu-id="5cdcb-152">más reciente</span><span class="sxs-lookup"><span data-stu-id="5cdcb-152">latest</span></span> |
| <span data-ttu-id="5cdcb-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="5cdcb-153">openSUSE</span></span> |<span data-ttu-id="5cdcb-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="5cdcb-154">SUSE</span></span> |<span data-ttu-id="5cdcb-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="5cdcb-155">openSUSE</span></span> |<span data-ttu-id="5cdcb-156">13.2</span><span class="sxs-lookup"><span data-stu-id="5cdcb-156">13.2</span></span> |<span data-ttu-id="5cdcb-157">más reciente</span><span class="sxs-lookup"><span data-stu-id="5cdcb-157">latest</span></span> |
| <span data-ttu-id="5cdcb-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="5cdcb-158">RHEL</span></span> |<span data-ttu-id="5cdcb-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="5cdcb-159">Redhat</span></span> |<span data-ttu-id="5cdcb-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="5cdcb-160">RHEL</span></span> |<span data-ttu-id="5cdcb-161">7,2</span><span class="sxs-lookup"><span data-stu-id="5cdcb-161">7.2</span></span> |<span data-ttu-id="5cdcb-162">más reciente</span><span class="sxs-lookup"><span data-stu-id="5cdcb-162">latest</span></span> |
| <span data-ttu-id="5cdcb-163">SLES</span><span class="sxs-lookup"><span data-stu-id="5cdcb-163">SLES</span></span> |<span data-ttu-id="5cdcb-164">SLES</span><span class="sxs-lookup"><span data-stu-id="5cdcb-164">SLES</span></span> |<span data-ttu-id="5cdcb-165">SLES</span><span class="sxs-lookup"><span data-stu-id="5cdcb-165">SLES</span></span> |<span data-ttu-id="5cdcb-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="5cdcb-166">12-SP1</span></span> |<span data-ttu-id="5cdcb-167">más reciente</span><span class="sxs-lookup"><span data-stu-id="5cdcb-167">latest</span></span> |
| <span data-ttu-id="5cdcb-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="5cdcb-168">UbuntuLTS</span></span> |<span data-ttu-id="5cdcb-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="5cdcb-169">Canonical</span></span> |<span data-ttu-id="5cdcb-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="5cdcb-170">UbuntuServer</span></span> |<span data-ttu-id="5cdcb-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="5cdcb-171">14.04.4-LTS</span></span> |<span data-ttu-id="5cdcb-172">más reciente</span><span class="sxs-lookup"><span data-stu-id="5cdcb-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="5cdcb-173">Uso de su propia imagen</span><span class="sxs-lookup"><span data-stu-id="5cdcb-173">Use your own image</span></span>
<span data-ttu-id="5cdcb-174">Si necesita realizar cambios personalizados específicos, use una imagen basada en una máquina virtual de Azure existente; para ello, capture esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="5cdcb-175">También puede cargar una imagen creada de forma local.</span><span class="sxs-lookup"><span data-stu-id="5cdcb-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="5cdcb-176">Para más información sobre las distribuciones compatibles y cómo usar sus propias imágenes, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-176">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="5cdcb-177">Distribuciones aprobadas por Azure</span><span class="sxs-lookup"><span data-stu-id="5cdcb-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="5cdcb-178">Información para las distribuciones no aprobadas</span><span class="sxs-lookup"><span data-stu-id="5cdcb-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="5cdcb-179">[Creación de una imagen a partir de una máquina virtual de Azure existente](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="5cdcb-179">[How to create an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="5cdcb-180">Comandos de ejemplo de inicio rápido para crear una imagen a partir de una máquina virtual de Azure existente:</span><span class="sxs-lookup"><span data-stu-id="5cdcb-180">Quick-start example commands to create an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="5cdcb-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cdcb-181">Next steps</span></span>
* <span data-ttu-id="5cdcb-182">Cree una máquina virtual Linux desde la [CLI](quick-create-cli.md), desde el [portal](quick-create-portal.md) o mediante una [plantilla de Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5cdcb-182">Create a Linux VM with the [CLI](quick-create-cli.md), from the [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="5cdcb-183">Después de crear una máquina virtual Linux, [aprenda sobre los discos y el almacenamiento de Azure](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="5cdcb-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="5cdcb-184">Pasos rápidos para [restablecer una contraseña o las claves SSH y administrar usuarios](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="5cdcb-184">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
