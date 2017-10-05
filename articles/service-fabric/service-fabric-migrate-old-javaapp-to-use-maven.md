---
title: "Migración del SDK de Java a Maven: actualización de las aplicaciones Java anteriores de Azure Service Fabric para usar Maven | Microsoft Docs"
description: "Actualice las aplicaciones de Java anteriores que usaban el SDK de Java de Service Fabric para capturar las dependencias de Java de Service Fabric desde Maven. Después de completar esta instalación, sus aplicaciones de Java anteriores podrían compilarse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 2123c5f26d77045bd22af56a844fdbf222930e7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="update-your-previous-java-service-fabric-application-to-fetch-java-libraries-from-maven"></a><span data-ttu-id="ebbc1-104">Actualice la aplicación de Java de Service Fabric anterior para capturar las bibliotecas de Java desde Maven</span><span class="sxs-lookup"><span data-stu-id="ebbc1-104">Update your previous Java Service Fabric application to fetch Java libraries from Maven</span></span>
<span data-ttu-id="ebbc1-105">Recientemente, se han transferido los archivos binarios de Java de Service Fabric desde el SDK de Java de Service Fabric al hospedaje de Maven.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-105">We have recently moved Service Fabric Java binaries from the Service Fabric Java SDK to Maven hosting.</span></span> <span data-ttu-id="ebbc1-106">Ahora puede usar **mavencentral** para capturar las dependencias de Java de Service Fabric más recientes.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-106">Now you can use **mavencentral** to fetch the latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="ebbc1-107">Esta guía de inicio rápido le ayuda a actualizar las aplicaciones de Java existentes, que creó anteriormente para usarse con el SDK de Java de Service Fabric, utilizando cualquier plantilla Yeoman o Eclipse, para ser compatibles con la compilación basada en Maven.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-107">This quick-start helps you update your existing Java applications, which you earlier created to be used with Service Fabric Java SDK, using either Yeoman template or Eclipse, to be compatible with the Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebbc1-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ebbc1-108">Prerequisites</span></span>
1. <span data-ttu-id="ebbc1-109">Primero debe desinstalar el SDK de Java existente.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-109">First you need to uninstall the existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="ebbc1-110">Instale la CLI de Service Fabric más reciente siguiendo los pasos mencionados [aquí](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ebbc1-110">Install the latest Service Fabric CLI following the steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="ebbc1-111">Para compilar y trabajar con las aplicaciones de Java de Service Fabric debe asegurarse de que tiene JDK 1.8 y Gradle instalados.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-111">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="ebbc1-112">Si aún no se han instalado, puede ejecutar el siguiente procedimiento para instalar JDK 1.8 (openjdk-8-jdk) y Gradle:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-112">If not yet installed, you can run the following to install JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="ebbc1-113">Actualice los scripts de instalación o desinstalación de la aplicación para utilizar la nueva CLI de Service Fabric siguiendo los pasos mencionados [aquí](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="ebbc1-113">Update the install/uninstall scripts of your application to use the new Service Fabric CLI following the steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="ebbc1-114">Puede hacer referencia a nuestros [ejemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) de introducción como referencia.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-114">You can refer to our getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="ebbc1-115">Después de desinstalar el SDK de Java de Service Fabric, Yeoman no funcionará.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-115">After uninstalling the Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="ebbc1-116">Siga los requisitos previos mencionados [aquí](service-fabric-create-your-first-linux-application-with-java.md) para que el generador de plantillas Java de Yeoman de Service Fabric funcione.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-116">Follow the Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) to have Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="ebbc1-117">Bibliotecas de Java de Service Fabric en Maven</span><span class="sxs-lookup"><span data-stu-id="ebbc1-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="ebbc1-118">Las bibliotecas de Java de Service Fabric han sido hospedadas en Maven.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="ebbc1-119">Puede agregar las dependencias en el archivo ``pom.xml`` o ``build.gradle`` de sus proyectos para usar las bibliotecas de Java de Service Fabric desde **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-119">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="ebbc1-120">Actores</span><span class="sxs-lookup"><span data-stu-id="ebbc1-120">Actors</span></span>

<span data-ttu-id="ebbc1-121">Compatibilidad con Reliable Actor de Service Fabric para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="ebbc1-122">Services</span><span class="sxs-lookup"><span data-stu-id="ebbc1-122">Services</span></span>

<span data-ttu-id="ebbc1-123">Compatibilidad con el servicio sin estado de Service Fabric para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="ebbc1-124">Otros</span><span class="sxs-lookup"><span data-stu-id="ebbc1-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="ebbc1-125">Transporte</span><span class="sxs-lookup"><span data-stu-id="ebbc1-125">Transport</span></span>

<span data-ttu-id="ebbc1-126">Compatibilidad de la capa de transporte para aplicaciones Java de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="ebbc1-127">No es necesario agregar explícitamente esta dependencia a sus aplicaciones Reliable Actor o de servicio, a menos que programe la capa de transporte.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-127">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="ebbc1-128">Compatibilidad con Fabric</span><span class="sxs-lookup"><span data-stu-id="ebbc1-128">Fabric support</span></span>

<span data-ttu-id="ebbc1-129">Compatibilidad en el nivel de sistema para Service Fabric, que se comunica con el entorno de tiempo de ejecución nativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-129">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="ebbc1-130">No es necesario agregar explícitamente esta dependencia a sus aplicaciones Reliable Actor o de servicio.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-130">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="ebbc1-131">Se recuperan automáticamente desde Maven, cuando se incluyen las dependencias anteriores.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-131">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="ebbc1-132">Migración del servicio sin estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebbc1-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="ebbc1-133">Para poder crear su servicio de Java sin estado de Service Fabric existente con las dependencias de Service Fabric capturadas desde Maven, debe actualizar el archivo ``build.gradle`` dentro del servicio.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-133">To be able to build your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need to update the ``build.gradle`` file inside the Service.</span></span> <span data-ttu-id="ebbc1-134">Antes solían ser como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-134">Previously it used to be like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="ebbc1-135">Ahora, para capturar las dependencias desde Maven, el archivo **actualizado** ``build.gradle`` tendría los elementos correspondientes como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-135">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="ebbc1-136">En general, para hacerse una idea general acerca de cómo sería el script de compilación para un servicio Java sin estado de Service Fabric, puede remitirse a cualquiera de nuestros ejemplos de introducción.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-136">In general, to get an overall idea about how the build script would look like for a Service Fabric stateless Java service, you can refer to any sample from our getting-started examples.</span></span> <span data-ttu-id="ebbc1-137">Este es el archivo [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) del ejemplo EchoServer.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-137">Here is the [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for the EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="ebbc1-138">Migración del servicio Actor de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebbc1-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="ebbc1-139">Para poder crear su aplicación Java Actor de Service Fabric existente con las dependencias de Service Fabric capturadas desde Maven, debe actualizar el archivo ``build.gradle`` dentro del paquete de interfaz y en el paquete de servicio.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-139">To be able to build your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need to update the ``build.gradle`` file inside the interface package and in the Service package.</span></span> <span data-ttu-id="ebbc1-140">Si tiene un paquete TestClient, debe actualizarlo también.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-140">If you have a TestClient package, you need to update that as well.</span></span> <span data-ttu-id="ebbc1-141">Así, para el actor ``Myactor``, lo siguiente sería localizar los lugares donde necesita actualizar:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-141">So, for your actor ``Myactor``, the following would be the places where you need to update -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-the-interface-project"></a><span data-ttu-id="ebbc1-142">Actualización del script de compilación para el proyecto de interfaz</span><span class="sxs-lookup"><span data-stu-id="ebbc1-142">Updating build script for the interface project</span></span>

<span data-ttu-id="ebbc1-143">Antes solían ser como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-143">Previously it used to be like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="ebbc1-144">Ahora, para capturar las dependencias desde Maven, el archivo **actualizado** ``build.gradle`` tendría los elementos correspondientes como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-144">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-the-actor-project"></a><span data-ttu-id="ebbc1-145">Actualización del script de compilación para el proyecto de actor</span><span class="sxs-lookup"><span data-stu-id="ebbc1-145">Updating build script for the actor project</span></span>

<span data-ttu-id="ebbc1-146">Antes solían ser como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-146">Previously it used to be like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="ebbc1-147">Ahora, para capturar las dependencias desde Maven, el archivo **actualizado** ``build.gradle`` tendría los elementos correspondientes como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-147">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-the-test-client-project"></a><span data-ttu-id="ebbc1-148">Actualización del script de compilación para el proyecto de cliente de prueba</span><span class="sxs-lookup"><span data-stu-id="ebbc1-148">Updating build script for the test client project</span></span>

<span data-ttu-id="ebbc1-149">Los cambios aquí son similares a los que se describen en la sección anterior, es decir, el proyecto de actor.</span><span class="sxs-lookup"><span data-stu-id="ebbc1-149">Changes here are similar to the changes discussed in previous section, that is, the actor project.</span></span> <span data-ttu-id="ebbc1-150">Anteriormente el script Gradle solía ser como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-150">Previously the Gradle script used to be like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="ebbc1-151">Ahora, para capturar las dependencias desde Maven, el archivo **actualizado** ``build.gradle`` tendría los elementos correspondientes como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="ebbc1-151">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="ebbc1-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebbc1-152">Next steps</span></span>

* [<span data-ttu-id="ebbc1-153">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman</span><span class="sxs-lookup"><span data-stu-id="ebbc1-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="ebbc1-154">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con el complemento de Eclipse para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebbc1-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="ebbc1-155">Interacción con los clústeres de Service Fabric mediante la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ebbc1-155">Interact with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
