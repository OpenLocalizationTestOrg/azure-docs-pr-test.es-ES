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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Actualizar las bibliotecas de Java anteriores de toofetch aplicación de Java Service Fabric desde Maven
Recientemente se han transferido los archivos binarios de Java de tejido de servicio de hello servicio SDK de Java de tejido tooMaven hospedaje. Ahora puede usar **mavencentral** dependencias de Java de tejido de servicio más recientes de toofetch Hola. Este inicio rápido le ayuda a actualizar las aplicaciones de Java existentes, que creó anteriormente toobe se usa con el SDK de Java de tejido de servicio, utilizando a cualquier Yeoman Eclipse, toobe compatible con la compilación de Maven en función de Hola o plantilla.

## <a name="prerequisites"></a>Requisitos previos
1. En primer lugar debe toouninstall Hola existente SDK de Java.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Siguiente de CLI de tejido de servicio más reciente de instalación Hola Hola pasos mencionados [aquí](service-fabric-cli.md).

3. toobuild y trabajo en aplicaciones de Java de tejido de servicio de hello, deberá tooensure que tiene JDK 1.8 y Gradle instalados. Si aún no se ha instalado, puede ejecutar Hola siguientes tooinstall JDK 1.8 (openjdk-8-jdk) y Gradle -

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Scripts de instalación/desinstalación Hola de actualización de la aplicación toouse Hola nueva CLI de tejido de servicio siguiendo los pasos de hello mencionados [aquí](service-fabric-application-lifecycle-sfctl.md). Se puede hacer referencia tooour Introducción [ejemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) como referencia.

>[!TIP]
> Después de desinstalar Hola servicio SDK de Java de tejido, Yeoman no funcionará. Siga los requisitos previos de hello mencionados [aquí](service-fabric-create-your-first-linux-application-with-java.md) toohave Yeoman de tejido de servicio Java generador de plantilla de seguridad y en funcionamiento.

## <a name="service-fabric-java-libraries-on-maven"></a>Bibliotecas de Java de Service Fabric en Maven
Las bibliotecas de Java de Service Fabric han sido hospedadas en Maven. También puede agregar dependencias de Hola Hola ``pom.xml`` o ``build.gradle`` de las bibliotecas de Java de tejido de servicio de proyectos toouse desde **mavenCentral**.

### <a name="actors"></a>Actores

Compatibilidad con Reliable Actor de Service Fabric para la aplicación.

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

### <a name="services"></a>Services

Compatibilidad con el servicio sin estado de Service Fabric para la aplicación.

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

### <a name="others"></a>Otros
#### <a name="transport"></a>Transporte

Compatibilidad de la capa de transporte para aplicaciones Java de Service Fabric. No es necesario tooexplicitly agregar esta dependencia tooyour Actor confiable o aplicaciones de servicio, a menos que se programan en la capa de transporte de Hola.

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

#### <a name="fabric-support"></a>Compatibilidad con Fabric

Compatibilidad de nivel de sistema para Service Fabric, que se comunica en tiempo de ejecución de toonative Service Fabric. No es necesario tooexplicitly agregar esta dependencia tooyour Actor confiable o las aplicaciones de servicio. Esto obtiene capturan automáticamente desde Maven, al incluir Hola otras dependencias anteriores.

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


## <a name="migrating-service-fabric-stateless-service"></a>Migración del servicio sin estado de Service Fabric

toobe toobuild capaz de su Service Fabric sin estado Java servicio existente con dependencias de Service Fabric Maven se captura, necesita hello tooupdate ``build.gradle`` archivo dentro de hello servicio. Usaban toobe como las siguientes:
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
Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:
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
En general, tooget una idea general acerca de cómo crear Hola de script sería similar para un servicio de Service Fabric sin estado Java, puede consultar tooany ejemplo de nuestros ejemplos de iniciación. Aquí es hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) de ejemplo de Hola a EchoServer.

## <a name="migrating-service-fabric-actor-service"></a>Migración del servicio Actor de Service Fabric

toobe toobuild capaz de la aplicación existente de Service Fabric Actor Java con dependencias de Service Fabric Maven se captura, necesita hello tooupdate ``build.gradle`` archivo dentro del paquete de interfaz de Hola y en el paquete del servicio de Hola. Si tiene un paquete TestClient, necesita tooupdate es así. Así, para su actor ``Myactor``, siguiente Hola sería lugares hello en las que necesite tooupdate -
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>Actualización del script de compilación para el proyecto de la interfaz de Hola

Usaban toobe como las siguientes:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:
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

#### <a name="updating-build-script-for-hello-actor-project"></a>Actualización del script de compilación para el proyecto de actor Hola

Usaban toobe como las siguientes:
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
Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:
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

#### <a name="updating-build-script-for-hello-test-client-project"></a>Actualización del script de compilación para el proyecto de cliente de prueba de Hola

Cambios relacionados con aquí son similares toohello mencionadas en la sección anterior, es decir, el proyecto de actor Hola. Hola anteriormente Gradle toobe de script que se utiliza, como las siguientes:
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
Ahora, las dependencias de Hola de toofetch de Maven, Hola **actualizar** ``build.gradle`` tendría los elementos correspondientes de hello las siguientes:
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

## <a name="next-steps"></a>Pasos siguientes

* [Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con el complemento de Eclipse para Service Fabric](service-fabric-get-started-eclipse.md)
* [Interactuar con los clústeres de Service Fabric mediante Hola CLI de tejido de servicio](service-fabric-cli.md)
