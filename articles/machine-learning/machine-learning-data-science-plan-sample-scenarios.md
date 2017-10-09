---
title: "aaaIdentify avanzada escenarios de análisis para el aprendizaje automático de Azure | Documentos de Microsoft"
description: "Seleccione escenarios adecuados de Hola para hacerlo avanzado análisis predictivos con hello proceso de ciencia de datos de equipo."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="05e3c-103">Escenarios para análisis avanzado en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="05e3c-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="05e3c-104">En este artículo se describe diversas Hola de orígenes de datos de ejemplo y escenarios de destino que pueden ser controlados por hello [proceso de ciencia de datos de equipo (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05e3c-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="05e3c-105">Hola TDSP proporciona un enfoque sistemático para toocollaborate de los equipos en la creación de aplicaciones inteligentes.</span><span class="sxs-lookup"><span data-stu-id="05e3c-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="05e3c-106">escenarios de Hello proporcionados en esta guía ilustran opciones disponibles en el flujo de trabajo de procesamiento de datos de Hola que dependen de las características de datos de hello, ubicaciones de origen y destino repositorios en Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="05e3c-107">Hola **árbol de decisión** para escenarios de ejemplo de Hola que sea adecuada para los datos y el objetivo de selección se presenta en la última sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="05e3c-108">Cada una de las siguientes secciones de hello presenta un escenario de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="05e3c-109">Para cada escenario, se enumera un posible flujo de ciencia de datos y análisis avanzado, así como los recursos de compatibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="05e3c-110">**Para todos los escenarios siguientes de hello, necesitará:**
> </span><span class="sxs-lookup"><span data-stu-id="05e3c-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="05e3c-111">[Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="05e3c-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="05e3c-112">Creación de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="05e3c-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="05e3c-113"><a name="smalllocal"></a>Escenario \#1: toomedium pequeño conjunto de datos tabular en un archivos locales</span><span class="sxs-lookup"><span data-stu-id="05e3c-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![Archivos locales toomedium pequeño][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="05e3c-115">Recursos adicionales de Azure: ninguno</span><span class="sxs-lookup"><span data-stu-id="05e3c-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="05e3c-116">Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="05e3c-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="05e3c-117">Cargue un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-117">Upload a dataset.</span></span>
3. <span data-ttu-id="05e3c-118">Cree un flujo de experimento de Aprendizaje automático de Azure comenzando con conjuntos de datos cargados.</span><span class="sxs-lookup"><span data-stu-id="05e3c-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="05e3c-119"><a name="smalllocalprocess"></a>Escenario \#2: toomedium pequeño conjunto de datos de los archivos locales que requieren un procesamiento</span><span class="sxs-lookup"><span data-stu-id="05e3c-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![Toomedium pequeños archivos locales con el procesamiento][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="05e3c-121">Recursos adicionales de Azure: Máquina virtual de Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="05e3c-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="05e3c-122">Cree una máquina virtual de Azure que ejecute IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="05e3c-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="05e3c-123">Cargar el contenedor de almacenamiento de Azure de tooan de datos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="05e3c-124">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde el contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="05e3c-125">Transformar datos toocleaned, un formato tabular.</span><span class="sxs-lookup"><span data-stu-id="05e3c-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="05e3c-126">Guarde los datos transformados en blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="05e3c-127">Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="05e3c-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="05e3c-128">Leer datos de Hola de blobs de Azure mediante hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="05e3c-129">Cree un flujo de experimento de Aprendizaje automático de Azure comenzando con conjuntos de datos introducidos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="05e3c-130"><a name="largelocal"></a>Escenario \#3: Conjunto de datos grande de archivos locales, con blobs de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="05e3c-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Archivos locales grandes][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="05e3c-132">Recursos adicionales de Azure: Máquina virtual de Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="05e3c-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="05e3c-133">Cree una máquina virtual de Azure que ejecute IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="05e3c-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="05e3c-134">Cargar el contenedor de almacenamiento de Azure de tooan de datos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="05e3c-135">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="05e3c-136">Transformar datos toocleaned, formato tabular, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="05e3c-137">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="05e3c-138">Extraiga una muestra de datos de tamaño pequeño a medio.</span><span class="sxs-lookup"><span data-stu-id="05e3c-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="05e3c-139">Guardar datos de hello muestreada en blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="05e3c-140">Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="05e3c-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="05e3c-141">Leer datos de Hola de blobs de Azure mediante hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="05e3c-142">Cree un flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos ingeridos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="05e3c-143"><a name="smalllocaltodb"></a>Escenario \#4: toomedium pequeño conjunto de datos de archivos locales, como el destino de SQL Server en una máquina Virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="05e3c-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Toomedium pequeños archivos locales tooSQL base de datos de Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="05e3c-145">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="05e3c-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="05e3c-146">Cree una máquina virtual de Azure que ejecute SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="05e3c-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="05e3c-147">Cargar el contenedor de almacenamiento de Azure de tooan de datos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="05e3c-148">Preprocese y limpie datos en el contenedor de almacenamiento de Azure usando IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="05e3c-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="05e3c-149">Transformar datos toocleaned, formato tabular, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="05e3c-150">Guardar archivos de datos local de tooVM (Bloc de notas de IPython se ejecuta en máquinas virtuales, las unidades locales, consulte tooVM unidades).</span><span class="sxs-lookup"><span data-stu-id="05e3c-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="05e3c-151">Carga datos tooSQL base de datos Server ejecuta en una VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="05e3c-152">Opción \#1: Mediante SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="05e3c-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="05e3c-153">Inicio de sesión tooSQL máquina virtual Server</span><span class="sxs-lookup"><span data-stu-id="05e3c-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="05e3c-154">Ejecute SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="05e3c-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="05e3c-155">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="05e3c-155">Create database and target tables.</span></span>
   * <span data-ttu-id="05e3c-156">Use uno de forma masiva de Hola importar datos de Hola de tooload de métodos de archivos de máquina virtual local.</span><span class="sxs-lookup"><span data-stu-id="05e3c-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="05e3c-157">Opción \#2: Mediante IPython Notebook (no se recomienda para conjuntos de datos de tamaño medio o más grandes)</span><span class="sxs-lookup"><span data-stu-id="05e3c-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="05e3c-158">Usar tooaccess de cadena de conexión de ODBC SQL Server en máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05e3c-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="05e3c-159">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="05e3c-159">Create database and target tables.</span></span>
   * <span data-ttu-id="05e3c-160">Use uno de forma masiva de Hola importar datos de Hola de tooload de métodos de archivos de máquina virtual local.</span><span class="sxs-lookup"><span data-stu-id="05e3c-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="05e3c-161">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-161">Explore data, create features as needed.</span></span> <span data-ttu-id="05e3c-162">Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="05e3c-163">Tenga en cuenta solo Hola consulta necesarios toocreate ellos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="05e3c-164">Elija un tamaño de muestra de datos, si lo necesita y/o desea.</span><span class="sxs-lookup"><span data-stu-id="05e3c-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="05e3c-165">Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="05e3c-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="05e3c-166">Datos de lectura Hola directamente de Hola a SQL Server mediante hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="05e3c-167">Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="05e3c-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="05e3c-168">Cree un flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos ingeridos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="05e3c-169"><a name="largelocaltodb"></a>Escenario \#5: Conjunto de datos grande de archivos locales, con SQL Server en una máquina virtual de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="05e3c-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Archivos locales grandes tooSQL base de datos de Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="05e3c-171">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="05e3c-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="05e3c-172">Cree una máquina virtual de Azure que ejecute SQL Server y el servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="05e3c-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="05e3c-173">Cargar el contenedor de almacenamiento de Azure de tooan de datos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="05e3c-174">(Opcional) Preprocese y limpie los datos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="05e3c-175">a.</span><span class="sxs-lookup"><span data-stu-id="05e3c-175">a.</span></span>  <span data-ttu-id="05e3c-176">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde Azure</span><span class="sxs-lookup"><span data-stu-id="05e3c-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="05e3c-177">b.</span><span class="sxs-lookup"><span data-stu-id="05e3c-177">b.</span></span>  <span data-ttu-id="05e3c-178">Transformar datos toocleaned, formato tabular, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="05e3c-179">c.</span><span class="sxs-lookup"><span data-stu-id="05e3c-179">c.</span></span>  <span data-ttu-id="05e3c-180">Guardar archivos de datos local de tooVM (Bloc de notas de IPython se ejecuta en máquinas virtuales, las unidades locales, consulte tooVM unidades).</span><span class="sxs-lookup"><span data-stu-id="05e3c-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="05e3c-181">Carga datos tooSQL base de datos Server ejecuta en una VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="05e3c-182">a.</span><span class="sxs-lookup"><span data-stu-id="05e3c-182">a.</span></span>  <span data-ttu-id="05e3c-183">TooSQL máquina virtual del servidor de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="05e3c-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="05e3c-184">b.</span><span class="sxs-lookup"><span data-stu-id="05e3c-184">b.</span></span>  <span data-ttu-id="05e3c-185">Si los datos todavía no están guardados, descargue los archivos de datos desde Azure</span><span class="sxs-lookup"><span data-stu-id="05e3c-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="05e3c-186">c.</span><span class="sxs-lookup"><span data-stu-id="05e3c-186">c.</span></span>  <span data-ttu-id="05e3c-187">Ejecute SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="05e3c-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="05e3c-188">d.</span><span class="sxs-lookup"><span data-stu-id="05e3c-188">d.</span></span>  <span data-ttu-id="05e3c-189">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="05e3c-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="05e3c-190">e.</span><span class="sxs-lookup"><span data-stu-id="05e3c-190">e.</span></span>  <span data-ttu-id="05e3c-191">Use uno de forma masiva de Hola importarlos métodos tooload Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="05e3c-192">f.</span><span class="sxs-lookup"><span data-stu-id="05e3c-192">f.</span></span>  <span data-ttu-id="05e3c-193">Si se necesitan combinaciones de tablas, crear combinaciones de tooexpedite de índices.</span><span class="sxs-lookup"><span data-stu-id="05e3c-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05e3c-194">Para acelerar la carga de tamaños de datos de gran tamaño, se recomienda que cree tablas con particiones y datos de Hola de importación en paralelo de forma masiva.</span><span class="sxs-lookup"><span data-stu-id="05e3c-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="05e3c-195">Para obtener más información, consulte [tooSQL de importación de datos paralelos Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="05e3c-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="05e3c-196">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-196">Explore data, create features as needed.</span></span> <span data-ttu-id="05e3c-197">Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="05e3c-198">Tenga en cuenta solo Hola consulta necesarios toocreate ellos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="05e3c-199">Elija un tamaño de muestra de datos, si lo necesita y/o desea.</span><span class="sxs-lookup"><span data-stu-id="05e3c-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="05e3c-200">Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="05e3c-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="05e3c-201">Datos de lectura Hola directamente de Hola a SQL Server mediante hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="05e3c-202">Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="05e3c-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="05e3c-203">Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados</span><span class="sxs-lookup"><span data-stu-id="05e3c-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="05e3c-204"><a name="largedbtodb"></a>Escenario \#6: Conjunto de datos grande de archivos locales, con SQL Server en una máquina virtual de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="05e3c-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Gran base de datos SQL local tooSQL base de datos de Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="05e3c-206">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="05e3c-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="05e3c-207">Cree una máquina virtual de Azure que ejecute SQL Server y el servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="05e3c-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="05e3c-208">Use uno de los datos de hello exportarlos métodos tooexport Hola desde archivos toodump de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="05e3c-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05e3c-209">Si decide toomove todos los datos de base de datos de hello local, una alternativa (más rápido) método toomove Hola completa de la base de datos toothe instancia de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="05e3c-210">Omitir pasos de hello tooexport datos, crear base de datos y base de datos de destino de carga/importar datos toohello y siga método alternativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="05e3c-211">Cargar el contenedor de almacenamiento de tooAzure de archivos de volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="05e3c-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="05e3c-212">Carga Hola datos tooa base datos SQL Server ejecuta en una máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="05e3c-213">a.</span><span class="sxs-lookup"><span data-stu-id="05e3c-213">a.</span></span>  <span data-ttu-id="05e3c-214">Inicio de sesión toohello VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="05e3c-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="05e3c-215">b.</span><span class="sxs-lookup"><span data-stu-id="05e3c-215">b.</span></span>  <span data-ttu-id="05e3c-216">Descargar archivos de datos desde una carpeta de local-VM de toohello de contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="05e3c-217">c.</span><span class="sxs-lookup"><span data-stu-id="05e3c-217">c.</span></span>  <span data-ttu-id="05e3c-218">Ejecute SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="05e3c-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="05e3c-219">d.</span><span class="sxs-lookup"><span data-stu-id="05e3c-219">d.</span></span>  <span data-ttu-id="05e3c-220">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="05e3c-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="05e3c-221">e.</span><span class="sxs-lookup"><span data-stu-id="05e3c-221">e.</span></span>  <span data-ttu-id="05e3c-222">Use uno de forma masiva de Hola importarlos métodos tooload Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="05e3c-223">f.</span><span class="sxs-lookup"><span data-stu-id="05e3c-223">f.</span></span>  <span data-ttu-id="05e3c-224">Si se necesitan combinaciones de tablas, crear combinaciones de tooexpedite de índices.</span><span class="sxs-lookup"><span data-stu-id="05e3c-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05e3c-225">Para acelerar la carga de tamaños de datos de gran tamaño, crear tablas con particiones y toobulk importar datos de hello en paralelo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="05e3c-226">Para obtener más información, consulte [tooSQL de importación de datos paralelos Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="05e3c-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="05e3c-227">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-227">Explore data, create features as needed.</span></span> <span data-ttu-id="05e3c-228">Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="05e3c-229">Tenga en cuenta solo Hola consulta necesarios toocreate ellos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="05e3c-230">Elija un tamaño de muestra de datos, si lo necesita y/o desea.</span><span class="sxs-lookup"><span data-stu-id="05e3c-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="05e3c-231">Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="05e3c-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="05e3c-232">Datos de lectura Hola directamente de Hola a SQL Server mediante hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="05e3c-233">Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="05e3c-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="05e3c-234">Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados.</span><span class="sxs-lookup"><span data-stu-id="05e3c-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="05e3c-235">Método alternativo toocopy una base de datos completa de un tooAzure de SQL Server local base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="05e3c-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Base de datos local de separar y adjuntar tooSQL base de datos de Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="05e3c-237">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="05e3c-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="05e3c-238">tooreplicate Hola SQL Server base de datos completa en la VM de SQL Server, debe copiar una base de datos de una tooanother/servidor de ubicación, suponiendo que esa base de datos de Hola se pueden desconectar temporalmente.</span><span class="sxs-lookup"><span data-stu-id="05e3c-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="05e3c-239">Para ello, en hello Explorador de objetos de SQL Server Management Studio, o mediante comandos de Transact-SQL equivalentes Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="05e3c-240">Separar base de datos de hello en la ubicación de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="05e3c-241">Para más información, consulte [Desasociar una base de datos](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="05e3c-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="05e3c-242">En la ventana del explorador de Windows o el símbolo del sistema de Windows, Hola copia separa el archivo de base de datos o archivos y archivo de registro o ubicación de destino de archivos toohello en hello VM de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="05e3c-243">Asociar instancia de SQL Server de destino de hello copian archivos toohello.</span><span class="sxs-lookup"><span data-stu-id="05e3c-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="05e3c-244">Para más información, consulte [Asociar una base de datos](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="05e3c-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="05e3c-245">[Mover una base de datos mediante las opciones desasociación y asociación (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="05e3c-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="05e3c-246"><a name="largedbtohive"></a>Escenario \#7: Big Data de archivos locales, con base de datos de Hive como destino en clústeres de Hadoop de Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="05e3c-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Datos de gran tamaño en Hive de destino local][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="05e3c-248">Recursos adicionales de Azure: Clúster de Hadoop de HDInsight de Azure y máquina virtual de Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="05e3c-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="05e3c-249">Cree una máquina virtual de Azure que ejecute el servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="05e3c-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="05e3c-250">Cree un clúster de Hadoop de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="05e3c-251">(Opcional) Preprocese y limpie los datos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="05e3c-252">a.</span><span class="sxs-lookup"><span data-stu-id="05e3c-252">a.</span></span>  <span data-ttu-id="05e3c-253">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde Azure</span><span class="sxs-lookup"><span data-stu-id="05e3c-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="05e3c-254">b.</span><span class="sxs-lookup"><span data-stu-id="05e3c-254">b.</span></span>  <span data-ttu-id="05e3c-255">Transformar datos toocleaned, formato tabular, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="05e3c-256">c.</span><span class="sxs-lookup"><span data-stu-id="05e3c-256">c.</span></span>  <span data-ttu-id="05e3c-257">Guardar archivos de datos local de tooVM (Bloc de notas de IPython se ejecuta en máquinas virtuales, las unidades locales, consulte tooVM unidades).</span><span class="sxs-lookup"><span data-stu-id="05e3c-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="05e3c-258">Cargar el contenedor de datos toohello predeterminado del clúster de Hadoop de hello seleccionado en el paso 2 de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="05e3c-259">Carga datos tooHive base de datos en clúster de HDInsight Hadoop de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="05e3c-260">a.</span><span class="sxs-lookup"><span data-stu-id="05e3c-260">a.</span></span>  <span data-ttu-id="05e3c-261">Inicie sesión en toohello nodo principal del clúster de Hadoop de Hola</span><span class="sxs-lookup"><span data-stu-id="05e3c-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="05e3c-262">b.</span><span class="sxs-lookup"><span data-stu-id="05e3c-262">b.</span></span>  <span data-ttu-id="05e3c-263">Abra Hola línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="05e3c-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="05e3c-264">c.</span><span class="sxs-lookup"><span data-stu-id="05e3c-264">c.</span></span>  <span data-ttu-id="05e3c-265">Escriba el directorio de raíz del subárbol de hello comando `cd %hive_home%\bin` en línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="05e3c-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="05e3c-266">d.</span><span class="sxs-lookup"><span data-stu-id="05e3c-266">d.</span></span>  <span data-ttu-id="05e3c-267">Ejecutar la base de datos toocreate consultas de Hive de Hola y tablas y cargar datos de tablas de tooHive de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="05e3c-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05e3c-268">Si los datos de hello están grandes, los usuarios pueden crear tabla de Hive Hola con particiones.</span><span class="sxs-lookup"><span data-stu-id="05e3c-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="05e3c-269">A continuación, los usuarios pueden utilizar un `for` bucle en la línea de comandos de Hadoop de hello en los datos de tooload de nodo principal de hello en tabla de Hive Hola particionado por partición.</span><span class="sxs-lookup"><span data-stu-id="05e3c-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="05e3c-270">Explore datos y cree características según sea necesario en la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="05e3c-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="05e3c-271">Tenga en cuenta que las características de hello no es necesario toobe materializar en tablas de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05e3c-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="05e3c-272">Tenga en cuenta solo Hola consulta necesarios toocreate ellos.</span><span class="sxs-lookup"><span data-stu-id="05e3c-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="05e3c-273">a.</span><span class="sxs-lookup"><span data-stu-id="05e3c-273">a.</span></span>  <span data-ttu-id="05e3c-274">Inicie sesión en toohello nodo principal del clúster de Hadoop de Hola</span><span class="sxs-lookup"><span data-stu-id="05e3c-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="05e3c-275">b.</span><span class="sxs-lookup"><span data-stu-id="05e3c-275">b.</span></span>  <span data-ttu-id="05e3c-276">Abra Hola línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="05e3c-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="05e3c-277">c.</span><span class="sxs-lookup"><span data-stu-id="05e3c-277">c.</span></span>  <span data-ttu-id="05e3c-278">Escriba el directorio de raíz del subárbol de hello comando `cd %hive_home%\bin` en línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="05e3c-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="05e3c-279">d.</span><span class="sxs-lookup"><span data-stu-id="05e3c-279">d.</span></span>  <span data-ttu-id="05e3c-280">Ejecutar consultas de Hive hello en línea de comandos de Hadoop en el nodo principal de Hola Hola Hadoop tooexplore Hola de datos de clúster y crear características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="05e3c-281">Si necesita y/o deseado, ejemplo de Hola datos toofit en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="05e3c-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="05e3c-282">Inicie sesión en toohello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="05e3c-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="05e3c-283">Leer datos de hello directamente desde hello `Hive Queries` con hello [importar datos] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="05e3c-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="05e3c-284">Pegar Hola consulta necesario que extrae los campos, crea características y ejemplos de datos si es necesario directamente en hello [importar datos] [ import-data] consulta.</span><span class="sxs-lookup"><span data-stu-id="05e3c-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="05e3c-285">Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados.</span><span class="sxs-lookup"><span data-stu-id="05e3c-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="05e3c-286"><a name="decisiontree"></a>Árbol de decisión de selección de escenario</span><span class="sxs-lookup"><span data-stu-id="05e3c-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="05e3c-287">Hello diagrama siguiente resume escenarios Hola que se ha descrito anteriormente y opciones proceso de análisis avanzado y la tecnología de hello elegido que toman tooeach de escenarios de hello detallado.</span><span class="sxs-lookup"><span data-stu-id="05e3c-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="05e3c-288">Tenga en cuenta que pueden llevar a cabo el procesamiento de datos, la exploración, ingeniería de característica y muestreo colocar en uno o más entornos de destino, o método/entorno--en origen hello, intermedio y puede realizarse de forma iterativa según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="05e3c-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="05e3c-289">diagrama de Hello solo sirve para ilustrar algunos de los flujos de posibles y no proporciona una enumeración exhaustiva.</span><span class="sxs-lookup"><span data-stu-id="05e3c-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Escenarios de tutoriales de proceso de ciencia de datos de ejemplo][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="05e3c-291">Ejemplos de análisis avanzado en acción</span><span class="sxs-lookup"><span data-stu-id="05e3c-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="05e3c-292">Para ver tutoriales de aprendizaje automático de Azure de extremo a extremo que emplean Hola tecnología y el proceso de análisis avanzado mediante conjuntos de datos públicas, vea:</span><span class="sxs-lookup"><span data-stu-id="05e3c-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="05e3c-293">[Proceso de ciencia de datos en equipos en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="05e3c-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="05e3c-294">[Proceso de ciencia de datos en equipos en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="05e3c-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
