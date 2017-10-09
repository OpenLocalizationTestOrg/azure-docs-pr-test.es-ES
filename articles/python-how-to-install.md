---
title: hello SDK - Azure y aaaInstall Python
description: "Obtenga información acerca de cómo toouse SDK de tooinstall hello y Python con Azure."
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a>Instalar Python y Hola SDK
Python es fácil tooset seguridad en Windows y viene preinstalado en Mac, Linux, y [Bash para Windows](https://msdn.microsoft.com/commandline/wsl/about). En esta guía se realizará un recorrido por la instalación y preparación de la máquina para su uso con Azure.

## <a name="whats-in-hello-python-azure-sdk"></a>¿Qué es en Hola Python Azure SDK?
Hello Azure SDK para Python incluye componentes que le permiten toodevelop, implementar y administrar aplicaciones de Python para Azure. En concreto, hello Azure SDK para Python incluye siguiente de hello:

* **Bibliotecas de administración**. Estas bibliotecas de clases proporcionan una interfaz de administración de recursos de Azure, como cuentas de almacenamiento y máquinas virtuales.
* **Bibliotecas tiempo de ejecución**. Estas bibliotecas de clases proporcionan una interfaz para tener acceso a funciones de Azure, como el bus de servicio y almacenamiento.

## <a name="which-python-and-which-version-toouse"></a>Qué versión de Python y qué versión toouse
Existen varios modelos de intérpretes Python disponibles, entre los ejemplos se incluyen los siguientes:

* CPython - intérprete de Python estándar y uso más frecuente de Hola
* PyPy - tooCPython rápido, compatible con implementación alternativa
* IronPython: El intérprete Python que se ejecuta en .Net/CLR.
* Jython - intérprete de Python que se ejecuta en la máquina Virtual Java de Hola

**CPython** v2.7 o v3.3 + PyPy 5.4.0 probado y son compatibles con hello Python Azure SDK.

## <a name="where-tooget-python"></a>¿Donde tooget Python?
Hay varias maneras tooget CPython:

* Directamente desde [www.python.org][www.python.org]
* Desde una distribución de confianza como [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] o [www.activestate.com][www.activestate.com]
* Creación a partir del origen.

A menos que tenga una necesidad concreta, se recomienda Hola dos primeras opciones.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Instalación del SDK en Windows, Linux y MacOS (solo bibliotecas de cliente)
Si ya tienes Python instalado, puede usar pip tooinstall una agrupación de todas las bibliotecas de cliente de hello en su entorno de Python 3.3 + o existente Python 2.7. Este paquete descargará los paquetes de saludo de hello [índice del paquete Python] [ Python Package Index] (PyPI).

Puede que necesite derechos de administrador:

* Linux y MacOS, usar hello `sudo` comando: `sudo pip install azure-mgmt-compute`.
* Windows: abra un símbolo del sistema/PowerShell como administrador

Puede instalar individualmente cada biblioteca para cada servicio de Azure:

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Pueden instalar paquetes de vista previa con hello `--pre` marca:

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

También puede instalar un conjunto de bibliotecas de Azure en una sola línea con hello `azure` meta-package. Puesto que no todos los paquetes de este paquete de metadatos se publican como estable aún, Hola `azure` meta-package aún está en vista previa.
Sin embargo, paquetes de núcleo de hello, desde las perspectivas de calidad/integridad de código se pueden considerar "estables" en este momento

* se etiquetan oficialmente como tal en sincronización con otros lenguajes tan pronto como sea posible.
  No estamos planeando cambios más importantes realizados hasta ese momento.

Puesto que es una versión preliminar, necesita toouse hello `--pre` marca:

```console
   $ pip install --pre azure
```

o directamente

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>Instalación de otros paquetes
Hola [índice del paquete Python] [ Python Package Index] (PyPI) tiene una selección enriquecida de bibliotecas de Python.  Si ha elegido tooinstall una distribución, ya tendrá la mayoría de hello interesantes bits para diversos escenarios de web development tooTechnical Computing.

## <a name="python-tools-for-visual-studio"></a>Python Tools para Visual Studio
[Python Tools para Visual Studio][Python Tools para Visual Studio] (PTVS) es un complemento gratuito o software de código abierto (OSS) de Microsoft que convierte VS en un IDE de Python completo:

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

El uso de PTVS es opcional, pero es recomendable, ya que le proporciona compatibilidad con soluciones o proyectos de Web y Python, depuración, creación de perfiles, ventana interactiva, edición de plantillas e IntelliSense.

PTVS también hace más fácil toodeploy tooMicrosoft Azure, con compatibilidad con la implementación demasiado[servicios en la nube](cloud-services/cloud-services-python-ptvs.md) y [sitios Web](app-service-web/web-sites-python-ptvs-django-mysql.md).

PTVS funciona con su instalación de Visual Studio 2013, 2015 o 2017 existente.  Para obtener documentación, descargas y discusiones, consulte [Python Tools para Visual Studio].  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Escenarios de Python Azure para Linux y MacOS
Para Linux o Mac OS, los escenarios principales de Azure que se admiten:

1. Consumir servicios de Azure mediante el uso de bibliotecas de cliente de Hola para Python
2. Ejecución de la aplicación en la VM de Linux
3. Desarrollar y publicar sitios Web tooAzure mediante Git

primer escenario de Hello permite tooauthor web enriquecido aplicaciones que aprovechan las ventajas del programa Hola a capacidades de PaaS de Azure como [almacenamiento de blobs](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [almacenamiento de colas](storage/queues/storage-python-how-to-use-queue-storage.md), [almacenamiento de tablas](cosmos-db/table-storage-how-to-use-python.md) etc. a través de contenedores Pythonic de hello las API de REST de Azure. Estos funcionan de forma idéntica en Windows, Mac y Linux.  También puede usar estas bibliotecas de cliente desde su equipo de desarrollo local o en una máquina virtual de Linux que se ejecute en Azure.

Para el escenario VM de hello, iniciar una VM Linux de su elección (Ubuntu, CentOS, Suse) y lo que desee ejecutar y administrar.  Por ejemplo, puede ejecutar [IPython] [ IPython] REPL/Bloc de notas en su equipo Mac/Windows/Linux y el punto de su explorador tooa Linux o ejecución de máquina virtual de varios procesadores de Windows hello motor IPython en Azure.

Para obtener información acerca de cómo tooset una VM de Linux, vea hello [crear una máquina Virtual ejecuta Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.

Mediante la implementación de Git, puede desarrollar una aplicación web de Python y publicarlo tooan sitio Web de Azure desde cualquier sistema operativo.  Cuando realice una inserción su tooAzure repositorio, crea automáticamente un entorno virtual y pip instala los paquetes necesarios.

Para obtener más información sobre el desarrollo y publicación de sitios Web de Azure, vea los tutoriales de Hola para [crear sitios Web con Django](app-service-web/web-sites-python-create-deploy-django-app.md), [crear sitios Web con Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), y [crear sitios Web con Matraz](app-service-web/web-sites-python-create-deploy-flask-app.md). Para obtener información general sobre el uso de cualquier marco de trabajo compatible con WSGI, consulte [Configuración de Python con Azure Websites](app-service-web/web-sites-python-configure.md).

## <a name="additional-software-and-resources"></a>Recursos y software adicionales:
* [SDK de Azure para Python ReadTheDocs](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Azure SDK para Python GitHub](https://github.com/Azure/azure-sdk-for-python)
* [Ejemplos oficiales de Azure para Python](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Distribución de Python de Continuum Analytics][Continuum Analytics Python Distribution]
* [Distribución de Python de Enthought][Enthought Python Distribution]
* [Distribución de Python de ActiveState][ActiveState Python Distribution]
* [SciPy: un conjunto de bibliotecas de Scientific Python][SciPy - A suite of Scientific Python libraries]
* [NumPy: biblioteca de tipos numéricos para Python][NumPy - A numerics library for Python]
* [Django Project: un CMS o marco de trabajo para web maduro][Django Project - A mature web framework/CMS]
* [IPython: un bloc de notas o REPL avanzado para Python][IPython - an advanced REPL/Notebook for Python]
* [Herramientas de Python para Visual Studio en GitHub][Python Tools for Visual Studio on GitHub]
* [Centro para desarrolladores de Python](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
