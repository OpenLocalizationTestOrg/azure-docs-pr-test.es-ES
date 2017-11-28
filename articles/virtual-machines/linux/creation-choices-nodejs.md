---
title: "Diferentes maneras de crear una máquina virtual Linux con la CLI de Azure 1.0 | Documentos de Microsoft"
description: "Conozca las distintas formas de crear una máquina virtual Linux en Azure, y obtenga vínculos a herramientas y tutoriales para cada método."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="32b58-103">Diferentes formas de crear una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="32b58-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="32b58-104">En Azure, tiene la flexibilidad crear una máquina virtual Linux con las herramientas y los flujos de trabajo que le resulten cómodos.</span><span class="sxs-lookup"><span data-stu-id="32b58-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="32b58-105">En este artículo se resumen estas diferencias y se ofrecen ejemplos para crear máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="32b58-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="32b58-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="32b58-106">Azure CLI</span></span>
<span data-ttu-id="32b58-107">En Azure se pueden crear máquinas virtuales con cualquiera de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="32b58-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="32b58-108">CLI de Azure 1.0: la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="32b58-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="32b58-109">[CLI de Azure 2.0 ](../windows/creation-choices.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="32b58-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="32b58-110">La CLI de Azure 1.0 se puede usar en distintas plataformas mediante un paquete de npm, paquetes proporcionados por la distribución o un contenedor de Docker.</span><span class="sxs-lookup"><span data-stu-id="32b58-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="32b58-111">Puede leer más sobre [cómo instalar y configurar la CLI de Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="32b58-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="32b58-112">Los siguientes tutoriales proporcionan ejemplos sobre el uso de la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="32b58-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="32b58-113">Lea cada artículo para más información sobre los comandos de inicio rápido de la CLI mostrados:</span><span class="sxs-lookup"><span data-stu-id="32b58-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="32b58-114">Creación de una máquina virtual con Linux en Azure mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="32b58-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="32b58-115">En el ejemplo siguiente se crea una máquina virtual de CoreOS con una clave pública llamada *azure_id_rsa.pub*:</span><span class="sxs-lookup"><span data-stu-id="32b58-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="32b58-116">Creación de una VM de Linux protegida mediante una plantilla de Azure</span><span class="sxs-lookup"><span data-stu-id="32b58-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="32b58-117">En el ejemplo siguiente se crea una máquina virtual mediante una plantilla almacenada en GitHub:</span><span class="sxs-lookup"><span data-stu-id="32b58-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="32b58-118">Creación de un entorno de Linux completo mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="32b58-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="32b58-119">Incluye la creación de un equilibrador de carga y varias máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="32b58-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="32b58-120">Adición de un disco a una máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="32b58-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="32b58-121">En el ejemplo siguiente se agrega un disco de *5* GB a una máquina virtual existente llamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="32b58-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="32b58-122">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="32b58-122">Azure portal</span></span>
<span data-ttu-id="32b58-123">[Azure Portal](https://portal.azure.com) le permite crear rápidamente una máquina virtual porque no hay nada que instalar en el sistema.</span><span class="sxs-lookup"><span data-stu-id="32b58-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="32b58-124">Use el Portal de Azure para crear la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="32b58-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="32b58-125">Creación de una máquina virtual Linux en Azure mediante el Portal</span><span class="sxs-lookup"><span data-stu-id="32b58-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="32b58-126">Sistema operativo y opciones de imagen</span><span class="sxs-lookup"><span data-stu-id="32b58-126">Operating system and image choices</span></span>
<span data-ttu-id="32b58-127">Al crear una máquina virtual, elija una imagen basada en el sistema operativo que desee ejecutar.</span><span class="sxs-lookup"><span data-stu-id="32b58-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="32b58-128">Azure y sus socios ofrecen muchas imágenes, algunas de las cuales incluyen aplicaciones y herramientas preinstaladas.</span><span class="sxs-lookup"><span data-stu-id="32b58-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="32b58-129">O bien, cargue una de sus propias imágenes (consulte [la siguiente sección](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="32b58-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="32b58-130">Imágenes de Azure</span><span class="sxs-lookup"><span data-stu-id="32b58-130">Azure images</span></span>
<span data-ttu-id="32b58-131">Puede usar los comandos de la CLI `azure vm image` para ver lo que hay disponible por publicador, versión de distribución y compilaciones.</span><span class="sxs-lookup"><span data-stu-id="32b58-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="32b58-132">Lista de publicadores disponibles:</span><span class="sxs-lookup"><span data-stu-id="32b58-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="32b58-133">Lista de productos disponibles (ofertas) de un publicador determinado:</span><span class="sxs-lookup"><span data-stu-id="32b58-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="32b58-134">Lista de SKU disponibles (versiones de distribución) de una oferta determinada:</span><span class="sxs-lookup"><span data-stu-id="32b58-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="32b58-135">Lista de todas las imágenes disponibles para una versión determinada:</span><span class="sxs-lookup"><span data-stu-id="32b58-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="32b58-136">Los comandos `azure vm quick-create` y `azure vm create` tienen alias que se pueden usar para acceder rápidamente a las distribuciones más comunes y sus versiones más recientes.</span><span class="sxs-lookup"><span data-stu-id="32b58-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="32b58-137">Usar alias es más fácil que tener que especificar el publicador, la oferta, el SKU y la versión cada vez que cree una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="32b58-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="32b58-138">Alias</span><span class="sxs-lookup"><span data-stu-id="32b58-138">Alias</span></span> | <span data-ttu-id="32b58-139">Publicador</span><span class="sxs-lookup"><span data-stu-id="32b58-139">Publisher</span></span> | <span data-ttu-id="32b58-140">Oferta</span><span class="sxs-lookup"><span data-stu-id="32b58-140">Offer</span></span> | <span data-ttu-id="32b58-141">SKU</span><span class="sxs-lookup"><span data-stu-id="32b58-141">SKU</span></span> | <span data-ttu-id="32b58-142">Versión</span><span class="sxs-lookup"><span data-stu-id="32b58-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="32b58-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="32b58-143">CentOS</span></span> |<span data-ttu-id="32b58-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="32b58-144">OpenLogic</span></span> |<span data-ttu-id="32b58-145">CentOS</span><span class="sxs-lookup"><span data-stu-id="32b58-145">Centos</span></span> |<span data-ttu-id="32b58-146">7,2</span><span class="sxs-lookup"><span data-stu-id="32b58-146">7.2</span></span> |<span data-ttu-id="32b58-147">más reciente</span><span class="sxs-lookup"><span data-stu-id="32b58-147">latest</span></span> |
| <span data-ttu-id="32b58-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="32b58-148">CoreOS</span></span> |<span data-ttu-id="32b58-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="32b58-149">CoreOS</span></span> |<span data-ttu-id="32b58-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="32b58-150">CoreOS</span></span> |<span data-ttu-id="32b58-151">Stable</span><span class="sxs-lookup"><span data-stu-id="32b58-151">Stable</span></span> |<span data-ttu-id="32b58-152">más reciente</span><span class="sxs-lookup"><span data-stu-id="32b58-152">latest</span></span> |
| <span data-ttu-id="32b58-153">Debian</span><span class="sxs-lookup"><span data-stu-id="32b58-153">Debian</span></span> |<span data-ttu-id="32b58-154">credativ</span><span class="sxs-lookup"><span data-stu-id="32b58-154">credativ</span></span> |<span data-ttu-id="32b58-155">Debian</span><span class="sxs-lookup"><span data-stu-id="32b58-155">Debian</span></span> |<span data-ttu-id="32b58-156">8</span><span class="sxs-lookup"><span data-stu-id="32b58-156">8</span></span> |<span data-ttu-id="32b58-157">más reciente</span><span class="sxs-lookup"><span data-stu-id="32b58-157">latest</span></span> |
| <span data-ttu-id="32b58-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="32b58-158">openSUSE</span></span> |<span data-ttu-id="32b58-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="32b58-159">SUSE</span></span> |<span data-ttu-id="32b58-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="32b58-160">openSUSE</span></span> |<span data-ttu-id="32b58-161">13.2</span><span class="sxs-lookup"><span data-stu-id="32b58-161">13.2</span></span> |<span data-ttu-id="32b58-162">más reciente</span><span class="sxs-lookup"><span data-stu-id="32b58-162">latest</span></span> |
| <span data-ttu-id="32b58-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="32b58-163">RHEL</span></span> |<span data-ttu-id="32b58-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="32b58-164">Redhat</span></span> |<span data-ttu-id="32b58-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="32b58-165">RHEL</span></span> |<span data-ttu-id="32b58-166">7,2</span><span class="sxs-lookup"><span data-stu-id="32b58-166">7.2</span></span> |<span data-ttu-id="32b58-167">más reciente</span><span class="sxs-lookup"><span data-stu-id="32b58-167">latest</span></span> |
| <span data-ttu-id="32b58-168">SLES</span><span class="sxs-lookup"><span data-stu-id="32b58-168">SLES</span></span> |<span data-ttu-id="32b58-169">SLES</span><span class="sxs-lookup"><span data-stu-id="32b58-169">SLES</span></span> |<span data-ttu-id="32b58-170">SLES</span><span class="sxs-lookup"><span data-stu-id="32b58-170">SLES</span></span> |<span data-ttu-id="32b58-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="32b58-171">12-SP1</span></span> |<span data-ttu-id="32b58-172">más reciente</span><span class="sxs-lookup"><span data-stu-id="32b58-172">latest</span></span> |
| <span data-ttu-id="32b58-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="32b58-173">UbuntuLTS</span></span> |<span data-ttu-id="32b58-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="32b58-174">Canonical</span></span> |<span data-ttu-id="32b58-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="32b58-175">UbuntuServer</span></span> |<span data-ttu-id="32b58-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="32b58-176">14.04.4-LTS</span></span> |<span data-ttu-id="32b58-177">más reciente</span><span class="sxs-lookup"><span data-stu-id="32b58-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="32b58-178">Uso de su propia imagen</span><span class="sxs-lookup"><span data-stu-id="32b58-178">Use your own image</span></span>
<span data-ttu-id="32b58-179">Si necesita realizar cambios personalizados específicos, use una imagen basada en una máquina virtual de Azure existente; para ello, *capture* esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="32b58-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="32b58-180">También puede cargar una imagen creada de forma local.</span><span class="sxs-lookup"><span data-stu-id="32b58-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="32b58-181">Para más información sobre las distribuciones compatibles y cómo usar sus propias imágenes, consulte los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="32b58-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="32b58-182">Distribuciones aprobadas por Azure</span><span class="sxs-lookup"><span data-stu-id="32b58-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="32b58-183">Información para las distribuciones no aprobadas</span><span class="sxs-lookup"><span data-stu-id="32b58-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="32b58-184">Carga y creación de una máquina virtual Linux desde una imagen de disco personalizada</span><span class="sxs-lookup"><span data-stu-id="32b58-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="32b58-185">[Captura de una máquina virtual Linux para usarla como plantilla de Resource Manager](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="32b58-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="32b58-186">Comandos de ejemplo para capturar una máquina virtual existente:</span><span class="sxs-lookup"><span data-stu-id="32b58-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="32b58-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32b58-187">Next steps</span></span>
* <span data-ttu-id="32b58-188">Cree una máquina virtual Linux desde el [portal](quick-create-portal.md), con la [CLI](quick-create-cli.md) o mediante una [plantilla de Azure Resource Manager](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="32b58-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="32b58-189">Después de crear una máquina virtual Linux, [agregue un disco de datos](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="32b58-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="32b58-190">Pasos rápidos para [restablecer una contraseña o las claves SSH y administrar usuarios](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="32b58-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

