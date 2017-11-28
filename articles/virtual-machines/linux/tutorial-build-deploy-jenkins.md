---
title: "aaaCI/CD desde Jenkins tooAzure las máquinas virtuales con Team Services | Documentos de Microsoft"
description: "Configurar la integración continua (CI) y la implementación continua (CD) de una aplicación de Node.js con las máquinas virtuales de Jenkins tooAzure de la administración de versión de Visual Studio Team Services (VSTS) o Microsoft Team Foundation Server (TFS)"
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
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="b1240-103">Implementar la VM de aplicación tooLinux con Jenkins y Team Services</span><span class="sxs-lookup"><span data-stu-id="b1240-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="b1240-104">La integración continua (CI) y la implementación continua (CD) constituyen una canalización mediante la que se puede compilar, publicar e implementar el código.</span><span class="sxs-lookup"><span data-stu-id="b1240-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="b1240-105">Team Services proporciona un conjunto completo, completo CI/CD de herramientas de automatización para tooAzure de implementación.</span><span class="sxs-lookup"><span data-stu-id="b1240-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="b1240-106">Jenkins es una popular herramienta basada en servidor de CI/CD de terceros que además proporciona automatización de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="b1240-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="b1240-107">Puede usar ambos conjuntamente toocustomize cómo entregar la aplicación en la nube o el servicio.</span><span class="sxs-lookup"><span data-stu-id="b1240-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="b1240-108">En este tutorial, utilice Jenkins toobuild una **aplicación web de Node.js**y Visual Studio Team Services toodeploy, tooa [grupo de implementación](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) que contiene máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="b1240-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="b1240-109">Podrá:</span><span class="sxs-lookup"><span data-stu-id="b1240-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1240-110">Compilar la aplicación en Jenkins</span><span class="sxs-lookup"><span data-stu-id="b1240-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="b1240-111">Configurar Jenkins para la integración con Team Services</span><span class="sxs-lookup"><span data-stu-id="b1240-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="b1240-112">Crear un grupo de implementación para hello máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="b1240-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="b1240-113">Crear una definición de la versión que configura las máquinas virtuales de hello e implementa la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="b1240-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b1240-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b1240-114">Before you begin</span></span>

* <span data-ttu-id="b1240-115">Necesita acceso tooa Jenkins cuenta.</span><span class="sxs-lookup"><span data-stu-id="b1240-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="b1240-116">Si aún no ha creado un servidor de Jenkins, vea [Jenkins Documentation (Documentación de Jenkins)](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="b1240-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="b1240-117">Inicie sesión en tooyour cuenta de Team Services (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="b1240-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="b1240-118">Puede obtener una [cuenta de Team Services gratuita](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="b1240-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="b1240-119">Para obtener más información, consulte [conectar servicios de tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="b1240-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="b1240-120">Si aún no tiene uno, cree un token de acceso personal (PAT) en la cuenta de Team Services.</span><span class="sxs-lookup"><span data-stu-id="b1240-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="b1240-121">Jenkins requiere esta tooaccess información de su cuenta de Team Services.</span><span class="sxs-lookup"><span data-stu-id="b1240-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="b1240-122">Lectura [cómo crear un token de acceso personal para Team Services y TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn cómo toogenerate uno.</span><span class="sxs-lookup"><span data-stu-id="b1240-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="b1240-123">Obtener la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="b1240-123">Get hello sample app</span></span>

<span data-ttu-id="b1240-124">Es necesario un toodeploy de aplicación almacenado en un repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="b1240-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="b1240-125">Para este tutorial se recomienda usar [esta aplicación de ejemplo disponible en GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="b1240-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="b1240-126">Crear una bifurcación de esta aplicación y tome nota de hello ubicación (URL) para su uso en pasos posteriores de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b1240-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="b1240-127">Asegúrese de bifurcación de hello **público** toosimplify conectar tooGitHub más tarde.</span><span class="sxs-lookup"><span data-stu-id="b1240-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="b1240-128">Para más información, vea [Fork a repo (Bifurcar un repositorio)](https://help.github.com/articles/fork-a-repo/) y [Making a private repository public (Hacer público un repositorio privado)](https://help.github.com/articles/making-a-private-repository-public/).</span><span class="sxs-lookup"><span data-stu-id="b1240-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="b1240-129">aplicación Hello se compiló mediante [Yeoman](http://yeoman.io/learning/index.html); usa **Express**, **bower**, y **grunt**; y tiene algunos **npm**paquetes como dependencias.</span><span class="sxs-lookup"><span data-stu-id="b1240-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="b1240-130">aplicación de ejemplo de Hola contiene un conjunto de [plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) que se toodynamically usado crear máquinas virtuales de hello para la implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="b1240-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="b1240-131">Estas plantillas se utilizan las tareas de hello [definición de la versión de Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="b1240-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="b1240-132">plantilla de Hello principal crea un grupo de seguridad de red, una máquina virtual y una red virtual.</span><span class="sxs-lookup"><span data-stu-id="b1240-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="b1240-133">Asigna una dirección IP pública y abre el puerto de entrada 80.</span><span class="sxs-lookup"><span data-stu-id="b1240-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="b1240-134">También agrega una etiqueta que se usa por la implementación de hello implementación grupo demasiado seleccione Hola máquinas tooreceive Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="b1240-135">ejemplo de Hola también contiene una secuencia de comandos que configura Nginx e implementa la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b1240-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="b1240-136">Se ejecuta en cada una de las máquinas virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="b1240-137">En concreto, el script de Hola instala nodo, Nginx y PM2; configura Nginx y PM2; a continuación, inicia Hola nodo aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1240-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="b1240-138">Configuración de complementos de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b1240-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="b1240-139">En primer lugar, debe configurar dos complementos de Jenkins para **NodeJS** y la **integración con Team Services**.</span><span class="sxs-lookup"><span data-stu-id="b1240-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="b1240-140">Abra la cuenta de Jenkins y elija **Manage Jenkins** (Administrar Jenkins).</span><span class="sxs-lookup"><span data-stu-id="b1240-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="b1240-141">Hola **administrar Jenkins** página, elija **administrar complementos**.</span><span class="sxs-lookup"><span data-stu-id="b1240-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="b1240-142">Filtro Hola lista toolocate Hola **NodeJS** complemento e instalarlo sin necesidad de reiniciar.</span><span class="sxs-lookup"><span data-stu-id="b1240-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Agregar complemento tooJenkins de hello NodeJS](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="b1240-144">Filtro Hola lista toofind Hola **Team Foundation Server** complemento e instalarlo.</span><span class="sxs-lookup"><span data-stu-id="b1240-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="b1240-145">(Este complemento funciona con Team Services y Team Foundation Server). No es necesario reiniciar Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b1240-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="b1240-146">Configuración de la compilación de Jenkins para Node.js</span><span class="sxs-lookup"><span data-stu-id="b1240-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="b1240-147">En Jenkins, cree un nuevo proyecto de compilación y configúrelo como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b1240-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="b1240-148">Hola **General** ficha, escriba un nombre para el proyecto de compilación.</span><span class="sxs-lookup"><span data-stu-id="b1240-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="b1240-149">Hola **administración de código fuente** ficha, seleccione **Git** y escriba los detalles de hello del repositorio de Hola y bifurcación de Hola que contiene el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1240-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Agregar una compilación de tooyour de repositorio](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="b1240-151">Si el repositorio no es público, elija **agregar** y proporcionar credenciales tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="b1240-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="b1240-152">Hola **crear desencadenadores** ficha, seleccione **sondeo SCM** y especifique la programación de hello `H/03 * * * *` repositorio de Git de hello toopoll cambios cada tres minutos.</span><span class="sxs-lookup"><span data-stu-id="b1240-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="b1240-153">Hola **entorno de compilación de** ficha, seleccione **proporcionar nodo &amp; npm bin / ruta de acceso de carpeta** y escriba `NodeJS` para el valor de nodo JS instalación Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="b1240-154">Deje **npmrc file** establecido en "Usar predeterminado del sistema".</span><span class="sxs-lookup"><span data-stu-id="b1240-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="b1240-155">Hola **generar** ficha, escriba el comando hello `npm install` tooensure se actualizan todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="b1240-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="b1240-156">Configurar Jenkins para la integración con Team Services</span><span class="sxs-lookup"><span data-stu-id="b1240-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="b1240-157">Hola **acciones posteriores a la compilación** ficha, para **archivos tooarchive**, escriba `**/*` tooinclude todos los archivos.</span><span class="sxs-lookup"><span data-stu-id="b1240-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="b1240-158">Para **desencadenar el lanzamiento de TFS y Team Services**, escriba Hola de dirección URL completa de la cuenta (como `https://your-account-name.visualstudio.com`), Hola nombre del proyecto, un nombre para la definición de versión de hello (creado más adelante), y Hola cuenta de credenciales tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="b1240-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="b1240-159">Necesita el nombre de usuario y Hola PAT que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b1240-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Configuración de acciones posteriores a la compilación de Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="b1240-161">Guarde el proyecto de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="b1240-162">Creación de un punto de conexión de servicio de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b1240-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="b1240-163">Un extremo de servicio permite Team Services tooconnect tooJenkins.</span><span class="sxs-lookup"><span data-stu-id="b1240-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="b1240-164">Abra hello **servicios** página en Team Services, abra hello **nuevo extremo de servicio** lista y elija **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="b1240-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Adición de un punto de conexión de Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="b1240-166">Escriba un nombre que se va a utilizar toorefer toothis conexión.</span><span class="sxs-lookup"><span data-stu-id="b1240-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="b1240-167">Escriba Hola URL del servidor Jenkins y graduación hello **Aceptar los certificados SSL no es de confianza** opción.</span><span class="sxs-lookup"><span data-stu-id="b1240-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="b1240-168">Escriba el nombre de usuario de Hola y la contraseña de su cuenta de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b1240-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="b1240-169">Elija **Comprobar conexión** toocheck que Hola información es correcta.</span><span class="sxs-lookup"><span data-stu-id="b1240-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="b1240-170">Elija **Aceptar** extremo de servicio de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="b1240-171">Creación de un grupo de implementación</span><span class="sxs-lookup"><span data-stu-id="b1240-171">Create a deployment group</span></span>

<span data-ttu-id="b1240-172">Necesita un [grupo de implementación](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) demasiado contienen hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b1240-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="b1240-173">Hola abierto **versiones** ficha de hello **generar &amp; versión** concentrador, a continuación, abra hello **grupos de implementación** y a **+ nuevo**.</span><span class="sxs-lookup"><span data-stu-id="b1240-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="b1240-174">Escriba un nombre para el grupo de implementación de hello y una descripción opcional.</span><span class="sxs-lookup"><span data-stu-id="b1240-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="b1240-175">Luego elija **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b1240-175">Then choose **Create**.</span></span>

<span data-ttu-id="b1240-176">tarea de implementación de grupo de recursos de Azure de Hello crea y registra hello las máquinas virtuales cuando se ejecuta con la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b1240-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="b1240-177">No necesita toocreate y registre las máquinas virtuales Hola usted mismo.</span><span class="sxs-lookup"><span data-stu-id="b1240-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="b1240-178">Creación de una definición de versión</span><span class="sxs-lookup"><span data-stu-id="b1240-178">Create a release definition</span></span>

<span data-ttu-id="b1240-179">Una definición de versión especifica proceso Hola Team Services ejecutará la aplicación de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b1240-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="b1240-180">definición de versión de hello toocreate en Team Services:</span><span class="sxs-lookup"><span data-stu-id="b1240-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="b1240-181">Hola abierto **versiones** ficha de hello **compilar &amp; versión** concentrador, abra hello  **+**  desplegable en la lista de Hola de definiciones de versión y elija Hola **crear versión definición**.</span><span class="sxs-lookup"><span data-stu-id="b1240-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="b1240-182">Seleccione hello **vacía** plantilla y elija **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b1240-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="b1240-183">Hola **artefactos** sección, haga clic en **vincular un artefacto** y elija **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="b1240-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="b1240-184">Seleccione la conexión del punto de conexión de servicio de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b1240-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="b1240-185">A continuación, seleccione Hola Jenkins origen trabajo y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="b1240-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="b1240-186">Hola nueva definición de la versión, elija **+ agregar tareas** y agregue un **implementación de grupo de recursos de Azure** entorno de tarea toohello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="b1240-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="b1240-187">Elija Hola desplegable flecha siguiente toohello **+ agregar tareas** vincular y agregar una definición de toohello de fase de grupo de implementación.</span><span class="sxs-lookup"><span data-stu-id="b1240-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Adición de una fase de grupo de implementación](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="b1240-189">En el catálogo de la tarea de hello, abra hello **utilidad** sección y agregue una instancia del programa Hola a **secuencia de comandos de Shell** tarea.</span><span class="sxs-lookup"><span data-stu-id="b1240-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="b1240-190">plantilla de parámetros de Hello utilizada en la tarea de implementación de grupo de recursos de Azure de hello establece Hola admin contraseña utilizada tooconnect toohello máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b1240-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="b1240-191">Indique la contraseña con la variable de hello **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="b1240-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="b1240-192">Abra hello **Variables** ficha y, en hello **Variables** sección, escriba el nombre de hello `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="b1240-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="b1240-193">Escriba la contraseña de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="b1240-194">Elija Hola "candado" icono siguiente toohello valor textbox tooprotect Hola contraseña.</span><span class="sxs-lookup"><span data-stu-id="b1240-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="b1240-195">Configurar la tarea de implementación de grupo de recursos de Azure de hello</span><span class="sxs-lookup"><span data-stu-id="b1240-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="b1240-196">Hola **implementación de grupo de recursos de Azure** tarea es el grupo de implementación de hello toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="b1240-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="b1240-197">Configúrelo de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="b1240-197">Configure it as follows:</span></span>

* <span data-ttu-id="b1240-198">**Suscripción de Azure:** seleccione una conexión de lista de hello en **conexiones de servicio de Azure disponibles**.</span><span class="sxs-lookup"><span data-stu-id="b1240-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="b1240-199">Si no hay ninguna conexión aparece, elija **administrar**, seleccione **nuevo extremo de servicio** , a continuación, **Azure Resource Manager**y siga las indicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="b1240-200">Devolver tooyour versión definición, actualización hello **AzureRM suscripción** lista y conexión Hola select que ha creado.</span><span class="sxs-lookup"><span data-stu-id="b1240-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="b1240-201">**Grupo de recursos**: escriba un nombre de grupo de recursos de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b1240-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="b1240-202">**Ubicación**: seleccionar una región para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-202">**Location**: Select a region for hello deployment.</span></span>

  ![Creación de un nuevo grupo de recursos](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="b1240-204">**Ubicación de la plantilla**: `URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="b1240-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="b1240-205">**Vínculo de la plantilla**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="b1240-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="b1240-206">**Vínculo de parámetros de la plantilla**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="b1240-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="b1240-207">**Reemplazar parámetros de plantilla**: una lista de hello invalidar valores, por ejemplo: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="b1240-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="b1240-208">Insertar sus propios valores específicos de Hola {marcadores de posición}.</span><span class="sxs-lookup"><span data-stu-id="b1240-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="b1240-209">**Habilitar requisitos previos**: `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="b1240-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="b1240-210">**Punto de conexión TFS/VSTS**: elija **agregar** y, en el cuadro de diálogo "Agregar nueva conexión de los servicios servidor/equipo de Team Foundation" Hola, seleccione **autenticación basada en Token**.</span><span class="sxs-lookup"><span data-stu-id="b1240-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="b1240-211">Escriba un nombre de conexión de Hola y Hola URL del proyecto de equipo.</span><span class="sxs-lookup"><span data-stu-id="b1240-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="b1240-212">A continuación, generar y escriba un [símbolo (token) de acceso Personal (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) proyecto de equipo de tooauthenticate Hola conexión tooyour.</span><span class="sxs-lookup"><span data-stu-id="b1240-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Creación de un token de acceso personal](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="b1240-214">**Proyecto de equipo**: seleccione el proyecto actual.</span><span class="sxs-lookup"><span data-stu-id="b1240-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="b1240-215">**Grupo de implementación**: escriba Hola el mismo nombre de grupo de implementación que ha usado para hello **grupo de recursos** parámetro.</span><span class="sxs-lookup"><span data-stu-id="b1240-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="b1240-216">configuración predeterminada de Hello para la tarea de implementación de grupo de recursos de Azure de hello es toocreate o actualiza un recurso y toodo de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="b1240-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="b1240-217">tarea Hello crea Hola Hola de máquinas virtuales de primera vez que se ejecuta y posteriormente simplemente actualizarlos.</span><span class="sxs-lookup"><span data-stu-id="b1240-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="b1240-218">Configurar la tarea de secuencia de comandos de Shell de Hola</span><span class="sxs-lookup"><span data-stu-id="b1240-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="b1240-219">Hola **secuencia de comandos de Shell** tarea es la configuración de Hola de tooprovide usado para un toorun de script en cada aplicación de hello de servidor tooinstall Node.js e iniciar.</span><span class="sxs-lookup"><span data-stu-id="b1240-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="b1240-220">Configúrelo de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="b1240-220">Configure it as follows:</span></span>

* <span data-ttu-id="b1240-221">**Ruta de acceso del script**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="b1240-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="b1240-222">**Especificar directorio de trabajo**: `Checked`</span><span class="sxs-lookup"><span data-stu-id="b1240-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="b1240-223">**Directorio de trabajo**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="b1240-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="b1240-224">Cambiar el nombre y guardar la definición de la versión de Hola</span><span class="sxs-lookup"><span data-stu-id="b1240-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="b1240-225">Editar nombre de Hola de nombre de definición toohello de hello versión especificada en el **acciones posteriores a la compilación** pestaña de generación de hello en Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b1240-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="b1240-226">Jenkins requiere este tootrigger capaz de una nueva versión toobe de nombre cuando se actualizan los artefactos de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="b1240-227">Si lo desea, cambie el nombre de hello del entorno de hello haciendo clic en el nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="b1240-228">Elija **Guardar** y luego **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b1240-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="b1240-229">Inicio de una implementación manual</span><span class="sxs-lookup"><span data-stu-id="b1240-229">Start a manual deployment</span></span>

1. <span data-ttu-id="b1240-230">Elija **+ Versión** y seleccione **Crear versión**.</span><span class="sxs-lookup"><span data-stu-id="b1240-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="b1240-231">Seleccionar compilación de Hola que completado en la lista desplegable resaltada de Hola y elija **crear**.</span><span class="sxs-lookup"><span data-stu-id="b1240-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="b1240-232">Elija el vínculo de la versión de hello en mensajes de bienvenida del menú emergente.</span><span class="sxs-lookup"><span data-stu-id="b1240-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="b1240-233">Por ejemplo: "Versión **Release-1** se ha creado".</span><span class="sxs-lookup"><span data-stu-id="b1240-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="b1240-234">Abra hello **registros** ficha salida de la consola de toowatch Hola versión.</span><span class="sxs-lookup"><span data-stu-id="b1240-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="b1240-235">En el explorador, abra Hola URL de uno de los servidores de hello Agregar grupo de implementación de tooyour.</span><span class="sxs-lookup"><span data-stu-id="b1240-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="b1240-236">Por ejemplo, escriba `http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="b1240-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="b1240-237">Inicio de una implementación de CI/CD</span><span class="sxs-lookup"><span data-stu-id="b1240-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="b1240-238">Hola de definición de la versión, desactive la opción hello **habilitado** checkbox en hello **opciones de Control** sección de configuración de hello para la tarea de implementación de grupo de recursos de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="b1240-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="b1240-239">Para el grupo futuras implementaciones toohello de implementación, no es necesario toore-ejecutar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="b1240-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="b1240-240">Vaya toohello repositorio de Git de origen y modificar contenido de Hola de hello **h1** encabezado en el archivo hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="b1240-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="b1240-241">Confirme el cambio.</span><span class="sxs-lookup"><span data-stu-id="b1240-241">Commit your change.</span></span>

1. <span data-ttu-id="b1240-242">Después de unos minutos, verá una nueva versión que creó en hello **versiones** página de Team Services o TFS.</span><span class="sxs-lookup"><span data-stu-id="b1240-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="b1240-243">Abra la implementación de Hola Hola versión toosee teniendo lugar.</span><span class="sxs-lookup"><span data-stu-id="b1240-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="b1240-244">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="b1240-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1240-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1240-245">Next Steps</span></span>

<span data-ttu-id="b1240-246">En este tutorial, se Hola la implementación automatizada de un tooAzure de aplicación con compilación Jenkins y servicios de equipo para la versión.</span><span class="sxs-lookup"><span data-stu-id="b1240-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="b1240-247">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="b1240-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1240-248">Compilar la aplicación en Jenkins</span><span class="sxs-lookup"><span data-stu-id="b1240-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="b1240-249">Configurar Jenkins para la integración con Team Services</span><span class="sxs-lookup"><span data-stu-id="b1240-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="b1240-250">Crear un grupo de implementación para hello máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="b1240-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="b1240-251">Crear una definición de la versión que configura las máquinas virtuales de hello e implementa la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="b1240-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="b1240-252">Avanzar toohello siguiente tutorial toolearn más información acerca de cómo la pila toodeploy una luz (Linux, Apache, MySQL y PHP).</span><span class="sxs-lookup"><span data-stu-id="b1240-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1240-253">Implementación de una pila de LAMP</span><span class="sxs-lookup"><span data-stu-id="b1240-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)