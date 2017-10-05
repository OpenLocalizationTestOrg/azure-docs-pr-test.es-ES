---
title: "Creación de un cuaderno de Jupyter/IPython Notebook | Microsoft Docs"
description: "Obtenga información sobre cómo implementar Jupyter/IPhyton Notebook en una máquina virtual de Linux creada con el modelo de implementación del administrador de recursos en Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="a71c8-103">Creación de una máquina virtual de Azure, e instalación y ejecución de cuadernos de Jupyter Notebook en Azure</span><span class="sxs-lookup"><span data-stu-id="a71c8-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="a71c8-104">El [proyecto Jupyter](http://jupyter.org), anteriormente conocido como el [proyecto IPython](http://ipython.org), proporciona una colección de herramientas para la informática científica mediante eficaces shells interactivos que combinan la ejecución de código con la creación de documentos informáticos activos.</span><span class="sxs-lookup"><span data-stu-id="a71c8-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="a71c8-105">Estos archivos del bloc de notas pueden contener texto arbitrario, fórmulas matemáticas, código de entrada, resultados, gráficos, vídeos y cualquier otra clase de contenido multimedia que pueda mostrar cualquier explorador web moderno.</span><span class="sxs-lookup"><span data-stu-id="a71c8-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="a71c8-106">Independientemente de si no tiene experiencia con Python y desea aprender en un entorno entretenido e interactivo, o bien desea realizar informática técnica o en paralelo, Jupyter Notebook es una excelente elección.</span><span class="sxs-lookup"><span data-stu-id="a71c8-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="a71c8-107">![Captura de pantalla](./media/jupyter-notebook/ipy-notebook-spectral.png) Uso de los paquetes SciPy y Matplotlib para analizar la estructura de una grabación de sonido.</span><span class="sxs-lookup"><span data-stu-id="a71c8-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="a71c8-108">Dos formas de Jupyter: Azure Notebooks o implementación personalizada</span><span class="sxs-lookup"><span data-stu-id="a71c8-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="a71c8-109">Azure ofrece un servicio que puede usar para [comenzar rápidamente a usar Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="a71c8-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="a71c8-110">Si utiliza el servicio de Azure Notebook, puede obtener acceso fácilmente a la interfaz accesible desde la Web de Jupyter a los recursos informáticos escalables con toda la potencia de Python y sus diversas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="a71c8-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="a71c8-111">Debido a que el servicio administra la instalación, los usuarios pueden obtener acceso a estos recursos sin necesidad de que el usuario los administre y configure.</span><span class="sxs-lookup"><span data-stu-id="a71c8-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="a71c8-112">Si el servicio de cuaderno no sirve en el escenario en cuestión, siga leyendo este artículo, que mostrará cómo implementar Jupyter Notebook en Microsoft Azure, mediante máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="a71c8-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="a71c8-113">Creación y configuración de una máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="a71c8-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="a71c8-114">El primer paso es crear una máquina virtual (VM) que se ejecute en Azure.</span><span class="sxs-lookup"><span data-stu-id="a71c8-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="a71c8-115">Esta máquina virtual consiste en un sistema operativo completo en la nube y se usará para ejecutar Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="a71c8-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="a71c8-116">Azure es capaz de ejecutar máquinas virtuales de Linux y Windows y abarcaremos la configuración de Jupyter en ambos tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a71c8-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="a71c8-117">Crear una máquina virtual de Linux y abrir un puerto para Jupyter</span><span class="sxs-lookup"><span data-stu-id="a71c8-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="a71c8-118">Siga las instrucciones que aparecen [aquí][portal-vm-linux] para crear una máquina virtual de la distribución *Ubuntu*.</span><span class="sxs-lookup"><span data-stu-id="a71c8-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="a71c8-119">En este tutorial se usa Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="a71c8-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="a71c8-120">Asumiremos que el nombre de usuario es *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="a71c8-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="a71c8-121">Una vez que se implementa la máquina virtual, es necesario abrir una regla de seguridad en el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="a71c8-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="a71c8-122">En Azure Portal, vaya a **Grupos de seguridad de red** y abra la pestaña del grupo de seguridad que corresponde a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a71c8-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="a71c8-123">Debe agregar una regla de seguridad de entrada con la configuración siguiente: **TCP** para el protocolo, **\*** para el puerto de origen (público) y **9999** para el puerto de destino (privado).</span><span class="sxs-lookup"><span data-stu-id="a71c8-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![Instantánea](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="a71c8-125">En el grupo de seguridad de red, haga clic en **Interfaces de red** y anote la **dirección IP pública**, la necesitará para conectarse a la máquina virtual en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="a71c8-126">Instalación del software necesario en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a71c8-126">Install required software on the VM</span></span>
<span data-ttu-id="a71c8-127">Para ejecutar Jupyter Notebook en nuestra máquina virtual, primero debemos instalar Jupyter y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="a71c8-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="a71c8-128">Conéctese a la máquina virtual de Linux con SSH y el par de nombre de usuario/contraseña que eligió cuando creó la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a71c8-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="a71c8-129">En este tutorial, se usará PuTTY y se conectará desde Windows.</span><span class="sxs-lookup"><span data-stu-id="a71c8-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="a71c8-130">Instalación de Jupyter en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a71c8-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="a71c8-131">Instale Anaconda, una popular distribución de Python para ciencia de datos, desde uno de los vínculos proporcionados por [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="a71c8-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="a71c8-132">En el momento de redactar este documento, los vínculos que aparecen a continuación son las versiones más actualizadas.</span><span class="sxs-lookup"><span data-stu-id="a71c8-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="a71c8-133">Instalaciones de Anaconda para Linux</span><span class="sxs-lookup"><span data-stu-id="a71c8-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="a71c8-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="a71c8-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="a71c8-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="a71c8-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="a71c8-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="a71c8-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="a71c8-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="a71c8-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="a71c8-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="a71c8-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="a71c8-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="a71c8-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="a71c8-140">Instalación de Anaconda3 2.3.0 de 64 bits en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a71c8-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="a71c8-141">Como ejemplo, se trata de cómo puede instalar Anaconda en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a71c8-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Instantánea](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="a71c8-143">Configuración de Jupyter y uso de SSL</span><span class="sxs-lookup"><span data-stu-id="a71c8-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="a71c8-144">Después de la instalación, necesitamos un momento para configurar los archivos de configuración de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="a71c8-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="a71c8-145">Si experimenta problemas con la configuración de Jupyter, puede resultar útil consultar la [documentación de Jupyter para ejecutar un servidor de Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="a71c8-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="a71c8-146">A continuación, mediante el comando `cd` , cámbiese al directorio del perfil para crear nuestro certificado SSL y modifique el archivo de configuración de perfiles.</span><span class="sxs-lookup"><span data-stu-id="a71c8-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="a71c8-147">En Linux, use el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="a71c8-148">Utilice el comando siguiente para crear el certificado SSL (Linux y Windows).</span><span class="sxs-lookup"><span data-stu-id="a71c8-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="a71c8-149">Tenga en cuenta que como estamos creando un certificado SSL autofirmado, al conectarse al bloc de notas el explorador le mostrará una advertencia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="a71c8-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="a71c8-150">En un uso de producción a largo plazo, querrá utilizar un certificado correctamente firmado asociado a la organización.</span><span class="sxs-lookup"><span data-stu-id="a71c8-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="a71c8-151">Como la administración de certificados va más allá del ámbito de esta demostración, de momento nos ceñiremos a un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="a71c8-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="a71c8-152">Además de utilizar un certificado, también debe proporcionar una contraseña para proteger el bloc de notas de un uso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="a71c8-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="a71c8-153">Por motivos de seguridad, Jupyter usa contraseñas cifradas en su archivo de configuración, por lo que deberá cifrar primero la contraseña.</span><span class="sxs-lookup"><span data-stu-id="a71c8-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="a71c8-154">IPython proporciona una utilidad para hacerlo; en el símbolo del sistema ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="a71c8-155">Se le solicitará una contraseña y su confirmación y, luego, se imprimirá la contraseña.</span><span class="sxs-lookup"><span data-stu-id="a71c8-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="a71c8-156">Anótela para el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="a71c8-157">A continuación, editaremos el archivo de configuración del perfil, que es el archivo `jupyter_notebook_config.py` del directorio en que se encuentra.</span><span class="sxs-lookup"><span data-stu-id="a71c8-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="a71c8-158">Observe que es posible que este archivo no exista. Si es así, simplemente créelo.</span><span class="sxs-lookup"><span data-stu-id="a71c8-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="a71c8-159">Estearchivo tiene varios campos que, de manera predeterminada, se convierten en comentario.</span><span class="sxs-lookup"><span data-stu-id="a71c8-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="a71c8-160">Puede abrir este archivo con el editor de texto que prefiera y debe asegurase de que al menos tiene el contenido siguiente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="a71c8-161">**Asegúrese de reemplazar c.NotebookApp.password en la configuración por sha1 del paso anterior**.</span><span class="sxs-lookup"><span data-stu-id="a71c8-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="a71c8-162">Ejecutar Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="a71c8-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="a71c8-163">En este momento, estamos preparados para iniciar Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="a71c8-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="a71c8-164">Para ello, vaya al directorio en el que desea almacenar los cuadernos e inicie el servidor Jupyter Notebook con el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="a71c8-165">Ahora debería poder tener acceso a Jupyter Notebook en la dirección `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="a71c8-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="a71c8-166">La primera vez que se accede a un cuaderno, la página de inicio de sesión pide una contraseña.</span><span class="sxs-lookup"><span data-stu-id="a71c8-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="a71c8-167">Y una vez que haya iniciado sesión, verá el "panel de control de Jupyter Notebook", que es el centro de control para todas las operaciones del cuaderno.</span><span class="sxs-lookup"><span data-stu-id="a71c8-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="a71c8-168">Desde esta página se pueden crear cuadernos nuevos y abrir los existentes.</span><span class="sxs-lookup"><span data-stu-id="a71c8-168">From this page you can create new notebooks and open existing ones.</span></span>

![Instantánea](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="a71c8-170">Uso de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="a71c8-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="a71c8-171">Si hace clic en el botón **Nuevo** , verá que se abre la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-171">If you click the **New** button, you will see the following opening page.</span></span>

![Instantánea](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="a71c8-173">El área marcada con el mensaje `In []:` es el área de entrada y ahí puede escribir cualquier código Python válido, que se ejecutará cuando presione `Shift-Enter` o haga clic en el icono "Play" (el triángulo que apunta a la derecha en la barra de herramientas).</span><span class="sxs-lookup"><span data-stu-id="a71c8-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="a71c8-174">Los documentos informáticos activos con medios enriquecidos son un potente paradigma.</span><span class="sxs-lookup"><span data-stu-id="a71c8-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="a71c8-175">El propio cuaderno le resultará muy familiar a cualquiera que haya utilizado Python y un procesador de textos, ya que, en cierto modo, es una mezcla de ambas cosas: permite ejecutar bloques de código de Python, pero también permite conservar notas y cualquier otro texto cambiando el estilo de una celda de "Code" a "Markdown" con el menú desplegable de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="a71c8-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="a71c8-176">Jupyter es mucho más que un simple procesador de texto, debido a que permite combinar informática y medios enriquecidos (texto, gráficos, vídeo y prácticamente todos los elementos que se pueden mostrar en un explorador web moderno).</span><span class="sxs-lookup"><span data-stu-id="a71c8-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="a71c8-177">Puede combinar texto, código, vídeos, etc.</span><span class="sxs-lookup"><span data-stu-id="a71c8-177">You can mix, text, code, videos and more!</span></span>

![Instantánea](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="a71c8-179">Y con la potencia de las gran cantidad de excelentes bibliotecas de Python para la informática técnica y científica, en la siguiente captura de pantalla, se puede realizar un cálculo simple con la misma facilidad que un análisis de red complejo, todo ello en un único entorno.</span><span class="sxs-lookup"><span data-stu-id="a71c8-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="a71c8-180">Este paradigma de combinar la potencia de la web moderna con la informática activa ofrece muchas posibilidades, y es perfectamente adecuado para la nube; el bloc de notas se puede usar:</span><span class="sxs-lookup"><span data-stu-id="a71c8-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="a71c8-181">Como bloc de dictado de cálculo para registrar el trabajo de exploración sobre un problema.</span><span class="sxs-lookup"><span data-stu-id="a71c8-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="a71c8-182">Para compartir resultados con compañeros, ya sea en forma de cálculo "activo" o en formatos para impresión (HTML, PDF),</span><span class="sxs-lookup"><span data-stu-id="a71c8-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="a71c8-183">Para distribuir y presentar materiales de formación dinámicos que impliquen cálculos, con el fin de que los estudiantes puedan experimentar inmediatamente con el código real, modificarlo y volver a ejecutarlo de manera interactiva.</span><span class="sxs-lookup"><span data-stu-id="a71c8-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="a71c8-184">Para proporcionar "documentos ejecutables" que presentan los resultados de la investigación de manera que otras puedan reproducirlos, validarlos y ampliarlos inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="a71c8-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="a71c8-185">Como plataforma de informática de colaboración: varios usuarios pueden iniciar sesión en el mismo servidor de IPython Notebook para compartir una sesión de cálculo dinámica.</span><span class="sxs-lookup"><span data-stu-id="a71c8-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="a71c8-186">Si va al [repositorio][repository] de código fuente de IPython, encontrará un directorio completo con ejemplos de cuadernos que se pueden descargar para experimentar en su propia máquina virtual de Jupyter de Azure.</span><span class="sxs-lookup"><span data-stu-id="a71c8-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="a71c8-187">Solo tiene que descargar los archivos `.ipynb` desde el sitio y cargarlos en el panel de la máquina virtual del bloc de notas de Azure (o descargarlos directamente en la máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="a71c8-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="a71c8-188">Conclusión</span><span class="sxs-lookup"><span data-stu-id="a71c8-188">Conclusion</span></span>
<span data-ttu-id="a71c8-189">Jupyter Notebook brinda una sólida interfaz para tener acceso de manera interactiva a la potencia del ecosistema Python en Azure.</span><span class="sxs-lookup"><span data-stu-id="a71c8-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="a71c8-190">Abarca una amplia variedad de casos de uso que incluye la exploración simple y el aprendizaje de Python, análisis de datos y visualización, simulación e informática en paralelo.</span><span class="sxs-lookup"><span data-stu-id="a71c8-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="a71c8-191">Los documentos de Notebook resultantes contienen un registro completo de los cálculos que se realizan y que se pueden compartir con otros usuarios de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="a71c8-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="a71c8-192">Jupyter Notebook se puede usar como aplicación local, pero es perfectamente adecuado para implementaciones de nube en Azure.</span><span class="sxs-lookup"><span data-stu-id="a71c8-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="a71c8-193">Las características centrales de Jupyter también está disponibles en Visual Studio mediante [Python Tools para Visual Studio][Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="a71c8-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="a71c8-194">PTVS es un complemento gratuito y de código abiertode Microsoft que convierte a Visual Studio unentorno de desarrollo avanzado de Python, que incluye un editor avanzado con la integración de IntelliSense, depuración,creación de perfiles y la informática en paralelo.</span><span class="sxs-lookup"><span data-stu-id="a71c8-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a71c8-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a71c8-195">Next steps</span></span>
<span data-ttu-id="a71c8-196">Para más información, vea el [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="a71c8-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
