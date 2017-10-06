---
title: aaaResources de lote y HPC en hello nube de Azure | Documentos de Microsoft
description: "Enumera toohelp recursos técnicos ejecutar la paralelas a gran escala, lote y las cargas de trabajo (HPC) en Azure de informática de alto rendimiento."
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
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="fedd7-103">Big Compute en Azure: Recursos técnicos para informática de alto rendimiento y computación por lotes</span><span class="sxs-lookup"><span data-stu-id="fedd7-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="fedd7-104">Se trata de un toohelp de recursos de guía tootechnical ejecutar la paralelas a gran escala, lote y las cargas de trabajo de informática de alto rendimiento (HPC) en Azure.</span><span class="sxs-lookup"><span data-stu-id="fedd7-104">This is a guide tootechnical resources toohelp you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="fedd7-105">Ampliar su lote existente o toohello de las cargas de trabajo HPC nube de Azure, o cree nuevas soluciones de Big Compute con los servicios de un intervalo de Azure.</span><span class="sxs-lookup"><span data-stu-id="fedd7-105">Extend your existing batch or HPC workloads toohello Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="fedd7-106">Opciones de soluciones</span><span class="sxs-lookup"><span data-stu-id="fedd7-106">Solutions options</span></span>
<span data-ttu-id="fedd7-107">Obtenga información acerca de las opciones de Big Compute en Azure y elija el enfoque correcto de Hola para sus necesidades de negocio y carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fedd7-107">Learn about Big Compute options in Azure, and choose hello right approach for your workload and business need.</span></span>

* [<span data-ttu-id="fedd7-108">Soluciones HPC y Lote</span><span class="sxs-lookup"><span data-stu-id="fedd7-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="fedd7-109">Vídeo: Big Compute en la nube de hello con Azure y HPC</span><span class="sxs-lookup"><span data-stu-id="fedd7-109">Video: Big Compute in hello cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="fedd7-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="fedd7-110">Azure Batch</span></span>
<span data-ttu-id="fedd7-111">[Lote](https://azure.microsoft.com/services/batch/) es un servicio de plataforma que resulta fácil toocloud a habilitar las aplicaciones de Windows y Linux y trabajos de ejecución sin configurar y administrar un clúster y el trabajo de programador.</span><span class="sxs-lookup"><span data-stu-id="fedd7-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy toocloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="fedd7-112">Usar las aplicaciones cliente de hello SDK toointegrate con Azure Batch a través de varios idiomas, fase tooAzure de datos y crear canalizaciones de ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="fedd7-112">Use hello SDK toointegrate client applications with Azure Batch through various languages, stage data tooAzure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="fedd7-113">Documentación</span><span class="sxs-lookup"><span data-stu-id="fedd7-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="fedd7-114">Referencia de [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) y API de [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)</span><span class="sxs-lookup"><span data-stu-id="fedd7-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="fedd7-115">[biblioteca .NET de administración de Lote](https://msdn.microsoft.com/library/mt463120.aspx)</span><span class="sxs-lookup"><span data-stu-id="fedd7-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="fedd7-116">Tutoriales: Introducción a la [biblioteca de Azure Batch para .NET](batch-dotnet-get-started.md) y el [cliente Python de Batch](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="fedd7-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="fedd7-117">Foro de Batch</span><span class="sxs-lookup"><span data-stu-id="fedd7-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="fedd7-118">Vídeos de Batch</span><span class="sxs-lookup"><span data-stu-id="fedd7-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="fedd7-119">Soluciones de clúster de HPC</span><span class="sxs-lookup"><span data-stu-id="fedd7-119">HPC cluster solutions</span></span>
<span data-ttu-id="fedd7-120">Implementar o ampliar su toorun existente de Windows o Linux HPC cluster tooAzure las cargas de trabajo intensivas de proceso.</span><span class="sxs-lookup"><span data-stu-id="fedd7-120">Deploy or extend your existing Windows or Linux HPC cluster tooAzure toorun your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="fedd7-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="fedd7-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="fedd7-122">HPC Pack es la solución HPC gratuita de Microsoft que se basa en las tecnologías de Microsoft Azure y Windows Server, capaz de ejecutar cargas de trabajo HPC de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="fedd7-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="fedd7-123">Descargar HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="fedd7-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="fedd7-124">Descargar HPC Pack 2012 R2 Update 3</span><span class="sxs-lookup"><span data-stu-id="fedd7-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="fedd7-125">Documentación</span><span class="sxs-lookup"><span data-stu-id="fedd7-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="fedd7-126">Opciones del clúster de HPC Pack de [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en Azure</span><span class="sxs-lookup"><span data-stu-id="fedd7-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="fedd7-127">Irrumpir en instancias de trabajo tooAzure con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="fedd7-127">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="fedd7-128">Ráfaga tooAzure por lotes con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="fedd7-128">Burst tooAzure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="fedd7-129">Foros de Windows HPC</span><span class="sxs-lookup"><span data-stu-id="fedd7-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="fedd7-130">Soluciones de clúster de Linux y OSS</span><span class="sxs-lookup"><span data-stu-id="fedd7-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="fedd7-131">Use estos toodeploy de plantillas de Azure de clústeres de Linux HPC.</span><span class="sxs-lookup"><span data-stu-id="fedd7-131">Use these Azure templates toodeploy Linux HPC clusters.</span></span>

* <span data-ttu-id="fedd7-132">[Establecimiento de un clúster SLURM](https://azure.microsoft.com/documentation/templates/slurm/) y una [entrada de blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="fedd7-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="fedd7-133">Establecimiento de un clúster de par</span><span class="sxs-lookup"><span data-stu-id="fedd7-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="fedd7-134">Plantillas de cuadrícula proceso con PBS Professional</span><span class="sxs-lookup"><span data-stu-id="fedd7-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="fedd7-135">Almacenamiento de HPC</span><span class="sxs-lookup"><span data-stu-id="fedd7-135">HPC storage</span></span>
* [<span data-ttu-id="fedd7-136">Sistemas de archivos en paralelo para el almacenamiento de HPC en Azure</span><span class="sxs-lookup"><span data-stu-id="fedd7-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="fedd7-137">Edición de nube de Intel para Software de Lustre - Eval</span><span class="sxs-lookup"><span data-stu-id="fedd7-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="fedd7-138">BeeGFS en la plantilla de CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="fedd7-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="fedd7-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="fedd7-139">Microsoft MPI</span></span>
<span data-ttu-id="fedd7-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) es una implementación de Microsoft de hello interfaz de pasar del mensaje estándar para desarrollar y ejecutar aplicaciones en paralelo en la plataforma de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="fedd7-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of hello Message Passing Interface standard for developing and running parallel applications on hello Windows platform.</span></span>

* [<span data-ttu-id="fedd7-141">Descargar MS-MPI</span><span class="sxs-lookup"><span data-stu-id="fedd7-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="fedd7-142">Referencia de MS-MPI</span><span class="sxs-lookup"><span data-stu-id="fedd7-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="fedd7-143">Foro de MPI</span><span class="sxs-lookup"><span data-stu-id="fedd7-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="fedd7-144">Instancias de proceso intensivo</span><span class="sxs-lookup"><span data-stu-id="fedd7-144">Compute-intensive instances</span></span>
<span data-ttu-id="fedd7-145">Azure ofrece un [tamaños de intervalo de la máquina virtual](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), incluido [H-series de proceso intensivo](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instancias capaces de conectar la red de tooa back-end RDMA, toorun las cargas de trabajo de HPC de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="fedd7-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting tooa back-end RDMA network, toorun your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="fedd7-146">Configurar una aplicación de MPI Linux RDMA toorun de clúster</span><span class="sxs-lookup"><span data-stu-id="fedd7-146">Set up a Linux RDMA cluster toorun MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="fedd7-147">Configurar un clúster de Windows RDMA con aplicaciones de MPI de Microsoft HPC Pack toorun</span><span class="sxs-lookup"><span data-stu-id="fedd7-147">Set up a Windows RDMA cluster with Microsoft HPC Pack toorun MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="fedd7-148">Para cargas de trabajo intensivas de la GPU, eche un vistazo al artículo de [tamaños NC y NV](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="fedd7-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="fedd7-149">Ejemplos y demos</span><span class="sxs-lookup"><span data-stu-id="fedd7-149">Samples and demos</span></span>
* [<span data-ttu-id="fedd7-150">Ejemplos de código de Lote de Azure para C# y Python</span><span class="sxs-lookup"><span data-stu-id="fedd7-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="fedd7-151">[Procesar por lotes astilleros](https://azure.github.io/batch-shipyard/) Kit de herramientas para facilitar la implementación de estilo de lote Dockerized las cargas de trabajo tooAzure por lotes</span><span class="sxs-lookup"><span data-stu-id="fedd7-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads tooAzure Batch</span></span>
* <span data-ttu-id="fedd7-152">El paquete de R[doAzureParallel](http://www.github.com/Azure/doAzureParallel), creado a partir de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="fedd7-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="fedd7-153">Versión de prueba de SUSE Linux Enterprise Server para HPC</span><span class="sxs-lookup"><span data-stu-id="fedd7-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="fedd7-154">Servicios de Azure relacionados</span><span class="sxs-lookup"><span data-stu-id="fedd7-154">Related Azure services</span></span>
* [<span data-ttu-id="fedd7-155">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="fedd7-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="fedd7-156">Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="fedd7-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="fedd7-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="fedd7-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="fedd7-158">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fedd7-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="fedd7-159">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fedd7-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="fedd7-160">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="fedd7-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="fedd7-161">Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fedd7-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="fedd7-162">Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="fedd7-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="fedd7-163">Funciones</span><span class="sxs-lookup"><span data-stu-id="fedd7-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="fedd7-164">Proyectos de arquitectura</span><span class="sxs-lookup"><span data-stu-id="fedd7-164">Architecture blueprints</span></span>
* <span data-ttu-id="fedd7-165">Archivo PDF [HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (Orquestación de HPC y datos mediante Lote de Azure y Data Factory de Azure) y este [artículo](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="fedd7-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="fedd7-166">Soluciones del sector</span><span class="sxs-lookup"><span data-stu-id="fedd7-166">Industry solutions</span></span>
* [<span data-ttu-id="fedd7-167">Mercados de capital y banca</span><span class="sxs-lookup"><span data-stu-id="fedd7-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="fedd7-168">Simulaciones de ingeniería</span><span class="sxs-lookup"><span data-stu-id="fedd7-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="fedd7-169">Testimonios de clientes</span><span class="sxs-lookup"><span data-stu-id="fedd7-169">Customer stories</span></span>
* [<span data-ttu-id="fedd7-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="fedd7-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="fedd7-171">d3View</span><span class="sxs-lookup"><span data-stu-id="fedd7-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="fedd7-172">Ludwig Institute of Cancer Research (Instituto Ludwig de investigación del cáncer)</span><span class="sxs-lookup"><span data-stu-id="fedd7-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="fedd7-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="fedd7-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="fedd7-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="fedd7-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="fedd7-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="fedd7-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="fedd7-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="fedd7-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="fedd7-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="fedd7-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="fedd7-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="fedd7-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="fedd7-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fedd7-179">Next steps</span></span>
* <span data-ttu-id="fedd7-180">Para anuncios de Hola más recientes, consulte hello [blog del equipo de Microsoft HPC y lote](http://blogs.technet.com/b/windowshpc/) hello y [blog de Azure](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="fedd7-180">For hello latest announcements, see hello [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and hello [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="fedd7-181">Consulte también [what's new en lote](https://azure.microsoft.com/updates/?service=batch) o suscribirse toohello [fuente RSS](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="fedd7-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe toohello [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

