---
title: aaaCI/CD con motor del servicio de contenedor de Azure y el modo Swarm | Documentos de Microsoft
description: "Usar el motor del servicio de contenedor de Azure con Docker Swarm modo, un registro de contenedor de Azure y Visual Studio Team Services toodeliver continuamente una aplicación de .NET Core contenedor múltiples"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, contenedores, microservicios, Swarm, Azure, Visual Studio Team Services, DevOps, ACS Engine
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="66546-104">Completa CI/CD canalización toodeploy una aplicación de contenedor múltiples en el servicio de contenedor de Azure con el motor de ACS y el modo de Swarm de Docker mediante Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="66546-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="66546-105">*En este artículo se basa en [completa/CD de elemento de configuración de canalización toodeploy una aplicación de contenedor múltiples en el servicio de contenedor de Azure con Docker Swarm con Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentación*</span><span class="sxs-lookup"><span data-stu-id="66546-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="66546-106">Hoy en día, uno de Hola mayores desafíos cuando desarrollo de aplicaciones modernas de nube de Hola se toodeliver capaz de estas aplicaciones continuamente.</span><span class="sxs-lookup"><span data-stu-id="66546-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="66546-107">En este artículo, aprenderá cómo tooimplement una integración completa continua e implementación (CI/CD) canalización utilizando:</span><span class="sxs-lookup"><span data-stu-id="66546-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="66546-108">Azure Container Service Engine con modo Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="66546-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="66546-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="66546-109">Azure Container Registry</span></span>
* <span data-ttu-id="66546-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="66546-110">Visual Studio Team Services</span></span>

<span data-ttu-id="66546-111">Este artículo se basa en una aplicación sencilla, disponible en [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), desarrollada con ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="66546-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="66546-112">aplicación Hello se compone de cuatro servicios diferentes: tres web API y front-end uno web:</span><span class="sxs-lookup"><span data-stu-id="66546-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="66546-114">el objetivo de Hello es toodeliver esta aplicación continuamente en un clúster en modo de Docker Swarm, mediante Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="66546-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="66546-115">Hola siguiente ilustración, detalles de esta canalización de la entrega continua:</span><span class="sxs-lookup"><span data-stu-id="66546-115">hello following figure details this continuous delivery pipeline:</span></span>

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="66546-117">Aquí es una breve explicación de los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="66546-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="66546-118">Cambios de código están confirmados toohello repositorio de código fuente (aquí, GitHub)</span><span class="sxs-lookup"><span data-stu-id="66546-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="66546-119">GitHub desencadena una compilación en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="66546-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="66546-120">Visual Studio Team Services obtiene la versión más reciente de Hola de orígenes de Hola y compila todas las imágenes de Hola que componen la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="66546-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="66546-121">Visual Studio Team Services inserta cada registro de Docker de tooa imágenes creado con el servicio de registro de contenedor de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="66546-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="66546-122">Visual Studio Team Services desencadena una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="66546-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="66546-123">versión de Hola ejecuta algunos comandos mediante SSH en el nodo principal del clúster de servicio de hello contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="66546-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="66546-124">Docker Swarm el modo en el clúster de hello extrae la versión más reciente de Hola de imágenes de Hola</span><span class="sxs-lookup"><span data-stu-id="66546-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="66546-125">se implementa Hola nueva versión de la aplicación hello utilizan la pila de Docker</span><span class="sxs-lookup"><span data-stu-id="66546-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="66546-126">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66546-126">Prerequisites</span></span>

<span data-ttu-id="66546-127">Antes de iniciar este tutorial, necesita hello toocomplete siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="66546-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="66546-128">Crear un clúster del modo Swarm en Azure Container Service con ACS Engine</span><span class="sxs-lookup"><span data-stu-id="66546-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="66546-129">Conectar con el clúster de conjunto de hello en el servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="66546-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="66546-130">Crear una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="66546-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="66546-131">Crear una cuenta y un proyecto de equipo de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="66546-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="66546-132">Bifurcar hello GitHub repositorio tooyour cuenta de GitHub</span><span class="sxs-lookup"><span data-stu-id="66546-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="66546-133">Hola Docker Swarm orchestrator en el servicio de contenedor de Azure utiliza la independiente heredado conjunto.</span><span class="sxs-lookup"><span data-stu-id="66546-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="66546-134">Actualmente, Hola integrado [modo conjunto](https://docs.docker.com/engine/swarm/) (en Docker 1.12 y versiones posteriores) no es un orchestrator admitido en el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="66546-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="66546-135">Por esta razón, estamos utilizando [motor ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), han contribuido una comunidad [plantilla de inicio rápido](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), o una solución de Docker en hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="66546-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="66546-136">Paso 1: Configuración de la cuenta de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="66546-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="66546-137">En esta sección, configurará su cuenta de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="66546-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="66546-138">Extremos de los servicios de VSTS tooconfigure, en el proyecto de Visual Studio Team Services, haga clic en hello **configuración** icono en la barra de herramientas de Hola y seleccione **Services**.</span><span class="sxs-lookup"><span data-stu-id="66546-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Abrir punto de conexión de servicios](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="66546-140">Conexión de Visual Studio Team Services y una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="66546-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="66546-141">Configure una conexión entre el proyecto de VSTS y su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="66546-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="66546-142">Hola izquierda, haga clic en **nuevo extremo de servicio** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="66546-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="66546-143">tooauthorize VSTS toowork con su cuenta de Azure, seleccione su **suscripción** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="66546-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services: autorización a Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="66546-145">Conexión de Visual Studio Team Services y GitHub</span><span class="sxs-lookup"><span data-stu-id="66546-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="66546-146">Configure una conexión entre el proyecto de VSTS y su cuenta de GitHub.</span><span class="sxs-lookup"><span data-stu-id="66546-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="66546-147">Hola izquierda, haga clic en **nuevo extremo de servicio** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="66546-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="66546-148">Haga clic en tooauthorize VSTS toowork con su cuenta de GitHub, **Authorize** y siga el procedimiento de hello en la ventana de Hola que se abre.</span><span class="sxs-lookup"><span data-stu-id="66546-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services: autorización a GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="66546-150">Conectar el clúster de servicio de contenedor de Azure VSTS tooyour</span><span class="sxs-lookup"><span data-stu-id="66546-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="66546-151">últimos pasos de Hello antes de obtener en la canalización de CI/CD Hola son tooconfigure conexiones externas tooyour Docker Swarm con clústeres en Azure.</span><span class="sxs-lookup"><span data-stu-id="66546-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="66546-152">Para clúster Docker Swarm hello, agregue un punto de conexión de tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="66546-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="66546-153">A continuación, escriba la información de conexión de SSH de Hola de su clúster de conjunto (nodo maestro).</span><span class="sxs-lookup"><span data-stu-id="66546-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services: SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="66546-155">Toda la configuración de Hola se realiza ahora.</span><span class="sxs-lookup"><span data-stu-id="66546-155">All hello configuration is done now.</span></span> <span data-ttu-id="66546-156">En pasos de hello, crear canalización de CI/CD de Hola que crea e implementa el clúster de Docker Swarm de hello application toohello.</span><span class="sxs-lookup"><span data-stu-id="66546-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="66546-157">Paso 2: Crear la definición de compilación de Hola</span><span class="sxs-lookup"><span data-stu-id="66546-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="66546-158">En este paso, debe configura una definición de compilación para el proyecto VSTS y definir flujo de trabajo de compilación de Hola para las imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="66546-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="66546-159">Configuración de la definición inicial</span><span class="sxs-lookup"><span data-stu-id="66546-159">Initial definition setup</span></span>

1. <span data-ttu-id="66546-160">toocreate una definición de compilación, conectar tooyour del proyecto de Visual Studio Team Services y haga clic en **de compilación y la versión**.</span><span class="sxs-lookup"><span data-stu-id="66546-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="66546-161">Hola **las definiciones de compilación** sección, haga clic en **+ nuevo**.</span><span class="sxs-lookup"><span data-stu-id="66546-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services: definición de nueva compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="66546-163">Seleccione hello **proceso vacío**.</span><span class="sxs-lookup"><span data-stu-id="66546-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services: nueva definición de compilación vacía](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="66546-165">A continuación, haga clic en hello **Variables** pestaña y cree dos nuevas variables: **RegistryURL** y **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="66546-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="66546-166">Pegue los valores de hello de su registro y DNS de agentes de clúster.</span><span class="sxs-lookup"><span data-stu-id="66546-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services configuración de variables de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="66546-168">En hello **definiciones de compilación** página, abra hello **desencadenadores** pestaña y configurar la integración continua de hello compilación toouse con bifurcar Hola del proyecto de MyShop Hola que creó en los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="66546-169">Luego, seleccione **Cambios del lote**.</span><span class="sxs-lookup"><span data-stu-id="66546-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="66546-170">Asegúrese de que selecciona *linux docker* como hello **bifurcar especificación**.</span><span class="sxs-lookup"><span data-stu-id="66546-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services: configuración del repositorio de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="66546-172">Por último, haga clic en hello **opciones** y a configurar cola Hola predeterminada del agente demasiado**vista previa de Linux hospedadas**.</span><span class="sxs-lookup"><span data-stu-id="66546-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services: configuración del agente de host](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="66546-174">Definir el flujo de trabajo de compilación de Hola</span><span class="sxs-lookup"><span data-stu-id="66546-174">Define hello build workflow</span></span>
<span data-ttu-id="66546-175">pasos de Hello definen flujo de trabajo de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="66546-176">En primer lugar, necesita tooconfigure Hola origen del código de hello.</span><span class="sxs-lookup"><span data-stu-id="66546-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="66546-177">toodo él, seleccione **GitHub** y su **repositorio** y **bifurcación** (docker-linux).</span><span class="sxs-lookup"><span data-stu-id="66546-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services: configurar origen del código](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="66546-179">Hay cinco toobuild de imágenes de contenedor para hello *MyShop* aplicación.</span><span class="sxs-lookup"><span data-stu-id="66546-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="66546-180">Cada imagen se basa en hello que dockerfile ubicado en carpetas de proyecto de hello:</span><span class="sxs-lookup"><span data-stu-id="66546-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="66546-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="66546-181">ProductsApi</span></span>
* <span data-ttu-id="66546-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="66546-182">Proxy</span></span>
* <span data-ttu-id="66546-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="66546-183">RatingsApi</span></span>
* <span data-ttu-id="66546-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="66546-184">RecommandationsApi</span></span>
* <span data-ttu-id="66546-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="66546-185">ShopFront</span></span>

<span data-ttu-id="66546-186">Necesita dos pasos de Docker para cada imagen, una imagen de hello toobuild y una imagen de hello toopush en el registro de hello contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="66546-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="66546-187">Haga clic en un paso en el flujo de trabajo de compilación de hello, tooadd **+ agregar el paso de compilación** y seleccione **Docker**.</span><span class="sxs-lookup"><span data-stu-id="66546-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services: adición de pasos de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="66546-189">Para cada imagen, configure un paso que usa hello `docker build` comando.</span><span class="sxs-lookup"><span data-stu-id="66546-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services: compilación de Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="66546-191">Operación de compilación para hello, seleccione el registro de contenedor de Azure, hello **crear una imagen** hello Dockerfile que define cada imagen y acción.</span><span class="sxs-lookup"><span data-stu-id="66546-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="66546-192">Hola de conjunto **Working Directory** como directorio raíz de hello Dockerfile, definir hello **nombre de la imagen**y seleccione **etiqueta más reciente Include**.</span><span class="sxs-lookup"><span data-stu-id="66546-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="66546-193">Nombre de la imagen de Hello tiene toobe en este formato: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="66546-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="66546-194">Reemplace **[NAME]** con el nombre de la imagen de hello:</span><span class="sxs-lookup"><span data-stu-id="66546-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="66546-195">Para cada imagen, configurar un segundo paso que usa hello `docker push` comando.</span><span class="sxs-lookup"><span data-stu-id="66546-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services: inserción de Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="66546-197">Para la operación de inserción de hello, seleccione el registro de contenedor de Azure, hello **insertar una imagen** acción, escriba Hola **nombre de la imagen** que está integrado en el paso anterior de Hola y seleccione **incluir la etiqueta más reciente** .</span><span class="sxs-lookup"><span data-stu-id="66546-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="66546-198">Después de configurar compilación hello e insertar pasos para cada una de las imágenes de cinco Hola, agregar que flujo de trabajo de generación de tres pasos más en Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services: adición de una tarea de la línea de comandos](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="66546-200">Una tarea de línea de comandos que usa un Hola de bash script tooreplace *RegistryURL* aparición en el archivo de docker compose.yml de hello con variable de RegistryURL Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services: actualización del archivo de Compose con la URL del Registro](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="66546-202">Una tarea de línea de comandos que usa un Hola de bash script tooreplace *AgentURL* aparición en el archivo de docker compose.yml de hello con variable de AgentURL Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="66546-203">Una tarea que quita Hola actualiza redactar archivo como un artefacto de compilación para que se puedan utilizar en la versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="66546-204">Vea Hola después de la pantalla para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="66546-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services: publicación de artefacto](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services: publicación del archivo de Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="66546-207">Haga clic en **Guardar & cola** tootest la definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="66546-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services: guardar y poner en cola](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services: nueva cola](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="66546-210">Si hello **generar** es correcta, deberá toosee esta pantalla:</span><span class="sxs-lookup"><span data-stu-id="66546-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services: compilación correcta](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="66546-212">Paso 3: Crear definición de la versión de Hola</span><span class="sxs-lookup"><span data-stu-id="66546-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="66546-213">Visual Studio Team Services le permite demasiado[administrar versiones a través de entornos](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="66546-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="66546-214">Puede habilitar la implementación continua toomake seguro de que la aplicación se implementa en los entornos diferentes (por ejemplo, desarrollo, prueba, el entorno de preproducción y producción) en una forma sencilla.</span><span class="sxs-lookup"><span data-stu-id="66546-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="66546-215">Puede crear un entorno que represente el clúster del modo Docker Swarm de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="66546-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - versión tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="66546-217">Configuración inicial de la versión.</span><span class="sxs-lookup"><span data-stu-id="66546-217">Initial release setup</span></span>

1. <span data-ttu-id="66546-218">toocreate una definición de la versión, haga clic en **versiones** > **+ de la versión**</span><span class="sxs-lookup"><span data-stu-id="66546-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="66546-219">origen de artefacto de hello tooconfigure, haga clic en **artefactos** > **vincular un origen de artefacto**.</span><span class="sxs-lookup"><span data-stu-id="66546-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="66546-220">A continuación, vincular esta nueva compilación de toohello de definición de versión que ha definido en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="66546-221">Después de eso, el archivo de docker compose.yml de hello está disponible en el proceso de lanzamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services: artefactos de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="66546-223">desencadenador de versión de hello tooconfigure, haga clic en **desencadenadores** y seleccione **implementación continua**.</span><span class="sxs-lookup"><span data-stu-id="66546-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="66546-224">Los desencadenadores de Hola de conjunto de Hola mismo origen de artefacto.</span><span class="sxs-lookup"><span data-stu-id="66546-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="66546-225">Este valor garantiza que una nueva versión se inicia cuando se complete correctamente la compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services: desencadenadores de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="66546-227">las variables de la versión de Hola del tooconfigure, haga clic en **Variables** y seleccione **+ Variable** toocreate tres nuevas variables con información de hello del registro de hello: **docker.username**, **docker.password**, y **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="66546-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="66546-228">Pegue los valores de hello de su registro y DNS de agentes de clúster.</span><span class="sxs-lookup"><span data-stu-id="66546-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services: configuración del repositorio de compilación](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="66546-230">Como se muestra en la pantalla de bienvenida anterior, haga clic en hello **bloqueo** checkbox en docker.password.</span><span class="sxs-lookup"><span data-stu-id="66546-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="66546-231">Esta configuración es la contraseña de Hola de toorestrict importante.</span><span class="sxs-lookup"><span data-stu-id="66546-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="66546-232">Definir el flujo de trabajo de hello versión</span><span class="sxs-lookup"><span data-stu-id="66546-232">Define hello release workflow</span></span>

<span data-ttu-id="66546-233">flujo de trabajo de Hello versión se compone de dos tareas que agregue.</span><span class="sxs-lookup"><span data-stu-id="66546-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="66546-234">Configurar un Hola de copia de tarea toosecurely crear archivo tooa *implementar* carpeta hello Docker Swarm nodo maestro, mediante conexión de SSH de Hola que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66546-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="66546-235">Vea Hola después de la pantalla para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="66546-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="66546-236">Carpeta de origen:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="66546-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services: SCP de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="66546-238">Configurar un segundo tooexecute de tarea un toorun de comandos de bash `docker` y `docker stack deploy` comandos en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="66546-239">Vea Hola después de la pantalla para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="66546-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services: bash de versión](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="66546-241">comando de Hello ejecutado en el maestro de hello usa Hola CLI de Docker y Hola Hola de toodo de CLI de Docker Compose siguiente las tareas:</span><span class="sxs-lookup"><span data-stu-id="66546-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="66546-242">Inicie sesión en el registro de contenedor de Azure toohello (utiliza tres variables de compilación que se definen en hello **Variables** ficha)</span><span class="sxs-lookup"><span data-stu-id="66546-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="66546-243">Definir hello **DOCKER_HOST** toowork variable con el punto de conexión de hello conjunto (: 2375)</span><span class="sxs-lookup"><span data-stu-id="66546-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="66546-244">Navegue toohello *implementar* carpeta Hola delante de la tarea de copia de seguridad que creó y que contiene el archivo de hello compose.yml docker</span><span class="sxs-lookup"><span data-stu-id="66546-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="66546-245">Ejecutar `docker stack deploy` comandos que extracción nuevas imágenes de Hola y crean contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="66546-246">Como se muestra en la pantalla de bienvenida anterior, deje hello **producirá un error en STDERR** casilla desactivada.</span><span class="sxs-lookup"><span data-stu-id="66546-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="66546-247">Esta opción permite que nos toocomplete Hola versión de vencimiento del proceso demasiado`docker-compose` imprime varios mensajes de diagnóstico, como los contenedores son deteniéndose o eliminando, en la salida de error estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="66546-248">Si activa la casilla de verificación de Hola, Visual Studio Team Services informa de que se producen errores durante la versión de hello, incluso si todo funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="66546-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="66546-249">Guarde esta nueva definición de versión.</span><span class="sxs-lookup"><span data-stu-id="66546-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="66546-250">Paso 4: Probar la canalización de CI/CD Hola</span><span class="sxs-lookup"><span data-stu-id="66546-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="66546-251">Ahora que ha terminado con la configuración de hello, es hora tootest esta nueva canalización de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="66546-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="66546-252">Hola tootest de manera más sencilla es tooupdate Hola origen código y confirmación Hola cambia en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="66546-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="66546-253">Unos pocos segundos después de insertar código de hello, verá una nueva compilación que se ejecuta en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="66546-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="66546-254">Una vez completada correctamente, una nueva versión se desencadena e implementa la nueva versión de hello de la aplicación hello en clúster del servicio de contenedor de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="66546-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66546-255">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66546-255">Next steps</span></span>

* <span data-ttu-id="66546-256">Para obtener más información acerca de elementos de configuración/CD con Visual Studio Team Services, vea hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="66546-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="66546-257">Para obtener más información sobre el motor de ACS, vea hello [repositorio de GitHub de motor de ACS](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="66546-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="66546-258">Para obtener más información acerca del modo de Docker Swarm, vea hello [Docker Swarm información general de modo](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="66546-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
