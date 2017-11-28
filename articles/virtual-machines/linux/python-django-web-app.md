---
title: "Aplicación web Python con Django en una máquina virtual Linux de Azure | Microsoft Docs"
description: "Aprenda a hospedar una aplicación web basada en Django en Azure con una máquina virtual Linux."
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
ms.openlocfilehash: 6e2ab8c7da7496d0e2b567a4bdc9341adcf01552
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="4ee58-103">Aplicación web Django Hello World en una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="4ee58-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ee58-104">Windows</span><span class="sxs-lookup"><span data-stu-id="4ee58-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="4ee58-105">Mac o Linux</span><span class="sxs-lookup"><span data-stu-id="4ee58-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="4ee58-106">En este tutorial se muestra cómo hospedar un sitio web basado en Django para Linux en Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="4ee58-106">This tutorial shows you how to host a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="4ee58-107">En el tutorial, se asume que no tiene experiencia con Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee58-107">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="4ee58-108">Cuando lo termine, tendrá una aplicación basada en Django que funcionará en la nube.</span><span class="sxs-lookup"><span data-stu-id="4ee58-108">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="4ee58-109">Obtenga información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="4ee58-109">Learn how to:</span></span>

* <span data-ttu-id="4ee58-110">Configure una máquina virtual de Azure para hospedar Django.</span><span class="sxs-lookup"><span data-stu-id="4ee58-110">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="4ee58-111">Aunque en este tutorial se explica cómo hacer esto para **Linux**, puede hacer lo mismo para una máquina virtual de Windows Server hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee58-111">Although this tutorial explains how to do this for **Linux**, you can do the same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="4ee58-112">Cree una nueva aplicación Django en Linux.</span><span class="sxs-lookup"><span data-stu-id="4ee58-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="4ee58-113">En el tutorial se muestra cómo crear una aplicación web básica de Hola mundo.</span><span class="sxs-lookup"><span data-stu-id="4ee58-113">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="4ee58-114">La aplicación se hospeda en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee58-114">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="4ee58-115">La siguiente captura de pantalla muestra la aplicación completada:</span><span class="sxs-lookup"><span data-stu-id="4ee58-115">The following screenshot shows the completed application:</span></span>

![Ventana del explorador que muestra la página Hola mundo en Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="4ee58-117">Creación y configuración de una máquina virtual de Azure para hospedar Django</span><span class="sxs-lookup"><span data-stu-id="4ee58-117">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="4ee58-118">Para crear una máquina virtual de Azure con la distribución de Ubuntu Server 14.04 LTS, consulte [Creación de una máquina virtual Linux en Azure Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ee58-118">To create an Azure virtual machine with the Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in the Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4ee58-119">También puede elegir una autenticación de contraseña en lugar de usar la clave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="4ee58-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="4ee58-120">Para editar el grupo de seguridad de red para que permita el tráfico HTTP entrante al puerto 80, consulte [Creación de grupos de seguridad de red en Azure Portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4ee58-120">To edit the network security group to allow incoming HTTP traffic to port 80, see [Create network security groups in the Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="4ee58-121">(Opcional) De forma predeterminada, la nueva máquina virtual no tiene un nombre de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="4ee58-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="4ee58-122">Para crear una máquina virtual con un nombre de dominio completo, consulte [Creación de un nombre de dominio completo en Azure Portal para una máquina virtual Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ee58-122">To create a VM with an FQDN, see [Create an FQDN in the Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4ee58-123">Este paso no es necesario para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4ee58-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="4ee58-124"><a id="setup"> </a>Configuración del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="4ee58-124"><a id="setup"> </a>Set up the development environment</span></span>
> [!NOTE]
> <span data-ttu-id="4ee58-125">Si es necesario instalar Python o desea usar las bibliotecas de clientes, consulte la [Guía de instalación de Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="4ee58-125">If you need to install Python or want to use the client libraries, see the [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="4ee58-126">La máquina virtual de Ubuntu Linux tiene Python 2.7 preinstalado, pero este no viene incluido con Apache o Django.</span><span class="sxs-lookup"><span data-stu-id="4ee58-126">The Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="4ee58-127">Realice los pasos siguientes para conectarse a la máquina virtual e instalar Apache y Django:</span><span class="sxs-lookup"><span data-stu-id="4ee58-127">Complete the following steps to connect to your VM and install Apache and Django:</span></span>

1. <span data-ttu-id="4ee58-128">Abra una nueva ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="4ee58-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="4ee58-129">Escriba el siguiente comando para conectarse a la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee58-129">To connect to the Azure VM, enter the following command.</span></span> <span data-ttu-id="4ee58-130">Si no creó un FQDN, puede conectarse mediante la dirección IP pública que se muestra en el resumen de la máquina virtual en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4ee58-130">If you didn't create an FQDN, you can connect by using the public IP address that's displayed in the virtual machine summary in the Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="4ee58-131">Escriba los siguientes comandos para instalar Django:</span><span class="sxs-lookup"><span data-stu-id="4ee58-131">To install Django, enter the following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="4ee58-132">Escriba el siguiente comando para instalar Apache con mod-wsgi:</span><span class="sxs-lookup"><span data-stu-id="4ee58-132">To install Apache with mod-wsgi, enter the following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="4ee58-133">Creación de una aplicación Django</span><span class="sxs-lookup"><span data-stu-id="4ee58-133">Create a new Django app</span></span>
1. <span data-ttu-id="4ee58-134">Para utilizar SSH para acceder a la máquina virtual, abra la ventana de terminal que utilizó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="4ee58-134">To use SSH to access your VM, open the Terminal window you used in the preceding section.</span></span>
2. <span data-ttu-id="4ee58-135">Escriba los siguientes comandos para crear un proyecto Django:</span><span class="sxs-lookup"><span data-stu-id="4ee58-135">To create a new Django project, enter the following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="4ee58-136">El script `django-admin.py` genera una estructura básica para los sitios web basados en Django:</span><span class="sxs-lookup"><span data-stu-id="4ee58-136">The `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="4ee58-137">`helloworld/manage.py` le ayuda a iniciar y detener el hospedaje del sitio web basado en Django.</span><span class="sxs-lookup"><span data-stu-id="4ee58-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="4ee58-138">`helloworld/helloworld/settings.py` tiene la configuración de Django para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ee58-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="4ee58-139">`helloworld/helloworld/urls.py` tiene el código de asignación entre las direcciones URL y sus vistas respectivas.</span><span class="sxs-lookup"><span data-stu-id="4ee58-139">`helloworld/helloworld/urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="4ee58-140">Cree un nuevo archivo denominado views.py en el directorio /var/www/helloworld/helloworld.</span><span class="sxs-lookup"><span data-stu-id="4ee58-140">In the /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="4ee58-141">Este archivo contiene la vista que representa la página "hola mundo".</span><span class="sxs-lookup"><span data-stu-id="4ee58-141">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="4ee58-142">En el editor de código, escriba los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4ee58-142">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="4ee58-143">Reemplace el contenido del archivo urls.py por los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4ee58-143">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="4ee58-144">Instalación de Apache</span><span class="sxs-lookup"><span data-stu-id="4ee58-144">Set up Apache</span></span>
1. <span data-ttu-id="4ee58-145">Cree un archivo de configuración del host virtual de Apache en la carpeta /etc/apache2/sites-available/helloworld.conf.</span><span class="sxs-lookup"><span data-stu-id="4ee58-145">In the /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="4ee58-146">Establezca el contenido en los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="4ee58-146">Set the contents to the following values.</span></span> <span data-ttu-id="4ee58-147">Sustituya el elemento *yourVmName* por el nombre real de la máquina que va a usar (por ejemplo, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="4ee58-147">Replace *yourVmName* with the actual name of the machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="4ee58-148">Para activar el sitio, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ee58-148">To activate the site, use the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="4ee58-149">Para reiniciar Apache, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ee58-149">To restart Apache, use the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="4ee58-150">Cargue la página web en el explorador:</span><span class="sxs-lookup"><span data-stu-id="4ee58-150">Load the webpage in your browser:</span></span>
   
   ![Ventana del explorador que muestra la página Hola mundo en Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="4ee58-152">Apagado de la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="4ee58-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="4ee58-153">Cuando haya terminado este tutorial, es recomendable apagar o quitar la máquina virtual de Azure que se creó.</span><span class="sxs-lookup"><span data-stu-id="4ee58-153">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="4ee58-154">Esto libera recursos para otros tutoriales y evita cargos de uso de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee58-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

