---
title: "Configuración del entorno de desarrollo en Mac OS X para trabajar con Azure Service Fabric | Microsoft Docs"
description: "Instale las herramientas, el SDK y el motor en tiempo de ejecución y cree un clúster de desarrollo local. Después de completar esta instalación, estará listo para compilar aplicaciones en Mac OS X."
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
ms.openlocfilehash: 8b4fc0ab9034263418cac42ced203035e0a8fcad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="d5dd0-104">Configuración de su entorno de desarrollo en Mac OS X</span><span class="sxs-lookup"><span data-stu-id="d5dd0-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5dd0-105">Windows</span><span class="sxs-lookup"><span data-stu-id="d5dd0-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="d5dd0-106">Linux</span><span class="sxs-lookup"><span data-stu-id="d5dd0-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="d5dd0-107">OSX</span><span class="sxs-lookup"><span data-stu-id="d5dd0-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="d5dd0-108">Puede compilar aplicaciones de Service Fabric para que ejecuten en clústeres de Linux con Mac OS X. En este artículo se describe cómo configurar su Mac para desarrollo.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-108">You can build Service Fabric applications to run on Linux clusters using Mac OS X. This article covers how to set up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5dd0-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d5dd0-109">Prerequisites</span></span>
<span data-ttu-id="d5dd0-110">Service Fabric no se ejecuta de forma nativa en OS X. Para ejecutar un clúster de Service Fabric local, proporcionamos una máquina virtual de Ubuntu preconfigurada mediante Vagrant y VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-110">Service Fabric does not run natively on OS X. To run a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="d5dd0-111">Antes de comenzar, necesita:</span><span class="sxs-lookup"><span data-stu-id="d5dd0-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="d5dd0-112">Vagrant (v1.8.4 o versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="d5dd0-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="d5dd0-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="d5dd0-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="d5dd0-114">Tiene que utilizar versiones de Vagrant y VirtualBox que sean compatibles entre sí.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-114">You need to use mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="d5dd0-115">Con una versión no compatible de VirtualBox, Vagrant pueden comportarse de forma errática.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-the-local-vm"></a><span data-ttu-id="d5dd0-116">Creación de la máquina virtual local</span><span class="sxs-lookup"><span data-stu-id="d5dd0-116">Create the local VM</span></span>
<span data-ttu-id="d5dd0-117">Para crear la máquina virtual local que contenga un clúster de Service Fabric de 5 nodos, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5dd0-117">To create the local VM containing a 5-node Service Fabric cluster, perform the following steps:</span></span>

1. <span data-ttu-id="d5dd0-118">Clone el repositorio `Vagrantfile`</span><span class="sxs-lookup"><span data-stu-id="d5dd0-118">Clone the `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="d5dd0-119">Este paso reduce el archivo `Vagrantfile` que contiene la configuración de la máquina virtual, junto con la ubicación desde la que se descarga la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-119">This steps bring downs the file `Vagrantfile` containing the VM configuration along with the location the VM is downloaded from.</span></span>

2. <span data-ttu-id="d5dd0-120">Vaya al clon local del repositorio</span><span class="sxs-lookup"><span data-stu-id="d5dd0-120">Navigate to the local clone of the repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="d5dd0-121">(Opcional) Modifique la configuración predeterminada de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d5dd0-121">(Optional) Modify the default VM settings</span></span>

    <span data-ttu-id="d5dd0-122">De forma predeterminada, la máquina virtual local está configurada de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="d5dd0-122">By default, the local VM is configured as follows:</span></span>

   * <span data-ttu-id="d5dd0-123">3 GB de memoria asignada</span><span class="sxs-lookup"><span data-stu-id="d5dd0-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="d5dd0-124">Red host privada configurada en la dirección IP 192.168.50.50, que permite el acceso directo del tráfico desde el host de Mac</span><span class="sxs-lookup"><span data-stu-id="d5dd0-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from the Mac host</span></span>

     <span data-ttu-id="d5dd0-125">Puede cambiar cualquiera de estas opciones o agregar otra configuración a la máquina virtual en `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-125">You can change either of these settings or add other configuration to the VM in the `Vagrantfile`.</span></span> <span data-ttu-id="d5dd0-126">Consulte la [documentación de Vagrant](http://www.vagrantup.com/docs) para obtener una lista completa de las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-126">See the [Vagrant documentation](http://www.vagrantup.com/docs) for the full list of configuration options.</span></span>
4. <span data-ttu-id="d5dd0-127">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d5dd0-127">Create the VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="d5dd0-128">En este paso, se descarga la imagen de máquina virtual preconfigurada, se arranca localmente y, a continuación, se configura un clúster de Service Fabric local en ella.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-128">This step downloads the preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="d5dd0-129">Tenga en cuenta que puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-129">You should expect it to take a few minutes.</span></span> <span data-ttu-id="d5dd0-130">Si la instalación se completa correctamente, verá un mensaje en la salida que indica que el clúster se está iniciando.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-130">If setup completes successfully, you see a message in the output indicating that the cluster is starting up.</span></span>

    ![El programa de instalación del clúster se inicia después de aprovisionar la máquina virtual][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="d5dd0-132">Si la descarga de la máquina virtual tarda mucho tiempo, puede descargarla mediante wget o curl, o si usa un explorador, navegando al vínculo que especifica **config.vm.box_url** en el archivo `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-132">If the VM download is taking a long time, you can download it using wget or curl or through a browser by navigating to the link specified by **config.vm.box_url** in the file `Vagrantfile`.</span></span> <span data-ttu-id="d5dd0-133">Después de descargarlo localmente, edite `Vagrantfile` para que apunte a la ruta de acceso local en la que descargó la imagen.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-133">After downloading it locally, edit `Vagrantfile` to point to the local path where you downloaded the image.</span></span> <span data-ttu-id="d5dd0-134">Por ejemplo si la descargó en /home/users/test/azureservicefabric.tp8.box, establezca **config.vm.box_url** en dicha ruta.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-134">For example if you downloaded the image to /home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** to that path.</span></span>
    >

5. <span data-ttu-id="d5dd0-135">Para comprobar que el clúster se ha instalado correctamente, vaya a Service Fabric Explorer en http://192.168.50.50:19080/Explorer (suponiendo que mantenga la IP de la red privada predeterminada).</span><span class="sxs-lookup"><span data-stu-id="d5dd0-135">Test that the cluster has been set up correctly by navigating to Service Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept the default private network IP).</span></span>

    ![Service Fabric Explorer visto desde el equipo Mac host][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="d5dd0-137">Creación de la aplicación en el equipo Mac usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="d5dd0-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="d5dd0-138">Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear una aplicación de Service Fabric desde el terminal mediante el generador de plantillas Yeoman.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="d5dd0-139">Siga los pasos siguientes para asegurarse de que el generador de plantillas yeoman de Service Fabric está en funcionamiento en la máquina.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-139">Please follow the steps below to ensure you have the Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="d5dd0-140">Debe tener Node.js y NPM instalados en el equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-140">You need to have Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="d5dd0-141">Si no los tiene, puede instalar Node.js y NPM mediante Homebrew utilizando lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-141">If not you can install Node.js and NPM using Homebrew using the following.</span></span> <span data-ttu-id="d5dd0-142">Para comprobar las versiones de Node.js y NPM instaladas en el equipo Mac, puede usar la opción ``-v``.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-142">To check the versions of Node.js and NPM installed on your Mac, you can use the ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="d5dd0-143">Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM</span><span class="sxs-lookup"><span data-stu-id="d5dd0-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="d5dd0-144">Para instalar el generador Yeoman que desea usar, siga los pasos descritos en la [documentación](service-fabric-get-started-linux.md) de introducción.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-144">Install the Yeoman generator you want to use, following the steps in the getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="d5dd0-145">Para crear aplicaciones de Service Fabric mediante Yeoman, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d5dd0-145">To create Service Fabric Applications using Yeoman, follow the steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="d5dd0-146">Para compilar una aplicación de Java de Service Fabric en Mac, necesita JDK 1.8 y Gradle instalados en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-146">To build a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on the machine.</span></span>


## <a name="install-the-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="d5dd0-147">Instalación del complemento de Eclipse Neon para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d5dd0-147">Install the Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="d5dd0-148">Service Fabric proporciona un complemento para **IDE de Java para Eclipse Neon** que puede simplificar el proceso de creación, compilación e implementación de servicios de Java.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-148">Service Fabric provides a plugin for the **Eclipse Neon for Java IDE** that can simplify the process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="d5dd0-149">Puede seguir los pasos de instalación que se indican en esta [documentación](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) general acerca de cómo instalar o actualizar el complemento de Eclipse para Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-149">You can follow the installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="d5dd0-150">De forma predeterminada, se admite la dirección IP predeterminada como se menciona en ``Vagrantfile``, en el archivo ``Local.json`` de la aplicación generada.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-150">By default we support the default IP as mentioned in the ``Vagrantfile`` in the ``Local.json`` of the generated application.</span></span> <span data-ttu-id="d5dd0-151">En caso de cambiar esta configuración e implementar Vagrant con una dirección IP diferente, actualice la dirección IP correspondiente en el archivo ``Local.json`` de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5dd0-151">In case you change that and deploy Vagrant with a different IP, please update the corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5dd0-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5dd0-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="d5dd0-153">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman</span><span class="sxs-lookup"><span data-stu-id="d5dd0-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="d5dd0-154">Creación e implementación de la primera aplicación de Java para Service Fabric con el complemento de Eclipse para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d5dd0-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="d5dd0-155">Configuración de un clúster de Service Fabric en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d5dd0-155">Create a Service Fabric cluster in the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="d5dd0-156">Creación de un clúster de Service Fabric en Azure mediante Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5dd0-156">Create a Service Fabric cluster using the Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="d5dd0-157">Entender el modelo de aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d5dd0-157">Understand the Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
