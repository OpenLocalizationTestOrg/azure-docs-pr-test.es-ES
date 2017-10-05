---
title: Recursos para cargas de trabajo por lotes y HPC en la nube de Azure | Microsoft Docs
description: "Enumera los recursos técnicos para ayudarle a ejecutar cargas de trabajo por lotes, a gran escala en paralelo y de informática de alto rendimiento (HPC) en Azure."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: 18be9f503b57117a7e8f5f0a4e9c93614cc7755b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="13e50-103">Big Compute en Azure: Recursos técnicos para informática de alto rendimiento y computación por lotes</span><span class="sxs-lookup"><span data-stu-id="13e50-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="13e50-104">Esta es una guía de recursos técnicos para ayudarle a ejecutar cargas de trabajo por lotes, a gran escala en paralelo y de informática de alto rendimiento (HPC) en Azure.</span><span class="sxs-lookup"><span data-stu-id="13e50-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="13e50-105">Amplíe sus cargas de trabajo de HPC o de lotes existentes a la nube de Azure, o cree nuevas soluciones de Big Compute mediante una gama de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="13e50-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="13e50-106">Opciones de soluciones</span><span class="sxs-lookup"><span data-stu-id="13e50-106">Solutions options</span></span>
<span data-ttu-id="13e50-107">Obtenga información sobre las opciones de Big Compute en Azure y elija el enfoque correcto para sus necesidades empresariales y de carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="13e50-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="13e50-108">Soluciones HPC y Lote</span><span class="sxs-lookup"><span data-stu-id="13e50-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="13e50-109">Vídeo: Big Compute en la nube con Azure y HPC</span><span class="sxs-lookup"><span data-stu-id="13e50-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="13e50-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="13e50-110">Azure Batch</span></span>
<span data-ttu-id="13e50-111">[Lote](https://azure.microsoft.com/services/batch/) es un servicio de plataforma que facilita el proceso de habilitar para la nube sus aplicaciones y de ejecutar trabajos sin configurar y administrar un clúster y un programador de trabajos.</span><span class="sxs-lookup"><span data-stu-id="13e50-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="13e50-112">Use el SDK para integrar aplicaciones cliente con Azure Batch a través de varios lenguajes, almacenar datos en Azure y crear canalizaciones de ejecución de trabajos.</span><span class="sxs-lookup"><span data-stu-id="13e50-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="13e50-113">Documentación</span><span class="sxs-lookup"><span data-stu-id="13e50-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="13e50-114">Referencia de [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) y API de [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)</span><span class="sxs-lookup"><span data-stu-id="13e50-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="13e50-115">[biblioteca .NET de administración de Lote](https://msdn.microsoft.com/library/mt463120.aspx) </span><span class="sxs-lookup"><span data-stu-id="13e50-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="13e50-116">Tutoriales: Introducción a la [biblioteca de Azure Batch para .NET](batch-dotnet-get-started.md) y el [cliente Python de Batch](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="13e50-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="13e50-117">Foro de Batch</span><span class="sxs-lookup"><span data-stu-id="13e50-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="13e50-118">Vídeos de Batch</span><span class="sxs-lookup"><span data-stu-id="13e50-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="13e50-119">Soluciones de clúster de HPC</span><span class="sxs-lookup"><span data-stu-id="13e50-119">HPC cluster solutions</span></span>
<span data-ttu-id="13e50-120">Implemente o amplíe su clúster de Windows o Linux HPC existente para ejecutar sus cargas de trabajo intensivas de proceso.</span><span class="sxs-lookup"><span data-stu-id="13e50-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="13e50-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="13e50-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="13e50-122">HPC Pack es la solución HPC gratuita de Microsoft que se basa en las tecnologías de Microsoft Azure y Windows Server, capaz de ejecutar cargas de trabajo HPC de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="13e50-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="13e50-123">Descargar HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="13e50-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="13e50-124">Descargar HPC Pack 2012 R2 Update 3</span><span class="sxs-lookup"><span data-stu-id="13e50-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="13e50-125">Documentación</span><span class="sxs-lookup"><span data-stu-id="13e50-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="13e50-126">Opciones del clúster de HPC Pack de [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en Azure</span><span class="sxs-lookup"><span data-stu-id="13e50-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="13e50-127">Irrumpir en instancias de trabajo de Azure con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="13e50-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="13e50-128">Expansión a Azure Batch con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="13e50-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="13e50-129">Foros de Windows HPC</span><span class="sxs-lookup"><span data-stu-id="13e50-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="13e50-130">Soluciones de clúster de Linux y OSS</span><span class="sxs-lookup"><span data-stu-id="13e50-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="13e50-131">Use estas plantillas de Azure para implementar clústeres de HPC de Linux.</span><span class="sxs-lookup"><span data-stu-id="13e50-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="13e50-132">[Establecimiento de un clúster SLURM](https://azure.microsoft.com/documentation/templates/slurm/) y una [entrada de blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="13e50-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="13e50-133">Establecimiento de un clúster de par</span><span class="sxs-lookup"><span data-stu-id="13e50-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="13e50-134">Plantillas de cuadrícula proceso con PBS Professional</span><span class="sxs-lookup"><span data-stu-id="13e50-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="13e50-135">Almacenamiento de HPC</span><span class="sxs-lookup"><span data-stu-id="13e50-135">HPC storage</span></span>
* [<span data-ttu-id="13e50-136">Sistemas de archivos en paralelo para el almacenamiento de HPC en Azure</span><span class="sxs-lookup"><span data-stu-id="13e50-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="13e50-137">Edición de nube de Intel para Software de Lustre - Eval</span><span class="sxs-lookup"><span data-stu-id="13e50-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="13e50-138">BeeGFS en la plantilla de CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="13e50-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="13e50-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="13e50-139">Microsoft MPI</span></span>
<span data-ttu-id="13e50-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) es una implementación de Microsoft del estándar de la interfaz de especificación de mensajes para desarrollar y ejecutar aplicaciones en paralelo en la plataforma de Windows.</span><span class="sxs-lookup"><span data-stu-id="13e50-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="13e50-141">Descargar MS-MPI</span><span class="sxs-lookup"><span data-stu-id="13e50-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="13e50-142">Referencia de MS-MPI</span><span class="sxs-lookup"><span data-stu-id="13e50-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="13e50-143">Foro de MPI</span><span class="sxs-lookup"><span data-stu-id="13e50-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="13e50-144">Instancias de proceso intensivo</span><span class="sxs-lookup"><span data-stu-id="13e50-144">Compute-intensive instances</span></span>
<span data-ttu-id="13e50-145">Azure ofrece un [rango de tamaños de VM](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), que incluye instancias de [serie H con un proceso intensivo](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) con capacidad para conectarse a una red RDMA de back-end, para ejecutar cargas de trabajo HPC de Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="13e50-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="13e50-146">Configuración de un clúster de Linux RDMA para ejecutar aplicaciones MPI</span><span class="sxs-lookup"><span data-stu-id="13e50-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="13e50-147">Configuración de un clúster de Windows RDMA con HPC Pack para ejecutar aplicaciones MPI</span><span class="sxs-lookup"><span data-stu-id="13e50-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="13e50-148">Para cargas de trabajo intensivas de la GPU, eche un vistazo al artículo de [tamaños NC y NV](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="13e50-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="13e50-149">Ejemplos y demos</span><span class="sxs-lookup"><span data-stu-id="13e50-149">Samples and demos</span></span>
* [<span data-ttu-id="13e50-150">Ejemplos de código de Lote de Azure para C# y Python</span><span class="sxs-lookup"><span data-stu-id="13e50-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="13e50-151">El kit de herramientas [Batch Shipyard](https://azure.github.io/batch-shipyard/) para facilitar la implementación en Azure Batch de cargas de trabajo de estilo lote "dockerizadas".</span><span class="sxs-lookup"><span data-stu-id="13e50-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="13e50-152">El paquete de R[doAzureParallel](http://www.github.com/Azure/doAzureParallel), creado a partir de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="13e50-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="13e50-153">Versión de prueba de SUSE Linux Enterprise Server para HPC</span><span class="sxs-lookup"><span data-stu-id="13e50-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="13e50-154">Servicios de Azure relacionados</span><span class="sxs-lookup"><span data-stu-id="13e50-154">Related Azure services</span></span>
* [<span data-ttu-id="13e50-155">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="13e50-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="13e50-156">Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="13e50-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="13e50-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="13e50-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="13e50-158">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="13e50-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="13e50-159">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="13e50-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="13e50-160">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="13e50-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="13e50-161">Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="13e50-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="13e50-162">Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="13e50-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="13e50-163">Funciones</span><span class="sxs-lookup"><span data-stu-id="13e50-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="13e50-164">Proyectos de arquitectura</span><span class="sxs-lookup"><span data-stu-id="13e50-164">Architecture blueprints</span></span>
* <span data-ttu-id="13e50-165">Archivo PDF [HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (Orquestación de HPC y datos mediante Lote de Azure y Data Factory de Azure) y este [artículo](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="13e50-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="13e50-166">Soluciones del sector</span><span class="sxs-lookup"><span data-stu-id="13e50-166">Industry solutions</span></span>
* [<span data-ttu-id="13e50-167">Mercados de capital y banca</span><span class="sxs-lookup"><span data-stu-id="13e50-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="13e50-168">Simulaciones de ingeniería</span><span class="sxs-lookup"><span data-stu-id="13e50-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="13e50-169">Testimonios de clientes</span><span class="sxs-lookup"><span data-stu-id="13e50-169">Customer stories</span></span>
* [<span data-ttu-id="13e50-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="13e50-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="13e50-171">d3View</span><span class="sxs-lookup"><span data-stu-id="13e50-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="13e50-172">Ludwig Institute of Cancer Research (Instituto Ludwig de investigación del cáncer)</span><span class="sxs-lookup"><span data-stu-id="13e50-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="13e50-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="13e50-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="13e50-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="13e50-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="13e50-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="13e50-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="13e50-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="13e50-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="13e50-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="13e50-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="13e50-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="13e50-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="13e50-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13e50-179">Next steps</span></span>
* <span data-ttu-id="13e50-180">Para los anuncios más recientes, lea el [blog del equipo de Microsoft HPC y Batch](http://blogs.technet.com/b/windowshpc/) y el [blog de Azure](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="13e50-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="13e50-181">Vea también [Actualizaciones de Azure](https://azure.microsoft.com/updates/?service=batch) o suscríbase a la [fuente RSS](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="13e50-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

