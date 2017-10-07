---
title: "aaaContinuous implementación tooAzure servicio de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable implementación continua tooAzure servicio de aplicaciones."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="3b588-103">TooAzure de implementación continua servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3b588-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="3b588-104">Este tutorial muestra cómo tooconfigure un flujo de trabajo de implementación continua para su [servicio de aplicaciones de Azure] aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b588-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="3b588-105">Integración con el servicio de aplicación con BitBucket, GitHub, y [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) permite una continua donde Azure extrae las actualizaciones más recientes de Hola desde el proyecto de flujo de trabajo de implementación publica tooone de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="3b588-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="3b588-106">La implementación continua representa una buena opción para los proyectos donde se integran contribuciones diversas y frecuentes.</span><span class="sxs-lookup"><span data-stu-id="3b588-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="3b588-107">toofind out cómo manualmente desde un repositorio de nube no aparece en una implementación continua tooconfigure Hola Portal de Azure (como [GitLab](https://gitlab.com/)), consulte [configurando la implementación continua mediante procesos manuales](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="3b588-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="3b588-108"><a name="overview"></a>Habilitación de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="3b588-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="3b588-109">implementación continua tooenable,</span><span class="sxs-lookup"><span data-stu-id="3b588-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="3b588-110">Publicar su repositorio de contenido toohello de aplicación que se usará para la implementación continuada.</span><span class="sxs-lookup"><span data-stu-id="3b588-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="3b588-111">Para obtener más información sobre cómo publicar los servicios de toothese de proyecto, vea [crear un repositorio (GitHub)], [crear un repositorio (BitBucket)], y [empezar a trabajar con VSTS].</span><span class="sxs-lookup"><span data-stu-id="3b588-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="3b588-112">En la hoja de menú de la aplicación Hola [portal de Azure], haga clic en **la implementación de aplicación > Opciones de implementación**.</span><span class="sxs-lookup"><span data-stu-id="3b588-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="3b588-113">Haga clic en **Elegir origen**, a continuación, seleccione origen de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b588-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="3b588-114">tooconfigure una cuenta VSTS de implementación de servicio de aplicaciones Vea este [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="3b588-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="3b588-115">Completar flujo de trabajo de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b588-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="3b588-116">Hola **origen de la implementación** hoja, elija el proyecto de Hola y crear una bifurcación toodeploy desde.</span><span class="sxs-lookup"><span data-stu-id="3b588-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="3b588-117">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b588-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="3b588-118">Al habilitar la implementación continua con GitHub o BitBucket, se mostrarán tanto los proyectos públicos como privados.</span><span class="sxs-lookup"><span data-stu-id="3b588-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="3b588-119">Servicio de aplicaciones crea una asociación con el repositorio seleccionado hello, extrae archivos Hola de bifurcación especificada hello y mantiene un clon del repositorio para la aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3b588-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="3b588-120">Al configurar la implementación continua de VSTS desde el portal de Azure hello, integración de hello usa Hola servicio de aplicaciones [motor de implementación de Kudu](https://github.com/projectkudu/kudu/wiki), que ya automatiza las tareas de compilación e implementación con cada `git push`.</span><span class="sxs-lookup"><span data-stu-id="3b588-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="3b588-121">No es necesario tooseparately configurar la implementación continua en VSTS.</span><span class="sxs-lookup"><span data-stu-id="3b588-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="3b588-122">Al finalizar este proceso, hello **opciones de implementación** hoja de la aplicación mostrará una implementación activa que indica que la implementación se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3b588-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="3b588-123">aplicación de hello tooverify se implementa correctamente, haga clic en hello **URL** princip Hola de hoja de la aplicación Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b588-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="3b588-124">tooverify que se está produciendo una implementación continua desde el repositorio de Hola de su elección, inserte un repositorio de toohello de cambio.</span><span class="sxs-lookup"><span data-stu-id="3b588-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="3b588-125">La aplicación debe actualizar los cambios de hello tooreflect poco después de repositorio de hello inserción toohello completa.</span><span class="sxs-lookup"><span data-stu-id="3b588-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="3b588-126">Puede comprobar que ha extraído en la actualización de Hola Hola **opciones de implementación** hoja de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b588-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="3b588-127"><a name="VSsolution"></a>Implementación continua de una solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3b588-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="3b588-128">Insertar un tooAzure de solución de Visual Studio servicio de aplicaciones es tan fácil como insertar un archivo index.html simple.</span><span class="sxs-lookup"><span data-stu-id="3b588-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="3b588-129">Hola proceso de implementación de servicio de aplicaciones optimiza todos los detalles de hello, incluida la restauración de las dependencias de NuGet y generar archivos binarios de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="3b588-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="3b588-130">Puede seguir Hola origen control los procedimientos recomendados de mantenimiento del código solo en el repositorio Git y permiten la implementación de servicio de aplicaciones tenga cuidado de rest de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b588-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="3b588-131">Hello pasos para insertar su tooApp de solución de Visual Studio son servicio Hola mismo como en hello [sección anterior](#overview), siempre que configure su solución y del repositorio como sigue:</span><span class="sxs-lookup"><span data-stu-id="3b588-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="3b588-132">Usar Hola Visual Studio origen control opción toogenerate una `.gitignore` de archivo como imagen de hello siguiente o agregar manualmente un `.gitignore` archivo en la raíz del repositorio con contenido toothis similar [.gitignore ejemplo](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="3b588-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="3b588-133">Agregar repositorio de tooyour de árbol del hello toda la solución directorio, con el archivo .sln de hello en el directorio raíz del repositorio Hola.</span><span class="sxs-lookup"><span data-stu-id="3b588-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="3b588-134">Una vez haya configurado el repositorio tal como se describe y configurado la aplicación en Azure para la publicación continua desde uno de los repositorios de Git en línea hello, puede desarrollar su aplicación de ASP.NET localmente en Visual Studio y continuamente simplemente a implementar el código Insertar el repositorio de Git cambios tooyour en línea.</span><span class="sxs-lookup"><span data-stu-id="3b588-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="3b588-135"><a name="disableCD"></a>Deshabilitación de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="3b588-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="3b588-136">implementación continua toodisable,</span><span class="sxs-lookup"><span data-stu-id="3b588-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="3b588-137">En la hoja de menú de la aplicación Hola [portal de Azure], haga clic en **la implementación de aplicación > Opciones de implementación**.</span><span class="sxs-lookup"><span data-stu-id="3b588-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="3b588-138">A continuación, haga clic en **desconexión** en hello **opciones de implementación** hoja.</span><span class="sxs-lookup"><span data-stu-id="3b588-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="3b588-139">Después de contestarse **Sí** toohello mensaje de confirmación, puede devolver la hoja de la aplicación tooyour y haga clic en **la implementación de aplicación > Opciones de implementación** si desea que tooset la publicación desde otro origen.</span><span class="sxs-lookup"><span data-stu-id="3b588-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b588-140">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3b588-140">Additional Resources</span></span>
* [<span data-ttu-id="3b588-141">¿Cómo se problemas comunes de tooinvestigate con una implementación continua</span><span class="sxs-lookup"><span data-stu-id="3b588-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="3b588-142">[¿Cómo toouse PowerShell de Azure]</span><span class="sxs-lookup"><span data-stu-id="3b588-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="3b588-143">[¿Cómo toouse Hola herramientas de línea de comandos de Azure para Mac y Linux]</span><span class="sxs-lookup"><span data-stu-id="3b588-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="3b588-144">[Documentación de Git]</span><span class="sxs-lookup"><span data-stu-id="3b588-144">[Git documentation]</span></span>
* [<span data-ttu-id="3b588-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="3b588-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="3b588-146">Usar Azure tooautomatically generar una aplicación de integración continua/CD canalización toodeploy un ASP.NET 4</span><span class="sxs-lookup"><span data-stu-id="3b588-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="3b588-147">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3b588-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3b588-148">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="3b588-148">No credit cards required; no commitments.</span></span>
> 
> 

[servicio de aplicaciones de Azure]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portal de Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[¿Cómo toouse PowerShell de Azure]: /powershell/azureps-cmdlets-docs
[¿Cómo toouse Hola herramientas de línea de comandos de Azure para Mac y Linux]:../cli-install-nodejs.md
[Documentación de Git]: http://git-scm.com/documentation

[crear un repositorio (GitHub)]: https://help.github.com/articles/create-a-repo
[crear un repositorio (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[empezar a trabajar con VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
