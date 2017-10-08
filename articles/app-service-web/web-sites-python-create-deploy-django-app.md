---
title: aplicaciones web aaaCreating con Django en Azure
description: "Un tutorial que le presenta toorunning una aplicación web de Python en aplicaciones de Web del servicio de aplicación de Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="f343c-103">Creación de aplicaciones web con Django en Azure</span><span class="sxs-lookup"><span data-stu-id="f343c-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="f343c-104">Este tutorial describe cómo tooget empezó a ejecutarse Python [aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f343c-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f343c-105">Aplicaciones web ofrece hospedaje gratuito limitado y una implementación rápida. Además, ahora también se puede usar Python.</span><span class="sxs-lookup"><span data-stu-id="f343c-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="f343c-106">Medida que crezca su aplicación, puede cambiar toopaid de hospedaje y también se puede integrar con todos Hola otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="f343c-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="f343c-107">Se creará una aplicación con el marco de trabajo de hello Django web (vea versiones alternativas de este tutorial para [matraz](web-sites-python-create-deploy-flask-app.md) y [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="f343c-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="f343c-108">Se crear una aplicación web de Hola de hello Azure Marketplace, configurar la implementación de Git y clonar el repositorio de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="f343c-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="f343c-109">A continuación, se ejecuta la aplicación hello localmente, realizar cambios, confirmar e insertarlas tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f343c-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="f343c-110">Hola tutorial se muestra cómo toodo de Windows o Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="f343c-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f343c-111">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f343c-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f343c-112">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="f343c-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f343c-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f343c-113">Prerequisites</span></span>
* <span data-ttu-id="f343c-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="f343c-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="f343c-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="f343c-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="f343c-116">setuptools, pip, virtualenv (solo en Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="f343c-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="f343c-117">Git</span><span class="sxs-lookup"><span data-stu-id="f343c-117">Git</span></span>
* <span data-ttu-id="f343c-118">[Python Tools para Visual Studio][Python Tools para Visual Studio] (PTVS)- Nota: Esto es opcional</span><span class="sxs-lookup"><span data-stu-id="f343c-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="f343c-119">**Nota:**la publicación TFS no se admite actualmente para los proyectos de Python.</span><span class="sxs-lookup"><span data-stu-id="f343c-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="f343c-120">Windows</span><span class="sxs-lookup"><span data-stu-id="f343c-120">Windows</span></span>
<span data-ttu-id="f343c-121">Si aún no tiene Python 2.7 o 3.4 instalado (32 bits), se recomienda instalar [Azure SDK para Python 2.7] o [Azure SDK para Python 3.4] mediante el instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="f343c-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="f343c-122">Esto instala la versión de 32 bits de Hola de Python, setuptools, pip, virtualenv, etcetera (32-bit Python es lo que se instala en equipos de host de Azure de hello).</span><span class="sxs-lookup"><span data-stu-id="f343c-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="f343c-123">También puede obtener Python en [python.org].</span><span class="sxs-lookup"><span data-stu-id="f343c-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="f343c-124">Para Git, recomendamos [Git para Windows] o [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="f343c-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="f343c-125">Si utiliza Visual Studio, puede usar soporte técnico de Git de hello integrado.</span><span class="sxs-lookup"><span data-stu-id="f343c-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="f343c-126">También se recomienda instalar [Python Tools 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f343c-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="f343c-127">Esto es opcional, pero si tiene [Visual Studio], incluidos Hola liberar Visual Studio Community 2013 o Visual Studio Express 2013 para Web, a continuación, esto le proporcionará un excelente IDE de Python.</span><span class="sxs-lookup"><span data-stu-id="f343c-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="f343c-128">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="f343c-128">Mac/Linux</span></span>
<span data-ttu-id="f343c-129">Debe tener Python y Git instalados, pero asegúrese de que tiene Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="f343c-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="f343c-130">Creación de la aplicación web en el Portal</span><span class="sxs-lookup"><span data-stu-id="f343c-130">Web App Creation on Portal</span></span>
<span data-ttu-id="f343c-131">primer paso para crear la aplicación Hello es toocreate hello web app mediante hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f343c-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="f343c-132">Inicie sesión en hello Portal de Azure y haga clic en hello **NEW** botón en la esquina izquierda inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="f343c-133">En el cuadro de búsqueda de hello, escriba "python".</span><span class="sxs-lookup"><span data-stu-id="f343c-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="f343c-134">En los resultados de la búsqueda de hello, seleccione **Django** (publicado por PTVS), a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="f343c-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="f343c-135">Configurar aplicación de Django nueva hello, como la creación de un nuevo plan de servicio de aplicaciones y un nuevo grupo de recursos para el mismo.</span><span class="sxs-lookup"><span data-stu-id="f343c-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="f343c-136">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f343c-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="f343c-137">Configurar la publicación de Git de la aplicación web recién creado siguiendo las instrucciones de hello en [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f343c-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="f343c-138">Información general de la aplicación</span><span class="sxs-lookup"><span data-stu-id="f343c-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="f343c-139">Contenido del repositorio de Git</span><span class="sxs-lookup"><span data-stu-id="f343c-139">Git repository contents</span></span>
<span data-ttu-id="f343c-140">Esta es una visión general de los archivos de Hola que encontrará en el repositorio de Git inicial hello, que se podrá clonar en la sección siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="f343c-141">Orígenes principales de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f343c-141">Main sources for hello application.</span></span> <span data-ttu-id="f343c-142">Consta de tres páginas (índice, acerca de, contacto) con un diseño principal.</span><span class="sxs-lookup"><span data-stu-id="f343c-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="f343c-143">El contenido estático y los scripts incluyen bootstrap, jquery, modernizr y respond.</span><span class="sxs-lookup"><span data-stu-id="f343c-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="f343c-144">Compatibilidad con administración local y con servidor de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="f343c-144">Local management and development server support.</span></span> <span data-ttu-id="f343c-145">Use esta aplicación de hello toorun localmente, sincronizar la base de datos de hello, etcetera.</span><span class="sxs-lookup"><span data-stu-id="f343c-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="f343c-146">Base de datos predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f343c-146">Default database.</span></span> <span data-ttu-id="f343c-147">Incluye tablas necesarias de Hola para hello toorun de aplicación, pero no contiene ningún usuario (sincronizar hello toocreate de base de datos un usuario).</span><span class="sxs-lookup"><span data-stu-id="f343c-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="f343c-148">Archivos de proyecto para su uso con [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f343c-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="f343c-149">Proxy IIS para entornos virtuales y compatibilidad con la depuración remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="f343c-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="f343c-150">Paquetes externos necesarios para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="f343c-150">External packages needed by this application.</span></span> <span data-ttu-id="f343c-151">script de implementación de Hola pip paquetes de Hola de instalación incluidos en este archivo.</span><span class="sxs-lookup"><span data-stu-id="f343c-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="f343c-152">Archivos de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="f343c-152">IIS configuration files.</span></span> <span data-ttu-id="f343c-153">script de implementación de Hello usará web.x.y.config adecuado de Hola y copiar como web.config.</span><span class="sxs-lookup"><span data-stu-id="f343c-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="f343c-154">Archivos opcionales - Implementación de personalización</span><span class="sxs-lookup"><span data-stu-id="f343c-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="f343c-155">Archivos opcionales - Tiempo de ejecución de Python</span><span class="sxs-lookup"><span data-stu-id="f343c-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="f343c-156">Archivos adicionales en el servidor</span><span class="sxs-lookup"><span data-stu-id="f343c-156">Additional files on server</span></span>
<span data-ttu-id="f343c-157">Algunos archivos existen en el servidor de hello pero no se agregan toohello repositorio de git.</span><span class="sxs-lookup"><span data-stu-id="f343c-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="f343c-158">Estos se crean mediante el script de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="f343c-159">Archivo de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="f343c-159">IIS configuration file.</span></span> <span data-ttu-id="f343c-160">Se crea desde web.x.y.config en cada implementación.</span><span class="sxs-lookup"><span data-stu-id="f343c-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="f343c-161">Entorno virtual de Python.</span><span class="sxs-lookup"><span data-stu-id="f343c-161">Python virtual environment.</span></span> <span data-ttu-id="f343c-162">Si aún no existe un entorno virtual compatible en la aplicación web de hello, creados durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="f343c-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="f343c-163">Paquetes incluidos en requirements.txt son pip instalado, pero pip omitirá la instalación si ya se han instalado paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="f343c-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="f343c-164">Hello 3 secciones describen cómo tooproceed con hello web desarrollo de aplicaciones en 3 entornos diferentes:</span><span class="sxs-lookup"><span data-stu-id="f343c-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="f343c-165">Windows, con Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f343c-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="f343c-166">Windows, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="f343c-166">Windows, with command line</span></span>
* <span data-ttu-id="f343c-167">Mac/Linux, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="f343c-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="f343c-168">Desarrollo de aplicaciones web: Windows, Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f343c-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f343c-169">Repositorio de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="f343c-169">Clone hello repository</span></span>
<span data-ttu-id="f343c-170">En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f343c-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="f343c-171">Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f343c-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="f343c-172">Hola abrir archivo de solución (.sln) que se incluye en la raíz de hello del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="f343c-173">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="f343c-173">Create virtual environment</span></span>
<span data-ttu-id="f343c-174">Ahora vamos a crear un entorno virtual para el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="f343c-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="f343c-175">Haga clic con el botón secundario en **Entornos de Python** y elija **Agregar entorno virtual...**</span><span class="sxs-lookup"><span data-stu-id="f343c-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="f343c-176">Asegúrese de que nombre hello del entorno de hello es `env`.</span><span class="sxs-lookup"><span data-stu-id="f343c-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="f343c-177">Seleccione intérprete base Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-177">Select hello base interpreter.</span></span> <span data-ttu-id="f343c-178">Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello **configuración de la aplicación** hoja de la aplicación web en hello Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="f343c-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="f343c-179">Asegúrese de que esté marcada Hola opción toodownload e instalar los paquetes.</span><span class="sxs-lookup"><span data-stu-id="f343c-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="f343c-180">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f343c-180">Click **Create**.</span></span> <span data-ttu-id="f343c-181">Esto se crear entorno virtual de hello e instalar las dependencias en requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f343c-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="f343c-182">Creación de un superusuario</span><span class="sxs-lookup"><span data-stu-id="f343c-182">Create a superuser</span></span>
<span data-ttu-id="f343c-183">base de datos de Hello incluida con la aplicación hello no tiene superusuario definido.</span><span class="sxs-lookup"><span data-stu-id="f343c-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f343c-184">En la orden toouse Hola inicio de sesión de funcionalidad de aplicación hello o interfaz de administración de hello Django (si decide tooenable lo), deberá toocreate un superusuario.</span><span class="sxs-lookup"><span data-stu-id="f343c-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f343c-185">Ejecute lo siguiente desde Hola de línea de comandos de la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="f343c-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f343c-186">Siga Hola indicaciones tooset Hola nombre de usuario, contraseña, etcetera.</span><span class="sxs-lookup"><span data-stu-id="f343c-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f343c-187">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="f343c-187">Run using development server</span></span>
<span data-ttu-id="f343c-188">Presione F5 toostart depuración y el explorador web abrirá automáticamente página toohello que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="f343c-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="f343c-189">Puede establecer puntos de interrupción en orígenes de hello, las ventanas de inspección de uso hello, etcetera. Vea hello [Python Tools para la documentación de Visual Studio] para obtener más información sobre Hola distintas características.</span><span class="sxs-lookup"><span data-stu-id="f343c-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="f343c-190">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="f343c-190">Make changes</span></span>
<span data-ttu-id="f343c-191">Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.</span><span class="sxs-lookup"><span data-stu-id="f343c-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f343c-192">Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="f343c-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="f343c-193">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="f343c-193">Install more packages</span></span>
<span data-ttu-id="f343c-194">La aplicación puede tener otras dependencias, aparte de Python y Django.</span><span class="sxs-lookup"><span data-stu-id="f343c-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f343c-195">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="f343c-195">You can install additional packages using pip.</span></span> <span data-ttu-id="f343c-196">tooinstall un paquete, haga doble clic en entorno virtual de Hola y seleccione **instalar un paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="f343c-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="f343c-197">Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba `azure`:</span><span class="sxs-lookup"><span data-stu-id="f343c-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="f343c-198">Haga doble clic en el entorno virtual de Hola y seleccione **generar requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f343c-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="f343c-199">A continuación, confirmar el repositorio de Git de hello cambios toorequirements.txt toohello.</span><span class="sxs-lookup"><span data-stu-id="f343c-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="f343c-200">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="f343c-200">Deploy tooAzure</span></span>
<span data-ttu-id="f343c-201">tootrigger una implementación, haga clic en **sincronización** o **Push**.</span><span class="sxs-lookup"><span data-stu-id="f343c-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="f343c-202">La sincronización realiza una inserción y una extracción.</span><span class="sxs-lookup"><span data-stu-id="f343c-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="f343c-203">primera implementación de Hello tardará algún tiempo, tal y como se va a crear un entorno virtual, paquetes de instalación, etcetera.</span><span class="sxs-lookup"><span data-stu-id="f343c-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="f343c-204">Visual Studio no muestra el progreso de Hola de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="f343c-205">Si desea que la salida de hello tooreview, vea la sección Hola en [solución de problemas - implementación](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="f343c-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="f343c-206">Examinar los cambios de toohello tooview de dirección URL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f343c-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="f343c-207">Desarrollo de aplicaciones web - Windows - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="f343c-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f343c-208">Repositorio de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="f343c-208">Clone hello repository</span></span>
<span data-ttu-id="f343c-209">En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure y agregar hello Azure repositorio como un control remoto.</span><span class="sxs-lookup"><span data-stu-id="f343c-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f343c-210">Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f343c-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f343c-211">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="f343c-211">Create virtual environment</span></span>
<span data-ttu-id="f343c-212">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue toohello repositorio).</span><span class="sxs-lookup"><span data-stu-id="f343c-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="f343c-213">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación hello creará su propias localmente.</span><span class="sxs-lookup"><span data-stu-id="f343c-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f343c-214">Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello hoja de configuración de la aplicación de la aplicación web en hello Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="f343c-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f343c-215">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f343c-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="f343c-216">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f343c-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="f343c-217">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f343c-217">Install any external packages required by your application.</span></span> <span data-ttu-id="f343c-218">Puede usar el archivo de requirements.txt de hello en raíz de Hola de paquetes de saludo repositorio tooinstall hello en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="f343c-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f343c-219">Creación de un superusuario</span><span class="sxs-lookup"><span data-stu-id="f343c-219">Create a superuser</span></span>
<span data-ttu-id="f343c-220">base de datos de Hello incluida con la aplicación hello no tiene superusuario definido.</span><span class="sxs-lookup"><span data-stu-id="f343c-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f343c-221">En la orden toouse Hola inicio de sesión de funcionalidad de aplicación hello o interfaz de administración de hello Django (si decide tooenable lo), deberá toocreate un superusuario.</span><span class="sxs-lookup"><span data-stu-id="f343c-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f343c-222">Ejecute lo siguiente desde Hola de línea de comandos de la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="f343c-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f343c-223">Siga Hola indicaciones tooset Hola nombre de usuario, contraseña, etcetera.</span><span class="sxs-lookup"><span data-stu-id="f343c-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f343c-224">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="f343c-224">Run using development server</span></span>
<span data-ttu-id="f343c-225">Puede iniciar la aplicación hello en un servidor de desarrollo con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f343c-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="f343c-226">consola de Hola mostrará la dirección URL de Hola y escucha servidor hello de puertos:</span><span class="sxs-lookup"><span data-stu-id="f343c-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="f343c-227">A continuación, abra la dirección URL toothat del explorador web.</span><span class="sxs-lookup"><span data-stu-id="f343c-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f343c-228">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="f343c-228">Make changes</span></span>
<span data-ttu-id="f343c-229">Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.</span><span class="sxs-lookup"><span data-stu-id="f343c-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f343c-230">Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="f343c-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f343c-231">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="f343c-231">Install more packages</span></span>
<span data-ttu-id="f343c-232">La aplicación puede tener otras dependencias, aparte de Python y Django.</span><span class="sxs-lookup"><span data-stu-id="f343c-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f343c-233">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="f343c-233">You can install additional packages using pip.</span></span> <span data-ttu-id="f343c-234">Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="f343c-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="f343c-235">Asegúrese de que requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="f343c-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="f343c-236">Confirmar cambios de hello:</span><span class="sxs-lookup"><span data-stu-id="f343c-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f343c-237">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="f343c-237">Deploy tooAzure</span></span>
<span data-ttu-id="f343c-238">una implementación de tootrigger, Hola de inserción cambia tooAzure:</span><span class="sxs-lookup"><span data-stu-id="f343c-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f343c-239">Se obtiene un resultado de hello del script de implementación de hello, incluida la creación del entorno virtual, instalación de paquetes, la creación del archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="f343c-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f343c-240">Examinar los cambios de toohello tooview de dirección URL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f343c-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="f343c-241">Desarrollo de aplicaciones web: Mac/Linux - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="f343c-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f343c-242">Repositorio de Hola de clon</span><span class="sxs-lookup"><span data-stu-id="f343c-242">Clone hello repository</span></span>
<span data-ttu-id="f343c-243">En primer lugar, clonar el repositorio de hello mediante dirección URL de hello proporcionada en hello Portal de Azure y agregar hello Azure repositorio como un control remoto.</span><span class="sxs-lookup"><span data-stu-id="f343c-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f343c-244">Para obtener más información, consulte [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f343c-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f343c-245">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="f343c-245">Create virtual environment</span></span>
<span data-ttu-id="f343c-246">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue toohello repositorio).</span><span class="sxs-lookup"><span data-stu-id="f343c-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="f343c-247">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación hello creará su propias localmente.</span><span class="sxs-lookup"><span data-stu-id="f343c-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f343c-248">Asegúrese de que toouse Hola la misma versión de Python que está seleccionada para la aplicación web (en runtime.txt o hello hoja de configuración de la aplicación de la aplicación web en hello Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="f343c-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f343c-249">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f343c-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="f343c-250">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f343c-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="f343c-251">o</span><span class="sxs-lookup"><span data-stu-id="f343c-251">or</span></span>

    pyvenv env

<span data-ttu-id="f343c-252">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f343c-252">Install any external packages required by your application.</span></span> <span data-ttu-id="f343c-253">Puede usar el archivo de requirements.txt de hello en raíz de Hola de paquetes de saludo repositorio tooinstall hello en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="f343c-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f343c-254">Creación de un superusuario</span><span class="sxs-lookup"><span data-stu-id="f343c-254">Create a superuser</span></span>
<span data-ttu-id="f343c-255">base de datos de Hello incluida con la aplicación hello no tiene superusuario definido.</span><span class="sxs-lookup"><span data-stu-id="f343c-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f343c-256">En la orden toouse Hola inicio de sesión de funcionalidad de aplicación hello o interfaz de administración de hello Django (si decide tooenable lo), deberá toocreate un superusuario.</span><span class="sxs-lookup"><span data-stu-id="f343c-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f343c-257">Ejecute lo siguiente desde Hola de línea de comandos de la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="f343c-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="f343c-258">Siga Hola indicaciones tooset Hola nombre de usuario, contraseña, etcetera.</span><span class="sxs-lookup"><span data-stu-id="f343c-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f343c-259">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="f343c-259">Run using development server</span></span>
<span data-ttu-id="f343c-260">Puede iniciar la aplicación hello en un servidor de desarrollo con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f343c-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="f343c-261">consola de Hola mostrará la dirección URL de Hola y escucha servidor hello de puertos:</span><span class="sxs-lookup"><span data-stu-id="f343c-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="f343c-262">A continuación, abra la dirección URL toothat del explorador web.</span><span class="sxs-lookup"><span data-stu-id="f343c-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f343c-263">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="f343c-263">Make changes</span></span>
<span data-ttu-id="f343c-264">Ahora puede experimentar realizando cambios toohello aplicación orígenes o plantillas.</span><span class="sxs-lookup"><span data-stu-id="f343c-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f343c-265">Después de haberlo probado los cambios, confirmarlos toohello repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="f343c-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f343c-266">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="f343c-266">Install more packages</span></span>
<span data-ttu-id="f343c-267">La aplicación puede tener otras dependencias, aparte de Python y Django.</span><span class="sxs-lookup"><span data-stu-id="f343c-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f343c-268">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="f343c-268">You can install additional packages using pip.</span></span> <span data-ttu-id="f343c-269">Por ejemplo, tooinstall hello Azure SDK para Python, que proporciona acceso tooAzure almacenamiento, bus de servicio y otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="f343c-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="f343c-270">Asegúrese de que requirements.txt tooupdate:</span><span class="sxs-lookup"><span data-stu-id="f343c-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="f343c-271">Confirmar cambios de hello:</span><span class="sxs-lookup"><span data-stu-id="f343c-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f343c-272">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="f343c-272">Deploy tooAzure</span></span>
<span data-ttu-id="f343c-273">una implementación de tootrigger, Hola de inserción cambia tooAzure:</span><span class="sxs-lookup"><span data-stu-id="f343c-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f343c-274">Se obtiene un resultado de hello del script de implementación de hello, incluida la creación del entorno virtual, instalación de paquetes, la creación del archivo web.config.</span><span class="sxs-lookup"><span data-stu-id="f343c-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f343c-275">Examinar los cambios de toohello tooview de dirección URL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f343c-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="f343c-276">Solución de problemas - Instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="f343c-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="f343c-277">Solución de problemas - Entorno virtual</span><span class="sxs-lookup"><span data-stu-id="f343c-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="f343c-278">Solución de problemas - Archivos estáticos</span><span class="sxs-lookup"><span data-stu-id="f343c-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="f343c-279">Django tiene el concepto de Hola de recopilación de archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="f343c-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="f343c-280">Esto tiene todos los archivos estáticos Hola desde su ubicación original y los copia tooa única carpeta.</span><span class="sxs-lookup"><span data-stu-id="f343c-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="f343c-281">Para esta aplicación, se copian demasiado`/static`.</span><span class="sxs-lookup"><span data-stu-id="f343c-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="f343c-282">Esto se realiza porque los archivos estáticos pueden proceder de otras aplicaciones Django diferentes.</span><span class="sxs-lookup"><span data-stu-id="f343c-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="f343c-283">Por ejemplo, archivos estáticos de Hola de interfaces de administración de hello Django se encuentran en una subcarpeta de la biblioteca de Django en el entorno virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="f343c-284">Los archivos estáticos definidos por esta aplicación se encuentran en `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="f343c-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="f343c-285">Cuantas más aplicaciones Django se utilicen, tendrá archivos estáticos ubicados en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="f343c-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="f343c-286">Cuando se ejecuta la aplicación hello en modo de depuración, aplicación hello sirve archivos estáticos de Hola desde su ubicación original.</span><span class="sxs-lookup"><span data-stu-id="f343c-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="f343c-287">Cuando se ejecuta la aplicación hello en modo de lanzamiento, aplicación de hello hace **no** servir archivos estáticos Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="f343c-288">Es responsabilidad de Hola de archivos del servidor de hello web tooserve Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="f343c-289">Para esta aplicación, IIS servirá archivos estáticos de Hola desde `/static`.</span><span class="sxs-lookup"><span data-stu-id="f343c-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="f343c-290">colección de Hola de archivos estáticos se realiza automáticamente como parte del script de implementación de hello, borrar previamente recopilado archivos.</span><span class="sxs-lookup"><span data-stu-id="f343c-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="f343c-291">Esto significa Hola recolección se produce en cada implementación, ralentizar implementación un poco, pero garantiza que los archivos obsoletos no estarán disponibles, evitar un posible riesgo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f343c-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="f343c-292">Si desea tooskip colección de archivos estáticos de la aplicación Django:</span><span class="sxs-lookup"><span data-stu-id="f343c-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="f343c-293">A continuación, necesitará colección de hello toodo manualmente en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="f343c-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="f343c-294">A continuación, quite hello `\static` carpeta desde `.gitignore` y Agregar repositorio de Git toohello.</span><span class="sxs-lookup"><span data-stu-id="f343c-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="f343c-295">Solución de problemas - Configuración</span><span class="sxs-lookup"><span data-stu-id="f343c-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="f343c-296">Distintas configuraciones para la aplicación hello pueden cambiarse en `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="f343c-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="f343c-297">Para mayor comodidad del desarrollador, se habilita el modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="f343c-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="f343c-298">Un efecto secundario "nice" de la es que estará toosee capaz de imágenes y otro contenido estático cuando se ejecuta localmente, sin necesidad de toocollect de archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="f343c-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="f343c-299">modo de depuración de toodisable:</span><span class="sxs-lookup"><span data-stu-id="f343c-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="f343c-300">Cuando se deshabilita la depuración, Hola valor para `ALLOWED_HOSTS` necesidades toobe actualiza el nombre de host de Azure de tooinclude Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="f343c-301">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f343c-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="f343c-302">o tooenable cualquier:</span><span class="sxs-lookup"><span data-stu-id="f343c-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="f343c-303">En la práctica, puede que desee toodo algo más compleja toodeal con cambiar entre depurar y liberar el modo y obtener nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="f343c-304">Se pueden establecer variables de entorno a través del portal de Azure de hello **configurar** página Hola **configuración de la aplicación** sección.</span><span class="sxs-lookup"><span data-stu-id="f343c-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="f343c-305">Esto puede ser útil para establecer los valores que no puede ser conveniente tooappear en orígenes de hello (las cadenas de conexión, las contraseñas, etcetera), o que quiere tooset diferente entre Azure y el equipo local.</span><span class="sxs-lookup"><span data-stu-id="f343c-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="f343c-306">En `settings.py`, puede consultar las variables de entorno de hello mediante `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="f343c-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="f343c-307">Uso de una base de datos</span><span class="sxs-lookup"><span data-stu-id="f343c-307">Using a Database</span></span>
<span data-ttu-id="f343c-308">base de datos de Hola que se incluye con la aplicación hello es una base de datos de sqlite.</span><span class="sxs-lookup"><span data-stu-id="f343c-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="f343c-309">Se trata de un toouse de base de datos predeterminada cómodo y útil para el desarrollo, ya que no requiere casi ningún programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="f343c-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="f343c-310">base de datos de Hola se almacena en el archivo db.sqlite3 de hello en la carpeta del proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="f343c-311">Azure proporciona servicios de base de datos que son toouse fácil desde una aplicación de Django.</span><span class="sxs-lookup"><span data-stu-id="f343c-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="f343c-312">Tutoriales para el uso de [base de datos SQL] y [MySQL] desde una aplicación de Django mostrar pasos Hola servicio de base de datos de hello toocreate es necesario, cambiar la configuración de la base de datos de hello en `DjangoWebProject/settings.py`, hello y bibliotecas tooinstall necesarios.</span><span class="sxs-lookup"><span data-stu-id="f343c-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="f343c-313">Por supuesto, si lo prefiere toomanage sus propios servidores de base de datos, puede hacerlo con máquinas virtuales Windows o Linux que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="f343c-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="f343c-314">Interfaz de administración de Django</span><span class="sxs-lookup"><span data-stu-id="f343c-314">Django Admin Interface</span></span>
<span data-ttu-id="f343c-315">Cuando se empieza a generar los modelos, le interesará base de datos de toopopulate Hola con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="f343c-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="f343c-316">Una manera fácil toodo agregar y editar contenido de forma interactiva es interfaz de administración de Django toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="f343c-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="f343c-317">código de Hello para la interfaz de administración de hello está comentada en orígenes de la aplicación hello, pero está marcado claramente por lo que puede habilitar fácilmente lo (busque 'admin').</span><span class="sxs-lookup"><span data-stu-id="f343c-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="f343c-318">Una vez habilitada, sincronizar la base de datos de hello, ejecutar la aplicación hello y navegar demasiado`/admin`.</span><span class="sxs-lookup"><span data-stu-id="f343c-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f343c-319">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f343c-319">Next Steps</span></span>
<span data-ttu-id="f343c-320">Siga estos toolearn de vínculos más información acerca de Django y Python Tools para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f343c-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="f343c-321">[Documentación de Django]</span><span class="sxs-lookup"><span data-stu-id="f343c-321">[Django Documentation]</span></span>
* <span data-ttu-id="f343c-322">[Python Tools para la documentación de Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f343c-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="f343c-323">Para obtener información sobre el uso de Base de datos SQL y MySQL:</span><span class="sxs-lookup"><span data-stu-id="f343c-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="f343c-324">[Django y MySQL en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f343c-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="f343c-325">[Django y Base de datos SQL en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f343c-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="f343c-326">Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f343c-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f343c-327">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="f343c-327">What's changed</span></span>
* <span data-ttu-id="f343c-328">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f343c-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django y MySQL en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django y Base de datos SQL en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-django-sql.md
[base de datos SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Documentación de Django]: https://www.djangoproject.com/
