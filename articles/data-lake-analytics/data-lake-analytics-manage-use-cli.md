---
title: "Administración de Azure Data Lake Analytics mediante la interfaz de la línea de comandos (CLI) de Azure | Microsoft Docs"
description: "Aprenda a administrar cuentas de Análisis con Data Lake, orígenes de datos, usuarios y trabajos mediante la CLI de Azure"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="02197-103">Administración del Análisis de Azure Data Lake mediante Interfaz de línea de comandos (CLI) de Azure</span><span class="sxs-lookup"><span data-stu-id="02197-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="02197-104">Aprenda a administrar cuentas, orígenes de datos, usuarios y trabajos de Azure Data Lake Analytics con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="02197-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="02197-105">Para ver los temas de administración con otras herramientas, haga clic en el selector de pestañas de arriba.</span><span class="sxs-lookup"><span data-stu-id="02197-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="02197-106">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="02197-106">**Prerequisites**</span></span>

<span data-ttu-id="02197-107">Antes de empezar este tutorial, debe contar con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="02197-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="02197-108">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="02197-108">**An Azure subscription**.</span></span> <span data-ttu-id="02197-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02197-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="02197-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="02197-110">**Azure CLI**.</span></span> <span data-ttu-id="02197-111">Consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="02197-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="02197-112">Descargue e instale la **versión preliminar** [herramientas de la CLI de Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) para completar esta demostración.</span><span class="sxs-lookup"><span data-stu-id="02197-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="02197-113">**Autenticación**, mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="02197-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="02197-114">Para más información acerca de cómo autenticarse con una cuenta profesional o educativa, consulte [Conexión a una suscripción de Azure desde la CLI de Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="02197-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="02197-115">**Cambiar al modo de Administrador de recursos de Azure**con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="02197-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="02197-116">**Para mostrar los comandos de Almacén Data Lake y Análisis de Data Lake:**</span><span class="sxs-lookup"><span data-stu-id="02197-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="02197-117">Administrar cuentas</span><span class="sxs-lookup"><span data-stu-id="02197-117">Manage accounts</span></span>
<span data-ttu-id="02197-118">Antes de ejecutar un trabajo de Análisis de Data Lake, debe tener una cuenta de Análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="02197-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="02197-119">A diferencia de HDInsight de Azure, no se paga por una cuenta de Análisis cuando no está ejecutando un trabajo.</span><span class="sxs-lookup"><span data-stu-id="02197-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="02197-120">Solo se paga por el tiempo en que se ejecuta un trabajo.</span><span class="sxs-lookup"><span data-stu-id="02197-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="02197-121">Para obtener más información, consulte la página con [información general sobre Análisis con Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02197-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="02197-122">Creación de cuentas</span><span class="sxs-lookup"><span data-stu-id="02197-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="02197-123">Actualización de cuentas</span><span class="sxs-lookup"><span data-stu-id="02197-123">Update accounts</span></span>
<span data-ttu-id="02197-124">El siguiente comando actualiza las propiedades de una cuenta existente de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="02197-125">Enumeración de cuentas</span><span class="sxs-lookup"><span data-stu-id="02197-125">List accounts</span></span>
<span data-ttu-id="02197-126">Enumeración de cuentas de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="02197-127">Enumerar cuentas de Análisis de Data Lake dentro de un grupo de recursos específico</span><span class="sxs-lookup"><span data-stu-id="02197-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="02197-128">Obtener detalles de una cuenta específica de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="02197-129">Eliminación de cuentas de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="02197-130">Administración de orígenes de datos de cuenta</span><span class="sxs-lookup"><span data-stu-id="02197-130">Manage account data sources</span></span>
<span data-ttu-id="02197-131">Actualmente, Análisis de Data Lake admite los siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="02197-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="02197-132">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="02197-133">Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="02197-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="02197-134">Cuando crea una cuenta de Análisis, debe designar una cuenta de Almacén de Azure Data Lake para que sea la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="02197-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="02197-135">La cuenta predeterminada de almacenamiento de ADL sirve para almacenar los metadatos de trabajos y los registros de auditoría de trabajos.</span><span class="sxs-lookup"><span data-stu-id="02197-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="02197-136">Una vez creada la cuenta de Análisis, puede agregar más cuentas de Almacén de Data Lake y/o cuentas de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="02197-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="02197-137">Búsqueda de la cuenta de almacenamiento de ADL predeterminada</span><span class="sxs-lookup"><span data-stu-id="02197-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="02197-138">El valor aparece en properties:datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="02197-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="02197-139">Adición de más cuentas de almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="02197-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="02197-140">Solo se admiten nombres cortos de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="02197-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="02197-141">No use el FQDN, por ejemplo "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="02197-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="02197-142">Adición de más cuentas de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="02197-143">[-d] es un modificador opcional para indicar si el Data Lake que se va a agregar es la cuenta de Data Lake predeterminada.</span><span class="sxs-lookup"><span data-stu-id="02197-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="02197-144">Actualizar el origen de datos existente</span><span class="sxs-lookup"><span data-stu-id="02197-144">Update existing data source</span></span>
<span data-ttu-id="02197-145">Para establecer una cuenta de Almacén Data Lake existente como predeterminada:</span><span class="sxs-lookup"><span data-stu-id="02197-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="02197-146">Para actualizar una clave de cuenta de almacenamiento de blobs existente:</span><span class="sxs-lookup"><span data-stu-id="02197-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="02197-147">Enumeración de orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="02197-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Origen de datos de lista de Análisis de Data Lake](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="02197-149">Eliminar orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="02197-149">Delete data sources:</span></span>
<span data-ttu-id="02197-150">Para eliminar una cuenta de Almacén Data Lake:</span><span class="sxs-lookup"><span data-stu-id="02197-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="02197-151">Para eliminar una cuenta de Almacenamiento de blobs:</span><span class="sxs-lookup"><span data-stu-id="02197-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="02197-152">Trabajos de administración</span><span class="sxs-lookup"><span data-stu-id="02197-152">Manage jobs</span></span>
<span data-ttu-id="02197-153">Debe tener una cuenta de Análisis de Data Lake para poder crear un trabajo.</span><span class="sxs-lookup"><span data-stu-id="02197-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="02197-154">Para obtener más información, consulte [Administración de cuentas de Análisis de Data Lake](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="02197-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="02197-155">Enumeración de trabajos</span><span class="sxs-lookup"><span data-stu-id="02197-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Origen de datos de lista de Análisis de Data Lake](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="02197-157">Obtención de detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="02197-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="02197-158">Envío de trabajos</span><span class="sxs-lookup"><span data-stu-id="02197-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="02197-159">La prioridad predeterminada de un trabajo es 1000 y el grado predeterminado de paralelismo para un trabajo es 1.</span><span class="sxs-lookup"><span data-stu-id="02197-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="02197-160">Cancelación de trabajos</span><span class="sxs-lookup"><span data-stu-id="02197-160">Cancel jobs</span></span>
<span data-ttu-id="02197-161">Use el comando de la lista para buscar el identificador del trabajo y, a continuación, use Cancelar para cancelar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="02197-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="02197-162">Administrar catálogo</span><span class="sxs-lookup"><span data-stu-id="02197-162">Manage catalog</span></span>
<span data-ttu-id="02197-163">El catálogo de U-SQL se usa para estructurar datos y código, para que puedan compartirse mediante scripts de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="02197-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="02197-164">El catálogo permite el mayor rendimiento posible con los datos en Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="02197-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="02197-165">Para obtener más información, consulte [Uso del catálogo de U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="02197-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="02197-166">Enumeración de elementos del catálogo</span><span class="sxs-lookup"><span data-stu-id="02197-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="02197-167">Entre los tipos, se incluyen base de datos, esquema, ensamblado, origen de datos externo, tabla, función con valores de tabla o estadísticas de tabla.</span><span class="sxs-lookup"><span data-stu-id="02197-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="02197-168">Usar grupos ARM</span><span class="sxs-lookup"><span data-stu-id="02197-168">Use ARM groups</span></span>
<span data-ttu-id="02197-169">Las aplicaciones normalmente se componen de muchos componentes,por ejemplo una aplicación web, base de datos, servidor de base de datos, almacenamiento y servicios de terceros.</span><span class="sxs-lookup"><span data-stu-id="02197-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="02197-170">El Administrador de recursos de Azure (ARM) permite trabajar con los recursos de la aplicación como un grupo al que se hace referencia como Grupo de recursos de Azures</span><span class="sxs-lookup"><span data-stu-id="02197-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="02197-171">Puede implementar, actualizar, supervisar o eliminar todos los recursos de la aplicación en una operación única y coordinada.</span><span class="sxs-lookup"><span data-stu-id="02197-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="02197-172">Para la implementación se utiliza una plantilla, y esta plantilla puede trabajar en diferentes entornos, como pruebas, ensayo y producción.</span><span class="sxs-lookup"><span data-stu-id="02197-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="02197-173">Puede aclarar la facturación de la organización consultando los costes acumulados de todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="02197-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="02197-174">Para obtener más información, consulte [Información general del Administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02197-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="02197-175">Un servicio Análisis de Data Lake puede incluir los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="02197-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="02197-176">Cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="02197-177">Cuenta predeterminada y necesaria de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="02197-178">Cuentas adicionales de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="02197-179">Cuentas adicionales de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="02197-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="02197-180">Puede crear todos estos componentes en un grupo de ARM para que sean más fáciles de administrar.</span><span class="sxs-lookup"><span data-stu-id="02197-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Cuenta y almacenamiento de Análisis de Azure Data Lake](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="02197-182">La cuenta de Análisis de Data Lake y las cuentas de almacenamiento dependientes deben ubicarse en el mismo centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="02197-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="02197-183">Sin embargo, el grupo de ARM puede encontrarse en otro centro de datos.</span><span class="sxs-lookup"><span data-stu-id="02197-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="02197-184">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="02197-184">See also</span></span>
* [<span data-ttu-id="02197-185">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="02197-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="02197-186">Introducción a Análisis de Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="02197-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="02197-187">Administración de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="02197-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="02197-188">Supervisión y solución de problemas de trabajos de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="02197-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

