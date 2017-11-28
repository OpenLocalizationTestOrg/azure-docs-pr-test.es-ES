---
title: Copia de datos hacia y desde Azure Data Lake Store | Microsoft Docs
description: Aprenda a copiar datos hacia y desde Data Lake Store mediante Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 11629fbc83f0554e2097eb4322701654c0bc2028
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="309d4-103">Copia de datos hacia y desde Data Lake Store mediante Data Factory</span><span class="sxs-lookup"><span data-stu-id="309d4-103">Copy data to and from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="309d4-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos hacia y desde Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-104">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Store.</span></span> <span data-ttu-id="309d4-105">Se basa en el artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md), una introducción al movimiento de datos con la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="309d4-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="309d4-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="309d4-106">Supported scenarios</span></span>
<span data-ttu-id="309d4-107">Puede copiar datos **desde Azure Data Lake Store** hacia los siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="309d4-107">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="309d4-108">Puede copiar datos desde los siguientes almacenes de datos **hacia Azure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="309d4-108">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="309d4-109">Cree una cuenta de Data Lake Store antes de crear una canalización con la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="309d4-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="309d4-110">Para más información, consulte [Introducción a Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="309d4-111">Tipos de autenticación que se admiten</span><span class="sxs-lookup"><span data-stu-id="309d4-111">Supported authentication types</span></span>
<span data-ttu-id="309d4-112">El conector de Data Lake Store admite estos tipos de autenticación:</span><span class="sxs-lookup"><span data-stu-id="309d4-112">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="309d4-113">Autenticación de entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="309d4-113">Service principal authentication</span></span>
* <span data-ttu-id="309d4-114">Autenticación de credenciales de usuario (OAuth)</span><span class="sxs-lookup"><span data-stu-id="309d4-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="309d4-115">Se recomienda que use la autenticación de la entidad de servicio, en especial para una copia de datos programada.</span><span class="sxs-lookup"><span data-stu-id="309d4-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="309d4-116">Con la autenticación se credenciales de usuario puede darse la situación de que expiren los tokens.</span><span class="sxs-lookup"><span data-stu-id="309d4-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="309d4-117">Para información sobre los detalles de configuración, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-117">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="309d4-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="309d4-118">Get started</span></span>
<span data-ttu-id="309d4-119">Puede crear una canalización con actividad de copia que mueva los datos hacia Azure Data Lake Store y desde este servicio mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="309d4-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="309d4-120">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="309d4-120">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="309d4-121">Para ver un tutorial sobre la creación de una canalización mediante el Asistente para copia, consulte [Tutorial: crear una canalización con el Asistente para copia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-121">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="309d4-122">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="309d4-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="309d4-123">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="309d4-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="309d4-124">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="309d4-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="309d4-125">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="309d4-125">Create a **data factory**.</span></span> <span data-ttu-id="309d4-126">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="309d4-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="309d4-127">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="309d4-128">Por ejemplo, si va a copiar datos desde una instancia de Azure Blob Storage hacia una instancia de Azure Data Lake Store, creará dos servicios vinculados para vincular la cuenta de Azure Storage y la instancia de Azure Data Lake Store a su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-128">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="309d4-129">Para información sobre las propiedades de los servicios vinculados que son específicas de Azure Data Lake Store, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-129">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="309d4-130">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="309d4-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="309d4-131">En el ejemplo mencionado en el último paso, se crea un conjunto de datos para especificar el contenedor de blobs y la carpeta que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="309d4-131">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="309d4-132">Además, se crea otro conjunto de datos para especificar la ruta de acceso al archivo y la carpeta en Data Lake Store que contiene los datos copiados de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="309d4-132">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="309d4-133">Para información sobre las propiedades del conjunto de datos que son específicas de Azure Data Lake Store, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-133">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="309d4-134">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="309d4-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="309d4-135">En el ejemplo que se ha mencionado anteriormente, se usa BlobSource como origen y AzureDataLakeStoreSink como receptor para la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="309d4-135">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="309d4-136">De igual forma, si va a copiar desde Azure Data Lake Store hacia Azure Blob Storage, usará AzureDataLakeStoreSource y BlobSink en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="309d4-136">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="309d4-137">Para información sobre las propiedades de la actividad de copia que son específicas de Azure Data Lake Store, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-137">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="309d4-138">Para más información sobre cómo usar un almacén de datos como origen o como receptor, haga clic en el vínculo de la sección anterior para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="309d4-139">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="309d4-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="309d4-140">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="309d4-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="309d4-141">Para obtener ejemplos con definiciones de JSON para entidades de Data Factory que se utilizan para copiar datos a Azure Data Lake Store y desde este servicio, consulte la sección [Ejemplos de JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="309d4-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="309d4-142">En las secciones siguientes se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="309d4-143">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="309d4-143">Linked service properties</span></span>
<span data-ttu-id="309d4-144">Un servicio vinculado vincula un almacén de datos a una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-144">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="309d4-145">Creará un servicio vinculado de tipo **AzureDataLakeStore** para vincular datos de Data Lake Store a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-145">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="309d4-146">En la tabla siguiente se describen los elementos JSON específicos de los servicios vinculados Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-146">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="309d4-147">Puede elegir entre la autenticación de la entidad de servicio y la autenticación de credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="309d4-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="309d4-148">Propiedad</span><span class="sxs-lookup"><span data-stu-id="309d4-148">Property</span></span> | <span data-ttu-id="309d4-149">Descripción</span><span class="sxs-lookup"><span data-stu-id="309d4-149">Description</span></span> | <span data-ttu-id="309d4-150">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="309d4-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="309d4-151">**type**</span><span class="sxs-lookup"><span data-stu-id="309d4-151">**type**</span></span> | <span data-ttu-id="309d4-152">La propiedad type debe establecerse en: **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="309d4-152">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="309d4-153">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-153">Yes</span></span> |
| <span data-ttu-id="309d4-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="309d4-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="309d4-155">Información sobre la cuenta de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-155">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="309d4-156">Esta información adopta uno de los siguientes formatos: `https://[accountname].azuredatalakestore.net/webhdfs/v1` o `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="309d4-156">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="309d4-157">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-157">Yes</span></span> |
| <span data-ttu-id="309d4-158">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="309d4-158">**subscriptionId**</span></span> | <span data-ttu-id="309d4-159">Id. de suscripción de Azure al que pertenece la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-159">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="309d4-160">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="309d4-160">Required for sink</span></span> |
| <span data-ttu-id="309d4-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="309d4-161">**resourceGroupName**</span></span> | <span data-ttu-id="309d4-162">Nombre del grupo de recursos de Azure al que pertenece la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-162">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="309d4-163">Necesario para el receptor</span><span class="sxs-lookup"><span data-stu-id="309d4-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="309d4-164">Autenticación de la entidad de servicio (recomendada)</span><span class="sxs-lookup"><span data-stu-id="309d4-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="309d4-165">Para usar la autenticación de la entidad de servicio, registre una entidad de aplicación en Azure Active Directory (AAD) y concédale acceso a Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-165">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="309d4-166">Consulte [Autenticación entre servicios](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) para ver los pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="309d4-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="309d4-167">Anote los siguientes valores; los usará para definir el servicio vinculado:</span><span class="sxs-lookup"><span data-stu-id="309d4-167">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="309d4-168">Identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="309d4-168">Application ID</span></span>
* <span data-ttu-id="309d4-169">Clave de la aplicación</span><span class="sxs-lookup"><span data-stu-id="309d4-169">Application key</span></span> 
* <span data-ttu-id="309d4-170">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="309d4-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="309d4-171">Si va a usar el Asistente para copia para crear canalizaciones de datos, asegúrese de conceder a la entidad de servicio al menos un rol de **lectura** en el control de acceso (administración de identidades y acceso) para la cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-171">If you are using the Copy Wizard to author data pipelines, make sure that you grant the service principal at least a **Reader** role in access control (identity and access management) for the Data Lake Store account.</span></span> <span data-ttu-id="309d4-172">Además, conceda a la entidad de servicio al menos un permiso de **lectura y ejecución** para la raíz de Data Lake Store ("/") y sus elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="309d4-172">Also, grant the service principal at least **Read + Execute** permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="309d4-173">De lo contrario, puede que aparezca el mensaje "Las credenciales proporcionadas no son válidas".</span><span class="sxs-lookup"><span data-stu-id="309d4-173">Otherwise you might see the message "The credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="309d4-174">Después de crear o actualizar una entidad de servicio en AAD, pueden transcurrir unos minutos hasta que se aplican los cambios.</span><span class="sxs-lookup"><span data-stu-id="309d4-174">After you create or update a service principal in Azure AD, it can take a few minutes for the changes to take effect.</span></span> <span data-ttu-id="309d4-175">Compruebe las configuraciones de la entidad de servicio y de la lista de control de acceso (ACL) de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-175">Check the service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="309d4-176">Si el mensaje anteriormente mencionado sigue apareciendo, espere unos instantes e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="309d4-176">If you still see the message "The credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="309d4-177">Para usar la autenticación de la entidad de servicio, especifique las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="309d4-177">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="309d4-178">Propiedad</span><span class="sxs-lookup"><span data-stu-id="309d4-178">Property</span></span> | <span data-ttu-id="309d4-179">Descripción</span><span class="sxs-lookup"><span data-stu-id="309d4-179">Description</span></span> | <span data-ttu-id="309d4-180">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="309d4-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="309d4-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="309d4-181">**servicePrincipalId**</span></span> | <span data-ttu-id="309d4-182">Especifique el id. de cliente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="309d4-182">Specify the application's client ID.</span></span> | <span data-ttu-id="309d4-183">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-183">Yes</span></span> |
| <span data-ttu-id="309d4-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="309d4-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="309d4-185">Especifique la clave de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="309d4-185">Specify the application's key.</span></span> | <span data-ttu-id="309d4-186">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-186">Yes</span></span> |
| <span data-ttu-id="309d4-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="309d4-187">**tenant**</span></span> | <span data-ttu-id="309d4-188">Especifique la información del inquilino (nombre de dominio o identificador de inquilino) en el que reside la aplicación.</span><span class="sxs-lookup"><span data-stu-id="309d4-188">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="309d4-189">Para recuperarlo, mantenga el puntero del mouse en la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="309d4-189">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="309d4-190">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-190">Yes</span></span> |

<span data-ttu-id="309d4-191">**Ejemplo: autenticación de la entidad de servicio**</span><span class="sxs-lookup"><span data-stu-id="309d4-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="309d4-192">Autenticación de credenciales de usuario</span><span class="sxs-lookup"><span data-stu-id="309d4-192">User credential authentication</span></span>
<span data-ttu-id="309d4-193">También puede usar la autenticación de credenciales de usuario para copiar hacia o desde Data Lake Store mediante la especificación de las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="309d4-193">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="309d4-194">Propiedad</span><span class="sxs-lookup"><span data-stu-id="309d4-194">Property</span></span> | <span data-ttu-id="309d4-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="309d4-195">Description</span></span> | <span data-ttu-id="309d4-196">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="309d4-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="309d4-197">**authorization**</span><span class="sxs-lookup"><span data-stu-id="309d4-197">**authorization**</span></span> | <span data-ttu-id="309d4-198">Haga clic en el botón **Autorizar** de Data Factory Editor y escriba sus credenciales, que asignan la dirección URL de autorización generada automáticamente a esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="309d4-198">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="309d4-199">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-199">Yes</span></span> |
| <span data-ttu-id="309d4-200">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="309d4-200">**sessionId**</span></span> | <span data-ttu-id="309d4-201">Id. de sesión de OAuth de la sesión de autorización de OAuth.</span><span class="sxs-lookup"><span data-stu-id="309d4-201">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="309d4-202">Cada id. de sesión es único y solo se puede usar una vez.</span><span class="sxs-lookup"><span data-stu-id="309d4-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="309d4-203">Esta configuración se genera automáticamente al usar Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="309d4-203">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="309d4-204">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-204">Yes</span></span> |

<span data-ttu-id="309d4-205">**Ejemplo: autenticación de credenciales de usuario**</span><span class="sxs-lookup"><span data-stu-id="309d4-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="309d4-206">Expiración del token</span><span class="sxs-lookup"><span data-stu-id="309d4-206">Token expiration</span></span>
<span data-ttu-id="309d4-207">El código de autorización que se genera con el botón **Autorizar** expira transcurrido un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="309d4-207">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="309d4-208">El siguiente mensaje significa que expiró el token de autenticación:</span><span class="sxs-lookup"><span data-stu-id="309d4-208">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="309d4-209">Error de operación de credencial: invalid_grant - AADSTS70002: error al validar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="309d4-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="309d4-210">AADSTS70008: la concesión de acceso proporcionada expiró o se revocó.</span><span class="sxs-lookup"><span data-stu-id="309d4-210">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="309d4-211">Id. de seguimiento: d18629e8-af88-43c5-88e3-d8419eb1fca1 Id. de correlación: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Marca de tiempo: 2015-12-15 21:09:31Z.</span><span class="sxs-lookup"><span data-stu-id="309d4-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="309d4-212">En la tabla siguiente se muestran los tiempos de expiración de los distintos tipos de cuentas de usuario:</span><span class="sxs-lookup"><span data-stu-id="309d4-212">The following table shows the expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="309d4-213">Tipo de usuario</span><span class="sxs-lookup"><span data-stu-id="309d4-213">User type</span></span> | <span data-ttu-id="309d4-214">Expira después de</span><span class="sxs-lookup"><span data-stu-id="309d4-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="309d4-215">Cuentas de usuario *no* administradas por Azure Active Directory (por ejemplo, @hotmail.com o @live.com)</span><span class="sxs-lookup"><span data-stu-id="309d4-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="309d4-216">12 horas</span><span class="sxs-lookup"><span data-stu-id="309d4-216">12 hours</span></span> |
| <span data-ttu-id="309d4-217">Cuentas de usuario administradas por Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="309d4-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="309d4-218">14 días después de la ejecución del último segmento.</span><span class="sxs-lookup"><span data-stu-id="309d4-218">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="309d4-219">90 días, si un segmento basado en un servicio vinculado basado en OAuth se ejecuta al menos una vez cada 14 días.</span><span class="sxs-lookup"><span data-stu-id="309d4-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="309d4-220">Si cambia la contraseña antes de la hora de expiración del token, el token expira inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="309d4-220">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="309d4-221">Verá el mensaje mencionado anteriormente en esta sección.</span><span class="sxs-lookup"><span data-stu-id="309d4-221">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="309d4-222">Puede volver a autorizar la cuenta mediante el botón **Autorizar** cuando expire el token para volver a implementar el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="309d4-222">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="309d4-223">También puede generar valores para las propiedades **sessionId** y **authorization** mediante programación por medio del código siguiente:</span><span class="sxs-lookup"><span data-stu-id="309d4-223">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="309d4-224">Para más información sobre las clases de Data Factory que se usan en el código, consulte los temas [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) y [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx).</span><span class="sxs-lookup"><span data-stu-id="309d4-224">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="309d4-225">Agregue una referencia a la versión `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para la clase `WindowsFormsWebAuthenticationDialog` usada en el código.</span><span class="sxs-lookup"><span data-stu-id="309d4-225">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="309d4-226">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="309d4-226">Dataset properties</span></span>
<span data-ttu-id="309d4-227">Para especificar un conjunto de datos para representar datos de entrada en Data Lake Store, establezca la propiedad **type** del conjunto de datos en **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="309d4-227">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="309d4-228">Establezca la propiedad **linkedServiceName** del conjunto de datos en el nombre del servicio vinculado Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-228">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="309d4-229">Para ver una lista completa de las secciones y propiedades JSON disponibles para definir conjuntos de datos, consulte el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-229">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="309d4-230">Las secciones de un conjunto de datos de JSON, como **structure**, **availability** y **policy**, son similares para todos los tipos de datos (base de datos SQL de Azure, blob de Azure y tabla de Azure, por ejemplo).</span><span class="sxs-lookup"><span data-stu-id="309d4-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="309d4-231">La sección **typeProperties** es diferente para cada tipo de conjunto de datos y proporciona información como la ubicación y el formato de los datos del almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-231">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="309d4-232">La sección **typeProperties** de un conjunto de datos de tipo **AzureDataLakeStore** contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="309d4-232">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="309d4-233">Propiedad</span><span class="sxs-lookup"><span data-stu-id="309d4-233">Property</span></span> | <span data-ttu-id="309d4-234">Descripción</span><span class="sxs-lookup"><span data-stu-id="309d4-234">Description</span></span> | <span data-ttu-id="309d4-235">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="309d4-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="309d4-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="309d4-236">**folderPath**</span></span> |<span data-ttu-id="309d4-237">Ruta de acceso al contenedor y la carpeta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-237">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="309d4-238">Sí</span><span class="sxs-lookup"><span data-stu-id="309d4-238">Yes</span></span> |
| <span data-ttu-id="309d4-239">**fileName**</span><span class="sxs-lookup"><span data-stu-id="309d4-239">**fileName**</span></span> |<span data-ttu-id="309d4-240">Nombre del archivo en Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-240">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="309d4-241">La propiedad **fileName** es opcional y distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="309d4-241">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="309d4-242">Si especifica **fileName**, la actividad (incluida la copia) funciona en el archivo específico.</span><span class="sxs-lookup"><span data-stu-id="309d4-242">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="309d4-243">Cuando no se especifica **fileName**, la copia incluye todos los archivos de **folderPath** en el conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="309d4-243">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="309d4-244">Cuando **fileName** no se especifica para un conjunto de datos de salida y **preserveHierarchy** no se especifica en el receptor de actividad, el nombre del archivo generado está en formato de datos._Guid_.txt'.</span><span class="sxs-lookup"><span data-stu-id="309d4-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="309d4-245">Por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="309d4-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="309d4-246">No</span><span class="sxs-lookup"><span data-stu-id="309d4-246">No</span></span> |
| <span data-ttu-id="309d4-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="309d4-247">**partitionedBy**</span></span> |<span data-ttu-id="309d4-248">La propiedad **partitionedBy** es opcional.</span><span class="sxs-lookup"><span data-stu-id="309d4-248">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="309d4-249">Puede usarla para especificar una ruta de acceso dinámica y un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="309d4-249">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="309d4-250">Por ejemplo, se puede parametrizar **folderPath** por cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="309d4-251">Para más información y ver algunos ejemplos, consulte [La propiedad partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="309d4-251">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="309d4-252">No</span><span class="sxs-lookup"><span data-stu-id="309d4-252">No</span></span> |
| <span data-ttu-id="309d4-253">**format**</span><span class="sxs-lookup"><span data-stu-id="309d4-253">**format**</span></span> | <span data-ttu-id="309d4-254">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="309d4-254">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="309d4-255">Establezca la propiedad **type** en **format** en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="309d4-255">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="309d4-256">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format) del artículo [Formatos de compresión de archivos admitidos por Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-256">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="309d4-257">Si desea copiar los archivos tal cual entre los almacenes basados en archivos (copia binaria), omita la sección `format` en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="309d4-257">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="309d4-258">No</span><span class="sxs-lookup"><span data-stu-id="309d4-258">No</span></span> |
| <span data-ttu-id="309d4-259">**compression**</span><span class="sxs-lookup"><span data-stu-id="309d4-259">**compression**</span></span> | <span data-ttu-id="309d4-260">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="309d4-260">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="309d4-261">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="309d4-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="309d4-262">Niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="309d4-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="309d4-263">Para más información, consulte el artículo sobre [Formatos de compresión de archivos admitidos por Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="309d4-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="309d4-264">No</span><span class="sxs-lookup"><span data-stu-id="309d4-264">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="309d4-265">La propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="309d4-265">The partitionedBy property</span></span>
<span data-ttu-id="309d4-266">Puede especificar las propiedades dinámicas **folderPath** y **fileName** para los datos de series temporales con la propiedad **partitionedBy**, funciones de Data Factory y variables del sistema.</span><span class="sxs-lookup"><span data-stu-id="309d4-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="309d4-267">Para más información, consulte el artículo [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-267">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="309d4-268">En el ejemplo siguiente, `{Slice}` se reemplaza por el valor de la variable del sistema de Data Factory `SliceStart` en el formato especificado (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="309d4-268">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="309d4-269">El nombre `SliceStart` hace referencia a la hora de inicio del segmento.</span><span class="sxs-lookup"><span data-stu-id="309d4-269">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="309d4-270">La propiedad `folderPath` es diferente para cada segmento, como en `wikidatagateway/wikisampledataout/2014100103` o `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="309d4-270">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="309d4-271">En el ejemplo siguiente, el año, el mes, el día y la hora de `SliceStart` se extraen en variables independientes que usan las propiedades `folderPath` y `fileName`:</span><span class="sxs-lookup"><span data-stu-id="309d4-271">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="309d4-272">Para más información sobre los conjuntos de datos, la programación y los segmentos de serie temporal, consulte [Conjuntos de datos en Azure Data Factory](data-factory-create-datasets.md) y [Programación y ejecución de Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-272">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="309d4-273">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="309d4-273">Copy activity properties</span></span>
<span data-ttu-id="309d4-274">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-274">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="309d4-275">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="309d4-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="309d4-276">Las propiedades disponibles en la sección **typeProperties** de una actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="309d4-276">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="309d4-277">En una actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="309d4-277">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="309d4-278">**AzureDataLakeStoreSource** admite la siguiente propiedad en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="309d4-278">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="309d4-279">Propiedad</span><span class="sxs-lookup"><span data-stu-id="309d4-279">Property</span></span> | <span data-ttu-id="309d4-280">Descripción</span><span class="sxs-lookup"><span data-stu-id="309d4-280">Description</span></span> | <span data-ttu-id="309d4-281">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="309d4-281">Allowed values</span></span> | <span data-ttu-id="309d4-282">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="309d4-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="309d4-283">**recursive**</span><span class="sxs-lookup"><span data-stu-id="309d4-283">**recursive**</span></span> |<span data-ttu-id="309d4-284">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="309d4-284">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="309d4-285">True (valor predeterminado), False</span><span class="sxs-lookup"><span data-stu-id="309d4-285">True (default value), False</span></span> |<span data-ttu-id="309d4-286">No</span><span class="sxs-lookup"><span data-stu-id="309d4-286">No</span></span> |


<span data-ttu-id="309d4-287">**AzureDataLakeStoreSink** admite las siguientes propiedades en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="309d4-287">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="309d4-288">Propiedad</span><span class="sxs-lookup"><span data-stu-id="309d4-288">Property</span></span> | <span data-ttu-id="309d4-289">Descripción</span><span class="sxs-lookup"><span data-stu-id="309d4-289">Description</span></span> | <span data-ttu-id="309d4-290">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="309d4-290">Allowed values</span></span> | <span data-ttu-id="309d4-291">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="309d4-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="309d4-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="309d4-292">**copyBehavior**</span></span> |<span data-ttu-id="309d4-293">Especifica el comportamiento de copia.</span><span class="sxs-lookup"><span data-stu-id="309d4-293">Specifies the copy behavior.</span></span> |<span data-ttu-id="309d4-294"><b>PreserveHierarchy</b>: conserva la jerarquía de archivos en la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="309d4-294"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="309d4-295">La ruta de acceso relativa del archivo de origen que apunta a la carpeta de origen es idéntica a la ruta de acceso relativa del archivo de destino que apunta a la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="309d4-295">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="309d4-296"><b>FlattenHierarchy</b>: todos los archivos de la carpeta de origen se crean en el primer nivel de la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="309d4-296"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="309d4-297">Los archivos de destino se crean con nombres generados automáticamente.</span><span class="sxs-lookup"><span data-stu-id="309d4-297">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="309d4-298"><b>MergeFiles</b>: combina todos los archivos de la carpeta de origen en un archivo.</span><span class="sxs-lookup"><span data-stu-id="309d4-298"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="309d4-299">Si se especifica el nombre del blob o del archivo, el nombre de archivo combinado es el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="309d4-299">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="309d4-300">En caso contrario, el nombre de archivo se genera automáticamente.</span><span class="sxs-lookup"><span data-stu-id="309d4-300">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="309d4-301">No</span><span class="sxs-lookup"><span data-stu-id="309d4-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="309d4-302">Ejemplos de recursive y copyBehavior</span><span class="sxs-lookup"><span data-stu-id="309d4-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="309d4-303">En esta sección se describe el comportamiento resultante de la operación de copia para diferentes combinaciones de valores recursive y copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="309d4-303">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="309d4-304">recursive</span><span class="sxs-lookup"><span data-stu-id="309d4-304">recursive</span></span> | <span data-ttu-id="309d4-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="309d4-305">copyBehavior</span></span> | <span data-ttu-id="309d4-306">Comportamiento resultante</span><span class="sxs-lookup"><span data-stu-id="309d4-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="309d4-307">true</span><span class="sxs-lookup"><span data-stu-id="309d4-307">true</span></span> |<span data-ttu-id="309d4-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="309d4-308">preserveHierarchy</span></span> |<span data-ttu-id="309d4-309">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="309d4-309">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="309d4-310">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-310">Folder1</span></span><br/><span data-ttu-id="309d4-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="309d4-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="309d4-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="309d4-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="309d4-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="309d4-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="309d4-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="309d4-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="309d4-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="309d4-317">la carpeta de destino Folder1 se crea con la misma estructura que la de origen</span><span class="sxs-lookup"><span data-stu-id="309d4-317">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="309d4-318">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-318">Folder1</span></span><br/><span data-ttu-id="309d4-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="309d4-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="309d4-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="309d4-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="309d4-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="309d4-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="309d4-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="309d4-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="309d4-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="309d4-325">true</span><span class="sxs-lookup"><span data-stu-id="309d4-325">true</span></span> |<span data-ttu-id="309d4-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="309d4-326">flattenHierarchy</span></span> |<span data-ttu-id="309d4-327">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="309d4-327">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="309d4-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-328">Folder1</span></span><br/><span data-ttu-id="309d4-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="309d4-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="309d4-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="309d4-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="309d4-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="309d4-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="309d4-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="309d4-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="309d4-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="309d4-335">la carpeta de destino Folder1 se crea con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="309d4-335">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="309d4-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-336">Folder1</span></span><br/><span data-ttu-id="309d4-337">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="309d4-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="309d4-338">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="309d4-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="309d4-339">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File3</span><span class="sxs-lookup"><span data-stu-id="309d4-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="309d4-340">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File4</span><span class="sxs-lookup"><span data-stu-id="309d4-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="309d4-341">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File5</span><span class="sxs-lookup"><span data-stu-id="309d4-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="309d4-342">true</span><span class="sxs-lookup"><span data-stu-id="309d4-342">true</span></span> |<span data-ttu-id="309d4-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="309d4-343">mergeFiles</span></span> |<span data-ttu-id="309d4-344">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="309d4-344">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="309d4-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-345">Folder1</span></span><br/><span data-ttu-id="309d4-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="309d4-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="309d4-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="309d4-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="309d4-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="309d4-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="309d4-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="309d4-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="309d4-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="309d4-352">la carpeta de destino Folder1 se crea con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="309d4-352">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="309d4-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-353">Folder1</span></span><br/><span data-ttu-id="309d4-354">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 + File3 + File4 + File 5 se combina en un archivo con un nombre de archivo generado automáticamente</span><span class="sxs-lookup"><span data-stu-id="309d4-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="309d4-355">false</span><span class="sxs-lookup"><span data-stu-id="309d4-355">false</span></span> |<span data-ttu-id="309d4-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="309d4-356">preserveHierarchy</span></span> |<span data-ttu-id="309d4-357">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="309d4-357">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="309d4-358">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-358">Folder1</span></span><br/><span data-ttu-id="309d4-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="309d4-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="309d4-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="309d4-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="309d4-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="309d4-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="309d4-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="309d4-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="309d4-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="309d4-365">la carpeta de destino Folder1 se crea con la estructura siguiente</span><span class="sxs-lookup"><span data-stu-id="309d4-365">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="309d4-366">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-366">Folder1</span></span><br/><span data-ttu-id="309d4-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="309d4-369">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="309d4-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="309d4-370">false</span><span class="sxs-lookup"><span data-stu-id="309d4-370">false</span></span> |<span data-ttu-id="309d4-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="309d4-371">flattenHierarchy</span></span> |<span data-ttu-id="309d4-372">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="309d4-372">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="309d4-373">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-373">Folder1</span></span><br/><span data-ttu-id="309d4-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="309d4-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="309d4-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="309d4-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="309d4-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="309d4-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="309d4-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="309d4-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="309d4-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="309d4-380">la carpeta de destino Folder1 se crea con la estructura siguiente</span><span class="sxs-lookup"><span data-stu-id="309d4-380">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="309d4-381">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-381">Folder1</span></span><br/><span data-ttu-id="309d4-382">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="309d4-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="309d4-383">&nbsp;&nbsp;&nbsp;&nbsp;Nombre de archivo generado automáticamente para File2</span><span class="sxs-lookup"><span data-stu-id="309d4-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="309d4-384">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="309d4-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="309d4-385">false</span><span class="sxs-lookup"><span data-stu-id="309d4-385">false</span></span> |<span data-ttu-id="309d4-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="309d4-386">mergeFiles</span></span> |<span data-ttu-id="309d4-387">Si la carpeta de origen Folder1 tiene esta estructura: </span><span class="sxs-lookup"><span data-stu-id="309d4-387">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="309d4-388">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-388">Folder1</span></span><br/><span data-ttu-id="309d4-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="309d4-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="309d4-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="309d4-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="309d4-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="309d4-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="309d4-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="309d4-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="309d4-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="309d4-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="309d4-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="309d4-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="309d4-395">la carpeta de destino Folder1 se crea con la estructura siguiente</span><span class="sxs-lookup"><span data-stu-id="309d4-395">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="309d4-396">Folder1</span><span class="sxs-lookup"><span data-stu-id="309d4-396">Folder1</span></span><br/><span data-ttu-id="309d4-397">&nbsp;&nbsp;&nbsp;&nbsp;El contenido de File1 + File2 se combina en un archivo con un nombre de archivo generado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="309d4-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="309d4-398">Nombre de archivo generado automáticamente para File1</span><span class="sxs-lookup"><span data-stu-id="309d4-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="309d4-399">No se selecciona la subcarpeta Subfolder1, que contiene los archivos File3, File4 y File5.</span><span class="sxs-lookup"><span data-stu-id="309d4-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="309d4-400">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="309d4-400">Supported file and compression formats</span></span>
<span data-ttu-id="309d4-401">Para más información, consulte el artículo [Formatos de compresión de archivos admitidos por Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-401">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="309d4-402">Ejemplos de JSON para copiar datos hacia y desde Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="309d4-402">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="309d4-403">En los ejemplos siguientes se proporcionan definiciones de JSON de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="309d4-403">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="309d4-404">Puede usar estas definiciones de ejemplo para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-404">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="309d4-405">En los ejemplos se muestra cómo copiar datos entre Azure Data Lake Store y Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="309d4-405">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="309d4-406">En cambio, los datos pueden copiarse _directamente_ desde cualquiera de los orígenes a cualquiera de los receptores admitidos.</span><span class="sxs-lookup"><span data-stu-id="309d4-406">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="309d4-407">Para más información, consulte la sección "Almacenes de datos y formatos que se admiten" del artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-407">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="309d4-408">Ejemplo: copia de datos desde Azure Blob Storage hacia Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="309d4-408">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="309d4-409">El código de ejemplo de esta sección muestra:</span><span class="sxs-lookup"><span data-stu-id="309d4-409">The example code in this section shows:</span></span>

* <span data-ttu-id="309d4-410">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="309d4-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="309d4-411">Un servicio vinculado de tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="309d4-412">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="309d4-413">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="309d4-414">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) y [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="309d4-415">En los ejemplos se muestra cómo los datos de serie temporal de Azure Blob Storage se copian en Data Lake Store cada hora.</span><span class="sxs-lookup"><span data-stu-id="309d4-415">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="309d4-416">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="309d4-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="309d4-417">**Servicio vinculado de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="309d4-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="309d4-418">Para información sobre los detalles de configuración, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-418">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="309d4-419">**Conjunto de datos de entrada de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="309d4-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="309d4-420">En el siguiente ejemplo, los datos se seleccionan de un nuevo blob cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="309d4-420">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="309d4-421">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="309d4-421">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="309d4-422">La ruta de acceso a la carpeta usa la parte de año, mes y día de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="309d4-422">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="309d4-423">El nombre de archivo usa la parte de hora de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="309d4-423">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="309d4-424">El valor `"external": true` informa al servicio Data Factory de que la tabla es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="309d4-424">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="309d4-425">**Conjunto de datos de salida de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="309d4-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="309d4-426">En el siguiente ejemplo se copian los datos en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="309d4-426">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="309d4-427">Los nuevos datos se copian en Data Lake Store cada hora.</span><span class="sxs-lookup"><span data-stu-id="309d4-427">New data is copied to Data Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="309d4-428">**Actividad de copia en una canalización con un origen de blob y el receptor de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="309d4-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="309d4-429">En el ejemplo siguiente, la canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="309d4-429">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="309d4-430">La actividad de copia está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="309d4-430">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="309d4-431">En la definición de JSON de la canalización, el tipo `source` está establecido en `BlobSource` y el tipo `sink` está establecido en `AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="309d4-431">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="309d4-432">Ejemplo: copia de datos desde Azure Data Lake Store hacia un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="309d4-432">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="309d4-433">El código de ejemplo de esta sección muestra:</span><span class="sxs-lookup"><span data-stu-id="309d4-433">The example code in this section shows:</span></span>

* <span data-ttu-id="309d4-434">Un servicio vinculado de tipo [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="309d4-435">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="309d4-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="309d4-436">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="309d4-437">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="309d4-438">Una [canalización](data-factory-create-pipelines.md) con una actividad de copia que usa [AzureDataLakeStoreSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="309d4-439">El código copia los datos de series temporales desde Data Lake Store hacia un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="309d4-439">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="309d4-440">**Servicio vinculado de Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="309d4-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="309d4-441">Para información sobre los detalles de configuración, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="309d4-441">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="309d4-442">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="309d4-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="309d4-443">**Conjunto de datos de entrada de Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="309d4-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="309d4-444">Si se establece `"external"` en `true`, se informa al servicio Data Factory de que la tabla es externa a la factoría de datos y no la produce ninguna actividad de dicha factoría.</span><span class="sxs-lookup"><span data-stu-id="309d4-444">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
<span data-ttu-id="309d4-445">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="309d4-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="309d4-446">En el ejemplo siguiente, los datos se escriben en un nuevo blob cada hora (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="309d4-446">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="309d4-447">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="309d4-447">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="309d4-448">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="309d4-448">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="309d4-449">**Una actividad de copia en una canalización con un origen de Azure Data Lake Store y un receptor de blob**</span><span class="sxs-lookup"><span data-stu-id="309d4-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="309d4-450">En el ejemplo siguiente, la canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida.</span><span class="sxs-lookup"><span data-stu-id="309d4-450">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="309d4-451">La actividad de copia está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="309d4-451">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="309d4-452">En la definición de JSON de la canalización, el tipo `source` está establecido en `AzureDataLakeStoreSource` y el tipo `sink` está establecido en `BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="309d4-452">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

<span data-ttu-id="309d4-453">En la definición de la actividad de copia, también puede asignar columnas del conjunto de datos de origen a columnas del conjunto de datos receptor.</span><span class="sxs-lookup"><span data-stu-id="309d4-453">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="309d4-454">Para más información, consulte [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Asignación de columnas de conjunto de datos de Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="309d4-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="309d4-455">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="309d4-455">Performance and tuning</span></span>
<span data-ttu-id="309d4-456">Para conocer los factores que afectan al rendimiento de la actividad de copia y cómo optimizarla, consulte el artículo [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="309d4-456">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
