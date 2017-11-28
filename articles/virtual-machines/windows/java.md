---
title: "aaaCreate y administrar un Java de uso de máquina Virtual de Azure | Documentos de Microsoft"
description: "Utilice toodeploy Java y el Administrador de recursos de Azure una máquina virtual y todos sus recursos de soporte."
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
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="545ff-103">Creación y administración de máquinas virtuales Windows en Azure mediante Java</span><span class="sxs-lookup"><span data-stu-id="545ff-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="545ff-104">Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles.</span><span class="sxs-lookup"><span data-stu-id="545ff-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="545ff-105">En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con Java.</span><span class="sxs-lookup"><span data-stu-id="545ff-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="545ff-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="545ff-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="545ff-107">Creación de un proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="545ff-107">Create a Maven project</span></span>
> * <span data-ttu-id="545ff-108">Adición de dependencias</span><span class="sxs-lookup"><span data-stu-id="545ff-108">Add dependencies</span></span>
> * <span data-ttu-id="545ff-109">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="545ff-109">Create credentials</span></span>
> * <span data-ttu-id="545ff-110">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="545ff-110">Create resources</span></span>
> * <span data-ttu-id="545ff-111">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="545ff-111">Perform management tasks</span></span>
> * <span data-ttu-id="545ff-112">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="545ff-112">Delete resources</span></span>
> * <span data-ttu-id="545ff-113">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="545ff-113">Run hello application</span></span>

<span data-ttu-id="545ff-114">Tarda aproximadamente 20 minutos toodo estos pasos.</span><span class="sxs-lookup"><span data-stu-id="545ff-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="545ff-115">Creación de un proyecto de Maven</span><span class="sxs-lookup"><span data-stu-id="545ff-115">Create a Maven project</span></span>

1. <span data-ttu-id="545ff-116">Si aún no lo ha hecho, instale [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="545ff-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="545ff-117">Instale [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="545ff-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="545ff-118">Cree un nuevo proyecto de hello y carpeta:</span><span class="sxs-lookup"><span data-stu-id="545ff-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="545ff-119">Adición de dependencias</span><span class="sxs-lookup"><span data-stu-id="545ff-119">Add dependencies</span></span>

1. <span data-ttu-id="545ff-120">En hello `testAzureApp` carpeta, abra hello `pom.xml` de archivos y agregue una configuración de compilación de hello demasiado&lt;proyecto&gt; tooenable creación de hello de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="545ff-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

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

2. <span data-ttu-id="545ff-121">Agregue las dependencias de Hola Hola tooaccess necesarios SDK de Java de Azure.</span><span class="sxs-lookup"><span data-stu-id="545ff-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

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

3. <span data-ttu-id="545ff-122">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="545ff-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="545ff-123">Crear credenciales</span><span class="sxs-lookup"><span data-stu-id="545ff-123">Create credentials</span></span>

<span data-ttu-id="545ff-124">Antes de empezar este paso, asegúrese de que tiene acceso tooan [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="545ff-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="545ff-125">También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesita en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="545ff-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="545ff-126">Crear archivo de autorización de hello</span><span class="sxs-lookup"><span data-stu-id="545ff-126">Create hello authorization file</span></span>

1. <span data-ttu-id="545ff-127">Cree un archivo denominado `azureauth.properties` y agregue estos tooit de propiedades:</span><span class="sxs-lookup"><span data-stu-id="545ff-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="545ff-128">Reemplace  **&lt;Id. de suscripción&gt;**  con su identificador de suscripción,  **&lt;identificador de la aplicación&gt;**  con hello aplicación de Active Directory identificador,  **&lt;clave de autenticación&gt;**  con clave de la aplicación hello, y  **&lt;Id. de inquilino&gt;**  con inquilinos de Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="545ff-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="545ff-129">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="545ff-129">Save hello file.</span></span>
3. <span data-ttu-id="545ff-130">Establecer una variable de entorno denominada AZURE_AUTH_LOCATION en el shell con archivo de autenticación de toohello de ruta de acceso completa de hello.</span><span class="sxs-lookup"><span data-stu-id="545ff-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="545ff-131">Crear el cliente de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="545ff-131">Create hello management client</span></span>

1. <span data-ttu-id="545ff-132">Abra hello `App.java` de archivos en `src\main\java\com\fabrikam` y asegúrese de que esta declaración de paquete está en la parte superior de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="545ff-133">En la instrucción de paquete de hello, agrega estas instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="545ff-133">Under hello package statement, add these import statements:</span></span>
   
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

2. <span data-ttu-id="545ff-134">las credenciales de Active Directory de hello toocreate necesita toomake solicitudes, agregue este método principal de toohello de código de hello clase de aplicación:</span><span class="sxs-lookup"><span data-stu-id="545ff-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
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

## <a name="create-resources"></a><span data-ttu-id="545ff-135">Crear recursos</span><span class="sxs-lookup"><span data-stu-id="545ff-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="545ff-136">Crear grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="545ff-136">Create hello resource group</span></span>

<span data-ttu-id="545ff-137">Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="545ff-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="545ff-138">toospecify los valores de hello aplicación y crear grupo de recursos de hello, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="545ff-139">Crear conjunto de disponibilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="545ff-139">Create hello availability set</span></span>

<span data-ttu-id="545ff-140">[Conjuntos de disponibilidad](tutorial-availability-sets.md) resultará más fácil máquinas virtuales toomaintain Hola que usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="545ff-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="545ff-141">disponibilidad de hello toocreate establecer, agregar este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="545ff-142">Crear dirección IP pública de Hola</span><span class="sxs-lookup"><span data-stu-id="545ff-142">Create hello public IP address</span></span>

<span data-ttu-id="545ff-143">A [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) es necesario toocommunicate con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="545ff-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="545ff-144">dirección IP toocreate Hola pública para la máquina virtual de hello, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="545ff-145">Crear red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="545ff-145">Create hello virtual network</span></span>

<span data-ttu-id="545ff-146">Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="545ff-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="545ff-147">toocreate una subred y una red virtual, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

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

### <a name="create-hello-network-interface"></a><span data-ttu-id="545ff-148">Crear la interfaz de red de Hola</span><span class="sxs-lookup"><span data-stu-id="545ff-148">Create hello network interface</span></span>

<span data-ttu-id="545ff-149">Una máquina virtual necesita un toocommunicate de interfaz de red en la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="545ff-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="545ff-150">toocreate una interfaz de red, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

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

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="545ff-151">Crear la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="545ff-151">Create hello virtual machine</span></span>

<span data-ttu-id="545ff-152">Ahora que ha creado Hola todos los recursos de soporte, puede crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="545ff-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="545ff-153">toocreate Hola máquina virtual, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

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
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="545ff-154">Este tutorial crea una máquina virtual con una versión de sistema operativo de Windows Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="545ff-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="545ff-155">toolearn más acerca de cómo seleccionar otras imágenes, vea [navegue y seleccione las imágenes de máquina virtual de Azure con Windows PowerShell y hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="545ff-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="545ff-156">Si desea toouse un disco existente en lugar de una imagen de marketplace, use este código:</span><span class="sxs-lookup"><span data-stu-id="545ff-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

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

## <a name="perform-management-tasks"></a><span data-ttu-id="545ff-157">Realizar tareas de administración</span><span class="sxs-lookup"><span data-stu-id="545ff-157">Perform management tasks</span></span>

<span data-ttu-id="545ff-158">Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="545ff-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="545ff-159">Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de código.</span><span class="sxs-lookup"><span data-stu-id="545ff-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="545ff-160">Cuando necesite toodo nada con hello VM, debe tooget una instancia del mismo.</span><span class="sxs-lookup"><span data-stu-id="545ff-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="545ff-161">Agregue este bloque de try toohello de código del método principal de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="545ff-162">Obtener información acerca de hello VM</span><span class="sxs-lookup"><span data-stu-id="545ff-162">Get information about hello VM</span></span>

<span data-ttu-id="545ff-163">tooget información acerca de la máquina virtual de hello, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

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
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="545ff-164">Detener Hola VM</span><span class="sxs-lookup"><span data-stu-id="545ff-164">Stop hello VM</span></span>

<span data-ttu-id="545ff-165">Puede detener una máquina virtual y mantener todas sus opciones, pero continuar toobe cobra por él, o puede detener una máquina virtual y cancelar la asignación lo.</span><span class="sxs-lookup"><span data-stu-id="545ff-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="545ff-166">Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.</span><span class="sxs-lookup"><span data-stu-id="545ff-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="545ff-167">toostop Hola virtual machine sin cancelar su asignación, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="545ff-168">Si desea que la máquina virtual de toodeallocate hello, cambiar código de hello apagado llamada toothis:</span><span class="sxs-lookup"><span data-stu-id="545ff-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="545ff-169">Iniciar Hola VM</span><span class="sxs-lookup"><span data-stu-id="545ff-169">Start hello VM</span></span>

<span data-ttu-id="545ff-170">toostart Hola máquina virtual, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="545ff-171">Cambiar el tamaño de hello VM</span><span class="sxs-lookup"><span data-stu-id="545ff-171">Resize hello VM</span></span>

<span data-ttu-id="545ff-172">Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación.</span><span class="sxs-lookup"><span data-stu-id="545ff-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="545ff-173">Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="545ff-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="545ff-174">toochange tamaño de máquina virtual de hello, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="545ff-175">Agregar un toohello de disco de datos VM</span><span class="sxs-lookup"><span data-stu-id="545ff-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="545ff-176">tooadd una máquina de virtual disco toohello de datos es de 2 GB de tamaño, tiene un LUN de 0 y un tipo de almacenamiento en caché de lectura y escritura, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="545ff-177">Eliminar recursos</span><span class="sxs-lookup"><span data-stu-id="545ff-177">Delete resources</span></span>

<span data-ttu-id="545ff-178">Dado que se le cobra por recursos que usa en Azure, siempre es recursos toodelete de buena práctica que ya no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="545ff-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="545ff-179">Si desea que las máquinas virtuales de toodelete Hola y Hola a todos los recursos de soporte todo lo que tiene toodo es el grupo de recursos de Hola de eliminación.</span><span class="sxs-lookup"><span data-stu-id="545ff-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="545ff-180">recursos de hello toodelete grupo, agregue este bloque try de toohello de código en el método main de hello:</span><span class="sxs-lookup"><span data-stu-id="545ff-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="545ff-181">Guarde el archivo de hello App.java.</span><span class="sxs-lookup"><span data-stu-id="545ff-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="545ff-182">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="545ff-182">Run hello application</span></span>

<span data-ttu-id="545ff-183">Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio.</span><span class="sxs-lookup"><span data-stu-id="545ff-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="545ff-184">toorun Hola aplicación, use este comando Maven:</span><span class="sxs-lookup"><span data-stu-id="545ff-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="545ff-185">Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos minutos creación de hello tooverify de recursos de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="545ff-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="545ff-186">Haga clic en información de toosee de estado de implementación de hello acerca de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="545ff-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="545ff-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="545ff-187">Next steps</span></span>
* <span data-ttu-id="545ff-188">Más información sobre el uso de hello [bibliotecas de Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="545ff-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

