---
title: "Creación y administración de una máquina virtual de Azure con C# | Microsoft Docs"
description: "Use C# y Azure Resource Manager para implementar una máquina virtual y todos sus recursos de apoyo."
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
ms.openlocfilehash: 5d9021c2f65b70e36d5ea82992c9fb9d2d6d394a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="78411-103">Creación y administración de máquinas virtuales Windows en Azure mediante C#</span><span class="sxs-lookup"><span data-stu-id="78411-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="78411-104">Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles.</span><span class="sxs-lookup"><span data-stu-id="78411-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="78411-105">En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con C#.</span><span class="sxs-lookup"><span data-stu-id="78411-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="78411-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="78411-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="78411-107">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78411-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="78411-108">Instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="78411-108">Install the package</span></span>
> * <span data-ttu-id="78411-109">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="78411-109">Create credentials</span></span>
> * <span data-ttu-id="78411-110">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="78411-110">Create resources</span></span>
> * <span data-ttu-id="78411-111">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="78411-111">Perform management tasks</span></span>
> * <span data-ttu-id="78411-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="78411-112">Delete resources</span></span>
> * <span data-ttu-id="78411-113">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="78411-113">Run the application</span></span>

<span data-ttu-id="78411-114">Tardará unos 20 minutos en realizar estos pasos.</span><span class="sxs-lookup"><span data-stu-id="78411-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="78411-115">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78411-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="78411-116">Si aún no lo ha hecho, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="78411-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="78411-117">Seleccione **Desarrollo de escritorio de .NET** en la página Cargas de trabajo y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="78411-117">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="78411-118">En el resumen, puede ver que **Herramientas de desarrollo de .NET Framework 4 – 4.6** se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="78411-118">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="78411-119">Si ya ha instalado Visual Studio, puede agregar la carga de trabajo de .NET con el selector de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78411-119">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="78411-120">En Visual Studio, haga clic en **Archivo** > **Nuevo** > **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="78411-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="78411-121">En **Plantillas** > **Visual C#**, seleccione **Aplicación de consola (.NET Framework)**, escriba *myDotnetProject* como nombre del proyecto, seleccione la ubicación del proyecto y, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="78411-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-package"></a><span data-ttu-id="78411-122">Instalación del paquete</span><span class="sxs-lookup"><span data-stu-id="78411-122">Install the package</span></span>

<span data-ttu-id="78411-123">Los paquetes de NuGet son la manera más fácil de instalar las bibliotecas que necesita para finalizar estos pasos.</span><span class="sxs-lookup"><span data-stu-id="78411-123">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="78411-124">Para obtener las bibliotecas que necesita en Visual Studio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="78411-124">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="78411-125">Haga clic en **Herramientas** > **Administrador de paquetes Nuget** y, después, haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="78411-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="78411-126">Escriba el siguiente comando en la consola:</span><span class="sxs-lookup"><span data-stu-id="78411-126">Type this command in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="78411-127">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="78411-127">Create credentials</span></span>

<span data-ttu-id="78411-128">Antes de empezar este paso, asegúrese de que tiene acceso a una [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78411-128">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="78411-129">También debe registrar el identificador de aplicación, la clave de autenticación y el identificador del inquilino que necesitará en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="78411-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="78411-130">Creación del archivo de autorización</span><span class="sxs-lookup"><span data-stu-id="78411-130">Create the authorization file</span></span>

1. <span data-ttu-id="78411-131">En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="78411-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="78411-132">Asigne un nombre al archivo *azureauth.properties* y, luego, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="78411-132">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="78411-133">Agregue estas propiedades de autorización:</span><span class="sxs-lookup"><span data-stu-id="78411-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="78411-134">Reemplace **&lt;subscription-id&gt;** por su identificador de suscripción, **&lt;application-id&gt;** por el identificador de aplicación de Active Directory, **&lt;authentication-key&gt;** por la clave de aplicación y **&lt;tenant-id&gt;** por el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="78411-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="78411-135">Guarde el archivo azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="78411-135">Save the azureauth.properties file.</span></span> 
4. <span data-ttu-id="78411-136">Establezca una variable de entorno de Windows denominada AZURE_AUTH_LOCATION con la ruta de acceso completa al archivo de autorización que ha creado.</span><span class="sxs-lookup"><span data-stu-id="78411-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created.</span></span> <span data-ttu-id="78411-137">Por ejemplo, puede usar el comando de PowerShell siguiente:</span><span class="sxs-lookup"><span data-stu-id="78411-137">For example, the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-the-management-client"></a><span data-ttu-id="78411-138">Creación del cliente de administración</span><span class="sxs-lookup"><span data-stu-id="78411-138">Create the management client</span></span>

1. <span data-ttu-id="78411-139">Abra el archivo Program.cs del proyecto que ha creado y agregue las siguientes instrucciones using a las instrucciones existentes en la parte superior del archivo:</span><span class="sxs-lookup"><span data-stu-id="78411-139">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="78411-140">Para crear el cliente de administración, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-140">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="78411-141">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="78411-141">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="78411-142">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="78411-142">Create the resource group</span></span>

<span data-ttu-id="78411-143">Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78411-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="78411-144">Para especificar los valores de la aplicación y crear el grupo de recursos, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-144">To specify values for the application and create the resource group, add this code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="78411-145">Creación del conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="78411-145">Create the availability set</span></span>

<span data-ttu-id="78411-146">Los [conjuntos de disponibilidad](tutorial-availability-sets.md) facilitan el mantenimiento de las máquinas virtuales que utiliza la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78411-146">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="78411-147">Para crear el conjunto de disponibilidad, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-147">To create the availability set, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-the-public-ip-address"></a><span data-ttu-id="78411-148">Crear la dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="78411-148">Create the public IP address</span></span>

<span data-ttu-id="78411-149">Se necesita una [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) para la comunicación con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78411-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="78411-150">Para crear la dirección IP pública de la máquina virtual, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-150">To create the public IP address for the virtual machine, add this code to the Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="78411-151">Crear la red virtual</span><span class="sxs-lookup"><span data-stu-id="78411-151">Create the virtual network</span></span>

<span data-ttu-id="78411-152">Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78411-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="78411-153">Para crear una subred y una red virtual, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-153">To create a subnet and a virtual network, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="78411-154">Creación de la interfaz de red</span><span class="sxs-lookup"><span data-stu-id="78411-154">Create the network interface</span></span>

<span data-ttu-id="78411-155">Una máquina virtual requiere una interfaz de red para comunicarse en la red virtual que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="78411-155">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="78411-156">Para crear una interfaz de red, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-156">To create a network interface, add this code to the Main method:</span></span>

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

### <a name="create-the-virtual-machine"></a><span data-ttu-id="78411-157">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78411-157">Create the virtual machine</span></span>

<span data-ttu-id="78411-158">Ahora que ha creado todos los recursos auxiliares, puede crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78411-158">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="78411-159">Para crear la máquina virtual, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-159">To create the virtual machine, add this code to the Main method:</span></span>

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
> <span data-ttu-id="78411-160">En este tutorial se crea una máquina virtual donde se ejecuta una versión del sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="78411-160">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="78411-161">Para más información sobre cómo seleccionar otras imágenes, consulte [Seleccione y navegue por imágenes de máquina virtual de Azure con PowerShell y la CLI de Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78411-161">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="78411-162">Si desea usar un disco existente en lugar de una imagen de Marketplace, use este código:</span><span class="sxs-lookup"><span data-stu-id="78411-162">If you want to use an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="78411-163">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="78411-163">Perform management tasks</span></span>

<span data-ttu-id="78411-164">Durante el ciclo de vida de una máquina virtual, puede ejecutar tareas de administración como iniciar, detener o eliminar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="78411-164">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="78411-165">Además, puede crear código para automatizar tareas repetitivas o complejas.</span><span class="sxs-lookup"><span data-stu-id="78411-165">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="78411-166">Cuando tenga que hacerlas con la máquina virtual, deberá obtener una instancia de ella:</span><span class="sxs-lookup"><span data-stu-id="78411-166">When you need to do anything with the VM, you need to get an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="78411-167">Obtención de información acerca de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78411-167">Get information about the VM</span></span>

<span data-ttu-id="78411-168">Para obtener información acerca de la máquina virtual, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-168">To get information about the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Getting information about the virtual machine...");
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
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="stop-the-vm"></a><span data-ttu-id="78411-169">Parada de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78411-169">Stop the VM</span></span>

<span data-ttu-id="78411-170">Puede detener una máquina virtual y mantener toda su configuración, pero se le seguirá cobrando, o puede detener una máquina virtual y desasignarla.</span><span class="sxs-lookup"><span data-stu-id="78411-170">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="78411-171">Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.</span><span class="sxs-lookup"><span data-stu-id="78411-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="78411-172">Para detener la máquina virtual sin desasignarla, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-172">To stop the virtual machine without deallocating it, add this code to the Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

<span data-ttu-id="78411-173">Si desea desasignar la máquina virtual, cambie la llamada de PowerOff por este código:</span><span class="sxs-lookup"><span data-stu-id="78411-173">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```
vm.Deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="78411-174">Inicio de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78411-174">Start the VM</span></span>

<span data-ttu-id="78411-175">Para iniciar la máquina virtual, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-175">To start the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="78411-176">Cambio de tamaño de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78411-176">Resize the VM</span></span>

<span data-ttu-id="78411-177">Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación.</span><span class="sxs-lookup"><span data-stu-id="78411-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="78411-178">Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="78411-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="78411-179">Para cambiar el tamaño de la máquina virtual, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-179">To change size of the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="78411-180">Incorporación de un disco de datos a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="78411-180">Add a data disk to the VM</span></span>

<span data-ttu-id="78411-181">Para agregar un disco de datos a la máquina virtual, agregue este código al método Main para agregar un disco de datos de 2 GB de tamaño, tener un LUN de 0 y un tipo de almacenamiento en caché de lectura y escritura:</span><span class="sxs-lookup"><span data-stu-id="78411-181">To add a data disk to the virtual machine, add this code to the Main method to add a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk to vm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter to delete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="78411-182">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="78411-182">Delete resources</span></span>

<span data-ttu-id="78411-183">Dado que se le cobrará por los recursos utilizados en Azure, siempre es conveniente eliminar los recursos que ya no sean necesarios.</span><span class="sxs-lookup"><span data-stu-id="78411-183">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="78411-184">Si quiere eliminar las máquinas virtuales y todos los recursos auxiliares, lo único que tiene que hacer es eliminar el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="78411-184">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

<span data-ttu-id="78411-185">Para eliminar el grupo de recursos, agregue este código al método Main:</span><span class="sxs-lookup"><span data-stu-id="78411-185">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="78411-186">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="78411-186">Run the application</span></span>

<span data-ttu-id="78411-187">Esta aplicación de consola tardará unos cinco minutos en ejecutarse completamente de principio a fin.</span><span class="sxs-lookup"><span data-stu-id="78411-187">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="78411-188">Para ejecutar la aplicación de consola, haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="78411-188">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="78411-189">Antes de presionar **Entrar** para comenzar la eliminación de recursos, puede dedicar unos minutos a comprobar la creación de los recursos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="78411-189">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="78411-190">Haga clic en el estado de implementación para ver información de la implementación.</span><span class="sxs-lookup"><span data-stu-id="78411-190">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78411-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78411-191">Next steps</span></span>
* <span data-ttu-id="78411-192">Aproveche las ventajas de usar una plantilla para crear una máquina virtual con la información que se muestra en [Implementación de una máquina virtual de Azure con C# y una plantilla de Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78411-192">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="78411-193">Para más información acerca del uso de las [bibliotecas de Azure para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="78411-193">Learn more about using the [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

