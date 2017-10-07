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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Aprovisionamiento de nodos de proceso de Linux en grupos de Batch

Puede usar las cargas de trabajo de Azure Batch toorun proceso paralelo en máquinas virtuales Linux y Windows. Este artículo detalla cómo toocreate grupos de Linux nodos de proceso en el servicio de lote de hello mediante el uso de ambos hello [lote Python] [ py_batch_package] y [.NET de lotes] [ api_net] bibliotecas de cliente.

> [!NOTE]
> Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017. Ahora se admiten en los grupos de lote creados entre el 10 de marzo de 2016 y 5 de julio de 2017 solo si se creó el grupo de hello mediante una configuración del servicio de nube. Los grupos de lote creados too10 anteriores de marzo de 2016 son compatibles con los paquetes de aplicaciones. Para obtener más información sobre el uso de la aplicación paquetes toodeploy los nodos de proceso por lotes de tooyour de aplicaciones, consulte [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Configuración de la máquina virtual
Cuando se crea un grupo de nodos de proceso en lote, tienes dos opciones desde la cual tooselect tamaño de nodo de Hola y el sistema operativo: configuración de máquina Virtual y la configuración de servicios de nube.

**Cloud Services Configuration** (Configuración de servicios en la nube) *solo*proporciona nodos de proceso de Windows. Tamaños de nodo de proceso disponibles se muestran en [tamaños para servicios en la nube](../cloud-services/cloud-services-sizes-specs.md), y sistemas operativos disponibles se enumeran en hello [versiones del SO invitado de Azure y la matriz de compatibilidad SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Cuando se crea un grupo que contiene los nodos de servicios en la nube, especifica el tamaño del nodo de Hola y Hola familia del SO, que se describen en hello mencionado previamente artículos. Para los grupos de nodos de proceso de Windows, la mayoría de las veces se utilizan los servicios en la nube.

**Configuración de la máquina virtual** proporciona imágenes de Linux y Windows para los nodos de proceso. Los tamaños de nodos de proceso disponibles se muestran en [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [Tamaños de las máquinas virtuales Windows en Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Cuando se crea un grupo que contiene los nodos de configuración de máquina Virtual, debe especificar tamaño Hola de nodos de hello, referencia de imagen de máquina virtual de Hola y Hola lote nodo agente SKU toobe instalados en nodos de Hola.

### <a name="virtual-machine-image-reference"></a>Referencia de imagen de máquina virtual
Hola servicio por lotes utiliza [conjuntos de escalas de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux nodos de proceso. Puede especificar una imagen de hello [Azure Marketplace][vm_marketplace], o proporcionar una imagen personalizada que haya preparado. Para más información acerca de las imágenes personalizadas, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#pool).

Cuando se configura una referencia de imagen de máquina virtual, se especifican propiedades de Hola de imagen de máquina virtual de Hola. Hola propiedades siguientes es necesario cuando se crea una referencia de imagen de máquina virtual:

| **Propiedades de la referencia de la imagen** | **Ejemplo** |
| --- | --- |
| Publicador |Canonical |
| Oferta |UbuntuServer |
| SKU |14.04.4-LTS |
| Versión |más reciente |

> [!TIP]
> Puede aprender más acerca de estas propiedades y cómo toolist Marketplace imágenes en [navegar y seleccionadas imágenes de máquinas virtuales de Linux en Azure con CLI o PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Tenga en cuenta que no todas las imágenes de Marketplace son actualmente compatibles con el servicio Lote. Para más información, consulte [SKU del agente de nodo](#node-agent-sku).
>
>

### <a name="node-agent-sku"></a>SKU del agente de nodo
agente de nodo de proceso por lotes de Hello es un programa que se ejecuta en cada nodo de grupo de Hola y proporciona interfaz de comando y control de hello entre el nodo de Hola y el servicio por lotes Hola. Hay diferentes implementaciones de agente de nodo de hello, conocido como las SKU para diferentes sistemas operativos. Básicamente, cuando se crea una configuración de máquina Virtual, especifique primero la referencia de imagen de máquina virtual de hello y, a continuación, especificar Hola nodo agente tooinstall en la imagen de Hola. Normalmente, cada SKU del agente de nodo es compatible con varias imágenes de máquina virtual. Estos son algunos ejemplos de SKU del agente de nodo:

* batch.node.ubuntu 14.04
* batch.node.centos 7
* batch.node.windows amd64

> [!IMPORTANT]
> No todas las imágenes de máquina virtual que están disponibles en hello Marketplace son compatibles con agentes de nodo de lote actualmente disponibles Hola. Usar el agente de nodo disponible de hello SDK de lote toolist Hola SKU y Hola imágenes de máquina virtual con el que son compatibles. Vea hello [imágenes de la lista de la máquina Virtual](#list-of-virtual-machine-images) más adelante en este artículo para obtener más información y ejemplos de cómo tooretrieve una lista de imágenes válidas en tiempo de ejecución.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Cree un grupo de Linux: Python de Lote
Hello fragmento de código siguiente muestra un ejemplo de cómo hello toouse [biblioteca de cliente de Microsoft Azure Batch para Python] [ py_batch_package] toocreate un grupo de Ubuntu Server nodos de proceso. Hacer referencia a documentación de hello módulo de Python de lote puede encontrarse en [azure.batch paquete] [ py_batch_docs] en documentos de Hola de lectura.

En este fragmento de código, se crea una [ImageReference][py_imagereference] explícitamente y se especifica cada una de sus propiedades (publicador, oferta, SKU, versión). En el código de producción, sin embargo, se recomienda que realice hello [list_node_agent_skus] [ py_list_skus] toodetermine de método y seleccionar Hola imagen y el nodo agente SKU combinaciones disponibles en tiempo de ejecución.

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

Como se mencionó anteriormente, se recomienda que en lugar de crear hello [ImageReference] [ py_imagereference] explícitamente, utilice hello [list_node_agent_skus] [ py_list_skus] método toodynamically seleccionar Hola admite combinaciones de imagen del agente/Marketplace de nodo. Hola Python fragmento siguiente muestra cómo toouse este método.

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

## <a name="create-a-linux-pool-batch-net"></a>Cree un grupo de Linux: .NET de Lote
Hello fragmento de código siguiente muestra un ejemplo de cómo hello toouse [.NET de lotes] [ nuget_batch_net] toocreate de biblioteca de cliente del servidor de Ubuntu de un grupo de nodos de proceso. Puede encontrar Hola [documentación de referencia de .NET de lotes] [ api_net] en MSDN.

fragmento de código siguiente Hello usa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect de método de lista de Hola de actualmente Marketplace imagen y el nodo agente SKU combinaciones admitidas. Esta técnica es deseable, porque puede cambiar lista Hola de combinaciones admitidas de tootime de tiempo. Normalmente, se agregan las combinaciones admitidas.

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

Aunque fragmento anterior hello usa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] método toodynamically y seleccione entre admite imagen y nodo combinaciones de SKU de agente (recomendados), también puede configurar un [ImageReference] [ net_imagereference] explícitamente:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>Lista de imágenes de máquinas virtuales
Hello siguiente tabla enumera las imágenes de máquina virtual de Marketplace de Hola que son compatibles con agentes de nodo de lote disponibles hello cuando este artículo se actualizó por última vez. Es importante toonote que esta lista no es definitiva porque las imágenes y los agentes de nodo pueden agregarse o quitarse en cualquier momento. Se recomienda que siempre utilizan los servicios y aplicaciones de lote [list_node_agent_skus] [ py_list_skus] (Python) y [ListNodeAgentSkus] [ net_list_skus] Toodetermine (lote .NET) y seleccione de Hola SKU disponibles actualmente.

> [!WARNING]
> Hola después de la lista puede cambiar en cualquier momento. Utilice siempre hello **agente de nodo de lista SKU** métodos disponibles en toolist de las API de lote de Hola Hola máquina virtual compatibles y el nodo agente SKU al ejecutar los trabajos por lotes.
>
>

| **Publicador** | **Oferta** | **SKU de imagen** | **Versión** | **Identificador de SKU del agente de nodo** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | más reciente | batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | más reciente | batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | más reciente | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | más reciente | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | más reciente | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1 | más reciente | batch.node.centos 7 |
| OpenLogic | CentOS | 7,2 | más reciente | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.0 | más reciente | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7,2 | más reciente | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | más reciente | batch.node.opensuse 13.2 |
| SUSE | openSUSE-Leap | 42.1 | más reciente | batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | más reciente | batch.node.opensuse 42.1 |
| SUSE | SLES-HPC | 12-SP1 | más reciente | batch.node.opensuse 42.1 |
| microsoft-ads | linux-data-science-vm | linuxdsvm | más reciente | batch.node.centos 7 |
| microsoft-ads | standard-data-science-vm | standard-data-science-vm | más reciente | batch.node.windows amd64 |
| Microsoft Windows Server | Windows Server | 2008-R2-SP1 | más reciente | batch.node.windows amd64 |
| Microsoft Windows Server | Windows Server | Centro de datos de 2012 | más reciente | batch.node.windows amd64 |
| Microsoft Windows Server | Windows Server | Centro de datos de 2012-R2 | más reciente | batch.node.windows amd64 |
| Microsoft Windows Server | Windows Server | 2016-Datacenter | más reciente | batch.node.windows amd64 |
| Microsoft Windows Server | Windows Server | 2016-Datacenter-with-Containers | más reciente | batch.node.windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>Conectar los nodos tooLinux mediante SSH
Durante el desarrollo, o si se intenta solucionar, quizá le resulte necesario toosign en los nodos de toohello en el grupo. A diferencia de los nodos de proceso de Windows, no puede usar los nodos de tooLinux tooconnect de protocolo de escritorio remoto (RDP). En su lugar, Hola servicio por lotes permite el acceso SSH en cada nodo para la conexión remota.

Hello fragmento de código Python siguiente crea un usuario en cada nodo en un grupo, que es necesario para la conexión remota. A continuación, imprime la información de conexión de hello shell seguro (SSH) para cada nodo.

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

Este es el resultado de ejemplo de código anterior de Hola para un grupo que contiene cuatro nodos de Linux:

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

En lugar de una contraseña, puede especificar una clave pública SSH al crear un usuario en un nodo. Hola SDK de Python, usar hello **ssh_public_key** parámetro en [ComputeNodeUser][py_computenodeuser]. En. NET, use hello [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] propiedad.

## <a name="pricing"></a>Precios
El servicio Lote de Azure se basa en la tecnología de Servicios en la nube de Azure y en la de Máquinas virtuales de Azure. Hola propio servicio de lote se ofrece sin costo alguno, que significa que se le cobra solo de hello recursos que consumen las soluciones de lote de proceso. Cuando eliges **configuración de servicios de nube**, se le cobra según hello [de precios de servicios de nube] [ cloud_services_pricing] estructura. Cuando eliges **configuración de máquina Virtual**, se le cobra según hello [precios de máquinas virtuales] [ vm_pricing] estructura. 

Si implementa nodos de lote de aplicaciones tooyour con [paquetes de aplicación](batch-application-packages.md), también se cobra por los recursos de almacenamiento de Azure de Hola que consumen los paquetes de aplicaciones. En general, los costos de almacenamiento de Azure de hello son mínimos. 

## <a name="next-steps"></a>Pasos siguientes
### <a name="batch-python-tutorial"></a>Tutorial de Python de Lote
Para obtener un tutorial más detallado acerca de cómo toowork con lote mediante el uso de Python, desprotección [empezar a trabajar con el cliente de Python de lote de Azure de hello](batch-python-tutorial.md). Su complementario [código de ejemplo] [ github_samples_pyclient] incluye una función auxiliar, `get_vm_config_for_distro`, que muestra otro tooobtain técnica una configuración de máquina virtual.

### <a name="batch-python-code-samples"></a>Ejemplos de código de Python de lote
Hola [ejemplos de código de Python] [ github_samples_py] en hello [ejemplos de lote de azure] [ github_samples] repositorio en GitHub contienen secuencias de comandos que le muestran cómo tooperform operaciones comunes de lote, como el grupo de trabajo y creación de tareas. Hola [Léame] [ github_py_readme] que acompaña a ejemplos de Python Hola con información detallada acerca de cómo tooinstall Hola necesario paquetes.

### <a name="batch-forum"></a>Foro de Lote
Hola [foro de lote de Azure] [ forum] en MSDN es una gran colocar toodiscuss por lotes y formular preguntas acerca del servicio de Hola. Lea los mensajes útiles publicados y envíe sus preguntas a medida que surjan mientras compila sus soluciones de Batch.

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
