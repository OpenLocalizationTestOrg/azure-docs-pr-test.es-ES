---
title: "aaaCreate una aplicación web de ASP.NET Core en código de Visual Studio"
description: "Este tutorial ilustra cómo toocreate un núcleo de ASP.NET web app mediante código de Visual Studio."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="e9e13-103">Creación de una aplicación web ASP.NET Core en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e9e13-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="e9e13-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e9e13-104">Overview</span></span>
<span data-ttu-id="e9e13-105">Este tutorial muestra cómo toocreate un núcleo de ASP.NET web de aplicación con [código de Visual Studio (VS Code)](http://code.visualstudio.com//Docs/whyvscode) e implementarlo demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e9e13-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="e9e13-106">Aunque en este artículo se refiere a aplicaciones tooweb, también se aplica tooAPI aplicaciones y aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="e9e13-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="e9e13-107">ASP.NET Core es un rediseño significativo de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e9e13-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="e9e13-108">ASP.NET Core es un nuevo marco de código abierto multiplataforma diseñado para crear modernas aplicaciones web basadas en la nube con .NET.</span><span class="sxs-lookup"><span data-stu-id="e9e13-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="e9e13-109">Para obtener más información, consulte [Introducción tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="e9e13-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="e9e13-110">Para obtener información sobre Aplicaciones web del Servicio de aplicaciones de Azure, consulte [Introducción a aplicaciones web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9e13-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="e9e13-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e9e13-111">Prerequisites</span></span>
* <span data-ttu-id="e9e13-112">Instalación de [VS Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="e9e13-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="e9e13-113">Instalación de Git. Puede instalarlo desde cualquiera de estas ubicaciones: [Chocolatey](https://chocolatey.org/packages/git) o [git-scm.com](http://git-scm.com/downloads). Si está tooGit nueva, elija [git scm.com](http://git-scm.com/downloads) y seleccione la opción de hello demasiado**Use Git desde el símbolo del sistema de Windows hello**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="e9e13-114">Una vez que instale Git, también necesitará nombre de usuario de tooset Hola Git y correo electrónico porque es necesaria más adelante en el tutorial de hello (al realizar una confirmación de VS Code).</span><span class="sxs-lookup"><span data-stu-id="e9e13-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="e9e13-115">Instalación de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e9e13-115">Install ASP.NET Core</span></span>
<span data-ttu-id="e9e13-116">ASP.NET Core es una pila de .NET eficiente que sirve para crear aplicaciones web y de nube modernas que se ejecutan en OS X, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="e9e13-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="e9e13-117">Se ha generado desde Hola masa seguridad tooprovide un marco de trabajo de desarrollo optimizado para las aplicaciones que están ya sea en la nube implementado toohello o ejecutar de forma local.</span><span class="sxs-lookup"><span data-stu-id="e9e13-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="e9e13-118">Consta de componentes modulares con una sobrecarga mínima, para continuar disfrutando de flexibilidad al crear soluciones.</span><span class="sxs-lookup"><span data-stu-id="e9e13-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="e9e13-119">Este tutorial está diseñado tooget empezó a crear aplicaciones con las últimas versiones de desarrollo Hola de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e9e13-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="e9e13-120">Hola siguiendo las instrucciones es tooWindows específico.</span><span class="sxs-lookup"><span data-stu-id="e9e13-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="e9e13-121">Para obtener instrucciones de instalación en OS X, Linux y Windows, consulte [Introducción a ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="e9e13-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="e9e13-122">Para obtener instrucciones de instalación más detalladas para Windows, Linux y OS X, consulte [Instalación de ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="e9e13-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="e9e13-123">Crear una aplicación web de Hola</span><span class="sxs-lookup"><span data-stu-id="e9e13-123">Create hello web app</span></span>
<span data-ttu-id="e9e13-124">Esta sección muestra cómo tooscaffold una nueva aplicación ASP.NET web aplicación mediante herramientas de .NET CLI Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e13-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="e9e13-125">Escriba Hola siguiente en el símbolo del sistema toocreate Hola proyecto carpeta y scaffold Hola aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e9e13-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI de donet: Generador de ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="e9e13-127">toorestore Hola paquetes de NuGet es necesarios, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e9e13-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="e9e13-128">Ejecutar la aplicación web de hello localmente</span><span class="sxs-lookup"><span data-stu-id="e9e13-128">Run hello web app locally</span></span>
<span data-ttu-id="e9e13-129">Ahora que ha creado la aplicación web de hello y recuperar todos los paquetes de NuGet de hello para la aplicación hello, puede ejecutar la aplicación web de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="e9e13-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="e9e13-130">Ejecutar aplicación hello (hello `dotnet run` comando creará una aplicación hello cuando está anticuada):</span><span class="sxs-lookup"><span data-stu-id="e9e13-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="e9e13-131">Abra un explorador y navegue toohello después de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e9e13-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="e9e13-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="e9e13-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="e9e13-133">página predeterminada de Hola de aplicación web de hello aparecerán como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="e9e13-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Aplicación web local en un explorador](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="e9e13-135">Cierre el explorador.</span><span class="sxs-lookup"><span data-stu-id="e9e13-135">Close your browser.</span></span> <span data-ttu-id="e9e13-136">Hola **ventana de comandos**, presione **Ctrl + C** tooshut hacia abajo de la aplicación hello y cerrar hello **ventana de comandos**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="e9e13-137">Crear una aplicación web en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e9e13-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="e9e13-138">Hello siguientes pasos le guiarán por la creación de una aplicación web en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e13-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="e9e13-139">Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9e13-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e9e13-140">Haga clic en **NEW** en hello parte superior izquierda de hello Portal.</span><span class="sxs-lookup"><span data-stu-id="e9e13-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="e9e13-141">Haga clic en **Web Apps > Aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-141">Click **Web Apps > Web App**.</span></span>
   
    ![Nueva aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="e9e13-143">Escriba un valor para **Nombre**, como **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="e9e13-144">Tenga en cuenta que este nombre debe toobe único y portal de hello aplicará cuando intente nombre de hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="e9e13-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="e9e13-145">Por lo tanto, si selecciona un especifique un valor diferente, necesitará toosubstitute ese valor para cada aparición de **SampleWebAppDemo** que se ven en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e9e13-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="e9e13-146">Seleccione un **plan de Servicio de aplicaciones** ya existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="e9e13-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="e9e13-147">Si crea un nuevo plan, seleccione Hola plan de tarifa, ubicación y otras opciones.</span><span class="sxs-lookup"><span data-stu-id="e9e13-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="e9e13-148">Para obtener más información sobre los planes de servicio de aplicaciones, vea el artículo de hello [información general detallada de planes de servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9e13-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Hoja de la nueva aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="e9e13-150">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-150">Click **Create**.</span></span>
   
    ![hoja de aplicación web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="e9e13-152">Habilitar la publicación de Git para la aplicación web nueva de Hola</span><span class="sxs-lookup"><span data-stu-id="e9e13-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="e9e13-153">GIT es un sistema de control de versiones distribuidas puede usar toodeploy en la aplicación web de servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e13-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="e9e13-154">Va a almacenar el código de hello que escribir para la aplicación web en un repositorio Git local y va a implementar el código tooAzure insertando repositorio remoto tooa.</span><span class="sxs-lookup"><span data-stu-id="e9e13-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="e9e13-155">Inicie sesión en hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9e13-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e9e13-156">Haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-156">Click **Browse**.</span></span>
3. <span data-ttu-id="e9e13-157">Haga clic en **aplicaciones Web** tooview una lista de aplicaciones web de hello asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e13-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="e9e13-158">Seleccione la aplicación web de Hola que creó en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e9e13-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="e9e13-159">En la hoja de la aplicación hello web, haga clic en **configuración** > **implementación continua**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Host de la aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="e9e13-161">Haga clic en **Elegir origen > Repositorio de Git local**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="e9e13-162">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-162">Click **OK**.</span></span>
   
    ![Repositorio de Git local de Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="e9e13-164">Si no ha configurado previamente las credenciales de implementación para publicar una aplicación web u otra aplicación del Servicio de aplicaciones, configúrelas ahora:</span><span class="sxs-lookup"><span data-stu-id="e9e13-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="e9e13-165">Haga clic en **Configuración** > **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="e9e13-166">Hola **configurar credenciales de implementación** hoja se mostrarán.</span><span class="sxs-lookup"><span data-stu-id="e9e13-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="e9e13-167">Cree un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="e9e13-167">Create a user name and password.</span></span>  <span data-ttu-id="e9e13-168">Necesitará esta contraseña más tarde al configurar Git.</span><span class="sxs-lookup"><span data-stu-id="e9e13-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="e9e13-169">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-169">Click **Save**.</span></span>
9. <span data-ttu-id="e9e13-170">En la hoja de la aplicación web, haga clic en **Configuración > Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="e9e13-171">dirección URL de Hola de hello repositorio de Git remoto que se va a implementar toois se muestra en **dirección URL de GIT**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="e9e13-172">Hola copia **dirección URL de GIT** valor para su uso posterior en el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e13-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![Dirección URL de Git de Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="e9e13-174">Publicar su tooAzure de aplicación web servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e9e13-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="e9e13-175">En esta sección, creará un repositorio Git local y su tooAzure de aplicación web de inserción desde ese toodeploy tooAzure de repositorio.</span><span class="sxs-lookup"><span data-stu-id="e9e13-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="e9e13-176">En el código de VS, seleccione hello **Git** opción en la barra de navegación izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e13-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![Icono de Git en VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="e9e13-178">Seleccione **repositorio de git Initialize** toomake seguro de que el área de trabajo está bajo control de código fuente git.</span><span class="sxs-lookup"><span data-stu-id="e9e13-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Inicializar Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="e9e13-180">Abra Hola ventana de comandos y cambie el directorio de toohello de directorios de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e9e13-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="e9e13-181">A continuación, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e9e13-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="e9e13-182">Este comando evita problemas relacionados con el texto donde existen las finalizaciones CRLF y LF.</span><span class="sxs-lookup"><span data-stu-id="e9e13-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="e9e13-183">En el código de VS, agregar un mensaje de confirmación y haga clic en hello **confirmación todos los** icono de comprobación.</span><span class="sxs-lookup"><span data-stu-id="e9e13-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Confirmar todo de Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="e9e13-185">Una vez haya completado el procesamiento Git, verá que no hay archivos enumerados en la ventana de Git de hello en **cambios**.</span><span class="sxs-lookup"><span data-stu-id="e9e13-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Sin cambios de Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="e9e13-187">Cambiar toohello back-ventana de comandos donde hello símbolo apunta toohello directorio donde se encuentra la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e9e13-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="e9e13-188">Crear una referencia remota para insertar actualizaciones tooyour web app mediante el uso de hello dirección URL de Git (que termina en ".git") que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e9e13-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="e9e13-189">Configurar Git toosave sus credenciales localmente para que estén tooyour anexado automáticamente comandos de inserción generados a partir de código de VS.</span><span class="sxs-lookup"><span data-stu-id="e9e13-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="e9e13-190">Insertar su tooAzure cambios escribiendo el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9e13-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="e9e13-191">Después de este tooAzure inserción inicial, será toodo capaz de inserción de hello todos los comandos desde el código de VS.</span><span class="sxs-lookup"><span data-stu-id="e9e13-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="e9e13-192">Se le pediremos la contraseña de Hola que creó anteriormente en Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e13-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="e9e13-193">**Nota: La contraseña no será visible.**</span><span class="sxs-lookup"><span data-stu-id="e9e13-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="e9e13-194">salida de Hello de hello encima comando finaliza con un mensaje que la implementación es correcta.</span><span class="sxs-lookup"><span data-stu-id="e9e13-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="e9e13-195">Si realiza cambios tooyour aplicación, puede volver a publicar directamente en el código de VS mediante la funcionalidad integrada de Git de hello seleccionando hello **confirmar todos los** opción seguida de hello **Push** opción.</span><span class="sxs-lookup"><span data-stu-id="e9e13-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="e9e13-196">Encontrará hello **Push** opción disponible en hello menú desplegable siguiente toohello **confirmar todos los** y **actualizar** botones.</span><span class="sxs-lookup"><span data-stu-id="e9e13-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="e9e13-197">Si necesita toocollaborate en un proyecto, considere la posibilidad de insertar tooGitHub entre insertar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e9e13-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="e9e13-198">Ejecutar la aplicación hello en Azure</span><span class="sxs-lookup"><span data-stu-id="e9e13-198">Run hello app in Azure</span></span>
<span data-ttu-id="e9e13-199">Ahora que ha implementado la aplicación web, vamos a ejecutar aplicación de hello mientras hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e13-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="e9e13-200">Esto puede hacerse de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="e9e13-200">This can be done in two ways:</span></span>

* <span data-ttu-id="e9e13-201">Abra un explorador y escriba el nombre de saludo de la aplicación web como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="e9e13-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="e9e13-202">Hola Portal de Azure, localice la hoja de la aplicación hello web para la aplicación web y haga clic en **examinar** tooview la aplicación</span><span class="sxs-lookup"><span data-stu-id="e9e13-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="e9e13-203">en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e9e13-203">in your default browser.</span></span>

![Aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="e9e13-205">Resumen</span><span class="sxs-lookup"><span data-stu-id="e9e13-205">Summary</span></span>
<span data-ttu-id="e9e13-206">En este tutorial, se habrá aprendido cómo toocreate una aplicación web en VS Code e implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e9e13-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="e9e13-207">Para obtener más información sobre el código de VS, vea el artículo de hello [¿por qué el código de Visual Studio?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="e9e13-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="e9e13-208">Para más información sobre App Service Web Apps, consulte [Información general de Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9e13-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

