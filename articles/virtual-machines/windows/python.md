---
title: "aaaCreate y administrar una máquina virtual de Windows en Azure con Python | Documentos de Microsoft"
description: "Obtenga información acerca de toouse Python toocreate y administrar una máquina virtual de Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="ae20e-103">Creación y administración de máquinas virtuales Windows en Azure con Python</span><span class="sxs-lookup"><span data-stu-id="ae20e-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="ae20e-104">Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles.</span><span class="sxs-lookup"><span data-stu-id="ae20e-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="ae20e-105">En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con Python.</span><span class="sxs-lookup"><span data-stu-id="ae20e-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="ae20e-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="ae20e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ae20e-107">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae20e-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="ae20e-108">Instalar paquetes</span><span class="sxs-lookup"><span data-stu-id="ae20e-108">Install packages</span></span>
> * <span data-ttu-id="ae20e-109">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="ae20e-109">Create credentials</span></span>
> * <span data-ttu-id="ae20e-110">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="ae20e-110">Create resources</span></span>
> * <span data-ttu-id="ae20e-111">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="ae20e-111">Perform management tasks</span></span>
> * <span data-ttu-id="ae20e-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="ae20e-112">Delete resources</span></span>
> * <span data-ttu-id="ae20e-113">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="ae20e-113">Run hello application</span></span>

<span data-ttu-id="ae20e-114">Tarda aproximadamente 20 minutos toodo estos pasos.</span><span class="sxs-lookup"><span data-stu-id="ae20e-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="ae20e-115">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae20e-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="ae20e-116">Si aún no lo ha hecho, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="ae20e-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="ae20e-117">Seleccione **desarrollo Python** en Hola página cargas de trabajo y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="ae20e-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="ae20e-118">En resumen de hello, puede ver que **Python 3 de 64 bits (3.6.0)** se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ae20e-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="ae20e-119">Si ya ha instalado Visual Studio, puede agregar carga de trabajo de Python de hello mediante Hola selector de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae20e-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="ae20e-120">Después de instalar e iniciar Visual Studio, haga clic en **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="ae20e-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="ae20e-121">Haga clic en **plantillas** > **Python** > **aplicación de Python**, escriba *myPythonProject* para nombre de Hola del proyecto de hello, Seleccionar ubicación de hello del proyecto de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ae20e-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="ae20e-122">Instalar paquetes</span><span class="sxs-lookup"><span data-stu-id="ae20e-122">Install packages</span></span>

1. <span data-ttu-id="ae20e-123">En el Explorador de soluciones, bajo *myPythonProject*, haga clic con el botón derecho en **Python Environments** (Entornos de Python) y seleccione **Add virtual environment** (Agregar entorno virtual).</span><span class="sxs-lookup"><span data-stu-id="ae20e-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="ae20e-124">En la pantalla de bienvenida agregar entorno Virtual, acepte el nombre de valor predeterminado de Hola de *env*, asegúrese de que *3.6 de Python (64 bits)* está seleccionada para el intérprete de base de hello y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="ae20e-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="ae20e-125">Menú contextual hello *env* entorno que creó, haga clic en **instalar un paquete de Python**, escriba *azure* en Hola cuadro de búsqueda y, a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="ae20e-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="ae20e-126">Debería ver en las ventanas de salida de hello que paquetes hello azure se han instalado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ae20e-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="ae20e-127">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="ae20e-127">Create credentials</span></span>

<span data-ttu-id="ae20e-128">Antes de empezar este paso, asegúrese de que tiene una [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ae20e-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="ae20e-129">También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesita en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="ae20e-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="ae20e-130">Abra *myPythonProject.py* archivo que se creó y, a continuación, agregar este código tooenable su toorun de aplicación:</span><span class="sxs-lookup"><span data-stu-id="ae20e-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="ae20e-131">código de hello tooimport que es necesario, agregue estos superior de toohello las instrucciones del archivo de Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="ae20e-132">A continuación en archivo de .py de hello, agregue variables después de instrucciones de importación de hello toospecify los valores comunes utilizados en Hola código:</span><span class="sxs-lookup"><span data-stu-id="ae20e-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="ae20e-133">Reemplace **subscription-id** por el identificador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ae20e-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="ae20e-134">las credenciales de Active Directory de hello toocreate necesita toomake solicitudes, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="ae20e-135">Reemplace **identificador de la aplicación**, **clave de autenticación**, y **Id. de inquilino** con valores de hello que previamente recopilados cuando se creó su Azure Active Directory entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="ae20e-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="ae20e-136">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="ae20e-137">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="ae20e-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="ae20e-138">Inicialización de los clientes de administración</span><span class="sxs-lookup"><span data-stu-id="ae20e-138">Initialize management clients</span></span>

<span data-ttu-id="ae20e-139">Clientes de administración necesario toocreate y administración recursos utilizando Hola SDK de Python en Azure.</span><span class="sxs-lookup"><span data-stu-id="ae20e-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="ae20e-140">los clientes de administración de toocreate hello, agregue este código en hello **si** instrucción al final, a continuación, del archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="ae20e-141">Crear hello VM y los recursos de soporte</span><span class="sxs-lookup"><span data-stu-id="ae20e-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="ae20e-142">Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae20e-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="ae20e-143">toocreate un grupo de recursos, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="ae20e-144">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="ae20e-145">[Conjuntos de disponibilidad](tutorial-availability-sets.md) resultará más fácil máquinas virtuales toomaintain Hola que usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ae20e-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="ae20e-146">conjunto de toocreate una disponibilidad, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="ae20e-147">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="ae20e-148">A [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) es necesario toocommunicate con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae20e-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="ae20e-149">toocreate una dirección IP pública para la máquina virtual de hello, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="ae20e-150">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="ae20e-151">Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae20e-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="ae20e-152">toocreate una red virtual, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="ae20e-153">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="ae20e-154">tooadd una red virtual toohello de subred, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="ae20e-155">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="ae20e-156">Una máquina virtual necesita un toocommunicate de interfaz de red en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae20e-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="ae20e-157">toocreate una interfaz de red, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="ae20e-158">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="ae20e-159">Ahora que ha creado Hola todos los recursos de soporte, puede crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ae20e-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="ae20e-160">toocreate Hola máquina virtual, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="ae20e-161">Este tutorial crea una máquina virtual con una versión de sistema operativo de Windows Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="ae20e-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="ae20e-162">toolearn más acerca de cómo seleccionar otras imágenes, vea [navegue y seleccione las imágenes de máquina virtual de Azure con Windows PowerShell y hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae20e-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="ae20e-163">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="ae20e-164">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="ae20e-164">Perform management tasks</span></span>

<span data-ttu-id="ae20e-165">Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ae20e-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="ae20e-166">Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de código.</span><span class="sxs-lookup"><span data-stu-id="ae20e-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="ae20e-167">Obtener información acerca de hello VM</span><span class="sxs-lookup"><span data-stu-id="ae20e-167">Get information about hello VM</span></span>

1. <span data-ttu-id="ae20e-168">tooget información acerca de la máquina virtual de hello, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="ae20e-169">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="ae20e-170">Detener Hola VM</span><span class="sxs-lookup"><span data-stu-id="ae20e-170">Stop hello VM</span></span>

<span data-ttu-id="ae20e-171">Puede detener una máquina virtual y mantener todas sus opciones, pero continuar toobe cobra por él, o puede detener una máquina virtual y cancelar la asignación lo.</span><span class="sxs-lookup"><span data-stu-id="ae20e-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="ae20e-172">Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.</span><span class="sxs-lookup"><span data-stu-id="ae20e-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="ae20e-173">toostop Hola virtual machine sin cancelar su asignación, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="ae20e-174">Si desea que la máquina virtual de toodeallocate hello, cambiar el código de hello power_off llamada toothis:</span><span class="sxs-lookup"><span data-stu-id="ae20e-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="ae20e-175">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="ae20e-176">Iniciar Hola VM</span><span class="sxs-lookup"><span data-stu-id="ae20e-176">Start hello VM</span></span>

1. <span data-ttu-id="ae20e-177">toostart Hola máquina virtual, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="ae20e-178">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="ae20e-179">Cambiar el tamaño de hello VM</span><span class="sxs-lookup"><span data-stu-id="ae20e-179">Resize hello VM</span></span>

<span data-ttu-id="ae20e-180">Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación.</span><span class="sxs-lookup"><span data-stu-id="ae20e-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="ae20e-181">Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="ae20e-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="ae20e-182">tamaño de hello toochange de máquina virtual de hello, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="ae20e-183">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="ae20e-184">Agregar un toohello de disco de datos VM</span><span class="sxs-lookup"><span data-stu-id="ae20e-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="ae20e-185">Las máquinas virtuales pueden tener uno o más [discos de datos](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) que se almacenen en discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="ae20e-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="ae20e-186">tooadd una máquina virtual de toohello de disco de datos, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="ae20e-187">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="ae20e-188">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="ae20e-188">Delete resources</span></span>

<span data-ttu-id="ae20e-189">Dado que se le cobra por recursos que usa en Azure, siempre es un recursos toodelete recomendable que ya no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="ae20e-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="ae20e-190">Si desea que las máquinas virtuales de toodelete Hola y Hola a todos los recursos de soporte todo lo que tiene toodo es el grupo de recursos de Hola de eliminación.</span><span class="sxs-lookup"><span data-stu-id="ae20e-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="ae20e-191">grupo de recursos de toodelete hello y todos los recursos, agregue esta función después de las variables de hello en el archivo de hello .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="ae20e-192">función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:</span><span class="sxs-lookup"><span data-stu-id="ae20e-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="ae20e-193">Guarde *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="ae20e-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="ae20e-194">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="ae20e-194">Run hello application</span></span>

1. <span data-ttu-id="ae20e-195">aplicación de consola de hello toorun, haga clic en **iniciar** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae20e-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="ae20e-196">Presione **ENTRAR** después de que se devuelve el estado de Hola de cada recurso.</span><span class="sxs-lookup"><span data-stu-id="ae20e-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="ae20e-197">En información de estado de hello, debería ver un **correcto** estado de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="ae20e-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="ae20e-198">Después de crear la máquina virtual de hello, tendrá Hola oportunidad toodelete todos los recursos de Hola que cree.</span><span class="sxs-lookup"><span data-stu-id="ae20e-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="ae20e-199">Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos tooverify minutos su creación en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae20e-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="ae20e-200">Si ha hello abierto de portal de Azure, podría tener recursos nuevos de toorefresh Hola hoja toosee.</span><span class="sxs-lookup"><span data-stu-id="ae20e-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="ae20e-201">Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio.</span><span class="sxs-lookup"><span data-stu-id="ae20e-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="ae20e-202">Puede tardar varios minutos después de aplicación hello ha finalizado antes de que todos los recursos de Hola y grupo de recursos de Hola se eliminan.</span><span class="sxs-lookup"><span data-stu-id="ae20e-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ae20e-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ae20e-203">Next steps</span></span>

- <span data-ttu-id="ae20e-204">Si había problemas con la implementación de hello, el siguiente paso sería toolook en [solucionar problemas en implementaciones de grupo de recursos con el portal de Azure](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ae20e-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="ae20e-205">Obtener más información sobre hello [biblioteca de Python de Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="ae20e-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

