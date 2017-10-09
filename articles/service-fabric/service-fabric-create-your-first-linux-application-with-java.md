---
title: "una aplicación de Java de Azure Service Fabric actores confiable en Linux aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate e implementar una aplicación de Java Service Fabric actores confiable en cinco minutos."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Creación de su primera aplicación Java de Reliable Actors de Service Fabric en Linux
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Este inicio rápido le ayuda a crear su primera aplicación Java de Azure Service Fabric en un entorno de desarrollo de Linux en tan solo unos minutos.  Cuando haya terminado, tendrá una aplicación de servicio de single Java simple que se ejecuta en clúster de desarrollo local Hola.  

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar a instalar Hola SDK del servicio de Fabric, Hola CLI de tejido de servicio y la instalación de un clúster de desarrollo en su [entorno de desarrollo de Linux](service-fabric-get-started-linux.md). Si usa Mac OS X, puede [configurar un entorno de desarrollo de Linux en una máquina virtual mediante Vagrant](service-fabric-get-started-mac.md).

También deberá hello tooinstall [Service Fabric CLI](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Instalar y configurar los generadores de Hola para Java
Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear una aplicación Java de Service Fabric desde el terminal mediante el generador de plantillas Yeoman. Siga estos pasos hello tooensure que tiene generador de plantilla yeoman Hola Service Fabric para Java trabajar en su equipo.
1. Instalación de nodejs y NPM en la máquina

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar el generador de aplicaciones de servicio Fabric Yeo Java Hola desde NPM

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Crear aplicación hello
Una aplicación de Service Fabric contiene uno o varios servicios, cada uno con un rol específico en la entrega de la funcionalidad de la aplicación hello. Generador de Hola que instaló en la última sección de hello, resulta fácil toocreate su primer servicio y tooadd más adelante.  También puede crear, compilar e implementar aplicaciones Java de Service Fabric mediante un complemento para Eclipse. Consulte [Creación e implementación de la primera aplicación Java mediante Eclipse](service-fabric-get-started-eclipse.md). Para este tutorial, utilice Yeoman toocreate una aplicación con un único servicio que almacena y obtiene un valor de contador.

1. En un terminal, escriba ``yo azuresfjava``.
2. Asigne un nombre a la aplicación.
3. Elegir tipo de Hola de su primer servicio y asígnele el nombre. En este tutorial, elija un servicio de Reliable Actor. Para obtener más información acerca de hello otros tipos de servicios, consulte [Service Fabric información general del modelo de programación](service-fabric-choose-framework.md).
   ![Generador Yeoman de Service Fabric para Java][sf-yeoman]

## <a name="build-hello-application"></a>Compilar la aplicación hello
plantillas de servicio tejido Yeoman Hola incluyen un script de compilación para [Gradle](https://gradle.org/), que puede usar toobuild aplicación Hola Hola terminal.
Las dependencias de Java de Service Fabric se recuperan de Maven. toobuild y trabajo en aplicaciones de Java de tejido de servicio de hello, deberá tooensure que tiene JDK y Gradle instalados. Si aún no se ha instalado, puede ejecutar Hola siguientes tooinstall JDK(openjdk-8-jdk) y Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild y el paquete de aplicación hello, ejecute hello siguiente:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Implementar la aplicación hello
Una vez que se compila la aplicación hello, puede implementarlo toohello local del clúster.

1. Conectar el clúster de Service Fabric local toohello.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Ejecutar script de instalación de hello en hello plantilla toocopy aplicación hello empaquetar almacén de imágenes del clúster toohello, registrar el tipo de aplicación hello y cree una instancia de la aplicación hello.

    ```bash
    ./install.sh
    ```

Implementar aplicación Hola integrada es Hola igual que cualquier otra aplicación de Service Fabric. Consulte la documentación de hello en [administrar una aplicación de Service Fabric con hello CLI de tejido de servicio](service-fabric-application-lifecycle-sfctl.md) para obtener instrucciones detalladas.

Comandos de toothese parámetros pueden encontrarse en los manifiestos de hello generado dentro del paquete de aplicación Hola.

Una vez que se ha implementado la aplicación hello, abra un explorador y vaya a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) en [http://localhost:19080/explorador](http://localhost:19080/Explorer).
A continuación, expanda hello **aplicaciones** nodo y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Inicie el cliente de prueba de Hola y realizar una conmutación por error
Actores no hacen nada por sí solas, que requieren otro toosend de servicio o cliente mensajes de ellos. plantilla de actor Hola incluye un script de prueba simple que puede usar con el servicio de actor hello toointeract.

1. Ejecutar script de Hola con hello inspección utilidad toosee Hola obtenidos del servicio de actor Hola.  script de prueba de Hello llama hello `setCountAsync()` llamadas de método en hello actor tooincrement un contador, hello `getCountAsync()` método en hello actor tooget Hola nuevo valor del contador y muestra ese valor toohello consola.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. En el Explorador de Service Fabric, busque Hola nodo hospedaje Hola réplica principal de servicio de actor Hola. En la captura de pantalla de hello siguiente, es el nodo 3. identificadores de réplica de servicio principal de Hello operaciones lectura y escritura.  Cambios de estado de servicio, a continuación, se replicaron toohello réplicas secundarias, ejecutar en los nodos 0 y 1 en la siguiente captura de pantalla de bienvenida.

    ![Buscar la réplica principal de hello en el Explorador de Service Fabric][sfx-primary]

3. En **nodos**, haga clic en el nodo de Hola que encontró en el paso anterior de hello, a continuación, seleccione **desactivar (reiniciar)** desde el menú de acciones de Hola. Esta acción reinicia nodo Hola ejecute réplica de servicio principal de Hola y fuerza una tooone de conmutación por error de réplicas secundarias Hola ejecuta en otro nodo.  Esa réplica secundaria es tooprimary promocionada, otra réplica secundaria se crea en un nodo diferente y réplica principal de hello inicia las operaciones de lectura/escritura de tootake. Cuando se reinicie el nodo de hello, ver salida de hello de cliente de prueba de hello y observe que ese contador Hola continúa tooincrement a pesar de hello conmutación por error.

## <a name="remove-hello-application"></a>Quitar aplicación hello
Usar script de desinstalación de hello proporcionado en la instancia de la aplicación de hello plantilla toodelete hello, anular el registro del paquete de aplicación Hola y quitar el paquete de aplicación Hola del clúster de hello almacén de imágenes.

```bash
./uninstall.sh
```

En el Explorador de Service Fabric verá que aplicación hello y el tipo de aplicación ya no aparecen en hello **aplicaciones** nodo.

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

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migrar toobe de aplicaciones de Java de tejido de servicio anterior utilizado con Maven
Recientemente se han transferido bibliotecas de Java de tejido de servicio desde el repositorio de tooMaven del SDK de Java del tejido de servicio. Mientras que las aplicaciones nuevas de Hola que genere con Yeoman o Eclipse, generará más reciente de los proyectos actualizados (que serán capaz de toowork con Maven), puede actualizar su tejido de servicio existente sin estado o las aplicaciones de Java de actor, que usaba Hola servicio Tejido SDK de Java de versiones anteriores, las dependencias de Java de tejido de servicio de Hola de toouse de Maven. Siga los pasos de hello mencionados [aquí](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure la aplicación anterior funcione con Maven.

## <a name="next-steps"></a>Pasos siguientes

* [Creación de la primera aplicación Java de Service Fabric en Linux](service-fabric-get-started-eclipse.md)
* [Más información acerca de Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interactuar con los clústeres de Service Fabric mediante Hola CLI de tejido de servicio](service-fabric-cli.md)
* Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)
* [Introducción a la CLI de Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
