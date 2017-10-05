---
title: "Creación de una aplicación web ASP.NET Core en Visual Studio Code"
description: "En este tutorial muestra cómo crear una aplicación web ASP.NET Core con Visual Studio Code."
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
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="192a4-103">Creación de una aplicación web ASP.NET Core en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="192a4-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="192a4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="192a4-104">Overview</span></span>
<span data-ttu-id="192a4-105">En este tutorial se muestra cómo se crea una aplicación web de ASP.NET Core con [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) y cómo se implementa en [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="192a4-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="192a4-106">Aunque este artículo se refiere a las aplicaciones web, también se aplica a las aplicaciones de API y las aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="192a4-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="192a4-107">ASP.NET Core es un rediseño significativo de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="192a4-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="192a4-108">ASP.NET Core es un nuevo marco de código abierto multiplataforma diseñado para crear modernas aplicaciones web basadas en la nube con .NET.</span><span class="sxs-lookup"><span data-stu-id="192a4-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="192a4-109">Para obtener más información, consulte [Introducción a ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="192a4-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="192a4-110">Para obtener información sobre Aplicaciones web del Servicio de aplicaciones de Azure, consulte [Introducción a aplicaciones web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="192a4-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="192a4-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="192a4-111">Prerequisites</span></span>
* <span data-ttu-id="192a4-112">Instalación de [VS Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="192a4-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="192a4-113">Instalación de Git. Puede instalarlo desde cualquiera de estas ubicaciones: [Chocolatey](https://chocolatey.org/packages/git) o [git-scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="192a4-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="192a4-114">Si no está familiarizado con Git, elija [git-scm.com](http://git-scm.com/downloads) y seleccione la opción para **usar Git desde el símbolo del sistema de Windows**.</span><span class="sxs-lookup"><span data-stu-id="192a4-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="192a4-115">Una vez que instale Git, también tendrá que establecer el nombre de usuario de Git y el correo electrónico, ya que es necesario más adelante en el tutorial (al realizar una confirmación desde VS Code).</span><span class="sxs-lookup"><span data-stu-id="192a4-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="192a4-116">Instalación de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="192a4-116">Install ASP.NET Core</span></span>
<span data-ttu-id="192a4-117">ASP.NET Core es una pila de .NET eficiente que sirve para crear aplicaciones web y de nube modernas que se ejecutan en OS X, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="192a4-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="192a4-118">Se ha desarrollado desde el principio para proporcionar un marco de desarrollo optimizado para las aplicaciones que se implementan en la nube o se ejecutan de forma local.</span><span class="sxs-lookup"><span data-stu-id="192a4-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="192a4-119">Consta de componentes modulares con una sobrecarga mínima, para continuar disfrutando de flexibilidad al crear soluciones.</span><span class="sxs-lookup"><span data-stu-id="192a4-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="192a4-120">Este tutorial está diseñado para ayudarle a comenzar a crear aplicaciones con las últimas versiones de desarrollo de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="192a4-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="192a4-121">Las instrucciones siguientes son específicas de Windows.</span><span class="sxs-lookup"><span data-stu-id="192a4-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="192a4-122">Para obtener instrucciones de instalación en OS X, Linux y Windows, consulte [Introducción a ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="192a4-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="192a4-123">Para obtener instrucciones de instalación más detalladas para Windows, Linux y OS X, consulte [Instalación de ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="192a4-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="192a4-124">Creación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="192a4-124">Create the web app</span></span>
<span data-ttu-id="192a4-125">En esta sección se explica cómo aplicar scaffold a una nueva aplicación web ASP.NET mediante la herramienta CLI de .NET.</span><span class="sxs-lookup"><span data-stu-id="192a4-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="192a4-126">En el símbolo del sistema para crear la carpeta del proyecto y aplicar la técnica scaffolding a la aplicación, escriba lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="192a4-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI de donet: Generador de ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="192a4-128">Para restaurar los paquetes NuGet necesarios, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="192a4-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="192a4-129">Ejecute la aplicación web localmente.</span><span class="sxs-lookup"><span data-stu-id="192a4-129">Run the web app locally</span></span>
<span data-ttu-id="192a4-130">Ahora que ha creado la aplicación web y ha recuperado todos los paquetes de NuGet para la aplicación, puede ejecutar la aplicación web localmente.</span><span class="sxs-lookup"><span data-stu-id="192a4-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="192a4-131">Ejecute la aplicación (el comando `dotnet run` creará la aplicación cuando está anticuada):</span><span class="sxs-lookup"><span data-stu-id="192a4-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="192a4-132">Abra un explorador y vaya a la dirección URL siguiente.</span><span class="sxs-lookup"><span data-stu-id="192a4-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="192a4-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="192a4-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="192a4-134">La página predeterminada de la aplicación web se mostrará como sigue.</span><span class="sxs-lookup"><span data-stu-id="192a4-134">The default page of the web app will appear as follows.</span></span>
   
    ![Aplicación web local en un explorador](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="192a4-136">Cierre el explorador.</span><span class="sxs-lookup"><span data-stu-id="192a4-136">Close your browser.</span></span> <span data-ttu-id="192a4-137">En la **ventana Comandos**, presione **Ctrl+C** para cerrar la aplicación o cerrar dicha **ventana**.</span><span class="sxs-lookup"><span data-stu-id="192a4-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="192a4-138">Creación de una aplicación web en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="192a4-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="192a4-139">Los pasos siguientes le guiarán a través de la creación de una aplicación web en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="192a4-140">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="192a4-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="192a4-141">Haga clic en **NUEVO** en la parte superior izquierda del portal.</span><span class="sxs-lookup"><span data-stu-id="192a4-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="192a4-142">Haga clic en **Web Apps > Aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="192a4-142">Click **Web Apps > Web App**.</span></span>
   
    ![Nueva aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="192a4-144">Escriba un valor para **Nombre**, como **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="192a4-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="192a4-145">Tenga en cuenta que este nombre debe ser exclusivo y que el portal le obligará a ello al escribir el nombre.</span><span class="sxs-lookup"><span data-stu-id="192a4-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="192a4-146">Por lo tanto, si selecciona un valor diferente, tendrá que sustituir ese valor en cada aparición de **SampleWebAppDemo** que aparezca en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="192a4-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="192a4-147">Seleccione un **plan de Servicio de aplicaciones** ya existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="192a4-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="192a4-148">Si crea un nuevo plan, seleccione el nivel de precios, la ubicación y otras opciones.</span><span class="sxs-lookup"><span data-stu-id="192a4-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="192a4-149">Para obtener más información sobre los planes del Servicio de aplicaciones, consulte el artículo [Introducción detallada sobre los planes del Servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="192a4-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Hoja de la nueva aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="192a4-151">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="192a4-151">Click **Create**.</span></span>
   
    ![hoja de aplicación web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="192a4-153">Habilitación de la publicación Git para la nueva aplicación web</span><span class="sxs-lookup"><span data-stu-id="192a4-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="192a4-154">Git es un sistema de control de versión distribuida que puede utilizar para implementar su aplicación web del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="192a4-155">Tendrá que almacenar el código que escriba para su aplicación web en un repositorio Git local y lo implementará en Azure insertando en un repositorio remoto.</span><span class="sxs-lookup"><span data-stu-id="192a4-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="192a4-156">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="192a4-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="192a4-157">Haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="192a4-157">Click **Browse**.</span></span>
3. <span data-ttu-id="192a4-158">Haga clic en **Aplicaciones web** para ver una lista de las aplicaciones web asociadas con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="192a4-159">Seleccione la aplicación web que creó en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="192a4-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="192a4-160">En la hoja de aplicaciones web, haga clic en **Configuración** > **Implementación continua**.</span><span class="sxs-lookup"><span data-stu-id="192a4-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Host de la aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="192a4-162">Haga clic en **Elegir origen > Repositorio de Git local**.</span><span class="sxs-lookup"><span data-stu-id="192a4-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="192a4-163">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="192a4-163">Click **OK**.</span></span>
   
    ![Repositorio de Git local de Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="192a4-165">Si no ha configurado previamente las credenciales de implementación para publicar una aplicación web u otra aplicación del Servicio de aplicaciones, configúrelas ahora:</span><span class="sxs-lookup"><span data-stu-id="192a4-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="192a4-166">Haga clic en **Configuración** > **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="192a4-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="192a4-167">Se mostrará la hoja **Configurar credenciales de implementación** .</span><span class="sxs-lookup"><span data-stu-id="192a4-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="192a4-168">Cree un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="192a4-168">Create a user name and password.</span></span>  <span data-ttu-id="192a4-169">Necesitará esta contraseña más tarde al configurar Git.</span><span class="sxs-lookup"><span data-stu-id="192a4-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="192a4-170">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="192a4-170">Click **Save**.</span></span>
9. <span data-ttu-id="192a4-171">En la hoja de la aplicación web, haga clic en **Configuración > Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="192a4-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="192a4-172">La dirección URL del repositorio Git remoto en el que implementará se muestra en **DIRECCIÓN URL DE GIT**.</span><span class="sxs-lookup"><span data-stu-id="192a4-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="192a4-173">Copie el valor **dirección URL de GIT** para su uso posterior en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="192a4-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![Dirección URL de Git de Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="192a4-175">Publicación de la aplicación web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="192a4-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="192a4-176">En esta sección, creará un repositorio Git local e insertará desde ese repositorio a Azure para implementar la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="192a4-177">En VS Code seleccione la opción **Git** en la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="192a4-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![Icono de Git en VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="192a4-179">Seleccione **Inicializar repositorio Git** para asegurarse de que el área de trabajo está bajo control del código fuente de git.</span><span class="sxs-lookup"><span data-stu-id="192a4-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Inicializar Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="192a4-181">Abra la ventana Comandos y cambie los directorios por el directorio de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="192a4-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="192a4-182">Después, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="192a4-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="192a4-183">Este comando evita problemas relacionados con el texto donde existen las finalizaciones CRLF y LF.</span><span class="sxs-lookup"><span data-stu-id="192a4-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="192a4-184">En VS Code, agregue un mensaje de confirmación y haga clic en el icono de marca **Confirmar todo** .</span><span class="sxs-lookup"><span data-stu-id="192a4-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Confirmar todo de Git](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="192a4-186">Una vez que Git haya completado el procesamiento, verá que no hay ningún archivo que aparezca en la ventana de Git en **Cambios**.</span><span class="sxs-lookup"><span data-stu-id="192a4-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Sin cambios de Git](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="192a4-188">Vuelva a la ventana Comandos donde el símbolo del sistema señala al directorio donde se encuentra la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="192a4-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="192a4-189">Cree una referencia remota para insertar actualizaciones en la aplicación web usando la dirección URL de Git (terminada en “.git”) que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="192a4-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="192a4-190">Configure Git para guardar las credenciales localmente de manera que se anexe automáticamente a los comandos de inserción generados a partir de código de VS.</span><span class="sxs-lookup"><span data-stu-id="192a4-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="192a4-191">Envíe los cambios a Azure escribiendo el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="192a4-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="192a4-192">Después de esta inserción inicial en Azure, podrá realizar todos los comandos de inserción desde el código de VS.</span><span class="sxs-lookup"><span data-stu-id="192a4-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="192a4-193">Se le solicitará la contraseña que ha creado anteriormente en Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="192a4-194">**Nota: La contraseña no será visible.**</span><span class="sxs-lookup"><span data-stu-id="192a4-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="192a4-195">La salida de este comando finaliza con un mensaje que indica que la implementación se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="192a4-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="192a4-196">Si realiza cambios en la aplicación, puede volver a publicar directamente en el código de VS con la funcionalidad integrada de Git seleccionando la opción **Confirmar todo**, seguida de la opción **Insertar**.</span><span class="sxs-lookup"><span data-stu-id="192a4-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="192a4-197">Encontrará la opción **Insertar** en el menú desplegable junto a los botones **Confirmar todo** y **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="192a4-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="192a4-198">Si necesita para colaborar en un proyecto, considere la posibilidad de insertar en GitHub entre la inserción en Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="192a4-199">Ejecución de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="192a4-199">Run the app in Azure</span></span>
<span data-ttu-id="192a4-200">Ahora que ha implementado la aplicación web, vamos a ejecutar la aplicación mientras está hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="192a4-201">Esto puede hacerse de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="192a4-201">This can be done in two ways:</span></span>

* <span data-ttu-id="192a4-202">Abra un explorador y escriba el nombre de la aplicación web de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="192a4-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="192a4-203">En el Portal de Azure, busque la hoja de aplicación web para la aplicación web y haga clic en **Examinar** para ver la aplicación.</span><span class="sxs-lookup"><span data-stu-id="192a4-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="192a4-204">en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="192a4-204">in your default browser.</span></span>

![Aplicación web de Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="192a4-206">Resumen</span><span class="sxs-lookup"><span data-stu-id="192a4-206">Summary</span></span>
<span data-ttu-id="192a4-207">En este tutorial, ha aprendido a crear una aplicación web en VS Code y a implementarla en Azure.</span><span class="sxs-lookup"><span data-stu-id="192a4-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="192a4-208">Para más información sobre VS Code, consulte el artículo [¿Por qué Visual Studio Code?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="192a4-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="192a4-209">Para más información sobre App Service Web Apps, consulte [Información general de Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="192a4-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

