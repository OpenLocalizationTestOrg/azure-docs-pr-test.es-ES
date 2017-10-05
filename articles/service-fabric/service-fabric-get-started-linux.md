---
title: "Configuración del entorno de desarrollo en Linux | Microsoft Docs"
description: "Instale el SDK y el motor en tiempo de ejecución, y cree un clúster de desarrollo local en Linux. Después de completar esta instalación, estará listo para crear aplicaciones."
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
ms.openlocfilehash: 58c6bbbb16d7008e6b573cf8dbc8cf62da9789f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="370ae-104">Preparación del entorno de desarrollo en Linux</span><span class="sxs-lookup"><span data-stu-id="370ae-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="370ae-105">Windows</span><span class="sxs-lookup"><span data-stu-id="370ae-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="370ae-106">Linux</span><span class="sxs-lookup"><span data-stu-id="370ae-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="370ae-107">OSX</span><span class="sxs-lookup"><span data-stu-id="370ae-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="370ae-108">Para implementar y ejecutar [aplicaciones de Azure Service Fabric](service-fabric-application-model.md) en la máquina de desarrollo de Linux, instale el motor de tiempo de ejecución y el SDK común.</span><span class="sxs-lookup"><span data-stu-id="370ae-108">To deploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install the runtime and common SDK.</span></span> <span data-ttu-id="370ae-109">También puede instalar SDK opcionales para Java y .NET Core.</span><span class="sxs-lookup"><span data-stu-id="370ae-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="370ae-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="370ae-110">Prerequisites</span></span>

<span data-ttu-id="370ae-111">Se admiten las siguientes versiones de sistemas operativos para desarrollo:</span><span class="sxs-lookup"><span data-stu-id="370ae-111">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="370ae-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="370ae-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="370ae-113">Actualización de los orígenes de APT</span><span class="sxs-lookup"><span data-stu-id="370ae-113">Update your APT sources</span></span>
<span data-ttu-id="370ae-114">Para instalar el SDK y el paquete en tiempo de ejecución asociado mediante la herramienta de línea de comandos apt-get, primero debe actualizar los orígenes de Advanced Packaging Tool (APT).</span><span class="sxs-lookup"><span data-stu-id="370ae-114">To install the SDK and the associated runtime package via the apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="370ae-115">Abra un terminal.</span><span class="sxs-lookup"><span data-stu-id="370ae-115">Open a terminal.</span></span>
2. <span data-ttu-id="370ae-116">Agregue el repositorio de Service Fabric a su lista de orígenes.</span><span class="sxs-lookup"><span data-stu-id="370ae-116">Add the Service Fabric repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="370ae-117">Agregue el repositorio `dotnet` a su lista de orígenes.</span><span class="sxs-lookup"><span data-stu-id="370ae-117">Add the `dotnet` repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="370ae-118">Agregue la clave de la protección de privacidad de Gnu (GnuPG o GPG) al conjunto de claves APT.</span><span class="sxs-lookup"><span data-stu-id="370ae-118">Add the new Gnu Privacy Guard (GnuPG, or GPG) key to your APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="370ae-119">Agregue la clave GPG oficial de Docker a su conjunto de claves APT.</span><span class="sxs-lookup"><span data-stu-id="370ae-119">Add the official Docker GPG key to your APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="370ae-120">Configure el repositorio de Docker.</span><span class="sxs-lookup"><span data-stu-id="370ae-120">Set up the Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="370ae-121">Actualice las listas de paquetes según los repositorios recién agregados.</span><span class="sxs-lookup"><span data-stu-id="370ae-121">Refresh your package lists based on the newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-the-sdk-for-local-cluster-setup"></a><span data-ttu-id="370ae-122">Instalación y configuración del SDK para la configuración del clúster local</span><span class="sxs-lookup"><span data-stu-id="370ae-122">Install and set up the SDK for local cluster setup</span></span>

<span data-ttu-id="370ae-123">Una vez actualizados los orígenes, puede instalar el SDK.</span><span class="sxs-lookup"><span data-stu-id="370ae-123">After you have updated your sources, you can install the SDK.</span></span> <span data-ttu-id="370ae-124">Instale el paquete del SDK de Service Fabric, confirme la instalación y acepte el contrato de licencia.</span><span class="sxs-lookup"><span data-stu-id="370ae-124">Install the Service Fabric SDK package, confirm the installation, and agree to the license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="370ae-125">Los siguientes comandos aceptan automáticamente la licencia para los paquetes de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="370ae-125">The following commands automate accepting the license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="370ae-126">Instalación de un clúster local</span><span class="sxs-lookup"><span data-stu-id="370ae-126">Set up a local cluster</span></span>
  <span data-ttu-id="370ae-127">Si todo se instaló correctamente, debe poder iniciar un clúster local.</span><span class="sxs-lookup"><span data-stu-id="370ae-127">If the installation is successful, you should be able to start a local cluster.</span></span>

  1. <span data-ttu-id="370ae-128">Ejecute el script de instalación del clúster.</span><span class="sxs-lookup"><span data-stu-id="370ae-128">Run the cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="370ae-129">Abra un explorador web y vaya a [Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="370ae-129">Open a web browser and go to [Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="370ae-130">Si el clúster se ha iniciado, debería ver el panel Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="370ae-130">If the cluster has started, you should see the Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer en Linux][sfx-linux]

  <span data-ttu-id="370ae-132">En este punto, puede implementar paquetes de aplicación de Service Fabric precompilados o nuevos basados en contenedores de invitado o archivos ejecutables de invitado.</span><span class="sxs-lookup"><span data-stu-id="370ae-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="370ae-133">Para compilar nuevos servicios con los SDK de .NET Core o de Java, siga los pasos de configuración opcionales proporcionados en las siguientes secciones.</span><span class="sxs-lookup"><span data-stu-id="370ae-133">To build new services by using the Java or .NET Core SDKs, follow the optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="370ae-134">No se admiten clústeres independientes en Linux.</span><span class="sxs-lookup"><span data-stu-id="370ae-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="370ae-135">La versión preliminar admite únicamente un equipo y clústeres de múltiples máquinas Linux de Azure.</span><span class="sxs-lookup"><span data-stu-id="370ae-135">The preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-the-service-fabric-cli"></a><span data-ttu-id="370ae-136">Configuración de la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="370ae-136">Set up the Service Fabric CLI</span></span>

<span data-ttu-id="370ae-137">La [CLI de Service Fabric](service-fabric-cli.md) tiene comandos para interactuar con las entidades de Service Fabric, incluidos los clústeres y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="370ae-137">The [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="370ae-138">Se basa en python, por tanto, asegúrese de tener python y pip instalados antes de continuar con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="370ae-138">It is based on python, so be sure to have python and pip installed before you proceed with the following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-the-generators-for-containers-and-guest-executables"></a><span data-ttu-id="370ae-139">Instalación y configuración de los generadores para los contenedores y los ejecutables invitados</span><span class="sxs-lookup"><span data-stu-id="370ae-139">Install and set up the generators for containers and guest-executables</span></span>
<span data-ttu-id="370ae-140">Service Fabric proporciona herramientas de scaffolding que le ayudarán a crear aplicaciones de Service Fabric desde el terminal mediante el generador de plantillas Yeoman.</span><span class="sxs-lookup"><span data-stu-id="370ae-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="370ae-141">Siga los pasos siguientes para asegurarse de que el generador de plantillas yeoman de Service Fabric está en funcionamiento en la máquina.</span><span class="sxs-lookup"><span data-stu-id="370ae-141">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="370ae-142">Instalación de nodejs y NPM en la máquina</span><span class="sxs-lookup"><span data-stu-id="370ae-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="370ae-143">Instalación del generador de plantillas [Yeoman](http://yeoman.io/) en la máquina desde NPM</span><span class="sxs-lookup"><span data-stu-id="370ae-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="370ae-144">Instalación del generador de contenedores Yeo de Service Fabric y el generador de ejecutables invitados desde NPM</span><span class="sxs-lookup"><span data-stu-id="370ae-144">Install the Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="370ae-145">Una vez instalados los generadores anteriores, puede crear aplicaciones con ejecutables invitados o servicios de contenedor mediante la ejecución de `yo azuresfguest` o `yo azuresfcontainer` respectivamente.</span><span class="sxs-lookup"><span data-stu-id="370ae-145">After you have installed the above generators, you should be able to create apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-the-necessary-java-artifacts-optional-if-you-want-to-use-the-java-programming-models"></a><span data-ttu-id="370ae-146">Instalación de los artefactos de Java necesarios (opcional, si desea usar los modelos de programación de Java)</span><span class="sxs-lookup"><span data-stu-id="370ae-146">Install the necessary Java artifacts (optional, if you want to use the Java programming models)</span></span>

<span data-ttu-id="370ae-147">Para compilar servicios de Service Fabric con Java, asegúrese de que tiene instalado JDK 1.8 junto con Gradle, que se utiliza para ejecutar tareas de compilación.</span><span class="sxs-lookup"><span data-stu-id="370ae-147">To build Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="370ae-148">El fragmento de código siguiente instala Open JDK 1.8 junto con Gradle.</span><span class="sxs-lookup"><span data-stu-id="370ae-148">The following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="370ae-149">Las bibliotecas de Java de Service Fabric se extraen de Maven.</span><span class="sxs-lookup"><span data-stu-id="370ae-149">The Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-the-eclipse-neon-plug-in-optional"></a><span data-ttu-id="370ae-150">Instalación del complemento Eclipse Neon (opcional)</span><span class="sxs-lookup"><span data-stu-id="370ae-150">Install the Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="370ae-151">Puede instalar el complemento de Eclipse para Service Fabric desde el **IDE de Eclipse para desarrolladores de Java**.</span><span class="sxs-lookup"><span data-stu-id="370ae-151">You can install the Eclipse plug-in for Service Fabric from within the **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="370ae-152">Eclipse se puede usar para crear aplicaciones ejecutables y contenedoras de invitado de Service Fabric, además de aplicaciones Java de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="370ae-152">You can use Eclipse to create Service Fabric guest executable applications and container applications in addition to Service Fabric Java applications.</span></span>

1. <span data-ttu-id="370ae-153">En Eclipse, asegúrese de tener instaladas las versiones más recientes de Eclipse Neon y Buildship (1.0.17 o versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="370ae-153">In Eclipse, ensure that you have latest Eclipse Neon and the latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="370ae-154">Puede comprobar las versiones de los componentes instalados seleccionando **Help** > **Installation Details** (Ayuda > Detalles de la instalación).</span><span class="sxs-lookup"><span data-stu-id="370ae-154">You can check the versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="370ae-155">Puede actualizar Buildship siguiendo las instrucciones de [Eclipse Buildship: Complementos de Eclipse para Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="370ae-155">You can update Buildship by using the instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="370ae-156">Para instalar el complemento de Service Fabric, seleccione **Help** > **Install New Software** (Ayuda > Instalar nuevo software).</span><span class="sxs-lookup"><span data-stu-id="370ae-156">To install the Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="370ae-157">En el cuadro de texto **Trabajar con**, escriba **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="370ae-157">In the **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="370ae-158">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="370ae-158">Click **Add**.</span></span>

    ![Página de Software disponible][sf-eclipse-plugin]

5. <span data-ttu-id="370ae-160">Seleccione el complemento **ServiceFabric** y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="370ae-160">Select the **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="370ae-161">Complete los pasos de instalación y, a continuación, acepte el contrato de licencia de usuario final.</span><span class="sxs-lookup"><span data-stu-id="370ae-161">Complete the installation steps, and then accept the end-user license agreement.</span></span>

<span data-ttu-id="370ae-162">Si el complemento de Eclipse para Service Fabric ya está instalado, asegúrese de que tiene la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="370ae-162">If you already have the Service Fabric Eclipse plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="370ae-163">Puede comprobarlo seleccionando **Help** > **Installation Details** (Ayuda > Detalles de instalación) y buscando Service Fabric en la lista de complementos instalados. Si hay disponible una versión más reciente, seleccione **Update** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="370ae-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in the list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="370ae-164">Para más información, consulte [Complemento de Service Fabric para el desarrollo de aplicaciones Java de Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="370ae-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-the-net-core-sdk-optional-if-you-want-to-use-the-net-core-programming-models"></a><span data-ttu-id="370ae-165">Instalación del SDK de .NET Core (opcional, si desea usar los modelos de programación de .NET Core)</span><span class="sxs-lookup"><span data-stu-id="370ae-165">Install the .NET Core SDK (optional, if you want to use the .NET Core programming models)</span></span>
<span data-ttu-id="370ae-166">El SDK de .NET Core proporciona las bibliotecas y plantillas necesarias para compilar servicios de Service Fabric con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="370ae-166">The .NET Core SDK provides the libraries and templates that are required to build Service Fabric services with .NET Core.</span></span> <span data-ttu-id="370ae-167">Instale el paquete SDK de .NET Core mediante los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="370ae-167">Install the .NET Core SDK package by running the following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-the-sdk-and-runtime"></a><span data-ttu-id="370ae-168">Actualización del SDK y del runtime</span><span class="sxs-lookup"><span data-stu-id="370ae-168">Update the SDK and runtime</span></span>

<span data-ttu-id="370ae-169">Para actualizar a la versión más reciente del SDK y el motor de tiempo de ejecución, ejecute los siguientes pasos (desactive los SDK que no desee actualizar o instalar):</span><span class="sxs-lookup"><span data-stu-id="370ae-169">To update to the latest version of the SDK and runtime, run the following commands (deselect the SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="370ae-170">Para actualizar los archivos binarios del SDK de Java desde Maven, debe actualizar los detalles de la versión del archivo binario correspondiente en el archivo ``build.gradle`` para que señale a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="370ae-170">To update the Java SDK binaries from Maven, you need to update the version details of the corresponding binary in the ``build.gradle`` file to point to the latest version.</span></span> <span data-ttu-id="370ae-171">Para saber exactamente dónde debe actualizar la versión, puede hacer referencia a cualquier archivo ``build.gradle`` en los ejemplos de Introducción a Service Fabric [aquí](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="370ae-171">To know exactly where you need to update the version, you can refer to any ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="370ae-172">La actualización de los paquetes puede dar lugar a que se detenga el clúster de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="370ae-172">Updating the packages might cause your local development cluster to stop running.</span></span> <span data-ttu-id="370ae-173">Reinicie el clúster local después de cada actualización, para lo que debe seguir las instrucciones de esta página.</span><span class="sxs-lookup"><span data-stu-id="370ae-173">Restart your local cluster after an upgrade by following the instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="370ae-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="370ae-174">Next steps</span></span>

* [<span data-ttu-id="370ae-175">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman</span><span class="sxs-lookup"><span data-stu-id="370ae-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="370ae-176">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con el complemento de Eclipse para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="370ae-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="370ae-177">Creación de su primera aplicación de CSharp en Linux</span><span class="sxs-lookup"><span data-stu-id="370ae-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="370ae-178">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="370ae-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="370ae-179">Uso de la CLI de Service Fabric para administrar las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="370ae-179">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="370ae-180">Diferencias entre Service Fabric para Windows y para Linux</span><span class="sxs-lookup"><span data-stu-id="370ae-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="370ae-181">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="370ae-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
