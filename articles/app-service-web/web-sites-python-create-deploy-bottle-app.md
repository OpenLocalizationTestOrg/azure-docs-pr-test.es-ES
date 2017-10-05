---
title: Aplicaciones web de Python con Bottle en Azure
description: "Un tutorial que indica cómo ejecutar una aplicación web de Python en Aplicaciones web del Servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="03062-103">Creación de aplicaciones web con Bottle en Azure</span><span class="sxs-lookup"><span data-stu-id="03062-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="03062-104">En este tutorial, se describe cómo empezar a ejecutar Python en Aplicaciones web del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="03062-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="03062-105">Aplicaciones web ofrece hospedaje gratuito limitado y una implementación rápida. Además, ahora también se puede usar Python.</span><span class="sxs-lookup"><span data-stu-id="03062-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="03062-106">A medida que su aplicación crece, puede cambiar a un tipo de hospedaje de pago e integrar el resto de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="03062-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="03062-107">Creará una aplicación web con el marco web de Bottle (consulte las versiones alternativas de este tutorial para [Django](web-sites-python-create-deploy-django-app.md) y [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="03062-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="03062-108">Creará la aplicación web en Azure Marketplace, configurará la implementación Git y clonará el repositorio en modo local.</span><span class="sxs-lookup"><span data-stu-id="03062-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="03062-109">A continuación, ejecutará la aplicación web localmente, realizará cambios, los confirmará y los insertará en [Aplicaciones web del Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="03062-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="03062-110">El tutorial muestra cómo llevarlo a cabo en Windows o Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="03062-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="03062-111">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="03062-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="03062-112">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="03062-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="03062-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="03062-113">Prerequisites</span></span>
* <span data-ttu-id="03062-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="03062-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="03062-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="03062-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="03062-116">setuptools, pip, virtualenv (solo en Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="03062-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="03062-117">Git</span><span class="sxs-lookup"><span data-stu-id="03062-117">Git</span></span>
* <span data-ttu-id="03062-118">[Python Tools 2.2 para Visual Studio][Python Tools 2.2 para Visual Studio] (PTVS) - Nota: Opcional</span><span class="sxs-lookup"><span data-stu-id="03062-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="03062-119">**Nota:**la publicación TFS no se admite actualmente para los proyectos de Python.</span><span class="sxs-lookup"><span data-stu-id="03062-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="03062-120">Windows</span><span class="sxs-lookup"><span data-stu-id="03062-120">Windows</span></span>
<span data-ttu-id="03062-121">Si aún no tiene Python 2.7 o 3.4 instalado (32 bits), se recomienda instalar [Azure SDK para Python 2.7] o [Azure SDK para Python 3.4] mediante el instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="03062-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="03062-122">Se instala la versión de 32 bits de Python, setuptools, pip, virtualenv, etc. (Python de 32 bits es lo que se instala en los equipos host de Azure).</span><span class="sxs-lookup"><span data-stu-id="03062-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="03062-123">También puede obtener Python en [python.org].</span><span class="sxs-lookup"><span data-stu-id="03062-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="03062-124">Para Git, recomendamos [Git para Windows] o [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="03062-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="03062-125">Si utiliza Visual Studio, puede utilizar la compatibilidad integrada con Git.</span><span class="sxs-lookup"><span data-stu-id="03062-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="03062-126">También se recomienda instalar [Python Tools 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="03062-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="03062-127">Esto es opcional, pero si tiene [Visual Studio], incluidas las versiones gratuitas Visual Studio Community 2013 o Visual Studio Express 2013 para web, obtendrá un excelente IDE de Python.</span><span class="sxs-lookup"><span data-stu-id="03062-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="03062-128">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="03062-128">Mac/Linux</span></span>
<span data-ttu-id="03062-129">Debe tener Python y Git instalados, pero asegúrese de que tiene Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="03062-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="03062-130">Creación de una aplicación web en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="03062-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="03062-131">El primer paso para crear la aplicación consiste en crear la aplicación web a través del [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03062-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="03062-132">Inicie sesión en el Portal de Azure, haga clic en el botón **Nuevo** situado en la esquina inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="03062-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="03062-133">En el cuadro de búsqueda, escriba "python".</span><span class="sxs-lookup"><span data-stu-id="03062-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="03062-134">En los resultados de búsqueda, seleccione **Bottle** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="03062-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="03062-135">Configure la nueva aplicación Flask, por ejemplo, la creación de un nuevo plan para el Servicio de aplicaciones y un nuevo grupo de recursos para él.</span><span class="sxs-lookup"><span data-stu-id="03062-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="03062-136">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="03062-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="03062-137">Configure la publicación de Git para la aplicación web recién creada siguiendo las instrucciones que se describen en [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="03062-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="03062-138">Información general de la aplicación</span><span class="sxs-lookup"><span data-stu-id="03062-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="03062-139">Contenido del repositorio de Git</span><span class="sxs-lookup"><span data-stu-id="03062-139">Git repository contents</span></span>
<span data-ttu-id="03062-140">A continuación se muestra información general de los archivos que encontrará en el repositorio de Git inicial, que se va a clonar en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="03062-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="03062-141">Orígenes principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03062-141">Main sources for the application.</span></span> <span data-ttu-id="03062-142">Consta de tres páginas (índice, acerca de, contacto) con un diseño principal.</span><span class="sxs-lookup"><span data-stu-id="03062-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="03062-143">El contenido estático y los scripts incluyen bootstrap, jquery, modernizr y respond.</span><span class="sxs-lookup"><span data-stu-id="03062-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="03062-144">Compatibilidad con servidor de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="03062-144">Local development server support.</span></span> <span data-ttu-id="03062-145">Úselo para ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="03062-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="03062-146">Archivos de proyecto para su uso con [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="03062-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="03062-147">Proxy IIS para entornos virtuales y compatibilidad con la depuración remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="03062-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="03062-148">Paquetes externos necesarios para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="03062-148">External packages needed by this application.</span></span> <span data-ttu-id="03062-149">El script de implementación instalará pip en los paquetes incluidos en este archivo.</span><span class="sxs-lookup"><span data-stu-id="03062-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="03062-150">Archivos de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="03062-150">IIS configuration files.</span></span> <span data-ttu-id="03062-151">El script de implementación utilizará el web.x.y.config adecuado y lo copiará como web.config.</span><span class="sxs-lookup"><span data-stu-id="03062-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="03062-152">Archivos opcionales - Implementación de personalización</span><span class="sxs-lookup"><span data-stu-id="03062-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="03062-153">Archivos opcionales - Tiempo de ejecución de Python</span><span class="sxs-lookup"><span data-stu-id="03062-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="03062-154">Archivos adicionales en el servidor</span><span class="sxs-lookup"><span data-stu-id="03062-154">Additional files on server</span></span>
<span data-ttu-id="03062-155">Algunos archivos existen en el servidor pero no se agregan al repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="03062-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="03062-156">Estos se crean mediante el script de implementación.</span><span class="sxs-lookup"><span data-stu-id="03062-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="03062-157">Archivo de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="03062-157">IIS configuration file.</span></span> <span data-ttu-id="03062-158">Se crea desde web.x.y.config en cada implementación.</span><span class="sxs-lookup"><span data-stu-id="03062-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="03062-159">Entorno virtual de Python.</span><span class="sxs-lookup"><span data-stu-id="03062-159">Python virtual environment.</span></span> <span data-ttu-id="03062-160">Se crea durante la implementación si todavía no existe un entorno virtual compatible en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="03062-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="03062-161">En los paquetes que aparecen en requirements.txt se instala pip, pero pip omitirá la instalación si los paquetes ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="03062-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="03062-162">En las tres secciones siguientes se describe cómo continuar con el desarrollo de aplicaciones web en tres entornos diferentes:</span><span class="sxs-lookup"><span data-stu-id="03062-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="03062-163">Windows, con Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03062-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="03062-164">Windows, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="03062-164">Windows, with command line</span></span>
* <span data-ttu-id="03062-165">Mac/Linux, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="03062-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="03062-166">Web de desarrollo de aplicaciones - Windows - Herramientas de Python para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03062-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="03062-167">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="03062-167">Clone the repository</span></span>
<span data-ttu-id="03062-168">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="03062-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="03062-169">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="03062-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="03062-170">Abra el archivo de la solución (.sln) que se incluye en la raíz del repositorio.</span><span class="sxs-lookup"><span data-stu-id="03062-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="03062-171">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="03062-171">Create virtual environment</span></span>
<span data-ttu-id="03062-172">Ahora vamos a crear un entorno virtual para el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="03062-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="03062-173">Haga clic con el botón secundario en **Entornos de Python** y elija **Agregar entorno virtual...**</span><span class="sxs-lookup"><span data-stu-id="03062-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="03062-174">Asegúrese de que el nombre del entorno sea `env`.</span><span class="sxs-lookup"><span data-stu-id="03062-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="03062-175">Seleccione el intérprete base.</span><span class="sxs-lookup"><span data-stu-id="03062-175">Select the base interpreter.</span></span> <span data-ttu-id="03062-176">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja **Configuración de la aplicación** de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="03062-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="03062-177">Asegúrese de que esté activada la opción para descargar e instalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="03062-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="03062-178">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="03062-178">Click **Create**.</span></span> <span data-ttu-id="03062-179">Esto creará el entorno virtual e instalará las dependencias mostradas en requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="03062-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="03062-180">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="03062-180">Run using development server</span></span>
<span data-ttu-id="03062-181">Presione F5 para iniciar la depuración y el explorador web abrirá automáticamente la página que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="03062-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="03062-182">Puede establecer puntos de interrupción en los orígenes, utilizar las ventanas Inspección, etc. Consulte la [Documentación sobre Python Tools para Visual Studio] para obtener más información sobre las distintas características.</span><span class="sxs-lookup"><span data-stu-id="03062-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="03062-183">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="03062-183">Make changes</span></span>
<span data-ttu-id="03062-184">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03062-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="03062-185">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="03062-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="03062-186">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="03062-186">Install more packages</span></span>
<span data-ttu-id="03062-187">La aplicación puede tener otras dependencias, aparte de Python y Bottle.</span><span class="sxs-lookup"><span data-stu-id="03062-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="03062-188">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="03062-188">You can install additional packages using pip.</span></span> <span data-ttu-id="03062-189">Para instalar un paquete, haga clic con el botón secundario en el entorno virtual y elija **Instalar paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="03062-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="03062-190">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba `azure`:</span><span class="sxs-lookup"><span data-stu-id="03062-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="03062-191">Haga clic con el botón secundario en el entorno virtual y elija **Generar requirements.txt** para actualizar requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="03062-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="03062-192">A continuación, confirme los cambios de requirements.txt en el repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="03062-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="03062-193">Implementar en Azure</span><span class="sxs-lookup"><span data-stu-id="03062-193">Deploy to Azure</span></span>
<span data-ttu-id="03062-194">Para desencadenar una implementación, haga clic en **Sincronizar** o **Insertar**.</span><span class="sxs-lookup"><span data-stu-id="03062-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="03062-195">La sincronización realiza una inserción y una extracción.</span><span class="sxs-lookup"><span data-stu-id="03062-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="03062-196">La primera implementación tardará algún tiempo, ya que crea un entorno virtual, paquetes de instalación, etc.</span><span class="sxs-lookup"><span data-stu-id="03062-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="03062-197">Visual Studio no muestra el progreso de la implementación.</span><span class="sxs-lookup"><span data-stu-id="03062-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="03062-198">Si desea revisar la salida, consulte la sección [Solución de problemas - Implementación](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="03062-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="03062-199">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="03062-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="03062-200">Desarrollo de aplicaciones web - Windows - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="03062-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="03062-201">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="03062-201">Clone the repository</span></span>
<span data-ttu-id="03062-202">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure y agregue el repositorio de Azure como remoto.</span><span class="sxs-lookup"><span data-stu-id="03062-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="03062-203">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="03062-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="03062-204">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="03062-204">Create virtual environment</span></span>
<span data-ttu-id="03062-205">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue al repositorio).</span><span class="sxs-lookup"><span data-stu-id="03062-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="03062-206">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación creará su propio entorno localmente.</span><span class="sxs-lookup"><span data-stu-id="03062-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="03062-207">Asegúrese de usar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja Configuración de la aplicación de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="03062-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="03062-208">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="03062-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="03062-209">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="03062-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="03062-210">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03062-210">Install any external packages required by your application.</span></span> <span data-ttu-id="03062-211">Puede utilizar el archivo requirements.txt en la raíz del repositorio para instalar los paquetes en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="03062-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="03062-212">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="03062-212">Run using development server</span></span>
<span data-ttu-id="03062-213">Puede iniciar la aplicación en un servidor de desarrollo con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="03062-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="03062-214">La consola mostrará la dirección URL y el puerto al que escucha el servidor:</span><span class="sxs-lookup"><span data-stu-id="03062-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="03062-215">A continuación, abra el explorador web para esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="03062-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="03062-216">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="03062-216">Make changes</span></span>
<span data-ttu-id="03062-217">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03062-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="03062-218">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="03062-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="03062-219">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="03062-219">Install more packages</span></span>
<span data-ttu-id="03062-220">La aplicación puede tener otras dependencias, aparte de Python y Bottle.</span><span class="sxs-lookup"><span data-stu-id="03062-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="03062-221">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="03062-221">You can install additional packages using pip.</span></span> <span data-ttu-id="03062-222">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="03062-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="03062-223">Asegúrese de actualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="03062-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="03062-224">Confirme los cambios:</span><span class="sxs-lookup"><span data-stu-id="03062-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="03062-225">Implementación en Azure</span><span class="sxs-lookup"><span data-stu-id="03062-225">Deploy to Azure</span></span>
<span data-ttu-id="03062-226">Para desencadenar una implementación, inserte los cambios en Azure:</span><span class="sxs-lookup"><span data-stu-id="03062-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="03062-227">Verá la salida del script de implementación, incluida la creación del entorno virtual, la instalación de paquetes y la creación de web.config.</span><span class="sxs-lookup"><span data-stu-id="03062-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="03062-228">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="03062-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="03062-229">Desarrollo de aplicaciones web: Mac/Linux - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="03062-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="03062-230">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="03062-230">Clone the repository</span></span>
<span data-ttu-id="03062-231">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure y agregue el repositorio de Azure como remoto.</span><span class="sxs-lookup"><span data-stu-id="03062-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="03062-232">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="03062-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="03062-233">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="03062-233">Create virtual environment</span></span>
<span data-ttu-id="03062-234">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue al repositorio).</span><span class="sxs-lookup"><span data-stu-id="03062-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="03062-235">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación creará su propio entorno localmente.</span><span class="sxs-lookup"><span data-stu-id="03062-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="03062-236">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja Configuración de la aplicación de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="03062-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="03062-237">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="03062-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="03062-238">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="03062-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="03062-239">o pyvenv env</span><span class="sxs-lookup"><span data-stu-id="03062-239">or pyvenv env</span></span>

<span data-ttu-id="03062-240">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03062-240">Install any external packages required by your application.</span></span> <span data-ttu-id="03062-241">Puede utilizar el archivo requirements.txt en la raíz del repositorio para instalar los paquetes en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="03062-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="03062-242">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="03062-242">Run using development server</span></span>
<span data-ttu-id="03062-243">Puede iniciar la aplicación en un servidor de desarrollo con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="03062-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="03062-244">La consola mostrará la dirección URL y el puerto al que escucha el servidor:</span><span class="sxs-lookup"><span data-stu-id="03062-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="03062-245">A continuación, abra el explorador web para esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="03062-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="03062-246">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="03062-246">Make changes</span></span>
<span data-ttu-id="03062-247">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03062-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="03062-248">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="03062-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="03062-249">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="03062-249">Install more packages</span></span>
<span data-ttu-id="03062-250">La aplicación puede tener otras dependencias, aparte de Python y Bottle.</span><span class="sxs-lookup"><span data-stu-id="03062-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="03062-251">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="03062-251">You can install additional packages using pip.</span></span> <span data-ttu-id="03062-252">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="03062-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="03062-253">Asegúrese de actualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="03062-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="03062-254">Confirme los cambios:</span><span class="sxs-lookup"><span data-stu-id="03062-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="03062-255">Implementación en Azure</span><span class="sxs-lookup"><span data-stu-id="03062-255">Deploy to Azure</span></span>
<span data-ttu-id="03062-256">Para desencadenar una implementación, inserte los cambios en Azure:</span><span class="sxs-lookup"><span data-stu-id="03062-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="03062-257">Verá la salida del script de implementación, incluida la creación del entorno virtual, la instalación de paquetes y la creación de web.config.</span><span class="sxs-lookup"><span data-stu-id="03062-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="03062-258">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="03062-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="03062-259">Solución de problemas - Instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="03062-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="03062-260">Solución de problemas - Entorno virtual</span><span class="sxs-lookup"><span data-stu-id="03062-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="03062-261">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03062-261">Next Steps</span></span>
<span data-ttu-id="03062-262">Siga estos vínculos para obtener más información acerca de Bottle y Python Tools para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="03062-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="03062-263">[Documentación de Bottle]</span><span class="sxs-lookup"><span data-stu-id="03062-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="03062-264">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="03062-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="03062-265">Para obtener información sobre el uso de Almacenamiento de tablas de Azure y MongoDB:</span><span class="sxs-lookup"><span data-stu-id="03062-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="03062-266">[Bottle y MongoDB en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="03062-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="03062-267">[Bottle y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="03062-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="03062-268">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="03062-268">What's changed</span></span>
* <span data-ttu-id="03062-269">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="03062-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="03062-270">[Bottle y MongoDB en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="03062-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="03062-271">[Bottle y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="03062-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="03062-272">[Azure SDK para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="03062-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="03062-273">[Azure SDK para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="03062-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="03062-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="03062-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="03062-275">[Git para Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="03062-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="03062-276">[GitHub para Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="03062-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="03062-277">[Python Tools para Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="03062-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="03062-278">[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="03062-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="03062-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="03062-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="03062-280">[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="03062-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="03062-281">[Documentación de Bottle]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="03062-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

