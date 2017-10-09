---
title: aaaCI/CD con conjunto y el servicio de contenedor de Azure | Documentos de Microsoft
description: "Usar el servicio de contenedor de Azure con Docker Swarm, un registro de contenedor de Azure y Visual Studio Team Services toodeliver continuamente una aplicación de .NET Core contenedor múltiples"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Swarm, Azure, Visual Studio Team Services, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="4254d-104">Total de elementos de configuración/CD canalización toodeploy una aplicación de contenedor múltiples en el servicio de contenedor de Azure con Docker Swarm con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4254d-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="4254d-105">Uno de Hola mayores desafíos cuando desarrollo de aplicaciones modernas de nube de Hola se toodeliver capaz de estas aplicaciones continuamente.</span><span class="sxs-lookup"><span data-stu-id="4254d-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="4254d-106">En este artículo, obtenga información acerca de cómo crear tooimplement una integración completa continua y la canalización de implementación (CI/CD) con el servicio de contenedor de Azure con Docker Swarm, registro de contenedor de Azure y Visual Studio Team Services y administración de versiones.</span><span class="sxs-lookup"><span data-stu-id="4254d-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="4254d-107">Este artículo se basa en una aplicación sencilla, disponible en [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), desarrollada con ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4254d-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="4254d-108">aplicación Hello se compone de cuatro servicios diferentes: tres web API y front-end uno web:</span><span class="sxs-lookup"><span data-stu-id="4254d-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="4254d-110">el objetivo de Hello es toodeliver esta aplicación continuamente en un clúster de Docker Swarm, mediante Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4254d-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="4254d-111">Hola siguiente ilustración, detalles de esta canalización de la entrega continua:</span><span class="sxs-lookup"><span data-stu-id="4254d-111">hello following figure details this continuous delivery pipeline:</span></span>

![Aplicación de ejemplo MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="4254d-113">Aquí es una breve explicación de los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4254d-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="4254d-114">Cambios de código están confirmados toohello repositorio de código fuente (aquí, GitHub)</span><span class="sxs-lookup"><span data-stu-id="4254d-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="4254d-115">GitHub desencadena una compilación en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4254d-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="4254d-116">Visual Studio Team Services obtiene la versión más reciente de Hola de orígenes de Hola y compila todas las imágenes de Hola que componen la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="4254d-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="4254d-117">Visual Studio Team Services inserta cada registro de Docker de tooa imágenes creado con el servicio de registro de contenedor de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="4254d-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="4254d-118">Visual Studio Team Services desencadena una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="4254d-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="4254d-119">versión de Hola ejecuta algunos comandos mediante SSH en el nodo principal del clúster de servicio de hello contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="4254d-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="4254d-120">Conjunto de docker en hello clúster extrae Hola versión más reciente de imágenes de Hola</span><span class="sxs-lookup"><span data-stu-id="4254d-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="4254d-121">nueva versión de la aplicación hello de Hola se implementa con Docker Compose</span><span class="sxs-lookup"><span data-stu-id="4254d-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4254d-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4254d-122">Prerequisites</span></span>

<span data-ttu-id="4254d-123">Antes de iniciar este tutorial, necesita hello toocomplete siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="4254d-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="4254d-124">Crear un clúster de Swarm en Azure Container Service (servicio Contenedor de Azure)</span><span class="sxs-lookup"><span data-stu-id="4254d-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="4254d-125">Conectar con el clúster de conjunto de hello en el servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="4254d-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="4254d-126">Crear una instancia de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="4254d-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="4254d-127">Crear una cuenta y un proyecto de equipo de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4254d-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="4254d-128">Bifurcar hello GitHub repositorio tooyour cuenta de GitHub</span><span class="sxs-lookup"><span data-stu-id="4254d-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="4254d-129">También se necesita una máquina Ubuntu (14.04 o 16.04) que tenga instalado Docker.</span><span class="sxs-lookup"><span data-stu-id="4254d-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="4254d-130">Este equipo se utiliza Visual Studio Team Services durante Hola compilar y procesos de la versión.</span><span class="sxs-lookup"><span data-stu-id="4254d-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="4254d-131">Una manera de toocreate esta máquina es la imagen de hello toouse disponible en hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="4254d-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="4254d-132">Paso 1: Configuración de la cuenta de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4254d-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="4254d-133">En esta sección, configurará su cuenta de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4254d-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="4254d-134">Configuración de un agente de compilación de Linux de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4254d-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="4254d-135">imágenes de Docker toocreate e inserción que generación estas imágenes en un registro de contenedor de Azure desde un Visual Studio Team Services, deberá tooregister un agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="4254d-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="4254d-136">Dispone de estas opciones de instalación:</span><span class="sxs-lookup"><span data-stu-id="4254d-136">You have these installation options:</span></span>

* [<span data-ttu-id="4254d-137">Implementar un agente en Linux</span><span class="sxs-lookup"><span data-stu-id="4254d-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="4254d-138">Usar el agente de Docker toorun Hola VSTS</span><span class="sxs-lookup"><span data-stu-id="4254d-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="4254d-139">Instalar extensión de Docker integración VSTS Hola</span><span class="sxs-lookup"><span data-stu-id="4254d-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="4254d-140">Microsoft proporciona una extensión VSTS toowork con Docker en la compilación y la versión de procesos.</span><span class="sxs-lookup"><span data-stu-id="4254d-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="4254d-141">Esta extensión está disponible en hello [Marketplace de VSTS](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="4254d-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="4254d-142">Haga clic en **instalar** tooadd esta cuenta VSTS tooyour de extensión:</span><span class="sxs-lookup"><span data-stu-id="4254d-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Instalar Hola integración del Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="4254d-144">Se le preguntará la cuenta VSTS tooyour tooconnect con sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="4254d-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="4254d-145">Conexión de Visual Studio Team Services y GitHub</span><span class="sxs-lookup"><span data-stu-id="4254d-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="4254d-146">Configure una conexión entre el proyecto de VSTS y su cuenta de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4254d-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="4254d-147">En el proyecto de Visual Studio Team Services, haga clic en hello **configuración** icono en la barra de herramientas de Hola y seleccione **Services**.</span><span class="sxs-lookup"><span data-stu-id="4254d-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services: conexión externa](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="4254d-149">Hola izquierda, haga clic en **nuevo extremo de servicio** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="4254d-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services: GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="4254d-151">Haga clic en tooauthorize VSTS toowork con su cuenta de GitHub, **Authorize** y siga el procedimiento de hello en la ventana de Hola que se abre.</span><span class="sxs-lookup"><span data-stu-id="4254d-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services: autorización a GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="4254d-153">Conectar del registro VSTS tooyour contenedor de Azure y Azure contenedor servicio de cluster Server</span><span class="sxs-lookup"><span data-stu-id="4254d-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="4254d-154">últimos pasos de Hello antes de obtener en la canalización de CI/CD Hola son del registro de tooconfigure conexiones externas tooyour contenedor y el clúster Docker Swarm en Azure.</span><span class="sxs-lookup"><span data-stu-id="4254d-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="4254d-155">Hola **servicios** la configuración del proyecto de Visual Studio Team Services, agrega un extremo de servicio de tipo **Docker registro**.</span><span class="sxs-lookup"><span data-stu-id="4254d-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="4254d-156">En la ventana emergente de Hola que se abre, escriba Hola URL y las credenciales de Hola de seguridad del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="4254d-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services: Docker Registry](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="4254d-158">Para clúster Docker Swarm hello, agregue un punto de conexión de tipo **SSH**.</span><span class="sxs-lookup"><span data-stu-id="4254d-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="4254d-159">A continuación, escriba la información de conexión de SSH de Hola de su clúster de conjunto.</span><span class="sxs-lookup"><span data-stu-id="4254d-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services: SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="4254d-161">Toda la configuración de Hola se realiza ahora.</span><span class="sxs-lookup"><span data-stu-id="4254d-161">All hello configuration is done now.</span></span> <span data-ttu-id="4254d-162">En pasos de hello, crear canalización de CI/CD de Hola que crea e implementa el clúster de Docker Swarm de hello application toohello.</span><span class="sxs-lookup"><span data-stu-id="4254d-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="4254d-163">Paso 2: Crear la definición de compilación de Hola</span><span class="sxs-lookup"><span data-stu-id="4254d-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="4254d-164">En este paso, debe configurar una definitionfor de compilación del proyecto VSTS y definir flujo de trabajo de compilación de Hola para las imágenes de contenedor</span><span class="sxs-lookup"><span data-stu-id="4254d-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="4254d-165">Configuración de la definición inicial</span><span class="sxs-lookup"><span data-stu-id="4254d-165">Initial definition setup</span></span>

1. <span data-ttu-id="4254d-166">toocreate una definición de compilación, conectar tooyour del proyecto de Visual Studio Team Services y haga clic en **de compilación y la versión**.</span><span class="sxs-lookup"><span data-stu-id="4254d-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="4254d-167">Hola **las definiciones de compilación** sección, haga clic en **+ nuevo**.</span><span class="sxs-lookup"><span data-stu-id="4254d-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="4254d-168">Seleccione hello **vacía** plantilla.</span><span class="sxs-lookup"><span data-stu-id="4254d-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services: definición de nueva compilación](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="4254d-170">Configurar la nueva compilación de hello con un origen de repositorio de GitHub, verificación **integración continua**y seleccione Hola agente cola que se ha registrado el agente de Linux.</span><span class="sxs-lookup"><span data-stu-id="4254d-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="4254d-171">Haga clic en **crear** toocreate Hola definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="4254d-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services: creación de la definición de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="4254d-173">En hello **definiciones de compilación** página, primero abra hello **repositorio** pestaña y configurar la bifurcación de Hola de hello compilación toouse del proyecto de MyShop Hola que creó en los requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="4254d-174">Asegúrese de que selecciona *acs documentos* como hello **rama predeterminada**.</span><span class="sxs-lookup"><span data-stu-id="4254d-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services: configuración del repositorio de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="4254d-176">En hello **desencadenadores** pestaña, configure Hola compilación toobe desencadena después de cada confirmación.</span><span class="sxs-lookup"><span data-stu-id="4254d-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="4254d-177">Seleccione **Integración continua** y **Batch changes** (Cambios en lote).</span><span class="sxs-lookup"><span data-stu-id="4254d-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services: configuración del desencadenador de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="4254d-179">Definir el flujo de trabajo de compilación de Hola</span><span class="sxs-lookup"><span data-stu-id="4254d-179">Define hello build workflow</span></span>
<span data-ttu-id="4254d-180">pasos de Hello definen flujo de trabajo de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="4254d-181">Hay cinco toobuild de imágenes de contenedor para hello *MyShop* aplicación.</span><span class="sxs-lookup"><span data-stu-id="4254d-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="4254d-182">Cada imagen se basa en hello que dockerfile ubicado en carpetas de proyecto de hello:</span><span class="sxs-lookup"><span data-stu-id="4254d-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="4254d-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="4254d-183">ProductsApi</span></span>
* <span data-ttu-id="4254d-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="4254d-184">Proxy</span></span>
* <span data-ttu-id="4254d-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="4254d-185">RatingsApi</span></span>
* <span data-ttu-id="4254d-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="4254d-186">RecommandationsApi</span></span>
* <span data-ttu-id="4254d-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="4254d-187">ShopFront</span></span>

<span data-ttu-id="4254d-188">Necesita dos pasos de Docker tooadd para cada imagen, una imagen de hello toobuild y una imagen de hello toopush en el registro de contenedor de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="4254d-189">Haga clic en un paso en el flujo de trabajo de compilación de hello, tooadd **+ agregar el paso de compilación** y seleccione **Docker**.</span><span class="sxs-lookup"><span data-stu-id="4254d-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services: adición de pasos de compilación](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="4254d-191">Para cada imagen, configure un paso que usa hello `docker build` comando.</span><span class="sxs-lookup"><span data-stu-id="4254d-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services: compilación de Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="4254d-193">Operación de compilación para hello, seleccione el registro de contenedor de Azure, hello **crear una imagen** hello Dockerfile que define cada imagen y acción.</span><span class="sxs-lookup"><span data-stu-id="4254d-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="4254d-194">Conjunto hello **contexto de la creación** como hello Dockerfile directorio raíz y definir hello **nombre de la imagen**.</span><span class="sxs-lookup"><span data-stu-id="4254d-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="4254d-195">Como se muestra en hello anterior pantalla, inicie nombre de la imagen de hello con hello URI de seguridad del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="4254d-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="4254d-196">(También puede usar una etiqueta de hello tooparameterize variables de compilación de imagen de hello, como identificador de compilación de hello en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="4254d-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="4254d-197">Para cada imagen, configurar un segundo paso que usa hello `docker push` comando.</span><span class="sxs-lookup"><span data-stu-id="4254d-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services: inserción de Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="4254d-199">Para la operación de inserción de hello, seleccione el registro de contenedor de Azure, hello **insertar una imagen** acción y escriba hello **nombre de imagen** que se generó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="4254d-200">Después de configurar compilación hello e insertar pasos para cada una de las imágenes de cinco Hola, agregar que flujo de trabajo de generación de dos pasos más en Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="4254d-201">a.</span><span class="sxs-lookup"><span data-stu-id="4254d-201">a.</span></span> <span data-ttu-id="4254d-202">Una tarea de línea de comandos que usa un Hola de bash script tooreplace *BuildNumber* aparición en el archivo de docker compose.yml de hello con hello actual generar Id. Vea Hola después de la pantalla para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4254d-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services: actualización de archivo de Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="4254d-204">b.</span><span class="sxs-lookup"><span data-stu-id="4254d-204">b.</span></span> <span data-ttu-id="4254d-205">Una tarea que quita Hola actualiza redactar archivo como un artefacto de compilación para que se puedan utilizar en la versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="4254d-206">Vea Hola después de la pantalla para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4254d-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services: publicación del archivo de Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="4254d-208">Haga clic en **Guardar** y asigne un nombre a la definición de compilación.</span><span class="sxs-lookup"><span data-stu-id="4254d-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="4254d-209">Paso 3: Crear definición de la versión de Hola</span><span class="sxs-lookup"><span data-stu-id="4254d-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="4254d-210">Visual Studio Team Services le permite demasiado[administrar versiones a través de entornos](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="4254d-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="4254d-211">Puede habilitar la implementación continua toomake seguro de que la aplicación se implementa en los entornos diferentes (por ejemplo, desarrollo, prueba, el entorno de preproducción y producción) en una forma sencilla.</span><span class="sxs-lookup"><span data-stu-id="4254d-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="4254d-212">Puede crear un nuevo entorno que representa el clúster de Docker Swarm de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="4254d-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - versión tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="4254d-214">Configuración inicial de la versión.</span><span class="sxs-lookup"><span data-stu-id="4254d-214">Initial release setup</span></span>

1. <span data-ttu-id="4254d-215">toocreate una definición de la versión, haga clic en **versiones** > **+ de la versión**</span><span class="sxs-lookup"><span data-stu-id="4254d-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="4254d-216">origen de artefacto de hello tooconfigure, haga clic en **artefactos** > **vincular un origen de artefacto**.</span><span class="sxs-lookup"><span data-stu-id="4254d-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="4254d-217">A continuación, vincular esta nueva compilación de toohello de definición de versión que ha definido en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="4254d-218">Al hacerlo, el archivo de docker compose.yml de hello está disponible en proceso de lanzamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services: artefactos de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="4254d-220">desencadenador de versión de hello tooconfigure, haga clic en **desencadenadores** y seleccione **implementación continua**.</span><span class="sxs-lookup"><span data-stu-id="4254d-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="4254d-221">Los desencadenadores de Hola de conjunto de Hola mismo origen de artefacto.</span><span class="sxs-lookup"><span data-stu-id="4254d-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="4254d-222">Este valor garantiza que una nueva versión se inicia en cuanto Hola generación finalice correctamente.</span><span class="sxs-lookup"><span data-stu-id="4254d-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services: desencadenadores de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="4254d-224">Definir el flujo de trabajo de hello versión</span><span class="sxs-lookup"><span data-stu-id="4254d-224">Define hello release workflow</span></span>

<span data-ttu-id="4254d-225">flujo de trabajo de Hello versión se compone de dos tareas que agregue.</span><span class="sxs-lookup"><span data-stu-id="4254d-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="4254d-226">Configurar un Hola de copia de tarea toosecurely crear archivo tooa *implementar* carpeta hello Docker Swarm nodo maestro, mediante conexión de SSH de Hola que configuró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4254d-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="4254d-227">Vea Hola después de la pantalla para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4254d-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services: SCP de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="4254d-229">Configurar un segundo tooexecute de tarea un toorun de comandos de bash `docker` y `docker-compose` comandos en el nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="4254d-230">Vea Hola después de la pantalla para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4254d-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services: bash de versión](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="4254d-232">comando de Hello ejecutado en uso principal de Hola Hola CLI de Docker y Hola Hola de toodo de CLI de Docker Compose siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="4254d-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="4254d-233">Registro de inicio de sesión toohello contenedor de Azure (usa tres variab'les de compilación que se definen en hello **Variables** ficha)</span><span class="sxs-lookup"><span data-stu-id="4254d-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="4254d-234">Definir hello **DOCKER_HOST** toowork variable con el punto de conexión de hello conjunto (: 2375)</span><span class="sxs-lookup"><span data-stu-id="4254d-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="4254d-235">Navegue toohello *implementar* carpeta Hola delante de la tarea de copia de seguridad que creó y que contiene el archivo de hello compose.yml docker</span><span class="sxs-lookup"><span data-stu-id="4254d-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="4254d-236">Ejecutar `docker-compose` comandos que extraen nuevas imágenes de hello, detener los servicios de hello, quitar servicios de Hola y crear contenedores de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="4254d-237">Como se muestra en hello delante de la pantalla, deje hello **producirá un error en STDERR** casilla desactivada.</span><span class="sxs-lookup"><span data-stu-id="4254d-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="4254d-238">Se trata de una opción importante, porque `docker-compose` imprime varios mensajes de diagnóstico, como los contenedores son deteniéndose o eliminando, en la salida de error estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="4254d-239">Si activa la casilla de verificación de Hola, Visual Studio Team Services informa de que se producen errores durante la versión de hello, incluso si todo funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="4254d-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="4254d-240">Guarde esta nueva definición de versión.</span><span class="sxs-lookup"><span data-stu-id="4254d-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="4254d-241">Esta implementación incluye algún tiempo de inactividad porque estamos detener servicios antiguo hello y ejecuta Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="4254d-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="4254d-242">Es posible tooavoid realizando una implementación de verde azulado.</span><span class="sxs-lookup"><span data-stu-id="4254d-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="4254d-243">Paso 4</span><span class="sxs-lookup"><span data-stu-id="4254d-243">Step 4.</span></span> <span data-ttu-id="4254d-244">Probar Hola CI/CD canalización</span><span class="sxs-lookup"><span data-stu-id="4254d-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="4254d-245">Ahora que ha terminado con la configuración de hello, es hora tootest esta nueva canalización de CI/CD.</span><span class="sxs-lookup"><span data-stu-id="4254d-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="4254d-246">Hola tootest de manera más sencilla es tooupdate Hola origen código y confirmación Hola cambia en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4254d-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="4254d-247">Unos pocos segundos después de insertar código de hello, verá una nueva compilación que se ejecuta en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4254d-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="4254d-248">Una vez completada correctamente, una nueva versión se activará e implementará la nueva versión de hello de la aplicación hello en clúster del servicio de contenedor de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="4254d-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4254d-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4254d-249">Next Steps</span></span>

* <span data-ttu-id="4254d-250">Para obtener más información acerca de elementos de configuración/CD con Visual Studio Team Services, vea hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="4254d-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
