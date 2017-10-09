---
title: "aplicación web de aaaPython con Django en una máquina virtual Linux de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toohost un Django-based web aplicación en Azure con una VM de Linux."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="ebb1a-103">Aplicación web Django Hello World en una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="ebb1a-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebb1a-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ebb1a-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="ebb1a-105">Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="ebb1a-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="ebb1a-106">Este tutorial muestra cómo toohost un sitio Web basado en Django en Linux en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="ebb1a-107">En el tutorial de hello, no suponemos ninguna experiencia previa con Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="ebb1a-108">Cuando termine de tutorial de hello, puede tener una aplicación basada en Django se pueden instalar y ejecutar en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="ebb1a-109">Obtenga información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-109">Learn how to:</span></span>

* <span data-ttu-id="ebb1a-110">Configurar un toohost Django de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="ebb1a-111">Aunque este tutorial le explica cómo toodo para **Linux**, puede hacer hello iguales para una VM de Windows Server hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="ebb1a-112">Cree una nueva aplicación Django en Linux.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="ebb1a-113">Hola tutorial le mostrará cómo toobuild un básica Hello World web application.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="ebb1a-114">aplicación Hello se hospeda en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="ebb1a-115">Hola siguiente captura de pantalla muestra la aplicación hello completado:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-115">hello following screenshot shows hello completed application:</span></span>

![Una ventana del explorador muestra la página de Hola Hola a todos en Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="ebb1a-117">Crear y configurar un toohost Django de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="ebb1a-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="ebb1a-118">vea toocreate una máquina virtual de Azure con hello distribución Ubuntu Server 14.04 LTS, [crear una máquina virtual Linux en el portal de Azure hello](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ebb1a-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ebb1a-119">También puede elegir una autenticación de contraseña en lugar de usar la clave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="ebb1a-120">tooedit Hola red seguridad grupo tooallow entrante HTTP tráfico tooport 80, consulte [crear grupos de seguridad de red en el portal de Azure hello](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="ebb1a-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="ebb1a-121">(Opcional) De forma predeterminada, la nueva máquina virtual no tiene un nombre de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="ebb1a-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="ebb1a-122">toocreate una máquina virtual con un FQDN, vea [crear un FQDN de hello portal de Azure para una VM de Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ebb1a-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ebb1a-123">Este paso no es necesario para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="ebb1a-124"><a id="setup"></a>Configurar el entorno de desarrollo de Hola</span><span class="sxs-lookup"><span data-stu-id="ebb1a-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="ebb1a-125">Si necesita tooinstall Python o desea bibliotecas de cliente de toouse hello, vea hello [Guía de instalación de Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="ebb1a-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="ebb1a-126">Hola Ubuntu Linux VM tiene preinstalado de Python 2.7, pero no proceder con Apache o Django.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="ebb1a-127">Complete Hola siguiendo los pasos tooconnect tooyour máquina virtual e instale Apache y Django:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="ebb1a-128">Abra una nueva ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="ebb1a-129">tooconnect toohello VM de Azure, escriba Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="ebb1a-130">Si no creó un FQDN, puede conectarse mediante el uso de la dirección IP pública Hola que se muestra en la máquina virtual de hello resumen Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="ebb1a-131">tooinstall Django, escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="ebb1a-132">tooinstall Apache con mod-wsgi, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="ebb1a-133">Creación de una aplicación Django</span><span class="sxs-lookup"><span data-stu-id="ebb1a-133">Create a new Django app</span></span>
1. <span data-ttu-id="ebb1a-134">toouse tooaccess SSH su máquina virtual, la ventana de Terminal de hello abierto que usaste en hello sección anterior.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="ebb1a-135">toocreate un nuevo proyecto de Django, escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="ebb1a-136">Hola `django-admin.py` secuencia de comandos genera una estructura básica de sitios Web basados en Django:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="ebb1a-137">`helloworld/manage.py` le ayuda a iniciar y detener el hospedaje del sitio web basado en Django.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="ebb1a-138">`helloworld/helloworld/settings.py` tiene la configuración de Django para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="ebb1a-139">`helloworld/helloworld/urls.py`tiene código de asignación de hello entre cada dirección URL y su vista.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="ebb1a-140">En el directorio de /var/www/helloworld/helloworld hello, cree un nuevo archivo denominado views.py.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="ebb1a-141">Este archivo tiene la vista de Hola que representa la página de "Hola a todos" Hola.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="ebb1a-142">En el editor de código, escriba Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="ebb1a-143">Reemplace el contenido de hello del archivo de urls.py de hello con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="ebb1a-144">Instalación de Apache</span><span class="sxs-lookup"><span data-stu-id="ebb1a-144">Set up Apache</span></span>
1. <span data-ttu-id="ebb1a-145">En la carpeta de /etc/apache2/sites-available/helloworld.conf hello, cree un archivo de configuración de host virtual de Apache.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="ebb1a-146">Establecer Hola contenido toohello después de valores.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="ebb1a-147">Reemplace *Nombredesuvm* con nombre real de Hola de máquina de hello está utilizando (por ejemplo, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="ebb1a-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="ebb1a-148">sitio de hello tooactivate, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="ebb1a-149">toorestart Apache, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="ebb1a-150">Carga la página Web de hello en el explorador:</span><span class="sxs-lookup"><span data-stu-id="ebb1a-150">Load hello webpage in your browser:</span></span>
   
   ![Una ventana del explorador muestra la página de hello hello world en Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="ebb1a-152">Apagado de la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="ebb1a-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="ebb1a-153">Cuando haya terminado con este tutorial, se recomienda apagar o quitar la máquina virtual de Azure que creó para el tutorial de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="ebb1a-154">Esto libera recursos para otros tutoriales y evita cargos de uso de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb1a-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

