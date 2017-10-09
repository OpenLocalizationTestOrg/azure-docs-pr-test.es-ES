---
title: "aaaCreate su primera aplicación de Azure microservicios en Linux con C# | Documentos de Microsoft"
description: "Creación e implementación de una aplicación de Service Fabric con C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>Creación de la primera aplicación de Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric ofrece SDK para compilar servicios en Linux tanto en .NET Core como Java. En este tutorial, veremos cómo toocreate una aplicación para Linux y generar un servicio usando C# (.NET Core).

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, asegúrese de [configurar el entorno de desarrollo Linux](service-fabric-get-started-linux.md). Si usa Mac OS X, puede [configurar un entorno one-box de Linux en una máquina virtual mediante Vagrant](service-fabric-get-started-mac.md).

También deberá tooinstall hello [CLI de tejido de servicio](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Instale y configure los generadores de Hola de CSharp
Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear una aplicación de CSharp de Service Fabric desde el terminal mediante el generador de plantillas Yeoman. Siga estos pasos hello tooensure que tendrá el generador de plantilla yeoman de Service Fabric Hola para CSharp trabajar en su equipo.
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
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Crear aplicación hello
Una aplicación de Service Fabric puede contener uno o varios servicios, cada uno con un rol específico en la entrega de la funcionalidad de la aplicación hello. Hola Service Fabric [Yeoman](http://yeoman.io/) generador para CSharp, que instala en el último paso, resulta fácil toocreate su primer servicio y tooadd más adelante. Vamos a usar Yeoman toocreate una aplicación con un único servicio.

1. En un terminal, escriba Hola después toostart comando compilar scaffolding hello:`yo azuresfcsharp`
2. Asigne un nombre a la aplicación.
3. Elegir tipo de Hola de su primer servicio y asígnele el nombre. Para fines de Hola de este tutorial, elegimos un servicio de Actor confiable.

   ![Generador Yeoman de Service Fabric para C#][sf-yeoman]

> [!NOTE]
> Para obtener más información acerca de las opciones de hello, consulte [Service Fabric información general del modelo de programación](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Compilar la aplicación hello
las plantillas de servicio tejido Yeoman Hola incluyen un script de compilación que puede usar toobuild aplicación Hola Hola terminal (después de navegar toohello carpeta de la aplicación).

  ```sh
 cd myapp
 ./build.sh
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

Una vez que se ha implementado la aplicación hello, abra un explorador y vaya a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) en [http://localhost:19080/explorador](http://localhost:19080/Explorer). A continuación, expanda hello **aplicaciones** nodo y observe que ahora hay una entrada para el tipo de aplicación y otro para hello primera instancia de ese tipo.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Inicie el cliente de prueba de Hola y realizar una conmutación por error
Los proyectos de actor no hacen nada por sí solos. Requieren otro toosend de servicio o cliente mensajes de ellos. plantilla de actor Hola incluye un script de prueba simple que puede usar con el servicio de actor hello toointeract.

1. Ejecutar script de Hola con hello inspección utilidad toosee Hola obtenidos del servicio de actor Hola.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. En Service Fabric Explorer, busque el nodo que hospeda la réplica principal de hello para el servicio de actor Hola. En la captura de pantalla de hello siguiente, es el nodo 3.

    ![Buscar la réplica principal de hello en el Explorador de Service Fabric][sfx-primary]
3. Haga clic en el nodo de Hola que encontró en el paso anterior de hello, a continuación, seleccione **desactivar (reiniciar)** desde el menú de acciones de Hola. Esta acción reinicia un nodo en el clúster local forzar una réplica secundaria de conmutación por error tooa ejecuta en otro nodo. Al realizar esta acción, paga salida toohello de atención de cliente de prueba de hello y observe que ese contador Hola continúa tooincrement a pesar de hello conmutación por error.

## <a name="adding-more-services-tooan-existing-application"></a>Agregar más servicios tooan existente aplicación

tooadd otra aplicación de tooan de servicio ya creado mediante `yo`, realizar Hola pasos:
1. Cambiar toohello raíz del directorio de aplicación existente de Hola.  Por ejemplo, `cd ~/YeomanSamples/MyApplication`si `MyApplication` es aplicación Hola creado por Yeoman.
2. Ejecute `yo azuresfcsharp:AddService`

## <a name="migrating-from-projectjson-toocsproj"></a>Migrar desde too.csproj project.json
1. Ejecutando 'dotnet migrar' en el directorio raíz del proyecto migrará el formato de todos los hello project.json toocsproj.
2. Actualización Hola referencias del proyecto en consecuencia toocsproj en archivos de proyecto.
3. Actualizar archivos toocsproj nombres de archivo de proyecto de hello en build.sh.

## <a name="next-steps"></a>Pasos siguientes

* [Más información acerca de Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Interactuar con los clústeres de Service Fabric usando Hola CLI de tejido de servicio](service-fabric-cli.md)
* Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)
* [Introducción a la CLI de Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
