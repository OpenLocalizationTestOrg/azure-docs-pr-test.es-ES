---
title: "Hola aaaUsing extensión de máquina virtual de Docker para Linux en Azure"
description: "Describe Docker y extensiones de máquinas virtuales de Azure de Hola y muestra cómo tooprogrammatically crear máquinas virtuales en Azure que son hosts de docker desde la línea de comandos de hello mediante Hola CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="ce06c-103">Uso de hello extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="ce06c-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="ce06c-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ce06c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ce06c-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="ce06c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ce06c-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce06c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ce06c-107">Para obtener información acerca del uso de extensión de máquina virtual Docker Hola con modelo de administrador de recursos de hello, consulte [aquí](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ce06c-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ce06c-108">Este tema describe cómo toocreate una máquina virtual con hello extensión de máquina virtual Docker de hello service modo de administración (asm) de CLI de Azure en cualquier plataforma.</span><span class="sxs-lookup"><span data-stu-id="ce06c-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="ce06c-109">[Docker](https://www.docker.com/) es uno de hello más populares enfoques de virtualización que utiliza [contenedores Linux](http://en.wikipedia.org/wiki/LXC) en lugar de máquinas virtuales como una manera de aislar los datos y calcular en recursos compartidos.</span><span class="sxs-lookup"><span data-stu-id="ce06c-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="ce06c-110">Puede usar la extensión de máquina virtual Docker de Hola y Hola [agente Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate una máquina virtual de Docker que hospeda cualquier número de contenedores para las aplicaciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="ce06c-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="ce06c-111">toosee un análisis de alto nivel de los contenedores y sus ventajas, vea hello [Docker alto nivel Pizarra](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="ce06c-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="ce06c-112">¿Cómo toouse Hola extensión de máquina virtual de Docker con Azure</span><span class="sxs-lookup"><span data-stu-id="ce06c-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="ce06c-113">extensión de máquina virtual Docker de hello toouse con Azure, debe instalar una versión de hello [interfaz de línea de comandos de Azure](https://github.com/Azure/azure-sdk-tools-xplat) (CLI de Azure) mayor que 0.8.6 (ya que de este hello escritura versión actual es 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="ce06c-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="ce06c-114">Puede instalar Hola CLI de Azure en Mac, Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="ce06c-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="ce06c-115">completar el proceso de Hello toouse Docker en Azure es sencillo:</span><span class="sxs-lookup"><span data-stu-id="ce06c-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="ce06c-116">Instalar Hola CLI de Azure y sus dependencias en equipo Hola desde el que desea toocontrol Azure (en Windows, será una distribución de Linux que se ejecuta como una máquina virtual)</span><span class="sxs-lookup"><span data-stu-id="ce06c-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="ce06c-117">Utilizar hello Azure CLI Docker comandos toocreate un host de máquina virtual Docker en Azure</span><span class="sxs-lookup"><span data-stu-id="ce06c-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="ce06c-118">Utilice Hola local Docker comandos toomanage los contenedores de Docker en la VM de Docker en Azure.</span><span class="sxs-lookup"><span data-stu-id="ce06c-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="ce06c-119">Instalar hello Azure interfaz de línea de comandos (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="ce06c-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="ce06c-120">tooinstall y configurar Hola CLI de Azure, consulte [cómo tooinstall Hola interfaz de línea de comandos de Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ce06c-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="ce06c-121">instalación de hello tooconfirm, tipo `azure` en línea de comandos de Hola y después de un breve momento debería ver Hola arte ASCII de CLI de Azure, que enumera Hola basic comandos tooyou disponible.</span><span class="sxs-lookup"><span data-stu-id="ce06c-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="ce06c-122">Si funcionó correctamente la instalación de hello, debe ser capaz de tootype `azure help vm` y que uno de los comandos de hello aparecen es "docker".</span><span class="sxs-lookup"><span data-stu-id="ce06c-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="ce06c-123">Docker tiene herramientas para Windows, [Docker máquina](https://docs.docker.com/installation/windows/), que también puede utilizar la creación de hello tooautomate de un cliente que puede usar toowork con máquinas virtuales de Azure como hosts de docker.</span><span class="sxs-lookup"><span data-stu-id="ce06c-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="ce06c-124">Conectar hello Azure CLI tootooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="ce06c-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="ce06c-125">Antes de poder usar Hola CLI de Azure debe asociar las credenciales de cuenta de Azure con hello CLI de Azure en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="ce06c-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="ce06c-126">Hola sección [cómo tooconnect tooyour suscripción de Azure](../../../xplat-cli-connect.md) explica cómo tooeither descargar e importar su **.publishsettings** de archivos o asociar la CLI de Azure con un Id. de organización.</span><span class="sxs-lookup"><span data-stu-id="ce06c-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="ce06c-127">Hay algunas diferencias de comportamiento cuando se usa una o hello otros métodos de autenticación, por lo que sea seguro tooread Hola documento por encima de una funcionalidad diferente toounderstand Hola.</span><span class="sxs-lookup"><span data-stu-id="ce06c-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="ce06c-128">Instalar a Docker y usar hello Docker extensión de máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="ce06c-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="ce06c-129">Siga hello [las instrucciones de instalación de Docker](https://docs.docker.com/installation/#installation) tooinstall Docker localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ce06c-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="ce06c-130">toouse Docker con máquinas virtuales de Azure, imagen de Linux de hello utilizada para hello VM debe tener hello [agente de VM de Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) instalado.</span><span class="sxs-lookup"><span data-stu-id="ce06c-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="ce06c-131">Actualmente, solamente hay dos tipos de imágenes que proporcionan esto:</span><span class="sxs-lookup"><span data-stu-id="ce06c-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="ce06c-132">Una imagen de Ubuntu desde la Galería de imágenes de Azure de Hola o</span><span class="sxs-lookup"><span data-stu-id="ce06c-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="ce06c-133">Una imagen personalizada de Linux que se crearon con hello agente de VM de Linux de Azure instalado y configurado.</span><span class="sxs-lookup"><span data-stu-id="ce06c-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="ce06c-134">Vea [agente de VM de Linux de Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener más información acerca de cómo toobuild una VM de Linux personalizado con hello agente de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ce06c-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="ce06c-135">Uso de la Galería de imágenes de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="ce06c-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="ce06c-136">Desde una sesión de Terminal o intensiva de errores, usar hello después toolocate Hola imagen Ubuntu más reciente en hello VM Galería toouse escribiendo el comando de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ce06c-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="ce06c-137">y seleccione uno de los nombres de imagen de hello, como `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, y comando de uso Hola siguiente toocreate una nueva máquina virtual con esa imagen.</span><span class="sxs-lookup"><span data-stu-id="ce06c-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="ce06c-138">donde:</span><span class="sxs-lookup"><span data-stu-id="ce06c-138">where:</span></span>

* <span data-ttu-id="ce06c-139">*&lt;nombre de la máquina virtual cloudservice&gt;*  es nombre Hola de hello VM que se convertirá en el equipo de host de contenedor de Docker de hello en Azure</span><span class="sxs-lookup"><span data-stu-id="ce06c-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="ce06c-140">*&lt;nombre de usuario&gt;*  es Hola nombre de usuario del usuario de raíz predeterminado de Hola de hello VM</span><span class="sxs-lookup"><span data-stu-id="ce06c-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="ce06c-141">*&lt;contraseña&gt;*  es contraseña Hola de hello *nombre de usuario* cuenta de que cumple los estándares de Hola de complejidad de Azure</span><span class="sxs-lookup"><span data-stu-id="ce06c-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="ce06c-142">Actualmente, una contraseña debe tener al menos 8 caracteres, contener minúscula y una letra mayúscula, un número y un carácter especial, como uno de los siguientes caracteres de hello: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="ce06c-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="ce06c-143">No, período de hello final Hola de hello anterior frase no es un carácter especial.</span><span class="sxs-lookup"><span data-stu-id="ce06c-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="ce06c-144">Si el comando de hello fue correcto, debería ver algo parecido a siguientes de hello, dependiendo de los argumentos precisa de Hola y opciones que se usó:</span><span class="sxs-lookup"><span data-stu-id="ce06c-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="ce06c-145">Crear una máquina virtual puede tardar unos minutos, pero una vez se ha proporcionado (es el valor de estado de hello `ReadyRole`) Hola inicia de Docker daemon (Hola servicio Docker) y se puede conectar el host de contenedor de Docker toohello.</span><span class="sxs-lookup"><span data-stu-id="ce06c-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="ce06c-146">Hola tootest VM de Docker han creado en Azure, tipo</span><span class="sxs-lookup"><span data-stu-id="ce06c-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="ce06c-147">donde  *&lt;vm-nombre--usó&gt;*  es Hola nombre de máquina virtual de Hola que utilizó en la llamada demasiado`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="ce06c-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="ce06c-148">Debería ver algo similar toohello siguientes, que indica que la máquina virtual de Host de Docker está activo y en ejecución en Azure y esperando los comandos.</span><span class="sxs-lookup"><span data-stu-id="ce06c-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="ce06c-149">Ahora puede probar tooconnect utilizando la información de su tooobtain de cliente de docker (en algunas configuraciones de cliente de Docker, tales como los de Mac, tal vez necesite toouse `sudo`):</span><span class="sxs-lookup"><span data-stu-id="ce06c-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="ce06c-150">Simplemente toobe seguro de que es todo en marcha, puede examinar hello VM para hello extensión Docker:</span><span class="sxs-lookup"><span data-stu-id="ce06c-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="ce06c-151">Autenticación de máquina virtual de host de Docker</span><span class="sxs-lookup"><span data-stu-id="ce06c-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="ce06c-152">Además Hola Hola toocreating VM de Docker, `azure vm docker create` comando crea también automáticamente Hola certificados necesarios tooallow su host de contenedor de Azure Docker cliente equipo tooconnect toohello que mediante HTTPS, y Hola certificados se almacenan en ambos Hola máquinas cliente y el host, según corresponda.</span><span class="sxs-lookup"><span data-stu-id="ce06c-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="ce06c-153">En los intentos posteriores, se reutiliza certificados existentes de Hola y se comparten con nuevo host de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce06c-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="ce06c-154">De forma predeterminada, los certificados se colocan en `~/.docker`, y Docker será toorun configurado en el puerto **2376**.</span><span class="sxs-lookup"><span data-stu-id="ce06c-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="ce06c-155">Si le gustaría toouse otro puerto o directorio, puede utilizar uno de los siguientes hello `azure vm docker create` opciones de línea de comandos tooconfigure los toouse un puerto diferente de la máquina virtual de host del contenedor Docker o certificados diferentes para conectar los clientes:</span><span class="sxs-lookup"><span data-stu-id="ce06c-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="ce06c-156">es toolisten configurado para Hello demonio de Docker en el host de Hola y autenticar las conexiones en hello especifican puerto mediante Hola certificados generados por Hola de cliente `azure vm docker create` comando.</span><span class="sxs-lookup"><span data-stu-id="ce06c-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="ce06c-157">equipo de cliente Hello debe tener estos host certificados toogain acceso toohello Docker.</span><span class="sxs-lookup"><span data-stu-id="ce06c-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="ce06c-158">Un host en red que se ejecuta sin estos certificados será vulnerable tooanyone que puede tooconnect toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="ce06c-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="ce06c-159">Antes de modificar la configuración predeterminada de hello, asegúrese de que comprende Hola riesgos tooyour equipos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ce06c-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ce06c-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce06c-160">Next steps</span></span>
* <span data-ttu-id="ce06c-161">Está listo toogo toohello [Guía de usuario de Docker] y usar la máquina virtual Docker.</span><span class="sxs-lookup"><span data-stu-id="ce06c-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="ce06c-162">toocreate una máquina virtual basadas en Docker en el nuevo portal de hello, consulte [cómo toouse Hola extensión de máquina virtual de Docker con hello Portal].</span><span class="sxs-lookup"><span data-stu-id="ce06c-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="ce06c-163">Hola extensión de máquina virtual de Azure Docker también es compatible con Docker Compose, que utiliza un tootake de archivo YAML declarativa una aplicación de modelado de desarrollador en cualquier entorno y generar una implementación coherente.</span><span class="sxs-lookup"><span data-stu-id="ce06c-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="ce06c-164">Vea [empezar a trabajar con Docker y toodefine de crear y ejecutar una aplicación de contenedor múltiples en una máquina virtual de Azure].</span><span class="sxs-lookup"><span data-stu-id="ce06c-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[cómo toouse Hola extensión de máquina virtual de Docker con hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Guía de usuario de Docker]:https://docs.docker.com/userguide/

[empezar a trabajar con Docker y toodefine de crear y ejecutar una aplicación de contenedor múltiples en una máquina virtual de Azure]:../docker-compose-quickstart.md
