---
title: "Implementación continua para Azure Functions | Microsoft Docs"
description: "Utilice las funciones de implementación continua de Azure App Service para publicar Azure Functions."
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
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="3054f-103">Implementación continua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3054f-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="3054f-104">Azure Functions facilita la implementación de Function App mediante la integración continua de App Service.</span><span class="sxs-lookup"><span data-stu-id="3054f-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="3054f-105">Functions se integra con BitBucket, Dropbox, GitHub y Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="3054f-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="3054f-106">Esto permite un flujo de trabajo en el que las actualizaciones del código de la función realizadas mediante uno de estos servicios integrados desencadenan la implementación en Azure.</span><span class="sxs-lookup"><span data-stu-id="3054f-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="3054f-107">Si no está familiarizado con Azure Functions, consulte primero [Información general sobre Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3054f-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="3054f-108">La implementación continua representa una buena opción para los proyectos donde se integran contribuciones diversas y frecuentes.</span><span class="sxs-lookup"><span data-stu-id="3054f-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="3054f-109">También le permite mantener el control de código fuente en el código de las funciones.</span><span class="sxs-lookup"><span data-stu-id="3054f-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="3054f-110">Actualmente se admiten los siguientes orígenes de implementación:</span><span class="sxs-lookup"><span data-stu-id="3054f-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="3054f-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="3054f-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="3054f-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="3054f-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="3054f-113">Repositorio externo (Git o Mercurial)</span><span class="sxs-lookup"><span data-stu-id="3054f-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="3054f-114">Repositorio local de GIT</span><span class="sxs-lookup"><span data-stu-id="3054f-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="3054f-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="3054f-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="3054f-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="3054f-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="3054f-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="3054f-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="3054f-118">Las implementaciones se configuran por Function App.</span><span class="sxs-lookup"><span data-stu-id="3054f-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="3054f-119">Después de habilitada la implementación continua, el acceso al código de la función en el portal está establecido en acceso *de solo lectura*.</span><span class="sxs-lookup"><span data-stu-id="3054f-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="3054f-120">Requisitos de implementación continua</span><span class="sxs-lookup"><span data-stu-id="3054f-120">Continuous deployment requirements</span></span>

<span data-ttu-id="3054f-121">Para configurar la implementación continua debe tener configurados el origen de implementación y el código de las funciones del origen de implementación.</span><span class="sxs-lookup"><span data-stu-id="3054f-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="3054f-122">En una implementación determinada de una aplicación de función, cada función se encuentra en un subdirectorio con nombre, donde el nombre del directorio es el nombre de la función.</span><span class="sxs-lookup"><span data-stu-id="3054f-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="3054f-123">Configurar la implementación continua</span><span class="sxs-lookup"><span data-stu-id="3054f-123">Set up continuous deployment</span></span>
<span data-ttu-id="3054f-124">Use este procedimiento para configurar la implementación continua para una Function App existente.</span><span class="sxs-lookup"><span data-stu-id="3054f-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="3054f-125">Estos pasos muestran la integración con un repositorio de GitHub, aunque se aplican pasos similares para Visual Studio Team Services u otros servicios de implementación.</span><span class="sxs-lookup"><span data-stu-id="3054f-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="3054f-126">En la Function App de [Azure Portal](https://portal.azure.com), haga clic en **Características de la plataforma** y en **Opciones de implementación**.</span><span class="sxs-lookup"><span data-stu-id="3054f-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="3054f-128">Luego, en la hoja **Implementación**, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="3054f-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="3054f-130">En la hoja **Origen de implementación**, haga clic en **Elegir origen**, rellene la información del origen de implementación elegido y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3054f-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Elegir origen de la implementación](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="3054f-132">Después de configurar la implementación continua, se copian todos los cambios de archivos del origen de implementación en la Function App y se desencadena una implementación completa del sitio.</span><span class="sxs-lookup"><span data-stu-id="3054f-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="3054f-133">Cuando se actualizan los archivos del origen se vuelve a implementar el sitio.</span><span class="sxs-lookup"><span data-stu-id="3054f-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="3054f-134">Opciones de implementación</span><span class="sxs-lookup"><span data-stu-id="3054f-134">Deployment options</span></span>

<span data-ttu-id="3054f-135">Los siguientes son algunos escenarios típicos de implementación:</span><span class="sxs-lookup"><span data-stu-id="3054f-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="3054f-136">Creación de una implementación de ensayo</span><span class="sxs-lookup"><span data-stu-id="3054f-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="3054f-137">Movimiento de funciones existentes para la implementación continua</span><span class="sxs-lookup"><span data-stu-id="3054f-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="3054f-138">Creación de una implementación de ensayo</span><span class="sxs-lookup"><span data-stu-id="3054f-138">Create a staging deployment</span></span>

<span data-ttu-id="3054f-139">Las aplicaciones de función todavía no admiten espacios de implementación.</span><span class="sxs-lookup"><span data-stu-id="3054f-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="3054f-140">Sin embargo, todavía puede administrar implementaciones de ensayo y producción independientes mediante la integración continua.</span><span class="sxs-lookup"><span data-stu-id="3054f-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="3054f-141">El proceso para configurar y trabajar con una implementación de ensayo tiene normalmente este aspecto:</span><span class="sxs-lookup"><span data-stu-id="3054f-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="3054f-142">Cree dos aplicaciones de función en su suscripción, una para el código de producción y otra para el ensayo.</span><span class="sxs-lookup"><span data-stu-id="3054f-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="3054f-143">Cree un origen de la implementación, si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="3054f-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="3054f-144">En este ejemplo se usa [GitHub].</span><span class="sxs-lookup"><span data-stu-id="3054f-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="3054f-145">Para la Function App de producción, complete los pasos anteriores descritos en **Configuración de la implementación continua** y establezca la rama de implementación en la rama principal del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3054f-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Elegir rama de la implementación](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="3054f-147">Repita este paso para la aplicación de función de ensayo, pero esta vez, seleccione la rama de ensayo en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3054f-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="3054f-148">Si el origen de la implementación no admite la bifurcación, utilice una carpeta diferente.</span><span class="sxs-lookup"><span data-stu-id="3054f-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="3054f-149">Realice actualizaciones en el código en la rama o carpeta de ensayo y, a continuación, compruebe que esos cambios se reflejan en la implementación de ensayo.</span><span class="sxs-lookup"><span data-stu-id="3054f-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="3054f-150">Después de la prueba, combine los cambios de la rama de ensayo en la rama principal.</span><span class="sxs-lookup"><span data-stu-id="3054f-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="3054f-151">Esta combinación desencadena la implementación en la Function App de producción.</span><span class="sxs-lookup"><span data-stu-id="3054f-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="3054f-152">Si el origen de la implementación no admite ramas, sobrescriba los archivos de la carpeta de producción con los archivos de la carpeta de ensayo.</span><span class="sxs-lookup"><span data-stu-id="3054f-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="3054f-153">Movimiento de funciones existentes para la implementación continua</span><span class="sxs-lookup"><span data-stu-id="3054f-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="3054f-154">Si dispone de funciones existentes que ha creado y mantenido en el portal, es necesario descargar los archivos de código de la función existente mediante FTP o mediante el repositorio de Git local antes de poder configurar la implementación continua como se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3054f-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="3054f-155">Puede hacerlo en la configuración de App Service de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="3054f-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="3054f-156">Una vez descargados los archivos, puede cargarlos en el origen de la implementación continua que haya seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3054f-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="3054f-157">Después de configurar la integración continua, ya no podrá modificar los archivos de origen en el portal de Funciones.</span><span class="sxs-lookup"><span data-stu-id="3054f-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="3054f-158">Configuración de las credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="3054f-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="3054f-159">Descarga de archivos mediante FTP</span><span class="sxs-lookup"><span data-stu-id="3054f-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="3054f-160">Descarga de archivos mediante el repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="3054f-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="3054f-161">Configuración de las credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="3054f-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="3054f-162">Para poder descargar archivos desde la Function App con FTP o el repositorio local de Git, debe configurar las credenciales para acceder al sitio.</span><span class="sxs-lookup"><span data-stu-id="3054f-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="3054f-163">Las credenciales se establecen en el nivel de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="3054f-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="3054f-164">Use los pasos siguientes para establecer las credenciales de implementación en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="3054f-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="3054f-165">En la Function App de [Azure Portal](https://portal.azure.com), haga clic en **Características de la plataforma** y en **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="3054f-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Configurar credenciales de implementación locales](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="3054f-167">Escriba un nombre de usuario y una contraseña y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3054f-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="3054f-168">Ahora puede usar estas credenciales para tener acceso a la aplicación de función mediante FTP o desde el repositorio de Git integrado.</span><span class="sxs-lookup"><span data-stu-id="3054f-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="3054f-169">Descarga de archivos mediante FTP</span><span class="sxs-lookup"><span data-stu-id="3054f-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="3054f-170">En la Function App de [Azure Portal](https://portal.azure.com), haga clic en **Características de la plataforma** y en **Propiedades** y luego copie los valores de **FTP/usuario de implementación**, **Nombre del host FTP** y **Nombre del host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="3054f-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="3054f-171">**FTP/usuario de implementación** debe escribirse tal como aparece en el portal, incluido el nombre de la aplicación, a fin de proporcionar el contexto adecuado para el servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="3054f-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Obtener la información de implementación](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="3054f-173">Desde el cliente de FTP, use la información de conexión recopilada para conectarse a la aplicación y descargar los archivos de origen de las funciones.</span><span class="sxs-lookup"><span data-stu-id="3054f-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="3054f-174">Descarga de archivos mediante el repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="3054f-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="3054f-175">En la Function App de [Azure Portal](https://portal.azure.com), haga clic en **Características de la plataforma** y en **Opciones de implementación**.</span><span class="sxs-lookup"><span data-stu-id="3054f-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="3054f-177">Luego, en la hoja **Implementación**, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="3054f-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar implementación continua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="3054f-179">En la hoja **Origen de implementación**, haga clic en **Repositorio de Git local** y luego en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3054f-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="3054f-180">En **Características de la plataforma**, haga clic en **Propiedades** y anote el valor de la dirección URL de Git.</span><span class="sxs-lookup"><span data-stu-id="3054f-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Configurar implementación continua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="3054f-182">Clone el repositorio en la máquina local mediante un símbolo del sistema compatible con Git o su herramienta de Git favorita.</span><span class="sxs-lookup"><span data-stu-id="3054f-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="3054f-183">El comando clone de Git tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="3054f-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="3054f-184">Recupere los archivos de su aplicación de función y póngalos en la copia del equipo local, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3054f-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="3054f-185">Si se le piden, proporcione las [credenciales de implementación configuradas](#credentials).</span><span class="sxs-lookup"><span data-stu-id="3054f-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="3054f-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="3054f-186">[GitHub]: https://github.com/</span></span>
