---
title: "Integración continua o implementación continua desde Jenkins en máquinas virtuales de Azure con Team Services | Microsoft Docs"
description: "Configure la integración continua (CI) y la implementación continua (CD) de una aplicación de Node.js con Jenkins en máquinas virtuales de Azure desde Release Management para Visual Studio Team Services (VSTS) o Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: a40e26a8681df31fad664e4d1df4c1513311900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-linux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="bee2b-103">Implementación de la aplicación en máquinas virtuales Linux con Jenkins y Team Services</span><span class="sxs-lookup"><span data-stu-id="bee2b-103">Deploy your app to Linux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="bee2b-104">La integración continua (CI) y la implementación continua (CD) constituyen una canalización mediante la que se puede compilar, publicar e implementar el código.</span><span class="sxs-lookup"><span data-stu-id="bee2b-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="bee2b-105">Team Services proporciona un completo conjunto rico en contenido de herramientas de automatización de CI/CD para la implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="bee2b-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment to Azure.</span></span> <span data-ttu-id="bee2b-106">Jenkins es una popular herramienta basada en servidor de CI/CD de terceros que además proporciona automatización de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="bee2b-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="bee2b-107">Puede usar ambos conjuntamente para personalizar la forma de entrega de la aplicación o el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bee2b-107">You can use both together to customize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="bee2b-108">En este tutorial se usa Jenkins para compilar una **aplicación web de Node.js** y Visual Studio Team Services para implementarla en un [grupo de implementación](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) que contiene máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="bee2b-108">In this tutorial, you use Jenkins to build a **Node.js web app**, and Visual Studio Team Services to deploy it to a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="bee2b-109">Podrá:</span><span class="sxs-lookup"><span data-stu-id="bee2b-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bee2b-110">Compilar la aplicación en Jenkins</span><span class="sxs-lookup"><span data-stu-id="bee2b-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="bee2b-111">Configurar Jenkins para la integración con Team Services</span><span class="sxs-lookup"><span data-stu-id="bee2b-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="bee2b-112">Crear un grupo de implementación para las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="bee2b-112">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="bee2b-113">Crear una definición de versión que configure las máquinas virtuales e implemente la aplicación</span><span class="sxs-lookup"><span data-stu-id="bee2b-113">Create a release definition that configures the VMs and deploys the app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bee2b-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="bee2b-114">Before you begin</span></span>

* <span data-ttu-id="bee2b-115">Necesita acceso a una cuenta de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bee2b-115">You need access to a Jenkins account.</span></span> <span data-ttu-id="bee2b-116">Si aún no ha creado un servidor de Jenkins, vea [Jenkins Documentation (Documentación de Jenkins)](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="bee2b-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="bee2b-117">Inicie sesión en la cuenta de Team Services (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="bee2b-117">Sign in to your Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="bee2b-118">Puede obtener una [cuenta de Team Services gratuita](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="bee2b-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="bee2b-119">Para más información, vea [Connect to Team Services (Conexión a Team Services)](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="bee2b-119">For more information, see [Connect to Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="bee2b-120">Si aún no tiene uno, cree un token de acceso personal (PAT) en la cuenta de Team Services.</span><span class="sxs-lookup"><span data-stu-id="bee2b-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="bee2b-121">Jenkins necesita esta información para acceder a la cuenta de Team Services.</span><span class="sxs-lookup"><span data-stu-id="bee2b-121">Jenkins requires this information to access your Team Services account.</span></span>
  <span data-ttu-id="bee2b-122">Lea [How do I create a personal access token for Team Services and TFS (Cómo crear un token de acceso personal para Team Services y TFS)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) para aprender a generar uno.</span><span class="sxs-lookup"><span data-stu-id="bee2b-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to learn how to generate one.</span></span>

## <a name="get-the-sample-app"></a><span data-ttu-id="bee2b-123">Obtención de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bee2b-123">Get the sample app</span></span>

<span data-ttu-id="bee2b-124">Necesita una aplicación para implementar almacenada en un repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="bee2b-124">You need an app to deploy stored in a Git repository.</span></span>
<span data-ttu-id="bee2b-125">Para este tutorial se recomienda usar [esta aplicación de ejemplo disponible en GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="bee2b-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="bee2b-126">Cree una bifurcación de esta aplicación y anote la ubicación (URL) para usarla en pasos posteriores de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bee2b-126">Create a fork of this app and take note of the location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="bee2b-127">Convierta la bifurcación en **pública** para simplificar la conexión a GitHub más adelante.</span><span class="sxs-lookup"><span data-stu-id="bee2b-127">Make the fork **public** to simplify connecting to GitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="bee2b-128">Para más información, vea [Fork a repo (Bifurcar un repositorio)](https://help.github.com/articles/fork-a-repo/) y [Making a private repository public (Hacer público un repositorio privado)](https://help.github.com/articles/making-a-private-repository-public/).</span><span class="sxs-lookup"><span data-stu-id="bee2b-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="bee2b-129">La aplicación se ha compilado mediante [Yeoman](http://yeoman.io/learning/index.html); usa **Express**, **Bower** y **Grunt** y tiene algunos paquetes **npm** como dependencias.</span><span class="sxs-lookup"><span data-stu-id="bee2b-129">The app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="bee2b-130">La aplicación de ejemplo contiene un conjunto de [plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) que se usan para crear de forma dinámica las máquinas virtuales para su implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="bee2b-130">The sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used to dynamically create the virtual machines for deployment on Azure.</span></span> <span data-ttu-id="bee2b-131">Las tareas de la [definición de versión de Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions) usan estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="bee2b-131">These templates are used by tasks in the [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="bee2b-132">La plantilla principal crea un grupo de seguridad de red, una máquina virtual y una red virtual.</span><span class="sxs-lookup"><span data-stu-id="bee2b-132">The main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="bee2b-133">Asigna una dirección IP pública y abre el puerto de entrada 80.</span><span class="sxs-lookup"><span data-stu-id="bee2b-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="bee2b-134">También agrega una etiqueta que usa el grupo de implementación para seleccionar las máquinas que van a recibir la implementación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-134">It also adds a tag that is used by the deployment group to select the machines to receive the deployment.</span></span>
>
> <span data-ttu-id="bee2b-135">El ejemplo también contiene un script que configura Nginx e implementa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-135">The sample also contains a script that sets up Nginx and deploys the app.</span></span> <span data-ttu-id="bee2b-136">Se ejecuta en cada una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bee2b-136">It is executed on each of the virtual machines.</span></span> <span data-ttu-id="bee2b-137">En concreto, el script instala Node, Nginx y PM2; configura Nginx y PM2 y luego inicia la aplicación Node.</span><span class="sxs-lookup"><span data-stu-id="bee2b-137">Specifically, the script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts the Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="bee2b-138">Configuración de complementos de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bee2b-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="bee2b-139">En primer lugar, debe configurar dos complementos de Jenkins para **NodeJS** y la **integración con Team Services**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="bee2b-140">Abra la cuenta de Jenkins y elija **Manage Jenkins** (Administrar Jenkins).</span><span class="sxs-lookup"><span data-stu-id="bee2b-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="bee2b-141">En la página **Manage Jenkins** (Administrar Jenkins), elija **Manage Plugins** (Administrar complementos).</span><span class="sxs-lookup"><span data-stu-id="bee2b-141">In the **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="bee2b-142">Filtre la lista para buscar el complemento **NodeJS** e instálelo sin reiniciar.</span><span class="sxs-lookup"><span data-stu-id="bee2b-142">Filter the list to locate the **NodeJS** plugin and install it without restart.</span></span>

   ![Adición del complemento NodeJS a Jenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="bee2b-144">Filtre la lista para buscar el complemento **Team Foundation Server** e instálelo.</span><span class="sxs-lookup"><span data-stu-id="bee2b-144">Filter the list to find the **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="bee2b-145">(Este complemento funciona con Team Services y Team Foundation Server). No es necesario reiniciar Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bee2b-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="bee2b-146">Configuración de la compilación de Jenkins para Node.js</span><span class="sxs-lookup"><span data-stu-id="bee2b-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="bee2b-147">En Jenkins, cree un nuevo proyecto de compilación y configúrelo como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="bee2b-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="bee2b-148">En la pestaña **General**, escriba un nombre para el proyecto de compilación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-148">In the **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="bee2b-149">En la pestaña **Administración de código fuente**, seleccione **Git** y escriba los detalles del repositorio y la bifurcación que contienen el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-149">In the **Source Code Management** tab, select **Git** and enter the details of the repository and the branch containing your app code.</span></span>

   ![Adición de un repositorio a la compilación](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="bee2b-151">Si el repositorio no es público, elija **Agregar** y proporcione las credenciales para conectarse a él.</span><span class="sxs-lookup"><span data-stu-id="bee2b-151">If your repository is not public, choose **Add** and provide credentials to connect to it.</span></span>

1. <span data-ttu-id="bee2b-152">En la pestaña **Build Triggers** (Desencadenadores de compilación), seleccione **Poll SCM** (Sondear SCM) y especifique la programación `H/03 * * * *` para sondear el repositorio de Git en busca de cambios cada tres minutos.</span><span class="sxs-lookup"><span data-stu-id="bee2b-152">In the **Build Triggers** tab, select **Poll SCM** and enter the schedule `H/03 * * * *` to poll the Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="bee2b-153">En la pestaña **Build Environment** (Entorno de compilación), seleccione **Provide Node &amp; npm bin/ folder PATH** (Proporcionar ruta de acceso a la carpeta bin/ de Node y npm) y escriba `NodeJS` para el valor de instalación de Node JS.</span><span class="sxs-lookup"><span data-stu-id="bee2b-153">In the **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for the Node JS Installation value.</span></span> <span data-ttu-id="bee2b-154">Deje **npmrc file** establecido en "Usar predeterminado del sistema".</span><span class="sxs-lookup"><span data-stu-id="bee2b-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="bee2b-155">En la pestaña **Compilación**, escriba el comando `npm install` para asegurarse de que se actualicen todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="bee2b-155">In the **Build** tab, enter the command `npm install` to ensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="bee2b-156">Configurar Jenkins para la integración con Team Services</span><span class="sxs-lookup"><span data-stu-id="bee2b-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="bee2b-157">En la pestaña **Post-build Actions** (Acciones posteriores a la compilación), en **Files to archive** (Archivos para archivar), escriba `**/*` para incluir todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="bee2b-157">In the **Post-build Actions** tab, for **Files to archive**, enter `**/*` to include all files.</span></span>

1. <span data-ttu-id="bee2b-158">En **Trigger release in TFS/Team Services** (Desencadenar versión en TFS/Team Services), escriba la dirección URL completa de la cuenta (por ejemplo, `https://your-account-name.visualstudio.com`), el nombre del proyecto, un nombre para la definición de versión (se crea más adelante) y las credenciales para conectarse a la cuenta.</span><span class="sxs-lookup"><span data-stu-id="bee2b-158">For **Trigger release in TFS/Team Services**, enter the full URL of your account (such as `https://your-account-name.visualstudio.com`), the project name, a name for the release definition (created later), and the credentials to connect to your account.</span></span>
   <span data-ttu-id="bee2b-159">Necesita el nombre de usuario y el PAT que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bee2b-159">You need your user name and the PAT you created earlier.</span></span> 

   ![Configuración de acciones posteriores a la compilación de Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="bee2b-161">Guarde el proyecto de compilación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-161">Save the build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="bee2b-162">Creación de un punto de conexión de servicio de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bee2b-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="bee2b-163">Un punto de conexión de servicio permite a Team Services conectarse a Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bee2b-163">A service endpoint allows Team Services to connect to Jenkins.</span></span>

1. <span data-ttu-id="bee2b-164">Abra la página **Servicios** de Team Services, abra la lista **Nuevo punto de conexión de servicio** y elija **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-164">Open the **Services** page in Team Services, open the **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Adición de un punto de conexión de Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="bee2b-166">Escriba el nombre que vaya a usar para hacer referencia a esta conexión.</span><span class="sxs-lookup"><span data-stu-id="bee2b-166">Enter a name you will use to refer to this connection.</span></span>

1. <span data-ttu-id="bee2b-167">Escriba la dirección URL del servidor de Jenkins y active la opción **Aceptar certificados SSL que no son de confianza**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-167">Enter the URL of your Jenkins server, and tick the **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="bee2b-168">Escriba el nombre de usuario y la contraseña de la cuenta de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bee2b-168">Enter the user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="bee2b-169">Elija **Comprobar conexión** para comprobar que la información es correcta.</span><span class="sxs-lookup"><span data-stu-id="bee2b-169">Choose **Verify connection** to check that the information is correct.</span></span>

1. <span data-ttu-id="bee2b-170">Elija **Aceptar** para crear el punto de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="bee2b-170">Choose **OK** to create the service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="bee2b-171">Creación de un grupo de implementación</span><span class="sxs-lookup"><span data-stu-id="bee2b-171">Create a deployment group</span></span>

<span data-ttu-id="bee2b-172">Necesita un [grupo de implementación](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) para incluir las máquinas virtuales en él.</span><span class="sxs-lookup"><span data-stu-id="bee2b-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) to  contain the virtual machines.</span></span>

1. <span data-ttu-id="bee2b-173">Abra la pestaña **Versiones** del nodo **Compilación y versión** y luego abra la pestaña **Grupos de implementación** y elija **+ Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-173">Open the **Releases** tab of the **Build &amp; Release** hub, then open the **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="bee2b-174">Especifique un nombre para el grupo de implementación y una descripción opcional.</span><span class="sxs-lookup"><span data-stu-id="bee2b-174">Enter a name for the deployment group, and an optional description.</span></span>
   <span data-ttu-id="bee2b-175">Luego elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-175">Then choose **Create**.</span></span>

<span data-ttu-id="bee2b-176">La tarea Implementación de un grupo de recursos de Azure crea y registra las máquinas virtuales cuando se ejecuta con la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bee2b-176">The Azure Resource Group Deployment task creates and registers the VMs when it runs using the Azure Resource Manager template.</span></span>
<span data-ttu-id="bee2b-177">El usuario no tiene que crear y registrar las máquinas virtuales por sí mismo.</span><span class="sxs-lookup"><span data-stu-id="bee2b-177">You don't need to create and register the virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="bee2b-178">Creación de una definición de versión</span><span class="sxs-lookup"><span data-stu-id="bee2b-178">Create a release definition</span></span>

<span data-ttu-id="bee2b-179">Una definición de versión especifica el proceso de Team Services que se ejecuta para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-179">A release definition specifies the process Team Services will execute to deploy the app.</span></span>
<span data-ttu-id="bee2b-180">Para crear la definición de versión en Team Services:</span><span class="sxs-lookup"><span data-stu-id="bee2b-180">To create the release definition in Team Services:</span></span>

1. <span data-ttu-id="bee2b-181">Abra la pestaña **Versiones** del nodo **Compilación y versión**, abra el desplegable **+** en la lista de definiciones de versión y elija **Crear definición de versión**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-181">Open the **Releases** tab of the **Build &amp; Release** hub, open the **+** drop-down in the list of release definitions, and choose the **Create release definition**.</span></span> 

1. <span data-ttu-id="bee2b-182">Seleccione la plantilla **Vacía** y elija **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-182">Select the **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="bee2b-183">En la sección **Artefactos**, haga clic en **Vincular un origen de artefacto** y elija **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-183">In the **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="bee2b-184">Seleccione la conexión del punto de conexión de servicio de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bee2b-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="bee2b-185">Luego seleccione el trabajo de origen de Jenkins y elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-185">Then select the Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="bee2b-186">En la nueva definición de versión, elija **+ Agregar tareas** y agregue una tarea **Implementación de un grupo de recursos de Azure** al entorno predeterminado.</span><span class="sxs-lookup"><span data-stu-id="bee2b-186">In the new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task to the default environment.</span></span>

1. <span data-ttu-id="bee2b-187">Elija la flecha desplegable situada junto al vínculo **+ Agregar tareas** y agregue una fase de grupo de implementación a la definición.</span><span class="sxs-lookup"><span data-stu-id="bee2b-187">Choose the drop down arrow next to the **+ Add tasks** link and add a deployment group phase to the definition.</span></span>

   ![Adición de una fase de grupo de implementación](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="bee2b-189">En el catálogo Tarea, abra la sección **Utilidad** y agregue una instancia de la tarea **Script de Shell**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-189">In the Task catalog, open the **Utility** section and add an instance of the **Shell Script** task.</span></span>

1. <span data-ttu-id="bee2b-190">La plantilla de parámetros usada en la tarea Implementación de un grupo de recursos de Azure establece la contraseña de administrador que se emplea para conectarse a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bee2b-190">The parameters template used in the Azure Resource Group Deployment task sets the admin password used to connect to the VMs.</span></span>
   <span data-ttu-id="bee2b-191">Indique esta contraseña con la variable **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="bee2b-191">You provide this password with the variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="bee2b-192">Abra la pestaña **Variables** y, en la sección **Variables**, escriba el nombre `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="bee2b-192">Open the **Variables** tab and, in the **Variables** section, enter the name `adminpassword`.</span></span>

   - <span data-ttu-id="bee2b-193">Escriba la contraseña de administrador.</span><span class="sxs-lookup"><span data-stu-id="bee2b-193">Enter the administrator password.</span></span>

   - <span data-ttu-id="bee2b-194">Elija el icono de "candado" situado junto al cuadro de texto de valor para proteger la contraseña.</span><span class="sxs-lookup"><span data-stu-id="bee2b-194">Choose the "padlock" icon next to the value textbox to protect the password.</span></span> 

## <a name="configure-the-azure-resource-group-deployment-task"></a><span data-ttu-id="bee2b-195">Configuración de la tarea Implementación de un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="bee2b-195">Configure the Azure Resource Group Deployment task</span></span>

<span data-ttu-id="bee2b-196">La tarea **Implementación de un grupo de recursos de Azure** se usa para crear el grupo de implementación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-196">The **Azure Resource Group Deployment** task is used to create the deployment group.</span></span> <span data-ttu-id="bee2b-197">Configúrelo de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="bee2b-197">Configure it as follows:</span></span>

* <span data-ttu-id="bee2b-198">**Suscripción de Azure:** seleccione una conexión de la lista de **Conexiones a servicios de Azure disponibles**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-198">**Azure Subscription:** Select a connection from the list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="bee2b-199">Si no aparece ninguna conexión, elija **Administrar**, seleccione **Nuevo punto de conexión de servicio**, luego **Azure Resource Manager** y siga los mensajes.</span><span class="sxs-lookup"><span data-stu-id="bee2b-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow the prompts.</span></span>
  <span data-ttu-id="bee2b-200">Vuelva a la definición de versión, actualice la lista **Suscripción de AzureRM** y seleccione la conexión creada.</span><span class="sxs-lookup"><span data-stu-id="bee2b-200">Return to your release definition, refresh the **AzureRM Subscription** list, and select the connection you created.</span></span>

* <span data-ttu-id="bee2b-201">**Grupo de recursos**: escriba el nombre del grupo de recursos creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bee2b-201">**Resource group**: Enter a name of the resource group you created earlier.</span></span>

* <span data-ttu-id="bee2b-202">**Ubicación**: seleccione una región para la implementación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-202">**Location**: Select a region for the deployment.</span></span>

  ![Creación de un nuevo grupo de recursos](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="bee2b-204">**Ubicación de la plantilla**: `URL of the file`</span><span class="sxs-lookup"><span data-stu-id="bee2b-204">**Template location**: `URL of the file`</span></span>

* <span data-ttu-id="bee2b-205">**Vínculo de la plantilla**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="bee2b-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="bee2b-206">**Vínculo de parámetros de la plantilla**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="bee2b-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="bee2b-207">**Reemplazar parámetros de plantilla**: una lista de los valores de invalidación, por ejemplo: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="bee2b-207">**Override template parameters**: A list of the override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="bee2b-208">Inserte sus propios valores específicos para los {marcadores de posición}.</span><span class="sxs-lookup"><span data-stu-id="bee2b-208">Insert your own specific values for the {placeholders}.</span></span> 

* <span data-ttu-id="bee2b-209">**Habilitar requisitos previos**: `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="bee2b-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="bee2b-210">**Punto de conexión de TFS o VSTS**: elija **Agregar** y, en el cuadro de diálogo "Agregar nueva conexión de Team Foundation Server/Team Services", seleccione **Autenticación basada en token**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-210">**TFS/VSTS endpoint**: Choose **Add** and, in the "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="bee2b-211">Escriba el nombre de la conexión y la dirección URL del proyecto de equipo.</span><span class="sxs-lookup"><span data-stu-id="bee2b-211">Enter a name of the connection and the URL of your team project.</span></span> <span data-ttu-id="bee2b-212">Luego genere y escriba un [token de acceso personal (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) para autenticar la conexión al proyecto de equipo.</span><span class="sxs-lookup"><span data-stu-id="bee2b-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to authenticate the connection to your team project.</span></span>

  ![Creación de un token de acceso personal](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="bee2b-214">**Proyecto de equipo**: seleccione el proyecto actual.</span><span class="sxs-lookup"><span data-stu-id="bee2b-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="bee2b-215">**Grupo de implementación**: escriba el mismo nombre de grupo de implementación que ha usado para el parámetro **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-215">**Deployment Group**: Enter the same deployment group name as you used for the **Resource group** parameter.</span></span>

<span data-ttu-id="bee2b-216">La configuración predeterminada de la tarea Implementación de un grupo de recursos de Azure es crear o actualizar un recurso y hacerlo de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="bee2b-216">The default settings for the Azure Resource Group Deployment task are to create or update a resource, and to do so incrementally.</span></span> <span data-ttu-id="bee2b-217">La tarea crea las máquinas virtuales la primera vez que se ejecuta y posteriormente simplemente las actualiza.</span><span class="sxs-lookup"><span data-stu-id="bee2b-217">The task creates the VMs the first time it runs, and subsequently just update them.</span></span>

## <a name="configure-the-shell-script-task"></a><span data-ttu-id="bee2b-218">Configuración de la tarea Script de Shell</span><span class="sxs-lookup"><span data-stu-id="bee2b-218">Configure the Shell Script task</span></span>

<span data-ttu-id="bee2b-219">La tarea **Script de Shell** se usa para proporcionar la configuración de un script que se ejecuta en cada servidor para instalar Node.js e iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-219">The **Shell Script** task is used to provide the configuration for a script to run on each server to install Node.js and start the app.</span></span> <span data-ttu-id="bee2b-220">Configúrelo de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="bee2b-220">Configure it as follows:</span></span>

* <span data-ttu-id="bee2b-221">**Ruta de acceso del script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="bee2b-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="bee2b-222">**Especificar directorio de trabajo**: `Checked`</span><span class="sxs-lookup"><span data-stu-id="bee2b-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="bee2b-223">**Directorio de trabajo**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="bee2b-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-the-release-definition"></a><span data-ttu-id="bee2b-224">Cambio del nombre de la definición de versión y guardado</span><span class="sxs-lookup"><span data-stu-id="bee2b-224">Rename and save the release definition</span></span>

1. <span data-ttu-id="bee2b-225">Cambie el nombre de la definición de versión por el nombre especificado en la pestaña **Post-build Actions** (Acciones posteriores a la compilación) de la compilación en Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bee2b-225">Edit the name of the release definition to the name you specified in the **Post-build Actions** tab of the build in Jenkins.</span></span> <span data-ttu-id="bee2b-226">Jenkins necesita este nombre para desencadenar una nueva versión cuando se actualizan los artefactos de origen.</span><span class="sxs-lookup"><span data-stu-id="bee2b-226">Jenkins requires this name to be able to trigger a new release when the source artifacts are updated.</span></span>

1. <span data-ttu-id="bee2b-227">Opcionalmente, cambie el nombre del entorno al hacer clic en el nombre.</span><span class="sxs-lookup"><span data-stu-id="bee2b-227">Optionally, change the name of the environment by clicking on the name.</span></span> 

1. <span data-ttu-id="bee2b-228">Elija **Guardar** y luego **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="bee2b-229">Inicio de una implementación manual</span><span class="sxs-lookup"><span data-stu-id="bee2b-229">Start a manual deployment</span></span>

1. <span data-ttu-id="bee2b-230">Elija **+ Versión** y seleccione **Crear versión**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="bee2b-231">Seleccione la compilación completada en la lista desplegable resaltada y elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bee2b-231">Select the build you completed in the highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="bee2b-232">Elija el vínculo de la versión en el mensaje emergente.</span><span class="sxs-lookup"><span data-stu-id="bee2b-232">Choose the release link in the popup message.</span></span> <span data-ttu-id="bee2b-233">Por ejemplo: "Versión **Release-1** se ha creado".</span><span class="sxs-lookup"><span data-stu-id="bee2b-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="bee2b-234">Abra la pestaña **Registros** para ver la salida de la consola de la versión.</span><span class="sxs-lookup"><span data-stu-id="bee2b-234">Open the **Logs** tab to watch the release console output.</span></span>

1. <span data-ttu-id="bee2b-235">En el explorador, abra la dirección URL de uno de los servidores agregados al grupo de implementación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-235">In your browser, open the URL of one of the servers you added to your deployment group.</span></span> <span data-ttu-id="bee2b-236">Por ejemplo, escriba `http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="bee2b-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="bee2b-237">Inicio de una implementación de CI/CD</span><span class="sxs-lookup"><span data-stu-id="bee2b-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="bee2b-238">En la definición de versión, desactive la casilla **Habilitado** de la sección **Opciones de control** de la configuración de la tarea Implementación de un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bee2b-238">In the release definition, uncheck the **Enabled** checkbox in the **Control Options** section of the settings for the Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="bee2b-239">Para implementaciones futuras en el grupo de implementación existente, no es necesario volver a ejecutar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="bee2b-239">For future deployments to the existing deployment group, you do not need to re-execute this task.</span></span>

1. <span data-ttu-id="bee2b-240">Vaya al repositorio de Git de origen y modifique el contenido del encabezado **h1** del archivo [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="bee2b-240">Go to the source Git repository and modify the contents of the **h1** heading in the file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="bee2b-241">Confirme el cambio.</span><span class="sxs-lookup"><span data-stu-id="bee2b-241">Commit your change.</span></span>

1. <span data-ttu-id="bee2b-242">Pasados unos minutos, verá una nueva versión creada en la página **Versiones** de Team Services o TFS.</span><span class="sxs-lookup"><span data-stu-id="bee2b-242">After a few minutes, you will see a new release created in the **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="bee2b-243">Abra la versión para ver cómo se realiza la implementación.</span><span class="sxs-lookup"><span data-stu-id="bee2b-243">Open the release to see the deployment taking place.</span></span> <span data-ttu-id="bee2b-244">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="bee2b-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="bee2b-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bee2b-245">Next Steps</span></span>

<span data-ttu-id="bee2b-246">En este tutorial se ha automatizado la implementación de una aplicación en Azure con la compilación de Jenkins y Team Services para la versión.</span><span class="sxs-lookup"><span data-stu-id="bee2b-246">In this tutorial, you automated the deployment of an app to Azure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="bee2b-247">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="bee2b-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bee2b-248">Compilar la aplicación en Jenkins</span><span class="sxs-lookup"><span data-stu-id="bee2b-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="bee2b-249">Configurar Jenkins para la integración con Team Services</span><span class="sxs-lookup"><span data-stu-id="bee2b-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="bee2b-250">Crear un grupo de implementación para las máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="bee2b-250">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="bee2b-251">Crear una definición de versión que configure las máquinas virtuales e implemente la aplicación</span><span class="sxs-lookup"><span data-stu-id="bee2b-251">Create a release definition that configures the VMs and deploys the app</span></span>

<span data-ttu-id="bee2b-252">Siga con el próximo tutorial para aprender a implementar una pila LAMP (Linux, Apache, MySQL y PHP).</span><span class="sxs-lookup"><span data-stu-id="bee2b-252">Advance to the next tutorial to learn more about how to deploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bee2b-253">Implementación de una pila de LAMP</span><span class="sxs-lookup"><span data-stu-id="bee2b-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)