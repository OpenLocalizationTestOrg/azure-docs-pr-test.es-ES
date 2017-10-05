---
title: "Uso de actividades personalizadas en una canalización de Factoría de datos de Azure"
description: "Obtenga información acerca de cómo crear actividades personalizadas y usarlas en una canalización de la factoría de datos de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f3d265f31cb653d32076747e586383d67bbccc41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="ab692-103">Uso de actividades personalizadas en una canalización de Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="ab692-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ab692-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="ab692-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="ab692-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="ab692-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ab692-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="ab692-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ab692-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="ab692-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ab692-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="ab692-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ab692-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ab692-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ab692-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ab692-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ab692-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="ab692-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ab692-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ab692-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ab692-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="ab692-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="ab692-114">Hay dos tipos de actividades que puede usar en una canalización de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="ab692-115">[Actividades de movimiento de datos](data-factory-data-movement-activities.md) para mover datos entre [almacenes de datos de origen y receptor compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ab692-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="ab692-116">[Actividades de transformación de datos](data-factory-data-transformation-activities.md) para transformar datos mediante procesos como Azure HDInsight, Azure Batch y Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ab692-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="ab692-117">Para mover datos a o desde un almacén de datos no compatible con Data Factory, cree una **actividad personalizada** con su propia lógica de movimiento de datos y utilícela en una canalización.</span><span class="sxs-lookup"><span data-stu-id="ab692-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span></span> <span data-ttu-id="ab692-118">De forma similar, para transformar y procesar datos de algún modo no compatible con Data Factory, cree una actividad personalizada con su propia lógica de transformación de datos y utilícela en una canalización.</span><span class="sxs-lookup"><span data-stu-id="ab692-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span></span> 

<span data-ttu-id="ab692-119">Puede configurar una actividad personalizada para que se ejecute un grupo de máquinas virtuales de **Azure Batch** o un clúster de **Azure HDInsight** basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="ab692-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="ab692-120">Si usa Azure Batch, solo puede utilizar un grupo de Azure Batch existente.</span><span class="sxs-lookup"><span data-stu-id="ab692-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="ab692-121">Sin embargo, al utilizar HDInsight, puede utilizar un clúster de HDInsight existente o un clúster creado automáticamente cuando se solicita en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ab692-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="ab692-122">En el siguiente tutorial se proporcionan instrucciones paso a paso para crear una actividad de .NET personalizada y utilizarla en una canalización.</span><span class="sxs-lookup"><span data-stu-id="ab692-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span></span> <span data-ttu-id="ab692-123">En el tutorial se utiliza un servicio vinculado de **Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="ab692-123">The walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="ab692-124">Para usar un servicio vinculado de Azure HDInsight, cree un servicio vinculado de tipo **HDInsight** (su propio clúster de HDInsight) o **HDInsightOnDemand** (Data Factory crea un clúster HDInsight a petición).</span><span class="sxs-lookup"><span data-stu-id="ab692-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="ab692-125">A continuación, configure una actividad personalizada para usar el servicio vinculado de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-125">Then, configure custom activity to use the HDInsight linked service.</span></span> <span data-ttu-id="ab692-126">Consulte la sección [Uso de los servicios vinculados de HDInsight de Azure](#use-hdinsight-compute-service) para obtener más información sobre cómo utilizar HDInsight de Azure para ejecutar la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="ab692-127">Las actividades personalizadas de .NET se ejecutan solo en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="ab692-127">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ab692-128">Una solución alternativa para esta limitación consiste en usar la actividad MapReduce para ejecutar código personalizado de Java en un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="ab692-128">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ab692-129">Otra opción es usar un grupo de máquinas virtuales de Azure Batch para ejecutar actividades personalizadas en lugar de utilizar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-129">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="ab692-130">No es posible usar una puerta de enlace de administración de datos procedente de una actividad personalizada para acceder a orígenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="ab692-130">It is not possible to use a Data Management Gateway from a custom activity to access on-premises data sources.</span></span> <span data-ttu-id="ab692-131">Actualmente, la [puerta de enlace de administración de datos](data-factory-data-management-gateway.md) solo admite las actividades de copia y de procedimiento almacenado en Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab692-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only the copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="ab692-132">Tutorial: creación de una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="ab692-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ab692-133">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ab692-133">Prerequisites</span></span>
* <span data-ttu-id="ab692-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="ab692-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="ab692-135">Descargue e instale el [SDK de .NET de Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="ab692-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="ab692-136">Requisitos previos de Lote de Azure</span><span class="sxs-lookup"><span data-stu-id="ab692-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="ab692-137">En el tutorial, ejecutará sus actividades de .NET personalizadas con Lote de Azure como recurso de proceso.</span><span class="sxs-lookup"><span data-stu-id="ab692-137">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="ab692-138">**Azure Batch** es un servicio de plataforma para ejecutar aplicaciones en paralelo a gran escala y de informática de alto rendimiento (HPC) de manera eficaz en la nube.</span><span class="sxs-lookup"><span data-stu-id="ab692-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="ab692-139">Azure Batch programa el trabajo de proceso intensivo para que se ejecute en una **colección administrada de máquinas virtuales** y puede escalar automáticamente los recursos de proceso para satisfacer las necesidades de sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="ab692-139">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span></span> <span data-ttu-id="ab692-140">Consulte el artículo [Datos básicos de Azure Batch][batch-technical-overview] para ver una descripción detallada del servicio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="ab692-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span></span>

<span data-ttu-id="ab692-141">Para el tutorial, cree una cuenta de Azure Batch con un grupo de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ab692-141">For the tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="ab692-142">Estos son los pasos que se deben seguir:</span><span class="sxs-lookup"><span data-stu-id="ab692-142">Here are the steps:</span></span>

1. <span data-ttu-id="ab692-143">Cree una **cuenta de Lote de Azure** en el [Portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ab692-143">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ab692-144">Para obtener instrucciones, consulte el artículo [Creación y administración de una cuenta de Azure Batch][batch-create-account].</span><span class="sxs-lookup"><span data-stu-id="ab692-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="ab692-145">Anote el nombre y la clave de la cuenta de Azure Batch el URI y el nombre del grupo.</span><span class="sxs-lookup"><span data-stu-id="ab692-145">Note down the Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="ab692-146">Los necesita para crear un servicio vinculado de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="ab692-146">You need them to create an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="ab692-147">En la página de inicio de la cuenta de Azure Batch, verá una **dirección URL** con el siguiente formato: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ab692-147">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="ab692-148">En este ejemplo, **myaccount** es el nombre de la cuenta de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="ab692-148">In this example, **myaccount** is the name of the Azure Batch account.</span></span> <span data-ttu-id="ab692-149">El URI que se utiliza en la definición del servicio vinculado es la dirección URL sin el nombre de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="ab692-149">URI you use in the linked service definition is the URL without the name of the account.</span></span> <span data-ttu-id="ab692-150">Por ejemplo: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ab692-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="ab692-151">Haga clic en **Claves** en el menú de la izquierda y copie la **CLAVE DE ACCESO PRIMARIA**.</span><span class="sxs-lookup"><span data-stu-id="ab692-151">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="ab692-152">Para usar un grupo existente, haga clic en **Grupos** en el menú y anote el **identificador** del grupo.</span><span class="sxs-lookup"><span data-stu-id="ab692-152">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span></span> <span data-ttu-id="ab692-153">Si no tienes ningún grupo, ve al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="ab692-153">If you don't have an existing pool, move to the next step.</span></span>     
2. <span data-ttu-id="ab692-154">Cree un **grupo de Lote de Azure**.</span><span class="sxs-lookup"><span data-stu-id="ab692-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="ab692-155">En [Azure Portal](https://portal.azure.com), haga clic en **Examinar** en el menú izquierdo y haga clic en **Cuentas de Lote**.</span><span class="sxs-lookup"><span data-stu-id="ab692-155">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="ab692-156">Seleccione la cuenta de Lote de Azure para abrir la hoja **Cuenta de Lote** .</span><span class="sxs-lookup"><span data-stu-id="ab692-156">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
   3. <span data-ttu-id="ab692-157">Haga clic en el icono **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="ab692-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="ab692-158">En la hoja **Grupos** , haga clic en el botón Agregar en la barra de herramientas para agregar un grupo.</span><span class="sxs-lookup"><span data-stu-id="ab692-158">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
      1. <span data-ttu-id="ab692-159">Especifique un identificador para el grupo (Identificador del grupo).</span><span class="sxs-lookup"><span data-stu-id="ab692-159">Enter an ID for the pool (Pool ID).</span></span> <span data-ttu-id="ab692-160">Anote el **identificador del grupo**; lo necesitará al crear la solución de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab692-160">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
      2. <span data-ttu-id="ab692-161">Especifique **Windows Server 2012 R2** en Familia del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ab692-161">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
      3. <span data-ttu-id="ab692-162">Seleccione un **plan de tarifa de nodos**.</span><span class="sxs-lookup"><span data-stu-id="ab692-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="ab692-163">Escriba **2** como valor en la configuración **Dedicada a destino**.</span><span class="sxs-lookup"><span data-stu-id="ab692-163">Enter **2** as value for the **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="ab692-164">Escriba **2** como valor en la configuración **Máximo de tareas por nodo**.</span><span class="sxs-lookup"><span data-stu-id="ab692-164">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="ab692-165">Haga clic en **Aceptar** para crear el grupo.</span><span class="sxs-lookup"><span data-stu-id="ab692-165">Click **OK** to create the pool.</span></span>
   6. <span data-ttu-id="ab692-166">Anote el **identificador** del grupo.</span><span class="sxs-lookup"><span data-stu-id="ab692-166">Note down the **ID** of the pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="ab692-167">Pasos de alto nivel</span><span class="sxs-lookup"><span data-stu-id="ab692-167">High-level steps</span></span>
<span data-ttu-id="ab692-168">Estos son los dos pasos de alto nivel que se realizan como parte de este tutorial:</span><span class="sxs-lookup"><span data-stu-id="ab692-168">Here are the two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="ab692-169">Cree una actividad personalizada que contenga una lógica de procesamiento o transformación de datos simple.</span><span class="sxs-lookup"><span data-stu-id="ab692-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="ab692-170">Cree una instancia de Azure Data Factory con una canalización que use la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-170">Create an Azure data factory with a pipeline that uses the custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="ab692-171">creación de una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="ab692-171">Create a custom activity</span></span>
<span data-ttu-id="ab692-172">Para crear una actividad personalizada de .NET, cree un proyecto de la **biblioteca de clases .NET** con una clase que implemente la interfaz **IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="ab692-172">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="ab692-173">Esta interfaz solo tiene un método, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , y su firma es:</span><span class="sxs-lookup"><span data-stu-id="ab692-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="ab692-174">El método toma cuatro parámetros:</span><span class="sxs-lookup"><span data-stu-id="ab692-174">The method takes four parameters:</span></span>

- <span data-ttu-id="ab692-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="ab692-175">**linkedServices**.</span></span> <span data-ttu-id="ab692-176">Esta propiedad es una lista enumerable de los servicios vinculados al almacén de datos a los que hacen referencia los conjuntos de datos de entrada y salida de la actividad.</span><span class="sxs-lookup"><span data-stu-id="ab692-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span></span>   
- <span data-ttu-id="ab692-177">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="ab692-177">**datasets**.</span></span> <span data-ttu-id="ab692-178">Esta propiedad es una lista enumerable de los conjuntos de datos de entrada/salida de la actividad.</span><span class="sxs-lookup"><span data-stu-id="ab692-178">This property is an enumerable list of input/output datasets for the activity.</span></span> <span data-ttu-id="ab692-179">Este parámetro se puede usar para obtener las ubicaciones y esquemas que definen los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="ab692-179">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="ab692-180">**activity**.</span><span class="sxs-lookup"><span data-stu-id="ab692-180">**activity**.</span></span> <span data-ttu-id="ab692-181">Esta propiedad representa la actividad actual.</span><span class="sxs-lookup"><span data-stu-id="ab692-181">This property represents the current activity.</span></span> <span data-ttu-id="ab692-182">Se puede utilizar para acceder a propiedades extendidas asociadas a la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-182">It can be used to access extended properties associated with the custom activity.</span></span> <span data-ttu-id="ab692-183">Consulte [Acceso a las propiedades extendidas](#access-extended-properties) para más información.</span><span class="sxs-lookup"><span data-stu-id="ab692-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="ab692-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="ab692-184">**logger**.</span></span> <span data-ttu-id="ab692-185">Este objeto permite escribir comentarios de depuración que se muestran en el registro de usuario en la canalización.</span><span class="sxs-lookup"><span data-stu-id="ab692-185">This object lets you write debug comments that surface in the user log for the pipeline.</span></span>

<span data-ttu-id="ab692-186">El método devuelve un diccionario que se puede usar para encadenar actividades personalizadas en el futuro.</span><span class="sxs-lookup"><span data-stu-id="ab692-186">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="ab692-187">Esta característica todavía no está implementada, así que devuelve un diccionario vacío del método.</span><span class="sxs-lookup"><span data-stu-id="ab692-187">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="ab692-188">Procedimiento</span><span class="sxs-lookup"><span data-stu-id="ab692-188">Procedure</span></span>
1. <span data-ttu-id="ab692-189">Cree un proyecto de **biblioteca de clases .NET** .</span><span class="sxs-lookup"><span data-stu-id="ab692-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="ab692-190">Inicie <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> o <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="ab692-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="ab692-191">Haga clic en <b>Archivo</b>, seleccione <b>Nuevo</b> y, luego, haga clic en <b>Proyecto</b>.</span><span class="sxs-lookup"><span data-stu-id="ab692-191">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="ab692-192">Expanda <b>Plantillas</b> y seleccione <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="ab692-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="ab692-193">En este tutorial se usa C#, pero puede usar cualquier lenguaje .NET para desarrollar la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-193">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span></span></li>
     <li><span data-ttu-id="ab692-194">Seleccione <b>Biblioteca de clases</b> en la lista de tipos de proyecto de la derecha.</span><span class="sxs-lookup"><span data-stu-id="ab692-194">Select <b>Class Library</b> from the list of project types on the right.</span></span> <span data-ttu-id="ab692-195">En VS 2017, elija <b>Biblioteca de clases (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="ab692-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="ab692-196">Escriba <b>MyDotNetActivity </b> para <b>Nombre</b>.</span><span class="sxs-lookup"><span data-stu-id="ab692-196">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="ab692-197">Seleccione <b>C:\ADFGetStarted</b> como <b>Ubicación</b>.</span><span class="sxs-lookup"><span data-stu-id="ab692-197">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="ab692-198">Haga clic en <b>Aceptar</b> para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ab692-198">Click <b>OK</b> to create the project.</span></span></li>
   </ol><span data-ttu-id="ab692-199">
2. Haga clic en **Herramientas**, seleccione **Administrador de paquetes de NuGet** y haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="ab692-199">
2. Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="ab692-200">3.</span><span class="sxs-lookup"><span data-stu-id="ab692-200">3.</span></span> <span data-ttu-id="ab692-201">En la Consola del Administrador de paquetes, ejecute el siguiente comando para importar **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="ab692-201">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="ab692-202">Importe el paquete NuGet de **Almacenamiento de Azure** en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ab692-202">Import the **Azure Storage** NuGet package in to the project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ab692-203">El iniciador del servicio Data Factory requiere la versión 4.3 de WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="ab692-203">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="ab692-204">Si agrega una referencia a una versión posterior del ensamblado de Azure Storage en el proyecto de actividad personalizada, verá un error cuando se ejecuta la actividad.</span><span class="sxs-lookup"><span data-stu-id="ab692-204">If you add a reference to a later version of Azure Storage assembly in your custom activity project, you see an error when the activity executes.</span></span> <span data-ttu-id="ab692-205">Para resolver el error, consulte la sección [Aislamiento de AppDomain](#appdomain-isolation).</span><span class="sxs-lookup"><span data-stu-id="ab692-205">To resolve the error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="ab692-206">Agregue las siguientes instrucciones **using** al archivo de origen en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ab692-206">Add the following **using** statements to the source file in the project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="ab692-207">Cambie el nombre del **espacio de nombres** por **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="ab692-207">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="ab692-208">Cambie el nombre de la clase por **MyDotNetActivity** y derívela desde la interfaz **IDotNetActivity** como se muestra en el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="ab692-208">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="ab692-209">Implemente (agregue) el método **Execute** de la interfaz **IDotNetActivity** en la clase **MyDotNetActivity** y copie el siguiente código de ejemplo en el método.</span><span class="sxs-lookup"><span data-stu-id="ab692-209">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span>

    <span data-ttu-id="ab692-210">El ejemplo siguiente cuenta el número de apariciones del término de búsqueda (“Microsoft”) en cada blob asociado con un segmento de datos.</span><span class="sxs-lookup"><span data-stu-id="ab692-210">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // to log information, use the logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass the connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize the continuation token before using it in the do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get the list of input blobs from the input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns the number of occurrences of
            // the search term (“Microsoft”) in each blob associated
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload the output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} to the output blob", output);
        outputBlob.UploadText(output);
    
        // The dictionary can be used to chain custom activities together in the future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="ab692-211">Agregue los siguientes métodos auxiliares:</span><span class="sxs-lookup"><span data-stu-id="ab692-211">Add the following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
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
                output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="ab692-212">El método GetFolderPath devuelve la ruta de acceso a la carpeta a la que apunta el conjunto de datos y el método GetFileName devuelve el nombre del blob o archivo a la que apunta el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="ab692-212">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span> <span data-ttu-id="ab692-213">Si tiene definiciones de folderPath que usan variables como {Year}, {Month}, {Day}, etc., el método devuelve la cadena tal cual, sin sustituir dichas variables por los valores de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ab692-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="ab692-214">Consulte la sección [Acceso a las propiedades extendidas](#access-extended-properties) para más información sobre cómo acceder a SliceStart, SliceEnd, etc.</span><span class="sxs-lookup"><span data-stu-id="ab692-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="ab692-215">El método Calculate calcula el número de instancias de la palabra clave Microsoft en los archivos de entrada (los blobs de la carpeta).</span><span class="sxs-lookup"><span data-stu-id="ab692-215">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span></span> <span data-ttu-id="ab692-216">El término de búsqueda ("Microsoft") está codificado de forma rígida en el código.</span><span class="sxs-lookup"><span data-stu-id="ab692-216">The search term (“Microsoft”) is hard-coded in the code.</span></span>
10. <span data-ttu-id="ab692-217">Compile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ab692-217">Compile the project.</span></span> <span data-ttu-id="ab692-218">Haga clic en **Compilar** en el menú y haga clic en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="ab692-218">Click **Build** from the menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ab692-219">Establezca la versión 4.5.2 de .NET Framework como la plataforma de destino para el proyecto: haga clic con el botón derecho en el proyecto y en **Propiedades** para establecer el marco de destino.</span><span class="sxs-lookup"><span data-stu-id="ab692-219">Set 4.5.2 version of .NET Framework as the target framework for your project: right-click the project, and click **Properties** to set the target framework.</span></span> <span data-ttu-id="ab692-220">Data Factory no admite actividades personalizadas que se compilaron con versiones de .NET Framework posteriores a la 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="ab692-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="ab692-221">Inicie el **Explorador de Windows** y vaya a la carpeta **bin\debug** o **bin\release**, según el tipo de compilación.</span><span class="sxs-lookup"><span data-stu-id="ab692-221">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span></span>
12. <span data-ttu-id="ab692-222">Cree un archivo ZIP **MyDotNetActivity.zip** que contenga todos los archivos binarios en la carpeta <project folder>\bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="ab692-222">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="ab692-223">Incluya el archivo **MyDotNetActivity.pdb** para ver detalles adicionales, como el número de línea en el código fuente que causó el problema, si hubo un error.</span><span class="sxs-lookup"><span data-stu-id="ab692-223">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="ab692-224">Todos los archivos incluidos en el archivo ZIP de la actividad personalizada deben estar en el **nivel superior** ; no debe haber subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="ab692-224">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>

    ![Archivos de salida binarios](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="ab692-226">Cree el contenedor de blobs **customactivitycontainer**, si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="ab692-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="ab692-227">Cargue MyDotNetActivity.zip como un blob para customactivitycontainer en una instancia de Azure Blob Storage **de uso general** (Blob Storage de acceso esporádico/no frecuente) al que AzureStorageLinkedService hace referencia.</span><span class="sxs-lookup"><span data-stu-id="ab692-227">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ab692-228">Si agrega este proyecto de actividad de .NET a una solución en Visual Studio que contenga un proyecto de Data Factory, y agrega una referencia al proyecto de actividad .NET del proyecto de la aplicación de Data Factory, no tendrá que realizar los últimos dos pasos para crear manualmente el archivo ZIP y cargarlo a la instancia de Azure Blob Storage de uso general.</span><span class="sxs-lookup"><span data-stu-id="ab692-228">If you add this .NET activity project to a solution in Visual Studio that contains a Data Factory project, and add a reference to .NET activity project from the Data Factory application project, you do not need to perform the last two steps of manually creating the zip file and uploading it to the general-purpose Azure blob storage.</span></span> <span data-ttu-id="ab692-229">Al publicar las entidades de la factoría de datos con Visual Studio el proceso de publicación realizar automáticamente estos pasos.</span><span class="sxs-lookup"><span data-stu-id="ab692-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by the publishing process.</span></span> <span data-ttu-id="ab692-230">Para obtener más información, consulte la sección [Proyecto de Data Factory en Visual Studio](#data-factory-project-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="ab692-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="ab692-231">Crear una canalización con una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="ab692-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="ab692-232">Ha creado una actividad personalizada y cargado el archivo zip con datos binarios en un contenedor de blobs en una cuenta de Azure Storage **de uso general**.</span><span class="sxs-lookup"><span data-stu-id="ab692-232">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="ab692-233">En esta sección, creará una instancia de Azure Data Factory con una canalización que usa la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-233">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="ab692-234">El conjunto de datos de entrada de la actividad personalizada representa los blobs (archivos) de la carpeta customactivityinput del contenedor adftutorial en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ab692-234">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span></span> <span data-ttu-id="ab692-235">El conjunto de datos de salida de la actividad representa los blobs de salida de la carpeta customactivityinput del contenedor adftutorial en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ab692-235">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span></span>

<span data-ttu-id="ab692-236">Cree el archivo **file.txt** con el siguiente contenido y cárguelo en la carpeta **customactivityinput** del contenedor **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="ab692-236">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span></span> <span data-ttu-id="ab692-237">Cree el contenedor adftutorial si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="ab692-237">Create the adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="ab692-238">La carpeta de entrada corresponde a un segmento de Data Factory de Azure, aunque la carpeta contenga dos, o más, archivos.</span><span class="sxs-lookup"><span data-stu-id="ab692-238">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span></span> <span data-ttu-id="ab692-239">Cuando la canalización procesa cada segmento, la actividad personalizada procesa una iteración en todos los blobs de la carpeta de entrada de dicho segmento.</span><span class="sxs-lookup"><span data-stu-id="ab692-239">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="ab692-240">Verá un archivo de salida en la carpeta adftutorial\customactivityoutput con una o varias líneas (tantas como blobs haya en la carpeta de entrada):</span><span class="sxs-lookup"><span data-stu-id="ab692-240">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="ab692-241">Estos son los pasos que se realizan en esta sección:</span><span class="sxs-lookup"><span data-stu-id="ab692-241">Here are the steps you perform in this section:</span></span>

1. <span data-ttu-id="ab692-242">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="ab692-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="ab692-243">Crear **servicios vinculados** del grupo de máquinas virtuales de Azure Batch en el que se ejecuta la actividad personalizada y la instancia de Azure Storage que contiene los blobs de entrada o salida.</span><span class="sxs-lookup"><span data-stu-id="ab692-243">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span></span>
3. <span data-ttu-id="ab692-244">Crear **conjuntos de datos** de entrada y salida que representan la entrada y salida de la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-244">Create input and output **datasets** that represent input and output of the custom activity.</span></span>
4. <span data-ttu-id="ab692-245">Crear una **canalización** que usa la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-245">Create a **pipeline** that uses the custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="ab692-246">Cree el archivo **file.txt** y cárguelo en un contenedor de blobs, si no lo ha hecho aún.</span><span class="sxs-lookup"><span data-stu-id="ab692-246">Create the **file.txt** and upload it to a blob container if you haven't already done so.</span></span> <span data-ttu-id="ab692-247">Consulte las instrucciones de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="ab692-247">See instructions in the preceding section.</span></span>   

### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="ab692-248">Paso 1: Creación de la factoría de datos</span><span class="sxs-lookup"><span data-stu-id="ab692-248">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="ab692-249">Tras iniciar sesión en Azure Portal, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ab692-249">After logging in to the Azure portal, do the following steps:</span></span>
   1. <span data-ttu-id="ab692-250">Haga clic en **NUEVO** en el menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="ab692-250">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="ab692-251">Haga clic en **Datos y análisis** en la hoja **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="ab692-251">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="ab692-252">Haga clic en **Factoría de datos** en la hoja **Análisis de datos**.</span><span class="sxs-lookup"><span data-stu-id="ab692-252">Click **Data Factory** on the **Data analytics** blade.</span></span>
   
    ![Nuevo menú de Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="ab692-254">En la hoja **Nueva factoría de datos**, escriba **CustomActivityFactory** en el campo Nombre.</span><span class="sxs-lookup"><span data-stu-id="ab692-254">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="ab692-255">El nombre del generador de datos de Azure debe ser único global.</span><span class="sxs-lookup"><span data-stu-id="ab692-255">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="ab692-256">Si recibe el error: **El nombre "CustomActivityFactory" de factoría de datos no está disponible**, cambie el nombre de la factoría de datos (por ejemplo, **suNombreCustomActivityFactory**) e intente crearla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ab692-256">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Nueva hoja de Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="ab692-258">Haga clic en **NOMBRE DEL GRUPO DE RECURSOS**y seleccione un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="ab692-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="ab692-259">Compruebe que usa la **suscripción** y la **región** correctas en las que desea que se cree la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ab692-259">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="ab692-260">Haga clic en **Crear** en la hoja **Nueva fábrica de datos**.</span><span class="sxs-lookup"><span data-stu-id="ab692-260">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="ab692-261">Verá la factoría de datos que se crea en el **Panel** del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-261">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="ab692-262">Una vez que la factoría de datos se ha creado correctamente, verá la hoja Data Factory, donde se muestra su contenido.</span><span class="sxs-lookup"><span data-stu-id="ab692-262">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span></span>
    
    ![Hoja de la Factoría de datos](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="ab692-264">Paso 2: Creación de servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="ab692-264">Step 2: Create linked services</span></span>
<span data-ttu-id="ab692-265">Los servicios vinculados vinculan almacenes de datos o servicios de proceso con una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-265">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="ab692-266">En este paso, vinculará su cuenta de Almacenamiento de Azure y la cuenta de Lote de Azure con su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ab692-266">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ab692-267">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ab692-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="ab692-268">Haga clic en el icono **Crear e implementar** de la hoja **FACTORÍA DE DATOS** de **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="ab692-268">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="ab692-269">Aparecerá Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="ab692-269">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="ab692-270">Haga clic en **Nuevo almacén de datos** en la barra de comandos y elija **Almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="ab692-270">Click **New data store** on the command bar and choose **Azure storage**.</span></span> <span data-ttu-id="ab692-271">Debería ver el script JSON para crear un servicio vinculado de Almacenamiento de Azure en el editor.</span><span class="sxs-lookup"><span data-stu-id="ab692-271">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>
    
    ![Nuevo almacén de datos: Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="ab692-273">Reemplace `<accountname>` por el nombre de la cuenta de Azure Storage y `<accountkey>` por la clave de acceso de la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab692-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span></span> <span data-ttu-id="ab692-274">Para aprender a obtener una clave de acceso de almacenamiento, consulte [Acerca de las cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ab692-274">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Servicio vinculado de Azure Storage](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="ab692-276">Haga clic en **Implementar** en la barra de comandos para implementar el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ab692-276">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="ab692-277">Creación del servicio vinculado de Lote de Azure</span><span class="sxs-lookup"><span data-stu-id="ab692-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="ab692-278">En Data Factory Editor, haga clic en **... Más** en la barra de comandos, haga clic en **Nuevo proceso** y luego seleccione **Azure Batch** en el menú.</span><span class="sxs-lookup"><span data-stu-id="ab692-278">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span></span>

    ![Nuevo proceso: Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="ab692-280">Realice los siguientes cambios en el script JSON:</span><span class="sxs-lookup"><span data-stu-id="ab692-280">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="ab692-281">Especifique el nombre de cuenta de Lote de Azure en la propiedad **accountName** .</span><span class="sxs-lookup"><span data-stu-id="ab692-281">Specify Azure Batch account name for the **accountName** property.</span></span> <span data-ttu-id="ab692-282">La **dirección URL** de la **hoja de la cuenta de Azure Batch** tiene el formato siguiente: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ab692-282">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="ab692-283">Para la propiedad **batchUri** en JSON, tiene que quitar `accountname.` de la dirección URL y usar `accountname` para la propiedad JSON `accountName`.</span><span class="sxs-lookup"><span data-stu-id="ab692-283">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span></span>
   2. <span data-ttu-id="ab692-284">Especifique la clave de cuenta de Lote de Azure en la propiedad **accessKey** .</span><span class="sxs-lookup"><span data-stu-id="ab692-284">Specify the Azure Batch account key for the **accessKey** property.</span></span>
   3. <span data-ttu-id="ab692-285">Especifique el nombre del grupo que creó como parte de los requisitos previos en la propiedad **poolName**.</span><span class="sxs-lookup"><span data-stu-id="ab692-285">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span></span> <span data-ttu-id="ab692-286">También puede especificar el id. del grupo, en lugar del nombre.</span><span class="sxs-lookup"><span data-stu-id="ab692-286">You can also specify the ID of the pool instead of the name of the pool.</span></span>
   4. <span data-ttu-id="ab692-287">Especifique el URI de Lote de Azure en la propiedad **batchUri** .</span><span class="sxs-lookup"><span data-stu-id="ab692-287">Specify Azure Batch URI for the **batchUri** property.</span></span> <span data-ttu-id="ab692-288">Ejemplo: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ab692-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="ab692-289">Especifique el servicio **AzureStorageLinkedService** for the **linkedServiceName** .</span><span class="sxs-lookup"><span data-stu-id="ab692-289">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="ab692-290">En la propiedad **poolName** , también puede especificar el identificador del grupo, en lugar del nombre del grupo.</span><span class="sxs-lookup"><span data-stu-id="ab692-290">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="ab692-291">El servicio de Factoría de datos no admite una opción a petición para el Lote de Azure como lo hace para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-291">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="ab692-292">Solo puede usar su propio grupo de Lote de Azure en una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="ab692-293">Paso 3: Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="ab692-293">Step 3: Create datasets</span></span>
<span data-ttu-id="ab692-294">En este paso, crea conjuntos de datos que representan los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="ab692-294">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="ab692-295">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="ab692-295">Create input dataset</span></span>
1. <span data-ttu-id="ab692-296">En el **Editor** en la instancia de Data Factory, haga clic en **... Más** en la barra de comandos y luego en **Nuevo conjunto de datos** y después, seleccione **Azure Blob Storage** desde el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="ab692-296">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="ab692-297">Reemplace el script JSON del panel derecho por el siguiente fragmento de código JSON:</span><span class="sxs-lookup"><span data-stu-id="ab692-297">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
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

   <span data-ttu-id="ab692-298">Más adelante, en este mismo tutorial, creará una canalización con la hora de inicio 2016-11-16T00:00:00Z y la de finalización 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="ab692-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="ab692-299">Está programada para generar datos cada hora, por lo que hay cinco segmentos de entrada o salida (entre **00**:00:00 -> **05**:00:00).</span><span class="sxs-lookup"><span data-stu-id="ab692-299">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="ab692-300">Los valores de **frequency** e **interval** del conjunto de datos de entrada se establecen en **Hour** y **1** respectivamente, lo que significa que el segmento de entrada está disponible cada hora.</span><span class="sxs-lookup"><span data-stu-id="ab692-300">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span> <span data-ttu-id="ab692-301">En este ejemplo, es el mismo archivo (file.txt) de la carpeta de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab692-301">In this sample, it is the same file (file.txt) in the intputfolder.</span></span>

   <span data-ttu-id="ab692-302">Estas son las horas de inicio de cada segmento, que se representa mediante la variable de sistema SliceStart en el fragmento de código JSON anterior.</span><span class="sxs-lookup"><span data-stu-id="ab692-302">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span></span>
3. <span data-ttu-id="ab692-303">Haga clic en **Implementar** en la barra de herramientas para crear e implementar **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ab692-303">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span></span> <span data-ttu-id="ab692-304">Confirme que aparece el mensaje **TABLA CREADA CORRECTAMENTE** en la barra de título del Editor.</span><span class="sxs-lookup"><span data-stu-id="ab692-304">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="ab692-305">Crear un conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="ab692-305">Create an output dataset</span></span>
1. <span data-ttu-id="ab692-306">En el **Data Factory Editor**, haga clic en **... Más** en la barra de comandos, haga clic en **Nuevo conjunto de datos** y después seleccione **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="ab692-306">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="ab692-307">Reemplace el script JSON en el panel derecho con el siguiente script JSON:</span><span class="sxs-lookup"><span data-stu-id="ab692-307">Replace the JSON script in the right pane with the following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
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

     <span data-ttu-id="ab692-308">La ubicación de salida es **adftutorial/customactivityoutput/** y el nombre del archivo de salida, yyyy-MM-dd-HH.txt, donde yyyy-MM-dd-HH es el año, el mes, el día y la hora del segmento que se está generando.</span><span class="sxs-lookup"><span data-stu-id="ab692-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span></span> <span data-ttu-id="ab692-309">Consulte la [Referencia para desarrolladores][adf-developer-reference] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ab692-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="ab692-310">Se genera un blob o archivo de salida para cada segmento de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab692-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="ab692-311">Así es cómo se asigna el nombre al archivo de salida de cada segmento.</span><span class="sxs-lookup"><span data-stu-id="ab692-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="ab692-312">Todos los archivos de salida se generan en una carpeta de salida: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="ab692-312">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="ab692-313">Segmento</span><span class="sxs-lookup"><span data-stu-id="ab692-313">Slice</span></span> | <span data-ttu-id="ab692-314">Hora de inicio</span><span class="sxs-lookup"><span data-stu-id="ab692-314">Start time</span></span> | <span data-ttu-id="ab692-315">Archivo de salida</span><span class="sxs-lookup"><span data-stu-id="ab692-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="ab692-316">1</span><span class="sxs-lookup"><span data-stu-id="ab692-316">1</span></span> |<span data-ttu-id="ab692-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="ab692-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="ab692-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="ab692-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="ab692-319">2</span><span class="sxs-lookup"><span data-stu-id="ab692-319">2</span></span> |<span data-ttu-id="ab692-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="ab692-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="ab692-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="ab692-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="ab692-322">3</span><span class="sxs-lookup"><span data-stu-id="ab692-322">3</span></span> |<span data-ttu-id="ab692-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="ab692-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="ab692-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="ab692-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="ab692-325">4</span><span class="sxs-lookup"><span data-stu-id="ab692-325">4</span></span> |<span data-ttu-id="ab692-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="ab692-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="ab692-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="ab692-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="ab692-328">5</span><span class="sxs-lookup"><span data-stu-id="ab692-328">5</span></span> |<span data-ttu-id="ab692-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="ab692-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="ab692-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="ab692-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="ab692-331">Recuerde que todos los archivos de una carpeta de entrada forman parte de un segmento con las horas de inicio mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab692-331">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span></span> <span data-ttu-id="ab692-332">Cuando se procesa este segmento, la actividad personalizada examinan todos los archivos y produce una línea en el archivo de salida con el número de apariciones del término de búsqueda ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="ab692-332">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="ab692-333">Si hay tres archivos en inputfolder, hay tres líneas en el archivo de salida para cada segmento horario: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span><span class="sxs-lookup"><span data-stu-id="ab692-333">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="ab692-334">Para implementar **OutputDataset**, haga clic en **Implementar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="ab692-334">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a><span data-ttu-id="ab692-335">Creación y ejecución de una canalización que usa la actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="ab692-335">Create and run a pipeline that uses the custom activity</span></span>
1. <span data-ttu-id="ab692-336">En Data Factory Editor, haga clic en **... Más** y luego seleccione **Nueva canalización** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="ab692-336">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span></span> 
2. <span data-ttu-id="ab692-337">Reemplace el script JSON del panel derecho con el siguiente script JSON:</span><span class="sxs-lookup"><span data-stu-id="ab692-337">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="ab692-338">Tenga en cuenta los siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="ab692-338">Note the following points:</span></span>

   * <span data-ttu-id="ab692-339">**Concurrency** se establece en **2** para que dos máquinas virtuales del grupo de Azure Batch procesen dos segmentos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="ab692-339">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span></span>
   * <span data-ttu-id="ab692-340">Hay una actividad en la sección de actividades y es de tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="ab692-340">There is one activity in the activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="ab692-341">**AssemblyName** se establece en el nombre del archivo DLL, **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="ab692-341">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="ab692-342">**EntryPoint** se establece **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="ab692-342">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="ab692-343">**PackageLinkedService** se establece en **AzureStorageLinkedService**, que apunta al almacenamiento de blobs que contiene el archivo ZIP de la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-343">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="ab692-344">Si usa diferentes cuentas de Almacenamiento de Azure para los archivos de entrada y salida y el archivo ZIP de actividad personalizada, tiene que crear otro servicio vinculado a Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-344">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="ab692-345">En este artículo, se da por supuesto que usa la misma cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-345">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="ab692-346">**PackageFile** se establece en **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="ab692-346">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="ab692-347">Está en el formato <contenedorDelZIP>/<nombreDelZIP.zip>.</span><span class="sxs-lookup"><span data-stu-id="ab692-347">It is in the format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="ab692-348">La actividad personalizada toma **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="ab692-348">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="ab692-349">La propiedad linkedServiceName de la actividad personalizada apunta a **AzureBatchLinkedService**, que indica a Data Factory de Azure que la actividad personalizada debe ejecutarse en Lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-349">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span></span>
   * <span data-ttu-id="ab692-350">**isPaused** se establece en **false** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ab692-350">**isPaused** property is set to **false** by default.</span></span> <span data-ttu-id="ab692-351">La canalización se ejecuta inmediatamente en este ejemplo, ya que los segmentos se inician en el pasado.</span><span class="sxs-lookup"><span data-stu-id="ab692-351">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="ab692-352">Esta propiedad se puede establecer en true para pausar la canalización y se puede volver a establecer en false para reiniciarla.</span><span class="sxs-lookup"><span data-stu-id="ab692-352">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>
   * <span data-ttu-id="ab692-353">Hay una diferencia de **cinco** horas entre la hora de **inicio** y la de **finalización**, y los segmentos se producen cada hora, por lo que la canalización produce cinco segmentos.</span><span class="sxs-lookup"><span data-stu-id="ab692-353">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>
3. <span data-ttu-id="ab692-354">Haga clic en **Implementar** en la barra de comandos para implementar la canalización.</span><span class="sxs-lookup"><span data-stu-id="ab692-354">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-the-pipeline"></a><span data-ttu-id="ab692-355">Supervisar la canalización</span><span class="sxs-lookup"><span data-stu-id="ab692-355">Monitor the pipeline</span></span>
1. <span data-ttu-id="ab692-356">En la hoja Data Factory del Portal de Azure, haga clic en **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="ab692-356">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

    ![Icono Diagrama](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="ab692-358">En la vista Diagrama, haga clic en OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="ab692-358">In the Diagram View, now click the OutputDataset.</span></span>

    ![Vista de diagrama](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="ab692-360">Debería ver que los cinco segmentos están en estado Listo.</span><span class="sxs-lookup"><span data-stu-id="ab692-360">You should see that the five output slices are in the Ready state.</span></span> <span data-ttu-id="ab692-361">Si no están en estado Listo, aún no se han producido.</span><span class="sxs-lookup"><span data-stu-id="ab692-361">If they are not in the Ready state, they haven't been produced yet.</span></span> 

   ![Segmentos de salida](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="ab692-363">Compruebe que los archivos de salida se generan en el almacenamiento de blobs del contenedor **adftutorial** .</span><span class="sxs-lookup"><span data-stu-id="ab692-363">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span></span>

   ![salida de la actividad personalizada][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="ab692-365">Si abre el archivo de salida, debería ver un resultado similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab692-365">If you open the output file, you should see the output similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="ab692-366">Use [Azure Portal][azure-preview-portal] o los cmdlets de Azure PowerShell para supervisar la factoría de datos, las canalizaciones y los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="ab692-366">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="ab692-367">Puede ver mensajes desde **ActivityLogger** en el código de la actividad personalizada en los registros (de forma específica user-0.log) que puede descargar desde el portal o con cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ab692-367">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span></span>

   ![registros de descarga de la actividad personalizada][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="ab692-369">Consulte [Supervisión y administración de canalizaciones de la Factoría de datos de Azure](data-factory-monitor-manage-pipelines.md) para obtener información detallada sobre los pasos que hay que seguir para supervisar los conjuntos de datos y las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="ab692-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="ab692-370">Proyecto de Data Factory en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ab692-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="ab692-371">Puede crear y publicar entidades de Data Factory usando Visual Studio en lugar de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ab692-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="ab692-372">Para obtener información sobre la creación y publicación de entidades de Data Factory mediante Visual Studio, consulte los artículos [Build your first pipeline using Visual Studio (Compilar la primera canalización mediante Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) y [Copy data from Azure Blob to Azure SQL (Copiar datos de Azure Blob a Azure SQL)](data-factory-copy-activity-tutorial-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ab692-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob to Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="ab692-373">Si crea el proyecto de Data Factory en Visual Studio, realice los siguientes pasos adicionales:</span><span class="sxs-lookup"><span data-stu-id="ab692-373">Do the following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="ab692-374">Agregue el proyecto de Data Factory a la solución de Visual Studio que contiene el proyecto de la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-374">Add the Data Factory project to the Visual Studio solution that contains the custom activity project.</span></span> 
2. <span data-ttu-id="ab692-375">Agregue una referencia al proyecto de la actividad de .NET desde el proyecto de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab692-375">Add a reference to the .NET activity project from the Data Factory project.</span></span> <span data-ttu-id="ab692-376">Haga clic con el botón derecho en el proyecto de Data Factory, seleccione **Agregar** y, a continuación, haga clic en **Referencia**.</span><span class="sxs-lookup"><span data-stu-id="ab692-376">Right-click Data Factory project, point to **Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="ab692-377">En el cuadro de diálogo **Agregar referencia**, seleccione el proyecto **MyDotNetActivity** y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ab692-377">In the **Add Reference** dialog box, select the **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="ab692-378">Compilar y publicar la solución.</span><span class="sxs-lookup"><span data-stu-id="ab692-378">Build and publish the solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ab692-379">Cuando publica las entidades de Data Factory, se crea un archivo ZIP automáticamente y se carga en el contenedor de blobs: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="ab692-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded to the blob container: customactivitycontainer.</span></span> <span data-ttu-id="ab692-380">Si no existe el contenedor de blobs, también se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ab692-380">If the blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="ab692-381">Integración de Data Factory y Lote</span><span class="sxs-lookup"><span data-stu-id="ab692-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="ab692-382">El servicio Data Factory crea un trabajo en Azure Batch con el nombre **adf-poolname: job-xxx**.</span><span class="sxs-lookup"><span data-stu-id="ab692-382">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="ab692-383">Haga clic en **Trabajos** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="ab692-383">Click **Jobs** from the left menu.</span></span> 

![Data Factory de Azure: trabajos por lotes](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="ab692-385">Se crea una tarea para cada ejecución de actividad de un segmento.</span><span class="sxs-lookup"><span data-stu-id="ab692-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="ab692-386">Si hay cinco segmentos listos para ser procesados, se crean cinco tareas de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="ab692-386">If there are five slices ready to be processed, five tasks are created in this job.</span></span> <span data-ttu-id="ab692-387">Si hay varios nodos de proceso en el grupo de Batch, se pueden ejecutar dos o más segmentos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="ab692-387">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="ab692-388">También puede haber más de un segmento en ejecución en el mismo proceso si el número máximo de tareas se establece un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="ab692-388">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span></span>

![Data Factory de Azure: tareas de trabajos por lotes](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="ab692-390">En el diagrama siguiente se ilustra la relación entre las tareas de Data Factory de Azure y Lote.</span><span class="sxs-lookup"><span data-stu-id="ab692-390">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span></span>

![Factoría de datos y Lote](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="ab692-392">Solución de errores</span><span class="sxs-lookup"><span data-stu-id="ab692-392">Troubleshoot failures</span></span>
<span data-ttu-id="ab692-393">La solución de problemas se compone de varias técnicas básicas:</span><span class="sxs-lookup"><span data-stu-id="ab692-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="ab692-394">Si ve el siguiente error, puede que esté usando una instancia de Blob Storage activa o de acceso esporádico en lugar de usar una de uso general.</span><span class="sxs-lookup"><span data-stu-id="ab692-394">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="ab692-395">Cargue el archivo zip en una **cuenta de Azure Storage de uso general**.</span><span class="sxs-lookup"><span data-stu-id="ab692-395">Upload the zip file to a **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="ab692-396">Si aparece el siguiente error, confirme que el nombre de la clase en el archivo CS coincide con el nombre especificado para la propiedad **EntryPoint** en el JSON de la canalización.</span><span class="sxs-lookup"><span data-stu-id="ab692-396">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span></span> <span data-ttu-id="ab692-397">En el tutorial, el nombre de la clase es MyDotNetActivity y la propiedad EntryPoint en el código JSON es MyDotNetActivityNS.**MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="ab692-397">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="ab692-398">Si los nombres coinciden, confirme que todos los archivos binarios se encuentran en la **carpeta raíz** del archivo zip.</span><span class="sxs-lookup"><span data-stu-id="ab692-398">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span></span> <span data-ttu-id="ab692-399">Es decir, cuando abra el archivo zip verá todos los archivos de la carpeta raíz, pero no los que están en las subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="ab692-399">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="ab692-400">Si el segmento de entrada no está establecido en **Listo**, confirme que la estructura de la carpeta de entrada es correcta y que **file.txt** se encuentra en las carpetas de entrada.</span><span class="sxs-lookup"><span data-stu-id="ab692-400">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span></span>
3. <span data-ttu-id="ab692-401">En el método **Execute** de la actividad personalizada, use el objeto **IActivityLogger** para registrar información que ayude a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="ab692-401">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="ab692-402">Los mensajes registrados se muestran en los archivos de registro del usuario (uno o varios archivos llamados user-0.log, user-1.log, user-2.log, etc.).</span><span class="sxs-lookup"><span data-stu-id="ab692-402">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="ab692-403">En la hoja **OutputDataset**, haga clic en el segmento para ver la hoja **SEGMENTO DE DATOS** de dicho segmento.</span><span class="sxs-lookup"><span data-stu-id="ab692-403">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="ab692-404">Verá **ejecuciones de actividad** para ese segmento.</span><span class="sxs-lookup"><span data-stu-id="ab692-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="ab692-405">Debería ver una ejecución de actividad del segmento.</span><span class="sxs-lookup"><span data-stu-id="ab692-405">You should see one activity run for the slice.</span></span> <span data-ttu-id="ab692-406">Si hace clic en Ejecutar en la barra de comandos, podrá iniciar otra ejecución de actividad en el mismo segmento.</span><span class="sxs-lookup"><span data-stu-id="ab692-406">If you click Run in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="ab692-407">Al hacer clic en la ejecución de actividad, verá la hoja **DETALLES DE LA EJECUCIÓN DE ACTIVIDAD** con una lista de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="ab692-407">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="ab692-408">Los mensajes registrados se encuentran en el archivo user_0.log.</span><span class="sxs-lookup"><span data-stu-id="ab692-408">You see logged messages in the user_0.log file.</span></span> <span data-ttu-id="ab692-409">Si se produce un error, verá tres ejecuciones de actividad, ya que el número de reintentos está establecido en 3 en la canalización o actividad JSON.</span><span class="sxs-lookup"><span data-stu-id="ab692-409">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="ab692-410">Al hacer clic en la ejecución de actividad, verá los archivos de registro que puede revisar para solucionar el error.</span><span class="sxs-lookup"><span data-stu-id="ab692-410">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   <span data-ttu-id="ab692-411">En la lista de archivos de registro, haga clic en **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="ab692-411">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="ab692-412">En el panel derecho, se encuentran los resultados del uso del método **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="ab692-412">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span> <span data-ttu-id="ab692-413">Si no ve todos los mensajes, compruebe si tiene más archivos de registro llamados user_1.log, user_2.log, etc. De lo contrario, es posible que el código haya generado algún error tras el último mensaje registrado.</span><span class="sxs-lookup"><span data-stu-id="ab692-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span></span>

   <span data-ttu-id="ab692-414">Además, consulte **system-0.log** para ver si hay alguna excepción o mensaje de error del sistema.</span><span class="sxs-lookup"><span data-stu-id="ab692-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="ab692-415">Incluya el archivo **PDB** en el archivo ZIP para que los detalles sobre un error contengan información como la **pila de llamadas** cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="ab692-415">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="ab692-416">Todos los archivos incluidos en el archivo ZIP de la actividad personalizada deben estar en el **nivel superior** ; no debe haber subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="ab692-416">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>
6. <span data-ttu-id="ab692-417">Asegúrese de que en **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip) y **packageLinkedService** (debe apuntar a la instancia de Azure Blob Storage **de uso general** que contiene el archivo ZIP) se han seleccionado los valores correctos.</span><span class="sxs-lookup"><span data-stu-id="ab692-417">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span></span>
7. <span data-ttu-id="ab692-418">Si corrigió algún error y desea volver a procesar el segmento, haga clic con el botón derecho en el segmento, en la hoja **OutputDataset**, y haga clic en **Run**.</span><span class="sxs-lookup"><span data-stu-id="ab692-418">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="ab692-419">Si ve el error siguiente, significa que está usando la versión 4.3.0 o posterior del paquete de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab692-419">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="ab692-420">El iniciador del servicio Data Factory requiere la versión 4.3 de WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="ab692-420">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="ab692-421">Consulte la sección [Aislamiento de AppDomain](#appdomain-isolation) para ver una solución alternativa si tiene que utilizar la versión más reciente del ensamblado de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ab692-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="ab692-422">Si puede usar la versión 4.3.0 del paquete de Azure Storage, quite la referencia al paquete de Azure.Storage de la versión 4.3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ab692-422">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="ab692-423">A continuación ejecute el siguiente comando de la Consola del administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="ab692-423">Then, run the following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="ab692-424">Compile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="ab692-424">Build the project.</span></span> <span data-ttu-id="ab692-425">Elimine la carpeta bin\Debug del ensamblado Azure.Storage de la versión 4.3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="ab692-425">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span></span> <span data-ttu-id="ab692-426">Cree un archivo .zip con los datos binarios y el archivo PDB.</span><span class="sxs-lookup"><span data-stu-id="ab692-426">Create a zip file with binaries and the PDB file.</span></span> <span data-ttu-id="ab692-427">Reemplace el antiguo archivo .zip por este otro en el contenedor de blobs (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="ab692-427">Replace the old zip file with this one in the blob container (customactivitycontainer).</span></span> <span data-ttu-id="ab692-428">Vuelva a ejecutar los segmentos con errores (haga clic con el botón derecho en el segmento y, después, haga clic en Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="ab692-428">Rerun the slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="ab692-429">La actividad personalizada no utiliza el archivo **app.config** desde el paquete.</span><span class="sxs-lookup"><span data-stu-id="ab692-429">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="ab692-430">Por lo tanto, si el código lee cualquier cadena de conexión del archivo de configuración, no funcionará en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ab692-430">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="ab692-431">El procedimiento recomendado al usar Azure Batch consiste en conservar los secretos en una instancia de **Azure Key Vault**, usar una entidad de servicio basada en certificados para proteger el **almacén de claves** y distribuir el certificado al grupo de Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="ab692-431">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="ab692-432">Tras ello, la actividad personalizada de .NET podrá acceder a los secretos desde el almacén de claves en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ab692-432">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="ab692-433">Esta es una solución genérica y se puede extrapolar a cualquier tipo de secreto, no solo a cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="ab692-433">This solution is a generic solution and can scale to any type of secret, not just connection string.</span></span>

   <span data-ttu-id="ab692-434">Existe una solución más sencilla, pero no es un procedimiento recomendado: puede crear un **servicio vinculado de SQL Azure** con configuración de cadena de conexión, crear un conjunto de datos que utilice el servicio vinculado y vincular el conjunto de datos (configurado con carácter de entrada ficticio) con la actividad de .NET personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="ab692-435">Tras ello, podrá acceder a la cadena de conexión del servicio vinculado del código de la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-435">You can then access the linked service's connection string in the custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="ab692-436">Actualización de una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="ab692-436">Update custom activity</span></span>
<span data-ttu-id="ab692-437">Si actualiza el código de la actividad personalizada, compílelo y cargue el archivo comprimido que contiene los nuevos binarios en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="ab692-437">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="ab692-438">Aislamiento de AppDomain</span><span class="sxs-lookup"><span data-stu-id="ab692-438">Appdomain isolation</span></span>
<span data-ttu-id="ab692-439">Consulte el [ejemplo Cross AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample), que muestra cómo crear una actividad personalizada que no esté restringida a las versiones de ensamblado que utiliza el iniciador de Data Factory (por ejemplo, WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span><span class="sxs-lookup"><span data-stu-id="ab692-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="ab692-440">Acceso a las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="ab692-440">Access extended properties</span></span>
<span data-ttu-id="ab692-441">Puede declarar propiedades extendidas en el JSON de actividad como se muestra en el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab692-441">You can declare extended properties in the activity JSON as shown in the following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="ab692-442">En el ejemplo, hay dos propiedades extendidas: **SliceStart** y **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="ab692-442">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="ab692-443">El valor de SliceStart se basa en la variable del sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="ab692-443">The value for SliceStart is based on the SliceStart system variable.</span></span> <span data-ttu-id="ab692-444">Consulte el artículo sobre las [variables del sistema](data-factory-functions-variables.md) para ver una lista de las variables del sistema admitidas.</span><span class="sxs-lookup"><span data-stu-id="ab692-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="ab692-445">El valor de DataFactoryName está incrustado directamente en CustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="ab692-445">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span></span>

<span data-ttu-id="ab692-446">Para acceder a estas propiedades extendidas en el método **Execute** , use código similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab692-446">To access these extended properties in the **Execute** method, use code similar to the following code:</span></span>

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="ab692-447">Escalado automático de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="ab692-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="ab692-448">También puede crear un grupo de Lote de Azure con la característica **autoescala** .</span><span class="sxs-lookup"><span data-stu-id="ab692-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="ab692-449">Por ejemplo, podría crear un grupo de Azure Batch con 0 VM dedicadas y una fórmula de escalado automático basada en el número de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="ab692-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="ab692-450">La fórmula del ejemplo logra el siguiente comportamiento: cuando el grupo se crea inicialmente, empieza con 1 VM.</span><span class="sxs-lookup"><span data-stu-id="ab692-450">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="ab692-451">La métrica $PendingTasks define el número de tareas que están en ejecución o activas (en cola).</span><span class="sxs-lookup"><span data-stu-id="ab692-451">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="ab692-452">La fórmula busca el número promedio de tareas pendientes en los últimos 180 segundos y establece TargetDedicated en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="ab692-452">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="ab692-453">Garantiza que TargetDedicated nunca supera las 25 VM.</span><span class="sxs-lookup"><span data-stu-id="ab692-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="ab692-454">Por tanto, a medida que se envían nuevas tareas, el grupo crece automáticamente y a medida que estás se completan, las VM se liberan una a una y el escalado automático las reduce.</span><span class="sxs-lookup"><span data-stu-id="ab692-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="ab692-455">startingNumberOfVMs y maxNumberofVMs se pueden adaptar a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="ab692-455">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="ab692-456">Fórmula de escalado automático:</span><span class="sxs-lookup"><span data-stu-id="ab692-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="ab692-457">Para más información, consulte [Escalado automático de los nodos de proceso en un grupo de Lote de Azure](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="ab692-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="ab692-458">Si el grupo usa el valor predeterminado de la propiedad [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), el servicio Lote puede tardar de 15 a 30 minutos en preparar la máquina virtual antes de ejecutar la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-458">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="ab692-459">Si el grupo usa otro valor de autoScaleEvaluationInterval diferente, el servicio Lote podría tardar el valor de autoScaleEvaluationInterval más 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="ab692-459">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="ab692-460">Uso del servicio de proceso de HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab692-460">Use HDInsight compute service</span></span>
<span data-ttu-id="ab692-461">En el tutorial, ha utilizado el proceso Lotes de Azure para ejecutar la actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="ab692-461">In the walkthrough, you used Azure Batch compute to run the custom activity.</span></span> <span data-ttu-id="ab692-462">También puede utilizar su propio clúster de HDInsight basado en Windows o hacer que Data Factory cree un clúster de HDInsight basado en Windows a petición y configurar la actividad personalizada para que se ejecute en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have the custom activity run on the HDInsight cluster.</span></span> <span data-ttu-id="ab692-463">Estos son los pasos de alto nivel para usar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-463">Here are the high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab692-464">Las actividades personalizadas de .NET se ejecutan solo en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="ab692-464">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ab692-465">Una solución alternativa para esta limitación consiste en usar la actividad MapReduce para ejecutar código personalizado de Java en un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="ab692-465">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ab692-466">Otra opción es usar un grupo de máquinas virtuales de Azure Batch para ejecutar actividades personalizadas en lugar de utilizar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-466">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="ab692-467">Cree un servicio vinculado de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab692-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="ab692-468">Utilice el servicio vinculado de HDInsight en lugar de **AzureBatchLinkedService** en el JSON de la canalización.</span><span class="sxs-lookup"><span data-stu-id="ab692-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span></span>

<span data-ttu-id="ab692-469">Si desea probarlo en el tutorial, cambie las horas de **inicio** y **finalización** de la canalización para poder probar el escenario con el servicio Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-469">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="ab692-470">Creación de un servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="ab692-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="ab692-471">El servicio Factoría de datos de Azure admite la creación de un clúster a petición y usarlo para procesar la entrada para generar datos de salida.</span><span class="sxs-lookup"><span data-stu-id="ab692-471">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span></span> <span data-ttu-id="ab692-472">También puede utilizar su propio clúster para realizar la misma tarea.</span><span class="sxs-lookup"><span data-stu-id="ab692-472">You can also use your own cluster to perform the same.</span></span> <span data-ttu-id="ab692-473">Cuando se utiliza el clúster de HDInsight a petición, se crea un clúster para cada sector.</span><span class="sxs-lookup"><span data-stu-id="ab692-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="ab692-474">Mientras que, si utiliza su propio clúster de HDInsight, el clúster está preparado para procesar el sector inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="ab692-474">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span></span> <span data-ttu-id="ab692-475">Por lo tanto, cuando utilice el clúster a petición, es posible que no vea los datos de salida tan rápido como cuando utilice su propio clúster.</span><span class="sxs-lookup"><span data-stu-id="ab692-475">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ab692-476">En tiempo de ejecución, una instancia de una actividad de .NET solo se ejecuta en un nodo de trabajo en el clúster de HDInsight; no se puede escalar para que se ejecute en varios nodos.</span><span class="sxs-lookup"><span data-stu-id="ab692-476">At runtime, an instance of a .NET activity runs only on one worker node in the HDInsight cluster; it cannot be scaled to run on multiple nodes.</span></span> <span data-ttu-id="ab692-477">Se pueden ejecutar en paralelo varias instancias de actividad de .NET en distintos nodos del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-477">Multiple instances of .NET activity can run in parallel on different nodes of the HDInsight cluster.</span></span>
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="ab692-478">Para utilizar un clúster de HDInsight a petición</span><span class="sxs-lookup"><span data-stu-id="ab692-478">To use an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="ab692-479">En el **Portal de Azure**, haga clic en **Crear e implementar** en la página principal de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab692-479">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="ab692-480">En el Editor de Data Factory, haga clic en **Nuevo proceso** en la barra de comandos y seleccione **On-demand HDInsight cluster** (Clúster de HDInsight a petición) en el menú.</span><span class="sxs-lookup"><span data-stu-id="ab692-480">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="ab692-481">Realice los siguientes cambios en el script JSON:</span><span class="sxs-lookup"><span data-stu-id="ab692-481">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="ab692-482">En la propiedad **clusterSize** , especifique el tamaño del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-482">For the **clusterSize** property, specify the size of the HDInsight cluster.</span></span>
   2. <span data-ttu-id="ab692-483">En la propiedad **timeToLive** , especifique cuánto tiempo el clúster puede estar inactivo antes de que se elimine.</span><span class="sxs-lookup"><span data-stu-id="ab692-483">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="ab692-484">En la propiedad **version** , especifique la versión de HDInsight que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="ab692-484">For the **version** property, specify the HDInsight version you want to use.</span></span> <span data-ttu-id="ab692-485">Si excluye esta propiedad, se usa la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="ab692-485">If you exclude this property, the latest version is used.</span></span>  
   4. <span data-ttu-id="ab692-486">En **linkedServiceName**, especifique **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ab692-486">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="ab692-487">Las actividades personalizadas de .NET se ejecutan solo en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="ab692-487">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ab692-488">Una solución alternativa para esta limitación consiste en usar la actividad MapReduce para ejecutar código personalizado de Java en un clúster de HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="ab692-488">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ab692-489">Otra opción es usar un grupo de máquinas virtuales de Azure Batch para ejecutar actividades personalizadas en lugar de utilizar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-489">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="ab692-490">Haga clic en **Implementar** en la barra de comandos para implementar el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ab692-490">Click **Deploy** on the command bar to deploy the linked service.</span></span>

##### <a name="to-use-your-own-hdinsight-cluster"></a><span data-ttu-id="ab692-491">Para utilizar su propio clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ab692-491">To use your own HDInsight cluster:</span></span>
1. <span data-ttu-id="ab692-492">En el **Portal de Azure**, haga clic en **Crear e implementar** en la página principal de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab692-492">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="ab692-493">En el **Editor de Data Factory**, haga clic en **Nuevo proceso** en la barra de comandos y seleccione **Clúster de HDInsight** en el menú.</span><span class="sxs-lookup"><span data-stu-id="ab692-493">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="ab692-494">Realice los siguientes cambios en el script JSON:</span><span class="sxs-lookup"><span data-stu-id="ab692-494">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="ab692-495">En la propiedad **clusterUri** , especifique la dirección URL para su HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-495">For the **clusterUri** property, enter the URL for your HDInsight.</span></span> <span data-ttu-id="ab692-496">Por ejemplo, https://<clustername>.azurehdinsight.net/.</span><span class="sxs-lookup"><span data-stu-id="ab692-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="ab692-497">En la propiedad **UserName** , escriba el nombre del usuario que tiene acceso al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ab692-497">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span></span>
   3. <span data-ttu-id="ab692-498">En la propiedad **Password** , especifique la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="ab692-498">For the **Password** property, enter the password for the user.</span></span>
   4. <span data-ttu-id="ab692-499">En la propiedad **LinkedServiceName**, escriba **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ab692-499">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="ab692-500">Haga clic en **Implementar** en la barra de comandos para implementar el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="ab692-500">Click **Deploy** on the command bar to deploy the linked service.</span></span>

<span data-ttu-id="ab692-501">Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="ab692-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="ab692-502">En el **JSON de la canalización**, utilice el servicio vinculado de HDInsight (a petición o el suyo propio):</span><span class="sxs-lookup"><span data-stu-id="ab692-502">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="ab692-503">Creación de una actividad personalizada mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="ab692-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="ab692-504">En el tutorial de este artículo, se crea una factoría de datos con una canalización que usa la actividad personalizada mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ab692-504">In the walkthrough in this article, you create a data factory with a pipeline that uses the custom activity by using the Azure portal.</span></span> <span data-ttu-id="ab692-505">El código siguiente muestra cómo crear la factoría de datos con el SDK de .NET en su lugar.</span><span class="sxs-lookup"><span data-stu-id="ab692-505">The following code shows you how to create the data factory by using .NET SDK instead.</span></span> <span data-ttu-id="ab692-506">Puede encontrar más detalles sobre cómo usar el SDK para crear mediante programación las canalizaciones en el artículo [crear una canalización con la actividad de copia mediante la API de NET](data-factory-copy-activity-tutorial-using-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="ab692-506">You can find more details about using SDK to programmatically create pipelines in the [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with the name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need to set slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed to acquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="ab692-507">Depurar una actividad personalizada en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ab692-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="ab692-508">El ejemplo de [Azure Data Factory: entorno local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) en GitHub incluye una herramienta que permite depurar actividades personalizadas de .NET en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab692-508">The [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you to debug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="ab692-509">Actividades personalizadas de ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="ab692-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="ab692-510">Muestra</span><span class="sxs-lookup"><span data-stu-id="ab692-510">Sample</span></span> | <span data-ttu-id="ab692-511">Qué hace la actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="ab692-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="ab692-512">[Descargador de datos HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="ab692-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="ab692-513">Descarga datos de un punto de conexión HTTP a Almacenamiento de blobs de Azure a través de una actividad personalizada de C# en Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab692-513">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="ab692-514">Ejemplo de Análisis de opiniones de Twitter.</span><span class="sxs-lookup"><span data-stu-id="ab692-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="ab692-515">Invoca un modelo de aprendizaje automático de Azure y realiza un análisis de opiniones, puntuación, predicción, etc.</span><span class="sxs-lookup"><span data-stu-id="ab692-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="ab692-516">[Ejecutar script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="ab692-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="ab692-517">Invoca el script de R; para ello, ejecuta RScript.exe en el clúster de HDInsight que ya tiene instalado R.</span><span class="sxs-lookup"><span data-stu-id="ab692-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="ab692-518">Actividad .NET entre AppDomain</span><span class="sxs-lookup"><span data-stu-id="ab692-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="ab692-519">Utiliza otras versiones de ensamblado que las utilizadas por el iniciador de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ab692-519">Uses different assembly versions from ones used by the Data Factory launcher</span></span> |
| [<span data-ttu-id="ab692-520">Reproceso de un modelo en Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ab692-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="ab692-521">Reprocesa un modelo en Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="ab692-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
