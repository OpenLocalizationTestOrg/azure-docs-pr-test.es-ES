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
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="90299-103">Instalar Python y Hola SDK</span><span class="sxs-lookup"><span data-stu-id="90299-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="90299-104">Python es fácil tooset seguridad en Windows y viene preinstalado en Mac, Linux, y [Bash para Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="90299-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="90299-105">En esta guía se realizará un recorrido por la instalación y preparación de la máquina para su uso con Azure.</span><span class="sxs-lookup"><span data-stu-id="90299-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="90299-106">¿Qué es en Hola Python Azure SDK?</span><span class="sxs-lookup"><span data-stu-id="90299-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="90299-107">Hello Azure SDK para Python incluye componentes que le permiten toodevelop, implementar y administrar aplicaciones de Python para Azure.</span><span class="sxs-lookup"><span data-stu-id="90299-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="90299-108">En concreto, hello Azure SDK para Python incluye siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="90299-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="90299-109">**Bibliotecas de administración**.</span><span class="sxs-lookup"><span data-stu-id="90299-109">**Management libraries**.</span></span> <span data-ttu-id="90299-110">Estas bibliotecas de clases proporcionan una interfaz de administración de recursos de Azure, como cuentas de almacenamiento y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="90299-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="90299-111">**Bibliotecas tiempo de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="90299-111">**Runtime libraries**.</span></span> <span data-ttu-id="90299-112">Estas bibliotecas de clases proporcionan una interfaz para tener acceso a funciones de Azure, como el bus de servicio y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="90299-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="90299-113">Qué versión de Python y qué versión toouse</span><span class="sxs-lookup"><span data-stu-id="90299-113">Which Python and which version toouse</span></span>
<span data-ttu-id="90299-114">Existen varios modelos de intérpretes Python disponibles, entre los ejemplos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="90299-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="90299-115">CPython - intérprete de Python estándar y uso más frecuente de Hola</span><span class="sxs-lookup"><span data-stu-id="90299-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="90299-116">PyPy - tooCPython rápido, compatible con implementación alternativa</span><span class="sxs-lookup"><span data-stu-id="90299-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="90299-117">IronPython: El intérprete Python que se ejecuta en .Net/CLR.</span><span class="sxs-lookup"><span data-stu-id="90299-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="90299-118">Jython - intérprete de Python que se ejecuta en la máquina Virtual Java de Hola</span><span class="sxs-lookup"><span data-stu-id="90299-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="90299-119">**CPython** v2.7 o v3.3 + PyPy 5.4.0 probado y son compatibles con hello Python Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="90299-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="90299-120">¿Donde tooget Python?</span><span class="sxs-lookup"><span data-stu-id="90299-120">Where tooget Python?</span></span>
<span data-ttu-id="90299-121">Hay varias maneras tooget CPython:</span><span class="sxs-lookup"><span data-stu-id="90299-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="90299-122">Directamente desde [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="90299-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="90299-123">Desde una distribución de confianza como [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] o [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="90299-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="90299-124">Creación a partir del origen.</span><span class="sxs-lookup"><span data-stu-id="90299-124">Build from source!</span></span>

<span data-ttu-id="90299-125">A menos que tenga una necesidad concreta, se recomienda Hola dos primeras opciones.</span><span class="sxs-lookup"><span data-stu-id="90299-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="90299-126">Instalación del SDK en Windows, Linux y MacOS (solo bibliotecas de cliente)</span><span class="sxs-lookup"><span data-stu-id="90299-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="90299-127">Si ya tienes Python instalado, puede usar pip tooinstall una agrupación de todas las bibliotecas de cliente de hello en su entorno de Python 3.3 + o existente Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="90299-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="90299-128">Este paquete descargará los paquetes de saludo de hello [índice del paquete Python] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="90299-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="90299-129">Puede que necesite derechos de administrador:</span><span class="sxs-lookup"><span data-stu-id="90299-129">You may need administrator rights:</span></span>

* <span data-ttu-id="90299-130">Linux y MacOS, usar hello `sudo` comando: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="90299-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="90299-131">Windows: abra un símbolo del sistema/PowerShell como administrador</span><span class="sxs-lookup"><span data-stu-id="90299-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="90299-132">Puede instalar individualmente cada biblioteca para cada servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="90299-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="90299-133">Pueden instalar paquetes de vista previa con hello `--pre` marca:</span><span class="sxs-lookup"><span data-stu-id="90299-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="90299-134">También puede instalar un conjunto de bibliotecas de Azure en una sola línea con hello `azure` meta-package.</span><span class="sxs-lookup"><span data-stu-id="90299-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="90299-135">Puesto que no todos los paquetes de este paquete de metadatos se publican como estable aún, Hola `azure` meta-package aún está en vista previa.</span><span class="sxs-lookup"><span data-stu-id="90299-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="90299-136">Sin embargo, paquetes de núcleo de hello, desde las perspectivas de calidad/integridad de código se pueden considerar "estables" en este momento</span><span class="sxs-lookup"><span data-stu-id="90299-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="90299-137">se etiquetan oficialmente como tal en sincronización con otros lenguajes tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="90299-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="90299-138">No estamos planeando cambios más importantes realizados hasta ese momento.</span><span class="sxs-lookup"><span data-stu-id="90299-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="90299-139">Puesto que es una versión preliminar, necesita toouse hello `--pre` marca:</span><span class="sxs-lookup"><span data-stu-id="90299-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="90299-140">o directamente</span><span class="sxs-lookup"><span data-stu-id="90299-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="90299-141">Instalación de otros paquetes</span><span class="sxs-lookup"><span data-stu-id="90299-141">Getting More Packages</span></span>
<span data-ttu-id="90299-142">Hola [índice del paquete Python] [ Python Package Index] (PyPI) tiene una selección enriquecida de bibliotecas de Python.</span><span class="sxs-lookup"><span data-stu-id="90299-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="90299-143">Si ha elegido tooinstall una distribución, ya tendrá la mayoría de hello interesantes bits para diversos escenarios de web development tooTechnical Computing.</span><span class="sxs-lookup"><span data-stu-id="90299-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="90299-144">Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90299-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="90299-145">[Python Tools para Visual Studio][Python Tools para Visual Studio] (PTVS) es un complemento gratuito o software de código abierto (OSS) de Microsoft que convierte VS en un IDE de Python completo:</span><span class="sxs-lookup"><span data-stu-id="90299-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="90299-147">El uso de PTVS es opcional, pero es recomendable, ya que le proporciona compatibilidad con soluciones o proyectos de Web y Python, depuración, creación de perfiles, ventana interactiva, edición de plantillas e IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="90299-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="90299-148">PTVS también hace más fácil toodeploy tooMicrosoft Azure, con compatibilidad con la implementación demasiado[servicios en la nube](cloud-services/cloud-services-python-ptvs.md) y [sitios Web](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="90299-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="90299-149">PTVS funciona con su instalación de Visual Studio 2013, 2015 o 2017 existente.</span><span class="sxs-lookup"><span data-stu-id="90299-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="90299-150">Para obtener documentación, descargas y discusiones, consulte [Python Tools para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="90299-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="90299-151">Escenarios de Python Azure para Linux y MacOS</span><span class="sxs-lookup"><span data-stu-id="90299-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="90299-152">Para Linux o Mac OS, los escenarios principales de Azure que se admiten:</span><span class="sxs-lookup"><span data-stu-id="90299-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="90299-153">Consumir servicios de Azure mediante el uso de bibliotecas de cliente de Hola para Python</span><span class="sxs-lookup"><span data-stu-id="90299-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="90299-154">Ejecución de la aplicación en la VM de Linux</span><span class="sxs-lookup"><span data-stu-id="90299-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="90299-155">Desarrollar y publicar sitios Web tooAzure mediante Git</span><span class="sxs-lookup"><span data-stu-id="90299-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="90299-156">primer escenario de Hello permite tooauthor web enriquecido aplicaciones que aprovechan las ventajas del programa Hola a capacidades de PaaS de Azure como [almacenamiento de blobs](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [almacenamiento de colas](storage/queues/storage-python-how-to-use-queue-storage.md), [almacenamiento de tablas](cosmos-db/table-storage-how-to-use-python.md) etc. a través de contenedores Pythonic de hello las API de REST de Azure.</span><span class="sxs-lookup"><span data-stu-id="90299-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="90299-157">Estos funcionan de forma idéntica en Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="90299-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="90299-158">También puede usar estas bibliotecas de cliente desde su equipo de desarrollo local o en una máquina virtual de Linux que se ejecute en Azure.</span><span class="sxs-lookup"><span data-stu-id="90299-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="90299-159">Para el escenario VM de hello, iniciar una VM Linux de su elección (Ubuntu, CentOS, Suse) y lo que desee ejecutar y administrar.</span><span class="sxs-lookup"><span data-stu-id="90299-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="90299-160">Por ejemplo, puede ejecutar [IPython] [ IPython] REPL/Bloc de notas en su equipo Mac/Windows/Linux y el punto de su explorador tooa Linux o ejecución de máquina virtual de varios procesadores de Windows hello motor IPython en Azure.</span><span class="sxs-lookup"><span data-stu-id="90299-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="90299-161">Para obtener información acerca de cómo tooset una VM de Linux, vea hello [crear una máquina Virtual ejecuta Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span><span class="sxs-lookup"><span data-stu-id="90299-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="90299-162">Mediante la implementación de Git, puede desarrollar una aplicación web de Python y publicarlo tooan sitio Web de Azure desde cualquier sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="90299-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="90299-163">Cuando realice una inserción su tooAzure repositorio, crea automáticamente un entorno virtual y pip instala los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="90299-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="90299-164">Para obtener más información sobre el desarrollo y publicación de sitios Web de Azure, vea los tutoriales de Hola para [crear sitios Web con Django](app-service-web/web-sites-python-create-deploy-django-app.md), [crear sitios Web con Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), y [crear sitios Web con Matraz](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="90299-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="90299-165">Para obtener información general sobre el uso de cualquier marco de trabajo compatible con WSGI, consulte [Configuración de Python con Azure Websites](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="90299-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="90299-166">Recursos y software adicionales:</span><span class="sxs-lookup"><span data-stu-id="90299-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="90299-167">SDK de Azure para Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="90299-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="90299-168">Azure SDK para Python GitHub</span><span class="sxs-lookup"><span data-stu-id="90299-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="90299-169">Ejemplos oficiales de Azure para Python</span><span class="sxs-lookup"><span data-stu-id="90299-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="90299-170">[Distribución de Python de Continuum Analytics][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="90299-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="90299-171">[Distribución de Python de Enthought][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="90299-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="90299-172">[Distribución de Python de ActiveState][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="90299-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="90299-173">[SciPy: un conjunto de bibliotecas de Scientific Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="90299-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="90299-174">[NumPy: biblioteca de tipos numéricos para Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="90299-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="90299-175">[Django Project: un CMS o marco de trabajo para web maduro][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="90299-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="90299-176">[IPython: un bloc de notas o REPL avanzado para Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="90299-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="90299-177">[Herramientas de Python para Visual Studio en GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="90299-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="90299-178">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="90299-178">Python Developer Center</span></span>](/develop/python/)

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
