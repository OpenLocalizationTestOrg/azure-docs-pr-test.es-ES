---
title: "aaaRun Linux en la máquina virtual de proceso nodos - Azure Batch | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprocess su paralelo calcular cargas de trabajo en grupos de máquinas virtuales de Linux en el lote de Azure."
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
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="d4f27-103">Aprovisionamiento de nodos de proceso de Linux en grupos de Batch</span><span class="sxs-lookup"><span data-stu-id="d4f27-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="d4f27-104">Puede usar las cargas de trabajo de Azure Batch toorun proceso paralelo en máquinas virtuales Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="d4f27-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="d4f27-105">Este artículo detalla cómo toocreate grupos de Linux nodos de proceso en el servicio de lote de hello mediante el uso de ambos hello [lote Python] [ py_batch_package] y [.NET de lotes] [ api_net] bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="d4f27-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="d4f27-106">Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017.</span><span class="sxs-lookup"><span data-stu-id="d4f27-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="d4f27-107">Ahora se admiten en los grupos de lote creados entre el 10 de marzo de 2016 y 5 de julio de 2017 solo si se creó el grupo de hello mediante una configuración del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="d4f27-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="d4f27-108">Los grupos de lote creados too10 anteriores de marzo de 2016 son compatibles con los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d4f27-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="d4f27-109">Para obtener más información sobre el uso de la aplicación paquetes toodeploy los nodos de proceso por lotes de tooyour de aplicaciones, consulte [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d4f27-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="d4f27-110">Configuración de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d4f27-110">Virtual machine configuration</span></span>
<span data-ttu-id="d4f27-111">Cuando se crea un grupo de nodos de proceso en lote, tienes dos opciones desde la cual tooselect tamaño de nodo de Hola y el sistema operativo: configuración de máquina Virtual y la configuración de servicios de nube.</span><span class="sxs-lookup"><span data-stu-id="d4f27-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="d4f27-112">**Cloud Services Configuration** (Configuración de servicios en la nube) *solo*proporciona nodos de proceso de Windows.</span><span class="sxs-lookup"><span data-stu-id="d4f27-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="d4f27-113">Tamaños de nodo de proceso disponibles se muestran en [tamaños para servicios en la nube](../cloud-services/cloud-services-sizes-specs.md), y sistemas operativos disponibles se enumeran en hello [versiones del SO invitado de Azure y la matriz de compatibilidad SDK](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="d4f27-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="d4f27-114">Cuando se crea un grupo que contiene los nodos de servicios en la nube, especifica el tamaño del nodo de Hola y Hola familia del SO, que se describen en hello mencionado previamente artículos.</span><span class="sxs-lookup"><span data-stu-id="d4f27-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="d4f27-115">Para los grupos de nodos de proceso de Windows, la mayoría de las veces se utilizan los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="d4f27-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="d4f27-116">**Configuración de la máquina virtual** proporciona imágenes de Linux y Windows para los nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="d4f27-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="d4f27-117">Los tamaños de nodos de proceso disponibles se muestran en [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [Tamaños de las máquinas virtuales Windows en Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4f27-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="d4f27-118">Cuando se crea un grupo que contiene los nodos de configuración de máquina Virtual, debe especificar tamaño Hola de nodos de hello, referencia de imagen de máquina virtual de Hola y Hola lote nodo agente SKU toobe instalados en nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f27-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="d4f27-119">Referencia de imagen de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d4f27-119">Virtual machine image reference</span></span>
<span data-ttu-id="d4f27-120">Hola servicio por lotes utiliza [conjuntos de escalas de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="d4f27-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="d4f27-121">Puede especificar una imagen de hello [Azure Marketplace][vm_marketplace], o proporcionar una imagen personalizada que haya preparado.</span><span class="sxs-lookup"><span data-stu-id="d4f27-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="d4f27-122">Para más información acerca de las imágenes personalizadas, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="d4f27-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="d4f27-123">Cuando se configura una referencia de imagen de máquina virtual, se especifican propiedades de Hola de imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f27-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="d4f27-124">Hola propiedades siguientes es necesario cuando se crea una referencia de imagen de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="d4f27-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="d4f27-125">**Propiedades de la referencia de la imagen**</span><span class="sxs-lookup"><span data-stu-id="d4f27-125">**Image reference properties**</span></span> | <span data-ttu-id="d4f27-126">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="d4f27-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="d4f27-127">Publicador</span><span class="sxs-lookup"><span data-stu-id="d4f27-127">Publisher</span></span> |<span data-ttu-id="d4f27-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="d4f27-128">Canonical</span></span> |
| <span data-ttu-id="d4f27-129">Oferta</span><span class="sxs-lookup"><span data-stu-id="d4f27-129">Offer</span></span> |<span data-ttu-id="d4f27-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="d4f27-130">UbuntuServer</span></span> |
| <span data-ttu-id="d4f27-131">SKU</span><span class="sxs-lookup"><span data-stu-id="d4f27-131">SKU</span></span> |<span data-ttu-id="d4f27-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="d4f27-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="d4f27-133">Versión</span><span class="sxs-lookup"><span data-stu-id="d4f27-133">Version</span></span> |<span data-ttu-id="d4f27-134">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="d4f27-135">Puede aprender más acerca de estas propiedades y cómo toolist Marketplace imágenes en [navegar y seleccionadas imágenes de máquinas virtuales de Linux en Azure con CLI o PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4f27-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d4f27-136">Tenga en cuenta que no todas las imágenes de Marketplace son actualmente compatibles con el servicio Lote.</span><span class="sxs-lookup"><span data-stu-id="d4f27-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="d4f27-137">Para más información, consulte [SKU del agente de nodo](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="d4f27-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="d4f27-138">SKU del agente de nodo</span><span class="sxs-lookup"><span data-stu-id="d4f27-138">Node agent SKU</span></span>
<span data-ttu-id="d4f27-139">agente de nodo de proceso por lotes de Hello es un programa que se ejecuta en cada nodo de grupo de Hola y proporciona interfaz de comando y control de hello entre el nodo de Hola y el servicio por lotes Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f27-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="d4f27-140">Hay diferentes implementaciones de agente de nodo de hello, conocido como las SKU para diferentes sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="d4f27-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="d4f27-141">Básicamente, cuando se crea una configuración de máquina Virtual, especifique primero la referencia de imagen de máquina virtual de hello y, a continuación, especificar Hola nodo agente tooinstall en la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f27-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="d4f27-142">Normalmente, cada SKU del agente de nodo es compatible con varias imágenes de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d4f27-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="d4f27-143">Estos son algunos ejemplos de SKU del agente de nodo:</span><span class="sxs-lookup"><span data-stu-id="d4f27-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="d4f27-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="d4f27-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="d4f27-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-145">batch.node.centos 7</span></span>
* <span data-ttu-id="d4f27-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="d4f27-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4f27-147">No todas las imágenes de máquina virtual que están disponibles en hello Marketplace son compatibles con agentes de nodo de lote actualmente disponibles Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f27-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="d4f27-148">Usar el agente de nodo disponible de hello SDK de lote toolist Hola SKU y Hola imágenes de máquina virtual con el que son compatibles.</span><span class="sxs-lookup"><span data-stu-id="d4f27-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="d4f27-149">Vea hello [imágenes de la lista de la máquina Virtual](#list-of-virtual-machine-images) más adelante en este artículo para obtener más información y ejemplos de cómo tooretrieve una lista de imágenes válidas en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="d4f27-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="d4f27-150">Cree un grupo de Linux: Python de Lote</span><span class="sxs-lookup"><span data-stu-id="d4f27-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="d4f27-151">Hello fragmento de código siguiente muestra un ejemplo de cómo hello toouse [biblioteca de cliente de Microsoft Azure Batch para Python] [ py_batch_package] toocreate un grupo de Ubuntu Server nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="d4f27-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="d4f27-152">Hacer referencia a documentación de hello módulo de Python de lote puede encontrarse en [azure.batch paquete] [ py_batch_docs] en documentos de Hola de lectura.</span><span class="sxs-lookup"><span data-stu-id="d4f27-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="d4f27-153">En este fragmento de código, se crea una [ImageReference][py_imagereference] explícitamente y se especifica cada una de sus propiedades (publicador, oferta, SKU, versión).</span><span class="sxs-lookup"><span data-stu-id="d4f27-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="d4f27-154">En el código de producción, sin embargo, se recomienda que realice hello [list_node_agent_skus] [ py_list_skus] toodetermine de método y seleccionar Hola imagen y el nodo agente SKU combinaciones disponibles en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="d4f27-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

```python
# Import hello required modules from the
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

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="d4f27-155">Como se mencionó anteriormente, se recomienda que en lugar de crear hello [ImageReference] [ py_imagereference] explícitamente, utilice hello [list_node_agent_skus] [ py_list_skus] método toodynamically seleccionar Hola admite combinaciones de imagen del agente/Marketplace de nodo.</span><span class="sxs-lookup"><span data-stu-id="d4f27-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="d4f27-156">Hola Python fragmento siguiente muestra cómo toouse este método.</span><span class="sxs-lookup"><span data-stu-id="d4f27-156">hello following Python snippet shows how toouse this method.</span></span>

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="d4f27-157">Cree un grupo de Linux: .NET de Lote</span><span class="sxs-lookup"><span data-stu-id="d4f27-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="d4f27-158">Hello fragmento de código siguiente muestra un ejemplo de cómo hello toouse [.NET de lotes] [ nuget_batch_net] toocreate de biblioteca de cliente del servidor de Ubuntu de un grupo de nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="d4f27-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="d4f27-159">Puede encontrar Hola [documentación de referencia de .NET de lotes] [ api_net] en MSDN.</span><span class="sxs-lookup"><span data-stu-id="d4f27-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="d4f27-160">fragmento de código siguiente Hello usa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect de método de lista de Hola de actualmente Marketplace imagen y el nodo agente SKU combinaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="d4f27-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="d4f27-161">Esta técnica es deseable, porque puede cambiar lista Hola de combinaciones admitidas de tootime de tiempo.</span><span class="sxs-lookup"><span data-stu-id="d4f27-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="d4f27-162">Normalmente, se agregan las combinaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="d4f27-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

<span data-ttu-id="d4f27-163">Aunque fragmento anterior hello usa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] método toodynamically y seleccione entre admite imagen y nodo combinaciones de SKU de agente (recomendados), también puede configurar un [ImageReference] [ net_imagereference] explícitamente:</span><span class="sxs-lookup"><span data-stu-id="d4f27-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="d4f27-164">Lista de imágenes de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d4f27-164">List of virtual machine images</span></span>
<span data-ttu-id="d4f27-165">Hello siguiente tabla enumera las imágenes de máquina virtual de Marketplace de Hola que son compatibles con agentes de nodo de lote disponibles hello cuando este artículo se actualizó por última vez.</span><span class="sxs-lookup"><span data-stu-id="d4f27-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="d4f27-166">Es importante toonote que esta lista no es definitiva porque las imágenes y los agentes de nodo pueden agregarse o quitarse en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="d4f27-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="d4f27-167">Se recomienda que siempre utilizan los servicios y aplicaciones de lote [list_node_agent_skus] [ py_list_skus] (Python) y [ListNodeAgentSkus] [ net_list_skus] Toodetermine (lote .NET) y seleccione de Hola SKU disponibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="d4f27-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="d4f27-168">Hola después de la lista puede cambiar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="d4f27-168">hello following list may change at any time.</span></span> <span data-ttu-id="d4f27-169">Utilice siempre hello **agente de nodo de lista SKU** métodos disponibles en toolist de las API de lote de Hola Hola máquina virtual compatibles y el nodo agente SKU al ejecutar los trabajos por lotes.</span><span class="sxs-lookup"><span data-stu-id="d4f27-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="d4f27-170">**Publicador**</span><span class="sxs-lookup"><span data-stu-id="d4f27-170">**Publisher**</span></span> | <span data-ttu-id="d4f27-171">**Oferta**</span><span class="sxs-lookup"><span data-stu-id="d4f27-171">**Offer**</span></span> | <span data-ttu-id="d4f27-172">**SKU de imagen**</span><span class="sxs-lookup"><span data-stu-id="d4f27-172">**Image SKU**</span></span> | <span data-ttu-id="d4f27-173">**Versión**</span><span class="sxs-lookup"><span data-stu-id="d4f27-173">**Version**</span></span> | <span data-ttu-id="d4f27-174">**Identificador de SKU del agente de nodo**</span><span class="sxs-lookup"><span data-stu-id="d4f27-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="d4f27-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="d4f27-175">Canonical</span></span> | <span data-ttu-id="d4f27-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="d4f27-176">UbuntuServer</span></span> | <span data-ttu-id="d4f27-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="d4f27-177">14.04.5-LTS</span></span> | <span data-ttu-id="d4f27-178">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-178">latest</span></span> | <span data-ttu-id="d4f27-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="d4f27-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="d4f27-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="d4f27-180">Canonical</span></span> | <span data-ttu-id="d4f27-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="d4f27-181">UbuntuServer</span></span> | <span data-ttu-id="d4f27-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="d4f27-182">16.04.0-LTS</span></span> | <span data-ttu-id="d4f27-183">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-183">latest</span></span> | <span data-ttu-id="d4f27-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d4f27-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="d4f27-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="d4f27-185">Credativ</span></span> | <span data-ttu-id="d4f27-186">Debian</span><span class="sxs-lookup"><span data-stu-id="d4f27-186">Debian</span></span> | <span data-ttu-id="d4f27-187">8</span><span class="sxs-lookup"><span data-stu-id="d4f27-187">8</span></span> | <span data-ttu-id="d4f27-188">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-188">latest</span></span> | <span data-ttu-id="d4f27-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="d4f27-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="d4f27-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="d4f27-190">OpenLogic</span></span> | <span data-ttu-id="d4f27-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="d4f27-191">CentOS</span></span> | <span data-ttu-id="d4f27-192">7.0</span><span class="sxs-lookup"><span data-stu-id="d4f27-192">7.0</span></span> | <span data-ttu-id="d4f27-193">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-193">latest</span></span> | <span data-ttu-id="d4f27-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="d4f27-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="d4f27-195">OpenLogic</span></span> | <span data-ttu-id="d4f27-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="d4f27-196">CentOS</span></span> | <span data-ttu-id="d4f27-197">7.1</span><span class="sxs-lookup"><span data-stu-id="d4f27-197">7.1</span></span> | <span data-ttu-id="d4f27-198">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-198">latest</span></span> | <span data-ttu-id="d4f27-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="d4f27-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="d4f27-200">OpenLogic</span></span> | <span data-ttu-id="d4f27-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="d4f27-201">CentOS-HPC</span></span> | <span data-ttu-id="d4f27-202">7.1</span><span class="sxs-lookup"><span data-stu-id="d4f27-202">7.1</span></span> | <span data-ttu-id="d4f27-203">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-203">latest</span></span> | <span data-ttu-id="d4f27-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="d4f27-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="d4f27-205">OpenLogic</span></span> | <span data-ttu-id="d4f27-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="d4f27-206">CentOS</span></span> | <span data-ttu-id="d4f27-207">7,2</span><span class="sxs-lookup"><span data-stu-id="d4f27-207">7.2</span></span> | <span data-ttu-id="d4f27-208">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-208">latest</span></span> | <span data-ttu-id="d4f27-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="d4f27-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="d4f27-210">Oracle</span></span> | <span data-ttu-id="d4f27-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="d4f27-211">Oracle-Linux</span></span> | <span data-ttu-id="d4f27-212">7.0</span><span class="sxs-lookup"><span data-stu-id="d4f27-212">7.0</span></span> | <span data-ttu-id="d4f27-213">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-213">latest</span></span> | <span data-ttu-id="d4f27-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="d4f27-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="d4f27-215">Oracle</span></span> | <span data-ttu-id="d4f27-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="d4f27-216">Oracle-Linux</span></span> | <span data-ttu-id="d4f27-217">7,2</span><span class="sxs-lookup"><span data-stu-id="d4f27-217">7.2</span></span> | <span data-ttu-id="d4f27-218">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-218">latest</span></span> | <span data-ttu-id="d4f27-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="d4f27-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="d4f27-220">SUSE</span></span> | <span data-ttu-id="d4f27-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="d4f27-221">openSUSE</span></span> | <span data-ttu-id="d4f27-222">13.2</span><span class="sxs-lookup"><span data-stu-id="d4f27-222">13.2</span></span> | <span data-ttu-id="d4f27-223">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-223">latest</span></span> | <span data-ttu-id="d4f27-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="d4f27-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="d4f27-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="d4f27-225">SUSE</span></span> | <span data-ttu-id="d4f27-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="d4f27-226">openSUSE-Leap</span></span> | <span data-ttu-id="d4f27-227">42.1</span><span class="sxs-lookup"><span data-stu-id="d4f27-227">42.1</span></span> | <span data-ttu-id="d4f27-228">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-228">latest</span></span> | <span data-ttu-id="d4f27-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="d4f27-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="d4f27-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="d4f27-230">SUSE</span></span> | <span data-ttu-id="d4f27-231">SLES</span><span class="sxs-lookup"><span data-stu-id="d4f27-231">SLES</span></span> | <span data-ttu-id="d4f27-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="d4f27-232">12-SP1</span></span> | <span data-ttu-id="d4f27-233">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-233">latest</span></span> | <span data-ttu-id="d4f27-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="d4f27-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="d4f27-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="d4f27-235">SUSE</span></span> | <span data-ttu-id="d4f27-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="d4f27-236">SLES-HPC</span></span> | <span data-ttu-id="d4f27-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="d4f27-237">12-SP1</span></span> | <span data-ttu-id="d4f27-238">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-238">latest</span></span> | <span data-ttu-id="d4f27-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="d4f27-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="d4f27-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="d4f27-240">microsoft-ads</span></span> | <span data-ttu-id="d4f27-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="d4f27-241">linux-data-science-vm</span></span> | <span data-ttu-id="d4f27-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="d4f27-242">linuxdsvm</span></span> | <span data-ttu-id="d4f27-243">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-243">latest</span></span> | <span data-ttu-id="d4f27-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="d4f27-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="d4f27-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="d4f27-245">microsoft-ads</span></span> | <span data-ttu-id="d4f27-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="d4f27-246">standard-data-science-vm</span></span> | <span data-ttu-id="d4f27-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="d4f27-247">standard-data-science-vm</span></span> | <span data-ttu-id="d4f27-248">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-248">latest</span></span> | <span data-ttu-id="d4f27-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="d4f27-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="d4f27-250">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="d4f27-251">Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-251">WindowsServer</span></span> | <span data-ttu-id="d4f27-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="d4f27-252">2008-R2-SP1</span></span> | <span data-ttu-id="d4f27-253">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-253">latest</span></span> | <span data-ttu-id="d4f27-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="d4f27-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="d4f27-255">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="d4f27-256">Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-256">WindowsServer</span></span> | <span data-ttu-id="d4f27-257">Centro de datos de 2012</span><span class="sxs-lookup"><span data-stu-id="d4f27-257">2012-Datacenter</span></span> | <span data-ttu-id="d4f27-258">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-258">latest</span></span> | <span data-ttu-id="d4f27-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="d4f27-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="d4f27-260">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="d4f27-261">Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-261">WindowsServer</span></span> | <span data-ttu-id="d4f27-262">Centro de datos de 2012-R2</span><span class="sxs-lookup"><span data-stu-id="d4f27-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="d4f27-263">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-263">latest</span></span> | <span data-ttu-id="d4f27-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="d4f27-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="d4f27-265">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="d4f27-266">Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-266">WindowsServer</span></span> | <span data-ttu-id="d4f27-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="d4f27-267">2016-Datacenter</span></span> | <span data-ttu-id="d4f27-268">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-268">latest</span></span> | <span data-ttu-id="d4f27-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="d4f27-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="d4f27-270">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="d4f27-271">Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4f27-271">WindowsServer</span></span> | <span data-ttu-id="d4f27-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="d4f27-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="d4f27-273">más reciente</span><span class="sxs-lookup"><span data-stu-id="d4f27-273">latest</span></span> | <span data-ttu-id="d4f27-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="d4f27-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="d4f27-275">Conectar los nodos tooLinux mediante SSH</span><span class="sxs-lookup"><span data-stu-id="d4f27-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="d4f27-276">Durante el desarrollo, o si se intenta solucionar, quizá le resulte necesario toosign en los nodos de toohello en el grupo.</span><span class="sxs-lookup"><span data-stu-id="d4f27-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="d4f27-277">A diferencia de los nodos de proceso de Windows, no puede usar los nodos de tooLinux tooconnect de protocolo de escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="d4f27-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="d4f27-278">En su lugar, Hola servicio por lotes permite el acceso SSH en cada nodo para la conexión remota.</span><span class="sxs-lookup"><span data-stu-id="d4f27-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="d4f27-279">Hello fragmento de código Python siguiente crea un usuario en cada nodo en un grupo, que es necesario para la conexión remota.</span><span class="sxs-lookup"><span data-stu-id="d4f27-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="d4f27-280">A continuación, imprime la información de conexión de hello shell seguro (SSH) para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="d4f27-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

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

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
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

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="d4f27-281">Este es el resultado de ejemplo de código anterior de Hola para un grupo que contiene cuatro nodos de Linux:</span><span class="sxs-lookup"><span data-stu-id="d4f27-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="d4f27-282">En lugar de una contraseña, puede especificar una clave pública SSH al crear un usuario en un nodo.</span><span class="sxs-lookup"><span data-stu-id="d4f27-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="d4f27-283">Hola SDK de Python, usar hello **ssh_public_key** parámetro en [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="d4f27-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="d4f27-284">En. NET, use hello [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] propiedad.</span><span class="sxs-lookup"><span data-stu-id="d4f27-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="d4f27-285">Precios</span><span class="sxs-lookup"><span data-stu-id="d4f27-285">Pricing</span></span>
<span data-ttu-id="d4f27-286">El servicio Lote de Azure se basa en la tecnología de Servicios en la nube de Azure y en la de Máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f27-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="d4f27-287">Hola propio servicio de lote se ofrece sin costo alguno, que significa que se le cobra solo de hello recursos que consumen las soluciones de lote de proceso.</span><span class="sxs-lookup"><span data-stu-id="d4f27-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="d4f27-288">Cuando eliges **configuración de servicios de nube**, se le cobra según hello [de precios de servicios de nube] [ cloud_services_pricing] estructura.</span><span class="sxs-lookup"><span data-stu-id="d4f27-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="d4f27-289">Cuando eliges **configuración de máquina Virtual**, se le cobra según hello [precios de máquinas virtuales] [ vm_pricing] estructura.</span><span class="sxs-lookup"><span data-stu-id="d4f27-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="d4f27-290">Si implementa nodos de lote de aplicaciones tooyour con [paquetes de aplicación](batch-application-packages.md), también se cobra por los recursos de almacenamiento de Azure de Hola que consumen los paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d4f27-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="d4f27-291">En general, los costos de almacenamiento de Azure de hello son mínimos.</span><span class="sxs-lookup"><span data-stu-id="d4f27-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d4f27-292">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4f27-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="d4f27-293">Tutorial de Python de Lote</span><span class="sxs-lookup"><span data-stu-id="d4f27-293">Batch Python tutorial</span></span>
<span data-ttu-id="d4f27-294">Para obtener un tutorial más detallado acerca de cómo toowork con lote mediante el uso de Python, desprotección [empezar a trabajar con el cliente de Python de lote de Azure de hello](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d4f27-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="d4f27-295">Su complementario [código de ejemplo] [ github_samples_pyclient] incluye una función auxiliar, `get_vm_config_for_distro`, que muestra otro tooobtain técnica una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d4f27-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="d4f27-296">Ejemplos de código de Python de lote</span><span class="sxs-lookup"><span data-stu-id="d4f27-296">Batch Python code samples</span></span>
<span data-ttu-id="d4f27-297">Hola [ejemplos de código de Python] [ github_samples_py] en hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub contienen secuencias de comandos que le muestran cómo tooperform operaciones comunes de lote, como el grupo de trabajo y creación de tareas.</span><span class="sxs-lookup"><span data-stu-id="d4f27-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="d4f27-298">Hola [Léame] [ github_py_readme] que acompaña a ejemplos de Python Hola con información detallada acerca de cómo tooinstall Hola necesario paquetes.</span><span class="sxs-lookup"><span data-stu-id="d4f27-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="d4f27-299">Foro de Lote</span><span class="sxs-lookup"><span data-stu-id="d4f27-299">Batch forum</span></span>
<span data-ttu-id="d4f27-300">Hola [foro de lote de Azure] [ forum] en MSDN es una gran colocar toodiscuss por lotes y formular preguntas acerca del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d4f27-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="d4f27-301">Lea los mensajes útiles publicados y envíe sus preguntas a medida que surjan mientras compila sus soluciones de Batch.</span><span class="sxs-lookup"><span data-stu-id="d4f27-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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
