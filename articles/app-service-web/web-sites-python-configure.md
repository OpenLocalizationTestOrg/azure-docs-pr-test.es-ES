---
title: "aaaConfiguring Python con aplicaciones de Web del servicio de aplicación de Azure"
description: "En este tutorial se describen las opciones para crear y configurar una aplicación Python básica compatible con la Interfaz de puerta de enlace de servicio web (WSGI) en Aplicaciones web del Servicio de aplicaciones de Azure."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="71fae-103">Configuración de Python con Aplicaciones web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="71fae-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="71fae-104">Este tutorial describen las opciones para crear y configurar una aplicación básica de interfaz de puerta de enlace de servidor web (WSGI) compatible con Python en [aplicaciones web del Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="71fae-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="71fae-105">Describe características adicionales de implementación de Git como, por ejemplo, el entorno virtual y la instalación del paquete mediante requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="71fae-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="71fae-106">¿Bottle, Django o Flask?</span><span class="sxs-lookup"><span data-stu-id="71fae-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="71fae-107">Hello Azure Marketplace contiene plantillas para marcos de trabajo de hello Bottle por sí solo, Django y matraz.</span><span class="sxs-lookup"><span data-stu-id="71fae-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="71fae-108">Si está desarrollando su primera aplicación web en el servicio de aplicación de Azure, o no está familiarizado con Git, recomendamos que siga uno de estos tutoriales, que incluyen instrucciones paso a paso para crear una aplicación operativa de la Galería de hello mediante la implementación de Git desde Windows o Mac:</span><span class="sxs-lookup"><span data-stu-id="71fae-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="71fae-109">Creación de Aplicaciones web con Bottle</span><span class="sxs-lookup"><span data-stu-id="71fae-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="71fae-110">Creación de Aplicaciones web con Django</span><span class="sxs-lookup"><span data-stu-id="71fae-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="71fae-111">Creación de Aplicaciones web con Flask</span><span class="sxs-lookup"><span data-stu-id="71fae-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="71fae-112">Creación de una aplicación web en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="71fae-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="71fae-113">Este tutorial se da por supuesto un existente Azure acceso y suscripción toohello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="71fae-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="71fae-114">Si no tiene una aplicación web existente, puede crear uno a partir de hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="71fae-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="71fae-115">Haga clic en botón nuevo de hello en la esquina superior izquierda de hello, a continuación, haga clic en **Web y móvil** > **aplicación Web**.</span><span class="sxs-lookup"><span data-stu-id="71fae-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="71fae-116">Publicación Git</span><span class="sxs-lookup"><span data-stu-id="71fae-116">Git Publishing</span></span>
<span data-ttu-id="71fae-117">Configurar la publicación de Git de la aplicación web recién creado siguiendo las instrucciones de hello en [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="71fae-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="71fae-118">Este tutorial usa Git toocreate, administrar y publicar nuestro tooAzure de aplicación web de Python servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71fae-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="71fae-119">Después de configurar la publicación Git, se creará un repositorio Git y se asociará a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="71fae-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="71fae-120">dirección URL del repositorio de Hola se mostrarán y puede ser de ahora en adelante toopush usa datos de nube de toohello de entorno de desarrollo local Hola.</span><span class="sxs-lookup"><span data-stu-id="71fae-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="71fae-121">aplicaciones de toopublish mediante Git, asegúrese de que también se instala un cliente de Git y use las instrucciones de hello proporcionan toopush su tooAzure de contenido de aplicación servicio de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="71fae-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="71fae-122">Información general de la aplicación</span><span class="sxs-lookup"><span data-stu-id="71fae-122">Application Overview</span></span>
<span data-ttu-id="71fae-123">En las secciones siguientes de hello, se crea Hola siguientes archivos.</span><span class="sxs-lookup"><span data-stu-id="71fae-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="71fae-124">Debe colocarse en la raíz de hello del repositorio de Git de Hola.</span><span class="sxs-lookup"><span data-stu-id="71fae-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="71fae-125">Controlador de WSGI</span><span class="sxs-lookup"><span data-stu-id="71fae-125">WSGI Handler</span></span>
<span data-ttu-id="71fae-126">WSGI es un estándar de Python descrito por [PEP 3333](http://www.python.org/dev/peps/pep-3333/) define una interfaz entre el servidor web de Hola y Python.</span><span class="sxs-lookup"><span data-stu-id="71fae-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="71fae-127">Ofrece una interfaz normalizada para escribir varios marcos de trabajo y aplicaciones web con Python.</span><span class="sxs-lookup"><span data-stu-id="71fae-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="71fae-128">Los marcos de trabajo web conocidos de Python usan WSGI hoy en día.</span><span class="sxs-lookup"><span data-stu-id="71fae-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="71fae-129">Azure proporciona aplicaciones de Web del servicio de aplicación que se admiten para los marcos de este tipo; Además, los usuarios avanzados pueden incluso crear sus propios como controlador personalizado Hola sigue directrices de especificación de hello WSGI.</span><span class="sxs-lookup"><span data-stu-id="71fae-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="71fae-130">A continuación se muestra un ejemplo de `app.py` que define un controlador personalizado:</span><span class="sxs-lookup"><span data-stu-id="71fae-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="71fae-131">Puede ejecutar esta aplicación localmente con `python app.py`, a continuación, examinar demasiado`http://localhost:5555` en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="71fae-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="71fae-132">Entorno virtual</span><span class="sxs-lookup"><span data-stu-id="71fae-132">Virtual Environment</span></span>
<span data-ttu-id="71fae-133">Aunque la aplicación de ejemplo de Hola anterior no requiere que todos los paquetes externos, es probable que la aplicación necesitará algunas.</span><span class="sxs-lookup"><span data-stu-id="71fae-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="71fae-134">toohelp administrar dependencias del paquete externo, implementación de Git de Azure admite la creación de hello de entornos virtuales.</span><span class="sxs-lookup"><span data-stu-id="71fae-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="71fae-135">Cuando Azure detecta un requirements.txt en la raíz de hello del repositorio de hello, crea automáticamente un entorno virtual denominado `env`.</span><span class="sxs-lookup"><span data-stu-id="71fae-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="71fae-136">Esto sólo ocurre en la primera implementación de Hola o durante cualquier implementación después de hello ha cambiado el tiempo de ejecución de Python seleccionado.</span><span class="sxs-lookup"><span data-stu-id="71fae-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="71fae-137">Probablemente deseará toocreate un entorno virtual localmente para el desarrollo, pero no lo incluya en el repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="71fae-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="71fae-138">Administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="71fae-138">Package Management</span></span>
<span data-ttu-id="71fae-139">Paquetes incluidos en requirements.txt se instalarán automáticamente en entorno virtual de hello mediante pip.</span><span class="sxs-lookup"><span data-stu-id="71fae-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="71fae-140">Esto se realiza en cada implementación, pero pip omitirá la instalación si un paquete ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="71fae-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="71fae-141">Ejemplo `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="71fae-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="71fae-142">versión de Python</span><span class="sxs-lookup"><span data-stu-id="71fae-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="71fae-143">Ejemplo `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="71fae-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="71fae-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="71fae-144">Web.config</span></span>
<span data-ttu-id="71fae-145">Deberá toocreate un toospecify del archivo web.config cómo servidor hello debe controlar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="71fae-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="71fae-146">Tenga en cuenta que si tiene un archivo de web.x.y.config en el repositorio, que coincide con x.y Hola había seleccionada en tiempo de ejecución de Python, Azure copiará automáticamente el archivo adecuado de hello como web.config.</span><span class="sxs-lookup"><span data-stu-id="71fae-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="71fae-147">Hello web.config en los ejemplos siguientes se basan en una secuencia de comandos de proxy de entorno virtual, que se describe en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="71fae-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="71fae-148">Funcionan con el controlador WSGI Hola utilizado en el ejemplo de Hola `app.py` anteriormente.</span><span class="sxs-lookup"><span data-stu-id="71fae-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="71fae-149">Ejemplo `web.config` para Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="71fae-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="71fae-150">Ejemplo `web.config` para Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="71fae-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="71fae-151">Archivos estáticos se controlarán por servidor web de hello directamente, sin tener que pasar por el código de Python para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="71fae-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="71fae-152">Hola por encima de los ejemplos, ubicación de Hola Hola estático de archivos del disco debe coincidir con ubicación hello en dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="71fae-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="71fae-153">Esto significa que una solicitud de `http://pythonapp.azurewebsites.net/static/site.css` servirá archivo hello en el disco en `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="71fae-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="71fae-154">`WSGI_ALT_VIRTUALENV_HANDLER`es donde se especifica controlador WSGI de Hola.</span><span class="sxs-lookup"><span data-stu-id="71fae-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="71fae-155">Hola por encima de los ejemplos, tiene `app.wsgi_app` porque el controlador de hello es una función denominada `wsgi_app` en `app.py` en la carpeta raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="71fae-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="71fae-156">`PYTHONPATH`se pueden personalizar, pero si instala todas las dependencias en el entorno virtual de hello especificándolas en requirements.txt, no es necesario toochange lo.</span><span class="sxs-lookup"><span data-stu-id="71fae-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="71fae-157">Proxy del entorno virtual</span><span class="sxs-lookup"><span data-stu-id="71fae-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="71fae-158">Hola siguiente secuencia de comandos es controlador WSGI de tooretrieve usado hello, activar Hola virtuales entorno y registre los errores.</span><span class="sxs-lookup"><span data-stu-id="71fae-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="71fae-159">Está diseñado toobe genérico y se utiliza sin modificaciones.</span><span class="sxs-lookup"><span data-stu-id="71fae-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="71fae-160">Contenido de `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="71fae-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="71fae-161">Personalización de la implementación de Git</span><span class="sxs-lookup"><span data-stu-id="71fae-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="71fae-162">Solución de problemas - Instalación de un paquete</span><span class="sxs-lookup"><span data-stu-id="71fae-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="71fae-163">Solución de problemas - Entorno virtual</span><span class="sxs-lookup"><span data-stu-id="71fae-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="71fae-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71fae-164">Next steps</span></span>
<span data-ttu-id="71fae-165">Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="71fae-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="71fae-166">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71fae-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="71fae-167">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="71fae-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="71fae-168">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="71fae-168">What's changed</span></span>
* <span data-ttu-id="71fae-169">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="71fae-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

