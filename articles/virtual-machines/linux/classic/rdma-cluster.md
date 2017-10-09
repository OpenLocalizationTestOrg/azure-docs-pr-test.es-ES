---
title: "aaaSet un aplicaciones de MPI de Linux RDMA clúster toorun | Documentos de Microsoft"
description: "Crear un clúster de Linux de tamaño H16r, H16mr, A8 o A9 VM toouse aplicaciones de MPI de hello RDMA de Azure red toorun"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="fdb29-103">Configurar una aplicación de MPI Linux RDMA toorun de clúster</span><span class="sxs-lookup"><span data-stu-id="fdb29-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="fdb29-104">Obtenga información acerca de cómo agrupar tooset seguridad un Linux RDMA en Azure con [tamaños de máquinas virtuales de proceso de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun aplicaciones de interfaz de paso de mensajes (MPI) paralelas.</span><span class="sxs-lookup"><span data-stu-id="fdb29-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="fdb29-105">Este artículo proporciona pasos tooprepare un toorun de imagen de Linux HPC MPI de Intel en un clúster.</span><span class="sxs-lookup"><span data-stu-id="fdb29-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="fdb29-106">Después de preparar, implementar un clúster de máquinas virtuales usando esta imagen y uno de los tamaños de máquina virtual de Azure compatibles con RDMA hello (actualmente H16r, H16mr, A8 o A9).</span><span class="sxs-lookup"><span data-stu-id="fdb29-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="fdb29-107">Utilice hello toorun MPI las aplicaciones de clúster que se comunican de manera eficiente a través de una red de baja latencia y alto rendimiento basada en la tecnología de memoria directa remota (RDMA) de acceso.</span><span class="sxs-lookup"><span data-stu-id="fdb29-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdb29-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico.</span><span class="sxs-lookup"><span data-stu-id="fdb29-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="fdb29-109">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="fdb29-110">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="fdb29-111">Opciones de implementación de clúster</span><span class="sxs-lookup"><span data-stu-id="fdb29-111">Cluster deployment options</span></span>
<span data-ttu-id="fdb29-112">Siguientes son métodos que puede usar un clúster de Linux RDMA toocreate con o sin un programador de trabajos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="fdb29-113">**Las secuencias de comandos CLI Azure**: como se muestra más adelante en este artículo, use hello [interfaz de línea de comandos de Azure](../../../cli-install-nodejs.md) implementación de Hola de tooscript (CLI) de un clúster de máquinas virtuales compatibles con RDMA.</span><span class="sxs-lookup"><span data-stu-id="fdb29-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="fdb29-114">Hola CLI en el modo de administración de servicios crea Hola nodos de clúster en serie en el modelo de implementación clásica de hello, por lo que implementar muchos nodos de proceso puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="fdb29-115">Hola tooenable conexión de red RDMA cuando se usa el modelo de implementación clásica de hello, implementar máquinas virtuales de Hola Hola mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fdb29-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="fdb29-116">**Plantillas de administrador de recursos de Azure**: también puede utilizar toodeploy de modelo de implementación un clúster de máquinas virtuales compatibles con RDMA que conecta la red RDMA de toohello de hello Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="fdb29-117">También puede [crear su propia plantilla](../../../resource-group-authoring-templates.md), o consulte hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) para plantillas aportadas por Microsoft o hello Comunidad toodeploy Hola solución deseada.</span><span class="sxs-lookup"><span data-stu-id="fdb29-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="fdb29-118">Plantillas de administrador de recursos pueden proporcionar un toodeploy de manera rápida y confiable de un clúster de Linux.</span><span class="sxs-lookup"><span data-stu-id="fdb29-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="fdb29-119">Hola tooenable conexión de red RDMA cuando se usa el modelo de implementación del Administrador de recursos de hello, implementar máquinas virtuales de Hola Hola mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="fdb29-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="fdb29-120">**HPC Pack**: crear un clúster de Microsoft HPC Pack en Azure y agregar nodos de cálculo compatibles con RDMA que se ejecutan en una red RDMA de Linux distribución tooaccess Hola admitida.</span><span class="sxs-lookup"><span data-stu-id="fdb29-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="fdb29-121">Para más información, consulte [Introducción a los nodos de ejecución de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="fdb29-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="fdb29-122">Los pasos de implementación de ejemplo de modelo clásico Hola</span><span class="sxs-lookup"><span data-stu-id="fdb29-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="fdb29-123">Hello pasos siguientes muestran cómo personalizarlo toouse hello Azure CLI toodeploy una máquina virtual de HPC de SUSE Linux Enterprise Server (SLES) 12 SP1 de hello Azure Marketplace y crear una imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="fdb29-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="fdb29-124">A continuación, puede usar la implementación de hello tooscript Hola una imagen de un clúster de máquinas virtuales compatibles con RDMA.</span><span class="sxs-lookup"><span data-stu-id="fdb29-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="fdb29-125">Usar un clúster de máquinas virtuales compatibles con RDMA basado en imágenes de CentOS-based HPC en Azure Marketplace Hola similar toodeploy de pasos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="fdb29-126">Es posible que, como se indica, algunos pasos sean ligeramente distintos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="fdb29-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fdb29-127">Prerequisites</span></span>
* <span data-ttu-id="fdb29-128">**Equipo cliente**: se necesita un toocommunicate de equipo de cliente de Windows, Linux o Mac con Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb29-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="fdb29-129">Estos pasos se supone que está usado un cliente Linux.</span><span class="sxs-lookup"><span data-stu-id="fdb29-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="fdb29-130">**Suscripción de Azure**: si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="fdb29-131">En los clústeres más grandes, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra.</span><span class="sxs-lookup"><span data-stu-id="fdb29-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="fdb29-132">**Disponibilidad de tamaño VM**: Hola siguientes tamaños de instancias es compatibles con RDMA: H16r, H16mr, A8 y A9.</span><span class="sxs-lookup"><span data-stu-id="fdb29-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="fdb29-133">Para ver la disponibilidad en las regiones de Azure, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/) .</span><span class="sxs-lookup"><span data-stu-id="fdb29-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="fdb29-134">**Cuota de núcleos**: es posible que tenga cuota de hello tooincrease de núcleos toodeploy un clúster de máquinas virtuales de proceso intensivo.</span><span class="sxs-lookup"><span data-stu-id="fdb29-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="fdb29-135">Por ejemplo, necesita al menos 128 núcleos si desea toodeploy 8 A9 VM como se muestra en este artículo.</span><span class="sxs-lookup"><span data-stu-id="fdb29-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="fdb29-136">La suscripción también puede limitar el número de Hola de núcleos que se puede implementar en ciertas familias de tamaño de máquina virtual, incluyendo Hola H-series.</span><span class="sxs-lookup"><span data-stu-id="fdb29-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="fdb29-137">aumentar una cuota de toorequest, [abrir una solicitud de soporte al cliente en línea](../../../azure-supportability/how-to-create-azure-support-request.md) sin cargo.</span><span class="sxs-lookup"><span data-stu-id="fdb29-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="fdb29-138">**CLI de Azure**: [instalar](../../../cli-install-nodejs.md) Hola CLI de Azure y [conectar tooyour suscripción de Azure](../../../xplat-cli-connect.md) desde el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="fdb29-139">Aprovisionamiento de una máquina virtual de HPC de SLES 12 SP1</span><span class="sxs-lookup"><span data-stu-id="fdb29-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="fdb29-140">Después de iniciar sesión en tooAzure con hello CLI de Azure, ejecute `azure config list` tooconfirm que Hola salida muestra el modo de administración de servicios.</span><span class="sxs-lookup"><span data-stu-id="fdb29-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="fdb29-141">Si no es así, establecer el modo de hello, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="fdb29-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="fdb29-142">Escriba Hola después a toolist todas las suscripciones de hello son toouse autorizado:</span><span class="sxs-lookup"><span data-stu-id="fdb29-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="fdb29-143">suscripción activa de Hello actual se identifica con `Current` establecido demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="fdb29-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="fdb29-144">Si esta suscripción no Hola uno que desea toouse toocreate Hola clúster, establecer Id. de suscripción adecuado de hello como suscripción activa de hello:</span><span class="sxs-lookup"><span data-stu-id="fdb29-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="fdb29-145">toosee Hola disponibles públicamente imágenes SLES 12 SP1 HPC en Azure, ejecute un comando como Hola sigue, suponiendo que el entorno de shell es compatible con **grep**:</span><span class="sxs-lookup"><span data-stu-id="fdb29-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="fdb29-146">El aprovisionamiento de una máquina virtual compatible con RDMA con una imagen de HPC de SLES 12 SP1 mediante la ejecución de un comando como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="fdb29-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="fdb29-147">Donde:</span><span class="sxs-lookup"><span data-stu-id="fdb29-147">Where:</span></span>

* <span data-ttu-id="fdb29-148">Hola tamaño (A9 en este ejemplo) es uno de los tamaños de máquinas virtuales de hello compatibles con RDMA.</span><span class="sxs-lookup"><span data-stu-id="fdb29-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="fdb29-149">número de puerto SSH Hola externo (22 en este ejemplo, que es hello predeterminada SSH) es cualquier número de puerto válido.</span><span class="sxs-lookup"><span data-stu-id="fdb29-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="fdb29-150">número de puerto SSH interno Hola se establece too22.</span><span class="sxs-lookup"><span data-stu-id="fdb29-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="fdb29-151">Un nuevo servicio de nube se crea en Hola especificada por la ubicación de Hola de región de Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb29-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="fdb29-152">Especifique una ubicación en qué Hola VM tamaño elegido está disponible.</span><span class="sxs-lookup"><span data-stu-id="fdb29-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="fdb29-153">Para obtener soporte de prioridad SUSE (que incurre en cargos adicionales), nombre de la imagen de hello SLES 12 SP1 actualmente puede ser una de estas dos opciones:</span><span class="sxs-lookup"><span data-stu-id="fdb29-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="fdb29-154">Personalizar Hola VM</span><span class="sxs-lookup"><span data-stu-id="fdb29-154">Customize hello VM</span></span>
<span data-ttu-id="fdb29-155">Al finalizar Hola VM aprovisionamiento, SSH toohello VM mediante el uso de Hola dirección IP externa de la máquina virtual (o nombre DNS) y Hola número de puerto externo configurado y, a continuación, personalizarlo.</span><span class="sxs-lookup"><span data-stu-id="fdb29-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="fdb29-156">Para obtener detalles de conexión, consulte [cómo toolog en la máquina virtual de tooa ejecutan Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fdb29-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="fdb29-157">Ejecute comandos como usuario de hello configurado en Hola de máquina virtual, a menos que el acceso a la raíz es toocomplete requiere un paso.</span><span class="sxs-lookup"><span data-stu-id="fdb29-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdb29-158">Microsoft Azure no proporciona acceso a la raíz tooLinux las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fdb29-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="fdb29-159">acceso administrativo de toogain cuando se conecta como un toohello de usuario de máquina virtual, ejecute los comandos mediante el uso de `sudo`.</span><span class="sxs-lookup"><span data-stu-id="fdb29-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="fdb29-160">**Actualizaciones**: instale las actualizaciones mediante zypper.</span><span class="sxs-lookup"><span data-stu-id="fdb29-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="fdb29-161">Puede que le interese tooinstall utilidades NFS.</span><span class="sxs-lookup"><span data-stu-id="fdb29-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="fdb29-162">En una VM de HPC SLES 12 SP1, se recomienda no aplicar actualizaciones de kernel, lo que pueden causar problemas con hello Linux RDMA controladores.</span><span class="sxs-lookup"><span data-stu-id="fdb29-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="fdb29-163">**Intel MPI**: completar la instalación de Hola de MPI de Intel en hello SLES 12 SP1 HPC VM ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fdb29-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="fdb29-164">**Bloquear la memoria**: para MPI códigos toolock Hola memoria disponible para RDMA, agregar o cambiar los Hola después de la configuración en el archivo de hello /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="fdb29-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="fdb29-165">Necesita tooedit de acceso raíz de este archivo.</span><span class="sxs-lookup"><span data-stu-id="fdb29-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="fdb29-166">Para realizar pruebas, también puede establecer memlock toounlimited.</span><span class="sxs-lookup"><span data-stu-id="fdb29-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="fdb29-167">Por ejemplo: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="fdb29-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="fdb29-168">Para más información, consulte los [métodos más conocidos para definir el tamaño de memoria bloqueada](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="fdb29-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="fdb29-169">**Claves SSH para máquinas virtuales de SLES**: generar SSH claves tooestablish relación de confianza para su cuenta de usuario entre Hola nodos de ejecución Hola SLES clúster cuando se ejecutan trabajos MPI.</span><span class="sxs-lookup"><span data-stu-id="fdb29-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="fdb29-170">Si implementó una máquina virtual de HPC basada en CentOS, no siga este paso.</span><span class="sxs-lookup"><span data-stu-id="fdb29-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="fdb29-171">Consulte las instrucciones más adelante en este tooset artículo passwordless confianza SSH entre los nodos del clúster Hola después de capturar imagen de hello e implementar clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="fdb29-172">claves de SSH toocreate, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="fdb29-173">Cuando se le pida para la entrada, seleccione **ENTRAR** toogenerate claves de hello en ubicación predeterminada de hello sin establecer una contraseña.</span><span class="sxs-lookup"><span data-stu-id="fdb29-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="fdb29-174">Anexar el archivo de authorized_keys toohello de clave pública de Hola para las claves públicas conocidas.</span><span class="sxs-lookup"><span data-stu-id="fdb29-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="fdb29-175">En el directorio de ~/.ssh hello, editar o crear el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="fdb29-176">Proporcionar el intervalo de direcciones IP de Hola de red privada de Hola que planea toouse en Azure (10.32.0.0/16 en este ejemplo):</span><span class="sxs-lookup"><span data-stu-id="fdb29-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="fdb29-177">Como alternativa, lista dirección IP de red privada de Hola de cada máquina virtual en el clúster como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="fdb29-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="fdb29-178">Configurar `StrictHostKeyChecking no` puede crear un posible riesgo de seguridad cuando no se especifica una dirección IP o un intervalo concretos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="fdb29-179">**Aplicaciones**: instalar ninguna aplicación necesita o realizar otras personalizaciones antes de capturar imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="fdb29-180">Capturar imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="fdb29-180">Capture hello image</span></span>
<span data-ttu-id="fdb29-181">imagen de hello toocapture, primero ejecute hello siguiente comando en hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="fdb29-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="fdb29-182">Este comando desactiva Hola VM pero mantiene las cuentas de usuario y las claves SSH que configuró.</span><span class="sxs-lookup"><span data-stu-id="fdb29-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="fdb29-183">Desde el equipo cliente, ejecute hello después de la imagen de Hola de toocapture de comandos de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="fdb29-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="fdb29-184">Para obtener más información, consulte [cómo toocapture una máquina virtual de Linux clásica como imagen](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="fdb29-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="fdb29-185">Después de ejecutar estos comandos, se captura la imagen de máquina virtual de Hola para su uso y Hola máquina virtual se elimina.</span><span class="sxs-lookup"><span data-stu-id="fdb29-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="fdb29-186">Ahora tiene la toodeploy listo de imagen personalizada un clúster.</span><span class="sxs-lookup"><span data-stu-id="fdb29-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="fdb29-187">Implementar un clúster con la imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="fdb29-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="fdb29-188">Modifica Hola siguiente secuencia de comandos de Bash con los valores adecuados para su entorno y lo ejecuta desde el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="fdb29-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="fdb29-189">Dado que Azure implementa máquinas virtuales de hello en serie en el modelo de implementación clásica de hello, tarda unos minutos toodeploy Hola ocho máquinas virtuales de A9 sugeridas en esta secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="fdb29-190">Consideraciones para un clúster de HPC de CentOS</span><span class="sxs-lookup"><span data-stu-id="fdb29-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="fdb29-191">Si desea tooset un clúster basado en una de las imágenes HPC basado en CentOS de hello en hello Azure Marketplace en lugar de SLES 12 para HPC, siga los pasos generales Hola Hola sección anterior.</span><span class="sxs-lookup"><span data-stu-id="fdb29-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="fdb29-192">Tenga en cuenta hello las siguientes diferencias cuando se aprovisiona y configura Hola VM:</span><span class="sxs-lookup"><span data-stu-id="fdb29-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="fdb29-193">Intel MPI ya está instalado en una máquina virtual aprovisionada desde una imagen de HPC basada en CentOS.</span><span class="sxs-lookup"><span data-stu-id="fdb29-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="fdb29-194">Configuración de la memoria de bloqueo ya se han agregado en archivo de la máquina virtual de hello /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="fdb29-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="fdb29-195">No se generan claves SSH en hello VM aprovisione para la captura.</span><span class="sxs-lookup"><span data-stu-id="fdb29-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="fdb29-196">En su lugar, se recomienda configurar la autenticación basada en usuario después de implementar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="fdb29-197">Para obtener más información, vea Hola pasos de la sección.</span><span class="sxs-lookup"><span data-stu-id="fdb29-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="fdb29-198">Establecer una confianza SSH passwordless en clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="fdb29-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="fdb29-199">En un clúster HPC basado en CentOS, existen dos métodos para establecer la confianza entre los nodos de proceso de hello: autenticación basada en host y la autenticación basada en usuario.</span><span class="sxs-lookup"><span data-stu-id="fdb29-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="fdb29-200">Autenticación basada en host está fuera del ámbito de Hola de este artículo y generalmente debe realizarse a través de una secuencia de comandos de extensión durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="fdb29-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="fdb29-201">Autenticación basada en usuario resulta útil para establecer la confianza después de la implementación y requiere la generación de Hola y uso compartido de las claves SSH entre Hola nodos de ejecución Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="fdb29-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="fdb29-202">Este método se suele conocer como inicio de sesión SSH sin contraseña y es necesario al ejecutar trabajos de MPI.</span><span class="sxs-lookup"><span data-stu-id="fdb29-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="fdb29-203">Está disponible en una secuencia de comandos de ejemplo que proceden de la Comunidad de hello [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable autenticación de usuario sencilla en un clúster HPC basado en CentOS.</span><span class="sxs-lookup"><span data-stu-id="fdb29-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="fdb29-204">Descargue y use este script mediante el uso de hello pasos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="fdb29-205">También puede modificar esta secuencia de comandos o usar cualquier otro método tooestablish passwordless autenticación de SSH entre nodos de proceso del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="fdb29-206">script de Hola toorun, se necesita un prefijo de hello tooknow para las direcciones IP de subred.</span><span class="sxs-lookup"><span data-stu-id="fdb29-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="fdb29-207">Obtiene el prefijo de hello ejecutando Hola siguiente comando en uno de los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="fdb29-208">El resultado debe ser similar a 10.1.3.5 y prefijo de hello es parte de hello 10.1.3.</span><span class="sxs-lookup"><span data-stu-id="fdb29-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="fdb29-209">Ahora ejecutar script de Hola con tres parámetros: nombre de usuario común de hello en hello nodos de proceso, contraseña común de Hola para ese usuario en hello nodos de proceso y del prefijo de subred de Hola que se devolvió desde el comando anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="fdb29-210">Este script Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fdb29-210">This script does hello following:</span></span>

* <span data-ttu-id="fdb29-211">Crea un directorio en el nodo de host de hello denominado .ssh, que es necesario para el inicio de sesión passwordless.</span><span class="sxs-lookup"><span data-stu-id="fdb29-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="fdb29-212">Crea un archivo de configuración en el directorio de .ssh Hola que indica el inicio de sesión de inicio de sesión passwordless tooallow desde cualquier nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="fdb29-213">Crea archivos que contienen nombres de nodo de Hola y direcciones IP del nodo para todos los nodos Hola Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="fdb29-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="fdb29-214">Estos archivos se mantienen después de ejecutar script de Hola para consultarlos más adelante.</span><span class="sxs-lookup"><span data-stu-id="fdb29-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="fdb29-215">Crea un par de claves público y privado para cada nodo del clúster (incluido el nodo de host de hello) y crea entradas en el archivo de hello authorized_keys.</span><span class="sxs-lookup"><span data-stu-id="fdb29-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="fdb29-216">La ejecución de este script puede crear un posible riesgo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fdb29-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="fdb29-217">Asegúrese de que no se distribuye información de clave pública de hello en ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="fdb29-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="fdb29-218">Configuración de Intel MPI</span><span class="sxs-lookup"><span data-stu-id="fdb29-218">Configure Intel MPI</span></span>
<span data-ttu-id="fdb29-219">aplicaciones de MPI toorun en RDMA de Linux de Azure, necesita tooconfigure determinada variables de entorno específicas tooIntel MPI.</span><span class="sxs-lookup"><span data-stu-id="fdb29-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="fdb29-220">Aquí es un toorun ejemplo Bash script tooconfigure hello las variables que se necesita una aplicación.</span><span class="sxs-lookup"><span data-stu-id="fdb29-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="fdb29-221">Cambiar toompivars.sh de ruta de acceso de hello según sea necesario para la instalación de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="fdb29-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="fdb29-222">Hola formato de archivo de host de hello es el siguiente.</span><span class="sxs-lookup"><span data-stu-id="fdb29-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="fdb29-223">Agregue una línea para cada nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="fdb29-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="fdb29-224">Especifique las direcciones IP privadas de la red virtual de hello definen anteriormente, no los nombres DNS.</span><span class="sxs-lookup"><span data-stu-id="fdb29-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="fdb29-225">Por ejemplo, para los dos hosts con direcciones IP 10.32.0.1 y 10.32.0.2, archivo hello contiene siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="fdb29-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="fdb29-226">Ejecución de MPI en un clúster de dos nodos básico</span><span class="sxs-lookup"><span data-stu-id="fdb29-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="fdb29-227">Si aún no lo ha hecho, en primer lugar configurar Hola entorno para Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="fdb29-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="fdb29-228">Ejecución de un comando de MPI</span><span class="sxs-lookup"><span data-stu-id="fdb29-228">Run an MPI command</span></span>
<span data-ttu-id="fdb29-229">Ejecutar un comando MPI en uno de tooshow de nodos de proceso de Hola que MPI esté instalado correctamente y se puede comunicar entre al menos dos nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="fdb29-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="fdb29-230">siguiente Hello **mpirun** comando ejecuta hello **hostname** comando dos nodos.</span><span class="sxs-lookup"><span data-stu-id="fdb29-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="fdb29-231">La salida debe enumerar nombres Hola de todos los nodos de Hola que pasan como entrada para `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="fdb29-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="fdb29-232">Por ejemplo, un **mpirun** comando con dos nodos devuelve resultados similares a Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fdb29-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="fdb29-233">Ejecución de una prueba comparativa de MPI</span><span class="sxs-lookup"><span data-stu-id="fdb29-233">Run an MPI benchmark</span></span>
<span data-ttu-id="fdb29-234">Hola siguiente comando de MPI Intel ejecuta una pingpong prueba comparativa tooverify Hola configuración y conexión toohello RDMA red del clúster.</span><span class="sxs-lookup"><span data-stu-id="fdb29-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="fdb29-235">En un clúster de trabajar con dos nodos, obtendrá unos resultados similares a los siguientes Hola.</span><span class="sxs-lookup"><span data-stu-id="fdb29-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="fdb29-236">En la red RDMA de Azure de hello, espera latencia en o por debajo de 3 microsegundos para tamaños de mensaje seguridad too512 bytes.</span><span class="sxs-lookup"><span data-stu-id="fdb29-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="fdb29-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fdb29-237">Next steps</span></span>
* <span data-ttu-id="fdb29-238">Implemente y ejecute las aplicaciones Linux MPI en el clúster de Linux.</span><span class="sxs-lookup"><span data-stu-id="fdb29-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="fdb29-239">Vea hello [documentación de la biblioteca de MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) para obtener instrucciones sobre MPI de Intel.</span><span class="sxs-lookup"><span data-stu-id="fdb29-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="fdb29-240">Intente una [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate un Lustre Intel de clúster mediante una imagen basada en CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="fdb29-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="fdb29-241">Para más información, consulte [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/) (Implementación de la edición de nube de Intel para Lustre en Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="fdb29-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
