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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="04c64-103">Creación y administración de máquinas virtuales Windows en Azure mediante C#</span><span class="sxs-lookup"><span data-stu-id="04c64-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="04c64-104">Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles.</span><span class="sxs-lookup"><span data-stu-id="04c64-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="04c64-105">En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con C#.</span><span class="sxs-lookup"><span data-stu-id="04c64-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="04c64-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="04c64-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="04c64-107">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04c64-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="04c64-108">Instalar el paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-108">Install hello package</span></span>
> * <span data-ttu-id="04c64-109">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="04c64-109">Create credentials</span></span>
> * <span data-ttu-id="04c64-110">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="04c64-110">Create resources</span></span>
> * <span data-ttu-id="04c64-111">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="04c64-111">Perform management tasks</span></span>
> * <span data-ttu-id="04c64-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="04c64-112">Delete resources</span></span>
> * <span data-ttu-id="04c64-113">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="04c64-113">Run hello application</span></span>

<span data-ttu-id="04c64-114">Tarda aproximadamente 20 minutos toodo estos pasos.</span><span class="sxs-lookup"><span data-stu-id="04c64-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="04c64-115">Creación de un proyecto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04c64-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="04c64-116">Si aún no lo ha hecho, instale [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="04c64-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="04c64-117">Seleccione **desarrollo de escritorio de .NET** en Hola página cargas de trabajo y, a continuación, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="04c64-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="04c64-118">En resumen de hello, puede ver que **herramientas de desarrollo de .NET Framework 4-4.6** se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="04c64-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="04c64-119">Si ya ha instalado Visual Studio, puede agregar carga de trabajo de .NET de hello mediante Hola selector de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04c64-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="04c64-120">En Visual Studio, haga clic en **Archivo** > **Nuevo** > **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="04c64-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="04c64-121">En **plantillas** > **Visual C#**, seleccione **aplicación de consola (.NET Framework)**, escriba *myDotnetProject* nombre Hola de Hola proyecto, ubicación de hello seleccione del proyecto de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="04c64-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="04c64-122">Instalar el paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-122">Install hello package</span></span>

<span data-ttu-id="04c64-123">Paquetes de NuGet son hello más fácil manera tooinstall Hola bibliotecas que necesita toofinish estos pasos.</span><span class="sxs-lookup"><span data-stu-id="04c64-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="04c64-124">bibliotecas de hello tooget que necesite en Visual Studio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="04c64-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="04c64-125">Haga clic en **Herramientas** > **Administrador de paquetes Nuget** y, después, haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="04c64-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="04c64-126">Escriba el siguiente comando en la consola de hello:</span><span class="sxs-lookup"><span data-stu-id="04c64-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="04c64-127">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="04c64-127">Create credentials</span></span>

<span data-ttu-id="04c64-128">Antes de empezar este paso, asegúrese de que tiene acceso tooan [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="04c64-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="04c64-129">También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesita en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="04c64-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="04c64-130">Crear archivo de autorización de hello</span><span class="sxs-lookup"><span data-stu-id="04c64-130">Create hello authorization file</span></span>

1. <span data-ttu-id="04c64-131">En el Explorador de soluciones, haga clic en *myDotnetProject* > **Agregar** > **Nuevo elemento** y, después, seleccione **Archivo de texto** en *Elementos de Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="04c64-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="04c64-132">Archivo de nombre hello *azureauth.properties*y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="04c64-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="04c64-133">Agregue estas propiedades de autorización:</span><span class="sxs-lookup"><span data-stu-id="04c64-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="04c64-134">Reemplace  **&lt;Id. de suscripción&gt;**  con su identificador de suscripción,  **&lt;identificador de la aplicación&gt;**  con hello aplicación de Active Directory identificador,  **&lt;clave de autenticación&gt;**  con clave de la aplicación hello, y  **&lt;Id. de inquilino&gt;**  con inquilinos de Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="04c64-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="04c64-135">Guarde el archivo de hello azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="04c64-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="04c64-136">Establecer una variable de entorno de Windows denominado AZURE_AUTH_LOCATION con el archivo de tooauthorization de ruta de acceso completa de hello que ha creado.</span><span class="sxs-lookup"><span data-stu-id="04c64-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="04c64-137">Por ejemplo, puede utilizarse Hola siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="04c64-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="04c64-138">Crear el cliente de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-138">Create hello management client</span></span>

1. <span data-ttu-id="04c64-139">Abrir archivo Program.cs de Hola para proyecto de Hola que creó y, a continuación, agregarlas mediante instrucciones toohello existente en la parte superior del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="04c64-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="04c64-140">cliente de administración de toocreate hello, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="04c64-141">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="04c64-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="04c64-142">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-142">Create hello resource group</span></span>

<span data-ttu-id="04c64-143">Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04c64-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="04c64-144">toospecify los valores de hello aplicación y crear grupo de recursos de hello, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="04c64-145">Crear conjunto de disponibilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-145">Create hello availability set</span></span>

<span data-ttu-id="04c64-146">[Conjuntos de disponibilidad](tutorial-availability-sets.md) resultará más fácil máquinas virtuales toomaintain Hola que usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04c64-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="04c64-147">conjunto de disponibilidad de hello toocreate, agregar este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="04c64-148">Crear dirección IP pública de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-148">Create hello public IP address</span></span>

<span data-ttu-id="04c64-149">A [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) es necesario toocommunicate con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="04c64-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="04c64-150">dirección IP toocreate Hola pública para la máquina virtual de hello, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="04c64-151">Crear red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-151">Create hello virtual network</span></span>

<span data-ttu-id="04c64-152">Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04c64-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="04c64-153">toocreate una subred y una red virtual, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="04c64-154">Crear la interfaz de red de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-154">Create hello network interface</span></span>

<span data-ttu-id="04c64-155">Una máquina virtual necesita un toocommunicate de interfaz de red en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="04c64-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="04c64-156">toocreate una interfaz de red, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-156">toocreate a network interface, add this code toohello Main method:</span></span>

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

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="04c64-157">Crear la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="04c64-157">Create hello virtual machine</span></span>

<span data-ttu-id="04c64-158">Ahora que ha creado Hola todos los recursos de soporte, puede crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04c64-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="04c64-159">toocreate Hola máquina virtual, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

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
> <span data-ttu-id="04c64-160">Este tutorial crea una máquina virtual con una versión de sistema operativo de Windows Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="04c64-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="04c64-161">toolearn más acerca de cómo seleccionar otras imágenes, vea [navegue y seleccione las imágenes de máquina virtual de Azure con Windows PowerShell y hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04c64-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="04c64-162">Si desea toouse un disco existente en lugar de una imagen de marketplace, use este código:</span><span class="sxs-lookup"><span data-stu-id="04c64-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="04c64-163">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="04c64-163">Perform management tasks</span></span>

<span data-ttu-id="04c64-164">Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04c64-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="04c64-165">Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de código.</span><span class="sxs-lookup"><span data-stu-id="04c64-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="04c64-166">Cuando necesite toodo nada con hello VM, debe tooget una instancia de ella:</span><span class="sxs-lookup"><span data-stu-id="04c64-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="04c64-167">Obtener información acerca de hello VM</span><span class="sxs-lookup"><span data-stu-id="04c64-167">Get information about hello VM</span></span>

<span data-ttu-id="04c64-168">tooget información acerca de la máquina virtual de hello, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

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

### <a name="stop-hello-vm"></a><span data-ttu-id="04c64-169">Detener Hola VM</span><span class="sxs-lookup"><span data-stu-id="04c64-169">Stop hello VM</span></span>

<span data-ttu-id="04c64-170">Puede detener una máquina virtual y mantener todas sus opciones, pero continuar toobe cobra por él, o puede detener una máquina virtual y cancelar la asignación lo.</span><span class="sxs-lookup"><span data-stu-id="04c64-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="04c64-171">Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.</span><span class="sxs-lookup"><span data-stu-id="04c64-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="04c64-172">toostop Hola virtual machine sin cancelar su asignación, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="04c64-173">Si desea que la máquina virtual de toodeallocate hello, cambiar código de hello apagado llamada toothis:</span><span class="sxs-lookup"><span data-stu-id="04c64-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="04c64-174">Iniciar Hola VM</span><span class="sxs-lookup"><span data-stu-id="04c64-174">Start hello VM</span></span>

<span data-ttu-id="04c64-175">toostart Hola máquina virtual, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="04c64-176">Cambiar el tamaño de hello VM</span><span class="sxs-lookup"><span data-stu-id="04c64-176">Resize hello VM</span></span>

<span data-ttu-id="04c64-177">Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación.</span><span class="sxs-lookup"><span data-stu-id="04c64-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="04c64-178">Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="04c64-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="04c64-179">toochange tamaño de máquina virtual de hello, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="04c64-180">Agregar un toohello de disco de datos VM</span><span class="sxs-lookup"><span data-stu-id="04c64-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="04c64-181">tooadd una máquina virtual de toohello de disco de datos, agregue este tooadd de método de código toohello Main un disco de datos que es de 2 GB de tamaño, han un LUN de 0 y un tipo de almacenamiento en caché de lectura y escritura:</span><span class="sxs-lookup"><span data-stu-id="04c64-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="04c64-182">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="04c64-182">Delete resources</span></span>

<span data-ttu-id="04c64-183">Dado que se le cobra por recursos que usa en Azure, siempre es recursos toodelete de buena práctica que ya no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="04c64-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="04c64-184">Si desea que las máquinas virtuales de toodelete Hola y Hola a todos los recursos de soporte todo lo que tiene toodo es el grupo de recursos de Hola de eliminación.</span><span class="sxs-lookup"><span data-stu-id="04c64-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="04c64-185">recursos de hello toodelete grupo, agregue este toohello código del método Main:</span><span class="sxs-lookup"><span data-stu-id="04c64-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="04c64-186">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="04c64-186">Run hello application</span></span>

<span data-ttu-id="04c64-187">Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio.</span><span class="sxs-lookup"><span data-stu-id="04c64-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="04c64-188">aplicación de consola de hello toorun, haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="04c64-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="04c64-189">Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos minutos creación de hello tooverify de recursos de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="04c64-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="04c64-190">Haga clic en información de toosee de estado de implementación de hello acerca de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="04c64-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04c64-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04c64-191">Next steps</span></span>
* <span data-ttu-id="04c64-192">Aprovechar las ventajas del uso de una plantilla toocreate una máquina virtual con información de hello en [implementar máquinas virtuales de Azure usando C# y una plantilla de administrador de recursos](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04c64-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="04c64-193">Más información sobre el uso de hello [Azure libraries para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="04c64-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

