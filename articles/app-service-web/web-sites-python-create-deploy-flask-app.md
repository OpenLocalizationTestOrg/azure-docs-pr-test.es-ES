---
title: aplicaciones web aaaCreating con matraz en Azure
description: "Un tutorial que le presenta toorunning una aplicación web de Python en Azure."
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
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="db5f8-103">Creación de aplicaciones web con Flask en Azure</span><span class="sxs-lookup"><span data-stu-id="db5f8-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="db5f8-104">Este tutorial describe cómo tooget comenzó a ejecutarse Python en [aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="db5f8-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="db5f8-105">Aplicaciones web ofrece hospedaje gratuito limitado y una implementación rápida. Además, ahora también se puede usar Python.</span><span class="sxs-lookup"><span data-stu-id="db5f8-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="db5f8-106">Medida que crezca su aplicación, puede cambiar toopaid de hospedaje y también se puede integrar con todos Hola otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="db5f8-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="db5f8-107">Se creará una aplicación con el marco de trabajo de hello matraz web (vea versiones alternativas de este tutorial para [Django](web-sites-python-create-deploy-django-app.md) y [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="db5f8-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="db5f8-108">Se crear sitio Web de Hola de hello Galería de Azure, configure la implementación de Git y clonar el repositorio de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="db5f8-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="db5f8-109">A continuación, se ejecuta la aplicación hello localmente, realizar cambios, confirmar e insertarlas tooAzure.</span><span class="sxs-lookup"><span data-stu-id="db5f8-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="db5f8-110">Hola tutorial se muestra cómo toodo de Windows o Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="db5f8-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="db5f8-111">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="db5f8-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="db5f8-112">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="db5f8-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="db5f8-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="db5f8-113">Prerequisites</span></span>
* <span data-ttu-id="db5f8-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="db5f8-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="db5f8-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="db5f8-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="db5f8-116">setuptools, pip, virtualenv (solo en Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="db5f8-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="db5f8-117">Git</span><span class="sxs-lookup"><span data-stu-id="db5f8-117">Git</span></span>
* <span data-ttu-id="db5f8-118">[Python Tools para Visual Studio][Python Tools para Visual Studio] (PTVS)- Nota: Esto es opcional</span><span class="sxs-lookup"><span data-stu-id="db5f8-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="db5f8-119">**Nota:**la publicación TFS no se admite actualmente para los proyectos de Python.</span><span class="sxs-lookup"><span data-stu-id="db5f8-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="db5f8-120">Windows</span><span class="sxs-lookup"><span data-stu-id="db5f8-120">Windows</span></span>
<span data-ttu-id="db5f8-121">Si aún no tiene Python 2.7 o 3.4 instalado (32 bits), se recomienda instalar [Azure SDK para Python 2.7] o [Azure SDK para Python 3.4] mediante el instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="db5f8-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="db5f8-122">Esto instala la versión de 32 bits de Hola de Python, setuptools, pip, virtualenv, etcetera (32-bit Python es lo que se instala en equipos de host de Azure de hello).</span><span class="sxs-lookup"><span data-stu-id="db5f8-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="db5f8-123">También puede obtener Python en [python.org].</span><span class="sxs-lookup"><span data-stu-id="db5f8-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="db5f8-124">Para Git, recomendamos [Git para Windows] o [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="db5f8-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="db5f8-125">Si utiliza Visual Studio, puede usar soporte técnico de Git de hello integrado.</span><span class="sxs-lookup"><span data-stu-id="db5f8-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="db5f8-126">También se recomienda instalar [Python Tools 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="db5f8-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="db5f8-127">Esto es opcional, pero si tiene [Visual Studio], incluidos Hola liberar Visual Studio Community 2013 o Visual Studio Express 2013 para Web, a continuación, esto le proporcionará un excelente IDE de Python.</span><span class="sxs-lookup"><span data-stu-id="db5f8-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="db5f8-128">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="db5f8-128">Mac/Linux</span></span>
<span data-ttu-id="db5f8-129">Debe tener Python y Git instalados, pero asegúrese de que tiene Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="db5f8-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="db5f8-130">Crear aplicación Web en hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="db5f8-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="db5f8-131">primer paso para crear la aplicación Hello es toocreate hello web app mediante hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="db5f8-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="db5f8-132">Inicie sesión en hello Portal de Azure y haga clic en hello **NEW** botón en la esquina izquierda inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="db5f8-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="db5f8-133">Haga clic en **Web y móvil**.</span><span class="sxs-lookup"><span data-stu-id="db5f8-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="db5f8-134">En el cuadro de búsqueda de hello, escriba "python".</span><span class="sxs-lookup"><span data-stu-id="db5f8-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="db5f8-135">En los resultados de la búsqueda de hello, seleccione **matraz**, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="db5f8-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="db5f8-136">Configurar aplicación de matraz nueva hello, como la creación de un nuevo plan de servicio de aplicaciones y un nuevo grupo de recursos para él.</span><span class="sxs-lookup"><span data-stu-id="db5f8-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="db5f8-137">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="db5f8-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="db5f8-138">Configurar la publicación de Git de la aplicación web recién creado siguiendo las instrucciones de hello en [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="db5f8-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="db5f8-139">Información general de la aplicación</span><span class="sxs-lookup"><span data-stu-id="db5f8-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="db5f8-140">Contenido del repositorio de Git</span><span class="sxs-lookup"><span data-stu-id="db5f8-140">Git repository contents</span></span>
<span data-ttu-id="db5f8-141">Esta es una visión general de los archivos de Hola que encontrará en el repositorio de Git inicial hello, que se podrá clonar en la sección siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="db5f8-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="db5f8-142">Orígenes principales de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="db5f8-142">Main sources for hello application.</span></span>  <span data-ttu-id="db5f8-143">Consta de tres páginas (índice, acerca de, contacto) con un diseño principal.</span><span class="sxs-lookup"><span data-stu-id="db5f8-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="db5f8-144">El contenido estático y los scripts incluyen bootstrap, jquery, modernizr y respond.</span><span class="sxs-lookup"><span data-stu-id="db5f8-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="db5f8-145">Compatibilidad con servidor de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="db5f8-145">Local development server support.</span></span> <span data-ttu-id="db5f8-146">Use esta aplicación de hello toorun localmente.</span><span class="sxs-lookup"><span data-stu-id="db5f8-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="db5f8-147">Archivos de proyecto para su uso con [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="db5f8-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="db5f8-148">Proxy IIS para entornos virtuales y compatibilidad con la depuración remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="db5f8-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="db5f8-149">Paquetes externos necesarios para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="db5f8-149">External packages needed by this application.</span></span> <span data-ttu-id="db5f8-150">script de implementación de Hola pip paquetes de Hola de instalación incluidos en este archivo.</span><span class="sxs-lookup"><span data-stu-id="db5f8-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="db5f8-151">Archivos de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="db5f8-151">IIS configuration files.</span></span>  <span data-ttu-id="db5f8-152">script de implementación de Hello usará web.x.y.config adecuado de Hola y copiar como web.config.</span><span class="sxs-lookup"><span data-stu-id="db5f8-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="db5f8-153">Archivos opcionales - Implementación de personalización</span><span class="sxs-lookup"><span data-stu-id="db5f8-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="db5f8-154">Archivos opcionales - Tiempo de ejecución de Python</span><span class="sxs-lookup"><span data-stu-id="db5f8-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="db5f8-155">Archivos adicionales en el servidor</span><span class="sxs-lookup"><span data-stu-id="db5f8-155">Additional files on server</span></span>
<span data-ttu-id="db5f8-156">Algunos archivos existen en el servidor de hello pero no se agregan toohello repositorio de git.</span><span class="sxs-lookup"><span data-stu-id="db5f8-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="db5f8-157">Estos se crean mediante el script de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="db5f8-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="db5f8-158">Archivo de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="db5f8-158">IIS configuration file.</span></span>  <span data-ttu-id="db5f8-159">Se crea desde web.x.y.config en cada implementación.</span><span class="sxs-lookup"><span data-stu-id="db5f8-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="db5f8-160">Entorno virtual de Python.</span><span class="sxs-lookup"><span data-stu-id="db5f8-160">Python virtual environment.</span></span>  <span data-ttu-id="db5f8-161">Si aún no existe un entorno virtual compatible en la aplicación hello, creados durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="db5f8-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="db5f8-162">Paquetes incluidos en requirements.txt son pip instalado, pero pip omitirá la instalación si ya se han instalado paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="db5f8-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="db5f8-163">Hello 3 secciones describen cómo tooproceed con hello web desarrollo de aplicaciones en 3 entornos diferentes:</span><span class="sxs-lookup"><span data-stu-id="db5f8-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="db5f8-164">Windows, con Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db5f8-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="db5f8-165">Windows, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="db5f8-165">Windows, with command line</span></span>
* <span data-ttu-id="db5f8-166">Mac/Linux, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="db5f8-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="db5f8-167">Desarrollo de aplicaciones web: Windows, Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db5f8-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="db5f8-168">Repositorio de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="db5f8-168">Clone hello repository</span></span>
<span data-ttu-id="db5f8-169">En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="db5f8-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="db5f8-170">Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="db5f8-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="db5f8-171">Hola abrir archivo de solución (.sln) que se incluye en la raíz de hello del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="db5f8-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="db5f8-172">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="db5f8-172">Create virtual environment</span></span>
<span data-ttu-id="db5f8-173">Ahora vamos a crear un entorno virtual para el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="db5f8-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="db5f8-174">Haga clic con el botón secundario en **Entornos de Python** y elija **Agregar entorno virtual...**</span><span class="sxs-lookup"><span data-stu-id="db5f8-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="db5f8-175">Asegúrese de que nombre hello del entorno de hello es `env`.</span><span class="sxs-lookup"><span data-stu-id="db5f8-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="db5f8-176">Seleccione intérprete base Hola.</span><span class="sxs-lookup"><span data-stu-id="db5f8-176">Select hello base interpreter.</span></span>  <span data-ttu-id="db5f8-177">Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello **configuración de la aplicación** hoja de la aplicación web en hello Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="db5f8-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="db5f8-178">Asegúrese de que esté marcada Hola opción toodownload e instalar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="db5f8-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="db5f8-179">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="db5f8-179">Click **Create**.</span></span>  <span data-ttu-id="db5f8-180">Esto se crear entorno virtual de hello e instalar las dependencias en requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="db5f8-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="db5f8-181">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="db5f8-181">Run using development server</span></span>
<span data-ttu-id="db5f8-182">Presione F5 toostart depuración y el explorador web abrirá automáticamente página toohello que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="db5f8-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="db5f8-183">Puede establecer puntos de interrupción en orígenes de hello, las ventanas de inspección de uso hello, etcetera.  Vea hello [Python Tools para la documentación de Visual Studio] para obtener más información sobre Hola distintas características.</span><span class="sxs-lookup"><span data-stu-id="db5f8-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="db5f8-184">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="db5f8-184">Make changes</span></span>
<span data-ttu-id="db5f8-185">Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.</span><span class="sxs-lookup"><span data-stu-id="db5f8-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="db5f8-186">Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="db5f8-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="db5f8-187">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="db5f8-187">Install more packages</span></span>
<span data-ttu-id="db5f8-188">La aplicación puede tener otras dependencias, aparte de Python y Flask.</span><span class="sxs-lookup"><span data-stu-id="db5f8-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="db5f8-189">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="db5f8-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="db5f8-190">tooinstall un paquete, haga doble clic en entorno virtual de Hola y seleccione **instalar un paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="db5f8-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="db5f8-191">Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba `azure`:</span><span class="sxs-lookup"><span data-stu-id="db5f8-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="db5f8-192">Haga doble clic en el entorno virtual de Hola y seleccione **generar requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="db5f8-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="db5f8-193">A continuación, confirmar el repositorio de Git de hello cambios toorequirements.txt toohello.</span><span class="sxs-lookup"><span data-stu-id="db5f8-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="db5f8-194">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="db5f8-194">Deploy tooAzure</span></span>
<span data-ttu-id="db5f8-195">tootrigger una implementación, haga clic en **sincronización** o **Push**.</span><span class="sxs-lookup"><span data-stu-id="db5f8-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="db5f8-196">La sincronización realiza una inserción y una extracción.</span><span class="sxs-lookup"><span data-stu-id="db5f8-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="db5f8-197">primera implementación de Hello tardará algún tiempo, tal y como se va a crear un entorno virtual, paquetes de instalación, etcetera.</span><span class="sxs-lookup"><span data-stu-id="db5f8-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="db5f8-198">Visual Studio no muestra el progreso de Hola de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="db5f8-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="db5f8-199">Si desea que la salida de hello tooreview, vea la sección Hola en [solución de problemas - implementación](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="db5f8-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="db5f8-200">Examinar los cambios de toohello tooview de dirección URL de Azure.</span><span class="sxs-lookup"><span data-stu-id="db5f8-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="db5f8-201">Desarrollo de aplicaciones web - Windows - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="db5f8-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="db5f8-202">Repositorio de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="db5f8-202">Clone hello repository</span></span>
<span data-ttu-id="db5f8-203">En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure y agregar hello Azure repositorio como un control remoto.</span><span class="sxs-lookup"><span data-stu-id="db5f8-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="db5f8-204">Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="db5f8-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="db5f8-205">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="db5f8-205">Create virtual environment</span></span>
<span data-ttu-id="db5f8-206">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue toohello repositorio).</span><span class="sxs-lookup"><span data-stu-id="db5f8-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="db5f8-207">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación hello creará su propias localmente.</span><span class="sxs-lookup"><span data-stu-id="db5f8-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="db5f8-208">Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello **configuración de la aplicación** hoja de la aplicación web en hello Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="db5f8-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="db5f8-209">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="db5f8-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="db5f8-210">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="db5f8-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="db5f8-211">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db5f8-211">Install any external packages required by your application.</span></span> <span data-ttu-id="db5f8-212">Puede usar el archivo de requirements.txt de hello en raíz de Hola de paquetes de saludo repositorio tooinstall hello en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="db5f8-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="db5f8-213">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="db5f8-213">Run using development server</span></span>
<span data-ttu-id="db5f8-214">Puede iniciar la aplicación hello en un servidor de desarrollo con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="db5f8-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="db5f8-215">consola de Hola mostrará la dirección URL de Hola y escucha servidor hello de puertos:</span><span class="sxs-lookup"><span data-stu-id="db5f8-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="db5f8-216">A continuación, abra la dirección URL toothat del explorador web.</span><span class="sxs-lookup"><span data-stu-id="db5f8-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="db5f8-217">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="db5f8-217">Make changes</span></span>
<span data-ttu-id="db5f8-218">Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.</span><span class="sxs-lookup"><span data-stu-id="db5f8-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="db5f8-219">Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="db5f8-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="db5f8-220">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="db5f8-220">Install more packages</span></span>
<span data-ttu-id="db5f8-221">La aplicación puede tener otras dependencias, aparte de Python y Flask.</span><span class="sxs-lookup"><span data-stu-id="db5f8-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="db5f8-222">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="db5f8-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="db5f8-223">Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="db5f8-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="db5f8-224">Asegúrese de que requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="db5f8-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="db5f8-225">Confirmar cambios de hello:</span><span class="sxs-lookup"><span data-stu-id="db5f8-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="db5f8-226">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="db5f8-226">Deploy tooAzure</span></span>
<span data-ttu-id="db5f8-227">una implementación de tootrigger, Hola de inserción cambia tooAzure:</span><span class="sxs-lookup"><span data-stu-id="db5f8-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="db5f8-228">Se obtiene un resultado de hello del script de implementación de hello, incluida la creación del entorno virtual, instalación de paquetes, la creación del archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="db5f8-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="db5f8-229">Examinar los cambios de toohello tooview de dirección URL de Azure.</span><span class="sxs-lookup"><span data-stu-id="db5f8-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="db5f8-230">Desarrollo de aplicaciones web: Mac/Linux - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="db5f8-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="db5f8-231">Repositorio de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="db5f8-231">Clone hello repository</span></span>
<span data-ttu-id="db5f8-232">En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure y agregar hello Azure repositorio como un control remoto.</span><span class="sxs-lookup"><span data-stu-id="db5f8-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="db5f8-233">Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="db5f8-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="db5f8-234">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="db5f8-234">Create virtual environment</span></span>
<span data-ttu-id="db5f8-235">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue toohello repositorio).</span><span class="sxs-lookup"><span data-stu-id="db5f8-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="db5f8-236">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación hello creará su propias localmente.</span><span class="sxs-lookup"><span data-stu-id="db5f8-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="db5f8-237">Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello **configuración de la aplicación** hoja de la aplicación web en hello Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="db5f8-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="db5f8-238">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="db5f8-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="db5f8-239">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="db5f8-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="db5f8-240">o pyvenv env</span><span class="sxs-lookup"><span data-stu-id="db5f8-240">or pyvenv env</span></span>

<span data-ttu-id="db5f8-241">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db5f8-241">Install any external packages required by your application.</span></span> <span data-ttu-id="db5f8-242">Puede usar el archivo de requirements.txt de hello en raíz de Hola de paquetes de saludo repositorio tooinstall hello en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="db5f8-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="db5f8-243">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="db5f8-243">Run using development server</span></span>
<span data-ttu-id="db5f8-244">Puede iniciar la aplicación hello en un servidor de desarrollo con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="db5f8-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="db5f8-245">consola de Hola mostrará la dirección URL de Hola y escucha servidor hello de puertos:</span><span class="sxs-lookup"><span data-stu-id="db5f8-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="db5f8-246">A continuación, abra la dirección URL toothat del explorador web.</span><span class="sxs-lookup"><span data-stu-id="db5f8-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="db5f8-247">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="db5f8-247">Make changes</span></span>
<span data-ttu-id="db5f8-248">Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.</span><span class="sxs-lookup"><span data-stu-id="db5f8-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="db5f8-249">Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="db5f8-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="db5f8-250">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="db5f8-250">Install more packages</span></span>
<span data-ttu-id="db5f8-251">La aplicación puede tener otras dependencias, aparte de Python y Flask.</span><span class="sxs-lookup"><span data-stu-id="db5f8-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="db5f8-252">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="db5f8-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="db5f8-253">Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="db5f8-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="db5f8-254">Asegúrese de que requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="db5f8-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="db5f8-255">Confirmar cambios de hello:</span><span class="sxs-lookup"><span data-stu-id="db5f8-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="db5f8-256">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="db5f8-256">Deploy tooAzure</span></span>
<span data-ttu-id="db5f8-257">una implementación de tootrigger, Hola de inserción cambia tooAzure:</span><span class="sxs-lookup"><span data-stu-id="db5f8-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="db5f8-258">Se obtiene un resultado de hello del script de implementación de hello, incluida la creación del entorno virtual, instalación de paquetes, la creación del archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="db5f8-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="db5f8-259">Examinar los cambios de toohello tooview de dirección URL de Azure.</span><span class="sxs-lookup"><span data-stu-id="db5f8-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="db5f8-260">Solución de problemas - Instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="db5f8-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="db5f8-261">Solución de problemas - Entorno virtual</span><span class="sxs-lookup"><span data-stu-id="db5f8-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="db5f8-262">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db5f8-262">Next Steps</span></span>
<span data-ttu-id="db5f8-263">Siga estos toolearn de vínculos más sobre matraz y Python Tools para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="db5f8-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="db5f8-264">[Documentación de Flask]</span><span class="sxs-lookup"><span data-stu-id="db5f8-264">[Flask Documentation]</span></span>
* <span data-ttu-id="db5f8-265">[Python Tools para la documentación de Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="db5f8-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="db5f8-266">Para obtener información sobre el uso de Almacenamiento de tablas de Azure y MongoDB:</span><span class="sxs-lookup"><span data-stu-id="db5f8-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="db5f8-267">[Flask y MongoDB en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="db5f8-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="db5f8-268">[Flask y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="db5f8-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="db5f8-269">Para obtener más información, vea también hello [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="db5f8-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="db5f8-270">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="db5f8-270">What's changed</span></span>
* <span data-ttu-id="db5f8-271">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="db5f8-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Flask y MongoDB en Azure con Python Tools para Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask y Almacenamiento de tablas de Azure en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[Azure SDK para Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK para Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git para Windows]: http://msysgit.github.io/
[GitHub para Windows]: https://windows.github.com/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python Tools para la documentación de Visual Studio]: http://aka.ms/ptvsdocs
[Documentación de Flask]: http://flask.pocoo.org/ 

