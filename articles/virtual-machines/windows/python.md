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
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Creación y administración de máquinas virtuales Windows en Azure con Python

Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles. En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con Python. Aprenderá a:

> [!div class="checklist"]
> * Creación de un proyecto de Visual Studio
> * Instalar paquetes
> * Crear credenciales
> * Crear recursos
> * Realizar tareas de administración
> * Eliminar recursos
> * Ejecutar la aplicación hello

Tarda aproximadamente 20 minutos toodo estos pasos.

## <a name="create-a-visual-studio-project"></a>Creación de un proyecto de Visual Studio

1. Si aún no lo ha hecho, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Seleccione **desarrollo Python** en Hola página cargas de trabajo y, a continuación, haga clic en **instalar**. En resumen de hello, puede ver que **Python 3 de 64 bits (3.6.0)** se selecciona automáticamente. Si ya ha instalado Visual Studio, puede agregar carga de trabajo de Python de hello mediante Hola selector de Visual Studio.
2. Después de instalar e iniciar Visual Studio, haga clic en **Archivo** > **Nuevo** > **Proyecto**.
3. Haga clic en **plantillas** > **Python** > **aplicación de Python**, escriba *myPythonProject* para nombre de Hola del proyecto de hello, Seleccionar ubicación de hello del proyecto de hello y, a continuación, haga clic en **Aceptar**.

## <a name="install-packages"></a>Instalar paquetes

1. En el Explorador de soluciones, bajo *myPythonProject*, haga clic con el botón derecho en **Python Environments** (Entornos de Python) y seleccione **Add virtual environment** (Agregar entorno virtual).
2. En la pantalla de bienvenida agregar entorno Virtual, acepte el nombre de valor predeterminado de Hola de *env*, asegúrese de que *3.6 de Python (64 bits)* está seleccionada para el intérprete de base de hello y, a continuación, haga clic en **crear**.
3. Menú contextual hello *env* entorno que creó, haga clic en **instalar un paquete de Python**, escriba *azure* en Hola cuadro de búsqueda y, a continuación, presione ENTRAR.

Debería ver en las ventanas de salida de hello que paquetes hello azure se han instalado correctamente. 

## <a name="create-credentials"></a>Crear credenciales

Antes de empezar este paso, asegúrese de que tiene una [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesita en un paso posterior.

1. Abra *myPythonProject.py* archivo que se creó y, a continuación, agregar este código tooenable su toorun de aplicación:

    ```python
    if __name__ == "__main__":
    ```

2. código de hello tooimport que es necesario, agregue estos superior de toohello las instrucciones del archivo de Hola .py:

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. A continuación en archivo de .py de hello, agregue variables después de instrucciones de importación de hello toospecify los valores comunes utilizados en Hola código:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Reemplace **subscription-id** por el identificador de la suscripción.

4. las credenciales de Active Directory de hello toocreate necesita toomake solicitudes, agregue esta función después de las variables de hello en el archivo de hello .py:

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Reemplace **identificador de la aplicación**, **clave de autenticación**, y **Id. de inquilino** con valores de hello que previamente recopilados cuando se creó su Azure Active Directory entidad de servicio.

5. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Crear recursos
 
### <a name="initialize-management-clients"></a>Inicialización de los clientes de administración

Clientes de administración necesario toocreate y administración recursos utilizando Hola SDK de Python en Azure. los clientes de administración de toocreate hello, agregue este código en hello **si** instrucción al final, a continuación, del archivo de hello .py:

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

### <a name="create-hello-vm-and-supporting-resources"></a>Crear hello VM y los recursos de soporte

Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

1. toocreate un grupo de recursos, agregue esta función después de las variables de hello en el archivo de hello .py:

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Conjuntos de disponibilidad](tutorial-availability-sets.md) resultará más fácil máquinas virtuales toomaintain Hola que usa la aplicación.

1. conjunto de toocreate una disponibilidad, agregue esta función después de las variables de hello en el archivo de hello .py:
   
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

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

A [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) es necesario toocommunicate con la máquina virtual de Hola.

1. toocreate una dirección IP pública para la máquina virtual de hello, agregue esta función después de las variables de hello en el archivo de hello .py:

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

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).

1. toocreate una red virtual, agregue esta función después de las variables de hello en el archivo de hello .py:

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

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd una red virtual toohello de subred, agregue esta función después de las variables de hello en el archivo de hello .py:
    
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
        
4. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Una máquina virtual necesita un toocommunicate de interfaz de red en la red virtual de Hola.

1. toocreate una interfaz de red, agregue esta función después de las variables de hello en el archivo de hello .py:

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

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Ahora que ha creado Hola todos los recursos de soporte, puede crear una máquina virtual.

1. toocreate Hola máquina virtual, agregue esta función después de las variables de hello en el archivo de hello .py:
   
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
    > Este tutorial crea una máquina virtual con una versión de sistema operativo de Windows Server de Hola. toolearn más acerca de cómo seleccionar otras imágenes, vea [navegue y seleccione las imágenes de máquina virtual de Azure con Windows PowerShell y hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Realizar tareas de administración

Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual. Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de código.

### <a name="get-information-about-hello-vm"></a>Obtener información acerca de hello VM

1. tooget información acerca de la máquina virtual de hello, agregue esta función después de las variables de hello en el archivo de hello .py:

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
2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Detener Hola VM

Puede detener una máquina virtual y mantener todas sus opciones, pero continuar toobe cobra por él, o puede detener una máquina virtual y cancelar la asignación lo. Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.

1. toostop Hola virtual machine sin cancelar su asignación, agregue esta función después de las variables de hello en el archivo de hello .py:

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Si desea que la máquina virtual de toodeallocate hello, cambiar el código de hello power_off llamada toothis:

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Iniciar Hola VM

1. toostart Hola máquina virtual, agregue esta función después de las variables de hello en el archivo de hello .py:

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Cambiar el tamaño de hello VM

Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación. Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).

1. tamaño de hello toochange de máquina virtual de hello, agregue esta función después de las variables de hello en el archivo de hello .py:

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

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Agregar un toohello de disco de datos VM

Las máquinas virtuales pueden tener uno o más [discos de datos](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) que se almacenen en discos duros virtuales.

1. tooadd una máquina virtual de toohello de disco de datos, agregue esta función después de las variables de hello en el archivo de hello .py: 

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

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Eliminar recursos

Dado que se le cobra por recursos que usa en Azure, siempre es un recursos toodelete recomendable que ya no son necesarios. Si desea que las máquinas virtuales de toodelete Hola y Hola a todos los recursos de soporte todo lo que tiene toodo es el grupo de recursos de Hola de eliminación.

1. grupo de recursos de toodelete hello y todos los recursos, agregue esta función después de las variables de hello en el archivo de hello .py:
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. función de hello toocall que agregó anteriormente, agregue este código en hello **si** instrucción al final de hello del Hola .py:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Guarde *myPythonProject.py*.

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

1. aplicación de consola de hello toorun, haga clic en **iniciar** en Visual Studio.

2. Presione **ENTRAR** después de que se devuelve el estado de Hola de cada recurso. En información de estado de hello, debería ver un **correcto** estado de aprovisionamiento. Después de crear la máquina virtual de hello, tendrá Hola oportunidad toodelete todos los recursos de Hola que cree. Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos tooverify minutos su creación en hello portal de Azure. Si ha hello abierto de portal de Azure, podría tener recursos nuevos de toorefresh Hola hoja toosee.  

    Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio. Puede tardar varios minutos después de aplicación hello ha finalizado antes de que todos los recursos de Hola y grupo de recursos de Hola se eliminan.


## <a name="next-steps"></a>Pasos siguientes

- Si había problemas con la implementación de hello, el siguiente paso sería toolook en [solucionar problemas en implementaciones de grupo de recursos con el portal de Azure](../../resource-manager-troubleshoot-deployments-portal.md)
- Obtener más información sobre hello [biblioteca de Python de Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

