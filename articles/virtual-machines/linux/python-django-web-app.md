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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Aplicación web Django Hello World en una máquina virtual Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac o Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Este tutorial muestra cómo toohost un sitio Web basado en Django en Linux en máquinas virtuales de Azure. En el tutorial de hello, no suponemos ninguna experiencia previa con Azure. Cuando termine de tutorial de hello, puede tener una aplicación basada en Django se pueden instalar y ejecutar en la nube de Hola.

Obtenga información sobre cómo:

* Configurar un toohost Django de máquina virtual de Azure. Aunque este tutorial le explica cómo toodo para **Linux**, puede hacer hello iguales para una VM de Windows Server hospedados en Azure. 
* Cree una nueva aplicación Django en Linux.

Hola tutorial le mostrará cómo toobuild un básica Hello World web application. aplicación Hello se hospeda en una máquina virtual de Azure.

Hola siguiente captura de pantalla muestra la aplicación hello completado:

![Una ventana del explorador muestra la página de Hola Hola a todos en Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Crear y configurar un toohost Django de máquina virtual de Azure

1. vea toocreate una máquina virtual de Azure con hello distribución Ubuntu Server 14.04 LTS, [crear una máquina virtual Linux en el portal de Azure hello](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). También puede elegir una autenticación de contraseña en lugar de usar la clave pública SSH.
2. tooedit Hola red seguridad grupo tooallow entrante HTTP tráfico tooport 80, consulte [crear grupos de seguridad de red en el portal de Azure hello](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Opcional) De forma predeterminada, la nueva máquina virtual no tiene un nombre de dominio completo (FQDN).  toocreate una máquina virtual con un FQDN, vea [crear un FQDN de hello portal de Azure para una VM de Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Este paso no es necesario para completar este tutorial.

## <a id="setup"></a>Configurar el entorno de desarrollo de Hola
> [!NOTE]
> Si necesita tooinstall Python o desea bibliotecas de cliente de toouse hello, vea hello [Guía de instalación de Python](../../python-how-to-install.md).

Hola Ubuntu Linux VM tiene preinstalado de Python 2.7, pero no proceder con Apache o Django. Complete Hola siguiendo los pasos tooconnect tooyour máquina virtual e instale Apache y Django:

1. Abra una nueva ventana de terminal.
2. tooconnect toohello VM de Azure, escriba Hola siguiente comando. Si no creó un FQDN, puede conectarse mediante el uso de la dirección IP pública Hola que se muestra en la máquina virtual de hello resumen Hola portal de Azure.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, escriba Hola siguientes comandos:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache con mod-wsgi, escriba Hola siguiente comando:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Creación de una aplicación Django
1. toouse tooaccess SSH su máquina virtual, la ventana de Terminal de hello abierto que usaste en hello sección anterior.
2. toocreate un nuevo proyecto de Django, escriba Hola siguientes comandos:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Hola `django-admin.py` secuencia de comandos genera una estructura básica de sitios Web basados en Django:
   
   * `helloworld/manage.py` le ayuda a iniciar y detener el hospedaje del sitio web basado en Django.
   * `helloworld/helloworld/settings.py` tiene la configuración de Django para la aplicación.
   * `helloworld/helloworld/urls.py`tiene código de asignación de hello entre cada dirección URL y su vista.
3. En el directorio de /var/www/helloworld/helloworld hello, cree un nuevo archivo denominado views.py. Este archivo tiene la vista de Hola que representa la página de "Hola a todos" Hola. En el editor de código, escriba Hola siguientes comandos:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Reemplace el contenido de hello del archivo de urls.py de hello con hello siguientes comandos:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Instalación de Apache
1. En la carpeta de /etc/apache2/sites-available/helloworld.conf hello, cree un archivo de configuración de host virtual de Apache. Establecer Hola contenido toohello después de valores. Reemplace *Nombredesuvm* con nombre real de Hola de máquina de hello está utilizando (por ejemplo, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. sitio de hello tooactivate, Hola de uso siguiente comando:
   
       $ sudo a2ensite helloworld
3. toorestart Apache, utilice Hola siguiente comando:
   
       $ sudo service apache2 reload
4. Carga la página Web de hello en el explorador:
   
   ![Una ventana del explorador muestra la página de hello hello world en Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Apagado de la máquina virtual de Azure
Cuando haya terminado con este tutorial, se recomienda apagar o quitar la máquina virtual de Azure que creó para el tutorial de Hola Hola. Esto libera recursos para otros tutoriales y evita cargos de uso de Azure.

