---
title: "Extensión de máquina virtual de Docker para Linux aaaUsing | Documentos de Microsoft"
description: "Describe Docker y las extensiones de máquinas virtuales de Azure de Hola y cómo toocreate máquinas virtuales de Azure que son hosts de docker mediante Hola CLI de Azure en el modelo de implementación clásica."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="fc714-103">Uso de hello extensión de máquina virtual de Docker con hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="fc714-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="fc714-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fc714-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc714-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="fc714-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fc714-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc714-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="fc714-107">[Docker](https://www.docker.com/) es uno de hello más populares enfoques de virtualización que utiliza [contenedores Linux](http://en.wikipedia.org/wiki/LXC) en lugar de máquinas virtuales como una manera de aislar los datos y calcular en recursos compartidos.</span><span class="sxs-lookup"><span data-stu-id="fc714-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="fc714-108">Puede utilizar la extensión de máquina virtual Docker Hola administrado por [agente Linux de Azure] toocreate una máquina virtual de Docker que hospeda cualquier número de contenedores para las aplicaciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="fc714-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="fc714-109">Este tema describe cómo toocreate una máquina virtual Docker desde Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="fc714-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="fc714-110">toosee toocreate una VM de Docker en línea de comandos de hello, vea [cómo toouse Hola extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)].</span><span class="sxs-lookup"><span data-stu-id="fc714-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="fc714-111">toosee un análisis de alto nivel de los contenedores y sus ventajas, vea hello [Docker alto nivel Pizarra](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="fc714-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="fc714-112">Crear una nueva máquina virtual de hello Galería de imágenes</span><span class="sxs-lookup"><span data-stu-id="fc714-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="fc714-113">Hola primer paso requiere una máquina virtual de Azure desde una imagen de Linux que admite Hola extensión de máquina virtual de Docker, mediante una imagen de Ubuntu 14.04 LTS de hello Galería de imágenes como una imagen de servidor de ejemplo y Ubuntu 14.04 escritorio como un cliente.</span><span class="sxs-lookup"><span data-stu-id="fc714-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="fc714-114">En el portal de hello, haga clic en **+ nuevo** Hola inferior izquierda esquina toocreate una nueva instancia de máquina virtual y seleccione una imagen de Ubuntu 14.04 LTS de selecciones de hello disponibles o de hello completa Galería de imágenes, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fc714-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="fc714-115">Actualmente, sólo Ubuntu 14.04 LTS las imágenes más recientes de julio de 2014 admiten Hola extensión de máquina virtual de Docker.</span><span class="sxs-lookup"><span data-stu-id="fc714-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Creación de una imagen Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="fc714-117">Creación de certificados de Docker</span><span class="sxs-lookup"><span data-stu-id="fc714-117">Create Docker Certificates</span></span>
<span data-ttu-id="fc714-118">Después de Hola se ha creado la máquina virtual, asegúrese de que Docker está instalado en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="fc714-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="fc714-119">(Para obtener detalles, consulte [Instrucciones de instalación de Docker](https://docs.docker.com/installation/#installation)).</span><span class="sxs-lookup"><span data-stu-id="fc714-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="fc714-120">Crear archivos de certificado y la clave para la comunicación de Docker según demasiado de hello[ejecutar Docker con https] y colocarlas en hello  **`~/.docker`**  directorio en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="fc714-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="fc714-121">Hola extensión de máquina virtual de Docker en el portal de hello actualmente requiere credenciales que están codificados con base64.</span><span class="sxs-lookup"><span data-stu-id="fc714-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="fc714-122">En la línea de comandos de hello, use  **`base64`**  o favorito otra codificación temas de herramienta toocreate con codificación base64.</span><span class="sxs-lookup"><span data-stu-id="fc714-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="fc714-123">Si hace esto con un sencillo conjunto de archivos de certificado y la clave podría ser toothis similar:</span><span class="sxs-lookup"><span data-stu-id="fc714-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="fc714-124">Agregar extensión de máquina virtual Docker Hola</span><span class="sxs-lookup"><span data-stu-id="fc714-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="fc714-125">tooadd Hola extensión de máquina virtual de Docker, busque la instancia VM de Hola que ha creado y desplácese hacia abajo demasiado**extensiones** y haga clic en él toobring las extensiones de máquina virtual, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fc714-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="fc714-126">Esta funcionalidad se admite en el portal de vista previa de hello solo: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="fc714-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="fc714-127">Adición de una extensión</span><span class="sxs-lookup"><span data-stu-id="fc714-127">Add an Extension</span></span>
<span data-ttu-id="fc714-128">Haga clic en hello **+ agregar** toodisplay Hola posibles extensiones de VM, puede agregar toothis máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fc714-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="fc714-129">Seleccione Hola extensión de máquina virtual Docker</span><span class="sxs-lookup"><span data-stu-id="fc714-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="fc714-130">Elija Hola extensión de máquina virtual de Docker, que ofrece una descripción de Docker de Hola y vínculos importantes, y, a continuación, haga clic en **crear** en el procedimiento de instalación de hello inferior toobegin Hola.</span><span class="sxs-lookup"><span data-stu-id="fc714-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="fc714-131">Adición de los archivos de certificado y clave:</span><span class="sxs-lookup"><span data-stu-id="fc714-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="fc714-132">Hola campos de formulario, escriba las versiones con codificación base64 de Hola de su certificado de CA, el certificado de servidor y la clave del servidor, tal y como se muestra en el siguiente gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc714-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="fc714-133">Tenga en cuenta que (como en Hola anterior imagen) Hola 2376 se rellena de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fc714-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="fc714-134">Puede escribir cualquier extremo aquí, pero Hola siguiente paso será tooopen seguridad Hola coincidencia de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="fc714-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="fc714-135">Si cambia de forma predeterminada hello, asegúrese de tooopen seguro seguridad Hola que coincidan con el extremo en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="fc714-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="fc714-136">Agregar Hola extremo de comunicación de Docker</span><span class="sxs-lookup"><span data-stu-id="fc714-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="fc714-137">Al ver el grupo de recursos de Hola que haya creado, seleccione Hola grupo de seguridad de red asociado a la máquina virtual y haga clic en **reglas de seguridad de entrada** tooview Hola reglas como se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="fc714-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="fc714-138">Haga clic en **+ agregar** tooadd otra regla y en caso de hello predeterminado, escriba un nombre para el extremo de hello (en este ejemplo, **Docker**) y 2376 'intervalo de puertos del destino'.</span><span class="sxs-lookup"><span data-stu-id="fc714-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="fc714-139">Establecer mostrando de valor de protocolo de hello **TCP**y haga clic en **Aceptar** regla de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="fc714-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="fc714-140">Comprobación del cliente de Docker y del host de Docker de Azure</span><span class="sxs-lookup"><span data-stu-id="fc714-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="fc714-141">Busque y copie Hola nombre de dominio de la máquina virtual y en línea de comandos de hello del equipo cliente, tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (donde *dockerextension* se sustituye por hello subdominio para la máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="fc714-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="fc714-142">resultado de Hello debe aparecer toothis similar:</span><span class="sxs-lookup"><span data-stu-id="fc714-142">hello result should appear similar toothis:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="fc714-143">Cuando se haya completado Hola por encima de los pasos, ahora tiene un host Docker totalmente funcional que se ejecuta en una máquina virtual de Azure, configurado toobe conectado tooremotely desde otros clientes.</span><span class="sxs-lookup"><span data-stu-id="fc714-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="fc714-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc714-144">Next steps</span></span>
<span data-ttu-id="fc714-145">Está listo toogo toohello [Guía de usuario de Docker] y usar la máquina virtual Docker.</span><span class="sxs-lookup"><span data-stu-id="fc714-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="fc714-146">Si desea tooautomate creación de hosts de Docker en máquinas virtuales de Azure a través de la interfaz de línea de comandos, vea [cómo toouse Hola extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)]</span><span class="sxs-lookup"><span data-stu-id="fc714-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[cómo toouse Hola extensión de máquina virtual Docker de hello Azure interfaz de línea de comandos (CLI de Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agente Linux de Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[ejecutar Docker con https]:http://docs.docker.com/articles/https/
[Guía de usuario de Docker]:https://docs.docker.com/userguide/
