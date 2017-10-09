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
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="b4469-104">Configuración de su entorno de desarrollo en Mac OS X</span><span class="sxs-lookup"><span data-stu-id="b4469-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4469-105">Windows</span><span class="sxs-lookup"><span data-stu-id="b4469-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="b4469-106">Linux</span><span class="sxs-lookup"><span data-stu-id="b4469-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="b4469-107">OSX</span><span class="sxs-lookup"><span data-stu-id="b4469-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="b4469-108">Puede compilar toorun de aplicaciones de Service Fabric en clústeres de Linux con Mac OS X. Este artículo se trata cómo tooset una el equipo Mac para el desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b4469-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4469-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b4469-109">Prerequisites</span></span>
<span data-ttu-id="b4469-110">Service Fabric no ejecuten de forma nativa en OS X. toorun un clúster de Service Fabric local, proporcionamos una máquina de virtual Ubuntu configurada previamente con Vagrant y VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="b4469-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="b4469-111">Antes de comenzar, necesita:</span><span class="sxs-lookup"><span data-stu-id="b4469-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="b4469-112">Vagrant (v1.8.4 o versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="b4469-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="b4469-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="b4469-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="b4469-114">Necesita toouse mutuamente admite versiones de Vagrant y VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="b4469-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="b4469-115">Con una versión no compatible de VirtualBox, Vagrant pueden comportarse de forma errática.</span><span class="sxs-lookup"><span data-stu-id="b4469-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="b4469-116">Crear Hola VM local</span><span class="sxs-lookup"><span data-stu-id="b4469-116">Create hello local VM</span></span>
<span data-ttu-id="b4469-117">toocreate Hola VM local que contenga un clúster de Service Fabric de 5 nodos, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b4469-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="b4469-118">Hola clon `Vagrantfile` repositorio</span><span class="sxs-lookup"><span data-stu-id="b4469-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="b4469-119">Poner este pasos listas desplegables Hola archivo `Vagrantfile` que contiene Hola VM configuración junto con Hola Hola de ubicación VM se descarga desde.</span><span class="sxs-lookup"><span data-stu-id="b4469-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="b4469-120">Navegue toohello clon local del repositorio de Hola</span><span class="sxs-lookup"><span data-stu-id="b4469-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="b4469-121">(Opcional) Modificar la configuración de máquina virtual de hello predeterminada</span><span class="sxs-lookup"><span data-stu-id="b4469-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="b4469-122">De forma predeterminada, hello VM local se configura como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b4469-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="b4469-123">3 GB de memoria asignada</span><span class="sxs-lookup"><span data-stu-id="b4469-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="b4469-124">Red privada host configurado en la dirección IP 192.168.50.50 habilitar paso a través del tráfico de host de Mac Hola</span><span class="sxs-lookup"><span data-stu-id="b4469-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="b4469-125">Puede cambiar cualquiera de estos valores o agregar otro toohello configuración VM en hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="b4469-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="b4469-126">Vea hello [documentación Vagrant](http://www.vagrantup.com/docs) para lista completa de Hola de opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="b4469-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="b4469-127">Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="b4469-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="b4469-128">Este paso descarga la imagen de VM de hello preconfigurado, arranque lo localmente y, a continuación, configure un tejido de servicio local de clúster en ella.</span><span class="sxs-lookup"><span data-stu-id="b4469-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="b4469-129">Se debería tootake unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b4469-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="b4469-130">Si el programa de instalación finaliza correctamente, verá un mensaje en la salida de hello que indica que ese clúster Hola se está iniciando.</span><span class="sxs-lookup"><span data-stu-id="b4469-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![El programa de instalación del clúster se inicia después de aprovisionar la máquina virtual][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="b4469-132">Si la descarga de la máquina virtual de hello tarda mucho tiempo, puede descargar mediante wget o curl o a través de un explorador navegando vínculo toohello especificado por **config.vm.box_url** en el archivo hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="b4469-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="b4469-133">Después de descargarlo de forma local, editar `Vagrantfile` toopoint toohello ruta local en la que descargó imagen Hola.</span><span class="sxs-lookup"><span data-stu-id="b4469-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="b4469-134">Por ejemplo si descargó Hola imagen too/home/users/test/azureservicefabric.tp8.box, a continuación, establezca **config.vm.box_url** toothat ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="b4469-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="b4469-135">Probar esa Hola clúster se ha configurado correctamente desplazándose tooService explorador Fabric en http://192.168.50.50:19080/explorador (suponiendo que mantienen IP de red privada de Hola de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="b4469-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Explorador de Service Fabric ven de hello dirección Mac del host][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="b4469-137">Creación de la aplicación en el equipo Mac usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="b4469-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="b4469-138">Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear una aplicación de Service Fabric desde el terminal mediante el generador de plantillas Yeoman.</span><span class="sxs-lookup"><span data-stu-id="b4469-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="b4469-139">Siga estos pasos hello tooensure que tiene generador de plantilla yeoman de Service Fabric Hola trabajar en su equipo.</span><span class="sxs-lookup"><span data-stu-id="b4469-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="b4469-140">Necesita toohave Node.js y NPM instalado en mac.</span><span class="sxs-lookup"><span data-stu-id="b4469-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="b4469-141">Si no puede instalar Node.js y NPM mediante Homebrew con hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="b4469-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="b4469-142">versiones de hello toocheck de Node.js y NPM instalado en el equipo Mac, puede usar hello ``-v`` opción.</span><span class="sxs-lookup"><span data-stu-id="b4469-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="b4469-143">Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM</span><span class="sxs-lookup"><span data-stu-id="b4469-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="b4469-144">Instalar hello Yeoman generador desea toouse, siga los pasos de Hola Hola Introducción [documentación](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b4469-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="b4469-145">Aplicaciones de tejido de servicio toocreate mediante Yeoman, siga pasos hello:</span><span class="sxs-lookup"><span data-stu-id="b4469-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="b4469-146">toobuild una aplicación Java de tejido de servicio en Mac, necesitaría - JDK 1.8 y Gradle instalados en el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4469-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="b4469-147">Instalar el complemento de Service Fabric Hola para Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="b4469-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="b4469-148">Service Fabric proporciona un complemento para hello **Neon Eclipse IDE Java** que pueden simplificar el proceso de Hola de crear, compilar e implementar servicios de Java.</span><span class="sxs-lookup"><span data-stu-id="b4469-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="b4469-149">Puede seguir los pasos de instalación de hello mencionados en esta general [documentación](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) acerca de cómo instalar o actualizar el complemento de Eclipse de tejido de servicio.</span><span class="sxs-lookup"><span data-stu-id="b4469-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="b4469-150">De forma predeterminada admitimos hello IP de forma predeterminada como se mencionó en hello ``Vagrantfile`` en hello ``Local.json`` de aplicación hello generado.</span><span class="sxs-lookup"><span data-stu-id="b4469-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="b4469-151">En caso de cambiar esta configuración e implementar Vagrant con una dirección IP diferente, actualice Hola IP correspondiente en ``Local.json`` de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4469-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4469-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4469-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="b4469-153">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman</span><span class="sxs-lookup"><span data-stu-id="b4469-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="b4469-154">Creación e implementación de la primera aplicación de Java para Service Fabric con el complemento de Eclipse para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b4469-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="b4469-155">Crear un clúster de Service Fabric en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b4469-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="b4469-156">Crear un clúster de Service Fabric mediante hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b4469-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="b4469-157">Entender el modelo de aplicaciones de Service Fabric Hola</span><span class="sxs-lookup"><span data-stu-id="b4469-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
