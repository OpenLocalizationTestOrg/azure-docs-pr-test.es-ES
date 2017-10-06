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
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="4f949-104">Preparación del entorno de desarrollo en Linux</span><span class="sxs-lookup"><span data-stu-id="4f949-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f949-105">Windows</span><span class="sxs-lookup"><span data-stu-id="4f949-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="4f949-106">Linux</span><span class="sxs-lookup"><span data-stu-id="4f949-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="4f949-107">OSX</span><span class="sxs-lookup"><span data-stu-id="4f949-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="4f949-108">toodeploy y ejecute [aplicaciones de Azure Service Fabric](service-fabric-application-model.md) en su equipo de desarrollo de Linux, instalar en tiempo de ejecución de Hola y SDK comunes.</span><span class="sxs-lookup"><span data-stu-id="4f949-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="4f949-109">También puede instalar SDK opcionales para Java y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4f949-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f949-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4f949-110">Prerequisites</span></span>

<span data-ttu-id="4f949-111">Hola siguientes versiones de sistema operativo es compatibles para el desarrollo:</span><span class="sxs-lookup"><span data-stu-id="4f949-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="4f949-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="4f949-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="4f949-113">Actualización de los orígenes de APT</span><span class="sxs-lookup"><span data-stu-id="4f949-113">Update your APT sources</span></span>
<span data-ttu-id="4f949-114">tooinstall Hola hello y SDK asociado en tiempo de ejecución paquete a través de la herramienta de línea de comandos de hello apt get, primero debe actualizar los orígenes de la herramienta de empaquetado avanzadas (APT).</span><span class="sxs-lookup"><span data-stu-id="4f949-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="4f949-115">Abra un terminal.</span><span class="sxs-lookup"><span data-stu-id="4f949-115">Open a terminal.</span></span>
2. <span data-ttu-id="4f949-116">Agregar lista de orígenes de hello Service Fabric repositorio tooyour.</span><span class="sxs-lookup"><span data-stu-id="4f949-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="4f949-117">Agregar hello `dotnet` lista de orígenes de tooyour de repositorio.</span><span class="sxs-lookup"><span data-stu-id="4f949-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="4f949-118">Agregar hello tooyour APT keyring de clave de la nueva restricción de privacidad de Gnu (GnuPG o GPG).</span><span class="sxs-lookup"><span data-stu-id="4f949-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="4f949-119">Agregar Hola oficial GPG Docker tooyour clave APT keyring.</span><span class="sxs-lookup"><span data-stu-id="4f949-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="4f949-120">Configurar el repositorio de Docker de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f949-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="4f949-121">El paquete de actualización listas basadas en hello recién agregan repositorios.</span><span class="sxs-lookup"><span data-stu-id="4f949-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="4f949-122">Instalar y configurar hello SDK para el programa de instalación de clúster local</span><span class="sxs-lookup"><span data-stu-id="4f949-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="4f949-123">Después de haber actualizado los orígenes, puede instalar Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="4f949-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="4f949-124">Instalar el paquete de servicio SDK de tejido de hello, confirmar la instalación de Hola y acepta el contrato de licencia de toohello.</span><span class="sxs-lookup"><span data-stu-id="4f949-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="4f949-125">Hello siguientes comandos automatizan aceptación licencia de Hola para paquetes de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="4f949-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="4f949-126">Instalación de un clúster local</span><span class="sxs-lookup"><span data-stu-id="4f949-126">Set up a local cluster</span></span>
  <span data-ttu-id="4f949-127">Si se realiza correctamente la instalación de hello, debe ser capaz de toostart un clúster local.</span><span class="sxs-lookup"><span data-stu-id="4f949-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="4f949-128">Ejecute el script de instalación de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f949-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="4f949-129">Abra un explorador web y vaya demasiado[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="4f949-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="4f949-130">Si Hola clúster se ha iniciado, debería ver el panel del explorador de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="4f949-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer en Linux][sfx-linux]

  <span data-ttu-id="4f949-132">En este punto, puede implementar paquetes de aplicación de Service Fabric precompilados o nuevos basados en contenedores de invitado o archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="4f949-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="4f949-133">toobuild nuevos servicios mediante Java de Hola o .NET Core SDK, siga los pasos de instalación opcional de Hola que se proporcionan en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="4f949-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="4f949-134">No se admiten clústeres independientes en Linux.</span><span class="sxs-lookup"><span data-stu-id="4f949-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="4f949-135">Hola preview admite sólo en un equipo y clústeres de varios equipos de Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f949-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="4f949-136">Configurar Hola CLI de tejido de servicio</span><span class="sxs-lookup"><span data-stu-id="4f949-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="4f949-137">Hola [Service Fabric CLI](service-fabric-cli.md) tiene comandos para interactuar con las entidades de Service Fabric, incluidos los clústeres y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4f949-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="4f949-138">Se basa en python, por lo que debe seguro toohave python y pip instalado antes de continuar con el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="4f949-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="4f949-139">Instalar y configurar los generadores de Hola para los contenedores y los archivos ejecutables de invitado</span><span class="sxs-lookup"><span data-stu-id="4f949-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="4f949-140">Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear aplicaciones de Service Fabric desde el terminal mediante el generador de plantillas Yeoman.</span><span class="sxs-lookup"><span data-stu-id="4f949-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="4f949-141">Siga estos pasos hello tooensure que tiene generador de plantilla yeoman Hola Service Fabric para trabajar en su equipo.</span><span class="sxs-lookup"><span data-stu-id="4f949-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="4f949-142">Instalación de nodejs y NPM en la máquina</span><span class="sxs-lookup"><span data-stu-id="4f949-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="4f949-143">Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM</span><span class="sxs-lookup"><span data-stu-id="4f949-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="4f949-144">Instalar el generador de contenedor de servicio Fabric Yeo Hola y el generador de execuatble de invitado de NPM</span><span class="sxs-lookup"><span data-stu-id="4f949-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="4f949-145">Después de haber instalado Hola anteriormente generadores, debe ser capaz de toocreate aplicaciones con servicios de archivo ejecutable o un contenedor de sistemas invitados ejecutando `yo azuresfguest` o `yo azuresfcontainer` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="4f949-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="4f949-146">Instalar los artefactos de Java necesarios de hello (opcionales, si desea que toouse Hola Java modelos de programación)</span><span class="sxs-lookup"><span data-stu-id="4f949-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="4f949-147">Servicios de Service Fabric toobuild con Java, asegúrese de tener 1.8 de JDK que se instala junto con Gradle que se utiliza para ejecutar tareas de compilación.</span><span class="sxs-lookup"><span data-stu-id="4f949-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="4f949-148">Hola siguiente fragmento de código instala abierto 1.8 de JDK junto con Gradle.</span><span class="sxs-lookup"><span data-stu-id="4f949-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="4f949-149">bibliotecas de Java de tejido de servicio de Hola se extraen de Maven.</span><span class="sxs-lookup"><span data-stu-id="4f949-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="4f949-150">Instalar Hola Eclipse Neon complemento (opcional)</span><span class="sxs-lookup"><span data-stu-id="4f949-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="4f949-151">Puede instalar Hola Eclipse complemento de Service Fabric desde dentro de hello **Eclipse IDE para los desarrolladores de Java**.</span><span class="sxs-lookup"><span data-stu-id="4f949-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="4f949-152">Puede utilizar aplicaciones ejecutables de Eclipse toocreate Service Fabric invitados y aplicaciones de contenedor suma tooService Fabric en aplicaciones de Java.</span><span class="sxs-lookup"><span data-stu-id="4f949-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="4f949-153">En Eclipse, asegúrese de que tiene más reciente Neon Eclipse y Hola versión más reciente de Buildship (1.0.17 o posterior) instalado.</span><span class="sxs-lookup"><span data-stu-id="4f949-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="4f949-154">Puede comprobar las versiones de componentes instalados Hola seleccionando **ayuda** > **detalles de instalación**.</span><span class="sxs-lookup"><span data-stu-id="4f949-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="4f949-155">Puede actualizar Buildship mediante instrucciones de hello en [Buildship Eclipse: complementos Eclipse para Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="4f949-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="4f949-156">tooinstall Hola seleccione complemento, Service Fabric **ayuda** > **instalar nuevo Software**.</span><span class="sxs-lookup"><span data-stu-id="4f949-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="4f949-157">Hola **trabajar con** , escriba **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="4f949-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="4f949-158">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4f949-158">Click **Add**.</span></span>

    ![página de Hello Software disponible][sf-eclipse-plugin]

5. <span data-ttu-id="4f949-160">Seleccione hello **ServiceFabric** complemento y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4f949-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="4f949-161">Complete los pasos de instalación de hello y, a continuación, acepte el contrato de licencia de usuario final de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f949-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="4f949-162">Si ya tiene Hola Service Fabric Eclipse complemento instalado, asegúrese de que tiene la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f949-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="4f949-163">Puede comprobar mediante la selección **ayuda** > **detalles de la instalación** y, a continuación, buscando Service Fabric en lista de Hola de complementos instalados. Si hay disponible una versión más reciente, seleccione **Update** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="4f949-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="4f949-164">Para más información, consulte [Complemento de Service Fabric para el desarrollo de aplicaciones Java de Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="4f949-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="4f949-165">Instalar Hola .NET Core SDK (opcional, si desea que los modelos de programación .NET Core toouse Hola)</span><span class="sxs-lookup"><span data-stu-id="4f949-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="4f949-166">Hola .NET Core SDK proporciona bibliotecas de Hola y plantillas de servicios de Service Fabric toobuild necesarios con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4f949-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="4f949-167">Instalar el paquete de .NET Core SDK de hello siguiendo ejecución hello-</span><span class="sxs-lookup"><span data-stu-id="4f949-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="4f949-168">Actualización hello SDK y en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="4f949-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="4f949-169">versión más reciente de tooupdate toohello de hello SDK y en tiempo de ejecución, ejecute hello siga los comandos (anule la selección de SDK de Hola que no desea):</span><span class="sxs-lookup"><span data-stu-id="4f949-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="4f949-170">tooupdate Hola SDK de Java los archivos binarios de Maven, necesita detalles de la versión tooupdate Hola del archivo binario correspondiente de Hola Hola ``build.gradle`` versión más reciente del archivo toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="4f949-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="4f949-171">tooknow exactamente donde necesita tooupdate versión de hello, puede hacer referencia a tooany ``build.gradle`` archivo en los ejemplos de introducción a Service Fabric [aquí](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4f949-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="4f949-172">Actualizar paquetes de saludo podría dar lugar a su toostop de clúster de desarrollo local que ejecuta.</span><span class="sxs-lookup"><span data-stu-id="4f949-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="4f949-173">Reinicie el clúster local después de una actualización, siga las instrucciones de hello en esta página.</span><span class="sxs-lookup"><span data-stu-id="4f949-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f949-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4f949-174">Next steps</span></span>

* [<span data-ttu-id="4f949-175">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman</span><span class="sxs-lookup"><span data-stu-id="4f949-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="4f949-176">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con el complemento de Eclipse para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4f949-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="4f949-177">Creación de su primera aplicación de CSharp en Linux</span><span class="sxs-lookup"><span data-stu-id="4f949-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="4f949-178">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="4f949-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="4f949-179">Usar las aplicaciones de hello CLI de tejido de servicio toomanage</span><span class="sxs-lookup"><span data-stu-id="4f949-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="4f949-180">Diferencias entre Service Fabric para Windows y para Linux</span><span class="sxs-lookup"><span data-stu-id="4f949-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="4f949-181">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4f949-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
