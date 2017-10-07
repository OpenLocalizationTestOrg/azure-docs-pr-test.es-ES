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
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Configuración de Python con Aplicaciones web del Servicio de aplicaciones de Azure
Este tutorial describen las opciones para crear y configurar una aplicación básica de interfaz de puerta de enlace de servidor web (WSGI) compatible con Python en [aplicaciones web del Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Describe características adicionales de implementación de Git como, por ejemplo, el entorno virtual y la instalación del paquete mediante requirements.txt.

## <a name="bottle-django-or-flask"></a>¿Bottle, Django o Flask?
Hello Azure Marketplace contiene plantillas para marcos de trabajo de hello Bottle por sí solo, Django y matraz. Si está desarrollando su primera aplicación web en el servicio de aplicación de Azure, o no está familiarizado con Git, recomendamos que siga uno de estos tutoriales, que incluyen instrucciones paso a paso para crear una aplicación operativa de la Galería de hello mediante la implementación de Git desde Windows o Mac:

* [Creación de Aplicaciones web con Bottle](web-sites-python-create-deploy-bottle-app.md)
* [Creación de Aplicaciones web con Django](web-sites-python-create-deploy-django-app.md)
* [Creación de Aplicaciones web con Flask](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Creación de una aplicación web en el Portal de Azure
Este tutorial se da por supuesto un existente Azure acceso y suscripción toohello Portal de Azure.

Si no tiene una aplicación web existente, puede crear uno a partir de hello [Portal de Azure](https://portal.azure.com).  Haga clic en botón nuevo de hello en la esquina superior izquierda de hello, a continuación, haga clic en **Web y móvil** > **aplicación Web**.

## <a name="git-publishing"></a>Publicación Git
Configurar la publicación de Git de la aplicación web recién creado siguiendo las instrucciones de hello en [tooAzure servicio de aplicaciones de la implementación de Git Local](app-service-deploy-local-git.md). Este tutorial usa Git toocreate, administrar y publicar nuestro tooAzure de aplicación web de Python servicio de aplicaciones.

Después de configurar la publicación Git, se creará un repositorio Git y se asociará a la aplicación web. dirección URL del repositorio de Hola se mostrarán y puede ser de ahora en adelante toopush usa datos de nube de toohello de entorno de desarrollo local Hola. aplicaciones de toopublish mediante Git, asegúrese de que también se instala un cliente de Git y use las instrucciones de hello proporcionan toopush su tooAzure de contenido de aplicación servicio de aplicaciones web.

## <a name="application-overview"></a>Información general de la aplicación
En las secciones siguientes de hello, se crea Hola siguientes archivos. Debe colocarse en la raíz de hello del repositorio de Git de Hola.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>Controlador de WSGI
WSGI es un estándar de Python descrito por [PEP 3333](http://www.python.org/dev/peps/pep-3333/) define una interfaz entre el servidor web de Hola y Python. Ofrece una interfaz normalizada para escribir varios marcos de trabajo y aplicaciones web con Python. Los marcos de trabajo web conocidos de Python usan WSGI hoy en día. Azure proporciona aplicaciones de Web del servicio de aplicación que se admiten para los marcos de este tipo; Además, los usuarios avanzados pueden incluso crear sus propios como controlador personalizado Hola sigue directrices de especificación de hello WSGI.

A continuación se muestra un ejemplo de `app.py` que define un controlador personalizado:

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

Puede ejecutar esta aplicación localmente con `python app.py`, a continuación, examinar demasiado`http://localhost:5555` en el explorador web.

## <a name="virtual-environment"></a>Entorno virtual
Aunque la aplicación de ejemplo de Hola anterior no requiere que todos los paquetes externos, es probable que la aplicación necesitará algunas.

toohelp administrar dependencias del paquete externo, implementación de Git de Azure admite la creación de hello de entornos virtuales.

Cuando Azure detecta un requirements.txt en la raíz de hello del repositorio de hello, crea automáticamente un entorno virtual denominado `env`. Esto sólo ocurre en la primera implementación de Hola o durante cualquier implementación después de hello ha cambiado el tiempo de ejecución de Python seleccionado.

Probablemente deseará toocreate un entorno virtual localmente para el desarrollo, pero no lo incluya en el repositorio de Git.

## <a name="package-management"></a>Administración de paquetes
Paquetes incluidos en requirements.txt se instalarán automáticamente en entorno virtual de hello mediante pip. Esto se realiza en cada implementación, pero pip omitirá la instalación si un paquete ya está instalado.

Ejemplo `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>versión de Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Ejemplo `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
Deberá toocreate un toospecify del archivo web.config cómo servidor hello debe controlar las solicitudes.

Tenga en cuenta que si tiene un archivo de web.x.y.config en el repositorio, que coincide con x.y Hola había seleccionada en tiempo de ejecución de Python, Azure copiará automáticamente el archivo adecuado de hello como web.config.

Hello web.config en los ejemplos siguientes se basan en una secuencia de comandos de proxy de entorno virtual, que se describe en la sección siguiente Hola.  Funcionan con el controlador WSGI Hola utilizado en el ejemplo de Hola `app.py` anteriormente.

Ejemplo `web.config` para Python 2.7:

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


Ejemplo `web.config` para Python 3.4:

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


Archivos estáticos se controlarán por servidor web de hello directamente, sin tener que pasar por el código de Python para mejorar el rendimiento.

Hola por encima de los ejemplos, ubicación de Hola Hola estático de archivos del disco debe coincidir con ubicación hello en dirección URL de Hola. Esto significa que una solicitud de `http://pythonapp.azurewebsites.net/static/site.css` servirá archivo hello en el disco en `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`es donde se especifica controlador WSGI de Hola. Hola por encima de los ejemplos, tiene `app.wsgi_app` porque el controlador de hello es una función denominada `wsgi_app` en `app.py` en la carpeta raíz de Hola.

`PYTHONPATH`se pueden personalizar, pero si instala todas las dependencias en el entorno virtual de hello especificándolas en requirements.txt, no es necesario toochange lo.

## <a name="virtual-environment-proxy"></a>Proxy del entorno virtual
Hola siguiente secuencia de comandos es controlador WSGI de tooretrieve usado hello, activar Hola virtuales entorno y registre los errores. Está diseñado toobe genérico y se utiliza sin modificaciones.

Contenido de `ptvs_virtualenv_proxy.py`:

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


## <a name="customize-git-deployment"></a>Personalización de la implementación de Git
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Solución de problemas - Instalación de un paquete
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Solución de problemas - Entorno virtual
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

