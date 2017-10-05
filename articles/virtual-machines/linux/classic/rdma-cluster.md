---
title: "Configuración de un clúster de Linux RDMA para ejecutar aplicaciones MPI | Microsoft Docs"
description: "Cree un clúster de Linux con máquinas virtuales de tamaño H16r, H16mr, A8 o A9 para usar la red de RDMA de Azure para ejecutar aplicaciones de MPI."
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
ms.openlocfilehash: 4b2ceb64b1737918458f6d5c692fc2bfbc0f12ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-a-linux-rdma-cluster-to-run-mpi-applications"></a><span data-ttu-id="ca0ee-103">Configuración de un clúster de Linux RDMA para ejecutar aplicaciones MPI</span><span class="sxs-lookup"><span data-stu-id="ca0ee-103">Set up a Linux RDMA cluster to run MPI applications</span></span>
<span data-ttu-id="ca0ee-104">Aprenda a configurar un clúster de Linux RDMA en Azure con [tamaños de máquina virtual de procesos de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para ejecutar aplicaciones de interfaz de paso de mensajes (MPI) paralelas.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-104">Learn how to set up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to run parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="ca0ee-105">En este artículo se incluyen los pasos necesarios para preparar una imagen de HPC de Linux para ejecutar Intel MPI en un clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-105">This article provides steps to prepare a Linux HPC image to run Intel MPI on a cluster.</span></span> <span data-ttu-id="ca0ee-106">Después de la preparación, se implementa un clúster de máquinas virtuales con esta imagen y uno de los tamaños de máquinas virtuales de Azure compatibles con RDMA (actualmente H16r, H16mr, A8 o A9).</span><span class="sxs-lookup"><span data-stu-id="ca0ee-106">After preparation, you deploy a cluster of VMs using this image and one of the RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="ca0ee-107">Use el clúster para ejecutar aplicaciones MPI que se comunican eficazmente a través de una red de latencia baja y alto rendimiento con tecnología de acceso directo a memoria remota (RDMA).</span><span class="sxs-lookup"><span data-stu-id="ca0ee-107">Use the cluster to run MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca0ee-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="ca0ee-109">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="ca0ee-110">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="ca0ee-111">Opciones de implementación de clúster</span><span class="sxs-lookup"><span data-stu-id="ca0ee-111">Cluster deployment options</span></span>
<span data-ttu-id="ca0ee-112">A continuación se facilitan métodos que puede usar para crear un clúster de Linux RDMA con o sin un programador de trabajos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-112">Following are methods you can use to create a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="ca0ee-113">**Scripts de la CLI de Azure**: como se muestra más adelante en este artículo, use la [interfaz de la línea de comandos de Azure](../../../cli-install-nodejs.md) (CLI) para automatizar la implementación de un clúster de máquinas virtuales compatibles con RDMA.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-113">**Azure CLI scripts**: As shown later in this article, use the [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) to script the deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="ca0ee-114">La CLI en modo de Administración de servicios crea los nodos del clúster en serie en el modelo de implementación clásica, por lo que la implementación de muchos nodos de proceso puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-114">The CLI in Service Management mode creates the cluster nodes serially in the classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="ca0ee-115">Para habilitar la conexión de red de RDMA cuando se usa el modelo de implementación clásica, implemente las máquinas virtuales en el mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-115">To enable the RDMA network connection when you use the classic deployment model, deploy the VMs in the same cloud service.</span></span>
* <span data-ttu-id="ca0ee-116">**Plantillas de Azure Resource Manager**: también puede usar el modelo de implementación de Resource Manager para implementar un clúster de máquinas virtuales compatibles con RDMA que se conecte a la red de RDMA.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-116">**Azure Resource Manager templates**: You can also use the Resource Manager deployment model to deploy a cluster of RDMA-capable VMs that connects to the RDMA network.</span></span> <span data-ttu-id="ca0ee-117">También puede [crear su propia plantilla](../../../resource-group-authoring-templates.md) o consultar las [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) para obtener plantillas proporcionadas por Microsoft o la comunidad para implementar la solución que desee.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or the community to deploy the solution you want.</span></span> <span data-ttu-id="ca0ee-118">Las plantillas del Administrador de recursos proporcionan una manera rápida y confiable de implementar un clúster de Linux.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-118">Resource Manager templates can provide a fast and reliable way to deploy a Linux cluster.</span></span> <span data-ttu-id="ca0ee-119">Para habilitar la conexión de red de RDMA cuando se usa el modelo de implementación de Resource Manager, implemente las máquinas virtuales en el mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-119">To enable the RDMA network connection when you use the Resource Manager deployment model, deploy the VMs in the same availability set.</span></span>
* <span data-ttu-id="ca0ee-120">**HPC Pack**: cree un clúster de Microsoft HPC Pack en Azure y agregue nodos de ejecución compatibles con RDMA que ejecuten una distribución de Linux compatible para acceder a la red de RDMA.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution to access the RDMA network.</span></span> <span data-ttu-id="ca0ee-121">Para más información, consulte [Introducción a los nodos de ejecución de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ca0ee-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-the-classic-model"></a><span data-ttu-id="ca0ee-122">Pasos de implementación de ejemplo en el modelo clásico</span><span class="sxs-lookup"><span data-stu-id="ca0ee-122">Sample deployment steps in the classic model</span></span>
<span data-ttu-id="ca0ee-123">Los pasos siguientes muestran cómo usar la CLI de Azure para implementar una máquina virtual de HPC de SUSE Linux Enterprise Server 12 SP1 (SLES) desde Azure Marketplace, personalizarla y crear una imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-123">The following steps show how to use the Azure CLI to deploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from the Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="ca0ee-124">Después puede usar la imagen para automatizar la implementación de un clúster de máquinas virtuales compatibles con RDMA.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-124">Then you can use the image to script the deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="ca0ee-125">Siga los mismos pasos para implementar un clúster de máquinas virtuales compatibles con RDMA basadas en imágenes de HPC basadas en CentOS en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-125">Use similar steps to deploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="ca0ee-126">Es posible que, como se indica, algunos pasos sean ligeramente distintos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="ca0ee-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ca0ee-127">Prerequisites</span></span>
* <span data-ttu-id="ca0ee-128">**Equipo cliente**: necesita un equipo cliente de Mac, Linux o Windows para comunicarse con Azure.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-128">**Client computer**: You need a Mac, Linux, or Windows client computer to communicate with Azure.</span></span> <span data-ttu-id="ca0ee-129">Estos pasos se supone que está usado un cliente Linux.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="ca0ee-130">**Suscripción de Azure**: si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="ca0ee-131">En los clústeres más grandes, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="ca0ee-132">**Disponibilidad de tamaño de máquina virtual**: los siguientes tamaños de instancia son compatibles con RDMA: H16r, H16mr, A8 y A9.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-132">**VM size availability**: The following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="ca0ee-133">Para ver la disponibilidad en las regiones de Azure, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/) .</span><span class="sxs-lookup"><span data-stu-id="ca0ee-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="ca0ee-134">**Cuota de núcleos**: es posible que tenga que aumentar la cuota de núcleos para implementar un clúster de máquinas virtuales de proceso intensivo.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-134">**Cores quota**: You might need to increase the quota of cores to deploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="ca0ee-135">Por ejemplo, necesita al menos 128 núcleos si desea implementar máquinas virtuales A8 o A9 tal y como se muestra en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-135">For example, you need at least 128 cores if you want to deploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="ca0ee-136">La suscripción también podría limitar el número de núcleos que se pueden implementar en ciertas familias de tamaño de máquina virtual, como la serie H.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-136">Your subscription might also limit the number of cores you can deploy in certain VM size families, including the H-series.</span></span> <span data-ttu-id="ca0ee-137">Para solicitar un aumento de cuota, [abra una solicitud de soporte técnico al cliente en línea](../../../azure-supportability/how-to-create-azure-support-request.md) sin cargo alguno.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-137">To request a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="ca0ee-138">**CLI de Azure**: [instale](../../../cli-install-nodejs.md) la CLI de Azure y [conéctela a su suscripción de Azure](../../../xplat-cli-connect.md) en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) the Azure CLI and [connect to your Azure subscription](../../../xplat-cli-connect.md) from the client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="ca0ee-139">Aprovisionamiento de una máquina virtual de HPC de SLES 12 SP1</span><span class="sxs-lookup"><span data-stu-id="ca0ee-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="ca0ee-140">Después de iniciar sesión en Azure con la CLI de Azure, ejecute `azure config list` para confirmar que la salida muestra el modo de Administración del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-140">After signing in to Azure with the Azure CLI, run `azure config list` to confirm that the output shows Service Management mode.</span></span> <span data-ttu-id="ca0ee-141">Si no es así, ejecute este comando para establecer el modo:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-141">If it does not, set the mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="ca0ee-142">Escriba lo siguiente para enumerar todas las suscripciones que está autorizado a usar:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-142">Type the following to list all the subscriptions you are authorized to use:</span></span>

    azure account list

<span data-ttu-id="ca0ee-143">La suscripción activa actual se identifica con `Current` establecido en `true`.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-143">The current active subscription is identified with `Current` set to `true`.</span></span> <span data-ttu-id="ca0ee-144">Si esta suscripción no es la que desea usar para crear el clúster, establezca el id. de suscripción adecuado como la suscripción activa:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-144">If this subscription isn't the one you want to use to create the cluster, set the appropriate subscription ID as the active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="ca0ee-145">Para ver las imágenes de HPC de SLES 12 SP1 disponibles públicamente en Azure, ejecute un comando similar al siguiente, asumiendo que el entorno de shell admite **grep**:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-145">To see the publicly available SLES 12 SP1 HPC images in Azure, run a command like the following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="ca0ee-146">Aprovisione una máquina virtual compatible con RDMA con una imagen de HPC de SLES 12 SP1 ejecutando un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like the following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="ca0ee-147">Donde:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-147">Where:</span></span>

* <span data-ttu-id="ca0ee-148">El tamaño (A9 en este ejemplo) es uno de los tamaños de máquina virtual compatibles con RDMA.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-148">The size (A9 in this example) is one of the RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="ca0ee-149">El número de puerto externo de SSH (22 en este ejemplo, que es el valor predeterminado de SSH) es cualquier número de puerto válido.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-149">The external SSH port number (22 in this example, which is the SSH default) is any valid port number.</span></span> <span data-ttu-id="ca0ee-150">El número de puerto interno de SSH se establece en 22.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-150">The internal SSH port number is set to 22.</span></span>
* <span data-ttu-id="ca0ee-151">Se crea un servicio en la nube en la región de Azure especificada por la ubicación.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-151">A new cloud service is created in the Azure region specified by the location.</span></span> <span data-ttu-id="ca0ee-152">Especifique una ubicación en la que esté disponible el tamaño de máquina virtual que elija.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-152">Specify a location in which the VM size you choose is available.</span></span>
* <span data-ttu-id="ca0ee-153">Para que disponga de compatibilidad prioritaria para SUSE (que puede significar cargos adicionales), el nombre de la imagen de SLES 12 SP1 puede ser una de estas dos opciones:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-153">For SUSE priority support (which incurs additional charges), the SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-the-vm"></a><span data-ttu-id="ca0ee-154">Personalización de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ca0ee-154">Customize the VM</span></span>
<span data-ttu-id="ca0ee-155">Después de que la máquina virtual finalice el aprovisionamiento, SSH a la máquina virtual con la dirección IP externa de la máquina virtual (o el nombre DNS) y el número de puerto externo que configuró y, luego, personalícelo.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-155">After the VM finishes provisioning, SSH to the VM by using the VM's external IP address (or DNS name) and the external port number you configured, and then customize it.</span></span> <span data-ttu-id="ca0ee-156">Para detalles de la conexión, consulte [Inicio de sesión en una máquina virtual Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ca0ee-156">For connection details, see [How to log on to a virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ca0ee-157">Ejecute los comandos como el usuario que haya configurado en la máquina virtual, a menos que se requiera el acceso a la raíz para completar un paso.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-157">Perform commands as the user you configured on the VM, unless root access is required to complete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca0ee-158">Microsoft Azure no proporciona acceso a la raíz a máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-158">Microsoft Azure does not provide root access to Linux VMs.</span></span> <span data-ttu-id="ca0ee-159">Para obtener acceso administrativo al conectarse como un usuario a la máquina virtual, ejecute los comandos mediante `sudo`.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-159">To gain administrative access when connected as a user to the VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="ca0ee-160">**Actualizaciones**: instale las actualizaciones mediante zypper.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="ca0ee-161">También puede instalar utilidades NFS.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-161">You might also want to install NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ca0ee-162">En una máquina virtual de HPC de SLES 12 SP1, es recomendable no aplicar actualizaciones de kernel, que pueden causar problemas con los controladores de RDMA de Linux.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with the Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="ca0ee-163">**Intel MPI**: complete la instalación de Intel MPI en la máquina virtual de HPC de SLES 12 SP1 ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-163">**Intel MPI**: Complete the installation of Intel MPI on the SLES 12 SP1 HPC VM by running the following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="ca0ee-164">**Bloquear memoria**: para que los códigos de MPI bloqueen la memoria disponible para RDMA, agregue o cambie la configuración siguiente en el archivo /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-164">**Lock memory**: For MPI codes to lock the memory available for RDMA, add or change the following settings in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="ca0ee-165">Necesita acceso a la raíz para editar este archivo.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-165">You need root access to edit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="ca0ee-166">Para realizar pruebas, también puede establecer memlock en ilimitado.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-166">For testing purposes, you can also set memlock to unlimited.</span></span> <span data-ttu-id="ca0ee-167">Por ejemplo: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="ca0ee-168">Para más información, consulte los [métodos más conocidos para definir el tamaño de memoria bloqueada](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="ca0ee-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="ca0ee-169">**Claves SSH para máquinas virtuales de SLES**: genere claves SSH para establecer la confianza para la cuenta de usuario entre los nodos de proceso del clúster de SLES al ejecutar trabajos MPI.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-169">**SSH keys for SLES VMs**: Generate SSH keys to establish trust for your user account among the compute nodes in the SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="ca0ee-170">Si implementó una máquina virtual de HPC basada en CentOS, no siga este paso.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="ca0ee-171">Consulte las instrucciones más adelante en este artículo para establecer una relación de confianza de SSH sin contraseña entre los nodos del clúster después de capturar la imagen y de implementar el clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-171">See instructions later in this article to set up passwordless SSH trust among the cluster nodes after you capture the image and deploy the cluster.</span></span>

    <span data-ttu-id="ca0ee-172">Para crear claves SSH, ejecute el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-172">To create SSH keys, run the following command.</span></span> <span data-ttu-id="ca0ee-173">Cuando se le pida una entrada, seleccione **Entrar** para generar las claves en la ubicación predeterminada sin tener que establecer una contraseña.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-173">When you are prompted for input, select **Enter** to generate the keys in the default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="ca0ee-174">Agregue la clave pública al archivo authorized_keys para las claves públicas conocidas.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-174">Append the public key to the authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="ca0ee-175">En el directorio ~/.ssh, edite o cree el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-175">In the ~/.ssh directory, edit or create the config file.</span></span> <span data-ttu-id="ca0ee-176">Proporcione el intervalo de direcciones IP de la red privada que planea usar en Azure (10.32.0.0/16 en este ejemplo):</span><span class="sxs-lookup"><span data-stu-id="ca0ee-176">Provide the IP address range of the private network that you plan to use in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="ca0ee-177">O bien, especifique la dirección IP de red privada de cada máquina virtual en el clúster como sigue:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-177">Alternatively, list the private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="ca0ee-178">Configurar `StrictHostKeyChecking no` puede crear un posible riesgo de seguridad cuando no se especifica una dirección IP o un intervalo concretos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="ca0ee-179">**Aplicaciones**: instale todas las aplicaciones que necesite o realice otras personalizaciones antes de capturar la imagen.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-179">**Applications**: Install any applications you need or perform other customizations before you capture the image.</span></span>

### <a name="capture-the-image"></a><span data-ttu-id="ca0ee-180">Capturar la imagen</span><span class="sxs-lookup"><span data-stu-id="ca0ee-180">Capture the image</span></span>
<span data-ttu-id="ca0ee-181">Para capturar la imagen, primero ejecute el comando siguiente en la máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-181">To capture the image, first run the following command on the Linux VM.</span></span> <span data-ttu-id="ca0ee-182">Este comando desaprovisiona la máquina virtual, pero mantiene las cuentas de usuario y las claves SSH que configure.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-182">This command deprovisions the VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="ca0ee-183">Desde el equipo cliente, ejecute los siguientes comandos de CLI de Azure para capturar la imagen.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-183">From your client computer, run the following Azure CLI commands to capture the image.</span></span> <span data-ttu-id="ca0ee-184">Para más información, consulte [Captura de una máquina virtual clásica con Linux para usarla como imagen](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="ca0ee-184">For more information, see [How to capture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="ca0ee-185">Después de ejecutar estos comandos, se captura la imagen de máquina virtual para su uso y se elimina la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-185">After you run these commands, the VM image is captured for your use and the VM is deleted.</span></span> <span data-ttu-id="ca0ee-186">Ahora tiene la imagen personalizada lista para implementar un clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-186">Now you have your custom image ready to deploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-the-image"></a><span data-ttu-id="ca0ee-187">Implementar un clúster con la imagen</span><span class="sxs-lookup"><span data-stu-id="ca0ee-187">Deploy a cluster with the image</span></span>
<span data-ttu-id="ca0ee-188">Modifique el script Bash siguiente con los valores apropiados para su entorno y ejecútelo desde el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-188">Modify the following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="ca0ee-189">Debido a que Azure implementa las máquinas virtuales en serie en el modelo de implementación clásica, tardará unos minutos en implementar las ocho máquinas virtuales A9 sugeridas en este script.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-189">Because Azure deploys the VMs serially in the classic deployment model, it takes a few minutes to deploy the eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script to create a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where the VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All the compute-intensive instances need to be in the same cloud service for Linux RDMA to work across InfiniBand.
# Note: The current maximum number of VMs in a cloud service is 50. If you need to provision more than 50 VMs in the same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want to turn off external ports and use only internal ports to communicate between compute nodes via port 22, don’t use this option. Since port numbers up to 10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 to cluster18. Specify your captured image in <image-name>. Specify the username and password you used when creating the SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment to provision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="ca0ee-190">Consideraciones para un clúster de HPC de CentOS</span><span class="sxs-lookup"><span data-stu-id="ca0ee-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="ca0ee-191">Si desea configurar un clúster basado en una de las imágenes de HPC de CentOS en Azure Marketplace en lugar de SLES 12 para HPC, siga los pasos generales de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-191">If you want to set up a cluster based on one of the CentOS-based HPC images in the Azure Marketplace instead of SLES 12 for HPC, follow the general steps in the preceding section.</span></span> <span data-ttu-id="ca0ee-192">Tenga en cuenta las siguientes diferencias al aprovisionar y configurar la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-192">Note the following differences when you provision and configure the VM:</span></span>

- <span data-ttu-id="ca0ee-193">Intel MPI ya está instalado en una máquina virtual aprovisionada desde una imagen de HPC basada en CentOS.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="ca0ee-194">La configuración de memoria bloqueada ya está agregada en el archivo /etc/security/limits.conf de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-194">Lock memory settings are already added in the VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="ca0ee-195">No se generan claves SSH en la máquina virtual aprovisionada para la captura.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-195">Do not generate SSH keys on the VM you provision for capture.</span></span> <span data-ttu-id="ca0ee-196">En su lugar, se recomienda establecer la autenticación basada en usuario después de implementar el clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-196">Instead, we recommend setting up user-based authentication after you deploy the cluster.</span></span> <span data-ttu-id="ca0ee-197">Para más información, consulte la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-197">For more information, see the following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-the-cluster"></a><span data-ttu-id="ca0ee-198">Configuración de confianza SSH sin contraseña en el clúster</span><span class="sxs-lookup"><span data-stu-id="ca0ee-198">Set up passwordless SSH trust on the cluster</span></span>
<span data-ttu-id="ca0ee-199">En un clúster de HPC basado en CentOS, existen dos métodos para establecer la confianza entre los nodos de proceso: la autenticación basada en host y la autenticación basada en usuario.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between the compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="ca0ee-200">La autenticación basada en host está fuera del ámbito de este artículo y por lo general debe realizarse a través de un script de extensión durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-200">Host-based authentication is outside of the scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="ca0ee-201">La autenticación basada en usuario es conveniente para establecer la confianza después de la implementación y requiere la generación y el uso compartido de claves SSH entre los nodos de proceso en el clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-201">User-based authentication is convenient for establishing trust after deployment and requires the generation and sharing of SSH keys among the compute nodes in the cluster.</span></span> <span data-ttu-id="ca0ee-202">Este método se suele conocer como inicio de sesión SSH sin contraseña y es necesario al ejecutar trabajos de MPI.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="ca0ee-203">Está disponible un script de ejemplo proporcionado por la comunidad en [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) para habilitar la autenticación de usuario sencilla en un clúster HPC basado en CentOS.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-203">A sample script contributed from the community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) to enable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="ca0ee-204">Descargue y use este script mediante los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-204">Download and use this script by using the following steps.</span></span> <span data-ttu-id="ca0ee-205">También puede modificar este script o utilizar cualquier otro método para establecer la autenticación de SSH sin contraseña entre los nodos del clúster de proceso.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-205">You can also modify this script or use any other method to establish passwordless SSH authentication between the cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="ca0ee-206">Para ejecutar el script, debe conocer el prefijo para las direcciones IP de subred.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-206">To run the script, you need to know the prefix for your subnet IP addresses.</span></span> <span data-ttu-id="ca0ee-207">Para obtener el prefijo, ejecute el siguiente comando en uno de los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-207">Get the prefix by running the following command on one of the cluster nodes.</span></span> <span data-ttu-id="ca0ee-208">El resultado debe ser similar al de 10.1.3.5, y el prefijo es la parte 10.1.3.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-208">Your output should look something like 10.1.3.5, and the prefix is the 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="ca0ee-209">Ahora ejecute el script con tres parámetros: el nombre de usuario común en los nodos de proceso, la contraseña común de ese usuario en los nodos de proceso y el prefijo de subred que se devolvió en el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-209">Now run the script using three parameters: the common user name on the compute nodes, the common password for that user on the compute nodes, and the subnet prefix that was returned from the previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="ca0ee-210">El script hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-210">This script does the following:</span></span>

* <span data-ttu-id="ca0ee-211">Crea un directorio en el nodo de host de host denominado .ssh, que es necesario para el inicio de sesión sin contraseña.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-211">Creates a directory on the host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="ca0ee-212">Crea un archivo de configuración en el directorio .ssh que indica el inicio de sesión sin contraseña para permitir el inicio de sesión desde cualquier nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-212">Creates a configuration file in the .ssh directory that instructs passwordless login to allow login from any node in the cluster.</span></span>
* <span data-ttu-id="ca0ee-213">Crea archivos que contienen los nombres de nodo y las direcciones IP de nodo para todos los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-213">Creates files containing the node names and node IP addresses for all the nodes in the cluster.</span></span> <span data-ttu-id="ca0ee-214">Estos archivos se mantienen después de ejecutar el script como referencia futura.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-214">These files are left after the script is run for later reference.</span></span>
* <span data-ttu-id="ca0ee-215">Crea un par de claves pública y privada para cada nodo de clúster, incluido el nodo de host, y crea entradas en el archivo authorized_keys.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-215">Creates a private and public key pair for each cluster node (including the host node) and creates entries in the authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="ca0ee-216">La ejecución de este script puede crear un posible riesgo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="ca0ee-217">Asegúrese de que no se distribuye la información de clave pública en ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-217">Ensure that the public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="ca0ee-218">Configuración de Intel MPI</span><span class="sxs-lookup"><span data-stu-id="ca0ee-218">Configure Intel MPI</span></span>
<span data-ttu-id="ca0ee-219">Para ejecutar aplicaciones de MPI en Azure Linux RDMA, necesitará configurar ciertas variables de entorno específicas de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-219">To run MPI applications on Azure Linux RDMA, you need to configure certain environment variables specific to Intel MPI.</span></span> <span data-ttu-id="ca0ee-220">A continuación se muestra un script Bash de ejemplo para configurar las variables necesarias para ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-220">Here is a sample Bash script to configure the variables needed to run an application.</span></span> <span data-ttu-id="ca0ee-221">Cambie la ruta de acceso a mpivars.sh según sea necesario para la instalación de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-221">Change the path to mpivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting the variable to shm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line to run the job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path to the application exe> <arguments specific to the application>

#end
```

<span data-ttu-id="ca0ee-222">El formato del archivo host es el siguiente.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-222">The format of the host file is as follows.</span></span> <span data-ttu-id="ca0ee-223">Agregue una línea para cada nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="ca0ee-224">Especifique las direcciones IP privadas de la red virtual definida anteriormente, no los nombres DNS.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-224">Specify private IP addresses from the virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="ca0ee-225">Por ejemplo, para dos hosts con direcciones IP 10.32.0.1 y 10.32.0.2, el archivo contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, the file contains the following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="ca0ee-226">Ejecución de MPI en un clúster de dos nodos básico</span><span class="sxs-lookup"><span data-stu-id="ca0ee-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="ca0ee-227">Si aún no lo hizo, configure primero el entorno para Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-227">If you haven't already done so, first set up the environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="ca0ee-228">Ejecución de un comando de MPI</span><span class="sxs-lookup"><span data-stu-id="ca0ee-228">Run an MPI command</span></span>
<span data-ttu-id="ca0ee-229">Ejecute un comando de MPI en uno de los nodos de proceso para mostrar que MPI se instaló correctamente y puede comunicarse entre al menos dos nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-229">Run an MPI command on one of the compute nodes to show that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="ca0ee-230">El siguiente comando **mpirun** ejecuta el comando **hostname** en dos nodos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-230">The following **mpirun** command runs the **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="ca0ee-231">La salida debe enumerar los nombres de todos los nodos que se pasaron como entrada para `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-231">Your output should list the names of all the nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="ca0ee-232">Por ejemplo, un comando **mpirun** con dos nodos devuelve una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca0ee-232">For example, an **mpirun** command with two nodes returns output like the following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="ca0ee-233">Ejecución de una prueba comparativa de MPI</span><span class="sxs-lookup"><span data-stu-id="ca0ee-233">Run an MPI benchmark</span></span>
<span data-ttu-id="ca0ee-234">El siguiente comando de Intel MPI ejecuta una prueba comparativa de pingpong para comprobar la configuración del clúster y la conexión a la red de RDMA.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-234">The following Intel MPI command runs a pingpong benchmark to verify the cluster configuration and connection to the RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="ca0ee-235">Debería ver un resultado similar al siguiente en un clúster de trabajo con dos nodos.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-235">On a working cluster with two nodes, you should see output like the following.</span></span> <span data-ttu-id="ca0ee-236">En la red de RDMA de Azure, se espera una latencia igual o inferior a 3 microsegundos para los tamaños de mensaje de hasta 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-236">On the Azure RDMA network, expect latency at or below 3 microseconds for message sizes up to 512 bytes.</span></span>

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
# the number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected to be exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through the flag => -time

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
# List of Benchmarks to run:
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



## <a name="next-steps"></a><span data-ttu-id="ca0ee-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca0ee-237">Next steps</span></span>
* <span data-ttu-id="ca0ee-238">Implemente y ejecute las aplicaciones Linux MPI en el clúster de Linux.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="ca0ee-239">Consulte la [documentación de la biblioteca de Intel MPI](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) para obtener orientación sobre Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-239">See the [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="ca0ee-240">Pruebe una [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) para crear un clúster de Intel Lustre mediante una imagen HPC basada en CentOS.</span><span class="sxs-lookup"><span data-stu-id="ca0ee-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) to create an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="ca0ee-241">Para más información, consulte [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/) (Implementación de la edición de nube de Intel para Lustre en Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="ca0ee-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
