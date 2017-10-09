---
title: aaaMigrate del SDK de Java tooMaven - actualizar toouse de aplicaciones de Java de Azure Service Fabric antiguo Maven | Documentos de Microsoft
description: "Actualizar Hola Java aplicaciones anteriores que usa toouse Hola SDK de Java del tejido de servicio, las dependencias de Java de tejido de servicio de toofetch de Maven. Después de completar la instalación, las aplicaciones de Java anteriores sería capaz de toobuild."
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
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="03fa0-104">Actualizar las bibliotecas de Java anteriores de toofetch aplicación de Java Service Fabric desde Maven</span><span class="sxs-lookup"><span data-stu-id="03fa0-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="03fa0-105">Recientemente se han transferido los archivos binarios de Java de tejido de servicio de hello servicio SDK de Java de tejido tooMaven hospedaje.</span><span class="sxs-lookup"><span data-stu-id="03fa0-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="03fa0-106">Ahora puede usar **mavencentral** dependencias de Java de tejido de servicio más recientes de toofetch Hola.</span><span class="sxs-lookup"><span data-stu-id="03fa0-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="03fa0-107">Este inicio rápido le ayuda a actualizar las aplicaciones de Java existentes, que creó anteriormente toobe se usa con el SDK de Java de tejido de servicio, utilizando a cualquier Yeoman Eclipse, toobe compatible con la compilación de Maven en función de Hola o plantilla.</span><span class="sxs-lookup"><span data-stu-id="03fa0-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03fa0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="03fa0-108">Prerequisites</span></span>
1. <span data-ttu-id="03fa0-109">En primer lugar debe toouninstall Hola existente SDK de Java.</span><span class="sxs-lookup"><span data-stu-id="03fa0-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="03fa0-110">Siguiente de CLI de tejido de servicio más reciente de instalación Hola Hola pasos mencionados [aquí](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="03fa0-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="03fa0-111">toobuild y trabajo en aplicaciones de Java de tejido de servicio de hello, deberá tooensure que tiene JDK 1.8 y Gradle instalados.</span><span class="sxs-lookup"><span data-stu-id="03fa0-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="03fa0-112">Si aún no se ha instalado, puede ejecutar Hola siguientes tooinstall JDK 1.8 (openjdk-8-jdk) y Gradle -</span><span class="sxs-lookup"><span data-stu-id="03fa0-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="03fa0-113">Scripts de instalación/desinstalación Hola de actualización de la aplicación toouse Hola nueva CLI de tejido de servicio siguiendo los pasos de hello mencionados [aquí](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="03fa0-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="03fa0-114">Se puede hacer referencia tooour Introducción [ejemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) como referencia.</span><span class="sxs-lookup"><span data-stu-id="03fa0-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="03fa0-115">Después de desinstalar Hola servicio SDK de Java de tejido, Yeoman no funcionará.</span><span class="sxs-lookup"><span data-stu-id="03fa0-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="03fa0-116">Siga los requisitos previos de hello mencionados [aquí](service-fabric-create-your-first-linux-application-with-java.md) toohave Yeoman de tejido de servicio Java generador de plantilla de seguridad y en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="03fa0-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="03fa0-117">Bibliotecas de Java de Service Fabric en Maven</span><span class="sxs-lookup"><span data-stu-id="03fa0-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="03fa0-118">Las bibliotecas de Java de Service Fabric han sido hospedadas en Maven.</span><span class="sxs-lookup"><span data-stu-id="03fa0-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="03fa0-119">También puede agregar dependencias de Hola Hola ``pom.xml`` o ``build.gradle`` de las bibliotecas de Java de tejido de servicio de proyectos toouse desde **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="03fa0-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="03fa0-120">Actores</span><span class="sxs-lookup"><span data-stu-id="03fa0-120">Actors</span></span>

<span data-ttu-id="03fa0-121">Compatibilidad con Reliable Actor de Service Fabric para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03fa0-121">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="03fa0-122">Services</span><span class="sxs-lookup"><span data-stu-id="03fa0-122">Services</span></span>

<span data-ttu-id="03fa0-123">Compatibilidad con el servicio sin estado de Service Fabric para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03fa0-123">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="03fa0-124">Otros</span><span class="sxs-lookup"><span data-stu-id="03fa0-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="03fa0-125">Transporte</span><span class="sxs-lookup"><span data-stu-id="03fa0-125">Transport</span></span>

<span data-ttu-id="03fa0-126">Compatibilidad de la capa de transporte para aplicaciones Java de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="03fa0-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="03fa0-127">No es necesario tooexplicitly agregar esta dependencia tooyour Actor confiable o aplicaciones de servicio, a menos que se programan en la capa de transporte de Hola.</span><span class="sxs-lookup"><span data-stu-id="03fa0-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="03fa0-128">Compatibilidad con Fabric</span><span class="sxs-lookup"><span data-stu-id="03fa0-128">Fabric support</span></span>

<span data-ttu-id="03fa0-129">Compatibilidad de nivel de sistema para Service Fabric, que se comunica en tiempo de ejecución de toonative Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="03fa0-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="03fa0-130">No es necesario tooexplicitly agregar esta dependencia tooyour Actor confiable o las aplicaciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="03fa0-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="03fa0-131">Esto obtiene capturan automáticamente desde Maven, al incluir Hola otras dependencias anteriores.</span><span class="sxs-lookup"><span data-stu-id="03fa0-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="03fa0-132">Migración del servicio sin estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="03fa0-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="03fa0-133">toobe toobuild capaz de su Service Fabric sin estado Java servicio existente con dependencias de Service Fabric Maven se captura, necesita hello tooupdate ``build.gradle`` archivo dentro de hello servicio.</span><span class="sxs-lookup"><span data-stu-id="03fa0-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="03fa0-134">Usaban toobe como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-134">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="03fa0-135">Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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
<span data-ttu-id="03fa0-136">En general, tooget una idea general acerca de cómo crear Hola de script sería similar para un servicio de Service Fabric sin estado Java, puede consultar tooany ejemplo de nuestros ejemplos de iniciación.</span><span class="sxs-lookup"><span data-stu-id="03fa0-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="03fa0-137">Aquí es hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) de ejemplo de Hola a EchoServer.</span><span class="sxs-lookup"><span data-stu-id="03fa0-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="03fa0-138">Migración del servicio Actor de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="03fa0-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="03fa0-139">toobe toobuild capaz de la aplicación existente de Service Fabric Actor Java con dependencias de Service Fabric Maven se captura, necesita hello tooupdate ``build.gradle`` archivo dentro del paquete de interfaz de Hola y en el paquete del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="03fa0-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="03fa0-140">Si tiene un paquete TestClient, necesita tooupdate es así.</span><span class="sxs-lookup"><span data-stu-id="03fa0-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="03fa0-141">Así, para su actor ``Myactor``, siguiente Hola sería lugares hello en las que necesite tooupdate -</span><span class="sxs-lookup"><span data-stu-id="03fa0-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="03fa0-142">Actualización del script de compilación para el proyecto de la interfaz de Hola</span><span class="sxs-lookup"><span data-stu-id="03fa0-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="03fa0-143">Usaban toobe como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="03fa0-144">Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="03fa0-145">Actualización del script de compilación para el proyecto de actor Hola</span><span class="sxs-lookup"><span data-stu-id="03fa0-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="03fa0-146">Usaban toobe como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-146">Previously it used toobe like as follows -</span></span>
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
<span data-ttu-id="03fa0-147">Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="03fa0-148">Actualización del script de compilación para el proyecto de cliente de prueba de Hola</span><span class="sxs-lookup"><span data-stu-id="03fa0-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="03fa0-149">Cambios relacionados con aquí son similares toohello mencionadas en la sección anterior, es decir, el proyecto de actor Hola.</span><span class="sxs-lookup"><span data-stu-id="03fa0-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="03fa0-150">Hola anteriormente Gradle toobe de script que se utiliza, como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-150">Previously hello Gradle script used toobe like as follows -</span></span>
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
<span data-ttu-id="03fa0-151">Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:</span><span class="sxs-lookup"><span data-stu-id="03fa0-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="03fa0-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03fa0-152">Next steps</span></span>

* [<span data-ttu-id="03fa0-153">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman</span><span class="sxs-lookup"><span data-stu-id="03fa0-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="03fa0-154">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con el complemento de Eclipse para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="03fa0-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="03fa0-155">Interactuar con los clústeres de Service Fabric mediante Hola CLI de tejido de servicio</span><span class="sxs-lookup"><span data-stu-id="03fa0-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
