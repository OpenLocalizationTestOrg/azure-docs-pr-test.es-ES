---
title: aaaSet del entorno de desarrollo en Mac OS X toowork con Azure Service Fabric | Documentos de Microsoft
description: "Instalar en tiempo de ejecución de hello, SDK y herramientas y crear un clúster de desarrollo local. Después de completar la instalación, estará listo toobuild aplicaciones en Mac OS X."
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
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a>Configuración de su entorno de desarrollo en Mac OS X
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

Puede compilar toorun de aplicaciones de Service Fabric en clústeres de Linux con Mac OS X. Este artículo se trata cómo tooset una el equipo Mac para el desarrollo.

## <a name="prerequisites"></a>Requisitos previos
Service Fabric no ejecuten de forma nativa en OS X. toorun un clúster de Service Fabric local, proporcionamos una máquina de virtual Ubuntu configurada previamente con Vagrant y VirtualBox. Antes de comenzar, necesita:

* [Vagrant (v1.8.4 o versiones posteriores)](http://www.vagrantup.com/downloads.html)
* [VirtualBox](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> Necesita toouse mutuamente admite versiones de Vagrant y VirtualBox. Con una versión no compatible de VirtualBox, Vagrant pueden comportarse de forma errática.
>

## <a name="create-hello-local-vm"></a>Crear Hola VM local
toocreate Hola VM local que contenga un clúster de Service Fabric de 5 nodos, lleve a cabo Hola pasos:

1. Hola clon `Vagrantfile` repositorio

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    Poner este pasos listas desplegables Hola archivo `Vagrantfile` que contiene Hola VM configuración junto con Hola Hola de ubicación VM se descarga desde.

2. Navegue toohello clon local del repositorio de Hola

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. (Opcional) Modificar la configuración de máquina virtual de hello predeterminada

    De forma predeterminada, hello VM local se configura como se indica a continuación:

   * 3 GB de memoria asignada
   * Red privada host configurado en la dirección IP 192.168.50.50 habilitar paso a través del tráfico de host de Mac Hola

     Puede cambiar cualquiera de estos valores o agregar otro toohello configuración VM en hello `Vagrantfile`. Vea hello [documentación Vagrant](http://www.vagrantup.com/docs) para lista completa de Hola de opciones de configuración.
4. Crear hello VM

    ```bash
    vagrant up
    ```

   Este paso descarga la imagen de VM de hello preconfigurado, arranque lo localmente y, a continuación, configure un tejido de servicio local de clúster en ella. Se debería tootake unos minutos. Si el programa de instalación finaliza correctamente, verá un mensaje en la salida de hello que indica que ese clúster Hola se está iniciando.

    ![El programa de instalación del clúster se inicia después de aprovisionar la máquina virtual][cluster-setup-script]

    >[!TIP]
    > Si la descarga de la máquina virtual de hello tarda mucho tiempo, puede descargar mediante wget o curl o a través de un explorador navegando vínculo toohello especificado por **config.vm.box_url** en el archivo hello `Vagrantfile`. Después de descargarlo de forma local, editar `Vagrantfile` toopoint toohello ruta local en la que descargó imagen Hola. Por ejemplo si descargó Hola imagen too/home/users/test/azureservicefabric.tp8.box, a continuación, establezca **config.vm.box_url** toothat ruta de acceso.
    >

5. Probar esa Hola clúster se ha configurado correctamente desplazándose tooService explorador Fabric en http://192.168.50.50:19080/explorador (suponiendo que mantienen IP de red privada de Hola de forma predeterminada).

    ![Explorador de Service Fabric ven de hello dirección Mac del host][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a>Creación de la aplicación en el equipo Mac usando Yeoman
Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear una aplicación de Service Fabric desde el terminal mediante el generador de plantillas Yeoman. Siga estos pasos hello tooensure que tiene generador de plantilla yeoman de Service Fabric Hola trabajar en su equipo.

1. Necesita toohave Node.js y NPM instalado en mac. Si no puede instalar Node.js y NPM mediante Homebrew con hello siguientes. versiones de hello toocheck de Node.js y NPM instalado en el equipo Mac, puede usar hello ``-v`` opción.

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM

  ```bash
  npm install -g yo
  ```
3. Instalar hello Yeoman generador desea toouse, siga los pasos de Hola Hola Introducción [documentación](service-fabric-get-started-linux.md). Aplicaciones de tejido de servicio toocreate mediante Yeoman, siga pasos hello:

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. toobuild una aplicación Java de tejido de servicio en Mac, necesitaría - JDK 1.8 y Gradle instalados en el equipo de Hola.


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a>Instalar el complemento de Service Fabric Hola para Eclipse Neon

Service Fabric proporciona un complemento para hello **Neon Eclipse IDE Java** que pueden simplificar el proceso de Hola de crear, compilar e implementar servicios de Java. Puede seguir los pasos de instalación de hello mencionados en esta general [documentación](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) acerca de cómo instalar o actualizar el complemento de Eclipse de tejido de servicio.

>[!TIP]
> De forma predeterminada admitimos hello IP de forma predeterminada como se mencionó en hello ``Vagrantfile`` en hello ``Local.json`` de aplicación hello generado. En caso de cambiar esta configuración e implementar Vagrant con una dirección IP diferente, actualice Hola IP correspondiente en ``Local.json`` de la aplicación.

## <a name="next-steps"></a>Pasos siguientes
<!-- Links -->
* [Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Creación e implementación de la primera aplicación de Java para Service Fabric con el complemento de Eclipse para Service Fabric](service-fabric-get-started-eclipse.md)
* [Crear un clúster de Service Fabric en hello portal de Azure](service-fabric-cluster-creation-via-portal.md)
* [Crear un clúster de Service Fabric mediante hello Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
* [Entender el modelo de aplicaciones de Service Fabric Hola](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
