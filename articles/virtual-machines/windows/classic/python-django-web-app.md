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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="6e692-103">Aplicación web Django Hola mundo en una máquina virtual de Windows Server</span><span class="sxs-lookup"><span data-stu-id="6e692-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6e692-104">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [modelo de implementación clásica de hello y Azure Resource Manager](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6e692-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6e692-105">Este artículo describe el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e692-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="6e692-106">Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas.</span><span class="sxs-lookup"><span data-stu-id="6e692-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="6e692-107">Este tutorial muestra cómo toohost un sitio Web basado en Django en Windows Server en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e692-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="6e692-108">En el tutorial de hello, no suponemos ninguna experiencia previa con Azure.</span><span class="sxs-lookup"><span data-stu-id="6e692-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="6e692-109">Cuando termine de tutorial de hello, puede tener una aplicación basada en Django se pueden instalar y ejecutar en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e692-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="6e692-110">Obtenga información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="6e692-110">Learn how to:</span></span>

* <span data-ttu-id="6e692-111">Configurar un toohost Django de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e692-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="6e692-112">Aunque este tutorial le explica cómo toodo para **Windows Server**, puede hacer Hola iguales para una VM de Linux hospedadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="6e692-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="6e692-113">Crear una aplicación Django en Windows.</span><span class="sxs-lookup"><span data-stu-id="6e692-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="6e692-114">Hola tutorial le mostrará cómo toobuild un básica Hello World web application.</span><span class="sxs-lookup"><span data-stu-id="6e692-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="6e692-115">aplicación Hello se hospeda en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e692-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="6e692-116">Hola siguiente captura de pantalla muestra la aplicación hello completado:</span><span class="sxs-lookup"><span data-stu-id="6e692-116">hello following screenshot shows hello completed application:</span></span>

![Una ventana del explorador muestra la página de hello hello world en Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="6e692-118">Crear y configurar un toohost Django de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="6e692-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="6e692-119">toocreate una máquina virtual de Azure con hello distribución de Windows Server 2012 R2 Datacenter, consulte [crear una máquina virtual que ejecuta Windows en el portal de Azure hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6e692-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="6e692-120">Establecer el tráfico del puerto 80 de Azure toodirect de hello web tooport 80 en la máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="6e692-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="6e692-121">Hola portal de Azure, vaya a Panel de toohello y seleccione la máquina virtual recién creada.</span><span class="sxs-lookup"><span data-stu-id="6e692-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="6e692-122">Haga clic en **Puntos de conexión** y luego en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e692-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Agregación de un extremo](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="6e692-124">En hello **Agregar extremo** página, para **nombre**, escriba **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="6e692-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="6e692-125">Establecer los puertos TCP de públicos y privados de hello demasiado**80**.</span><span class="sxs-lookup"><span data-stu-id="6e692-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Escritura del nombre y configuración de los puertos público y privado](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="6e692-127">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6e692-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="6e692-128">En el panel de hello, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e692-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="6e692-129">Haga clic en Inicio de sesión de toouse protocolo de escritorio remoto (RDP) tooremotely en toohello recién creado la máquina virtual de Azure **conectar**.</span><span class="sxs-lookup"><span data-stu-id="6e692-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="6e692-130">Hola siguiendo las instrucciones se supone firmado correctamente en la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="6e692-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="6e692-131">También supone que se emite comandos en la máquina virtual de hello y no en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="6e692-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="6e692-132"><a id="setup"></a>Instalación de Python, Django y WFastCGI</span><span class="sxs-lookup"><span data-stu-id="6e692-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="6e692-133">toodownload mediante Internet Explorer, es posible que tenga tooconfigure Internet Explorer **configuración de seguridad mejorada** configuración.</span><span class="sxs-lookup"><span data-stu-id="6e692-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="6e692-134">toodo, haga clic en **iniciar** > **herramientas administrativas** > **el administrador del servidor** > **deservidorLocal**.</span><span class="sxs-lookup"><span data-stu-id="6e692-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="6e692-135">Haga clic en **Configuración de seguridad mejorada de IE** y seleccione **Desactivar**.</span><span class="sxs-lookup"><span data-stu-id="6e692-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="6e692-136">Instalar versiones más recientes de Hola de Python 2.7 o 3.4 de Python de [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="6e692-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="6e692-137">Instalar paquetes de wfastcgi y django de hello mediante pip.</span><span class="sxs-lookup"><span data-stu-id="6e692-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="6e692-138">Para Python 2.7, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6e692-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="6e692-139">Para Python 3.4, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6e692-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="6e692-140">Instalación de ISS con FastCGI</span><span class="sxs-lookup"><span data-stu-id="6e692-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="6e692-141">Instale Internet Information Services (IIS) con compatibilidad para FastCGI.</span><span class="sxs-lookup"><span data-stu-id="6e692-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="6e692-142">Esta operación puede tardar varios tooexecute minutos.</span><span class="sxs-lookup"><span data-stu-id="6e692-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="6e692-143">Creación de una aplicación Django</span><span class="sxs-lookup"><span data-stu-id="6e692-143">Create a new Django application</span></span>
1. <span data-ttu-id="6e692-144">En C:\inetpub\wwwroot, toocreate un nuevo proyecto de Django, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6e692-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="6e692-145">Para Python 2.7, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6e692-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="6e692-146">Para Python 3.4, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6e692-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![resultado de Hello de comando de hello New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="6e692-148">Hola `django-admin` comando genera una estructura básica de sitios Web basados en Django:</span><span class="sxs-lookup"><span data-stu-id="6e692-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="6e692-149">`helloworld\manage.py` le ayuda a iniciar y detener el hospedaje del sitio web basado en Django.</span><span class="sxs-lookup"><span data-stu-id="6e692-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="6e692-150">`helloworld\helloworld\settings.py` tiene la configuración de Django para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e692-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="6e692-151">`helloworld\helloworld\urls.py`tiene código de asignación de hello entre cada dirección URL y su vista.</span><span class="sxs-lookup"><span data-stu-id="6e692-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="6e692-152">En el directorio de C:\inetpub\wwwroot\helloworld\helloworld hello, cree un nuevo archivo denominado views.py.</span><span class="sxs-lookup"><span data-stu-id="6e692-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="6e692-153">Este archivo tiene la vista de Hola que representa la página de "Hola a todos" Hola.</span><span class="sxs-lookup"><span data-stu-id="6e692-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="6e692-154">En el editor de código, escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="6e692-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="6e692-155">Reemplace el contenido de hello del archivo de urls.py de hello con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="6e692-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="6e692-156">Configuración de IIS</span><span class="sxs-lookup"><span data-stu-id="6e692-156">Set up IIS</span></span>
1. <span data-ttu-id="6e692-157">En el archivo applicationhost.config global de hello, desbloquee la sección de controladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e692-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="6e692-158">Esto permite que el controlador de Python de web.config archivo toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="6e692-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="6e692-159">Agregue este comando:</span><span class="sxs-lookup"><span data-stu-id="6e692-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="6e692-160">Active WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="6e692-160">Activate WFastCGI.</span></span> <span data-ttu-id="6e692-161">Esto agrega un archivo de aplicación toohello applicationhost.config global, que hace referencia tooyour intérprete hello y ejecutable wfastcgi.py script de Python.</span><span class="sxs-lookup"><span data-stu-id="6e692-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="6e692-162">En Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6e692-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="6e692-163">En Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6e692-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="6e692-164">Cree un archivo web.config en C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="6e692-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="6e692-165">Hola valo hello `scriptProcessor` atributo debe coincidir con la salida de hello de hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="6e692-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="6e692-166">Para obtener más información acerca de la configuración de wfastcgi hello, consulte [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="6e692-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="6e692-167">En Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6e692-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="6e692-168">En Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6e692-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="6e692-169">Actualice la ubicación de Hola de hello IIS predeterminado toopoint toohello Django proyecto carpeta del sitio Web:</span><span class="sxs-lookup"><span data-stu-id="6e692-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="6e692-170">Cargar la página Web de hello en el explorador.</span><span class="sxs-lookup"><span data-stu-id="6e692-170">Load hello webpage in your browser.</span></span>

![Una ventana del explorador muestra la página de hello hello world en Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="6e692-172">Apagado de la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="6e692-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="6e692-173">Cuando haya terminado con este tutorial, se recomienda apagar o quitar la máquina virtual de Azure que creó para el tutorial de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="6e692-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="6e692-174">Esto libera recursos para otros tutoriales y evita cargos de uso de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e692-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
