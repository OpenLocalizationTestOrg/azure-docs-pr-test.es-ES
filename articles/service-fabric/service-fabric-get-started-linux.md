---
title: aaaSet del entorno de desarrollo en Linux | Documentos de Microsoft
description: "Instalar SDK y runtime hello y crear un clúster de desarrollo local en Linux. Después de completar la instalación, estará listo toobuild aplicaciones."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>Preparación del entorno de desarrollo en Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy y ejecute [aplicaciones de Azure Service Fabric](service-fabric-application-model.md) en su equipo de desarrollo de Linux, instalar en tiempo de ejecución de Hola y SDK comunes. También puede instalar SDK opcionales para Java y .NET Core.

## <a name="prerequisites"></a>Requisitos previos

Hola siguientes versiones de sistema operativo es compatibles para el desarrollo:

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>Actualización de los orígenes de APT
tooinstall Hola hello y SDK asociado en tiempo de ejecución paquete a través de la herramienta de línea de comandos de hello apt get, primero debe actualizar los orígenes de la herramienta de empaquetado avanzadas (APT).

1. Abra un terminal.
2. Agregar lista de orígenes de hello Service Fabric repositorio tooyour.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Agregar hello `dotnet` lista de orígenes de tooyour de repositorio.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Agregar hello tooyour APT keyring de clave de la nueva restricción de privacidad de Gnu (GnuPG o GPG).

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Agregar Hola oficial GPG Docker tooyour clave APT keyring.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Configurar el repositorio de Docker de Hola.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. El paquete de actualización listas basadas en hello recién agregan repositorios.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Instalar y configurar hello SDK para el programa de instalación de clúster local

Después de haber actualizado los orígenes, puede instalar Hola SDK. Instalar el paquete de servicio SDK de tejido de hello, confirmar la instalación de Hola y acepta el contrato de licencia de toohello.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Hello siguientes comandos automatizan aceptación licencia de Hola para paquetes de Service Fabric:
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Instalación de un clúster local
  Si se realiza correctamente la instalación de hello, debe ser capaz de toostart un clúster local.

  1. Ejecute el script de instalación de clúster de Hola.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Abra un explorador web y vaya demasiado[Service Fabric Explorer](http://localhost:19080/Explorer). Si Hola clúster se ha iniciado, debería ver el panel del explorador de Service Fabric Hola.

      ![Service Fabric Explorer en Linux][sfx-linux]

  En este punto, puede implementar paquetes de aplicación de Service Fabric precompilados o nuevos basados en contenedores de invitado o archivos ejecutables de invitado. toobuild nuevos servicios mediante Java de Hola o .NET Core SDK, siga los pasos de instalación opcional de Hola que se proporcionan en las secciones siguientes.


  > [!NOTE]
  > No se admiten clústeres independientes en Linux. Hola preview admite sólo en un equipo y clústeres de varios equipos de Linux de Azure.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Configurar Hola CLI de tejido de servicio

Hola [Service Fabric CLI](service-fabric-cli.md) tiene comandos para interactuar con las entidades de Service Fabric, incluidos los clústeres y las aplicaciones. Se basa en python, por lo que debe seguro toohave python y pip instalado antes de continuar con el siguiente comando de hello:

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Instalar y configurar los generadores de Hola para los contenedores y los archivos ejecutables de invitado
Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear aplicaciones de Service Fabric desde el terminal mediante el generador de plantillas Yeoman. Siga estos pasos hello tooensure que tiene generador de plantilla yeoman Hola Service Fabric para trabajar en su equipo.

1. Instalación de nodejs y NPM en la máquina

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM

  ```bash
  sudo npm install -g yo
  ```
3. Instalar el generador de contenedor de servicio Fabric Yeo Hola y el generador de execuatble de invitado de NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Después de haber instalado Hola anteriormente generadores, debe ser capaz de toocreate aplicaciones con servicios de archivo ejecutable o un contenedor de sistemas invitados ejecutando `yo azuresfguest` o `yo azuresfcontainer` respectivamente.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Instalar los artefactos de Java necesarios de hello (opcionales, si desea que toouse Hola Java modelos de programación)

Servicios de Service Fabric toobuild con Java, asegúrese de tener 1.8 de JDK que se instala junto con Gradle que se utiliza para ejecutar tareas de compilación. Hola siguiente fragmento de código instala abierto 1.8 de JDK junto con Gradle. bibliotecas de Java de tejido de servicio de Hola se extraen de Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Instalar Hola Eclipse Neon complemento (opcional)

Puede instalar Hola Eclipse complemento de Service Fabric desde dentro de hello **Eclipse IDE para los desarrolladores de Java**. Puede utilizar aplicaciones ejecutables de Eclipse toocreate Service Fabric invitados y aplicaciones de contenedor suma tooService Fabric en aplicaciones de Java.

1. En Eclipse, asegúrese de que tiene más reciente Neon Eclipse y Hola versión más reciente de Buildship (1.0.17 o posterior) instalado. Puede comprobar las versiones de componentes instalados Hola seleccionando **ayuda** > **detalles de instalación**. Puede actualizar Buildship mediante instrucciones de hello en [Buildship Eclipse: complementos Eclipse para Gradle][buildship-update].

2. tooinstall Hola seleccione complemento, Service Fabric **ayuda** > **instalar nuevo Software**.

3. Hola **trabajar con** , escriba **http://dl.microsoft.com/eclipse**.

4. Haga clic en **Agregar**.

    ![página de Hello Software disponible][sf-eclipse-plugin]

5. Seleccione hello **ServiceFabric** complemento y, a continuación, haga clic en **siguiente**.

6. Complete los pasos de instalación de hello y, a continuación, acepte el contrato de licencia de usuario final de Hola.

Si ya tiene Hola Service Fabric Eclipse complemento instalado, asegúrese de que tiene la versión más reciente de Hola. Puede comprobar mediante la selección **ayuda** > **detalles de la instalación** y, a continuación, buscando Service Fabric en lista de Hola de complementos instalados. Si hay disponible una versión más reciente, seleccione **Update** (Actualizar).

Para más información, consulte [Complemento de Service Fabric para el desarrollo de aplicaciones Java de Eclipse](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Instalar Hola .NET Core SDK (opcional, si desea que los modelos de programación .NET Core toouse Hola)
Hola .NET Core SDK proporciona bibliotecas de Hola y plantillas de servicios de Service Fabric toobuild necesarios con .NET Core. Instalar el paquete de .NET Core SDK de hello siguiendo ejecución hello-

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Actualización hello SDK y en tiempo de ejecución

versión más reciente de tooupdate toohello de hello SDK y en tiempo de ejecución, ejecute hello siga los comandos (anule la selección de SDK de Hola que no desea):

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
tooupdate Hola SDK de Java los archivos binarios de Maven, necesita detalles de la versión tooupdate Hola del archivo binario correspondiente de Hola Hola ``build.gradle`` versión más reciente del archivo toopoint toohello. tooknow exactamente donde necesita tooupdate versión de hello, puede hacer referencia a tooany ``build.gradle`` archivo en los ejemplos de introducción a Service Fabric [aquí](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Actualizar paquetes de saludo podría dar lugar a su toostop de clúster de desarrollo local que ejecuta. Reinicie el clúster local después de una actualización, siga las instrucciones de hello en esta página.

## <a name="next-steps"></a>Pasos siguientes

* [Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con el complemento de Eclipse para Service Fabric](service-fabric-get-started-eclipse.md)
* [Creación de su primera aplicación de CSharp en Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Prepare your development environment on OSX](service-fabric-get-started-mac.md)
* [Usar las aplicaciones de hello CLI de tejido de servicio toomanage](service-fabric-application-lifecycle-sfctl.md)
* [Diferencias entre Service Fabric para Windows y para Linux](service-fabric-linux-windows-differences.md)
* [Introducción a la CLI de Service Fabric](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
