---
title: "conjuntos de datos a gran escala de aaaProcess con factoría de datos y por lotes | Documentos de Microsoft"
description: "Describe cómo tooprocess enormes cantidades de datos de una factoría de datos de Azure de canalización mediante el uso de capacidad de procesamiento en paralelo de lote de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="8ee7b-103">Procesamiento de datos a gran escala mediante Data Factory y Batch</span><span class="sxs-lookup"><span data-stu-id="8ee7b-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="8ee7b-104">En este artículo se describe la arquitectura de una solución de ejemplo en la que se mueven y se procesan conjuntos de datos a gran escala de forma automática y programada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="8ee7b-105">También proporciona una solución de hello-to-end tutorial tooimplement con factoría de datos de Azure y Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="8ee7b-106">Este artículo es más largo de lo habitual, ya que contiene un tutorial de una solución de ejemplo completa.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="8ee7b-107">Si estás tooBatch nuevo y el generador de datos, puede obtener información acerca de estos servicios y cómo funcionan conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="8ee7b-108">Si sabe algo acerca de los servicios de Hola y se diseña y diseñar una solución, se puede concentrar en hello [sección arquitectura](#architecture-of-sample-solution) del artículo de Hola y si está desarrollando un prototipo o una solución, puede que también desee tootry out instrucciones paso a paso en hello [tutorial](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="8ee7b-109">No dude en hacernos llegar cualquier comentario que tenga sobre el contenido y su uso.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="8ee7b-110">En primer lugar, echemos un vistazo a cómo pueden ayudar servicios de la factoría de datos y por lotes con el procesamiento de grandes conjuntos de datos en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="8ee7b-111">¿Por qué elegir Azure Batch?</span><span class="sxs-lookup"><span data-stu-id="8ee7b-111">Why Azure Batch?</span></span>
<span data-ttu-id="8ee7b-112">Lote de Azure también permite que las aplicaciones a gran escala paralelas y de alto rendimiento informática (HPC) de toorun eficacia en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="8ee7b-113">Es un servicio de plataforma que programa el trabajo de proceso intensivo toorun en una colección administrada de máquinas virtuales, y puede automáticamente escala calcular necesidades de hello toomeet de recursos de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="8ee7b-114">Con hello servicio por lotes, se definen las tooexecute de recursos de proceso de Azure las aplicaciones en paralelo y a escala.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="8ee7b-115">Puede ejecutar a petición o programado trabajos y no es necesario toomanually crear, configurar y administrar un clúster de HPC, máquinas virtuales individuales, redes virtuales o un trabajo complejo e infraestructura de programación de tareas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="8ee7b-116">Vea Hola siguientes artículos si no está familiarizado con el lote de Azure ya que esto ayuda a comprender Hola arquitectura e implementación de solución de hello descrita en este artículo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="8ee7b-117">Datos básicos de Lote de Batch</span><span class="sxs-lookup"><span data-stu-id="8ee7b-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="8ee7b-118">Información general de las características de Lote</span><span class="sxs-lookup"><span data-stu-id="8ee7b-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="8ee7b-119">(opcional) toolearn más información acerca de Azure Batch, vea hello [ruta de acceso de aprendizaje para Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="8ee7b-120">¿Por qué elegir Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="8ee7b-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="8ee7b-121">Factoría de datos es un servicio de integración de datos en la nube que organiza y automatiza el movimiento de Hola y la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="8ee7b-122">Usar servicio de factoría de datos de hello, puede crear canalizaciones de datos administrados que se mueven datos desde el entorno local y almacén de datos centralizado de tooa de almacenes de datos en la nube (por ejemplo: almacenamiento de blobs de Azure) y el proceso o transformar datos mediante servicios como HDInsight de Azure y Azure Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="8ee7b-123">También puede programar toorun de canalizaciones de datos de una manera programada (cada hora, diariamente, semanalmente, etc.) y un monitor y administrarlos en un problemas de tooidentify de vista y tomar medidas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="8ee7b-124">Vea Hola siguientes artículos si no está familiarizado con Data Factory de Azure ya que esto ayuda a comprender Hola arquitectura e implementación de solución de hello descrita en este artículo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="8ee7b-125">Introducción al servicio Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="8ee7b-126">Creación de la primera canalización de datos</span><span class="sxs-lookup"><span data-stu-id="8ee7b-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="8ee7b-127">(opcional) toolearn más información acerca de la factoría de datos de Azure, vea hello [ruta de acceso de aprendizaje de factoría de datos de Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="8ee7b-128">Data Factory y Batch juntos</span><span class="sxs-lookup"><span data-stu-id="8ee7b-128">Data Factory and Batch together</span></span>
<span data-ttu-id="8ee7b-129">Factoría de datos incluye las actividades integradas como toocopy/mover datos de actividad de copia de un origen de datos de almacén de almacén de datos de destino tooa y los datos de tooprocess de actividad de Hive con clústeres de Hadoop (HDInsight) en Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="8ee7b-130">Consulte en este artículo la lista de [actividades de transformación de datos](data-factory-data-transformation-activities.md) admitidas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="8ee7b-131">También permite toocreate .NET actividades personalizadas toomove o procesen datos con su propia lógica y ejecutar estas actividades en un clúster de HDInsight de Azure o en un grupo de lote de Azure de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="8ee7b-132">Cuando usas Azure Batch, puede configurar grupo de hello tooauto-escala (Agregar o quitar máquinas virtuales en función de la carga de trabajo de hello) según una fórmula que proporcione.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="8ee7b-133">Arquitectura de la solución de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ee7b-133">Architecture of sample solution</span></span>
<span data-ttu-id="8ee7b-134">Aunque la arquitectura de Hola que se describe en este artículo es una solución simple, es escenarios de toocomplex relevante, como el modelado, servicios financieros, procesamiento de imágenes, representación y genómica análisis de riesgos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="8ee7b-135">diagrama de Hello muestra 1) cómo organiza la factoría de datos de movimiento de datos y el procesamiento y (2) cómo procesa el lote de Azure Hola datos de forma paralela.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="8ee7b-136">Descarga y diagrama de impresión Hola para facilitar su consulta (11 x 17 pulgadas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="8ee7b-137">o tamaño A3): [Orquestación de HPC y de datos mediante Azure Batch y Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="8ee7b-138">[![Diagrama de procesamiento de datos de gran escala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="8ee7b-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="8ee7b-139">Hello lista siguiente proporciona pasos básicos de hello del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="8ee7b-140">solución de Hello incluye código y explicaciones solución end-to-end de toobuild Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="8ee7b-141">**Configure Lote de Azure con un grupo de nodos de proceso (máquinas virtuales)**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="8ee7b-142">Puede especificar el número de Hola de nodos y el tamaño de cada nodo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="8ee7b-143">**Cree una instancia de Azure Data Factory** que esté configurada con entidades que representen Azure Blob Storage, el servicio de proceso Azure Batch, los datos de entrada y salida y un flujo de trabajo o una canalización con las actividades que mueven y transforman datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="8ee7b-144">**Crear una actividad personalizada de .NET en la canalización de factoría de datos de hello**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="8ee7b-145">actividad Hello es el código de usuario que se ejecuta en hello grupo de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="8ee7b-146">**Almacene grandes cantidades de datos de entrada como blobs en Almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="8ee7b-147">Los datos se dividen en segmentos lógicos (normalmente, en función de la fecha y la hora).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="8ee7b-148">**Factoría de datos de copia de datos que se procesan en paralelo** ubicación secundaria toohello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="8ee7b-149">**Factoría de datos ejecuta la actividad personalizada hello use el grupo de hello asignado por lote**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="8ee7b-150">Además, puede ejecutar actividades al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="8ee7b-151">Cada actividad procesa un segmento de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="8ee7b-152">Hola resultados se almacenan en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="8ee7b-153">**Factoría de datos mueve la tercera ubicación de hello resultados finales tooa**, ya sea para su distribución a través de una aplicación, o para su posterior procesamiento por otras herramientas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="8ee7b-154">Implementación de la solución de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ee7b-154">Implementation of sample solution</span></span>
<span data-ttu-id="8ee7b-155">solución de ejemplo de Hola es deliberadamente simple y es tooshow, cómo toouse factoría de datos y por lotes juntos tooprocess conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="8ee7b-156">solución de Hello simplemente cuenta el número de Hola de apariciones de un término de búsqueda ("Microsoft") en los archivos de entrada organizados en una serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="8ee7b-157">Genera archivos de toooutput de recuento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="8ee7b-158">**Tiempo**: si está familiarizado con conceptos básicos de Azure, la factoría de datos y el lote y tienen requisitos previos de hello completado indicadas a continuación, se estima que esta solución toma toocomplete 1 y 2 horas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8ee7b-159">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8ee7b-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="8ee7b-160">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-160">Azure subscription</span></span>
<span data-ttu-id="8ee7b-161">Si carece de suscripción de Azure, puede crear una cuenta de prueba gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8ee7b-162">Consulte [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="8ee7b-163">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-163">Azure storage account</span></span>
<span data-ttu-id="8ee7b-164">Usar una cuenta de almacenamiento de Azure para almacenar datos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="8ee7b-165">Si no dispone de una, consulte [Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="8ee7b-166">solución de ejemplo de Hola usa almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="8ee7b-167">Cuenta de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="8ee7b-167">Azure Batch account</span></span>
<span data-ttu-id="8ee7b-168">Crear una cuenta de Azure Batch mediante hello [portal de Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="8ee7b-169">Consulte [Creación y administración de una cuenta de Azure Batch en Azure Portal](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="8ee7b-170">Tenga en cuenta clave de nombre y la cuenta de la cuenta del lote de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="8ee7b-171">También puede usar [AzureRmBatchAccount New](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate una cuenta de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="8ee7b-172">Consulte [Introducción a los cmdlets de PowerShell para Azure Batch](../batch/batch-powershell-cmdlets-get-started.md) para obtener instrucciones detalladas para usar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="8ee7b-173">solución de ejemplo de Hola utiliza datos de tooprocess de lote de Azure (indirectamente a través de una canalización del generador de datos de Azure) de forma paralela en un grupo de nodos de cálculo (una colección administrada de máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="8ee7b-174">Grupo de máquinas virtuales (VM) de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="8ee7b-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="8ee7b-175">Cree un **grupo Azure Batch** con al menos 2 nodos de proceso.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="8ee7b-176">Hola [portal de Azure](https://portal.azure.com), haga clic en **examinar** en Hola menú izquierdo y haga clic en **las cuentas por lotes**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="8ee7b-177">Seleccione su hello tooopen de cuenta de Azure Batch **cuenta de lote** hoja.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="8ee7b-178">Haga clic en el icono **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="8ee7b-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="8ee7b-179">Hola **grupos** hoja, haga clic en el botón Agregar en la barra de herramientas de hello tooadd un grupo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="8ee7b-180">Escriba un Id. de grupo de hello (**Id. de grupo**).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="8ee7b-181">Hola Nota **Id. de grupo de hello**; necesita al crear soluciones de hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="8ee7b-182">Especifique **Windows Server 2012 R2** para configuración de la familia de sistemas operativos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="8ee7b-183">Seleccione un **plan de tarifa de nodos**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="8ee7b-184">Escriba **2** como valor de hello **destino dedicado** configuración.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="8ee7b-185">Escriba **2** como valor de hello **Max tareas por nodo** configuración.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="8ee7b-186">Haga clic en **Aceptar** grupo de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="8ee7b-187">Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8ee7b-187">Azure Storage Explorer</span></span>
<span data-ttu-id="8ee7b-188">[Explorador de Azure Storage 6 (herramienta)](https://azurestorageexplorer.codeplex.com/) o [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (de ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="8ee7b-189">Usar estas herramientas para inspeccionar y modificar datos de hello en los proyectos de almacenamiento de Azure, incluidos los registros de Hola de las aplicaciones hospedadas en la nube.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="8ee7b-190">Cree un contenedor denominado **mycontainer** con acceso privado (sin acceso anónimo).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="8ee7b-191">Si utilizas **CloudXplorer**, crear carpetas y subcarpetas con Hola siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="8ee7b-192">`Inputfolder` y `outputfolder` son carpetas de nivel superior en `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="8ee7b-193">Hola `inputfolder` tiene subcarpetas con marcas de fecha y hora (aaaa-MM-DD-HH).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="8ee7b-194">Si utilizas **Azure Storage Explorer**, en el paso siguiente de hello, necesita tooupload archivos con nombres: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="8ee7b-195">Este paso crea automáticamente carpetas Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="8ee7b-196">Crear un archivo de texto **file.txt** en su equipo con contenido con la palabra clave de hello **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="8ee7b-197">Por ejemplo: "test custom activity Microsoft test custom activity Microsoft".</span><span class="sxs-lookup"><span data-stu-id="8ee7b-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="8ee7b-198">Cargar Hola archivo toohello siguientes carpetas de entrada en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="8ee7b-199">Si utilizas **Azure Storage Explorer**, cargue el archivo hello **file.txt** demasiado**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="8ee7b-200">Haga clic en **copia** en la barra de herramientas de hello toocreate una copia de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="8ee7b-201">Hola **Copy Blob** cuadro de diálogo, cambio hello **nombre de blob de destino** demasiado`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="8ee7b-202">Repita este paso toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="8ee7b-203">Esta acción crea automáticamente carpetas Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="8ee7b-204">Cree otro contenedor denominado: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="8ee7b-205">Cargar el contenedor de toothis de archivos zip de hello actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="8ee7b-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8ee7b-206">Visual Studio</span></span>
<span data-ttu-id="8ee7b-207">Instalar Microsoft Visual Studio 2012 o posterior toocreate Hola personalizado lote actividad toobe usa Hola solución factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="8ee7b-208">Solución de pasos de alto nivel toocreate Hola</span><span class="sxs-lookup"><span data-stu-id="8ee7b-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="8ee7b-209">Crear una actividad personalizada que contiene la lógica de procesamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="8ee7b-210">Cree un generador de datos de Azure que utiliza la actividad personalizada hello:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="8ee7b-211">Crear actividad personalizada hello</span><span class="sxs-lookup"><span data-stu-id="8ee7b-211">Create hello custom activity</span></span>
<span data-ttu-id="8ee7b-212">Hola actividad personalizada de factoría de datos es la esencia de Hola de esta solución de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="8ee7b-213">solución de ejemplo de Hola usa la actividad personalizada hello toorun de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="8ee7b-214">Vea [utilizar actividades personalizadas en una canalización del generador de datos de Azure](data-factory-use-custom-activities.md) de actividades personalizadas de toodevelop de información básica de Hola y uso en Data Factory de Azure canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="8ee7b-215">toocreate una actividad personalizada .NET que puede usar en una canalización de factoría de datos de Azure, deberá toocreate un **biblioteca de clases .NET** proyecto con una clase que implementa que **IDotNetActivity** interfaz.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="8ee7b-216">Esta interfaz tiene un solo método, **Execute**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="8ee7b-217">Esta es la firma Hola del método hello:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="8ee7b-218">método Hello tiene unos componentes claves que necesita toounderstand.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="8ee7b-219">método Hello toma cuatro parámetros:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="8ee7b-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-220">**linkedServices**.</span></span> <span data-ttu-id="8ee7b-221">Lista enumerable de servicios vinculados que vinculan orígenes de datos de entrada/salida (por ejemplo: almacenamiento de blobs de Azure) toohello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="8ee7b-222">En este ejemplo, hay solo un servicio vinculado del tipo Azure Storage que se utilice como entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="8ee7b-223">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-223">**datasets**.</span></span> <span data-ttu-id="8ee7b-224">Se trata de una lista enumerable de conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="8ee7b-225">Puede usar este ubicaciones de parámetro tooget hello y esquemas definidos por los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="8ee7b-226">**activity**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-226">**activity**.</span></span> <span data-ttu-id="8ee7b-227">Este parámetro representa Hola proceso entidad actual - en este caso, un servicio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="8ee7b-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-228">**logger**.</span></span> <span data-ttu-id="8ee7b-229">permite del registrador de Hello para que escribir comentarios de depuración que superficie como Hola "Usuario" iniciar sesión Hola canalización.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="8ee7b-230">método Hello devuelve un diccionario que puede ser actividades personalizadas utilizadas toochain juntos en un futuro Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="8ee7b-231">Esta característica todavía no está implementada, por lo que devuelve un diccionario vacío de método hello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="8ee7b-232">Procedimiento: Crear la actividad personalizada hello</span><span class="sxs-lookup"><span data-stu-id="8ee7b-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="8ee7b-233">Cree un proyecto de biblioteca de clases .NET en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="8ee7b-234">Inicie **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="8ee7b-235">Haga clic en **archivo**, seleccione demasiado**New**y haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="8ee7b-236">Expanda **Plantillas** y seleccione **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="8ee7b-237">En este tutorial, utilice C\#, pero puede usar cualquier actividad personalizada .NET language toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="8ee7b-238">Seleccione **biblioteca de clases** de lista de Hola de tipos de proyecto en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="8ee7b-239">Escriba **MyDotNetActivity** para hello **nombre**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="8ee7b-240">Seleccione **C:\\ADF** para hello **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="8ee7b-241">Crear carpeta de hello **ADF** si no existe.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="8ee7b-242">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="8ee7b-243">Haga clic en **herramientas**, seleccione demasiado**Administrador de paquetes de NuGet**y haga clic en **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="8ee7b-244">Hola **Package Manager Console**, ejecutar Hola después comando tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="8ee7b-245">Hola de importación **el almacenamiento de Azure** paquetes de NuGet en los proyectos de toohello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="8ee7b-246">Este paquete es necesario porque usa la API de almacenamiento de blobs de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="8ee7b-247">Agregue los siguiente hello **con** archivo de código fuente de toohello de directivas en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="8ee7b-248">Cambiar el nombre del programa Hola Hola **espacio de nombres** demasiado**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="8ee7b-249">Cambiar nombre de Hola de clase hello demasiado**MyDotNetActivity** y derivan de hello **IDotNetActivity** interfaz tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="8ee7b-250">Hola implemente (Agregar) **Execute** método de hello **IDotNetActivity** interfaz toohello **MyDotNetActivity** Hola de clase y copia siguiendo el método de toohello de código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="8ee7b-251">Vea hello [Execute Method](#execute-method) sección para ver una explicación de lógica de hello utilizada en este método.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="8ee7b-252">Agregar Hola después de la clase de toohello de métodos de aplicación auxiliar.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="8ee7b-253">Estos métodos se invocan hello **Execute** método.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="8ee7b-254">Lo más importante, Hola **Calculate** método aísla el código de hello que recorre en iteración cada blob.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="8ee7b-255">Hola **GetFolderPath** método devuelve la carpeta de toohello de ruta de acceso de hello ese conjunto de datos de Hola puntos tooand Hola **GetFileName** método devuelve el nombre de Hola de Hola/archivo de blob que Hola conjunto de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="8ee7b-256">Hola **Calculate** método calcula el número de Hola de instancias de la palabra clave **Microsoft** en archivos de entrada de hello (BLOB en la carpeta de hello).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="8ee7b-257">término de búsqueda de Hello ("Microsoft") está codificado de forma rígida en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="8ee7b-258">Compile el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-258">Compile hello project.</span></span> <span data-ttu-id="8ee7b-259">Haga clic en **generar** desde el menú de Hola y haga clic en **generar solución**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="8ee7b-260">Iniciar **el Explorador de Windows**, del sistema y desplácese demasiado**bin\\depurar** o **bin\\versión** carpeta según el tipo de saludo de compilación.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="8ee7b-261">Crear un archivo zip **MyDotNetActivity.zip** que contiene todos los archivos binarios de Hola Hola  **\\bin\\depurar** carpeta.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="8ee7b-262">Puede que desee tooinclude hello MyDotNetActivity. **pdb** de archivos para que obtengan detalles adicionales, como el número de línea de código fuente de Hola que causó el problema de hello cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="8ee7b-263">Cargar **MyDotNetActivity.zip** como un contenedor de blobs de blob toohello: `customactivitycontainer` en hello Azure almacenamiento de blobs que hello **StorageLinkedService** servicio Hola vinculado  **ADFTutorialDataFactory** usa.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="8ee7b-264">Crear contenedor de blobs de hello `customactivitycontainer` si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="8ee7b-265">Método Execute</span><span class="sxs-lookup"><span data-stu-id="8ee7b-265">Execute method</span></span>
<span data-ttu-id="8ee7b-266">Esta sección proporciona más detalles y notas acerca del código de hello en hello método Execute.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="8ee7b-267">miembros de Hola para recorrer en iteración la colección de entrada de Hola se encuentran en hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="8ee7b-268">Recorrer en iteración la colección de blobs de hello requiere el uso de hello **BlobContinuationToken** clase.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="8ee7b-269">En esencia, debe usar un no-bucle con token de hello como mecanismo de Hola para salir Hola bucle while.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="8ee7b-270">Para obtener más información, consulte [cómo toouse almacenamiento de blobs en .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8ee7b-271">Aquí se muestra un bucle básico:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="8ee7b-272">Consulte la documentación de Hola para hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) método para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="8ee7b-273">Hello código para trabajar con el conjunto de Hola de blobs lógicamente entra dentro de hello hacer-bucle while.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="8ee7b-274">Hola **Execute** método, realice de hello-mientras el bucle pasa lista Hola de blobs con el nombre de método de tooa **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="8ee7b-275">método Hello devuelve una variable de cadena denominada **salida** que es resultado de hello de tener que se itera a través de todos los blobs de hello en el segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="8ee7b-276">Devuelve Hola número de repeticiones del término de búsqueda de hello (**Microsoft**) en el blob de hello pasa toohello **Calculate** método.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="8ee7b-277">Una vez Hola **Calculate** método ha realizado el trabajo de hello, debe escribirse tooa nuevo blob.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="8ee7b-278">Por lo que para cada conjunto de blobs que se procesa, se puede escribir un nuevo blob con resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="8ee7b-279">toowrite tooa nuevo blob, el primer conjunto de datos de salida de hello buscar.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="8ee7b-280">código de Hello también llama a un método auxiliar: **GetFolderPath** ruta de acceso de la carpeta de hello tooretrieve (nombre de contenedor de almacenamiento de hello).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="8ee7b-281">Hola **GetFolderPath** conversiones Hola tooan del objeto de conjunto de datos AzureBlobDataSet, que tiene una propiedad denominada FolderPath.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="8ee7b-282">Hola de llamadas de código de Hello **GetFileName** método tooretrieve Hola archivo nombre (blob).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="8ee7b-283">código de Hello es toohello similar por encima de la ruta de acceso de carpeta de código tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="8ee7b-284">nombre de Hello del archivo hello se escribe mediante la creación de un objeto URI.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="8ee7b-285">constructor URI de Hello utiliza hello **BlobEndpoint** nombre de contenedor de propiedad tooreturn Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="8ee7b-286">nombre de archivo y ruta de acceso de carpeta de Hola se agregan tooconstruct el URI del blob de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="8ee7b-287">se ha escrito el nombre de Hello del archivo hello y ahora puede escribir la cadena de salida de hello de hello **Calculate** tooa nuevo blob de método:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="8ee7b-288">Crear Hola factoría de datos</span><span class="sxs-lookup"><span data-stu-id="8ee7b-288">Create hello data factory</span></span>
<span data-ttu-id="8ee7b-289">Hola [Crear actividad personalizada hello](#create-the-custom-activity) sección, se crea una actividad personalizada y archivo zip de hello cargados con los archivos binarios y Hola PDB archivo tooan contenedor de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="8ee7b-290">En esta sección, creará un Azure **factoría de datos** con un **canalización** que usa hello **actividad personalizada**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="8ee7b-291">Hola conjunto de datos de entrada para la actividad personalizada hello representa blobs hello (archivos) en la carpeta de entrada de hello (`mycontainer\\inputfolder`) en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="8ee7b-292">conjunto de datos de salida de Hello para la actividad hello representa blobs de salida de hello en la carpeta de salida de hello (`mycontainer\\outputfolder`) en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="8ee7b-293">Quitar uno o varios archivos en carpetas de entrada de hello:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="8ee7b-294">Por ejemplo, colocar un archivo (file.txt) con hello siguen contenido en cada una de las carpetas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="8ee7b-295">Cada carpeta de entrada corresponde tooa segmento de factoría de datos de Azure, incluso si la carpeta de hello tiene 2 o más archivos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="8ee7b-296">Cuando se procesa cada segmento de canalización de hello, la actividad personalizada hello recorre en iteración todos los blobs de hello en la carpeta de entrada de Hola para dicho sector.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="8ee7b-297">Verá cinco archivos de salida con hello mismo contenido.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-297">You see five output files with hello same content.</span></span> <span data-ttu-id="8ee7b-298">Por ejemplo, el archivo de salida de hello de procesar el archivo de hello en la carpeta de hello 2015-11-16: 00 tiene Hola siguen contenido:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="8ee7b-299">Si quita varios archivos (file.txt, archivo2.txt, archivo3.txt) con hello mismo contenido toohello carpeta de entrada, vea Hola siguen contenido en el archivo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="8ee7b-300">Cada carpeta (2015-11-16: 00, etc.) corresponde segmento tooa en este ejemplo, incluso si la carpeta de hello tiene varios archivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="8ee7b-301">archivo de salida de Hello tiene tres líneas ahora, uno para cada archivo de entrada (blob) en la carpeta de hello asociada con el segmento de hello (2015-11-16: 00).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="8ee7b-302">Se crea una tarea para cada ejecución de actividad.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-302">A task is created for each activity run.</span></span> <span data-ttu-id="8ee7b-303">En este ejemplo, hay sólo una actividad en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="8ee7b-304">Cuando se procesa un segmento de canalización de hello, actividad personalizada hello se ejecuta en el segmento de lote de Azure tooprocess Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="8ee7b-305">Puesto que hay 5 segmentos (cada segmento puede tener varios blobs o archivos), se crearán 5 tareas en Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="8ee7b-306">Cuando una tarea se ejecuta en proceso por lotes, es realmente Hola actividad personalizada que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="8ee7b-307">Hola tutorial proporciona detalles adicionales.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="8ee7b-308">Paso 1: Crear la factoría de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="8ee7b-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="8ee7b-309">Después de iniciar sesión toohello [portal de Azure](https://portal.azure.com/), Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="8ee7b-310">Haga clic en **NEW** en el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="8ee7b-311">Haga clic en **datos + análisis** en hello **New** hoja.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="8ee7b-312">Haga clic en **factoría de datos** en hello **análisis de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="8ee7b-313">Hola **factoría de datos** hoja, escriba **CustomActivityFactory** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="8ee7b-314">nombre de Hola Hola Azure factoría de datos debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="8ee7b-315">Si recibe el error hello: **nombre de generador de datos "CustomActivityFactory" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, **yournameCustomActivityFactory**) y pruebe a crear volver a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="8ee7b-316">Haga clic en **NOMBRE DEL GRUPO DE RECURSOS**y seleccione un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="8ee7b-317">Compruebe que está usando la suscripción correcta de Hola y la región donde desea Hola datos generador toobe creado.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="8ee7b-318">Haga clic en **crear** en hello **factoría de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="8ee7b-319">Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="8ee7b-320">Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="8ee7b-321">Paso 2: Creación de servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="8ee7b-321">Step 2: Create linked services</span></span>
<span data-ttu-id="8ee7b-322">Servicios vinculados vinculan almacenes de datos o generador de datos de Azure de tooan de servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="8ee7b-323">En este paso, se vinculan los **el almacenamiento de Azure** cuenta y **Azure Batch** factoría de datos de cuenta tooyour.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="8ee7b-324">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="8ee7b-325">Haga clic en hello **autor e implementar** icono hello **factoría de datos** hoja para **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="8ee7b-326">Vea Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="8ee7b-327">Haga clic en **nuevo almacén de datos** en Hola barra de comandos y elija **almacenamiento de Azure.**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="8ee7b-328">Debería ver Hola script JSON para crear un almacenamiento de Azure vinculada servicio en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="8ee7b-329">Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de almacenamiento de Azure y **clave de cuenta** por clave de acceso de Hola de hello cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="8ee7b-330">toolearn cómo tooget el almacenamiento de tener acceso a clave, consulte [ver, copiar y regenerar almacenamiento de claves de acceso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="8ee7b-331">Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="8ee7b-332">Creación del servicio vinculado de Lote de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="8ee7b-333">En este paso, creará un servicio vinculado para su **Azure Batch** cuenta de actividad personalizado de toorun usado hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="8ee7b-334">Haga clic en **nuevo proceso** en Hola barra de comandos y elija **lote de Azure.**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="8ee7b-335">Debería ver Hola script JSON para la creación de un lote de Azure vinculada servicio en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="8ee7b-336">Hola script JSON:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="8ee7b-337">Reemplace **nombre de la cuenta** con nombre de saludo de la cuenta de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="8ee7b-338">Reemplace **clave de acceso** por clave de acceso de Hola de hello cuenta de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="8ee7b-339">Escriba Hola identificador de grupo de Hola para hello **poolName** propiedad**.**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="8ee7b-340">Para esta propiedad, puede especificar cualquier nombre de grupo o id. de bloque.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="8ee7b-341">Especificar por lotes de hello URI para hello **batchUri** propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="8ee7b-342">Hola **URL** de hello **hoja de la cuenta de Azure Batch** en hello siguiendo el formato: \<accountname\>.\< región\>. batch.azure.com. Para hello **batchUri** propiedad Hola JSON, necesita demasiado**quitar "accountname."**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="8ee7b-343">desde la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-343">from hello URL.</span></span> <span data-ttu-id="8ee7b-344">Ejemplo: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="8ee7b-345">Para hello **poolName** propiedad, también puede especificar el identificador de hello del grupo de hello en lugar del nombre de Hola de grupo de Hola de.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8ee7b-346">Hola servicio factoría de datos no admite una opción de petición para el lote de Azure que lo hace para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="8ee7b-347">Solo puede usar su propio grupo de Lote de Azure en una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="8ee7b-348">Especifique **StorageLinkedService** para hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="8ee7b-349">Crea este servicio vinculado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="8ee7b-350">Este almacenamiento se usa como área de almacenamiento provisional para archivos y registros.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="8ee7b-351">Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="8ee7b-352">Paso 3: Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="8ee7b-352">Step 3: Create datasets</span></span>
<span data-ttu-id="8ee7b-353">En este paso, creará entrada toorepresent de conjuntos de datos y los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="8ee7b-354">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="8ee7b-354">Create input dataset</span></span>
1. <span data-ttu-id="8ee7b-355">Hola **Editor** para hello factoría de datos, haga clic en **nuevo conjunto de datos** los botones de barra de herramientas de Hola y haga clic en **almacenamiento de blobs de Azure** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="8ee7b-356">Reemplace Hola JSON en el panel derecho de hello con hello siguiente fragmento de JSON:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="8ee7b-357">Más adelante, en este mismo tutorial, creará una canalización cuya hora de finalización es 2015-11-16T00:00:00Z, y cuya hora de finalización es 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="8ee7b-358">Se trata de datos programada tooproduce **cada hora**, por lo que hay 5 segmentos de entrada/salida (entre **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="8ee7b-359">Hola **frecuencia** y **intervalo** de conjunto de datos de entrada de Hola se establece demasiado**hora** y **1**, lo que significa que Hola entrada segmento está disponible cada hora.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="8ee7b-360">Estos son los tiempos de inicio de Hola para cada segmento, que se representan mediante **SliceStart** variable del sistema en hello por encima del fragmento de JSON.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="8ee7b-361">**Segmento**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-361">**Slice**</span></span> | <span data-ttu-id="8ee7b-362">**Hora de inicio**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="8ee7b-363">1</span><span class="sxs-lookup"><span data-stu-id="8ee7b-363">1</span></span>         | <span data-ttu-id="8ee7b-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="8ee7b-365">2</span><span class="sxs-lookup"><span data-stu-id="8ee7b-365">2</span></span>         | <span data-ttu-id="8ee7b-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="8ee7b-367">3</span><span class="sxs-lookup"><span data-stu-id="8ee7b-367">3</span></span>         | <span data-ttu-id="8ee7b-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="8ee7b-369">4</span><span class="sxs-lookup"><span data-stu-id="8ee7b-369">4</span></span>         | <span data-ttu-id="8ee7b-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="8ee7b-371">5</span><span class="sxs-lookup"><span data-stu-id="8ee7b-371">5</span></span>         | <span data-ttu-id="8ee7b-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="8ee7b-373">Hola **folderPath** se calcula mediante el uso de la parte de año, mes, día y hora de Hola de hora de inicio del segmento de hello (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="8ee7b-374">Por lo tanto, mostramos cómo una carpeta de entrada es el intervalo de tooa asignado.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="8ee7b-375">**Segmento**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-375">**Slice**</span></span> | <span data-ttu-id="8ee7b-376">**Hora de inicio**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-376">**Start time**</span></span>          | <span data-ttu-id="8ee7b-377">**Carpeta de entrada**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="8ee7b-378">1</span><span class="sxs-lookup"><span data-stu-id="8ee7b-378">1</span></span>         | <span data-ttu-id="8ee7b-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="8ee7b-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="8ee7b-381">2</span><span class="sxs-lookup"><span data-stu-id="8ee7b-381">2</span></span>         | <span data-ttu-id="8ee7b-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="8ee7b-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="8ee7b-384">3</span><span class="sxs-lookup"><span data-stu-id="8ee7b-384">3</span></span>         | <span data-ttu-id="8ee7b-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="8ee7b-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="8ee7b-387">4</span><span class="sxs-lookup"><span data-stu-id="8ee7b-387">4</span></span>         | <span data-ttu-id="8ee7b-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="8ee7b-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="8ee7b-390">5</span><span class="sxs-lookup"><span data-stu-id="8ee7b-390">5</span></span>         | <span data-ttu-id="8ee7b-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="8ee7b-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="8ee7b-393">Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **InputDataset** tabla.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="8ee7b-394">Creación del conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="8ee7b-394">Create output dataset</span></span>
<span data-ttu-id="8ee7b-395">En este paso, creará otro conjunto de datos de tipo de datos de salida de AzureBlob toorepresent Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="8ee7b-396">Hola **Editor** para hello factoría de datos, haga clic en **nuevo conjunto de datos** los botones de barra de herramientas de Hola y haga clic en **almacenamiento de blobs de Azure** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="8ee7b-397">Reemplace Hola JSON en el panel derecho de hello con hello siguiente fragmento de JSON:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="8ee7b-398">Se genera un blob o archivo de salida para cada segmento de entrada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="8ee7b-399">Así es cómo se asigna el nombre al archivo de salida de cada segmento.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="8ee7b-400">Todos los archivos de salida de hello se generan en una carpeta de salida: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="8ee7b-401">**Segmento**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-401">**Slice**</span></span> | <span data-ttu-id="8ee7b-402">**Hora de inicio**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-402">**Start time**</span></span>          | <span data-ttu-id="8ee7b-403">**Archivo de salida**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="8ee7b-404">1</span><span class="sxs-lookup"><span data-stu-id="8ee7b-404">1</span></span>         | <span data-ttu-id="8ee7b-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="8ee7b-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="8ee7b-407">2</span><span class="sxs-lookup"><span data-stu-id="8ee7b-407">2</span></span>         | <span data-ttu-id="8ee7b-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="8ee7b-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="8ee7b-410">3</span><span class="sxs-lookup"><span data-stu-id="8ee7b-410">3</span></span>         | <span data-ttu-id="8ee7b-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="8ee7b-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="8ee7b-413">4</span><span class="sxs-lookup"><span data-stu-id="8ee7b-413">4</span></span>         | <span data-ttu-id="8ee7b-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="8ee7b-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="8ee7b-416">5</span><span class="sxs-lookup"><span data-stu-id="8ee7b-416">5</span></span>         | <span data-ttu-id="8ee7b-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="8ee7b-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="8ee7b-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="8ee7b-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="8ee7b-419">Recuerde que Hola a todos los archivos en una carpeta de entrada (por ejemplo: 2015-11-16: 00) forman parte de un segmento con la hora de inicio de hello: 2015-11-16: 00.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="8ee7b-420">Cuando se procesa este segmento, actividad personalizada hello recorre cada archivo y genera una línea en el archivo de salida de hello con número de Hola de repeticiones del término de búsqueda ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="8ee7b-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="8ee7b-421">Si hay tres archivos en la carpeta de hello 2015-11-16: 00, hay tres líneas en el archivo de salida de hello: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="8ee7b-422">Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="8ee7b-423">Paso 4: Crear y ejecutar canalización Hola con actividades personalizadas</span><span class="sxs-lookup"><span data-stu-id="8ee7b-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="8ee7b-424">En este paso, creará una canalización con una actividad de la actividad personalizada hello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ee7b-425">Si no ha cargado hello **file.txt** tooinput carpetas en el contenedor de blobs de hello, hacerlo antes de crear la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="8ee7b-426">Hola **isPaused** propiedad se establece toofalse en canalización Hola JSON, por lo que la canalización Hola se ejecuta inmediatamente como Hola **iniciar** fecha es Hola anteriores.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="8ee7b-427">Hola Editor de generador de datos, haga clic en **nueva canalización** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="8ee7b-428">Si no ve el comando hello, haga clic en **... (Puntos suspensivos)**  toosee se.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="8ee7b-429">Reemplace Hola JSON en el panel derecho de hello con hello siguiente secuencia de comandos JSON:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="8ee7b-430">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-430">Note hello following points:</span></span>

   * <span data-ttu-id="8ee7b-431">Hay sólo una actividad en la canalización de Hola y que es de tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="8ee7b-432">**AssemblyName** se establece el nombre toohello de hello DLL: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="8ee7b-433">**Punto de entrada** se establece demasiado**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="8ee7b-434">Es básicamente \<espacioDeNombres\>.\<nombreDeClase\> en el código.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="8ee7b-435">**PackageLinkedService** se establece demasiado**StorageLinkedService** que señala el almacenamiento de blobs de toohello que contiene el archivo zip de hello actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="8ee7b-436">Si usas cuentas de almacenamiento de Azure diferentes para los archivos de entrada/salida y el archivo zip de actividad personalizada de hello, tienen toocreate almacenamiento de Azure de otro servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="8ee7b-437">En este artículo se da por supuesto que está usando Hola la misma cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="8ee7b-438">**PackageFile** se establece demasiado**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="8ee7b-439">Se encuentra en formato de hello: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="8ee7b-440">toma la actividad personalizada Hello **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="8ee7b-441">Hola **linkedServiceName** propiedad de actividad personalizada hello señala toohello **AzureBatchLinkedService**, lo que indica a Data Factory de Azure esa actividad personalizada hello necesita toorun en lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="8ee7b-442">Hola **simultaneidad** configuración es importante.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="8ee7b-443">Si utiliza el valor predeterminado de hello, que es 1, incluso si tiene 2 o más nodos de cálculo en grupo de lote de Azure de hello, segmentos de Hola se procesan uno tras otro.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="8ee7b-444">Por lo tanto, no se sacar partido de la capacidad de procesamiento en paralelo de Hola de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="8ee7b-445">Si establece **simultaneidad** tooa mayor valor, digamos 2, significa que dos segmentan (corresponde tootwo tareas en el lote de Azure) pueden ser procesados en hello mismo tiempo, en cuyo caso, ambas máquinas virtuales de Hola Hola se utilizan el grupo de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="8ee7b-446">Por consiguiente, establecer propiedad de simultaneidad de hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="8ee7b-447">De manera predeterminada, solo se ejecuta una tarea (segmento) en una máquina virtual en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="8ee7b-448">Hello motivo es que, de forma predeterminada, hello **tareas máxima por máquina virtual** se establece too1 para un grupo de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="8ee7b-449">Como parte de los requisitos previos, creó un grupo con este too2 de conjunto de propiedades, por lo que dos segmentos de la factoría de datos se pueden ejecutar en una máquina virtual en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="8ee7b-450">**isPaused** propiedad se establece toofalse de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="8ee7b-451">canalización de Hola se ejecuta inmediatamente en este ejemplo porque se inician los segmentos de Hola Hola anteriores.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="8ee7b-452">Puede establecer esta canalización de Hola de propiedad tootrue toopause y establecer toorestart toofalse atrás.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="8ee7b-453">Hola **iniciar** tiempo y **final** tiempos son cinco horas separadas y segmentos se producen cada hora, por lo que cinco segmentos son generadas por la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="8ee7b-454">Haga clic en **implementar** en la canalización de hello toodeploy la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="8ee7b-455">Paso 5: Probar la canalización de Hola</span><span class="sxs-lookup"><span data-stu-id="8ee7b-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="8ee7b-456">En este paso, para probar la canalización de hello, al colocar los archivos en carpetas de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="8ee7b-457">Comenzaremos con la canalización de hello pruebas con un archivo por una carpeta de entrada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="8ee7b-458">En la hoja de la factoría de datos de Hola Hola portal de Azure, haga clic en **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="8ee7b-459">En la vista de diagrama de hello, haga doble clic en el conjunto de datos de entrada: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="8ee7b-460">Debería ver Hola **InputDataset** hoja con todas las cinco segmentos de lista.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="8ee7b-461">Hola aviso **hora de inicio del segmento** y **hora de finalización de segmento** para cada sector.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="8ee7b-462">Hola **vista de diagrama**, haga clic en **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="8ee7b-463">Debería ver que los sectores de salida cinco Hola están en estado listo de hello si ya se han producido.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="8ee7b-464">Hola tooview portal Azure de uso **tareas** asociados con hello **sectores** y vea qué VM cada sector se ejecutó en.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="8ee7b-465">Para obtener más información, consulte la sección [Integración de Data Factory y Batch](#data-factory-and-batch-integration) .</span><span class="sxs-lookup"><span data-stu-id="8ee7b-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="8ee7b-466">Debería ver los archivos de salida de hello de hello `outputfolder` de `mycontainer` almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="8ee7b-467">Debería ver cinco archivos de salida, uno para cada segmento de entrada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="8ee7b-468">Cada uno de hello salida archivo debe tener contenido toohello similar después de salida:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="8ee7b-469">Hello diagrama siguiente ilustra cómo asignan los segmentos de la factoría de datos de hello tootasks en el lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="8ee7b-470">En este ejemplo, un segmento tiene solo una ejecución.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="8ee7b-471">Ahora, probemos con varios archivos en una carpeta.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="8ee7b-472">Crear archivos: **file2.txt**, **archivo3.txt**, **file4.txt**, y **file5.txt** con hello en el mismo contenido como en file.txt en carpeta hello: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="8ee7b-473">En la carpeta de salida de hello, **eliminar** archivo de salida de hello: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="8ee7b-474">Ahora, en hello **OutputDataset** hoja, segmento de hello contextual con **hora de inicio del segmento** establecido demasiado**16/11/2015 01:00:00 AM**y haga clic en **ejecutar**segmento hello toorerun/volver-process.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="8ee7b-475">Ahora, el segmento de hello tiene cinco archivos en lugar de un archivo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="8ee7b-476">Una vez ejecutada de segmento de Hola y su estado es **listo**, comprobar que el contenido de hello en archivo de salida de hello para este segmento (**2015-11-16-01.txt**) en hello `outputfolder` de `mycontainer` en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="8ee7b-477">Debería haber una línea para cada archivo de sector de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="8ee7b-478">Si no se eliminara Hola salida archivo 2015-11-16-01.txt antes de intentar con cinco archivos de entrada, verá una línea de segmento anterior Hola ejecutar y cinco líneas de segmento actual Hola ejecutar.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="8ee7b-479">De forma predeterminada, contenido de hello es toooutput anexado archivo si ya existe.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="8ee7b-480">Integración de Data Factory y Lote</span><span class="sxs-lookup"><span data-stu-id="8ee7b-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="8ee7b-481">Hola servicio factoría de datos crea un trabajo de lote de Azure con el nombre de hello: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Data Factory de Azure: trabajos por lotes](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="8ee7b-483">Se crea una tarea en el trabajo de Hola para cada ejecución de la actividad de un segmento.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="8ee7b-484">Si hay 10 toobe lista de segmentos procesados, 10 tareas se crean en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="8ee7b-485">Puede tener más de un sector que se ejecuta en paralelo si dispone de varios nodos de proceso en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="8ee7b-486">Si las tareas máximo de Hola por calculan nodo está establecido demasiado > 1, puede haber más de una división quedando Hola mismo proceso.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="8ee7b-487">En este ejemplo, hay 5 segmentos y, por tanto, 5 tareas en Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="8ee7b-488">Con hello **simultaneidad** establecido demasiado**5** Hola de canalización JSON de factoría de datos de Azure y **tareas máxima por máquina virtual** establecido demasiado**2** en Azure Batch bloque con **2** máquinas virtuales, Hola tareas se ejecuta rápida (compruebe las horas de inicio y finalización para las tareas).</span><span class="sxs-lookup"><span data-stu-id="8ee7b-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="8ee7b-489">Utilice el proceso por lotes de hello tooview portal hello y sus tareas asociadas con hello **sectores** y vea qué VM cada sector se ejecutó en.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Data Factory de Azure: tareas de trabajos por lotes](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="8ee7b-491">Depurar Hola canalización</span><span class="sxs-lookup"><span data-stu-id="8ee7b-491">Debug hello pipeline</span></span>
<span data-ttu-id="8ee7b-492">La depuración se compone de varias técnicas básicas:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="8ee7b-493">Si no se establece demasiado el segmento de entrada de hello**listo**, confirme que es correcta la estructura de carpetas de entrada de Hola y file.txt existe en las carpetas de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="8ee7b-494">Hola **Execute** método de la actividad personalizada, utilice hello **IActivityLogger** información sobre los objetos toolog que le ayude a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="8ee7b-495">mensajes de saludo registrado aparecen en usuario hello\_archivo de registro de 0.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="8ee7b-496">Hola **OutputDataset** hoja, haga clic en Hola segmento toosee Hola **el segmento de datos** hoja para dicho sector.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="8ee7b-497">Verá **ejecuciones de actividad** para ese segmento.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="8ee7b-498">Debería ver una actividad ejecutar para el intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="8ee7b-499">Si hace clic en **ejecutar** en la barra de comandos de hello, puede iniciar otra actividad ejecutar para hello mismo segmento.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="8ee7b-500">Al hacer clic en la ejecución de la actividad de hello, vea hello **detalles de ejecución de la actividad** hoja con una lista de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="8ee7b-501">Vea los mensajes registrados en hello **usuario\_registro 0** archivo.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="8ee7b-502">Cuando se produce un error, verá tres ejecuciones de actividad porque Hola de reintentos se establece too3 en hello canalización/JSON de la actividad.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="8ee7b-503">Al hacer clic en la ejecución de la actividad de hello, consulte los archivos de registro de hello que se puede revisar el error de hello tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="8ee7b-504">Hola lista de archivos de registro, haga clic en hello **0.log usuario**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="8ee7b-505">En el panel derecho de Hola se muestran resultados de hello del uso de hello **IActivityLogger.Write** método.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="8ee7b-506">Compruebe system-0.log para ver si hay alguna excepción o mensaje de error del sistema.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="8ee7b-507">Incluir hello **PDB** de archivos en el archivo zip de Hola para que los detalles del error Hola tienen información como **pila de llamadas** cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="8ee7b-508">Todos los Hola archivos en el archivo zip de hello para la actividad personalizada hello debe estar en hello **nivel superior** sin subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="8ee7b-509">Asegúrese de que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), y **packageLinkedService** (debe Azure toohello de punto de almacenamiento de blobs que contiene el archivo zip de Hola) se establecen valores de toocorrect.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="8ee7b-510">Si corrige un segmento de hello tooreprocess error y quiere, haga clic en segmento Hola Hola **OutputDataset** hoja y haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="8ee7b-511">Verá un **contenedor** en la instancia de Azure Blob Storage denominado: `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="8ee7b-512">Este contenedor no se elimina automáticamente, pero puede eliminarla con seguridad una vez que haya solución Hola pruebas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="8ee7b-513">De forma similar, Hola solución factoría de datos crea un lote de Azure **trabajo** denominado: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="8ee7b-514">Puede eliminar este trabajo después de probar soluciones de hello si lo desea.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="8ee7b-515">actividad personalizada Hello no utiliza hello **app.config** archivo desde el paquete.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="8ee7b-516">Por lo tanto, si el código lee las cadenas de conexión del archivo de configuración de hello, no funciona en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="8ee7b-517">Hola se recomienda una vez con Azure Batch toohold los secretos en un **KeyVault Azure**, use un keyvault de hello tooprotect principal de servicio basada en certificados y distribuir el grupo de lote de hello certificado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="8ee7b-518">Hola actividad personalizada. NET, a continuación, puede tener acceso a los secretos de hello KeyVault en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="8ee7b-519">Esta solución es un genérico y puede escalarse tooany tipo de secreto, no solo la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="8ee7b-520">Hay una solución más fácil (pero no es una práctica recomendada): puede crear un **servicio vinculado de SQL Azure** con valores de cadena de conexión, cree un conjunto de datos que usa Hola servicios vinculados y conjunto de datos de cadena Hola como un conjunto de datos de entrada ficticio toohello la actividad personalizada. NET.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="8ee7b-521">También puede, a continuación, Hola de acceso vinculado cadena de conexión del servicio en el código de actividad personalizada hello y debe funcionar bien en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="8ee7b-522">Ampliar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="8ee7b-522">Extend hello sample</span></span>
<span data-ttu-id="8ee7b-523">Puede extender este ejemplo toolearn más información sobre las características de Data Factory de Azure y Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="8ee7b-524">Por ejemplo, sectores tooprocess en un intervalo de tiempo diferente, Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="8ee7b-525">Agregar Hola siguiendo las subcarpetas de Hola `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 09-2015-11-16 y coloque los archivos de entrada en esas carpetas.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="8ee7b-526">Cambiar la hora de finalización de Hola de canalización de Hola desde `2015-11-16T05:00:00Z` demasiado`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="8ee7b-527">Hola **vista de diagrama**, haga doble clic en hello **InputDataset**y confirme que los segmentos de entrada de hello están listos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="8ee7b-528">Haga doble clic en **OuptutDataset** toosee estado de saludo de los sectores de salida.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="8ee7b-529">Si se encuentran en estado listo, compruebe la carpeta de salida de hello de archivos de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="8ee7b-530">Aumentar o disminuir hello **simultaneidad** configuración toounderstand cómo afecta al rendimiento de saludo de la solución, especialmente Hola de procesamiento que se produce en el lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="8ee7b-531">(Vea el paso 4: crear y ejecutar la canalización de Hola para obtener más información sobre hello **simultaneidad** configuración.)</span><span class="sxs-lookup"><span data-stu-id="8ee7b-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="8ee7b-532">Cree un grupo con un valor mayor o menor en **Máximo de tareas por máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="8ee7b-533">toouse Hola nuevo grupo creado, Hola de actualización de servicio vinculado Azure Batch en soluciones de hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="8ee7b-534">(Vea el paso 4: crear y ejecutar la canalización de Hola para obtener más información sobre hello **tareas máxima por máquina virtual** configuración.)</span><span class="sxs-lookup"><span data-stu-id="8ee7b-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="8ee7b-535">Cree un grupo de Azure Batch con la característica de **escalado automático** .</span><span class="sxs-lookup"><span data-stu-id="8ee7b-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="8ee7b-536">El escalado automático de nodos de proceso en un grupo de lote de Azure es realizar un ajuste dinámico Hola de procesamiento de la potencia utilizada por la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="8ee7b-537">fórmula de ejemplo de Hola aquí logra Hola siguiente comportamiento: cuando inicialmente se crea el grupo de hello, empieza por 1 máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="8ee7b-538">Métrica de $PendingTasks define el número de Hola de tareas en ejecución + activo (en cola) estado.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="8ee7b-539">fórmula de Hello busca Hola promedio de las tareas pendientes de hello últimos 180 segundos y establece el valor de TargetDedicated en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="8ee7b-540">Garantiza que TargetDedicated nunca supera las 25 VM.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="8ee7b-541">Por lo tanto, tal y como se envían las nuevas tareas, grupo crece automáticamente y como tareas se completan, las máquinas virtuales, se convierten en uno por uno libre y escalado automático de hello disminuye esas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="8ee7b-542">startingNumberOfVMs y maxNumberofVMs pueden ser necesidades tooyour ajustada.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="8ee7b-543">Fórmula de escalado automático:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="8ee7b-544">Para más información, consulte [Escalado automático de los nodos de proceso en un grupo de Lote de Azure](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="8ee7b-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="8ee7b-545">Si grupo hello usa predeterminado hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Hola servicio por lotes puede tardar 15 a 30 minutos tooprepare Hola VM antes de ejecutar la actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="8ee7b-546">Si el grupo de hello está usando un autoScaleEvaluationInterval diferente, podría tardar Hola servicio por lotes autoScaleEvaluationInterval + 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="8ee7b-547">En la solución de ejemplo de Hola Hola **Execute** método invoca hello **Calculate** método que procesa una tooproduce de segmento de datos de entrada un segmento de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="8ee7b-548">Puede escribir su propio método tooprocess los datos de entrada y reemplace la llamada al método Calculate de hello en el método Execute de hello con un método de llamada tooyour.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="8ee7b-549">Pasos siguientes: consumir datos Hola</span><span class="sxs-lookup"><span data-stu-id="8ee7b-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="8ee7b-550">Después de procesar datos, puede consumirlos con herramientas en línea como **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="8ee7b-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="8ee7b-551">Estos son toohelp vínculos entender Power BI y cómo toouse en Azure:</span><span class="sxs-lookup"><span data-stu-id="8ee7b-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="8ee7b-552">Exploración de un conjunto de datos en Power BI</span><span class="sxs-lookup"><span data-stu-id="8ee7b-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="8ee7b-553">Introducción a Hola Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="8ee7b-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="8ee7b-554">Actualizar datos en Power BI</span><span class="sxs-lookup"><span data-stu-id="8ee7b-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="8ee7b-555">Azure y Power BI</span><span class="sxs-lookup"><span data-stu-id="8ee7b-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="8ee7b-556">Referencias</span><span class="sxs-lookup"><span data-stu-id="8ee7b-556">References</span></span>
* [<span data-ttu-id="8ee7b-557">Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="8ee7b-558">Introducción tooAzure servicio de factoría de datos</span><span class="sxs-lookup"><span data-stu-id="8ee7b-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="8ee7b-559">Introducción a Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8ee7b-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="8ee7b-560">Uso de actividades personalizadas en una canalización de Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="8ee7b-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="8ee7b-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="8ee7b-562">Datos básicos de Lote de Batch</span><span class="sxs-lookup"><span data-stu-id="8ee7b-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="8ee7b-563">Información general de las características de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="8ee7b-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="8ee7b-564">Crear y administrar la cuenta de Azure Batch en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8ee7b-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="8ee7b-565">Introducción a la biblioteca de Lote de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="8ee7b-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
