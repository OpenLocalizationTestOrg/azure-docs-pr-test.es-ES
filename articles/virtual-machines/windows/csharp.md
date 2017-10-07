---
title: "aaaCreate y administrar un Azure Máquina Virtual usando C# | Documentos de Microsoft"
description: "Use C# y el Administrador de recursos de Azure toodeploy una máquina virtual y todos sus recursos de soporte."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Creación y administración de máquinas virtuales Windows en Azure mediante C# #

Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles. En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con C#. Aprenderá a:

> [!div class="checklist"]
> * Creación de un proyecto de Visual Studio
> * Instalar el paquete de Hola
> * Crear credenciales
> * Crear recursos
> * Realizar tareas de administración
> * Eliminar recursos
> * Ejecutar la aplicación hello

Tarda aproximadamente 20 minutos toodo estos pasos.

## <a name="create-a-visual-studio-project"></a>Creación de un proyecto de Visual Studio

1. Si aún no lo ha hecho, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Seleccione **desarrollo de escritorio de .NET** en Hola página cargas de trabajo y, a continuación, haga clic en **instalar**. En resumen de hello, puede ver que **herramientas de desarrollo de .NET Framework 4-4.6** se selecciona automáticamente. Si ya ha instalado Visual Studio, puede agregar carga de trabajo de .NET de hello mediante Hola selector de Visual Studio.
2. En Visual Studio, haga clic en **Archivo** > **Nuevo** > **proyecto**.
3. En **plantillas** > **Visual C#**, seleccione **aplicación de consola (.NET Framework)**, escriba *myDotnetProject* nombre Hola de Hola proyecto, ubicación de hello seleccione del proyecto de hello y, a continuación, haga clic en **Aceptar**.

## <a name="install-hello-package"></a>Instalar el paquete de Hola

Paquetes de NuGet son hello más fácil manera tooinstall Hola bibliotecas que necesita toofinish estos pasos. bibliotecas de hello tooget que necesite en Visual Studio, siga estos pasos:

1. Haga clic en **Herramientas** > **Administrador de paquetes Nuget** y, después, haga clic en **Consola del Administrador de paquetes**.
2. Escriba el siguiente comando en la consola de hello:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Crear credenciales

Antes de empezar este paso, asegúrese de que tiene acceso tooan [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesita en un paso posterior.

### <a name="create-hello-authorization-file"></a>Crear archivo de autorización de hello

1. En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*. Archivo de nombre hello *azureauth.properties*y, a continuación, haga clic en **agregar**.
2. Agregue estas propiedades de autorización:

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    Reemplace  **&lt;Id. de suscripción&gt;**  con su identificador de suscripción,  **&lt;identificador de la aplicación&gt;**  con hello aplicación de Active Directory identificador,  **&lt;clave de autenticación&gt;**  con clave de la aplicación hello, y  **&lt;Id. de inquilino&gt;**  con inquilinos de Hola identificador.

3. Guarde el archivo de hello azureauth.properties. 
4. Establecer una variable de entorno de Windows denominado AZURE_AUTH_LOCATION con el archivo de tooauthorization de ruta de acceso completa de hello que ha creado. Por ejemplo, puede utilizarse Hola siguiente comando de PowerShell:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Crear el cliente de administración de Hola

1. Abrir archivo Program.cs de Hola para proyecto de Hola que creó y, a continuación, agregarlas mediante instrucciones toohello existente en la parte superior del archivo hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. cliente de administración de toocreate hello, agregue este toohello código del método Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Crear recursos

### <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

toospecify los valores de hello aplicación y crear grupo de recursos de hello, agregue este toohello código del método Main:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Crear conjunto de disponibilidad de Hola

[Conjuntos de disponibilidad](tutorial-availability-sets.md) resultará más fácil máquinas virtuales toomaintain Hola que usa la aplicación.

conjunto de disponibilidad de hello toocreate, agregar este toohello código del método Main:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Crear dirección IP pública de Hola

A [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) es necesario toocommunicate con la máquina virtual de Hola.

dirección IP toocreate Hola pública para la máquina virtual de hello, agregue este toohello código del método Main:
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Crear red virtual de Hola

Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).

toocreate una subred y una red virtual, agregue este toohello código del método Main:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Crear la interfaz de red de Hola

Una máquina virtual necesita un toocommunicate de interfaz de red en la red virtual de Hola.

toocreate una interfaz de red, agregue este toohello código del método Main:

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a>Crear la máquina virtual de Hola

Ahora que ha creado Hola todos los recursos de soporte, puede crear una máquina virtual.

toocreate Hola máquina virtual, agregue este toohello código del método Main:

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> Este tutorial crea una máquina virtual con una versión de sistema operativo de Windows Server de Hola. toolearn más acerca de cómo seleccionar otras imágenes, vea [navegue y seleccione las imágenes de máquina virtual de Azure con Windows PowerShell y hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Si desea toouse un disco existente en lugar de una imagen de marketplace, use este código:

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a>Realizar tareas de administración

Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual. Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de código.

Cuando necesite toodo nada con hello VM, debe tooget una instancia de ella:

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Obtener información acerca de hello VM

tooget información acerca de la máquina virtual de hello, agregue este toohello código del método Main:

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a>Detener Hola VM

Puede detener una máquina virtual y mantener todas sus opciones, pero continuar toobe cobra por él, o puede detener una máquina virtual y cancelar la asignación lo. Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.

toostop Hola virtual machine sin cancelar su asignación, agregue este toohello código del método Main:

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Si desea que la máquina virtual de toodeallocate hello, cambiar código de hello apagado llamada toothis:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Iniciar Hola VM

toostart Hola máquina virtual, agregue este toohello código del método Main:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Cambiar el tamaño de hello VM

Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación. Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).  

toochange tamaño de máquina virtual de hello, agregue este toohello código del método Main:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Agregar un toohello de disco de datos VM

tooadd una máquina virtual de toohello de disco de datos, agregue este tooadd de método de código toohello Main un disco de datos que es de 2 GB de tamaño, han un LUN de 0 y un tipo de almacenamiento en caché de lectura y escritura:

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Eliminar recursos

Dado que se le cobra por recursos que usa en Azure, siempre es recursos toodelete de buena práctica que ya no son necesarios. Si desea que las máquinas virtuales de toodelete Hola y Hola a todos los recursos de soporte todo lo que tiene toodo es el grupo de recursos de Hola de eliminación.

recursos de hello toodelete grupo, agregue este toohello código del método Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio. 

1. aplicación de consola de hello toorun, haga clic en **iniciar**.

2. Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos minutos creación de hello tooverify de recursos de Hola Hola portal de Azure. Haga clic en información de toosee de estado de implementación de hello acerca de la implementación de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Aprovechar las ventajas del uso de una plantilla toocreate una máquina virtual con información de hello en [implementar máquinas virtuales de Azure usando C# y una plantilla de administrador de recursos](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Más información sobre el uso de hello [Azure libraries para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

