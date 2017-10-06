---
title: "aaaManage análisis de Data Lake de Azure mediante la interfaz de línea de comandos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo trabajos de cuentas de análisis de Data Lake toomanage, orígenes de datos y los usuarios mediante la CLI de Azure"
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
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="90199-103">Administración del Análisis de Azure Data Lake mediante Interfaz de línea de comandos (CLI) de Azure</span><span class="sxs-lookup"><span data-stu-id="90199-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="90199-104">Obtenga información acerca de cómo las cuentas de análisis de Azure Data Lake toomanage, orígenes de datos, los usuarios y trabajos mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="90199-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="90199-105">temas de administración de toosee con otras herramientas, haga clic en Seleccionar de pestaña de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="90199-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="90199-106">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="90199-106">**Prerequisites**</span></span>

<span data-ttu-id="90199-107">Antes de comenzar este tutorial, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="90199-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="90199-108">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="90199-108">**An Azure subscription**.</span></span> <span data-ttu-id="90199-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90199-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="90199-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="90199-110">**Azure CLI**.</span></span> <span data-ttu-id="90199-111">Consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="90199-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="90199-112">Descargue e instale hello **preliminares** [herramientas de Azure CLI](https://github.com/MicrosoftBigData/AzureDataLake/releases) en orden toocomplete esta demostración.</span><span class="sxs-lookup"><span data-stu-id="90199-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="90199-113">**Autenticación**con Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="90199-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="90199-114">Para obtener más información acerca de cómo autenticar con una cuenta profesional o educativa, consulte [conectarse tooan suscripción de Azure desde hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="90199-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="90199-115">**Modo del conmutador toohello Azure Resource Manager**con Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="90199-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="90199-116">**comandos de almacén de Data Lake y análisis de Data Lake de Hola toolist:**</span><span class="sxs-lookup"><span data-stu-id="90199-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="90199-117">Administrar cuentas</span><span class="sxs-lookup"><span data-stu-id="90199-117">Manage accounts</span></span>
<span data-ttu-id="90199-118">Antes de ejecutar un trabajo de Análisis de Data Lake, debe tener una cuenta de Análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="90199-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="90199-119">A diferencia de HDInsight de Azure, no se paga por una cuenta de Análisis cuando no está ejecutando un trabajo.</span><span class="sxs-lookup"><span data-stu-id="90199-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="90199-120">Solo paga por vez hello cuando se ejecuta un trabajo.</span><span class="sxs-lookup"><span data-stu-id="90199-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="90199-121">Para obtener más información, consulte la página con [información general sobre Análisis con Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90199-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="90199-122">Creación de cuentas</span><span class="sxs-lookup"><span data-stu-id="90199-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="90199-123">Actualización de cuentas</span><span class="sxs-lookup"><span data-stu-id="90199-123">Update accounts</span></span>
<span data-ttu-id="90199-124">Hello comando siguiente actualiza las propiedades de Hola de una cuenta de análisis de Data Lake existente</span><span class="sxs-lookup"><span data-stu-id="90199-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="90199-125">Enumeración de cuentas</span><span class="sxs-lookup"><span data-stu-id="90199-125">List accounts</span></span>
<span data-ttu-id="90199-126">Enumeración de cuentas de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="90199-127">Enumerar cuentas de Análisis de Data Lake dentro de un grupo de recursos específico</span><span class="sxs-lookup"><span data-stu-id="90199-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="90199-128">Obtener detalles de una cuenta específica de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="90199-129">Eliminación de cuentas de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="90199-130">Administración de orígenes de datos de cuenta</span><span class="sxs-lookup"><span data-stu-id="90199-130">Manage account data sources</span></span>
<span data-ttu-id="90199-131">Análisis de Data Lake admite actualmente Hola siguientes orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="90199-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="90199-132">Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="90199-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="90199-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="90199-134">Cuando se crea una cuenta de análisis, debe designar una cuenta de almacenamiento predeterminada de almacenamiento de Azure datos Lake cuenta toobe Hola.</span><span class="sxs-lookup"><span data-stu-id="90199-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="90199-135">Hello cuenta de almacenamiento predeterminado ADL se utiliza registros de auditoría de metadatos de trabajo toostore y trabajo.</span><span class="sxs-lookup"><span data-stu-id="90199-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="90199-136">Una vez creada la cuenta de Análisis, puede agregar más cuentas de Almacén de Data Lake y/o cuentas de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="90199-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="90199-137">Busque la cuenta de almacenamiento de hello predeterminado ADL</span><span class="sxs-lookup"><span data-stu-id="90199-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="90199-138">valor de Hello aparece en propiedades: datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="90199-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="90199-139">Adición de más cuentas de almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="90199-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="90199-140">Solo se admiten nombres cortos de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="90199-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="90199-141">No use el FQDN, por ejemplo "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="90199-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="90199-142">Adición de más cuentas de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="90199-143">[-[d] es un modificador opcional tooindicate si Hola Data Lake añadidos es cuenta de Data Lake de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="90199-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="90199-144">Actualizar el origen de datos existente</span><span class="sxs-lookup"><span data-stu-id="90199-144">Update existing data source</span></span>
<span data-ttu-id="90199-145">tooset una existente almacén de Data Lake cuenta toobe Hola de forma predeterminada:</span><span class="sxs-lookup"><span data-stu-id="90199-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="90199-146">tooupdate una clave de cuenta de almacenamiento de blobs existente:</span><span class="sxs-lookup"><span data-stu-id="90199-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="90199-147">Enumeración de orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="90199-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Origen de datos de lista de Análisis de Data Lake](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="90199-149">Eliminar orígenes de datos:</span><span class="sxs-lookup"><span data-stu-id="90199-149">Delete data sources:</span></span>
<span data-ttu-id="90199-150">toodelete una cuenta de almacén de Data Lake:</span><span class="sxs-lookup"><span data-stu-id="90199-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="90199-151">toodelete una cuenta de almacenamiento de blobs:</span><span class="sxs-lookup"><span data-stu-id="90199-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="90199-152">Trabajos de administración</span><span class="sxs-lookup"><span data-stu-id="90199-152">Manage jobs</span></span>
<span data-ttu-id="90199-153">Debe tener una cuenta de Análisis de Data Lake para poder crear un trabajo.</span><span class="sxs-lookup"><span data-stu-id="90199-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="90199-154">Para obtener más información, consulte [Administración de cuentas de Análisis de Data Lake](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="90199-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="90199-155">Enumeración de trabajos</span><span class="sxs-lookup"><span data-stu-id="90199-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Origen de datos de lista de Análisis de Data Lake](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="90199-157">Obtención de detalles del trabajo</span><span class="sxs-lookup"><span data-stu-id="90199-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="90199-158">Envío de trabajos</span><span class="sxs-lookup"><span data-stu-id="90199-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="90199-159">prioridad de Hello predeterminada de un trabajo es 1000 y grado de hello predeterminado de paralelismo para un trabajo es 1.</span><span class="sxs-lookup"><span data-stu-id="90199-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="90199-160">Cancelación de trabajos</span><span class="sxs-lookup"><span data-stu-id="90199-160">Cancel jobs</span></span>
<span data-ttu-id="90199-161">Usar identificador de trabajo de hello toofind del comando de la lista hello y, a continuación, usar Cancelar toocancel Hola trabajo.</span><span class="sxs-lookup"><span data-stu-id="90199-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="90199-162">Administrar catálogo</span><span class="sxs-lookup"><span data-stu-id="90199-162">Manage catalog</span></span>
<span data-ttu-id="90199-163">catálogo de Hello U-SQL es toostructure usa datos y el código para que pueda compartir por secuencias de comandos SQL U.</span><span class="sxs-lookup"><span data-stu-id="90199-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="90199-164">catálogo de Hello permite Hola mayor rendimiento posible con los datos de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="90199-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="90199-165">Para obtener más información, consulte [Uso del catálogo de U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="90199-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="90199-166">Enumeración de elementos del catálogo</span><span class="sxs-lookup"><span data-stu-id="90199-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="90199-167">los tipos de Hello incluyen la base de datos, esquema, ensamblado, origen de datos externo, tabla, función con valores de tabla o las estadísticas de tabla.</span><span class="sxs-lookup"><span data-stu-id="90199-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="90199-168">Usar grupos ARM</span><span class="sxs-lookup"><span data-stu-id="90199-168">Use ARM groups</span></span>
<span data-ttu-id="90199-169">Las aplicaciones normalmente se componen de muchos componentes,por ejemplo una aplicación web, base de datos, servidor de base de datos, almacenamiento y servicios de terceros.</span><span class="sxs-lookup"><span data-stu-id="90199-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="90199-170">Azure Resource Manager (ARM) permite toowork con recursos de hello en la aplicación como un grupo, denominado tooas un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="90199-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="90199-171">Puede implementar, actualizar, supervisar o eliminar todos los recursos de Hola para su aplicación en una única operación coordinada.</span><span class="sxs-lookup"><span data-stu-id="90199-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="90199-172">Para la implementación se utiliza una plantilla, y esta plantilla puede trabajar en diferentes entornos, como pruebas, ensayo y producción.</span><span class="sxs-lookup"><span data-stu-id="90199-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="90199-173">Para aclarar la facturación para su organización mediante la visualización de los costos de consolidada de hello para el grupo completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="90199-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="90199-174">Para obtener más información, consulte [Información general del Administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90199-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="90199-175">Un servicio de análisis de Data Lake puede incluir Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="90199-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="90199-176">Cuenta de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="90199-177">Cuenta predeterminada y necesaria de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="90199-178">Cuentas adicionales de Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="90199-179">Cuentas adicionales de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="90199-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="90199-180">Puede crear todos estos componentes en un BRAZO grupo toomake les toomanage más fácil.</span><span class="sxs-lookup"><span data-stu-id="90199-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Cuenta y almacenamiento de Análisis de Azure Data Lake](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="90199-182">Una cuenta de análisis de Data Lake y cuentas de almacenamiento dependientes de hello deben colocarse en hello mismo centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="90199-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="90199-183">grupo de Hello ARM no obstante puede encontrarse en otro centro de datos.</span><span class="sxs-lookup"><span data-stu-id="90199-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="90199-184">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="90199-184">See also</span></span>
* [<span data-ttu-id="90199-185">Información general de Análisis de Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="90199-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="90199-186">Introducción a Análisis de Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="90199-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="90199-187">Administración de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="90199-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="90199-188">Supervisión y solución de problemas de trabajos de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="90199-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

