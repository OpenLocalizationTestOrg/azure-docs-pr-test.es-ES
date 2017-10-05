---
title: "Identificación de escenarios de análisis avanzados para Azure Machine Learning | Microsoft Docs"
description: "Seleccione los escenarios adecuados para el proceso de análisis predictivo avanzado con el proceso de ciencia de datos en equipos."
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
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="9558c-103">Escenarios para análisis avanzado en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="9558c-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="9558c-104">En este artículo se describen los distintos escenarios de origen y destino de datos de ejemplo que se pueden administrar con el [proceso de ciencia de datos en equipos (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9558c-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="9558c-105">El TDSP proporciona un enfoque sistemático a los equipos que colaboran en la compilación de aplicaciones inteligentes.</span><span class="sxs-lookup"><span data-stu-id="9558c-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="9558c-106">Los escenarios que se exponen aquí muestran las opciones disponibles en el flujo de trabajo de procesamiento de datos en función de las características de datos, las ubicaciones de origen y los repositorios de destino de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="9558c-107">En la última sección se presenta el **árbol de decisión** para seleccionar los escenarios de ejemplo adecuados para los datos y el objetivo.</span><span class="sxs-lookup"><span data-stu-id="9558c-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="9558c-108">Cada una de las secciones siguientes presenta un escenario de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9558c-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="9558c-109">Para cada escenario, se enumera un posible flujo de ciencia de datos y análisis avanzado, así como los recursos de compatibilidad de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="9558c-110">**Para todos los escenarios siguientes, debe:**
> </span><span class="sxs-lookup"><span data-stu-id="9558c-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="9558c-111">[Crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="9558c-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="9558c-112">Creación de un área de trabajo de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="9558c-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="9558c-113"><a name="smalllocal"></a>Escenario \#1: Conjunto de datos tabular de tamaño pequeño a medio de archivos locales</span><span class="sxs-lookup"><span data-stu-id="9558c-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Archivos locales de tamaño pequeño a medio][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="9558c-115">Recursos adicionales de Azure: ninguno</span><span class="sxs-lookup"><span data-stu-id="9558c-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="9558c-116">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9558c-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="9558c-117">Cargue un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-117">Upload a dataset.</span></span>
3. <span data-ttu-id="9558c-118">Cree un flujo de experimento de Aprendizaje automático de Azure comenzando con conjuntos de datos cargados.</span><span class="sxs-lookup"><span data-stu-id="9558c-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="9558c-119"><a name="smalllocalprocess"></a>Escenario \#2: Conjunto de datos de tamaño pequeño a medio de archivos locales que requieren procesamiento</span><span class="sxs-lookup"><span data-stu-id="9558c-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Archivos locales de tamaño pequeño a medio con procesamiento][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9558c-121">Recursos adicionales de Azure: Máquina virtual de Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="9558c-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9558c-122">Cree una máquina virtual de Azure que ejecute IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="9558c-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="9558c-123">Cargue datos en un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9558c-124">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde el contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="9558c-125">Transforme datos para un formulario limpio y tabular.</span><span class="sxs-lookup"><span data-stu-id="9558c-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="9558c-126">Guarde los datos transformados en blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="9558c-127">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9558c-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="9558c-128">Lea los datos de blobs de Azure mediante el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="9558c-129">Cree un flujo de experimento de Aprendizaje automático de Azure comenzando con conjuntos de datos introducidos.</span><span class="sxs-lookup"><span data-stu-id="9558c-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9558c-130"><a name="largelocal"></a>Escenario \#3: Conjunto de datos grande de archivos locales, con blobs de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="9558c-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Archivos locales grandes][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9558c-132">Recursos adicionales de Azure: Máquina virtual de Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="9558c-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9558c-133">Cree una máquina virtual de Azure que ejecute IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="9558c-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="9558c-134">Cargue datos en un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9558c-135">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="9558c-136">Transforme datos en un formulario limpio y tabular si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="9558c-137">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="9558c-138">Extraiga una muestra de datos de tamaño pequeño a medio.</span><span class="sxs-lookup"><span data-stu-id="9558c-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="9558c-139">Guarde los datos de muestra en blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="9558c-140">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9558c-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="9558c-141">Lea los datos de blobs de Azure mediante el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="9558c-142">Cree un flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos ingeridos.</span><span class="sxs-lookup"><span data-stu-id="9558c-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9558c-143"><a name="smalllocaltodb"></a>Escenario \#4: Conjunto de datos de tamaño pequeño a medio de archivos locales, con SQL Server en una máquina virtual de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="9558c-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Archivos locales de tamaño pequeño a medio a Base de datos SQL de Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9558c-145">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="9558c-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9558c-146">Cree una máquina virtual de Azure que ejecute SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="9558c-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="9558c-147">Cargue datos en un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9558c-148">Preprocese y limpie datos en el contenedor de almacenamiento de Azure usando IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="9558c-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="9558c-149">Transforme datos en un formulario limpio y tabular si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="9558c-150">Guarde datos en archivos locales de máquina virtual (IPython Notebook se ejecuta en una máquina virtual; las unidades locales hacen referencia a unidades de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="9558c-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="9558c-151">Cargue datos en la base de datos de SQL Server que se ejecuta en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="9558c-152">Opción \#1: Mediante SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9558c-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="9558c-153">Inicie sesión en la máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9558c-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="9558c-154">Ejecute SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9558c-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="9558c-155">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="9558c-155">Create database and target tables.</span></span>
   * <span data-ttu-id="9558c-156">Use uno de los métodos de importación en bloque para cargar los datos desde archivos locales de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9558c-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="9558c-157">Opción \#2: Mediante IPython Notebook (no se recomienda para conjuntos de datos de tamaño medio o más grandes)</span><span class="sxs-lookup"><span data-stu-id="9558c-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="9558c-158">Use la cadena de conexión ODBC para obtener acceso a SQL Server en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9558c-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="9558c-159">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="9558c-159">Create database and target tables.</span></span>
   * <span data-ttu-id="9558c-160">Use uno de los métodos de importación en bloque para cargar los datos desde archivos locales de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9558c-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="9558c-161">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-161">Explore data, create features as needed.</span></span> <span data-ttu-id="9558c-162">Tenga en cuenta que las características no necesitan materializarse en las tablas de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9558c-163">Solo tenga en cuenta la consulta necesaria para crearlas.</span><span class="sxs-lookup"><span data-stu-id="9558c-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="9558c-164">Elija un tamaño de muestra de datos, si lo necesita y/o desea.</span><span class="sxs-lookup"><span data-stu-id="9558c-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="9558c-165">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9558c-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="9558c-166">Lea los datos directamente desde SQL Server mediante el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9558c-167">Pegue la consulta necesaria que extrae los campos, crea características y toma muestras de datos si es necesario directamente en la consulta [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="9558c-168">Cree un flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos ingeridos.</span><span class="sxs-lookup"><span data-stu-id="9558c-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9558c-169"><a name="largelocaltodb"></a>Escenario \#5: Conjunto de datos grande de archivos locales, con SQL Server en una máquina virtual de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="9558c-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Archivos locales grandes a Base de datos SQL de Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9558c-171">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="9558c-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9558c-172">Cree una máquina virtual de Azure que ejecute SQL Server y el servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="9558c-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="9558c-173">Cargue datos en un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9558c-174">(Opcional) Preprocese y limpie los datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="9558c-175">a.</span><span class="sxs-lookup"><span data-stu-id="9558c-175">a.</span></span>  <span data-ttu-id="9558c-176">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde Azure</span><span class="sxs-lookup"><span data-stu-id="9558c-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="9558c-177">b.</span><span class="sxs-lookup"><span data-stu-id="9558c-177">b.</span></span>  <span data-ttu-id="9558c-178">Transforme datos en un formulario limpio y tabular si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="9558c-179">c.</span><span class="sxs-lookup"><span data-stu-id="9558c-179">c.</span></span>  <span data-ttu-id="9558c-180">Guarde datos en archivos locales de máquina virtual (IPython Notebook se ejecuta en una máquina virtual; las unidades locales hacen referencia a unidades de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="9558c-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="9558c-181">Cargue datos en la base de datos de SQL Server que se ejecuta en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="9558c-182">a.</span><span class="sxs-lookup"><span data-stu-id="9558c-182">a.</span></span>  <span data-ttu-id="9558c-183">Inicie sesión en la máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9558c-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="9558c-184">b.</span><span class="sxs-lookup"><span data-stu-id="9558c-184">b.</span></span>  <span data-ttu-id="9558c-185">Si los datos todavía no están guardados, descargue los archivos de datos desde Azure</span><span class="sxs-lookup"><span data-stu-id="9558c-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="9558c-186">c.</span><span class="sxs-lookup"><span data-stu-id="9558c-186">c.</span></span>  <span data-ttu-id="9558c-187">Ejecute SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9558c-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="9558c-188">d.</span><span class="sxs-lookup"><span data-stu-id="9558c-188">d.</span></span>  <span data-ttu-id="9558c-189">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="9558c-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="9558c-190">e.</span><span class="sxs-lookup"><span data-stu-id="9558c-190">e.</span></span>  <span data-ttu-id="9558c-191">Use uno de los métodos de importación en masa para cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="9558c-192">f.</span><span class="sxs-lookup"><span data-stu-id="9558c-192">f.</span></span>  <span data-ttu-id="9558c-193">Si se requieren combinaciones de tablas, cree índices para acelerar dichas combinaciones.</span><span class="sxs-lookup"><span data-stu-id="9558c-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9558c-194">Para acelerar la carga de tamaños de datos de gran volumen, es recomendable crear tablas con particiones e importar en masa los datos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="9558c-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="9558c-195">Para obtener más información, vea [Importación de datos en paralelo a tablas con particiones de SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9558c-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9558c-196">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-196">Explore data, create features as needed.</span></span> <span data-ttu-id="9558c-197">Tenga en cuenta que las características no necesitan materializarse en las tablas de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9558c-198">Solo tenga en cuenta la consulta necesaria para crearlas.</span><span class="sxs-lookup"><span data-stu-id="9558c-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="9558c-199">Elija un tamaño de muestra de datos, si lo necesita y/o desea.</span><span class="sxs-lookup"><span data-stu-id="9558c-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="9558c-200">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9558c-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="9558c-201">Lea los datos directamente desde SQL Server mediante el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9558c-202">Pegue la consulta necesaria que extrae los campos, crea características y toma muestras de datos si es necesario directamente en la consulta [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="9558c-203">Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados</span><span class="sxs-lookup"><span data-stu-id="9558c-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="9558c-204"><a name="largedbtodb"></a>Escenario \#6: Conjunto de datos grande de archivos locales, con SQL Server en una máquina virtual de Azure como destino</span><span class="sxs-lookup"><span data-stu-id="9558c-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Base de datos SQL local a Base be datos SQL de Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9558c-206">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="9558c-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9558c-207">Cree una máquina virtual de Azure que ejecute SQL Server y el servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="9558c-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="9558c-208">Use uno de los métodos de exportación de datos para exportar los datos desde SQL Server a archivos de volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="9558c-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9558c-209">Si decide mover todos los datos de la base de datos local, un método alternativo (más rápido) para mover la base de datos completa a la instancia de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="9558c-210">Omita los pasos para exportar datos, crear la base de datos y cargar e importar datos a la base de datos de destino y siga el método alternativo.</span><span class="sxs-lookup"><span data-stu-id="9558c-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="9558c-211">Cargue archivos de volcado de memoria en el contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="9558c-212">Cargue los datos en una base de datos de SQL Server que se ejecute en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="9558c-213">a.</span><span class="sxs-lookup"><span data-stu-id="9558c-213">a.</span></span>  <span data-ttu-id="9558c-214">Inicie sesión en la máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9558c-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="9558c-215">b.</span><span class="sxs-lookup"><span data-stu-id="9558c-215">b.</span></span>  <span data-ttu-id="9558c-216">Descargue los archivos de datos desde un contenedor de almacenamiento de Azure a la carpeta de la máquina virtual local.</span><span class="sxs-lookup"><span data-stu-id="9558c-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="9558c-217">c.</span><span class="sxs-lookup"><span data-stu-id="9558c-217">c.</span></span>  <span data-ttu-id="9558c-218">Ejecute SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9558c-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="9558c-219">d.</span><span class="sxs-lookup"><span data-stu-id="9558c-219">d.</span></span>  <span data-ttu-id="9558c-220">Cree tablas de base de datos y de destino.</span><span class="sxs-lookup"><span data-stu-id="9558c-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="9558c-221">e.</span><span class="sxs-lookup"><span data-stu-id="9558c-221">e.</span></span>  <span data-ttu-id="9558c-222">Use uno de los métodos de importación en masa para cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="9558c-223">f.</span><span class="sxs-lookup"><span data-stu-id="9558c-223">f.</span></span>  <span data-ttu-id="9558c-224">Si se requieren combinaciones de tablas, cree índices para acelerar dichas combinaciones.</span><span class="sxs-lookup"><span data-stu-id="9558c-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9558c-225">Para acelerar la carga de tamaños de datos de gran tamaño, cree tablas con particiones e importe en masa los datos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="9558c-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="9558c-226">Para obtener más información, vea [Importación de datos en paralelo a tablas con particiones de SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9558c-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9558c-227">Explore datos y cree características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-227">Explore data, create features as needed.</span></span> <span data-ttu-id="9558c-228">Tenga en cuenta que las características no necesitan materializarse en las tablas de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9558c-229">Solo tenga en cuenta la consulta necesaria para crearlas.</span><span class="sxs-lookup"><span data-stu-id="9558c-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="9558c-230">Elija un tamaño de muestra de datos, si lo necesita y/o desea.</span><span class="sxs-lookup"><span data-stu-id="9558c-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="9558c-231">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9558c-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="9558c-232">Lea los datos directamente desde SQL Server mediante el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9558c-233">Pegue la consulta necesaria que extrae los campos, crea características y toma muestras de datos si es necesario directamente en la consulta [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="9558c-234">Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados.</span><span class="sxs-lookup"><span data-stu-id="9558c-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="9558c-235">Método alternativo para copiar una base de datos completa desde un servidor SQL Server local a Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9558c-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Desasociación de base de datos local y asociación a Base de datos SQL de Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9558c-237">Recursos adicionales de Azure: Máquina virtual de Azure (AQL Server/servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="9558c-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="9558c-238">Para replicar toda la base de datos de SQL Server en la máquina virtual de SQL Server, debe copiar una base de datos desde una ubicación o  un servidor a otro, suponiendo que la base de datos se puede desconectar temporalmente.</span><span class="sxs-lookup"><span data-stu-id="9558c-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="9558c-239">Esto se realiza en el Explorador de objetos de SQL Server Management Studio o mediante los comandos de Transact-SQL equivalentes.</span><span class="sxs-lookup"><span data-stu-id="9558c-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="9558c-240">Desasocie la base de datos en la ubicación de origen.</span><span class="sxs-lookup"><span data-stu-id="9558c-240">Detach the database at the source location.</span></span> <span data-ttu-id="9558c-241">Para más información, consulte [Desasociar una base de datos](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="9558c-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="9558c-242">En el Explorador de Windows o en la ventana del símbolo del sistema de Windows, copie los archivos de base de datos desasociados o los archivos de registro a la ubicación de destino en la máquina virtual de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="9558c-243">Asocie los archivos copiados a la instancia de SQL Server de destino.</span><span class="sxs-lookup"><span data-stu-id="9558c-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="9558c-244">Para más información, consulte [Asociar una base de datos](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="9558c-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="9558c-245">[Mover una base de datos mediante las opciones desasociación y asociación (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="9558c-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="9558c-246"><a name="largedbtohive"></a>Escenario \#7: Big Data de archivos locales, con base de datos de Hive como destino en clústeres de Hadoop de Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9558c-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Datos de gran tamaño en Hive de destino local][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9558c-248">Recursos adicionales de Azure: Clúster de Hadoop de HDInsight de Azure y máquina virtual de Azure (servidor IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="9558c-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9558c-249">Cree una máquina virtual de Azure que ejecute el servidor IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="9558c-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="9558c-250">Cree un clúster de Hadoop de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="9558c-251">(Opcional) Preprocese y limpie los datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="9558c-252">a.</span><span class="sxs-lookup"><span data-stu-id="9558c-252">a.</span></span>  <span data-ttu-id="9558c-253">Preprocese y limpie datos en IPython Notebook obteniendo acceso desde Azure</span><span class="sxs-lookup"><span data-stu-id="9558c-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="9558c-254">b.</span><span class="sxs-lookup"><span data-stu-id="9558c-254">b.</span></span>  <span data-ttu-id="9558c-255">Transforme datos en un formulario limpio y tabular si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="9558c-256">c.</span><span class="sxs-lookup"><span data-stu-id="9558c-256">c.</span></span>  <span data-ttu-id="9558c-257">Guarde datos en archivos locales de máquina virtual (IPython Notebook se ejecuta en una máquina virtual; las unidades locales hacen referencia a unidades de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="9558c-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="9558c-258">Cargue datos en el contenedor predeterminado del clúster de Hadoop que seleccionó en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="9558c-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="9558c-259">Cargue datos en la base de datos de Hive en el clúster de Hadoop de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="9558c-260">a.</span><span class="sxs-lookup"><span data-stu-id="9558c-260">a.</span></span>  <span data-ttu-id="9558c-261">Inicie sesión en el nodo principal del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9558c-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="9558c-262">b.</span><span class="sxs-lookup"><span data-stu-id="9558c-262">b.</span></span>  <span data-ttu-id="9558c-263">Abra la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9558c-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9558c-264">c.</span><span class="sxs-lookup"><span data-stu-id="9558c-264">c.</span></span>  <span data-ttu-id="9558c-265">Especifique el directorio raíz de Hive mediante el comando `cd %hive_home%\bin` en la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9558c-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9558c-266">d.</span><span class="sxs-lookup"><span data-stu-id="9558c-266">d.</span></span>  <span data-ttu-id="9558c-267">Ejecute las consultas de Hive para crear bases de datos y tablas, y cargar datos desde el almacenamiento de blobs en tablas de Hive.</span><span class="sxs-lookup"><span data-stu-id="9558c-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9558c-268">Si los datos son grandes, los usuarios pueden crear la tabla de Hive con particiones.</span><span class="sxs-lookup"><span data-stu-id="9558c-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="9558c-269">A continuación, los usuarios pueden usar un bucle `for` en la línea de comandos de Hadoop en el nodo principal para cargar datos en la tabla de Hive con particiones por partición.</span><span class="sxs-lookup"><span data-stu-id="9558c-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="9558c-270">Explore datos y cree características según sea necesario en la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9558c-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="9558c-271">Tenga en cuenta que las características no necesitan materializarse en las tablas de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9558c-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9558c-272">Solo tenga en cuenta la consulta necesaria para crearlas.</span><span class="sxs-lookup"><span data-stu-id="9558c-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="9558c-273">a.</span><span class="sxs-lookup"><span data-stu-id="9558c-273">a.</span></span>  <span data-ttu-id="9558c-274">Inicie sesión en el nodo principal del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9558c-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="9558c-275">b.</span><span class="sxs-lookup"><span data-stu-id="9558c-275">b.</span></span>  <span data-ttu-id="9558c-276">Abra la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9558c-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9558c-277">c.</span><span class="sxs-lookup"><span data-stu-id="9558c-277">c.</span></span>  <span data-ttu-id="9558c-278">Especifique el directorio raíz de Hive mediante el comando `cd %hive_home%\bin` en la línea de comandos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9558c-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9558c-279">d.</span><span class="sxs-lookup"><span data-stu-id="9558c-279">d.</span></span>  <span data-ttu-id="9558c-280">Ejecute las consultas de Hive en línea de comandos de Hadoop en el nodo principal del clúster de Hadoop para explorar los datos y crear características según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="9558c-281">Si lo necesita o desea, muestree los datos para ajustarlos en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="9558c-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="9558c-282">Inicie sesión en [Estudio de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9558c-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="9558c-283">Lea los datos directamente desde `Hive Queries` mediante el módulo [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9558c-284">Pegue la consulta necesaria que extrae los campos, crea características y toma muestras de datos si es necesario directamente en la consulta [Importar datos][import-data].</span><span class="sxs-lookup"><span data-stu-id="9558c-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="9558c-285">Flujo de experimento de Azure Machine Learning comenzando con conjuntos de datos cargados.</span><span class="sxs-lookup"><span data-stu-id="9558c-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="9558c-286"><a name="decisiontree"></a>Árbol de decisión de selección de escenario</span><span class="sxs-lookup"><span data-stu-id="9558c-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="9558c-287">El diagrama siguiente resume los escenarios descritos anteriormente y las opciones de la Tecnología y procesos de análisis avanzado elegidas que le guiarán a través de los escenarios detallados.</span><span class="sxs-lookup"><span data-stu-id="9558c-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="9558c-288">Tenga en cuenta que el procesamiento de datos, la exploración, la ingeniería de características y el muestreo pueden tener lugar en uno o varios métodos o entornos (en los entornos de origen, intermedio o de destino) y pueden continuar de forma iterativa según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9558c-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="9558c-289">El diagrama solo sirve para ilustrar algunos de los flujos de posibles y no proporciona una enumeración exhaustiva.</span><span class="sxs-lookup"><span data-stu-id="9558c-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Escenarios de tutoriales de proceso de ciencia de datos de ejemplo][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="9558c-291">Ejemplos de análisis avanzado en acción</span><span class="sxs-lookup"><span data-stu-id="9558c-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="9558c-292">Para los tutoriales de Aprendizaje automático de Azure completos que emplean la Tecnología y procesos de análisis avanzado mediante conjuntos de datos públicos, consulte:</span><span class="sxs-lookup"><span data-stu-id="9558c-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="9558c-293">[Proceso de ciencia de datos en equipos en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="9558c-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="9558c-294">[Proceso de ciencia de datos en equipos en acción: uso de clústeres de Hadoop de HDInsight](machine-learning-data-science-process-hive-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="9558c-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
