---
title: "Ejecución de Linux en nodos de proceso de máquinas virtuales - Azure Batch | Microsoft Docs"
description: "Obtenga información acerca de cómo procesar las cargas de trabajo de proceso paralelas en grupos de máquinas virtuales de Linux en el servicio Lote de Azure."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b2257917e2368478beb75957677de23d4157865
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="6033b-103">Aprovisionamiento de nodos de proceso de Linux en grupos de Batch</span><span class="sxs-lookup"><span data-stu-id="6033b-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="6033b-104">Puede usar el servicio Lote de Azure para ejecutar cargas de trabajo de proceso paralelas en máquinas virtuales Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="6033b-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="6033b-105">Este artículo detalla cómo crear grupos de nodos de proceso de Linux en el servicio Lote mediante las bibliotecas de cliente de [Python de Lote][py_batch_package] y [.NET de Lote][api_net].</span><span class="sxs-lookup"><span data-stu-id="6033b-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="6033b-106">Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="6033b-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="6033b-107">Se admiten en los grupos de Batch creados entre el 10 de marzo de 2016 y el 5 de julio de 2017 únicamente si el grupo se creó mediante una configuración de Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="6033b-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="6033b-108">Los grupos de Batch creados antes del 10 de marzo de 2016 no admiten los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6033b-108">Batch pools created prior to 10 March 2016 do not support application packages.</span></span> <span data-ttu-id="6033b-109">Para más información sobre el uso de los paquetes de aplicación para implementar las aplicaciones en los nodos de Batch, consulte [Implementación de aplicaciones en nodos de proceso con paquetes de aplicaciones de Batch](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6033b-109">For more information about using application packages to deploy your applications to your Batch nodes, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="6033b-110">Configuración de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6033b-110">Virtual machine configuration</span></span>
<span data-ttu-id="6033b-111">Cuando crea un grupo de nodos de proceso en el servicio Lote, tiene dos opciones para seleccionar el sistema operativo y el tamaño de nodo: configuración de servicios en la nube y configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6033b-111">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="6033b-112">**configuración de Servicios en la nube**  *solo*.</span><span class="sxs-lookup"><span data-stu-id="6033b-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="6033b-113">Los tamaños de nodos de proceso disponibles se muestran en [Tamaños de los servicios en la nube](../cloud-services/cloud-services-sizes-specs.md) y los sistemas operativos disponibles se enumeran en [Matriz de compatibilidad del SDK y versiones del SO invitado de Azure](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="6033b-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="6033b-114">Al crear un grupo que contiene nodos de Azure Cloud Services, debe especificar el tamaño del nodo y la familia del SO, que se describen en los artículos mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6033b-114">When you create a pool that contains Azure Cloud Services nodes, you specify the node size and the OS family, which are described in the previously mentioned articles.</span></span> <span data-ttu-id="6033b-115">Para los grupos de nodos de proceso de Windows, la mayoría de las veces se utilizan los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="6033b-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="6033b-116">**Configuración de la máquina virtual** proporciona imágenes de Linux y Windows para los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="6033b-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="6033b-117">Los tamaños de nodos de proceso disponibles se muestran en [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [Tamaños de las máquinas virtuales Windows en Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6033b-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="6033b-118">Cuando se crea un grupo que contiene los nodos de configuración de la máquina virtual, debe especificar su tamaño, la referencia de la imagen de máquina virtual y el SKU del agente de nodo del servicio Lote que desea instalar en los nodos.</span><span class="sxs-lookup"><span data-stu-id="6033b-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="6033b-119">Referencia de imagen de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6033b-119">Virtual machine image reference</span></span>
<span data-ttu-id="6033b-120">El servicio de Batch usa [conjuntos de escalado de máquinas virtuales](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) para proporcionar nodos de proceso de Linux.</span><span class="sxs-lookup"><span data-stu-id="6033b-120">The Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide Linux compute nodes.</span></span> <span data-ttu-id="6033b-121">Puede especificar una imagen de [Azure Marketplace][vm_marketplace] o proporcionar una imagen personalizada que haya preparado.</span><span class="sxs-lookup"><span data-stu-id="6033b-121">You can specify an image from the [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="6033b-122">Para más información acerca de las imágenes personalizadas, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="6033b-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="6033b-123">Al configurar una referencia de la imagen de máquina virtual, especifique las propiedades de la imagen de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6033b-123">When you configure a virtual machine image reference, you specify the properties of the virtual machine image.</span></span> <span data-ttu-id="6033b-124">Las propiedades siguientes son necesarias cuando se crea una referencia de la imagen de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="6033b-124">The following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="6033b-125">**Propiedades de la referencia de la imagen**</span><span class="sxs-lookup"><span data-stu-id="6033b-125">**Image reference properties**</span></span> | <span data-ttu-id="6033b-126">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="6033b-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="6033b-127">Publicador</span><span class="sxs-lookup"><span data-stu-id="6033b-127">Publisher</span></span> |<span data-ttu-id="6033b-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="6033b-128">Canonical</span></span> |
| <span data-ttu-id="6033b-129">Oferta</span><span class="sxs-lookup"><span data-stu-id="6033b-129">Offer</span></span> |<span data-ttu-id="6033b-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6033b-130">UbuntuServer</span></span> |
| <span data-ttu-id="6033b-131">SKU</span><span class="sxs-lookup"><span data-stu-id="6033b-131">SKU</span></span> |<span data-ttu-id="6033b-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="6033b-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="6033b-133">Versión</span><span class="sxs-lookup"><span data-stu-id="6033b-133">Version</span></span> |<span data-ttu-id="6033b-134">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="6033b-135">Puede obtener más información sobre estas propiedades y cómo mostrar imágenes de Marketplace en [Navegación y selección de las imágenes de máquina virtual Linux en Azure con la CLI o PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6033b-135">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6033b-136">Tenga en cuenta que no todas las imágenes de Marketplace son actualmente compatibles con el servicio Lote.</span><span class="sxs-lookup"><span data-stu-id="6033b-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="6033b-137">Para más información, consulte [SKU del agente de nodo](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="6033b-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="6033b-138">SKU del agente de nodo</span><span class="sxs-lookup"><span data-stu-id="6033b-138">Node agent SKU</span></span>
<span data-ttu-id="6033b-139">El agente de nodo del servicio Lote es un programa que se ejecuta en cada nodo del grupo y proporciona la interfaz de comandos y control entre el nodo y el servicio.</span><span class="sxs-lookup"><span data-stu-id="6033b-139">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="6033b-140">Hay diferentes implementaciones del agente de nodo, conocidas como SKU, para distintos sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="6033b-140">There are different implementations of the node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="6033b-141">Básicamente, al crear una configuración de la máquina virtual, debe especificar primero la referencia de la imagen de máquina virtual y, después, el agente de nodo que se va a instalar en la imagen.</span><span class="sxs-lookup"><span data-stu-id="6033b-141">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span></span> <span data-ttu-id="6033b-142">Normalmente, cada SKU del agente de nodo es compatible con varias imágenes de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6033b-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="6033b-143">Estos son algunos ejemplos de SKU del agente de nodo:</span><span class="sxs-lookup"><span data-stu-id="6033b-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="6033b-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6033b-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="6033b-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-145">batch.node.centos 7</span></span>
* <span data-ttu-id="6033b-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6033b-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6033b-147">No todas las imágenes de máquinas virtuales que están disponibles en Marketplace son compatibles con los agentes de nodo de Lote disponibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="6033b-147">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span></span> <span data-ttu-id="6033b-148">Use los SDK de Batch para mostrar las SKU del agente de nodo disponibles y las imágenes de máquina virtual con las que son compatibles.</span><span class="sxs-lookup"><span data-stu-id="6033b-148">Use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span></span> <span data-ttu-id="6033b-149">Consulte la [lista de imágenes de máquinas virtuales](#list-of-virtual-machine-images), que se detalla más adelante en este artículo, para obtener más información y ejemplos sobre cómo recuperar una lista de imágenes válidas en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6033b-149">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how to retrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="6033b-150">Cree un grupo de Linux: Python de Lote</span><span class="sxs-lookup"><span data-stu-id="6033b-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="6033b-151">El fragmento de código siguiente muestra un ejemplo de cómo usar la [biblioteca de cliente de Lote de Microsoft Azure para Python][py_batch_package] para crear un grupo de nodos de proceso del servidor de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6033b-151">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="6033b-152">Puede encontrar la documentación de referencia del módulo de Python de Batch en [azure.batch package][py_batch_docs] (sección Lea los documentos).</span><span class="sxs-lookup"><span data-stu-id="6033b-152">Reference documentation for the Batch Python module can be found at [azure.batch package][py_batch_docs] on Read the Docs.</span></span>

<span data-ttu-id="6033b-153">En este fragmento de código, se crea una [ImageReference][py_imagereference] explícitamente y se especifica cada una de sus propiedades (publicador, oferta, SKU, versión).</span><span class="sxs-lookup"><span data-stu-id="6033b-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="6033b-154">No obstante, en el código de producción recomendamos usar el método [list_node_agent_skus][py_list_skus] para determinar y seleccionar entre las combinaciones disponibles de SKU del agente de nodo y las imágenes en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="6033b-154">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span></span>

```python
# Import the required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize the Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure the start task for the pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies the Marketplace
# virtual machine image to install on the nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="6033b-155">Tal y como se mencionó anteriormente, es recomendable que en lugar de crear una [ImageReference][py_imagereference] explícitamente, utilice el método [list_node_agent_skus][py_list_skus] para seleccionar dinámicamente entre las combinaciones de imágenes de Marketplace y los agentes de nodo admitidas actualmente.</span><span class="sxs-lookup"><span data-stu-id="6033b-155">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="6033b-156">El siguiente fragmento de código de Python muestra cómo usar este método.</span><span class="sxs-lookup"><span data-stu-id="6033b-156">The following Python snippet shows how to use this method.</span></span>

```python
# Get the list of node agents from the Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain the desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick the first image reference from the list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create the VirtualMachineConfiguration, specifying the VM image
# reference and the Batch node agent to be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="6033b-157">Cree un grupo de Linux: .NET de Lote</span><span class="sxs-lookup"><span data-stu-id="6033b-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="6033b-158">El fragmento de código siguiente muestra un ejemplo de cómo utilizar la biblioteca de cliente [.NET de lote][nuget_batch_net] para crear un grupo de nodos de proceso del servidor de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6033b-158">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="6033b-159">Puede encontrar la [documentación de referencia de .NET de Lote][api_net] en MSDN.</span><span class="sxs-lookup"><span data-stu-id="6033b-159">You can find the [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="6033b-160">El fragmento de código siguiente utiliza el método [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] para seleccionar entre la lista de combinaciones de imágenes de Marketplace y SKU del agente de nodo admitidas actualmente.</span><span class="sxs-lookup"><span data-stu-id="6033b-160">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="6033b-161">Esta técnica es deseable porque la lista de combinaciones admitidas puede cambiar de vez en cuando.</span><span class="sxs-lookup"><span data-stu-id="6033b-161">This technique is desirable because the list of supported combinations may change from time to time.</span></span> <span data-ttu-id="6033b-162">Normalmente, se agregan las combinaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="6033b-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us to select from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image
// that we wish to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the VirtualMachineConfiguration for use when actually
// creating the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create the unbound pool object using the VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit the pool to the Batch service
await pool.CommitAsync();
```

<span data-ttu-id="6033b-163">Aunque el fragmento de código anterior usa el método [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] para mostrar y seleccionar entre las combinaciones admitidas de imágenes y SKU del agente de nodo (recomendadas), también puede configurar una [ImageReference][net_imagereference] explícitamente:</span><span class="sxs-lookup"><span data-stu-id="6033b-163">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="6033b-164">Lista de imágenes de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="6033b-164">List of virtual machine images</span></span>
<span data-ttu-id="6033b-165">En la tabla siguiente se enumeran las imágenes de máquinas virtuales de Marketplace que son compatibles con los agentes de nodo de Lote disponibles cuando se actualizó por última vez este artículo.</span><span class="sxs-lookup"><span data-stu-id="6033b-165">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="6033b-166">Es importante tener en cuenta que esta lista no es definitiva, ya que se pueden agregar o quitar imágenes y agentes de nodo en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="6033b-166">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="6033b-167">Se recomienda que los servicios y aplicaciones de Lote utilicen siempre los métodos [list_node_agent_skus][py_list_skus] (Python) y [ListNodeAgentSkus][net_list_skus] (.NET de Lote) para determinar y seleccionar entre las SKU disponibles.</span><span class="sxs-lookup"><span data-stu-id="6033b-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="6033b-168">La siguiente lista se puede cambiar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="6033b-168">The following list may change at any time.</span></span> <span data-ttu-id="6033b-169">Use siempre los métodos **list_node_agent_SKU** disponibles en las API de Batch para mostrar los SKU de máquina virtual y del agente de nodo disponibles al ejecutar los trabajos de Batch.</span><span class="sxs-lookup"><span data-stu-id="6033b-169">Always use the **list node agent SKU** methods available in the Batch APIs to list the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="6033b-170">**Publicador**</span><span class="sxs-lookup"><span data-stu-id="6033b-170">**Publisher**</span></span> | <span data-ttu-id="6033b-171">**Oferta**</span><span class="sxs-lookup"><span data-stu-id="6033b-171">**Offer**</span></span> | <span data-ttu-id="6033b-172">**SKU de imagen**</span><span class="sxs-lookup"><span data-stu-id="6033b-172">**Image SKU**</span></span> | <span data-ttu-id="6033b-173">**Versión**</span><span class="sxs-lookup"><span data-stu-id="6033b-173">**Version**</span></span> | <span data-ttu-id="6033b-174">**Identificador de SKU del agente de nodo**</span><span class="sxs-lookup"><span data-stu-id="6033b-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="6033b-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="6033b-175">Canonical</span></span> | <span data-ttu-id="6033b-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6033b-176">UbuntuServer</span></span> | <span data-ttu-id="6033b-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="6033b-177">14.04.5-LTS</span></span> | <span data-ttu-id="6033b-178">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-178">latest</span></span> | <span data-ttu-id="6033b-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6033b-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="6033b-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="6033b-180">Canonical</span></span> | <span data-ttu-id="6033b-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6033b-181">UbuntuServer</span></span> | <span data-ttu-id="6033b-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="6033b-182">16.04.0-LTS</span></span> | <span data-ttu-id="6033b-183">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-183">latest</span></span> | <span data-ttu-id="6033b-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6033b-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="6033b-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="6033b-185">Credativ</span></span> | <span data-ttu-id="6033b-186">Debian</span><span class="sxs-lookup"><span data-stu-id="6033b-186">Debian</span></span> | <span data-ttu-id="6033b-187">8</span><span class="sxs-lookup"><span data-stu-id="6033b-187">8</span></span> | <span data-ttu-id="6033b-188">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-188">latest</span></span> | <span data-ttu-id="6033b-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="6033b-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="6033b-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6033b-190">OpenLogic</span></span> | <span data-ttu-id="6033b-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="6033b-191">CentOS</span></span> | <span data-ttu-id="6033b-192">7.0</span><span class="sxs-lookup"><span data-stu-id="6033b-192">7.0</span></span> | <span data-ttu-id="6033b-193">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-193">latest</span></span> | <span data-ttu-id="6033b-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="6033b-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6033b-195">OpenLogic</span></span> | <span data-ttu-id="6033b-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="6033b-196">CentOS</span></span> | <span data-ttu-id="6033b-197">7.1</span><span class="sxs-lookup"><span data-stu-id="6033b-197">7.1</span></span> | <span data-ttu-id="6033b-198">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-198">latest</span></span> | <span data-ttu-id="6033b-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="6033b-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6033b-200">OpenLogic</span></span> | <span data-ttu-id="6033b-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="6033b-201">CentOS-HPC</span></span> | <span data-ttu-id="6033b-202">7.1</span><span class="sxs-lookup"><span data-stu-id="6033b-202">7.1</span></span> | <span data-ttu-id="6033b-203">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-203">latest</span></span> | <span data-ttu-id="6033b-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="6033b-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6033b-205">OpenLogic</span></span> | <span data-ttu-id="6033b-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="6033b-206">CentOS</span></span> | <span data-ttu-id="6033b-207">7,2</span><span class="sxs-lookup"><span data-stu-id="6033b-207">7.2</span></span> | <span data-ttu-id="6033b-208">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-208">latest</span></span> | <span data-ttu-id="6033b-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="6033b-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="6033b-210">Oracle</span></span> | <span data-ttu-id="6033b-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="6033b-211">Oracle-Linux</span></span> | <span data-ttu-id="6033b-212">7.0</span><span class="sxs-lookup"><span data-stu-id="6033b-212">7.0</span></span> | <span data-ttu-id="6033b-213">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-213">latest</span></span> | <span data-ttu-id="6033b-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="6033b-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="6033b-215">Oracle</span></span> | <span data-ttu-id="6033b-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="6033b-216">Oracle-Linux</span></span> | <span data-ttu-id="6033b-217">7,2</span><span class="sxs-lookup"><span data-stu-id="6033b-217">7.2</span></span> | <span data-ttu-id="6033b-218">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-218">latest</span></span> | <span data-ttu-id="6033b-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="6033b-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="6033b-220">SUSE</span></span> | <span data-ttu-id="6033b-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6033b-221">openSUSE</span></span> | <span data-ttu-id="6033b-222">13.2</span><span class="sxs-lookup"><span data-stu-id="6033b-222">13.2</span></span> | <span data-ttu-id="6033b-223">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-223">latest</span></span> | <span data-ttu-id="6033b-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="6033b-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="6033b-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="6033b-225">SUSE</span></span> | <span data-ttu-id="6033b-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="6033b-226">openSUSE-Leap</span></span> | <span data-ttu-id="6033b-227">42.1</span><span class="sxs-lookup"><span data-stu-id="6033b-227">42.1</span></span> | <span data-ttu-id="6033b-228">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-228">latest</span></span> | <span data-ttu-id="6033b-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6033b-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6033b-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="6033b-230">SUSE</span></span> | <span data-ttu-id="6033b-231">SLES</span><span class="sxs-lookup"><span data-stu-id="6033b-231">SLES</span></span> | <span data-ttu-id="6033b-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="6033b-232">12-SP1</span></span> | <span data-ttu-id="6033b-233">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-233">latest</span></span> | <span data-ttu-id="6033b-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6033b-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6033b-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="6033b-235">SUSE</span></span> | <span data-ttu-id="6033b-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="6033b-236">SLES-HPC</span></span> | <span data-ttu-id="6033b-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="6033b-237">12-SP1</span></span> | <span data-ttu-id="6033b-238">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-238">latest</span></span> | <span data-ttu-id="6033b-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6033b-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6033b-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="6033b-240">microsoft-ads</span></span> | <span data-ttu-id="6033b-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="6033b-241">linux-data-science-vm</span></span> | <span data-ttu-id="6033b-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="6033b-242">linuxdsvm</span></span> | <span data-ttu-id="6033b-243">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-243">latest</span></span> | <span data-ttu-id="6033b-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6033b-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="6033b-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="6033b-245">microsoft-ads</span></span> | <span data-ttu-id="6033b-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="6033b-246">standard-data-science-vm</span></span> | <span data-ttu-id="6033b-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="6033b-247">standard-data-science-vm</span></span> | <span data-ttu-id="6033b-248">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-248">latest</span></span> | <span data-ttu-id="6033b-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6033b-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6033b-250">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6033b-251">Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-251">WindowsServer</span></span> | <span data-ttu-id="6033b-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="6033b-252">2008-R2-SP1</span></span> | <span data-ttu-id="6033b-253">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-253">latest</span></span> | <span data-ttu-id="6033b-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6033b-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6033b-255">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6033b-256">Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-256">WindowsServer</span></span> | <span data-ttu-id="6033b-257">Centro de datos de 2012</span><span class="sxs-lookup"><span data-stu-id="6033b-257">2012-Datacenter</span></span> | <span data-ttu-id="6033b-258">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-258">latest</span></span> | <span data-ttu-id="6033b-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6033b-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6033b-260">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6033b-261">Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-261">WindowsServer</span></span> | <span data-ttu-id="6033b-262">Centro de datos de 2012-R2</span><span class="sxs-lookup"><span data-stu-id="6033b-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="6033b-263">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-263">latest</span></span> | <span data-ttu-id="6033b-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6033b-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6033b-265">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6033b-266">Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-266">WindowsServer</span></span> | <span data-ttu-id="6033b-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="6033b-267">2016-Datacenter</span></span> | <span data-ttu-id="6033b-268">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-268">latest</span></span> | <span data-ttu-id="6033b-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6033b-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6033b-270">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6033b-271">Windows Server</span><span class="sxs-lookup"><span data-stu-id="6033b-271">WindowsServer</span></span> | <span data-ttu-id="6033b-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="6033b-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="6033b-273">más reciente</span><span class="sxs-lookup"><span data-stu-id="6033b-273">latest</span></span> | <span data-ttu-id="6033b-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6033b-274">batch.node.windows amd64</span></span> |

## <a name="connect-to-linux-nodes-using-ssh"></a><span data-ttu-id="6033b-275">Conexión a los nodos de Linux mediante SSH</span><span class="sxs-lookup"><span data-stu-id="6033b-275">Connect to Linux nodes using SSH</span></span>
<span data-ttu-id="6033b-276">Durante el desarrollo o solución de problemas, es posible que necesite iniciar sesión en los nodos del grupo.</span><span class="sxs-lookup"><span data-stu-id="6033b-276">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span></span> <span data-ttu-id="6033b-277">A diferencia de los nodos de proceso de Windows, no puede utilizar el protocolo de escritorio remoto (RDP) para conectarse a los nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="6033b-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span></span> <span data-ttu-id="6033b-278">En su lugar, el servicio de Lote habilita el acceso SSH en cada nodo para la conexión remota.</span><span class="sxs-lookup"><span data-stu-id="6033b-278">Instead, the Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="6033b-279">El siguiente fragmento de código de Python crea un usuario en cada nodo de un grupo, que es necesario para la conexión remota.</span><span class="sxs-lookup"><span data-stu-id="6033b-279">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="6033b-280">A continuación, imprime la información de conexión de SSH para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="6033b-280">It then prints the secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify the ID of an existing pool containing Linux nodes
# currently in the 'idle' state
pool_id = ''

# Specify the username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create the user that will be added to each node in the pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get the list of nodes in the pool
nodes = batch_client.compute_node.list(pool_id)

# Add the user to each node in the pool and print
# the connection information for the node
for node in nodes:
    # Add the user to the node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for the node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print the connection info for the node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="6033b-281">Este es un ejemplo de resultado del código anterior para un grupo que contiene cuatro nodos de Linux:</span><span class="sxs-lookup"><span data-stu-id="6033b-281">Here is sample output for the previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="6033b-282">En lugar de una contraseña, puede especificar una clave pública SSH al crear un usuario en un nodo.</span><span class="sxs-lookup"><span data-stu-id="6033b-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="6033b-283">En el SDK de Python, use el parámetro **ssh_public_key** en [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="6033b-283">In the Python SDK, use the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="6033b-284">En .NET, use la propiedad [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key].</span><span class="sxs-lookup"><span data-stu-id="6033b-284">In .NET, use the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="6033b-285">Precios</span><span class="sxs-lookup"><span data-stu-id="6033b-285">Pricing</span></span>
<span data-ttu-id="6033b-286">El servicio Lote de Azure se basa en la tecnología de Servicios en la nube de Azure y en la de Máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="6033b-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="6033b-287">El propio servicio Lote se ofrece sin costo, lo que significa que solo se cobrará por los recursos de proceso utilizados por las soluciones del servicio.</span><span class="sxs-lookup"><span data-stu-id="6033b-287">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="6033b-288">Al elegir **Cloud Services Configuration** (Configuración de Cloud Services), se le cobrará según la estructura de [precios de Cloud Services][cloud_services_pricing].</span><span class="sxs-lookup"><span data-stu-id="6033b-288">When you choose **Cloud Services Configuration**, you are charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="6033b-289">Al elegir **Configuración de la máquina virtual**, se le cobrará según la estructura de [precios de máquinas virtuales][vm_pricing].</span><span class="sxs-lookup"><span data-stu-id="6033b-289">When you choose **Virtual Machine Configuration**, you are charged based on the [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="6033b-290">Si implementa aplicaciones en los nodos de Batch mediante [paquetes de aplicaciones](batch-application-packages.md), también se le cobrarán los recursos de Azure Storage que consumen los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6033b-290">If you deploy applications to your Batch nodes using [application packages](batch-application-packages.md), you are also charged for the Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="6033b-291">En general, los costos de Azure Storage son mínimos.</span><span class="sxs-lookup"><span data-stu-id="6033b-291">In general, the Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6033b-292">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6033b-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="6033b-293">Tutorial de Python de Lote</span><span class="sxs-lookup"><span data-stu-id="6033b-293">Batch Python tutorial</span></span>
<span data-ttu-id="6033b-294">Para ver un tutorial más completo sobre cómo trabajar con Lote mediante Python, consulte [Introducción al cliente Python de Lote de Azure](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6033b-294">For a more in-depth tutorial about how to work with Batch by using Python, check out [Get started with the Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="6033b-295">El [código de ejemplo][github_samples_pyclient] complementario incluye una función auxiliar, `get_vm_config_for_distro`, que muestra otra técnica para obtener una configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6033b-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique to obtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="6033b-296">Ejemplos de código de Python de lote</span><span class="sxs-lookup"><span data-stu-id="6033b-296">Batch Python code samples</span></span>
<span data-ttu-id="6033b-297">Los [ejemplos de código de Python][github_samples_py] del repositorio [azure-batch-samples][github_samples] de GitHub contienen scripts que muestran cómo llevar a cabo operaciones comunes de Batch, como crear grupos, trabajos y tareas.</span><span class="sxs-lookup"><span data-stu-id="6033b-297">The [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how to perform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="6033b-298">El archivo [LÉAME][github_py_readme] que acompaña a los ejemplos de Python incluye detalles sobre cómo instalar los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="6033b-298">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="6033b-299">Foro de Lote</span><span class="sxs-lookup"><span data-stu-id="6033b-299">Batch forum</span></span>
<span data-ttu-id="6033b-300">El [foro de Azure Batch][forum] en MSDN es un lugar excelente para debatir y formular preguntas sobre el servicio.</span><span class="sxs-lookup"><span data-stu-id="6033b-300">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="6033b-301">Lea los mensajes útiles publicados y envíe sus preguntas a medida que surjan mientras compila sus soluciones de Batch.</span><span class="sxs-lookup"><span data-stu-id="6033b-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
