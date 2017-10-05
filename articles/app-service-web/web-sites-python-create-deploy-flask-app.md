---
title: "Creación de aplicaciones web con Flask en Azure"
description: "Un tutorial que indica cómo ejecutar una aplicación web de Python en Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="92f3d-103">Creación de aplicaciones web con Flask en Azure</span><span class="sxs-lookup"><span data-stu-id="92f3d-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="92f3d-104">En este tutorial, se describe cómo empezar a ejecutar Python en [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="92f3d-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="92f3d-105">Aplicaciones web ofrece hospedaje gratuito limitado y una implementación rápida. Además, ahora también se puede usar Python.</span><span class="sxs-lookup"><span data-stu-id="92f3d-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="92f3d-106">A medida que su aplicación crece, puede cambiar a un tipo de hospedaje de pago e integrar el resto de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="92f3d-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="92f3d-107">Creará una aplicación con el marco web de Flask (consulte las versiones alternativas de este tutorial para [Django](web-sites-python-create-deploy-django-app.md) y [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="92f3d-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="92f3d-108">Creará el sitio web en la galería de Azure, configurará la implementación Git y clonará el repositorio en modo local.</span><span class="sxs-lookup"><span data-stu-id="92f3d-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="92f3d-109">A continuación, ejecutará la aplicación localmente, realizará cambios, los confirmará y los insertará en Azure.</span><span class="sxs-lookup"><span data-stu-id="92f3d-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="92f3d-110">El tutorial muestra cómo llevarlo a cabo en Windows o Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="92f3d-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="92f3d-111">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="92f3d-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="92f3d-112">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="92f3d-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="92f3d-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="92f3d-113">Prerequisites</span></span>
* <span data-ttu-id="92f3d-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="92f3d-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="92f3d-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="92f3d-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="92f3d-116">setuptools, pip, virtualenv (solo en Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="92f3d-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="92f3d-117">Git</span><span class="sxs-lookup"><span data-stu-id="92f3d-117">Git</span></span>
* <span data-ttu-id="92f3d-118">[Python Tools para Visual Studio][Python Tools para Visual Studio] (PTVS)- Nota: Esto es opcional</span><span class="sxs-lookup"><span data-stu-id="92f3d-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="92f3d-119">**Nota:**la publicación TFS no se admite actualmente para los proyectos de Python.</span><span class="sxs-lookup"><span data-stu-id="92f3d-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="92f3d-120">Windows</span><span class="sxs-lookup"><span data-stu-id="92f3d-120">Windows</span></span>
<span data-ttu-id="92f3d-121">Si aún no tiene Python 2.7 o 3.4 instalado (32 bits), se recomienda instalar [Azure SDK para Python 2.7] o [Azure SDK para Python 3.4] mediante el instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="92f3d-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="92f3d-122">Se instala la versión de 32 bits de Python, setuptools, pip, virtualenv, etc. (Python de 32 bits es lo que se instala en los equipos host de Azure).</span><span class="sxs-lookup"><span data-stu-id="92f3d-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="92f3d-123">También puede obtener Python en [python.org].</span><span class="sxs-lookup"><span data-stu-id="92f3d-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="92f3d-124">Para Git, recomendamos [Git para Windows] o [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="92f3d-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="92f3d-125">Si utiliza Visual Studio, puede utilizar la compatibilidad integrada con Git.</span><span class="sxs-lookup"><span data-stu-id="92f3d-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="92f3d-126">También se recomienda instalar [Python Tools 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="92f3d-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="92f3d-127">Esto es opcional, pero si tiene [Visual Studio], incluidas las versiones gratuitas Visual Studio Community 2013 o Visual Studio Express 2013 para web, obtendrá un excelente IDE de Python.</span><span class="sxs-lookup"><span data-stu-id="92f3d-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="92f3d-128">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="92f3d-128">Mac/Linux</span></span>
<span data-ttu-id="92f3d-129">Debe tener Python y Git instalados, pero asegúrese de que tiene Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="92f3d-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="92f3d-130">Creación de una aplicación web en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="92f3d-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="92f3d-131">El primer paso para crear la aplicación consiste en crear la aplicación web a través del [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92f3d-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="92f3d-132">Inicie sesión en el Portal de Azure, haga clic en el botón **Nuevo** situado en la esquina inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="92f3d-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="92f3d-133">Haga clic en **Web y móvil**.</span><span class="sxs-lookup"><span data-stu-id="92f3d-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="92f3d-134">En el cuadro de búsqueda, escriba "python".</span><span class="sxs-lookup"><span data-stu-id="92f3d-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="92f3d-135">En los resultados de búsqueda, seleccione **Flask** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="92f3d-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="92f3d-136">Configure la nueva aplicación Flask, por ejemplo, la creación de un nuevo plan para el Servicio de aplicaciones y un nuevo grupo de recursos para él.</span><span class="sxs-lookup"><span data-stu-id="92f3d-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="92f3d-137">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="92f3d-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="92f3d-138">Configure la publicación de Git para la aplicación web recién creada siguiendo las instrucciones que se describen en [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="92f3d-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="92f3d-139">Información general de la aplicación</span><span class="sxs-lookup"><span data-stu-id="92f3d-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="92f3d-140">Contenido del repositorio de Git</span><span class="sxs-lookup"><span data-stu-id="92f3d-140">Git repository contents</span></span>
<span data-ttu-id="92f3d-141">A continuación se muestra información general de los archivos que encontrará en el repositorio de Git inicial, que se va a clonar en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="92f3d-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="92f3d-142">Orígenes principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-142">Main sources for the application.</span></span>  <span data-ttu-id="92f3d-143">Consta de tres páginas (índice, acerca de, contacto) con un diseño principal.</span><span class="sxs-lookup"><span data-stu-id="92f3d-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="92f3d-144">El contenido estático y los scripts incluyen bootstrap, jquery, modernizr y respond.</span><span class="sxs-lookup"><span data-stu-id="92f3d-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="92f3d-145">Compatibilidad con servidor de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="92f3d-145">Local development server support.</span></span> <span data-ttu-id="92f3d-146">Úselo para ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="92f3d-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="92f3d-147">Archivos de proyecto para su uso con [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="92f3d-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="92f3d-148">Proxy IIS para entornos virtuales y compatibilidad con la depuración remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="92f3d-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="92f3d-149">Paquetes externos necesarios para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-149">External packages needed by this application.</span></span> <span data-ttu-id="92f3d-150">El script de implementación instalará pip en los paquetes incluidos en este archivo.</span><span class="sxs-lookup"><span data-stu-id="92f3d-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="92f3d-151">Archivos de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="92f3d-151">IIS configuration files.</span></span>  <span data-ttu-id="92f3d-152">El script de implementación utilizará el web.x.y.config adecuado y lo copiará como web.config.</span><span class="sxs-lookup"><span data-stu-id="92f3d-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="92f3d-153">Archivos opcionales - Implementación de personalización</span><span class="sxs-lookup"><span data-stu-id="92f3d-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="92f3d-154">Archivos opcionales - Tiempo de ejecución de Python</span><span class="sxs-lookup"><span data-stu-id="92f3d-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="92f3d-155">Archivos adicionales en el servidor</span><span class="sxs-lookup"><span data-stu-id="92f3d-155">Additional files on server</span></span>
<span data-ttu-id="92f3d-156">Algunos archivos existen en el servidor pero no se agregan al repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="92f3d-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="92f3d-157">Estos se crean mediante el script de implementación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="92f3d-158">Archivo de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="92f3d-158">IIS configuration file.</span></span>  <span data-ttu-id="92f3d-159">Se crea desde web.x.y.config en cada implementación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="92f3d-160">Entorno virtual de Python.</span><span class="sxs-lookup"><span data-stu-id="92f3d-160">Python virtual environment.</span></span>  <span data-ttu-id="92f3d-161">Se crea durante la implementación si aún no existe un entorno virtual compatible en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="92f3d-162">En los paquetes que aparecen en requirements.txt se instala pip, pero pip omitirá la instalación si los paquetes ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="92f3d-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="92f3d-163">En las tres secciones siguientes se describe cómo continuar con el desarrollo de aplicaciones web en tres entornos diferentes:</span><span class="sxs-lookup"><span data-stu-id="92f3d-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="92f3d-164">Windows, con Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92f3d-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="92f3d-165">Windows, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="92f3d-165">Windows, with command line</span></span>
* <span data-ttu-id="92f3d-166">Mac/Linux, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="92f3d-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="92f3d-167">Desarrollo de aplicaciones web: Windows, Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92f3d-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="92f3d-168">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="92f3d-168">Clone the repository</span></span>
<span data-ttu-id="92f3d-169">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="92f3d-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="92f3d-170">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="92f3d-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="92f3d-171">Abra el archivo de la solución (.sln) que se incluye en la raíz del repositorio.</span><span class="sxs-lookup"><span data-stu-id="92f3d-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="92f3d-172">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="92f3d-172">Create virtual environment</span></span>
<span data-ttu-id="92f3d-173">Ahora vamos a crear un entorno virtual para el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="92f3d-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="92f3d-174">Haga clic con el botón secundario en **Entornos de Python** y elija **Agregar entorno virtual...**</span><span class="sxs-lookup"><span data-stu-id="92f3d-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="92f3d-175">Asegúrese de que el nombre del entorno sea `env`.</span><span class="sxs-lookup"><span data-stu-id="92f3d-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="92f3d-176">Seleccione el intérprete base.</span><span class="sxs-lookup"><span data-stu-id="92f3d-176">Select the base interpreter.</span></span>  <span data-ttu-id="92f3d-177">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja **Configuración de la aplicación** de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="92f3d-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="92f3d-178">Asegúrese de que esté activada la opción para descargar e instalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="92f3d-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="92f3d-179">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="92f3d-179">Click **Create**.</span></span>  <span data-ttu-id="92f3d-180">Esto creará el entorno virtual e instalará las dependencias mostradas en requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="92f3d-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="92f3d-181">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="92f3d-181">Run using development server</span></span>
<span data-ttu-id="92f3d-182">Presione F5 para iniciar la depuración y el explorador web abrirá automáticamente la página que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="92f3d-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="92f3d-183">Puede establecer puntos de interrupción en los orígenes, utilizar las ventanas Inspección, etc.  Consulte la [Documentación sobre Python Tools para Visual Studio] para obtener más información sobre las distintas características.</span><span class="sxs-lookup"><span data-stu-id="92f3d-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="92f3d-184">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="92f3d-184">Make changes</span></span>
<span data-ttu-id="92f3d-185">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="92f3d-186">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="92f3d-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="92f3d-187">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="92f3d-187">Install more packages</span></span>
<span data-ttu-id="92f3d-188">La aplicación puede tener otras dependencias, aparte de Python y Flask.</span><span class="sxs-lookup"><span data-stu-id="92f3d-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="92f3d-189">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="92f3d-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="92f3d-190">Para instalar un paquete, haga clic con el botón secundario en el entorno virtual y elija **Instalar paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="92f3d-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="92f3d-191">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba `azure`:</span><span class="sxs-lookup"><span data-stu-id="92f3d-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="92f3d-192">Haga clic con el botón secundario en el entorno virtual y elija **Generar requirements.txt** para actualizar requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="92f3d-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="92f3d-193">A continuación, confirme los cambios de requirements.txt en el repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="92f3d-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="92f3d-194">Implementar en Azure</span><span class="sxs-lookup"><span data-stu-id="92f3d-194">Deploy to Azure</span></span>
<span data-ttu-id="92f3d-195">Para desencadenar una implementación, haga clic en **Sincronizar** o **Insertar**.</span><span class="sxs-lookup"><span data-stu-id="92f3d-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="92f3d-196">La sincronización realiza una inserción y una extracción.</span><span class="sxs-lookup"><span data-stu-id="92f3d-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="92f3d-197">La primera implementación tardará algún tiempo, ya que crea un entorno virtual, paquetes de instalación, etc.</span><span class="sxs-lookup"><span data-stu-id="92f3d-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="92f3d-198">Visual Studio no muestra el progreso de la implementación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="92f3d-199">Si desea revisar la salida, consulte la sección [Solución de problemas - Implementación](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="92f3d-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="92f3d-200">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="92f3d-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="92f3d-201">Desarrollo de aplicaciones web - Windows - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="92f3d-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="92f3d-202">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="92f3d-202">Clone the repository</span></span>
<span data-ttu-id="92f3d-203">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure y agregue el repositorio de Azure como remoto.</span><span class="sxs-lookup"><span data-stu-id="92f3d-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="92f3d-204">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="92f3d-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="92f3d-205">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="92f3d-205">Create virtual environment</span></span>
<span data-ttu-id="92f3d-206">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue al repositorio).</span><span class="sxs-lookup"><span data-stu-id="92f3d-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="92f3d-207">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación creará su propio entorno localmente.</span><span class="sxs-lookup"><span data-stu-id="92f3d-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="92f3d-208">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja **Configuración de la aplicación** de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="92f3d-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="92f3d-209">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="92f3d-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="92f3d-210">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="92f3d-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="92f3d-211">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-211">Install any external packages required by your application.</span></span> <span data-ttu-id="92f3d-212">Puede utilizar el archivo requirements.txt en la raíz del repositorio para instalar los paquetes en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="92f3d-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="92f3d-213">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="92f3d-213">Run using development server</span></span>
<span data-ttu-id="92f3d-214">Puede iniciar la aplicación en un servidor de desarrollo con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="92f3d-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="92f3d-215">La consola mostrará la dirección URL y el puerto al que escucha el servidor:</span><span class="sxs-lookup"><span data-stu-id="92f3d-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="92f3d-216">A continuación, abra el explorador web para esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="92f3d-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="92f3d-217">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="92f3d-217">Make changes</span></span>
<span data-ttu-id="92f3d-218">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="92f3d-219">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="92f3d-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="92f3d-220">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="92f3d-220">Install more packages</span></span>
<span data-ttu-id="92f3d-221">La aplicación puede tener otras dependencias, aparte de Python y Flask.</span><span class="sxs-lookup"><span data-stu-id="92f3d-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="92f3d-222">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="92f3d-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="92f3d-223">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="92f3d-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="92f3d-224">Asegúrese de actualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="92f3d-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="92f3d-225">Confirme los cambios:</span><span class="sxs-lookup"><span data-stu-id="92f3d-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="92f3d-226">Implementación en Azure</span><span class="sxs-lookup"><span data-stu-id="92f3d-226">Deploy to Azure</span></span>
<span data-ttu-id="92f3d-227">Para desencadenar una implementación, inserte los cambios en Azure:</span><span class="sxs-lookup"><span data-stu-id="92f3d-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="92f3d-228">Verá la salida del script de implementación, incluida la creación del entorno virtual, la instalación de paquetes y la creación de web.config.</span><span class="sxs-lookup"><span data-stu-id="92f3d-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="92f3d-229">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="92f3d-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="92f3d-230">Desarrollo de aplicaciones web: Mac/Linux - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="92f3d-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="92f3d-231">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="92f3d-231">Clone the repository</span></span>
<span data-ttu-id="92f3d-232">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure y agregue el repositorio de Azure como remoto.</span><span class="sxs-lookup"><span data-stu-id="92f3d-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="92f3d-233">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="92f3d-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="92f3d-234">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="92f3d-234">Create virtual environment</span></span>
<span data-ttu-id="92f3d-235">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue al repositorio).</span><span class="sxs-lookup"><span data-stu-id="92f3d-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="92f3d-236">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación creará su propio entorno localmente.</span><span class="sxs-lookup"><span data-stu-id="92f3d-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="92f3d-237">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja **Configuración de la aplicación** de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="92f3d-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="92f3d-238">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="92f3d-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="92f3d-239">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="92f3d-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="92f3d-240">o pyvenv env</span><span class="sxs-lookup"><span data-stu-id="92f3d-240">or pyvenv env</span></span>

<span data-ttu-id="92f3d-241">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-241">Install any external packages required by your application.</span></span> <span data-ttu-id="92f3d-242">Puede utilizar el archivo requirements.txt en la raíz del repositorio para instalar los paquetes en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="92f3d-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="92f3d-243">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="92f3d-243">Run using development server</span></span>
<span data-ttu-id="92f3d-244">Puede iniciar la aplicación en un servidor de desarrollo con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="92f3d-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="92f3d-245">La consola mostrará la dirección URL y el puerto al que escucha el servidor:</span><span class="sxs-lookup"><span data-stu-id="92f3d-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="92f3d-246">A continuación, abra el explorador web para esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="92f3d-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="92f3d-247">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="92f3d-247">Make changes</span></span>
<span data-ttu-id="92f3d-248">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92f3d-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="92f3d-249">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="92f3d-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="92f3d-250">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="92f3d-250">Install more packages</span></span>
<span data-ttu-id="92f3d-251">La aplicación puede tener otras dependencias, aparte de Python y Flask.</span><span class="sxs-lookup"><span data-stu-id="92f3d-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="92f3d-252">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="92f3d-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="92f3d-253">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="92f3d-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="92f3d-254">Asegúrese de actualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="92f3d-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="92f3d-255">Confirme los cambios:</span><span class="sxs-lookup"><span data-stu-id="92f3d-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="92f3d-256">Implementación en Azure</span><span class="sxs-lookup"><span data-stu-id="92f3d-256">Deploy to Azure</span></span>
<span data-ttu-id="92f3d-257">Para desencadenar una implementación, inserte los cambios en Azure:</span><span class="sxs-lookup"><span data-stu-id="92f3d-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="92f3d-258">Verá la salida del script de implementación, incluida la creación del entorno virtual, la instalación de paquetes y la creación de web.config.</span><span class="sxs-lookup"><span data-stu-id="92f3d-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="92f3d-259">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="92f3d-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="92f3d-260">Solución de problemas - Instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="92f3d-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="92f3d-261">Solución de problemas - Entorno virtual</span><span class="sxs-lookup"><span data-stu-id="92f3d-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="92f3d-262">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92f3d-262">Next Steps</span></span>
<span data-ttu-id="92f3d-263">Siga estos vínculos para obtener más información acerca de Flask y Python Tools para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="92f3d-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="92f3d-264">[Documentación de Flask]</span><span class="sxs-lookup"><span data-stu-id="92f3d-264">[Flask Documentation]</span></span>
* <span data-ttu-id="92f3d-265">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="92f3d-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="92f3d-266">Para obtener información sobre el uso de Almacenamiento de tablas de Azure y MongoDB:</span><span class="sxs-lookup"><span data-stu-id="92f3d-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="92f3d-267">[Flask y MongoDB en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="92f3d-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="92f3d-268">[Flask y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="92f3d-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="92f3d-269">Para obtener más información, consulte también el [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="92f3d-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="92f3d-270">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="92f3d-270">What's changed</span></span>
* <span data-ttu-id="92f3d-271">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="92f3d-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="92f3d-272">[Flask y MongoDB en Azure con Python Tools para Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="92f3d-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="92f3d-273">[Flask y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="92f3d-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="92f3d-274">[Azure SDK para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="92f3d-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="92f3d-275">[Azure SDK para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="92f3d-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="92f3d-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="92f3d-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="92f3d-277">[Git para Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="92f3d-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="92f3d-278">[GitHub para Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="92f3d-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="92f3d-279">[Python Tools para Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="92f3d-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="92f3d-280">[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="92f3d-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="92f3d-281">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="92f3d-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="92f3d-282">[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="92f3d-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="92f3d-283">[Documentación de Flask]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="92f3d-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

