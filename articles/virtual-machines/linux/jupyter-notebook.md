---
title: aaaCreate un bloc de notas de IPython/Jupyter | Documentos de Microsoft
description: "Obtenga información acerca de cómo se crea toodeploy Hola Bloc de notas de IPython/Jupyter en una máquina virtual Linux con el modelo de implementación de administrador de recursos de hello en Azure."
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
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="f4f34-103">Creación de una máquina virtual de Azure, e instalación y ejecución de cuadernos de Jupyter Notebook en Azure</span><span class="sxs-lookup"><span data-stu-id="f4f34-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="f4f34-104">Hola [Jupyter proyecto](http://jupyter.org), Hola anteriormente [IPython proyecto](http://ipython.org), proporciona una colección de herramientas para informática científica con eficaces shells interactivos que combinan la ejecución de código con la creación de hello de un documento de cálculo activo.</span><span class="sxs-lookup"><span data-stu-id="f4f34-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="f4f34-105">Estos archivos del bloc de notas pueden contener texto arbitrario, fórmulas matemáticas, código de entrada, resultados, gráficos, vídeos y cualquier otra clase de contenido multimedia que pueda mostrar cualquier explorador web moderno.</span><span class="sxs-lookup"><span data-stu-id="f4f34-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="f4f34-106">Si el usuario está absolutamente nueva tooPython y desea toolearn en un divertido, entorno interactivo o realice algunas grave paralelo/técnico informática, hello Jupyter Notebook es una excelente opción.</span><span class="sxs-lookup"><span data-stu-id="f4f34-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="f4f34-107">![Captura de pantalla de](./media/jupyter-notebook/ipy-notebook-spectral.png) utilizando SciPy y Matplotlib paquetes tooanalyze Hola la estructura de una grabación de sonido.</span><span class="sxs-lookup"><span data-stu-id="f4f34-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="f4f34-108">Dos formas de Jupyter: Azure Notebooks o implementación personalizada</span><span class="sxs-lookup"><span data-stu-id="f4f34-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="f4f34-109">Azure proporciona un servicio que puede usar demasiado[comenzar rápidamente a usar Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4f34-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="f4f34-110">Mediante el uso de hello servicio de Azure Bloc de notas, puede obtener fácilmente interfaz web accesible del tooJupyter de acceso a los recursos de cálculo escalables con toda la eficacia de Hola de Python y sus muchas bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="f4f34-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="f4f34-111">Puesto que la instalación de Hola se controla mediante el servicio de hello, los usuarios pueden acceder a estos recursos sin necesidad de hello para la administración y configuración por usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f34-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="f4f34-112">Si el servicio de Bloc de notas de hello no funciona para su escenario continuar tooread este artículo que se le mostrará cómo toodeploy Hola Jupyter Notebook en Microsoft Azure, usando máquinas virtuales (VM) en Linux.</span><span class="sxs-lookup"><span data-stu-id="f4f34-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="f4f34-113">Creación y configuración de una máquina virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="f4f34-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="f4f34-114">primer paso de Hello es toocreate una máquina virtual (VM) que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f34-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="f4f34-115">Esta máquina virtual es un sistema operativo completo en la nube de Hola y se usará para ejecutar hello Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="f4f34-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="f4f34-116">Es capaz de ejecutar máquinas virtuales Linux y Windows Azure y se explicará el programa de instalación de Hola de Jupyter en ambos tipos de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f4f34-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="f4f34-117">Crear una máquina virtual de Linux y abrir un puerto para Jupyter</span><span class="sxs-lookup"><span data-stu-id="f4f34-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="f4f34-118">Siga las instrucciones de hello proporcionadas [aquí] [ portal-vm-linux] toocreate una máquina virtual de hello *Ubuntu* distribución.</span><span class="sxs-lookup"><span data-stu-id="f4f34-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="f4f34-119">En este tutorial se usa Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="f4f34-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="f4f34-120">Supondremos que el nombre de usuario de hello *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="f4f34-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="f4f34-121">Después de que implementa la máquina virtual de hello necesitamos tooopen de una regla de seguridad en el grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f34-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="f4f34-122">Desde Hola portal de Azure, vaya demasiado**grupos de seguridad de red** y pestaña abierta Hola Hola de grupo de seguridad correspondiente tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="f4f34-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="f4f34-123">Necesita tooadd una regla de seguridad de entrada con hello después de configuración: **TCP** para el protocolo de hello,  **\***  para el puerto de origen (público) hello y **9999** para puerto de destino (privado) de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f34-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![Instantánea](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="f4f34-125">Mientras que en el grupo de seguridad de red, haga clic en **Interfaces de red** Nota hello y **dirección IP pública** porque será necesaria tooconnect tooyour VM en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f34-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="f4f34-126">Instalar el software necesario en hello VM</span><span class="sxs-lookup"><span data-stu-id="f4f34-126">Install required software on hello VM</span></span>
<span data-ttu-id="f4f34-127">toorun Hola Jupyter Notebook en la máquina virtual, se deben instalar primero Jupyter y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f4f34-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="f4f34-128">Conectar máquinas virtuales de linux tooyour mediante ssh y Hola de par de nombre de usuario y contraseña de Hola que eligió al crear máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f4f34-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="f4f34-129">En este tutorial, se usará PuTTY y se conectará desde Windows.</span><span class="sxs-lookup"><span data-stu-id="f4f34-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="f4f34-130">Instalación de Jupyter en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f4f34-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="f4f34-131">Instalar Anaconda, una distribución de python de ciencia de datos muy popular, mediante uno de los vínculos de hello proporcionados a partir de [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="f4f34-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="f4f34-132">Redactar Hola de este documento, Hola vínculos siguientes son hello más seguridad toodate versiones.</span><span class="sxs-lookup"><span data-stu-id="f4f34-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="f4f34-133">Instalaciones de Anaconda para Linux</span><span class="sxs-lookup"><span data-stu-id="f4f34-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="f4f34-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="f4f34-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="f4f34-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="f4f34-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="f4f34-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="f4f34-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="f4f34-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="f4f34-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="f4f34-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="f4f34-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="f4f34-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="f4f34-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="f4f34-140">Instalación de Anaconda3 2.3.0 de 64 bits en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f4f34-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="f4f34-141">Como ejemplo, se trata de cómo puede instalar Anaconda en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f4f34-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Instantánea](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="f4f34-143">Configuración de Jupyter y uso de SSL</span><span class="sxs-lookup"><span data-stu-id="f4f34-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="f4f34-144">Después de instalar necesitamos tootake una archivos de configuración de momento toosetup Hola para Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f4f34-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="f4f34-145">Si experimenta problemas con la configuración de Jupyter puede ser útil toolook en hello [Jupyter documentación para ejecutar un servidor de Bloc de notas](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="f4f34-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="f4f34-146">Siguiente se `cd` toohello perfil directory toocreate nuestro certificado SSL y editar el archivo de configuración de perfiles de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f34-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="f4f34-147">En Linux usar hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="f4f34-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="f4f34-148">Usar hello después de certificado SSL de Hola de comando toocreate (Linux y Windows).</span><span class="sxs-lookup"><span data-stu-id="f4f34-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="f4f34-149">Tenga en cuenta que puesto que vamos a crear un certificado SSL autofirmado, cuando se conecta el Bloc de notas toohello el explorador le proporcionará una advertencia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f4f34-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="f4f34-150">Para su uso en producción a largo plazo, deberá toouse un certificado debidamente firmado asociado a su organización.</span><span class="sxs-lookup"><span data-stu-id="f4f34-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="f4f34-151">Puesto que la administración de certificados está más allá del ámbito de Hola de esta demostración, se quedará certificado autofirmado tooa por ahora.</span><span class="sxs-lookup"><span data-stu-id="f4f34-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="f4f34-152">Además toousing un certificado, también debe proporcionar una contraseña tooprotect del Bloc de notas de uso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="f4f34-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="f4f34-153">Por motivos de seguridad Jupyter utiliza contraseñas cifradas en su archivo de configuración, por lo que necesitará tooencrypt su contraseña en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="f4f34-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="f4f34-154">IPython proporciona un toodo utilidad en un símbolo del sistema ejecute hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="f4f34-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="f4f34-155">Esto le solicitará una contraseña y la confirmación y, a continuación, imprimirá la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f34-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="f4f34-156">Tenga en cuenta esto para hello siguiendo el paso.</span><span class="sxs-lookup"><span data-stu-id="f4f34-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="f4f34-157">A continuación, se modificará el archivo de configuración del perfil de hello, que es el `jupyter_notebook_config.py` archivo directorio Hola se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="f4f34-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="f4f34-158">Tenga en cuenta que este archivo no exista, basta con crear, si ese es el caso de hello.</span><span class="sxs-lookup"><span data-stu-id="f4f34-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="f4f34-159">Estearchivo tiene varios campos que, de manera predeterminada, se convierten en comentario.  Puede abrir este archivo con cualquier editor de texto de su gusto, y debe asegurarse de que al menos se Hola después de contenido.</span><span class="sxs-lookup"><span data-stu-id="f4f34-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="f4f34-160">**Ser seguro tooreplace hello c.NotebookApp.password en la configuración de hello con sha1 Hola del paso anterior hello**.</span><span class="sxs-lookup"><span data-stu-id="f4f34-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="f4f34-161">Ejecute hello Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="f4f34-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="f4f34-162">En este momento se está listo toostart hello Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="f4f34-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="f4f34-163">toodo, navegue toohello directory desee toostore blocs de notas y comenzar a servidor de Jupyter Notebook Hola con hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="f4f34-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="f4f34-164">Ahora debería ser capaz de tooaccess su Jupyter Notebook en la dirección de hello `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="f4f34-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="f4f34-165">Al acceder primero el Bloc de notas, página de inicio de sesión de hello solicita la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f4f34-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="f4f34-166">Y una vez que inicie sesión, verá el saludo "Jupyter Notebook panel", que es el centro de ontrol para todas las operaciones de Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f4f34-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="f4f34-167">Desde esta página se pueden crear cuadernos nuevos y abrir los existentes.</span><span class="sxs-lookup"><span data-stu-id="f4f34-167">From this page you can create new notebooks and open existing ones.</span></span>

![Instantánea](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="f4f34-169">Uso de hello Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="f4f34-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="f4f34-170">Si hace clic en hello **New** botón, verá Hola después de la página inicial.</span><span class="sxs-lookup"><span data-stu-id="f4f34-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![Instantánea](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="f4f34-172">área de Hello marcados con un `In []:` símbolo del sistema es el área de entrada de hello, aquí puede escribir cualquier código Python válido y se ejecutará cuando se alcance `Shift-Enter` o haga clic en el icono "Reproducir" hello (Hola triángulo hacia la derecha en la barra de herramientas de hello).</span><span class="sxs-lookup"><span data-stu-id="f4f34-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="f4f34-173">Los documentos informáticos activos con medios enriquecidos son un potente paradigma.</span><span class="sxs-lookup"><span data-stu-id="f4f34-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="f4f34-174">Bloc de notas de Hello propio se sentirá muy natural tooanyone que ha usado Python y un procesador de textos, porque es en cierto modo una combinación de ambos: puede ejecutar bloques de código de Python, pero también puede mantener notas y cualquier otro texto cambiando demasiado estilo de hello de una celda de "Código" "Ma rkdown"mediante el menú desplegable de hello en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="f4f34-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="f4f34-175">Jupyter es mucho más que un simple procesador de texto, debido a que permite combinar informática y medios enriquecidos (texto, gráficos, vídeo y prácticamente todos los elementos que se pueden mostrar en un explorador web moderno).</span><span class="sxs-lookup"><span data-stu-id="f4f34-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="f4f34-176">Puede combinar texto, código, vídeos, etc.</span><span class="sxs-lookup"><span data-stu-id="f4f34-176">You can mix, text, code, videos and more!</span></span>

![Instantánea](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="f4f34-178">Y la potencia de Hola de muchas bibliotecas excelente de Python para la informática científicos y técnicos, Hola siguiente captura de pantalla, se puede realizar un cálculo simple con hello mismo facilitar como un análisis de red compleja, todo ello en un entorno.</span><span class="sxs-lookup"><span data-stu-id="f4f34-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="f4f34-179">Este paradigma de mezcla potencia de Hola de web moderna Hola con cálculo en vivo ofrece muchas posibilidades y es ideal para la nube de hello; se puede utilizar Hola Bloc de notas:</span><span class="sxs-lookup"><span data-stu-id="f4f34-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="f4f34-180">Como una exploración toorecord de Bloc de notas de cálculo del trabajo en un problema.</span><span class="sxs-lookup"><span data-stu-id="f4f34-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="f4f34-181">el resultado es tooshare con compañeros, ya sea en forma de cálculo 'activo' o en copia impresa formatos (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="f4f34-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="f4f34-182">toodistribute y presente materiales teaching en vivo que implican el cálculo, por tanto, los alumnos inmediatamente pueden experimentar con el código real de hello, modificarlo y volver a ejecutan de forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="f4f34-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="f4f34-183">tooprovide "ejecutable del producto" que presentan los resultados de Hola de investigación de forma que puede reproducir inmediatamente, validar y ampliado por otras personas.</span><span class="sxs-lookup"><span data-stu-id="f4f34-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="f4f34-184">Como plataforma de informática en colaboración: varios usuarios pueden iniciar sesión en toothe mismo servidor de Bloc de notas tooshare una sesión de cálculo activa.</span><span class="sxs-lookup"><span data-stu-id="f4f34-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="f4f34-185">Si se dejan de código fuente de toohello IPython [repositorio][repository], encontrará todo un directorio con ejemplos de Bloc de notas que se pueden descargar y, a continuación, experimentar con en su propia máquina virtual Jupyter de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4f34-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="f4f34-186">Simplemente descargue hello `.ipynb` archivos de Hola de sitio y cargarlos en el panel de saludo de la máquina virtual de Azure del Bloc de notas (o descargarlos directamente en hello VM).</span><span class="sxs-lookup"><span data-stu-id="f4f34-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="f4f34-187">Conclusión</span><span class="sxs-lookup"><span data-stu-id="f4f34-187">Conclusion</span></span>
<span data-ttu-id="f4f34-188">Hola Jupyter Notebook proporciona una interfaz eficaz para tener acceso a power Hola del ecosistema de Python de hello en Azure de forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="f4f34-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="f4f34-189">Abarca una amplia variedad de casos de uso que incluye la exploración simple y el aprendizaje de Python, análisis de datos y visualización, simulación e informática en paralelo.</span><span class="sxs-lookup"><span data-stu-id="f4f34-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="f4f34-190">documentos de Bloc de notas de Hello resultantes contienen un registro completo de los cálculos de Hola que se llevan a cabo y se puede compartir con otros usuarios de Jupyter.</span><span class="sxs-lookup"><span data-stu-id="f4f34-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="f4f34-191">Hola Jupyter Notebook puede utilizarse como una aplicación local, pero es especialmente adecuado para las implementaciones de nube en Azure</span><span class="sxs-lookup"><span data-stu-id="f4f34-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="f4f34-192">las características básicas de Hola de Jupyter también están disponibles dentro de Visual Studio a través de la [Python Tools para Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="f4f34-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="f4f34-193">PTVS es un complemento gratuito y de código abiertode Microsoft que convierte a Visual Studio unentorno de desarrollo avanzado de Python, que incluye un editor avanzado con la integración de IntelliSense, depuración,creación de perfiles y la informática en paralelo.</span><span class="sxs-lookup"><span data-stu-id="f4f34-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4f34-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4f34-194">Next steps</span></span>
<span data-ttu-id="f4f34-195">Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f4f34-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
