---
title: "Creación de aplicaciones web con Django en Azure"
description: "Un tutorial que indica cómo ejecutar una aplicación web de Python en Aplicacicones web del Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="c77da-103">Creación de aplicaciones web con Django en Azure</span><span class="sxs-lookup"><span data-stu-id="c77da-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="c77da-104">En este tutorial, se describe cómo empezar a ejecutar Python en [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c77da-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c77da-105">Aplicaciones web ofrece hospedaje gratuito limitado y una implementación rápida. Además, ahora también se puede usar Python.</span><span class="sxs-lookup"><span data-stu-id="c77da-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="c77da-106">A medida que su aplicación crece, puede cambiar a un tipo de hospedaje de pago e integrar el resto de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="c77da-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="c77da-107">Creará una aplicación con el marco web de Django (consulte las versiones alternativas de este tutorial para [Flask](web-sites-python-create-deploy-flask-app.md) y [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="c77da-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="c77da-108">Creará la aplicación web en Azure Marketplace, configurará la implementación Git y clonará el repositorio en modo local.</span><span class="sxs-lookup"><span data-stu-id="c77da-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="c77da-109">A continuación, ejecutará la aplicación localmente, realizará cambios, los confirmará y los insertará en Azure.</span><span class="sxs-lookup"><span data-stu-id="c77da-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="c77da-110">El tutorial muestra cómo llevarlo a cabo en Windows o Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="c77da-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="c77da-111">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c77da-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c77da-112">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="c77da-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c77da-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c77da-113">Prerequisites</span></span>
* <span data-ttu-id="c77da-114">Windows, Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="c77da-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="c77da-115">Python 2.7 o 3.4</span><span class="sxs-lookup"><span data-stu-id="c77da-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="c77da-116">setuptools, pip, virtualenv (solo en Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="c77da-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="c77da-117">Git</span><span class="sxs-lookup"><span data-stu-id="c77da-117">Git</span></span>
* <span data-ttu-id="c77da-118">[Python Tools para Visual Studio][Python Tools para Visual Studio] (PTVS)- Nota: Esto es opcional</span><span class="sxs-lookup"><span data-stu-id="c77da-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="c77da-119">**Nota:**la publicación TFS no se admite actualmente para los proyectos de Python.</span><span class="sxs-lookup"><span data-stu-id="c77da-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="c77da-120">Windows</span><span class="sxs-lookup"><span data-stu-id="c77da-120">Windows</span></span>
<span data-ttu-id="c77da-121">Si aún no tiene Python 2.7 o 3.4 instalado (32 bits), se recomienda instalar [Azure SDK para Python 2.7] o [Azure SDK para Python 3.4] mediante el instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="c77da-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="c77da-122">Se instala la versión de 32 bits de Python, setuptools, pip, virtualenv, etc. (Python de 32 bits es lo que se instala en los equipos host de Azure).</span><span class="sxs-lookup"><span data-stu-id="c77da-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="c77da-123">También puede obtener Python en [python.org].</span><span class="sxs-lookup"><span data-stu-id="c77da-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="c77da-124">Para Git, recomendamos [Git para Windows] o [GitHub para Windows].</span><span class="sxs-lookup"><span data-stu-id="c77da-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="c77da-125">Si utiliza Visual Studio, puede utilizar la compatibilidad integrada con Git.</span><span class="sxs-lookup"><span data-stu-id="c77da-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="c77da-126">También se recomienda instalar [Python Tools 2.2 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c77da-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="c77da-127">Esto es opcional, pero si tiene [Visual Studio], incluidas las versiones gratuitas Visual Studio Community 2013 o Visual Studio Express 2013 para web, obtendrá un excelente IDE de Python.</span><span class="sxs-lookup"><span data-stu-id="c77da-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="c77da-128">Mac o Linux:</span><span class="sxs-lookup"><span data-stu-id="c77da-128">Mac/Linux</span></span>
<span data-ttu-id="c77da-129">Debe tener Python y Git instalados, pero asegúrese de que tiene Python 2.7 o 3.4.</span><span class="sxs-lookup"><span data-stu-id="c77da-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="c77da-130">Creación de la aplicación web en el Portal</span><span class="sxs-lookup"><span data-stu-id="c77da-130">Web App Creation on Portal</span></span>
<span data-ttu-id="c77da-131">El primer paso para crear la aplicación consiste en crear la aplicación web a través del [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c77da-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="c77da-132">Inicie sesión en el Portal de Azure, haga clic en el botón **Nuevo** situado en la esquina inferior izquierda.</span><span class="sxs-lookup"><span data-stu-id="c77da-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="c77da-133">En el cuadro de búsqueda, escriba "python".</span><span class="sxs-lookup"><span data-stu-id="c77da-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="c77da-134">En los resultados de búsqueda, seleccione **Django** (publicado por PTVS) y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c77da-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="c77da-135">Configure la nueva aplicación Django, por ejemplo, la creación de un nuevo plan para el Servicio de aplicaciones y un nuevo grupo de recursos para él.</span><span class="sxs-lookup"><span data-stu-id="c77da-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="c77da-136">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c77da-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="c77da-137">Configure la publicación de Git para la aplicación web recién creada siguiendo las instrucciones que se describen en [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c77da-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="c77da-138">Información general de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c77da-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="c77da-139">Contenido del repositorio de Git</span><span class="sxs-lookup"><span data-stu-id="c77da-139">Git repository contents</span></span>
<span data-ttu-id="c77da-140">A continuación se muestra información general de los archivos que encontrará en el repositorio de Git inicial, que se va a clonar en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="c77da-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

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

<span data-ttu-id="c77da-141">Orígenes principales de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c77da-141">Main sources for the application.</span></span> <span data-ttu-id="c77da-142">Consta de tres páginas (índice, acerca de, contacto) con un diseño principal.</span><span class="sxs-lookup"><span data-stu-id="c77da-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="c77da-143">El contenido estático y los scripts incluyen bootstrap, jquery, modernizr y respond.</span><span class="sxs-lookup"><span data-stu-id="c77da-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="c77da-144">Compatibilidad con administración local y con servidor de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c77da-144">Local management and development server support.</span></span> <span data-ttu-id="c77da-145">Utilícelo para ejecutar la aplicación de manera local o sincronizar la base de datos, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c77da-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="c77da-146">Base de datos predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c77da-146">Default database.</span></span> <span data-ttu-id="c77da-147">Incluye las tablas necesarias para que se ejecute la aplicación, pero no contiene usuarios (sincronice la base de datos para crear un usuario).</span><span class="sxs-lookup"><span data-stu-id="c77da-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="c77da-148">Archivos de proyecto para su uso con [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c77da-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="c77da-149">Proxy IIS para entornos virtuales y compatibilidad con la depuración remota de PTVS.</span><span class="sxs-lookup"><span data-stu-id="c77da-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="c77da-150">Paquetes externos necesarios para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="c77da-150">External packages needed by this application.</span></span> <span data-ttu-id="c77da-151">El script de implementación instalará pip en los paquetes incluidos en este archivo.</span><span class="sxs-lookup"><span data-stu-id="c77da-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="c77da-152">Archivos de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="c77da-152">IIS configuration files.</span></span> <span data-ttu-id="c77da-153">El script de implementación utilizará el web.x.y.config adecuado y lo copiará como web.config.</span><span class="sxs-lookup"><span data-stu-id="c77da-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="c77da-154">Archivos opcionales - Implementación de personalización</span><span class="sxs-lookup"><span data-stu-id="c77da-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="c77da-155">Archivos opcionales - Tiempo de ejecución de Python</span><span class="sxs-lookup"><span data-stu-id="c77da-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="c77da-156">Archivos adicionales en el servidor</span><span class="sxs-lookup"><span data-stu-id="c77da-156">Additional files on server</span></span>
<span data-ttu-id="c77da-157">Algunos archivos existen en el servidor pero no se agregan al repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="c77da-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="c77da-158">Estos se crean mediante el script de implementación.</span><span class="sxs-lookup"><span data-stu-id="c77da-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="c77da-159">Archivo de configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="c77da-159">IIS configuration file.</span></span> <span data-ttu-id="c77da-160">Se crea desde web.x.y.config en cada implementación.</span><span class="sxs-lookup"><span data-stu-id="c77da-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="c77da-161">Entorno virtual de Python.</span><span class="sxs-lookup"><span data-stu-id="c77da-161">Python virtual environment.</span></span> <span data-ttu-id="c77da-162">Se crea durante la implementación si todavía no existe un entorno virtual compatible en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c77da-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="c77da-163">En los paquetes que aparecen en requirements.txt se instala pip, pero pip omitirá la instalación si los paquetes ya están instalados.</span><span class="sxs-lookup"><span data-stu-id="c77da-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="c77da-164">En las tres secciones siguientes se describe cómo continuar con el desarrollo de aplicaciones web en tres entornos diferentes:</span><span class="sxs-lookup"><span data-stu-id="c77da-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="c77da-165">Windows, con Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c77da-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="c77da-166">Windows, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="c77da-166">Windows, with command line</span></span>
* <span data-ttu-id="c77da-167">Mac/Linux, con línea de comandos</span><span class="sxs-lookup"><span data-stu-id="c77da-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="c77da-168">Desarrollo de aplicaciones web: Windows, Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c77da-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c77da-169">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="c77da-169">Clone the repository</span></span>
<span data-ttu-id="c77da-170">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c77da-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="c77da-171">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c77da-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="c77da-172">Abra el archivo de la solución (.sln) que se incluye en la raíz del repositorio.</span><span class="sxs-lookup"><span data-stu-id="c77da-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="c77da-173">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="c77da-173">Create virtual environment</span></span>
<span data-ttu-id="c77da-174">Ahora vamos a crear un entorno virtual para el desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="c77da-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="c77da-175">Haga clic con el botón secundario en **Entornos de Python** y elija **Agregar entorno virtual...**</span><span class="sxs-lookup"><span data-stu-id="c77da-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="c77da-176">Asegúrese de que el nombre del entorno sea `env`.</span><span class="sxs-lookup"><span data-stu-id="c77da-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="c77da-177">Seleccione el intérprete base.</span><span class="sxs-lookup"><span data-stu-id="c77da-177">Select the base interpreter.</span></span> <span data-ttu-id="c77da-178">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja **Configuración de la aplicación** de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="c77da-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="c77da-179">Asegúrese de que esté activada la opción para descargar e instalar paquetes.</span><span class="sxs-lookup"><span data-stu-id="c77da-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="c77da-180">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c77da-180">Click **Create**.</span></span> <span data-ttu-id="c77da-181">Esto creará el entorno virtual e instalará las dependencias mostradas en requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c77da-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="c77da-182">Creación de un superusuario</span><span class="sxs-lookup"><span data-stu-id="c77da-182">Create a superuser</span></span>
<span data-ttu-id="c77da-183">La base de datos incluida en la aplicación no dispone de superusuario definido.</span><span class="sxs-lookup"><span data-stu-id="c77da-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c77da-184">Para utilizar la funcionalidad de inicio de sesión en la aplicación o la interfaz de administración de Django (si opta por habilitarla), tendrá que crear un superusuario.</span><span class="sxs-lookup"><span data-stu-id="c77da-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c77da-185">Ejecute lo siguiente de la línea de comandos desde la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="c77da-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c77da-186">Siga las indicaciones para establecer el nombre de usuario o la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c77da-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c77da-187">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="c77da-187">Run using development server</span></span>
<span data-ttu-id="c77da-188">Presione F5 para iniciar la depuración y el explorador web abrirá automáticamente la página que se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="c77da-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="c77da-189">Puede establecer puntos de interrupción en los orígenes, utilizar las ventanas Inspección, etc. Consulte la [Documentación sobre Python Tools para Visual Studio] para obtener más información sobre las distintas características.</span><span class="sxs-lookup"><span data-stu-id="c77da-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="c77da-190">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="c77da-190">Make changes</span></span>
<span data-ttu-id="c77da-191">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c77da-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c77da-192">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="c77da-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="c77da-193">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="c77da-193">Install more packages</span></span>
<span data-ttu-id="c77da-194">La aplicación puede tener otras dependencias, aparte de Python y Django.</span><span class="sxs-lookup"><span data-stu-id="c77da-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c77da-195">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="c77da-195">You can install additional packages using pip.</span></span> <span data-ttu-id="c77da-196">Para instalar un paquete, haga clic con el botón secundario en el entorno virtual y elija **Instalar paquete de Python**.</span><span class="sxs-lookup"><span data-stu-id="c77da-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="c77da-197">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba `azure`:</span><span class="sxs-lookup"><span data-stu-id="c77da-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="c77da-198">Haga clic con el botón secundario en el entorno virtual y elija **Generar requirements.txt** para actualizar requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c77da-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="c77da-199">A continuación, confirme los cambios de requirements.txt en el repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="c77da-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="c77da-200">Implementar en Azure</span><span class="sxs-lookup"><span data-stu-id="c77da-200">Deploy to Azure</span></span>
<span data-ttu-id="c77da-201">Para desencadenar una implementación, haga clic en **Sincronizar** o **Insertar**.</span><span class="sxs-lookup"><span data-stu-id="c77da-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="c77da-202">La sincronización realiza una inserción y una extracción.</span><span class="sxs-lookup"><span data-stu-id="c77da-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="c77da-203">La primera implementación tardará algún tiempo, ya que crea un entorno virtual, paquetes de instalación, etc.</span><span class="sxs-lookup"><span data-stu-id="c77da-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="c77da-204">Visual Studio no muestra el progreso de la implementación.</span><span class="sxs-lookup"><span data-stu-id="c77da-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="c77da-205">Si desea revisar la salida, consulte la sección [Solución de problemas - Implementación](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="c77da-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="c77da-206">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="c77da-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="c77da-207">Desarrollo de aplicaciones web - Windows - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="c77da-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c77da-208">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="c77da-208">Clone the repository</span></span>
<span data-ttu-id="c77da-209">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure y agregue el repositorio de Azure como remoto.</span><span class="sxs-lookup"><span data-stu-id="c77da-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="c77da-210">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c77da-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c77da-211">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="c77da-211">Create virtual environment</span></span>
<span data-ttu-id="c77da-212">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue al repositorio).</span><span class="sxs-lookup"><span data-stu-id="c77da-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="c77da-213">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación creará su propio entorno localmente.</span><span class="sxs-lookup"><span data-stu-id="c77da-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="c77da-214">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja Configuración de la aplicación de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="c77da-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="c77da-215">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="c77da-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="c77da-216">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="c77da-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="c77da-217">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c77da-217">Install any external packages required by your application.</span></span> <span data-ttu-id="c77da-218">Puede utilizar el archivo requirements.txt en la raíz del repositorio para instalar los paquetes en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="c77da-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c77da-219">Creación de un superusuario</span><span class="sxs-lookup"><span data-stu-id="c77da-219">Create a superuser</span></span>
<span data-ttu-id="c77da-220">La base de datos incluida en la aplicación no dispone de superusuario definido.</span><span class="sxs-lookup"><span data-stu-id="c77da-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c77da-221">Para utilizar la funcionalidad de inicio de sesión en la aplicación o la interfaz de administración de Django (si opta por habilitarla), tendrá que crear un superusuario.</span><span class="sxs-lookup"><span data-stu-id="c77da-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c77da-222">Ejecute lo siguiente de la línea de comandos desde la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="c77da-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c77da-223">Siga las indicaciones para establecer el nombre de usuario o la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c77da-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c77da-224">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="c77da-224">Run using development server</span></span>
<span data-ttu-id="c77da-225">Puede iniciar la aplicación en un servidor de desarrollo con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c77da-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="c77da-226">La consola mostrará la dirección URL y el puerto al que escucha el servidor:</span><span class="sxs-lookup"><span data-stu-id="c77da-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="c77da-227">A continuación, abra el explorador web para esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="c77da-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c77da-228">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="c77da-228">Make changes</span></span>
<span data-ttu-id="c77da-229">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c77da-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c77da-230">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="c77da-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c77da-231">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="c77da-231">Install more packages</span></span>
<span data-ttu-id="c77da-232">La aplicación puede tener otras dependencias, aparte de Python y Django.</span><span class="sxs-lookup"><span data-stu-id="c77da-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c77da-233">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="c77da-233">You can install additional packages using pip.</span></span> <span data-ttu-id="c77da-234">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="c77da-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="c77da-235">Asegúrese de actualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c77da-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="c77da-236">Confirme los cambios:</span><span class="sxs-lookup"><span data-stu-id="c77da-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="c77da-237">Implementación en Azure</span><span class="sxs-lookup"><span data-stu-id="c77da-237">Deploy to Azure</span></span>
<span data-ttu-id="c77da-238">Para desencadenar una implementación, inserte los cambios en Azure:</span><span class="sxs-lookup"><span data-stu-id="c77da-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="c77da-239">Verá la salida del script de implementación, incluida la creación del entorno virtual, la instalación de paquetes y la creación de web.config.</span><span class="sxs-lookup"><span data-stu-id="c77da-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c77da-240">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="c77da-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="c77da-241">Desarrollo de aplicaciones web: Mac/Linux - Línea de comandos</span><span class="sxs-lookup"><span data-stu-id="c77da-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c77da-242">Clonación del repositorio</span><span class="sxs-lookup"><span data-stu-id="c77da-242">Clone the repository</span></span>
<span data-ttu-id="c77da-243">En primer lugar, clone el repositorio mediante la dirección URL proporcionada en el Portal de Azure y agregue el repositorio de Azure como remoto.</span><span class="sxs-lookup"><span data-stu-id="c77da-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="c77da-244">Para más información, consulte [Implementación de Git local en el Servicio de aplicaciones de Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c77da-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c77da-245">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="c77da-245">Create virtual environment</span></span>
<span data-ttu-id="c77da-246">Vamos a crear un nuevo entorno virtual para fines de desarrollo (no lo agregue al repositorio).</span><span class="sxs-lookup"><span data-stu-id="c77da-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="c77da-247">Los entornos virtuales de Python no son reubicables, por lo que cada desarrollador que trabaja en la aplicación creará su propio entorno localmente.</span><span class="sxs-lookup"><span data-stu-id="c77da-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="c77da-248">Asegúrese de utilizar la misma versión de Python que la seleccionada para la aplicación web (en runtime.txt o en la hoja Configuración de la aplicación de la aplicación web en el Portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="c77da-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="c77da-249">Para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="c77da-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="c77da-250">Para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="c77da-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="c77da-251">o</span><span class="sxs-lookup"><span data-stu-id="c77da-251">or</span></span>

    pyvenv env

<span data-ttu-id="c77da-252">Instale los paquetes externos requeridos por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c77da-252">Install any external packages required by your application.</span></span> <span data-ttu-id="c77da-253">Puede utilizar el archivo requirements.txt en la raíz del repositorio para instalar los paquetes en su entorno virtual:</span><span class="sxs-lookup"><span data-stu-id="c77da-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c77da-254">Creación de un superusuario</span><span class="sxs-lookup"><span data-stu-id="c77da-254">Create a superuser</span></span>
<span data-ttu-id="c77da-255">La base de datos incluida en la aplicación no dispone de superusuario definido.</span><span class="sxs-lookup"><span data-stu-id="c77da-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c77da-256">Para utilizar la funcionalidad de inicio de sesión en la aplicación o la interfaz de administración de Django (si opta por habilitarla), tendrá que crear un superusuario.</span><span class="sxs-lookup"><span data-stu-id="c77da-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c77da-257">Ejecute lo siguiente de la línea de comandos desde la carpeta del proyecto:</span><span class="sxs-lookup"><span data-stu-id="c77da-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="c77da-258">Siga las indicaciones para establecer el nombre de usuario o la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c77da-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c77da-259">Ejecución con el servidor de desarrollo</span><span class="sxs-lookup"><span data-stu-id="c77da-259">Run using development server</span></span>
<span data-ttu-id="c77da-260">Puede iniciar la aplicación en un servidor de desarrollo con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c77da-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="c77da-261">La consola mostrará la dirección URL y el puerto al que escucha el servidor:</span><span class="sxs-lookup"><span data-stu-id="c77da-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="c77da-262">A continuación, abra el explorador web para esa dirección URL.</span><span class="sxs-lookup"><span data-stu-id="c77da-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c77da-263">Realización de cambios</span><span class="sxs-lookup"><span data-stu-id="c77da-263">Make changes</span></span>
<span data-ttu-id="c77da-264">Ahora puede experimentar mediante la realización de cambios en los orígenes o plantillas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c77da-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c77da-265">Una vez probados los cambios, confírmelos en el repositorio de Git:</span><span class="sxs-lookup"><span data-stu-id="c77da-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c77da-266">Instalación de más paquetes</span><span class="sxs-lookup"><span data-stu-id="c77da-266">Install more packages</span></span>
<span data-ttu-id="c77da-267">La aplicación puede tener otras dependencias, aparte de Python y Django.</span><span class="sxs-lookup"><span data-stu-id="c77da-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c77da-268">Puede instalar paquetes adicionales con pip.</span><span class="sxs-lookup"><span data-stu-id="c77da-268">You can install additional packages using pip.</span></span> <span data-ttu-id="c77da-269">Por ejemplo, para instalar el SDK de Azure para Python, que proporciona acceso al almacenamiento de Azure, al bus de servicio y a otros servicios de Azure, escriba:</span><span class="sxs-lookup"><span data-stu-id="c77da-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="c77da-270">Asegúrese de actualizar requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="c77da-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="c77da-271">Confirme los cambios:</span><span class="sxs-lookup"><span data-stu-id="c77da-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="c77da-272">Implementación en Azure</span><span class="sxs-lookup"><span data-stu-id="c77da-272">Deploy to Azure</span></span>
<span data-ttu-id="c77da-273">Para desencadenar una implementación, inserte los cambios en Azure:</span><span class="sxs-lookup"><span data-stu-id="c77da-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="c77da-274">Verá la salida del script de implementación, incluida la creación del entorno virtual, la instalación de paquetes y la creación de web.config.</span><span class="sxs-lookup"><span data-stu-id="c77da-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c77da-275">Vaya a la dirección URL de Azure para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="c77da-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="c77da-276">Solución de problemas - Instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="c77da-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="c77da-277">Solución de problemas - Entorno virtual</span><span class="sxs-lookup"><span data-stu-id="c77da-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="c77da-278">Solución de problemas - Archivos estáticos</span><span class="sxs-lookup"><span data-stu-id="c77da-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="c77da-279">Django refuerza el concepto de recopilación de archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="c77da-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="c77da-280">Lo que significa que toma todos los archivos estáticos de su ubicación original y los copia en una única carpeta.</span><span class="sxs-lookup"><span data-stu-id="c77da-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="c77da-281">Para esta aplicación, se copian en `/static`.</span><span class="sxs-lookup"><span data-stu-id="c77da-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="c77da-282">Esto se realiza porque los archivos estáticos pueden proceder de otras aplicaciones Django diferentes.</span><span class="sxs-lookup"><span data-stu-id="c77da-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="c77da-283">Por ejemplo, los archivos estáticos de las interfaces de administración de Django se encuentran en una subcarpeta de la biblioteca de Django en el entorno virtual.</span><span class="sxs-lookup"><span data-stu-id="c77da-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="c77da-284">Los archivos estáticos definidos por esta aplicación se encuentran en `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="c77da-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="c77da-285">Cuantas más aplicaciones Django se utilicen, tendrá archivos estáticos ubicados en varios lugares.</span><span class="sxs-lookup"><span data-stu-id="c77da-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="c77da-286">Al ejecutar la aplicación en modo de depuración, la aplicación transmite archivos estáticos desde su ubicación original.</span><span class="sxs-lookup"><span data-stu-id="c77da-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="c77da-287">Al ejecutar la aplicación en modo de lanzamiento, la aplicación **no** transmite los archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="c77da-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="c77da-288">Es responsabilidad del servidor web transmitir los archivos.</span><span class="sxs-lookup"><span data-stu-id="c77da-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="c77da-289">Para esta aplicación, IIS transmitirá archivos estáticos desde `/static`.</span><span class="sxs-lookup"><span data-stu-id="c77da-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="c77da-290">La recolección de archivos estáticos se realiza automáticamente como parte del script de implementación, mediante el borrado de los archivos previamente recopilados.</span><span class="sxs-lookup"><span data-stu-id="c77da-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="c77da-291">Esto significa que la recolección se produce en cada implementación, ralentizando la implementación un poco, pero garantiza que los archivos desusados no estarán disponibles, con lo que se evita un posible riesgo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c77da-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="c77da-292">Si desea omitir la recopilación de archivos estáticos de la aplicación Django:</span><span class="sxs-lookup"><span data-stu-id="c77da-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="c77da-293">Tendrá que hacer la recopilación de manera manual en el equipo local:</span><span class="sxs-lookup"><span data-stu-id="c77da-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="c77da-294">Después, quite la carpeta `\static` de `.gitignore` y agréguela al repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="c77da-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="c77da-295">Solución de problemas - Configuración</span><span class="sxs-lookup"><span data-stu-id="c77da-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="c77da-296">Se pueden cambiar varias configuraciones para la aplicación en `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="c77da-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="c77da-297">Para mayor comodidad del desarrollador, se habilita el modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="c77da-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="c77da-298">Un efecto colateral interesante que es que podrá ver imágenes y cualquier otro contenido estático cuando se ejecuta localmente, sin necesidad de recopilar archivos estáticos.</span><span class="sxs-lookup"><span data-stu-id="c77da-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="c77da-299">Para deshabilitar el modo de depuración:</span><span class="sxs-lookup"><span data-stu-id="c77da-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="c77da-300">Cuando se deshabilita la depuración, hay que actualizar el valor de `ALLOWED_HOSTS` para que incluya el nombre de host de Azure.</span><span class="sxs-lookup"><span data-stu-id="c77da-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="c77da-301">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c77da-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="c77da-302">o para habilitar cualquiera de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c77da-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="c77da-303">En la práctica, puede que desee hacer algo más complejo para tratar con el cambio entre el modo de depuración y de lanzamiento y obtener el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="c77da-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="c77da-304">Se pueden establecer variables de entorno a través de la página **CONFIGURAQR** de Azure Portal, en la sección **Configuración de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c77da-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="c77da-305">Puede resultar útil para establecer valores que no desee que aparezcan en los orígenes (cadenas de conexión, contraseñas, etc.), o que desee establecer de forma diferente entre Azure y su equipo local.</span><span class="sxs-lookup"><span data-stu-id="c77da-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="c77da-306">En `settings.py`, puede consultar las variables de entorno mediante `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="c77da-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="c77da-307">Uso de una base de datos</span><span class="sxs-lookup"><span data-stu-id="c77da-307">Using a Database</span></span>
<span data-ttu-id="c77da-308">La base de datos que se incluye con la aplicación es una base de datos sqlite.</span><span class="sxs-lookup"><span data-stu-id="c77da-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="c77da-309">Se trata de una base de datos predeterminada, cómoda y útil, que se utilizará para el desarrollo, ya que prácticamente no requiere configuración.</span><span class="sxs-lookup"><span data-stu-id="c77da-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="c77da-310">La base de datos se almacena en el archivo db.sqlite3 en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c77da-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="c77da-311">Azure proporciona servicios de base de datos que son fáciles de usar desde una aplicación de Django.</span><span class="sxs-lookup"><span data-stu-id="c77da-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="c77da-312">Los tutoriales para usar [SQL Database] y [MySQL] desde una aplicación Django muestran los pasos necesarios para crear el servicio de base de datos, cambiar la configuración de la base de datos en `DjangoWebProject/settings.py` y las bibliotecas necesarias para realizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="c77da-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="c77da-313">Por supuesto, si prefiere administrar sus propios servidores de base de datos, puede hacerlo mediante máquinas virtuales Windows o Linux que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="c77da-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="c77da-314">Interfaz de administración de Django</span><span class="sxs-lookup"><span data-stu-id="c77da-314">Django Admin Interface</span></span>
<span data-ttu-id="c77da-315">Cuando empiece a crear los modelos, deseará rellenar la base de datos con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="c77da-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="c77da-316">Una manera fácil de agregar y editar el contenido de forma interactiva es utilizar la interfaz de administración de Django.</span><span class="sxs-lookup"><span data-stu-id="c77da-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="c77da-317">El código de la interfaz de administración se convierte en comentarios en los orígenes de la aplicación, pero está marcado claramente para que pueda habilitarlo fácilmente (busque 'admin').</span><span class="sxs-lookup"><span data-stu-id="c77da-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="c77da-318">Una vez habilitado, sincronice la base de datos, ejecute la aplicación y vaya a `/admin`.</span><span class="sxs-lookup"><span data-stu-id="c77da-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c77da-319">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c77da-319">Next Steps</span></span>
<span data-ttu-id="c77da-320">Siga estos vínculos para obtener más información acerca de Django y Python Tools para Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c77da-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="c77da-321">[Documentación de Django]</span><span class="sxs-lookup"><span data-stu-id="c77da-321">[Django Documentation]</span></span>
* <span data-ttu-id="c77da-322">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c77da-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="c77da-323">Para obtener información sobre el uso de Base de datos SQL y MySQL:</span><span class="sxs-lookup"><span data-stu-id="c77da-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="c77da-324">[Django y MySQL en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c77da-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="c77da-325">[Django y Base de datos SQL en Azure con Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c77da-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="c77da-326">Para obtener más información, consulte el [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c77da-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c77da-327">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="c77da-327">What's changed</span></span>
* <span data-ttu-id="c77da-328">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c77da-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django y MySQL en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django y Base de datos SQL en Azure con Python Tools para Visual Studio]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
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
[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs
[Documentación de Django]: https://www.djangoproject.com/
