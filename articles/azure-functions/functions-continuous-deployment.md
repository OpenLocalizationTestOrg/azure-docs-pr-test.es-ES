---
title: "implementación de aaaContinuous para las funciones de Azure | Documentos de Microsoft"
description: "Utilizar servicios de implementación continua del servicio de aplicaciones de Azure toopublish las funciones de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="39704-103">Implementación continua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="39704-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="39704-104">Las funciones de Azure hace fácil toodeploy la aplicación de función mediante la integración continua de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="39704-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="39704-105">Functions se integra con BitBucket, Dropbox, GitHub y Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="39704-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="39704-106">Esto permite que un flujo de trabajo que actualiza el código de la función realizada mediante uno de estos tooAzure de implementación del desencadenador de servicios integrados.</span><span class="sxs-lookup"><span data-stu-id="39704-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="39704-107">Si son nuevas funciones de tooAzure, comience con [información general de las funciones de Azure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39704-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="39704-108">La implementación continua representa una buena opción para los proyectos donde se integran contribuciones diversas y frecuentes.</span><span class="sxs-lookup"><span data-stu-id="39704-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="39704-109">También le permite mantener el control de código fuente en el código de las funciones.</span><span class="sxs-lookup"><span data-stu-id="39704-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="39704-110">actualmente se admite Hola siguientes orígenes de implementación:</span><span class="sxs-lookup"><span data-stu-id="39704-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="39704-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="39704-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="39704-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="39704-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="39704-113">Repositorio externo (Git o Mercurial)</span><span class="sxs-lookup"><span data-stu-id="39704-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="39704-114">Repositorio local de GIT</span><span class="sxs-lookup"><span data-stu-id="39704-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="39704-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="39704-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="39704-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="39704-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="39704-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="39704-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="39704-118">Las implementaciones se configuran por Function App.</span><span class="sxs-lookup"><span data-stu-id="39704-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="39704-119">Después de habilita la implementación continua, código de acceso toofunction en el portal de Hola se establece demasiado*de sólo lectura*.</span><span class="sxs-lookup"><span data-stu-id="39704-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="39704-120">Requisitos de implementación continua</span><span class="sxs-lookup"><span data-stu-id="39704-120">Continuous deployment requirements</span></span>

<span data-ttu-id="39704-121">Debe tener configurado el origen de la implementación y el código de las funciones en el origen de la implementación de hello antes de configurar la implementación continua.</span><span class="sxs-lookup"><span data-stu-id="39704-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="39704-122">En una implementación de aplicación de la función especificada, cada función reside en un subdirectorio con nombre, donde el nombre del directorio de hello es nombre Hola de función hello.</span><span class="sxs-lookup"><span data-stu-id="39704-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="39704-123">Configurar la implementación continua</span><span class="sxs-lookup"><span data-stu-id="39704-123">Set up continuous deployment</span></span>
<span data-ttu-id="39704-124">Utilice este procedimiento tooconfigure la implementación continua para una aplicación de función existente.</span><span class="sxs-lookup"><span data-stu-id="39704-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="39704-125">Estos pasos muestran la integración con un repositorio de GitHub, aunque se aplican pasos similares para Visual Studio Team Services u otros servicios de implementación.</span><span class="sxs-lookup"><span data-stu-id="39704-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="39704-126">En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **opciones de implementación**.</span><span class="sxs-lookup"><span data-stu-id="39704-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="39704-128">A continuación, en hello **implementaciones** hoja haga clic en **el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="39704-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="39704-130">Hola **origen de la implementación** hoja, haga clic en **Elegir origen**, a continuación, rellene la información de hello para el origen de implementación elegido y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="39704-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Elegir origen de la implementación](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="39704-132">Después de configura una implementación continua, todos los cambios de archivo en el origen de implementación son copiados toohello función aplicación y se desencadena una implementación completa.</span><span class="sxs-lookup"><span data-stu-id="39704-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="39704-133">Cuando se actualizan los archivos de origen de hello, sitio Hola se vuelve a implementar.</span><span class="sxs-lookup"><span data-stu-id="39704-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="39704-134">Opciones de implementación</span><span class="sxs-lookup"><span data-stu-id="39704-134">Deployment options</span></span>

<span data-ttu-id="39704-135">siguiente Hola se muestran algunos escenarios típicos de implementación:</span><span class="sxs-lookup"><span data-stu-id="39704-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="39704-136">Creación de una implementación de ensayo</span><span class="sxs-lookup"><span data-stu-id="39704-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="39704-137">Mover la implementación de toocontinuous de funciones existente</span><span class="sxs-lookup"><span data-stu-id="39704-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="39704-138">Creación de una implementación de ensayo</span><span class="sxs-lookup"><span data-stu-id="39704-138">Create a staging deployment</span></span>

<span data-ttu-id="39704-139">Las aplicaciones de función todavía no admiten espacios de implementación.</span><span class="sxs-lookup"><span data-stu-id="39704-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="39704-140">Sin embargo, todavía puede administrar implementaciones de ensayo y producción independientes mediante la integración continua.</span><span class="sxs-lookup"><span data-stu-id="39704-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="39704-141">Hola tooconfigure de proceso y trabajar con una implementación de ensayo generalmente es similar a esto:</span><span class="sxs-lookup"><span data-stu-id="39704-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="39704-142">Cree dos aplicaciones en función de su suscripción, uno para el código de producción de hello y otro para el almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="39704-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="39704-143">Cree un origen de la implementación, si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="39704-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="39704-144">En este ejemplo se usa [GitHub].</span><span class="sxs-lookup"><span data-stu-id="39704-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="39704-145">Para la aplicación de función de producción, los pasos de hello completa anterior **configurar la implementación continua** y conjunto Hola implementación bifurcación toohello bifurcación principal de su repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="39704-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Elegir rama de la implementación](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="39704-147">Repita este paso para la aplicación de la función de almacenamiento provisional de Hola, pero elija Hola rama de ensayo en su lugar en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="39704-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="39704-148">Si el origen de la implementación no admite la bifurcación, utilice una carpeta diferente.</span><span class="sxs-lookup"><span data-stu-id="39704-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="39704-149">Realizar actualizaciones tooyour código de hello bifurcación o carpeta de almacenamiento provisional, a continuación, comprobar que esos cambios se reflejan en la implementación de ensayo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39704-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="39704-150">Después de probar, combinar los cambios de bifurcación de almacenamiento provisional de hello en la bifurcación principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="39704-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="39704-151">Esta combinación desencadenadores toohello producción función aplicación de la implementación.</span><span class="sxs-lookup"><span data-stu-id="39704-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="39704-152">Si el origen de la implementación no es compatible con bifurcaciones, sobrescriba los archivos de hello en la carpeta de producción de hello con archivos de Hola de Hola carpeta de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="39704-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="39704-153">Mover la implementación de toocontinuous de funciones existente</span><span class="sxs-lookup"><span data-stu-id="39704-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="39704-154">Cuando tenga las funciones existentes que ha creado y mantiene en el portal de hello, necesita toodownload sus función archivos de código mediante FTP o hello repositorio Git local para poder configurar la implementación continua como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="39704-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="39704-155">Para hacer esto en hello configuración de servicio de aplicaciones para la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="39704-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="39704-156">Después de descargan los archivos, puede cargarlos de origen de la implementación continua de tooyour elegido.</span><span class="sxs-lookup"><span data-stu-id="39704-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="39704-157">Después de configurar la integración continua, ya no será capaz de tooedit el origen de los archivos en el portal de funciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="39704-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="39704-158">Configuración de las credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="39704-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="39704-159">Descarga de archivos mediante FTP</span><span class="sxs-lookup"><span data-stu-id="39704-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="39704-160">Cómo: descargar archivos mediante el repositorio de Git local Hola</span><span class="sxs-lookup"><span data-stu-id="39704-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="39704-161">Configuración de las credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="39704-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="39704-162">Para poder descargar archivos desde la aplicación de la función con FTP o en el repositorio de Git local, debe configurar el sitio de hello tooaccess de credenciales.</span><span class="sxs-lookup"><span data-stu-id="39704-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="39704-163">Las credenciales se establecen en el nivel de aplicación de función hello.</span><span class="sxs-lookup"><span data-stu-id="39704-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="39704-164">Use Hola siguientes pasos le indican las credenciales de la implementación de tooset Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="39704-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="39704-165">En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **las credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="39704-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Configurar credenciales de implementación locales](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="39704-167">Escriba un nombre de usuario y una contraseña y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="39704-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="39704-168">Ahora puede usar estos tooaccess las credenciales de la aplicación de la función de FTP o hello repositorio Git integrado.</span><span class="sxs-lookup"><span data-stu-id="39704-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="39704-169">Descarga de archivos mediante FTP</span><span class="sxs-lookup"><span data-stu-id="39704-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="39704-170">En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **propiedades**, a continuación, copie los valores de hello para **FTP/implementación usuario**, **Nombre de Host FTP**, y **nombre de Host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="39704-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="39704-171">**Usuario de implementación/FTP** debe especificarse como se muestra en el portal de hello, incluidos el nombre de la aplicación hello, tooprovide contexto adecuado para el servidor FTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="39704-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Obtener la información de implementación](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="39704-173">Desde el cliente FTP, use información de conexión de Hola que recopiló tooconnect tooyour aplicación y descargar archivos de origen de Hola para sus funciones.</span><span class="sxs-lookup"><span data-stu-id="39704-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="39704-174">Descarga de archivos mediante el repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="39704-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="39704-175">En la aplicación de la función en hello [portal de Azure](https://portal.azure.com), haga clic en **características de la plataforma** y **opciones de implementación**.</span><span class="sxs-lookup"><span data-stu-id="39704-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="39704-177">A continuación, en hello **implementaciones** hoja haga clic en **el programa de instalación**.</span><span class="sxs-lookup"><span data-stu-id="39704-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="39704-179">Hola **origen de la implementación** hoja, haga clic en **repositorio de Git Local** y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="39704-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="39704-180">En **características de la plataforma**, haga clic en **propiedades** y anote el valor de Hola de dirección URL de Git.</span><span class="sxs-lookup"><span data-stu-id="39704-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="39704-182">Clonar el repositorio de hello en el equipo local mediante un símbolo del sistema compatible con Git o su herramienta preferida de Git.</span><span class="sxs-lookup"><span data-stu-id="39704-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="39704-183">comando de clonación de Git Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="39704-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="39704-184">Capturar los archivos de su clonación toohello de aplicación de función en el equipo local, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="39704-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="39704-185">Si se le piden, proporcione las [credenciales de implementación configuradas](#credentials).</span><span class="sxs-lookup"><span data-stu-id="39704-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
