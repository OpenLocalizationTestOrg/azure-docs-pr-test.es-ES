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
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Creación y administración de máquinas virtuales Windows en Azure mediante Java

Las [máquinas virtuales de Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) necesitan varios recursos de Azure compatibles. En este artículo se trata la creación, la administración y la eliminación de recursos de máquina virtual con Java. Aprenderá a:

> [!div class="checklist"]
> * Creación de un proyecto de Maven
> * Adición de dependencias
> * Crear credenciales
> * Crear recursos
> * Realizar tareas de administración
> * Eliminar recursos
> * Ejecutar la aplicación hello

Tarda aproximadamente 20 minutos toodo estos pasos.

## <a name="create-a-maven-project"></a>Creación de un proyecto de Maven

1. Si aún no lo ha hecho, instale [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
2. Instale [Maven](http://maven.apache.org/download.cgi).
3. Cree un nuevo proyecto de hello y carpeta:
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Adición de dependencias

1. En hello `testAzureApp` carpeta, abra hello `pom.xml` de archivos y agregue una configuración de compilación de hello demasiado&lt;proyecto&gt; tooenable creación de hello de la aplicación:

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

2. Agregue las dependencias de Hola Hola tooaccess necesarios SDK de Java de Azure.

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

3. Guarde el archivo hello.

## <a name="create-credentials"></a>Crear credenciales

Antes de empezar este paso, asegúrese de que tiene acceso tooan [entidad de servicio de Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). También debe registrar el identificador de la aplicación hello y clave de autenticación de hello, Id. de inquilino de Hola que necesita en un paso posterior.

### <a name="create-hello-authorization-file"></a>Crear archivo de autorización de hello

1. Cree un archivo denominado `azureauth.properties` y agregue estos tooit de propiedades:

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

2. Guarde el archivo hello.
3. Establecer una variable de entorno denominada AZURE_AUTH_LOCATION en el shell con archivo de autenticación de toohello de ruta de acceso completa de hello.

### <a name="create-hello-management-client"></a>Crear el cliente de administración de Hola

1. Abra hello `App.java` de archivos en `src\main\java\com\fabrikam` y asegúrese de que esta declaración de paquete está en la parte superior de hello:

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. En la instrucción de paquete de hello, agrega estas instrucciones de importación:
   
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

2. las credenciales de Active Directory de hello toocreate necesita toomake solicitudes, agregue este método principal de toohello de código de hello clase de aplicación:
   
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

## <a name="create-resources"></a>Crear recursos

### <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

Todos los recursos deben encontrarse en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

toospecify los valores de hello aplicación y crear grupo de recursos de hello, agregue este bloque try de toohello de código en el método main de hello:

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Crear conjunto de disponibilidad de Hola

[Conjuntos de disponibilidad](tutorial-availability-sets.md) resultará más fácil máquinas virtuales toomaintain Hola que usa la aplicación.

disponibilidad de hello toocreate establecer, agregar este bloque try de toohello de código en el método main de hello:

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Crear dirección IP pública de Hola

A [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) es necesario toocommunicate con la máquina virtual de Hola.

dirección IP toocreate Hola pública para la máquina virtual de hello, agregue este bloque try de toohello de código en el método main de hello:

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Crear red virtual de Hola

Debe haber una máquina virtual en una subred de una [red virtual](../../virtual-network/virtual-networks-overview.md).

toocreate una subred y una red virtual, agregue este bloque try de toohello de código en el método main de hello:

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

### <a name="create-hello-network-interface"></a>Crear la interfaz de red de Hola

Una máquina virtual necesita un toocommunicate de interfaz de red en la red virtual de Hola.

toocreate una interfaz de red, agregue este bloque try de toohello de código en el método main de hello:

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

### <a name="create-hello-virtual-machine"></a>Crear la máquina virtual de Hola

Ahora que ha creado Hola todos los recursos de soporte, puede crear una máquina virtual.

toocreate Hola máquina virtual, agregue este bloque try de toohello de código en el método main de hello:

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
> Este tutorial crea una máquina virtual con una versión de sistema operativo de Windows Server de Hola. toolearn más acerca de cómo seleccionar otras imágenes, vea [navegue y seleccione las imágenes de máquina virtual de Azure con Windows PowerShell y hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Si desea toouse un disco existente en lugar de una imagen de marketplace, use este código: 

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

## <a name="perform-management-tasks"></a>Realizar tareas de administración

Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual. Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de código.

Cuando necesite toodo nada con hello VM, debe tooget una instancia del mismo. Agregue este bloque de try toohello de código del método principal de hello:

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Obtener información acerca de hello VM

tooget información acerca de la máquina virtual de hello, agregue este bloque try de toohello de código en el método main de hello:

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

### <a name="stop-hello-vm"></a>Detener Hola VM

Puede detener una máquina virtual y mantener todas sus opciones, pero continuar toobe cobra por él, o puede detener una máquina virtual y cancelar la asignación lo. Cuando se desasigna una máquina virtual, todos los recursos asociados a ella también se desasignan y se le deja de cobrar por ellos.

toostop Hola virtual machine sin cancelar su asignación, agregue este bloque try de toohello de código en el método main de hello:

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

Si desea que la máquina virtual de toodeallocate hello, cambiar código de hello apagado llamada toothis:

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Iniciar Hola VM

toostart Hola máquina virtual, agregue este bloque try de toohello de código en el método main de hello:

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Cambiar el tamaño de hello VM

Para decidir un tamaño de máquina virtual, se deben considerar muchos aspectos de la implementación. Para más información, consulte el artículo sobre los [tamaños de máquina virtual](sizes.md).  

toochange tamaño de máquina virtual de hello, agregue este bloque try de toohello de código en el método main de hello:

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Agregar un toohello de disco de datos VM

tooadd una máquina de virtual disco toohello de datos es de 2 GB de tamaño, tiene un LUN de 0 y un tipo de almacenamiento en caché de lectura y escritura, agregue este bloque try de toohello de código en el método main de hello:

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Eliminar recursos

Dado que se le cobra por recursos que usa en Azure, siempre es recursos toodelete de buena práctica que ya no son necesarios. Si desea que las máquinas virtuales de toodelete Hola y Hola a todos los recursos de soporte todo lo que tiene toodo es el grupo de recursos de Hola de eliminación.

1. recursos de hello toodelete grupo, agregue este bloque try de toohello de código en el método main de hello:
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Guarde el archivo de hello App.java.

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

Tardará aproximadamente cinco minutos para este toorun de aplicación de consola completamente de toofinish de inicio.

1. toorun Hola aplicación, use este comando Maven:

    ```
    mvn compile exec:java
    ```

2. Antes de presionar **ENTRAR** toostart eliminar recursos, podría tardar unos minutos creación de hello tooverify de recursos de Hola Hola portal de Azure. Haga clic en información de toosee de estado de implementación de hello acerca de la implementación de Hola.


## <a name="next-steps"></a>Pasos siguientes
* Más información sobre el uso de hello [bibliotecas de Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).

