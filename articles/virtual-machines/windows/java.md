---
title: "Creación y administración de una máquina virtual de Azure con Java | Microsoft Docs"
description: "Use Java y Azure Resource Manager para implementar una máquina virtual y todos sus recursos de apoyo."
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
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b9e739a07c5863577285fb3a221b372b385c6762
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="1ecae-103">Creación y administración de máquinas virtuales Windows en Azure mediante Java</span><span class="sxs-lookup"><span data-stu-id="1ecae-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="1ecae-104">Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles.</span><span class="sxs-lookup"><span data-stu-id="1ecae-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="1ecae-105">En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con Java.</span><span class="sxs-lookup"><span data-stu-id="1ecae-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="1ecae-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="1ecae-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ecae-107">Creación de un proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="1ecae-107">Create a Maven project</span></span>
> * <span data-ttu-id="1ecae-108">Adición de dependencias</span><span class="sxs-lookup"><span data-stu-id="1ecae-108">Add dependencies</span></span>
> * <span data-ttu-id="1ecae-109">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="1ecae-109">Create credentials</span></span>
> * <span data-ttu-id="1ecae-110">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="1ecae-110">Create resources</span></span>
> * <span data-ttu-id="1ecae-111">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="1ecae-111">Perform management tasks</span></span>
> * <span data-ttu-id="1ecae-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="1ecae-112">Delete resources</span></span>
> * <span data-ttu-id="1ecae-113">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1ecae-113">Run the application</span></span>

<span data-ttu-id="1ecae-114">Tardará unos 20 minutos en realizar estos pasos.</span><span class="sxs-lookup"><span data-stu-id="1ecae-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="1ecae-115">Creación de un proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="1ecae-115">Create a Maven project</span></span>

1. <span data-ttu-id="1ecae-116">Si aún no lo ha hecho, instale [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="1ecae-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="1ecae-117">Instale [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="1ecae-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="1ecae-118">Cree una nueva carpeta y el proyecto:</span><span class="sxs-lookup"><span data-stu-id="1ecae-118">Create a new folder and the project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="1ecae-119">Adición de dependencias</span><span class="sxs-lookup"><span data-stu-id="1ecae-119">Add dependencies</span></span>

1. <span data-ttu-id="1ecae-120">En la carpeta `testAzureApp`, abra el archivo `pom.xml` y agregue la configuración de compilación al &lt;proyecto&gt; para habilitar la compilación de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="1ecae-120">Under the `testAzureApp` folder, open the `pom.xml` file and add the build configuration to &lt;project&gt; to enable the building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="1ecae-121">Agregue las dependencias necesarias para acceder al SDK de Java de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ecae-121">Add the dependencies that are needed to access the Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="1ecae-122">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="1ecae-122">Save the file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="1ecae-123">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="1ecae-123">Create credentials</span></span>

<span data-ttu-id="1ecae-124">Antes de empezar este paso, asegúrese de que tiene acceso a una [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1ecae-124">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="1ecae-125">También debe registrar el identificador de aplicación, la clave de autenticación y el identificador del inquilino que necesitará en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="1ecae-125">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="1ecae-126">Creación del archivo de autorización</span><span class="sxs-lookup"><span data-stu-id="1ecae-126">Create the authorization file</span></span>

1. <span data-ttu-id="1ecae-127">Cree un archivo denominado "`azureauth.properties`" y agregar estas propiedades:</span><span class="sxs-lookup"><span data-stu-id="1ecae-127">Create a file named `azureauth.properties` and add these properties to it:</span></span>

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

    <span data-ttu-id="1ecae-128">Reemplace **&lt;subscription-id&gt;** por su identificador de suscripción, **&lt;application-id&gt;** por el identificador de aplicación de Active Directory, **&lt;authentication-key&gt;** por la clave de aplicación y **&lt;tenant-id&gt;** por el identificador de inquilino.</span><span class="sxs-lookup"><span data-stu-id="1ecae-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

2. <span data-ttu-id="1ecae-129">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="1ecae-129">Save the file.</span></span>
3. <span data-ttu-id="1ecae-130">Establezca una variable de entorno denominada "AZURE_AUTH_LOCATION" en el shell con la ruta de acceso completa al archivo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="1ecae-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with the full path to the authentication file.</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="1ecae-131">Creación del cliente de administración</span><span class="sxs-lookup"><span data-stu-id="1ecae-131">Create the management client</span></span>

1. <span data-ttu-id="1ecae-132">Abra el archivo `App.java` en `src\main\java\com\fabrikam` y asegúrese de que esta instrucción del paquete esté en la parte superior:</span><span class="sxs-lookup"><span data-stu-id="1ecae-132">Open the `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at the top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="1ecae-133">En la instrucción del paquete, agregue estas instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="1ecae-133">Under the package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="1ecae-134">Para crear las credenciales de Active Directory que necesita para realizar solicitudes, agregue este código al método Main de la clase App:</span><span class="sxs-lookup"><span data-stu-id="1ecae-134">To create the Active Directory credentials that you need to make requests, add this code to the main method of the App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="1ecae-135">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="1ecae-135">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="1ecae-136">Creación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1ecae-136">Create the resource group</span></span>

<span data-ttu-id="1ecae-137">Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ecae-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="1ecae-138">Para especificar los valores de la aplicación y crear el grupo de recursos, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-138">To specify values for the application and create the resource group, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="1ecae-139">Creación del conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="1ecae-139">Create the availability set</span></span>

<span data-ttu-id="1ecae-140">Los [conjuntos de disponibilidad](tutorial-availability-sets.md) facilitan el mantenimiento de las máquinas virtuales que utiliza la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1ecae-140">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="1ecae-141">Para crear el conjunto de disponibilidad, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-141">To create the availability set, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-the-public-ip-address"></a><span data-ttu-id="1ecae-142">Crear la dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="1ecae-142">Create the public IP address</span></span>

<span data-ttu-id="1ecae-143">Se necesita una [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) para la comunicación con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1ecae-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="1ecae-144">Para crear la dirección IP pública de la máquina virtual, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-144">To create the public IP address for the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="1ecae-145">Crear la red virtual</span><span class="sxs-lookup"><span data-stu-id="1ecae-145">Create the virtual network</span></span>

<span data-ttu-id="1ecae-146">Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ecae-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="1ecae-147">Para crear una subred y una red virtual, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-147">To create a subnet and a virtual network, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="1ecae-148">Creación de la interfaz de red</span><span class="sxs-lookup"><span data-stu-id="1ecae-148">Create the network interface</span></span>

<span data-ttu-id="1ecae-149">Una máquina virtual requiere una interfaz de red para comunicarse en la red virtual que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1ecae-149">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="1ecae-150">Para crear una interfaz de red, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-150">To create a network interface, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-the-virtual-machine"></a><span data-ttu-id="1ecae-151">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1ecae-151">Create the virtual machine</span></span>

<span data-ttu-id="1ecae-152">Ahora que ha creado todos los recursos auxiliares, puede crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1ecae-152">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="1ecae-153">Para crear la máquina virtual, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-153">To create the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter to get information about the VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="1ecae-154">En este tutorial se crea una máquina virtual donde se ejecuta una versión del sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1ecae-154">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="1ecae-155">Para más información sobre cómo seleccionar otras imágenes, consulte [Seleccione y navegue por imágenes de máquina virtual de Azure con PowerShell y la CLI de Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ecae-155">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="1ecae-156">Si desea usar un disco existente en lugar de una imagen de Marketplace, use este código:</span><span class="sxs-lookup"><span data-stu-id="1ecae-156">If you want to use an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="1ecae-157">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="1ecae-157">Perform management tasks</span></span>

<span data-ttu-id="1ecae-158">Durante el ciclo de vida de una máquina virtual, puede ejecutar tareas de administración como iniciar, detener o eliminar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1ecae-158">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="1ecae-159">Además, puede crear código para automatizar tareas repetitivas o complejas.</span><span class="sxs-lookup"><span data-stu-id="1ecae-159">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="1ecae-160">Cuando tenga que hacerlas con la máquina virtual, deberá obtener una instancia de ella.</span><span class="sxs-lookup"><span data-stu-id="1ecae-160">When you need to do anything with the VM, you need to get an instance of it.</span></span> <span data-ttu-id="1ecae-161">Agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-161">Add this code to the try block of the main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="1ecae-162">Obtención de información acerca de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1ecae-162">Get information about the VM</span></span>

<span data-ttu-id="1ecae-163">Para obtener información sobre la máquina virtual, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-163">To get information about the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter to continue...");
input.nextLine();   
```

### <a name="stop-the-vm"></a><span data-ttu-id="1ecae-164">Parada de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1ecae-164">Stop the VM</span></span>

<span data-ttu-id="1ecae-165">Puede detener una máquina virtual y mantener toda su configuración, pero se le seguirá cobrando, o puede detener una máquina virtual y desasignarla.</span><span class="sxs-lookup"><span data-stu-id="1ecae-165">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="1ecae-166">Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.</span><span class="sxs-lookup"><span data-stu-id="1ecae-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="1ecae-167">Para detener la máquina virtual sin desasignarla, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-167">To stop the virtual machine without deallocating it, add this code to the try block in the main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter to continue...");
input.nextLine();
```

<span data-ttu-id="1ecae-168">Si desea desasignar la máquina virtual, cambie la llamada de PowerOff por este código:</span><span class="sxs-lookup"><span data-stu-id="1ecae-168">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```java
vm.deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="1ecae-169">Inicio de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1ecae-169">Start the VM</span></span>

<span data-ttu-id="1ecae-170">Para iniciar la máquina virtual, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-170">To start the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="1ecae-171">Cambio de tamaño de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1ecae-171">Resize the VM</span></span>

<span data-ttu-id="1ecae-172">Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación.</span><span class="sxs-lookup"><span data-stu-id="1ecae-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="1ecae-173">Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1ecae-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="1ecae-174">Para cambiar el tamaño de la máquina virtual, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-174">To change size of the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="1ecae-175">Incorporación de un disco de datos a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1ecae-175">Add a data disk to the VM</span></span>

<span data-ttu-id="1ecae-176">Para agregar un disco de datos a la máquina virtual, agregue este código al bloque Try del método Main para agregar un disco de datos de 2 GB de tamaño, tener un LUN de 0 y un tipo de almacenamiento en caché de lectura y escritura:</span><span class="sxs-lookup"><span data-stu-id="1ecae-176">To add a data disk to the virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code to the try block in the main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter to delete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="1ecae-177">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="1ecae-177">Delete resources</span></span>

<span data-ttu-id="1ecae-178">Dado que se le cobrará por los recursos utilizados en Azure, siempre es conveniente eliminar los recursos que ya no sean necesarios.</span><span class="sxs-lookup"><span data-stu-id="1ecae-178">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="1ecae-179">Si quiere eliminar las máquinas virtuales y todos los recursos auxiliares, lo único que tiene que hacer es eliminar el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1ecae-179">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="1ecae-180">Para eliminar el grupo de recursos, agregue este código al bloque Try del método Main:</span><span class="sxs-lookup"><span data-stu-id="1ecae-180">To delete the resource group, add this code to the try block in the main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="1ecae-181">Guarde el archivo App.java.</span><span class="sxs-lookup"><span data-stu-id="1ecae-181">Save the App.java file.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="1ecae-182">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="1ecae-182">Run the application</span></span>

<span data-ttu-id="1ecae-183">Esta aplicación de consola tardará unos cinco minutos en ejecutarse completamente de principio a fin.</span><span class="sxs-lookup"><span data-stu-id="1ecae-183">It should take about five minutes for this console application to run completely from start to finish.</span></span>

1. <span data-ttu-id="1ecae-184">Para ejecutar la aplicación, use este comando de Maven:</span><span class="sxs-lookup"><span data-stu-id="1ecae-184">To run the application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="1ecae-185">Antes de presionar **Entrar** para comenzar la eliminación de recursos, puede dedicar unos minutos a comprobar la creación de los recursos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1ecae-185">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="1ecae-186">Haga clic en el estado de implementación para ver información de la implementación.</span><span class="sxs-lookup"><span data-stu-id="1ecae-186">Click the deployment status to see information about the deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1ecae-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ecae-187">Next steps</span></span>
* <span data-ttu-id="1ecae-188">Para obtener más información sobre cómo usar las [bibliotecas de Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="1ecae-188">Learn more about using the [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

