---
title: "aaaUse actividades personalizadas en una canalización de factoría de datos de Azure"
description: "Obtenga información acerca de cómo las actividades personalizadas de toocreate y usarlos en una canalización del generador de datos de Azure."
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
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="11228-103">Uso de actividades personalizadas en una canalización de Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="11228-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="11228-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="11228-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="11228-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="11228-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="11228-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="11228-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="11228-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="11228-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="11228-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="11228-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="11228-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="11228-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="11228-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="11228-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="11228-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="11228-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="11228-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="11228-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="11228-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="11228-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="11228-114">Hay dos tipos de actividades que puede usar en una canalización de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="11228-115">[Las actividades de movimiento de datos](data-factory-data-movement-activities.md) toomove datos entre [admite almacenes de datos de origen y el receptor](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="11228-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="11228-116">[Las actividades de transformación de datos](data-factory-data-transformation-activities.md) datos tootransform mediante servicios como HDInsight de Azure y Azure Batch, aprendizaje automático de Azure de proceso.</span><span class="sxs-lookup"><span data-stu-id="11228-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="11228-117">datos de toomove hacia/desde un almacén de datos que no es compatible con la factoría de datos, crear un **actividad personalizada** con su propios datos movimiento lógica y uso actividad hello en una canalización.</span><span class="sxs-lookup"><span data-stu-id="11228-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="11228-118">Del mismo modo, tootransform/procesar los datos de forma que no es compatible con la factoría de datos, crear una actividad personalizada con su propia lógica de transformación de datos y utilizar la actividad hello en una canalización.</span><span class="sxs-lookup"><span data-stu-id="11228-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="11228-119">Puede configurar una actividad personalizada toorun en un **Azure Batch** grupo de máquinas virtuales o basados en Windows **HDInsight de Azure** clúster.</span><span class="sxs-lookup"><span data-stu-id="11228-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="11228-120">Si usa Azure Batch, solo puede utilizar un grupo de Azure Batch existente.</span><span class="sxs-lookup"><span data-stu-id="11228-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="11228-121">Sin embargo, al utilizar HDInsight, puede utilizar un clúster de HDInsight existente o un clúster creado automáticamente cuando se solicita en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="11228-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="11228-122">Hello en el tutorial siguiente proporciona instrucciones paso a paso para crear una actividad personalizada de .NET y usar la actividad personalizada hello en una canalización.</span><span class="sxs-lookup"><span data-stu-id="11228-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="11228-123">Tutorial de Hello usa un **Azure Batch** servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="11228-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="11228-124">servicio vinculado de toouse un HDInsight de Azure en su lugar, cree un servicio vinculado de tipo **HDInsight** (su propio clúster de HDInsight) o **HDInsightOnDemand** (factoría de datos crea un clúster de HDInsight a petición).</span><span class="sxs-lookup"><span data-stu-id="11228-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="11228-125">A continuación, configure hello de la actividad personalizada toouse servicio vinculado de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="11228-126">Vea [servicios vinculados de HDInsight de Azure de uso](#use-hdinsight-compute-service) sección para obtener más información sobre el uso de la actividad personalizada hello toorun de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="11228-127">las actividades de .NET personalizadas Hola ejecutarán solo en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="11228-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="11228-128">Una solución alternativa para esta limitación es toouse Hola mapa reducir actividad toorun Java código personalizado en un clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="11228-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="11228-129">Otra opción es toouse un grupo de lote de Azure de las máquinas virtuales toorun actividades personalizadas en lugar de utilizar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="11228-130">No es posible toouse una puerta de enlace de administración de datos de orígenes de datos de actividad personalizada tooaccess local.</span><span class="sxs-lookup"><span data-stu-id="11228-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="11228-131">Actualmente, [Data Management Gateway](data-factory-data-management-gateway.md) solo admite la actividad de copia de hello y actividad de procedimiento almacenado de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="11228-132">Tutorial: creación de una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="11228-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="11228-133">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="11228-133">Prerequisites</span></span>
* <span data-ttu-id="11228-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="11228-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="11228-135">Descargue e instale el [SDK de .NET de Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="11228-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="11228-136">Requisitos previos de Lote de Azure</span><span class="sxs-lookup"><span data-stu-id="11228-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="11228-137">En el tutorial de hello, ejecute sus actividades personalizadas de .NET con Azure Batch como un recurso de proceso.</span><span class="sxs-lookup"><span data-stu-id="11228-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="11228-138">**Lote de Azure** es una plataforma de alto rendimiento (HPC) informática eficacia en la nube de Hola y del servicio para ejecutar paralelas a gran escala.</span><span class="sxs-lookup"><span data-stu-id="11228-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="11228-139">Lote de Azure programa toorun de trabajo de proceso intensivo en administrada **colección de máquinas virtuales**, y puede automáticamente escala calcular necesidades de hello toomeet de recursos de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="11228-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="11228-140">Vea [conceptos básicos de Azure Batch] [ batch-technical-overview] artículo para obtener una descripción detallada de hello servicio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="11228-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="11228-141">Para ver tutorial Hola, cree una cuenta de lote de Azure con un grupo de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="11228-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="11228-142">Estos son los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="11228-142">Here are hello steps:</span></span>

1. <span data-ttu-id="11228-143">Crear un **cuenta de Azure Batch** con hello [portal de Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11228-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="11228-144">Para obtener instrucciones, consulte el artículo [Creación y administración de una cuenta de Azure Batch][batch-create-account].</span><span class="sxs-lookup"><span data-stu-id="11228-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="11228-145">Anote el nombre de la cuenta de hello Azure Batch, clave de cuenta, URI y nombre del grupo.</span><span class="sxs-lookup"><span data-stu-id="11228-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="11228-146">Vaya necesitando toocreate un servicio vinculado Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="11228-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="11228-147">En página de inicio de hello para la cuenta de lote de Azure, verá un **URL** Hola siguiendo el formato: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="11228-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="11228-148">En este ejemplo, **myaccount** es nombre Hola de hello cuenta de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="11228-149">URI que se use en definición de servicio vinculado de hello es dirección URL de hello sin nombre Hola de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="11228-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="11228-150">Por ejemplo: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="11228-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="11228-151">Haga clic en **claves** en el menú izquierdo de Hola y Hola copia **clave de acceso principal**.</span><span class="sxs-lookup"><span data-stu-id="11228-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="11228-152">toouse un grupo existente, haga clic en **grupos** en el menú de Hola y tome nota de hello **identificador** del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="11228-153">Si no tienes un grupo existente, mueva toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="11228-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="11228-154">Cree un **grupo de Lote de Azure**.</span><span class="sxs-lookup"><span data-stu-id="11228-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="11228-155">Hola [portal de Azure](https://portal.azure.com), haga clic en **examinar** en Hola menú izquierdo y haga clic en **las cuentas por lotes**.</span><span class="sxs-lookup"><span data-stu-id="11228-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="11228-156">Seleccione su hello tooopen de cuenta de Azure Batch **cuenta de lote** hoja.</span><span class="sxs-lookup"><span data-stu-id="11228-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="11228-157">Haga clic en el icono **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="11228-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="11228-158">Hola **grupos** hoja, haga clic en el botón Agregar en la barra de herramientas de hello tooadd un grupo.</span><span class="sxs-lookup"><span data-stu-id="11228-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="11228-159">Escriba un Id. de grupo de hello (Id. de grupo).</span><span class="sxs-lookup"><span data-stu-id="11228-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="11228-160">Hola Nota **Id. de grupo de hello**; necesita al crear soluciones de hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="11228-161">Especifique **Windows Server 2012 R2** para configuración de la familia de sistemas operativos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="11228-162">Seleccione un **plan de tarifa de nodos**.</span><span class="sxs-lookup"><span data-stu-id="11228-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="11228-163">Escriba **2** como valor de hello **destino dedicado** configuración.</span><span class="sxs-lookup"><span data-stu-id="11228-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="11228-164">Escriba **2** como valor de hello **Max tareas por nodo** configuración.</span><span class="sxs-lookup"><span data-stu-id="11228-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="11228-165">Haga clic en **Aceptar** grupo de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="11228-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="11228-166">Tome nota de hello **identificador** del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="11228-167">Pasos de alto nivel</span><span class="sxs-lookup"><span data-stu-id="11228-167">High-level steps</span></span>
<span data-ttu-id="11228-168">Estos son los pasos de alto nivel dos Hola que realizar como parte de este tutorial:</span><span class="sxs-lookup"><span data-stu-id="11228-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="11228-169">Cree una actividad personalizada que contenga una lógica de procesamiento o transformación de datos simple.</span><span class="sxs-lookup"><span data-stu-id="11228-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="11228-170">Cree un generador de datos de Azure con una canalización que usa la actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="11228-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="11228-171">creación de una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="11228-171">Create a custom activity</span></span>
<span data-ttu-id="11228-172">crear una actividad personalizada. NET, toocreate una **biblioteca de clases .NET** proyecto con una clase que implementa que **IDotNetActivity** interfaz.</span><span class="sxs-lookup"><span data-stu-id="11228-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="11228-173">Esta interfaz solo tiene un método, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , y su firma es:</span><span class="sxs-lookup"><span data-stu-id="11228-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="11228-174">método Hello toma cuatro parámetros:</span><span class="sxs-lookup"><span data-stu-id="11228-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="11228-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="11228-175">**linkedServices**.</span></span> <span data-ttu-id="11228-176">Esta propiedad es una lista enumerable de servicios de almacenamiento de datos vinculado hace referencia a los conjuntos de datos de entrada y salida de actividad hello.</span><span class="sxs-lookup"><span data-stu-id="11228-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="11228-177">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="11228-177">**datasets**.</span></span> <span data-ttu-id="11228-178">Esta propiedad es una lista enumerable de conjuntos de datos de entrada y salida de actividad hello.</span><span class="sxs-lookup"><span data-stu-id="11228-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="11228-179">Puede usar este ubicaciones de parámetro tooget hello y esquemas definidos por los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="11228-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="11228-180">**activity**.</span><span class="sxs-lookup"><span data-stu-id="11228-180">**activity**.</span></span> <span data-ttu-id="11228-181">Esta propiedad representa la actividad actual de hello.</span><span class="sxs-lookup"><span data-stu-id="11228-181">This property represents hello current activity.</span></span> <span data-ttu-id="11228-182">Puede ser usado tooaccess propiedades extendidas asociadas con la actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="11228-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="11228-183">Consulte [Acceso a las propiedades extendidas](#access-extended-properties) para más información.</span><span class="sxs-lookup"><span data-stu-id="11228-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="11228-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="11228-184">**logger**.</span></span> <span data-ttu-id="11228-185">Este objeto le permite escribir comentarios de depuración que superficie en Inicio de sesión de usuario de hello para la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="11228-186">método Hello devuelve un diccionario que puede ser actividades personalizadas utilizadas toochain juntos en un futuro Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="11228-187">Esta característica todavía no está implementada, por lo que devuelve un diccionario vacío de método hello.</span><span class="sxs-lookup"><span data-stu-id="11228-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="11228-188">Procedimiento</span><span class="sxs-lookup"><span data-stu-id="11228-188">Procedure</span></span>
1. <span data-ttu-id="11228-189">Cree un proyecto de **biblioteca de clases .NET** .</span><span class="sxs-lookup"><span data-stu-id="11228-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="11228-190">Inicie <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> o <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="11228-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="11228-191">Haga clic en <b>archivo</b>, seleccione demasiado<b>New</b>y haga clic en <b>proyecto</b>.</span><span class="sxs-lookup"><span data-stu-id="11228-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="11228-192">Expanda <b>Plantillas</b> y seleccione <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="11228-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="11228-193">En este tutorial, use C#, pero puede usar cualquier actividad personalizada .NET language toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="11228-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="11228-194">Seleccione <b>biblioteca de clases</b> de lista de Hola de tipos de proyecto en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="11228-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="11228-195">En VS 2017, elija <b>Biblioteca de clases (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="11228-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="11228-196">Escriba <b>MyDotNetActivity</b> para hello <b>nombre</b>.</span><span class="sxs-lookup"><span data-stu-id="11228-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="11228-197">Seleccione <b>C:\ADFGetStarted</b> para hello <b>ubicación</b>.</span><span class="sxs-lookup"><span data-stu-id="11228-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="11228-198">Haga clic en <b>Aceptar</b> proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="11228-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="11228-199">
2.Haga clic en **herramientas**, seleccione demasiado**Administrador de paquetes de NuGet**y haga clic en **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="11228-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="11228-200">3.</span><span class="sxs-lookup"><span data-stu-id="11228-200">3.</span></span> <span data-ttu-id="11228-201">Hola consola de administrador de paquetes, ejecutar Hola después comando tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="11228-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="11228-202">Hola de importación **el almacenamiento de Azure** paquetes de NuGet en los proyectos de toohello.</span><span class="sxs-lookup"><span data-stu-id="11228-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="11228-203">Selector de servicio de factoría de datos requiere la versión de Hola 4.3 de WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="11228-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="11228-204">Si agrega una referencia tooa una versión posterior del ensamblado de almacenamiento de Azure en el proyecto de actividad personalizada, verá un error cuando se ejecuta la actividad hello.</span><span class="sxs-lookup"><span data-stu-id="11228-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="11228-205">error de hello tooresolve, consulte [Appdomain aislamiento](#appdomain-isolation) sección.</span><span class="sxs-lookup"><span data-stu-id="11228-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="11228-206">Agregue los siguiente hello **mediante** archivo de código fuente de toohello las instrucciones en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-206">Add hello following **using** statements toohello source file in hello project.</span></span>

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
6. <span data-ttu-id="11228-207">Cambiar el nombre del programa Hola Hola **espacio de nombres** demasiado**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="11228-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="11228-208">Cambiar nombre de Hola de clase hello demasiado**MyDotNetActivity** y derivan de hello **IDotNetActivity** interfaz tal y como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="11228-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="11228-209">Hola implemente (Agregar) **Execute** método de hello **IDotNetActivity** interfaz toohello **MyDotNetActivity** Hola de clase y copia siguiendo el método de toohello de código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="11228-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="11228-210">Hello en el ejemplo siguiente cuenta Hola número de repeticiones del término de búsqueda de hello ("Microsoft") en cada blob asociado a un segmento de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
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

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
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
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
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
9. <span data-ttu-id="11228-211">Agregue Hola siguiendo métodos auxiliares:</span><span class="sxs-lookup"><span data-stu-id="11228-211">Add hello following helper methods:</span></span> 

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

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
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
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
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

    <span data-ttu-id="11228-212">Hola GetFolderPath método devuelve Hola ruta de acceso toohello que Hola conjunto de datos que señala la carpeta tooand Hola GetFileName devuelve Hola nombre de método hello/archivo de blob que Hola conjunto de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="11228-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="11228-213">Si havefolderPath se define usando variables como {Year}, {Month} devuelve {Day} etc., método hello Hola cadena tal cual sin sustituirlos con valores de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="11228-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="11228-214">Consulte la sección [Acceso a las propiedades extendidas](#access-extended-properties) para más información sobre cómo acceder a SliceStart, SliceEnd, etc.</span><span class="sxs-lookup"><span data-stu-id="11228-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="11228-215">Hola método Calculate calcula número Hola de instancias de la palabra clave de Microsoft en archivos de entrada de hello (BLOB en la carpeta de hello).</span><span class="sxs-lookup"><span data-stu-id="11228-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="11228-216">término de búsqueda de Hello ("Microsoft") está codificado de forma rígida en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="11228-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="11228-217">Compile el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-217">Compile hello project.</span></span> <span data-ttu-id="11228-218">Haga clic en **generar** desde el menú de Hola y haga clic en **generar solución**.</span><span class="sxs-lookup"><span data-stu-id="11228-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="11228-219">Versión del conjunto 4.5.2 de .NET Framework, como .NET framework de destino de hello para el proyecto: haga clic en proyecto de Hola y haga clic en **propiedades** tooset de .NET framework de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="11228-220">Data Factory no admite actividades personalizadas que se compilaron con versiones de .NET Framework posteriores a la 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="11228-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="11228-221">Iniciar **el Explorador de Windows**, del sistema y desplácese demasiado**bin\debug** o **bin\release** carpeta según el tipo de saludo de compilación.</span><span class="sxs-lookup"><span data-stu-id="11228-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="11228-222">Crear un archivo zip **MyDotNetActivity.zip** que contiene todos los archivos binarios de Hola Hola <project folder>carpeta \bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="11228-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="11228-223">Incluir hello **MyDotNetActivity.pdb** de archivos para que obtengan detalles adicionales, como el número de línea de código fuente de Hola que causó el problema de hello si hubo un error.</span><span class="sxs-lookup"><span data-stu-id="11228-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="11228-224">Todos los Hola archivos en el archivo zip de hello para la actividad personalizada hello debe estar en hello **nivel superior** con ningún subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="11228-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![Archivos de salida binarios](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="11228-226">Cree el contenedor de blobs **customactivitycontainer**, si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="11228-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="11228-227">Cargar MyDotNetActivity.zip como un customactivitycontainer de toohello de blob en un **general** almacenamiento de blobs de Azure (almacenamiento de blobs activos/frío) que se hace referencia mediante AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="11228-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="11228-228">Si agrega esta solución de tooa del proyecto de actividad de .NET en Visual Studio que contiene un proyecto de la factoría de datos y agregar un proyecto de actividad de too.NET de referencia de proyecto de aplicación de hello factoría de datos, no es necesario dos últimos pasos de la creación manual de Hola de tooperform archivo zip de Hola y cargarlo toohello almacenamiento de blobs de Azure de uso general.</span><span class="sxs-lookup"><span data-stu-id="11228-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="11228-229">Cuando publique las entidades de la factoría de datos con Visual Studio, estos pasos se realizan automáticamente por el proceso de publicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="11228-230">Para obtener más información, consulte la sección [Proyecto de Data Factory en Visual Studio](#data-factory-project-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="11228-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="11228-231">Crear una canalización con una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="11228-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="11228-232">Se ha creado una actividad personalizada y cargado el archivo zip de hello con el contenedor de blobs de tooa de los archivos binarios en una **general** cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="11228-233">En esta sección, se crea un generador de datos de Azure con una canalización que usa la actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="11228-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="11228-234">conjunto de datos de entrada de Hello para la actividad personalizada hello representa blobs (archivos) en carpeta de hello customactivityinput adftutorial del contenedor de en el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="11228-235">conjunto de datos de salida de Hello para la actividad de hello representa blobs de salida en la carpeta de hello customactivityoutput adftutorial del contenedor de en el almacenamiento de blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="11228-236">Crear **file.txt** archivo con hello siguiente contenido y cargarlo demasiado**customactivityinput** carpeta de hello **adftutorial** contenedor.</span><span class="sxs-lookup"><span data-stu-id="11228-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="11228-237">Crear contenedor de hello adftutorial si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="11228-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="11228-238">carpeta de entrada de Hello corresponde tooa segmento de factoría de datos de Azure incluso si la carpeta de hello tiene dos o más archivos.</span><span class="sxs-lookup"><span data-stu-id="11228-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="11228-239">Cuando se procesa cada segmento de canalización de hello, la actividad personalizada hello recorre en iteración todos los blobs de hello en la carpeta de entrada de Hola para dicho sector.</span><span class="sxs-lookup"><span data-stu-id="11228-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="11228-240">Verá un archivo con en la carpeta de hello adftutorial\customactivityoutput de salida con una o varias líneas (igual que el número de blobs en la carpeta de entrada de hello):</span><span class="sxs-lookup"><span data-stu-id="11228-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="11228-241">Estos son los pasos de hello que lleva a cabo en esta sección:</span><span class="sxs-lookup"><span data-stu-id="11228-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="11228-242">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="11228-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="11228-243">Crear **servicios vinculados** para grupo de Azure Batch Hola de máquinas virtuales en qué Hola actividad personalizada se ejecuta y Hola almacenamiento de Azure que contiene Hola blobs de entrada/salida.</span><span class="sxs-lookup"><span data-stu-id="11228-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="11228-244">Crear la entrada y salida **conjuntos de datos** que representan la entrada y salida de actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="11228-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="11228-245">Crear un **canalización** que usa la actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="11228-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="11228-246">Crear hello **file.txt** y cargarlo contenedor de blobs de tooa si aún no lo ha hecho.</span><span class="sxs-lookup"><span data-stu-id="11228-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="11228-247">Consulte las instrucciones en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="11228-248">Paso 1: Crear la factoría de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="11228-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="11228-249">Después de iniciar sesión toohello el portal de Azure, Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="11228-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="11228-250">Haga clic en **NEW** en el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="11228-251">Haga clic en **datos + análisis** en hello **New** hoja.</span><span class="sxs-lookup"><span data-stu-id="11228-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="11228-252">Haga clic en **factoría de datos** en hello **análisis de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="11228-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Nuevo menú de Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="11228-254">Hola **factoría de datos** hoja, escriba **CustomActivityFactory** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="11228-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="11228-255">nombre de Hola Hola Azure factoría de datos debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="11228-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="11228-256">Si recibe el error hello: **nombre de generador de datos "CustomActivityFactory" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, **yournameCustomActivityFactory**) y pruebe a crear volver a ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="11228-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Nueva hoja de Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="11228-258">Haga clic en **NOMBRE DEL GRUPO DE RECURSOS**y seleccione un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="11228-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="11228-259">Compruebe que está usando Hola correcto **suscripción** y **región** donde desea Hola datos generador toobe creado.</span><span class="sxs-lookup"><span data-stu-id="11228-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="11228-260">Haga clic en **crear** en hello **factoría de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="11228-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="11228-261">Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="11228-262">Una vez creado correctamente la factoría de datos de hello, consulte hoja de la factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Hoja de la Factoría de datos](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="11228-264">Paso 2: Creación de servicios vinculados</span><span class="sxs-lookup"><span data-stu-id="11228-264">Step 2: Create linked services</span></span>
<span data-ttu-id="11228-265">Servicios vinculados vinculan almacenes de datos o generador de datos de Azure de tooan de servicios de proceso.</span><span class="sxs-lookup"><span data-stu-id="11228-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="11228-266">En este paso, vincular su cuenta de almacenamiento de Azure y la factoría de datos de Azure Batch cuenta tooyour.</span><span class="sxs-lookup"><span data-stu-id="11228-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="11228-267">Creación de un servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="11228-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="11228-268">Haga clic en hello **autor e implementar** icono hello **factoría de datos** hoja para **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="11228-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="11228-269">Vea Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="11228-270">Haga clic en **nuevo almacén de datos** en Hola barra de comandos y elija **almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="11228-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="11228-271">Debería ver Hola script JSON para crear un almacenamiento de Azure vinculada servicio en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![Nuevo almacén de datos: Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="11228-273">Reemplace `<accountname>` con el nombre de la cuenta de almacenamiento de Azure y `<accountkey>` con la clave de acceso del programa Hola a cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="11228-274">toolearn cómo tooget el almacenamiento de tener acceso a clave, consulte [ver, copiar y regenerar almacenamiento de claves de acceso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="11228-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Servicio vinculado de Azure Storage](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="11228-276">Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="11228-277">Creación del servicio vinculado de Lote de Azure</span><span class="sxs-lookup"><span data-stu-id="11228-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="11228-278">Hola Editor de generador de datos, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo proceso**y, a continuación, seleccione **Azure Batch** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![Nuevo proceso: Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="11228-280">Asegúrese de hello siguiente secuencia de comandos de cambios toohello JSON:</span><span class="sxs-lookup"><span data-stu-id="11228-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="11228-281">Especifique el nombre de la cuenta de Azure Batch para hello **accountName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="11228-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="11228-282">Hola **URL** de hello **hoja de la cuenta de Azure Batch** en hello siguiendo el formato: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="11228-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="11228-283">Para hello **batchUri** propiedad Hola JSON, necesita tooremove `accountname.` de dirección URL y el uso de Hola Hola `accountname` para hello `accountName` propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="11228-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="11228-284">Especificar clave de cuenta de lote de Azure de Hola para hello **accessKey** propiedad.</span><span class="sxs-lookup"><span data-stu-id="11228-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="11228-285">Especifique el nombre de hello del grupo de Hola que creó como parte de los requisitos previos para hello **poolName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="11228-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="11228-286">También puede especificar el identificador de hello del grupo de hello en lugar del nombre de Hola de grupo de Hola de.</span><span class="sxs-lookup"><span data-stu-id="11228-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="11228-287">Especifique el URI de lote de Azure para hello **batchUri** propiedad.</span><span class="sxs-lookup"><span data-stu-id="11228-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="11228-288">Ejemplo: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="11228-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="11228-289">Especificar hello **AzureStorageLinkedService** para hello **linkedServiceName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="11228-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

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

       <span data-ttu-id="11228-290">Para hello **poolName** propiedad, también puede especificar el identificador de hello del grupo de hello en lugar del nombre de Hola de grupo de Hola de.</span><span class="sxs-lookup"><span data-stu-id="11228-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="11228-291">Hola servicio factoría de datos no admite una opción de petición para el lote de Azure que lo hace para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="11228-292">Solo puede usar su propio grupo de Lote de Azure en una factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="11228-293">Paso 3: Creación de conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="11228-293">Step 3: Create datasets</span></span>
<span data-ttu-id="11228-294">En este paso, creará entrada toorepresent de conjuntos de datos y los datos de salida.</span><span class="sxs-lookup"><span data-stu-id="11228-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="11228-295">Creación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="11228-295">Create input dataset</span></span>
1. <span data-ttu-id="11228-296">Hola **Editor** para hello factoría de datos, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y, a continuación, seleccione **almacenamiento de blobs de Azure** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="11228-297">Reemplace Hola JSON en el panel derecho de hello con hello siguiente fragmento de JSON:</span><span class="sxs-lookup"><span data-stu-id="11228-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

   <span data-ttu-id="11228-298">Más adelante, en este mismo tutorial, creará una canalización con la hora de inicio 2016-11-16T00:00:00Z y la de finalización 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="11228-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="11228-299">Es tooproduce programada datos cada hora, por lo que hay cinco segmentos de entrada/salida (entre **00**: 00:00 -> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="11228-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="11228-300">Hola **frecuencia** y **intervalo** de conjunto de datos de entrada de Hola se establece demasiado**hora** y **1**, lo que significa que Hola entrada segmento está disponible cada hora.</span><span class="sxs-lookup"><span data-stu-id="11228-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="11228-301">En este ejemplo, es Hola mismo archivo (file.txt) en intputfolder Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="11228-302">Estas son las horas de inicio de Hola para cada segmento, que se representa mediante la variable del sistema SliceStart Hola por encima del fragmento de JSON.</span><span class="sxs-lookup"><span data-stu-id="11228-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="11228-303">Haga clic en **implementar** en Hola toocreate de barra de herramientas e implementar hello **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="11228-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="11228-304">Confirme que aparece hello **tabla creado correctamente** mensaje en la barra de título de Hola de hello Editor.</span><span class="sxs-lookup"><span data-stu-id="11228-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="11228-305">Crear un conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="11228-305">Create an output dataset</span></span>
1. <span data-ttu-id="11228-306">Hola **editor de la factoría de datos**, haga clic en **... Más** en la barra de comandos de hello, haga clic en **nuevo conjunto de datos**y, a continuación, seleccione **almacenamiento de blobs de Azure**.</span><span class="sxs-lookup"><span data-stu-id="11228-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="11228-307">Reemplace el script JSON de hello en el panel derecho de hello con hello siguiente secuencia de comandos JSON:</span><span class="sxs-lookup"><span data-stu-id="11228-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

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

     <span data-ttu-id="11228-308">Ubicación de salida es **adftutorial/customactivityoutput/** y nombre de archivo de salida es aaaa-MM-dd-HH.txt, donde AAAA-MM-dd-HH es Hola año, mes, fecha y hora del segmento de saludo se está generando.</span><span class="sxs-lookup"><span data-stu-id="11228-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="11228-309">Consulte la [Referencia para desarrolladores][adf-developer-reference] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="11228-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="11228-310">Se genera un blob o archivo de salida para cada segmento de entrada.</span><span class="sxs-lookup"><span data-stu-id="11228-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="11228-311">Así es cómo se asigna el nombre al archivo de salida de cada segmento.</span><span class="sxs-lookup"><span data-stu-id="11228-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="11228-312">Todos los archivos de salida de hello se generan en una carpeta de salida: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="11228-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="11228-313">Segmento</span><span class="sxs-lookup"><span data-stu-id="11228-313">Slice</span></span> | <span data-ttu-id="11228-314">Hora de inicio</span><span class="sxs-lookup"><span data-stu-id="11228-314">Start time</span></span> | <span data-ttu-id="11228-315">Archivo de salida</span><span class="sxs-lookup"><span data-stu-id="11228-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="11228-316">1</span><span class="sxs-lookup"><span data-stu-id="11228-316">1</span></span> |<span data-ttu-id="11228-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="11228-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="11228-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="11228-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="11228-319">2</span><span class="sxs-lookup"><span data-stu-id="11228-319">2</span></span> |<span data-ttu-id="11228-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="11228-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="11228-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="11228-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="11228-322">3</span><span class="sxs-lookup"><span data-stu-id="11228-322">3</span></span> |<span data-ttu-id="11228-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="11228-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="11228-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="11228-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="11228-325">4</span><span class="sxs-lookup"><span data-stu-id="11228-325">4</span></span> |<span data-ttu-id="11228-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="11228-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="11228-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="11228-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="11228-328">5</span><span class="sxs-lookup"><span data-stu-id="11228-328">5</span></span> |<span data-ttu-id="11228-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="11228-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="11228-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="11228-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="11228-331">Recuerde que todos los archivos de hello en una carpeta de entrada son parte de un segmento con horas de inicio de hello mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="11228-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="11228-332">Cuando se procesa este segmento, actividad personalizada hello recorre cada archivo y genera una línea en el archivo de salida de hello con número de Hola de repeticiones del término de búsqueda ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="11228-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="11228-333">Si hay tres archivos en hello inputfolder, hay tres líneas en archivo de salida de hello para cada intervalo por hora: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, etcetera.</span><span class="sxs-lookup"><span data-stu-id="11228-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="11228-334">Hola toodeploy **OutputDataset**, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="11228-335">Crear y ejecutar una canalización que usa la actividad personalizada hello</span><span class="sxs-lookup"><span data-stu-id="11228-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="11228-336">Hola Editor de generador de datos, haga clic en **... Más**y, a continuación, seleccione **nueva canalización** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="11228-337">Reemplace Hola JSON en el panel derecho de hello con hello siguiente secuencia de comandos JSON:</span><span class="sxs-lookup"><span data-stu-id="11228-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

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

    <span data-ttu-id="11228-338">Tenga en cuenta Hola siguientes puntos:</span><span class="sxs-lookup"><span data-stu-id="11228-338">Note hello following points:</span></span>

   * <span data-ttu-id="11228-339">**Simultaneidad** se establece demasiado**2** para que dos segmentos se procesan en paralelo con 2 máquinas virtuales en el grupo de lote de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="11228-340">Hay una actividad en la sección de actividades de Hola y es de tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="11228-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="11228-341">**AssemblyName** se establece el nombre toohello de hello DLL: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="11228-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="11228-342">**Punto de entrada** se establece demasiado**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="11228-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="11228-343">**PackageLinkedService** se establece demasiado**AzureStorageLinkedService** que señala el almacenamiento de blobs de toohello que contiene el archivo zip de hello actividad personalizada.</span><span class="sxs-lookup"><span data-stu-id="11228-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="11228-344">Si utiliza varias cuentas de almacenamiento de Azure para archivos de entrada/salida y hello archivo zip de actividad personalizada, crear otro servicio vinculado de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="11228-345">En este artículo se da por supuesto que está usando Hola la misma cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="11228-346">**PackageFile** se establece demasiado**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="11228-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="11228-347">Se encuentra en formato de hello: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="11228-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="11228-348">toma la actividad personalizada Hello **InputDataset** como entrada y **OutputDataset** como salida.</span><span class="sxs-lookup"><span data-stu-id="11228-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="11228-349">propiedad de linkedServiceName Hola de actividad personalizada hello señala toohello **AzureBatchLinkedService**, lo que indica a Data Factory de Azure esa actividad personalizada hello necesita toorun en máquinas virtuales de lote de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="11228-350">**isPaused** propiedad se establece demasiado**false** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="11228-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="11228-351">canalización de Hola se ejecuta inmediatamente en este ejemplo porque se inician los segmentos de Hola Hola anteriores.</span><span class="sxs-lookup"><span data-stu-id="11228-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="11228-352">Puede establecer esta canalización de Hola de propiedad tootrue toopause y establecer toorestart toofalse atrás.</span><span class="sxs-lookup"><span data-stu-id="11228-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="11228-353">Hola **iniciar** tiempo y **final** tiempos son **cinco** horas separadas y segmentos se producen cada hora, por lo que cinco segmentos son generadas por la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="11228-354">canalización de hello toodeploy, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="11228-355">Canalización de Hola de Monitor</span><span class="sxs-lookup"><span data-stu-id="11228-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="11228-356">En la hoja de la factoría de datos de Hola Hola portal de Azure, haga clic en **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="11228-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Icono Diagrama](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="11228-358">Hola vista de diagrama, haga clic en hello OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="11228-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Vista de diagrama](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="11228-360">Debería ver que los sectores de salida cinco Hola están en estado listo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="11228-361">Si no están en estado listo hello, aún no se han producido aún.</span><span class="sxs-lookup"><span data-stu-id="11228-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Segmentos de salida](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="11228-363">Compruebe que se generan archivos de salida de hello en el almacenamiento de blobs de hello en hello **adftutorial** contenedor.</span><span class="sxs-lookup"><span data-stu-id="11228-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![salida de la actividad personalizada][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="11228-365">Si abre el archivo de salida de hello, debería ver Hola salida toohello similar después de salida:</span><span class="sxs-lookup"><span data-stu-id="11228-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="11228-366">Hola de uso [portal de Azure] [ azure-preview-portal] o toomonitor de cmdlets de PowerShell de Azure la factoría de datos, canalizaciones y conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="11228-367">Puede ver mensajes de Hola **ActivityLogger** en el código de hello para la actividad personalizada hello en los registros de hello (específicamente 0.log usuario) que puede descargarse desde el portal de Hola o mediante cmdlets.</span><span class="sxs-lookup"><span data-stu-id="11228-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![registros de descarga de la actividad personalizada][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="11228-369">Consulte [Supervisión y administración de canalizaciones de la Factoría de datos de Azure](data-factory-monitor-manage-pipelines.md) para obtener información detallada sobre los pasos que hay que seguir para supervisar los conjuntos de datos y las canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="11228-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="11228-370">Proyecto de Data Factory en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11228-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="11228-371">Puede crear y publicar entidades de Data Factory usando Visual Studio en lugar de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="11228-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="11228-372">Para obtener información acerca de cómo crear y publicar las entidades de la factoría de datos mediante el uso de Visual Studio, vea [crear su primera canalización mediante Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) y [copiar los datos de Blob de Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="11228-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="11228-373">Hola siguiendo los pasos adicionales si va a crear el proyecto de la factoría de datos en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="11228-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="11228-374">Agregar proyecto toohello solución de Visual Studio que contiene el proyecto de actividad personalizada hello de hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="11228-375">Agregue un proyecto de actividad de .NET de toohello de referencia de proyecto de la factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="11228-376">Haga clic en proyecto de la factoría de datos, seleccione demasiado**agregar**y, a continuación, haga clic en **referencia**.</span><span class="sxs-lookup"><span data-stu-id="11228-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="11228-377">Hola **Agregar referencia** cuadro de diálogo, seleccione hello **MyDotNetActivity** del proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="11228-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="11228-378">Generar y publicar soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="11228-379">Cuando publique las entidades de la factoría de datos, un archivo zip se crea automáticamente y es el contenedor de blob cargado toohello: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="11228-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="11228-380">Si no existe el contenedor de blob de hello, automáticamente se crea demasiado.</span><span class="sxs-lookup"><span data-stu-id="11228-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="11228-381">Integración de Data Factory y Lote</span><span class="sxs-lookup"><span data-stu-id="11228-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="11228-382">Hola servicio factoría de datos crea un trabajo de lote de Azure con el nombre de hello: **adf poolname: trabajo-xxx**.</span><span class="sxs-lookup"><span data-stu-id="11228-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="11228-383">Haga clic en **trabajos** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-383">Click **Jobs** from hello left menu.</span></span> 

![Data Factory de Azure: trabajos por lotes](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="11228-385">Se crea una tarea para cada ejecución de actividad de un segmento.</span><span class="sxs-lookup"><span data-stu-id="11228-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="11228-386">Si hay cinco segmentos de toobe listo procesado, se crean cinco tareas de este trabajo.</span><span class="sxs-lookup"><span data-stu-id="11228-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="11228-387">Si hay varios nodos de ejecución en el grupo de lote de Hola, dos o más segmentos pueden ejecutar en paralelo.</span><span class="sxs-lookup"><span data-stu-id="11228-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="11228-388">Si se establece el nodo de proceso de tareas máximo de Hola por demasiado > 1, también puede tener más de un segmento con hello mismo proceso.</span><span class="sxs-lookup"><span data-stu-id="11228-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Data Factory de Azure: tareas de trabajos por lotes](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="11228-390">Hola siguiente diagrama ilustra la relación de hello entre tareas de Data Factory de Azure y por lotes.</span><span class="sxs-lookup"><span data-stu-id="11228-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Factoría de datos y Lote](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="11228-392">Solución de errores</span><span class="sxs-lookup"><span data-stu-id="11228-392">Troubleshoot failures</span></span>
<span data-ttu-id="11228-393">La solución de problemas se compone de varias técnicas básicas:</span><span class="sxs-lookup"><span data-stu-id="11228-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="11228-394">Si ve Hola tras error, puede que esté usando un almacenamiento de blobs activa/recuperación en lugar de usar un almacenamiento de blobs de Azure de uso general.</span><span class="sxs-lookup"><span data-stu-id="11228-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="11228-395">Cargar Hola zip archivo tooa **cuenta de almacenamiento de Azure para fines generales**.</span><span class="sxs-lookup"><span data-stu-id="11228-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="11228-396">Si ve Hola tras error, confirme ese nombre Hola de clase Hola Hola CS coincidencias hello en nombre de archivo que especificó para hello **EntryPoint** propiedad de canalización de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="11228-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="11228-397">En el tutorial de hello, nombre de clase hello es: MyDotNetActivity y Hola EntryPoint Hola JSON es: MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="11228-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="11228-398">Si coinciden los nombres de hello, confirme que todos los archivos binarios de hello son Hola **carpeta raíz** del archivo zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="11228-399">Es decir, cuando se abre el archivo zip de hello, debería ver todos los archivos de hello en la carpeta raíz de hello, no en todas las subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="11228-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="11228-400">Si no se establece demasiado el segmento de entrada de hello**listo**, confirme que la estructura de carpetas de entrada de hello es correcta y **file.txt** existe en las carpetas de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="11228-401">Hola **Execute** método de la actividad personalizada, utilice hello **IActivityLogger** información sobre los objetos toolog que le ayude a solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="11228-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="11228-402">mensajes de saludo registrado aparecen en archivos de registro de usuario de hello (uno o más archivos con nombre: usuario 0.log, 1.log de usuario, usuario 2.log, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="11228-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="11228-403">Hola **OutputDataset** hoja, haga clic en Hola segmento toosee Hola **el segmento de datos** hoja para dicho sector.</span><span class="sxs-lookup"><span data-stu-id="11228-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="11228-404">Verá **ejecuciones de actividad** para ese segmento.</span><span class="sxs-lookup"><span data-stu-id="11228-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="11228-405">Debería ver una actividad ejecutar para el intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="11228-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="11228-406">Si hace clic en ejecutar en la barra de comandos de hello, puede iniciar otra actividad ejecutar para hello mismo segmento.</span><span class="sxs-lookup"><span data-stu-id="11228-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="11228-407">Al hacer clic en la ejecución de la actividad de hello, vea hello **detalles de ejecución de la actividad** hoja con una lista de archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="11228-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="11228-408">Vea los mensajes registrados en el archivo de hello user_0.log.</span><span class="sxs-lookup"><span data-stu-id="11228-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="11228-409">Cuando se produce un error, verá tres ejecuciones de actividad porque Hola de reintentos se establece too3 en hello canalización/JSON de la actividad.</span><span class="sxs-lookup"><span data-stu-id="11228-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="11228-410">Al hacer clic en la ejecución de la actividad de hello, consulte los archivos de registro de hello que se puede revisar el error de hello tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="11228-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="11228-411">Hola lista de archivos de registro, haga clic en hello **0.log usuario**.</span><span class="sxs-lookup"><span data-stu-id="11228-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="11228-412">En el panel derecho de Hola se muestran resultados de hello del uso de hello **IActivityLogger.Write** método.</span><span class="sxs-lookup"><span data-stu-id="11228-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="11228-413">Si no ve todos los mensajes, compruebe si tiene más archivos de registro llamados user_1.log, user_2.log, etc. En caso contrario, código de hello puede haya fallado después Hola último mensaje registrado.</span><span class="sxs-lookup"><span data-stu-id="11228-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="11228-414">Además, consulte **system-0.log** para ver si hay alguna excepción o mensaje de error del sistema.</span><span class="sxs-lookup"><span data-stu-id="11228-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="11228-415">Incluir hello **PDB** de archivos en el archivo zip de Hola para que los detalles del error Hola tienen información como **pila de llamadas** cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="11228-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="11228-416">Todos los Hola archivos en el archivo zip de hello para la actividad personalizada hello debe estar en hello **nivel superior** con ningún subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="11228-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="11228-417">Asegúrese de que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), y **packageLinkedService** (debe apuntar toohello **general**almacenamiento de blobs de Azure que contiene el archivo zip de Hola) se establecen valores de toocorrect.</span><span class="sxs-lookup"><span data-stu-id="11228-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="11228-418">Si corrige un segmento de hello tooreprocess error y quiere, haga clic en segmento Hola Hola **OutputDataset** hoja y haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="11228-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="11228-419">Si ve Hola tras error, que usa el paquete de almacenamiento de Azure Hola de versión > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="11228-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="11228-420">Selector de servicio de factoría de datos requiere la versión de Hola 4.3 de WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="11228-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="11228-421">Vea [Appdomain aislamiento](#appdomain-isolation) sección para una solución alternativa, si tiene que utilizar Hola una versión posterior del ensamblado del almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="11228-422">Si puede usar la versión de Hola 4.3.0 del paquete de almacenamiento de Azure, quite Hola existente referencia tooAzure paquete almacenamiento de información de versión > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="11228-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="11228-423">A continuación, ejecute el siguiente comando desde la consola de administrador de paquetes de NuGet de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="11228-424">Compile el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-424">Build hello project.</span></span> <span data-ttu-id="11228-425">Eliminar Azure.Storage ensamblado de versión > 4.3.0 desde la carpeta bin\Debug del saludo.</span><span class="sxs-lookup"><span data-stu-id="11228-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="11228-426">Crear un archivo zip con archivos binarios y un archivo PDB de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="11228-427">Reemplazar el archivo zip antiguo de hello por este otro en contenedor de blobs de hello (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="11228-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="11228-428">Hola vuelva a ejecutar intervalos que no se pudo (haga clic en el segmento y haga clic en ejecutar).</span><span class="sxs-lookup"><span data-stu-id="11228-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="11228-429">actividad personalizada Hello no utiliza hello **app.config** archivo desde el paquete.</span><span class="sxs-lookup"><span data-stu-id="11228-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="11228-430">Por lo tanto, si el código lee las cadenas de conexión del archivo de configuración de hello, no funciona en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="11228-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="11228-431">Hola se recomienda una vez con Azure Batch toohold los secretos en un **Azure KeyVault**, usar un hello tooprotect principal de servicio basada en certificados **keyvault**y distribuir el certificado de Hola tooAzure grupo de lote.</span><span class="sxs-lookup"><span data-stu-id="11228-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="11228-432">Hola actividad personalizada. NET, a continuación, puede tener acceso a los secretos de hello KeyVault en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="11228-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="11228-433">Esta solución es una solución genérica y puede escalarse tooany tipo de secreto, no solo la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="11228-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="11228-434">Hay una solución más fácil (pero no es una práctica recomendada): puede crear un **servicio vinculado de SQL Azure** con valores de cadena de conexión, cree un conjunto de datos que usa Hola servicios vinculados y conjunto de datos de cadena Hola como un conjunto de datos de entrada ficticio toohello la actividad personalizada. NET.</span><span class="sxs-lookup"><span data-stu-id="11228-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="11228-435">También puede, a continuación, Hola de acceso había vinculado cadena de conexión del servicio en el código de actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="11228-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="11228-436">Actualización de una actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="11228-436">Update custom activity</span></span>
<span data-ttu-id="11228-437">Si actualiza el código de hello para la actividad personalizada hello, compilación y cargar el archivo zip de Hola que contiene el nuevo almacenamiento de blobs de toohello de los archivos binarios.</span><span class="sxs-lookup"><span data-stu-id="11228-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="11228-438">Aislamiento de AppDomain</span><span class="sxs-lookup"><span data-stu-id="11228-438">Appdomain isolation</span></span>
<span data-ttu-id="11228-439">Vea [Cross AppDomain ejemplo](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) que muestra cómo toocreate una actividad personalizada que no está restringida versiones tooassembly utilizadas por el iniciador de la factoría de datos de hello (ejemplo: WindowsAzure.Storage v4.3.0, v6.0.x Newtonsoft.Json, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="11228-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="11228-440">Acceso a las propiedades extendidas</span><span class="sxs-lookup"><span data-stu-id="11228-440">Access extended properties</span></span>
<span data-ttu-id="11228-441">Puede declarar propiedades extendidas en JSON de la actividad de hello tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="11228-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

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


<span data-ttu-id="11228-442">En el ejemplo de Hola, hay dos propiedades extendidas: **SliceStart** y **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="11228-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="11228-443">valor de Hola para SliceStart se basa en la variable del sistema SliceStart Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="11228-444">Consulte el artículo sobre las [variables del sistema](data-factory-functions-variables.md) para ver una lista de las variables del sistema admitidas.</span><span class="sxs-lookup"><span data-stu-id="11228-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="11228-445">valor de Hola para DataFactoryName es tooCustomActivityFactory codificado de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="11228-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="11228-446">tooaccess estas propiedades extendidas en hello **Execute** método, use código similar toohello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="11228-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="11228-447">Escalado automático de Azure Batch</span><span class="sxs-lookup"><span data-stu-id="11228-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="11228-448">También puede crear un grupo de Lote de Azure con la característica **autoescala** .</span><span class="sxs-lookup"><span data-stu-id="11228-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="11228-449">Por ejemplo, podría crear un grupo de lote de azure con 0 VM dedicadas y una fórmula de Autoescala según el número de Hola de las tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="11228-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="11228-450">fórmula de ejemplo de Hola aquí logra Hola siguiente comportamiento: cuando inicialmente se crea el grupo de hello, empieza por 1 máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="11228-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="11228-451">Métrica de $PendingTasks define el número de Hola de tareas en ejecución + activo (en cola) estado.</span><span class="sxs-lookup"><span data-stu-id="11228-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="11228-452">fórmula de Hello busca Hola promedio de las tareas pendientes de hello últimos 180 segundos y establece el valor de TargetDedicated en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="11228-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="11228-453">Garantiza que TargetDedicated nunca supera las 25 VM.</span><span class="sxs-lookup"><span data-stu-id="11228-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="11228-454">Por lo tanto, tal y como se envían las nuevas tareas, grupo crece automáticamente y como tareas se completan, las máquinas virtuales, se convierten en uno por uno libre y escalado automático de hello disminuye esas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="11228-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="11228-455">startingNumberOfVMs y maxNumberofVMs pueden ser necesidades tooyour ajustada.</span><span class="sxs-lookup"><span data-stu-id="11228-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="11228-456">Fórmula de escalado automático:</span><span class="sxs-lookup"><span data-stu-id="11228-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="11228-457">Para más información, consulte [Escalado automático de los nodos de proceso en un grupo de Lote de Azure](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="11228-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="11228-458">Si grupo hello usa predeterminado hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Hola servicio por lotes puede tardar 15 a 30 minutos tooprepare Hola VM antes de ejecutar la actividad personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="11228-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="11228-459">Si el grupo de hello está usando un autoScaleEvaluationInterval diferente, podría tardar Hola servicio por lotes autoScaleEvaluationInterval + 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="11228-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="11228-460">Uso del servicio de proceso de HDInsight</span><span class="sxs-lookup"><span data-stu-id="11228-460">Use HDInsight compute service</span></span>
<span data-ttu-id="11228-461">En el tutorial de hello, utiliza actividades personalizadas de lote de Azure compute toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="11228-462">También puede utilizar su propio clúster de HDInsight basados en Windows o hacer factoría de datos crea un clúster de HDInsight basados en Windows a petición y tiene actividad personalizada hello ejecutar en el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="11228-463">Estos son los pasos de alto nivel de hello para el uso de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11228-464">las actividades de .NET personalizadas Hola ejecutarán solo en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="11228-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="11228-465">Una solución alternativa para esta limitación es toouse Hola mapa reducir actividad toorun Java código personalizado en un clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="11228-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="11228-466">Otra opción es toouse un grupo de lote de Azure de las máquinas virtuales toorun actividades personalizadas en lugar de utilizar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="11228-467">Cree un servicio vinculado de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="11228-468">Servicio en lugar de vinculado de HDInsight de uso **AzureBatchLinkedService** Hola de canalización JSON.</span><span class="sxs-lookup"><span data-stu-id="11228-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="11228-469">Si desea que tootest con el tutorial de hello, cambio **iniciar** y **final** el tiempo de espera de la canalización de Hola para que pueda probar el escenario de hello con hello servicio HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="11228-470">Creación de un servicio vinculado de HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="11228-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="11228-471">Hola servicio Data Factory de Azure admite la creación de un clúster a petición y usar datos de salida de tooprocess tooproduce de entrada.</span><span class="sxs-lookup"><span data-stu-id="11228-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="11228-472">También puede utilizar su propio clúster tooperform Hola igual.</span><span class="sxs-lookup"><span data-stu-id="11228-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="11228-473">Cuando se utiliza el clúster de HDInsight a petición, se crea un clúster para cada sector.</span><span class="sxs-lookup"><span data-stu-id="11228-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="11228-474">Sin embargo, si usa su propio clúster de HDInsight, clúster de hello es listo tooprocess Hola segmento inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="11228-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="11228-475">Por lo tanto, cuando se usa el clúster a petición, no verá los datos de salida de hello tan pronto como cuando usa su propio clúster.</span><span class="sxs-lookup"><span data-stu-id="11228-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="11228-476">En tiempo de ejecución, una instancia de una actividad de .NET sólo se ejecuta en un nodo de trabajo en clúster de HDInsight de hello; no puede ser toorun escalado en varios nodos.</span><span class="sxs-lookup"><span data-stu-id="11228-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="11228-477">Pueden ejecutar varias instancias de actividad de .NET en paralelo en distintos nodos del clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="11228-478">toouse un clúster de HDInsight a petición</span><span class="sxs-lookup"><span data-stu-id="11228-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="11228-479">Hola **portal de Azure**, haga clic en **autor e implementar** en la página principal de hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="11228-480">Hola Editor de generador de datos, haga clic en **nuevo proceso** de comando de hello barra y seleccione **clúster de HDInsight a petición** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="11228-481">Asegúrese de hello siguiente secuencia de comandos de cambios toohello JSON:</span><span class="sxs-lookup"><span data-stu-id="11228-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="11228-482">Para hello **clusterSize** propiedad, especifique el tamaño Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="11228-483">Para hello **timeToLive** propiedad, especifique cuánto tiempo cliente hello puede estar inactivo antes de eliminarla.</span><span class="sxs-lookup"><span data-stu-id="11228-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="11228-484">Para hello **versión** propiedad, especifique la versión de HDInsight de hello desea toouse.</span><span class="sxs-lookup"><span data-stu-id="11228-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="11228-485">Si excluye esta propiedad, se utiliza la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="11228-486">Para hello **linkedServiceName**, especifique **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="11228-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

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
    > <span data-ttu-id="11228-487">las actividades de .NET personalizadas Hola ejecutarán solo en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="11228-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="11228-488">Una solución alternativa para esta limitación es toouse Hola mapa reducir actividad toorun Java código personalizado en un clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="11228-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="11228-489">Otra opción es toouse un grupo de lote de Azure de las máquinas virtuales toorun actividades personalizadas en lugar de utilizar un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="11228-490">Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="11228-491">toouse su propio clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="11228-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="11228-492">Hola **portal de Azure**, haga clic en **autor e implementar** en la página principal de hello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="11228-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="11228-493">Hola **Editor de generador de datos**, haga clic en **nuevo proceso** de comando de hello barra y seleccione **clúster de HDInsight** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="11228-494">Asegúrese de hello siguiente secuencia de comandos de cambios toohello JSON:</span><span class="sxs-lookup"><span data-stu-id="11228-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="11228-495">Para hello **clusterUri** propiedad, escriba la dirección URL de Hola para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11228-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="11228-496">Por ejemplo, https://<clustername>.azurehdinsight.net/.</span><span class="sxs-lookup"><span data-stu-id="11228-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="11228-497">Para hello **nombre de usuario** propiedad, escriba nombre de usuario de hello con clúster de HDInsight de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="11228-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="11228-498">Para hello **contraseña** propiedad, escriba la contraseña de hello para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="11228-499">Para hello **LinkedServiceName** propiedad, escriba **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="11228-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="11228-500">Haga clic en **implementar** en toodeploy Hola vinculado servicio la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11228-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="11228-501">Consulte [Servicios vinculados de procesos](data-factory-compute-linked-services.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="11228-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="11228-502">Hola **JSON de canalización**, utilice HDInsight (a petición o su propia) servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="11228-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

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

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="11228-503">Creación de una actividad personalizada mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="11228-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="11228-504">En el tutorial de hello en este artículo, se crea una factoría de datos con una canalización que usa la actividad personalizada hello mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="11228-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="11228-505">Hola siguiente código muestra cómo toocreate Hola factoría de datos con el SDK de .NET en su lugar.</span><span class="sxs-lookup"><span data-stu-id="11228-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="11228-506">Puede encontrar más detalles sobre el uso de SDK tooprogrammatically crean canalizaciones en hello [crear una canalización con la actividad de copia mediante el uso de API de .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="11228-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

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

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
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

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="11228-507">Depurar una actividad personalizada en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11228-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="11228-508">Hola [factoría de datos de Azure: entorno local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) ejemplo en GitHub incluye una herramienta que permite toodebug actividades personalizadas de .NET en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11228-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="11228-509">Actividades personalizadas de ejemplo en GitHub</span><span class="sxs-lookup"><span data-stu-id="11228-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="11228-510">Muestra</span><span class="sxs-lookup"><span data-stu-id="11228-510">Sample</span></span> | <span data-ttu-id="11228-511">Qué hace la actividad personalizada</span><span class="sxs-lookup"><span data-stu-id="11228-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="11228-512">[Descargador de datos HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="11228-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="11228-513">Descarga los datos desde un almacenamiento de blobs mediante la actividad personalizada de C# de factoría de datos de tooAzure de extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="11228-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="11228-514">Ejemplo de Análisis de opiniones de Twitter.</span><span class="sxs-lookup"><span data-stu-id="11228-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="11228-515">Invoca un modelo de aprendizaje automático de Azure y realiza un análisis de opiniones, puntuación, predicción, etc.</span><span class="sxs-lookup"><span data-stu-id="11228-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="11228-516">[Ejecutar script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="11228-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="11228-517">Invoca el script de R; para ello, ejecuta RScript.exe en el clúster de HDInsight que ya tiene instalado R.</span><span class="sxs-lookup"><span data-stu-id="11228-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="11228-518">Actividad .NET entre AppDomain</span><span class="sxs-lookup"><span data-stu-id="11228-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="11228-519">Utiliza las versiones de ensamblado diferente de la utilizada por el iniciador de la factoría de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="11228-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="11228-520">Reproceso de un modelo en Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="11228-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="11228-521">Reprocesa un modelo en Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="11228-521">Reprocesses a model in Azure Analysis Services.</span></span> |

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
