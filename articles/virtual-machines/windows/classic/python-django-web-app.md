---
title: "aplicación web de aaaDjango en una VM de Azure Windows Server | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toohost un sitio Web basado en Django en Azure con una VM de Windows Server 2012 R2 Datacenter con el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Aplicación web Django Hola mundo en una máquina virtual de Windows Server

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [modelo de implementación clásica de hello y Azure Resource Manager](../../../resource-manager-deployment-model.md). Este artículo describe el modelo de implementación clásica de Hola. Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas.

Este tutorial muestra cómo toohost un sitio Web basado en Django en Windows Server en máquinas virtuales de Azure. En el tutorial de hello, no suponemos ninguna experiencia previa con Azure. Cuando termine de tutorial de hello, puede tener una aplicación basada en Django se pueden instalar y ejecutar en la nube de Hola.

Obtenga información sobre cómo:

* Configurar un toohost Django de máquina virtual de Azure. Aunque este tutorial le explica cómo toodo para **Windows Server**, puede hacer Hola iguales para una VM de Linux hospedadas en Azure.
* Crear una aplicación Django en Windows.

Hola tutorial le mostrará cómo toobuild un básica Hello World web application. aplicación Hello se hospeda en una máquina virtual de Azure.

Hola siguiente captura de pantalla muestra la aplicación hello completado:

![Una ventana del explorador muestra la página de hello hello world en Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Crear y configurar un toohost Django de máquina virtual de Azure

1. toocreate una máquina virtual de Azure con hello distribución de Windows Server 2012 R2 Datacenter, consulte [crear una máquina virtual que ejecuta Windows en el portal de Azure hello](tutorial.md).
2. Establecer el tráfico del puerto 80 de Azure toodirect de hello web tooport 80 en la máquina virtual de hello:
   
   1. Hola portal de Azure, vaya a Panel de toohello y seleccione la máquina virtual recién creada.
   2. Haga clic en **Puntos de conexión** y luego en **Agregar**.

     ![Agregación de un extremo](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. En hello **Agregar extremo** página, para **nombre**, escriba **HTTP**. Establecer los puertos TCP de públicos y privados de hello demasiado**80**.

     ![Escritura del nombre y configuración de los puertos público y privado](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Haga clic en **Aceptar**.
     
3. En el panel de hello, seleccione la máquina virtual. Haga clic en Inicio de sesión de toouse protocolo de escritorio remoto (RDP) tooremotely en toohello recién creado la máquina virtual de Azure **conectar**.  

> [!IMPORTANT] 
> Hola siguiendo las instrucciones se supone firmado correctamente en la máquina virtual de toohello. También supone que se emite comandos en la máquina virtual de hello y no en el equipo local.

## <a id="setup"></a>Instalación de Python, Django y WFastCGI
> [!NOTE]
> toodownload mediante Internet Explorer, es posible que tenga tooconfigure Internet Explorer **configuración de seguridad mejorada** configuración. toodo, haga clic en **iniciar** > **herramientas administrativas** > **el administrador del servidor** > **deservidorLocal**. Haga clic en **Configuración de seguridad mejorada de IE** y seleccione **Desactivar**.

1. Instalar versiones más recientes de Hola de Python 2.7 o 3.4 de Python de [python.org][python.org].
2. Instalar paquetes de wfastcgi y django de hello mediante pip.
   
    Para Python 2.7, use Hola siguiente comando:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Para Python 3.4, use Hola siguiente comando:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>Instalación de ISS con FastCGI
* Instale Internet Information Services (IIS) con compatibilidad para FastCGI. Esta operación puede tardar varios tooexecute minutos.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Creación de una aplicación Django
1. En C:\inetpub\wwwroot, toocreate un nuevo proyecto de Django, escriba Hola siguiente comando:
   
   Para Python 2.7, use Hola siguiente comando:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Para Python 3.4, use Hola siguiente comando:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![resultado de Hello de comando de hello New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Hola `django-admin` comando genera una estructura básica de sitios Web basados en Django:
   
   * `helloworld\manage.py` le ayuda a iniciar y detener el hospedaje del sitio web basado en Django.
   * `helloworld\helloworld\settings.py` tiene la configuración de Django para la aplicación.
   * `helloworld\helloworld\urls.py`tiene código de asignación de hello entre cada dirección URL y su vista.
3. En el directorio de C:\inetpub\wwwroot\helloworld\helloworld hello, cree un nuevo archivo denominado views.py. Este archivo tiene la vista de Hola que representa la página de "Hola a todos" Hola. En el editor de código, escriba Hola siguientes comandos:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Reemplace el contenido de hello del archivo de urls.py de hello con hello siguientes comandos:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Configuración de IIS
1. En el archivo applicationhost.config global de hello, desbloquee la sección de controladores de Hola.  Esto permite que el controlador de Python de web.config archivo toouse Hola. Agregue este comando:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Active WFastCGI. Esto agrega un archivo de aplicación toohello applicationhost.config global, que hace referencia tooyour intérprete hello y ejecutable wfastcgi.py script de Python.
   
    En Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    En Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. Cree un archivo web.config en C:\inetpub\wwwroot\helloworld. Hola valo hello `scriptProcessor` atributo debe coincidir con la salida de hello de hello anterior paso. Para obtener más información acerca de la configuración de wfastcgi hello, consulte [pypi wfastcgi][wfastcgi].
   
   En Python 2.7:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   En Python 3.4:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. Actualice la ubicación de Hola de hello IIS predeterminado toopoint toohello Django proyecto carpeta del sitio Web:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Cargar la página Web de hello en el explorador.

![Una ventana del explorador muestra la página de hello hello world en Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Apagado de la máquina virtual de Azure
Cuando haya terminado con este tutorial, se recomienda apagar o quitar la máquina virtual de Azure que creó para el tutorial de Hola Hola. Esto libera recursos para otros tutoriales y evita cargos de uso de Azure.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
